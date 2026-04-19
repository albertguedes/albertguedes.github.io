---
layout: post
title: "Laravel Ecommerce API: Arquitetura RESTful para E-commerce"
description: "Implementação completa de uma API REST para e-commerce usando Laravel, cobrindo produtos, pedidos, autenticação e as melhores práticas de APIs Laravel."
date: 2026-04-19
tags: ["projects", "github", "php", "laravel", "rest-api", "ecommerce"]
categories: ["backend", "api", "php"]
---

O projeto **LARAVEL-ECOMMERCE-API-PROJECT** é uma implementação robusta de uma API RESTful para e-commerce usando o framework Laravel. O projeto demonstra domínio do ecossistema Laravel e habilidades em arquitetura de APIs REST.

## Arquitetura do Projeto

```
LARAVEL-ECOMMERCE-API-PROJECT/
├── app/
│   ├── Http/
│   │   ├── Controllers/     # Controladores REST
│   │   ├── Middleware/       # Auth, CORS, etc
│   │   └── Requests/         # Form Requests
│   ├── Models/               # Eloquent Models
│   └── Services/             # Lógica de negócio
├── database/
│   ├── migrations/           # Schema do banco
│   └── seeders/              # Dados iniciais
├── routes/
│   └── api.php               # Rotas da API
├── tests/                    # Feature/Unit tests
└── .env.example
```

## Models e Relacionamentos

### Model de Produto

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\HasMany;
use Illuminate\Database\Eloquent\Relations\BelongsToMany;

class Product extends Model
{
    protected $fillable = [
        'name',
        'description',
        'price',
        'stock',
        'sku',
        'category_id',
        'is_active'
    ];

    protected $casts = [
        'price' => 'decimal:2',
        'stock' => 'integer',
        'is_active' => 'boolean',
    ];

    public function category(): BelongsTo
    {
        return $this->belongsTo(Category::class);
    }

    public function orders(): BelongsToMany
    {
        return $this->belongsToMany(Order::class)
            ->withPivot('quantity', 'price_at_purchase')
            ->withTimestamps();
    }

    public function scopeActive($query)
    {
        return $query->where('is_active', true);
    }

    public function scopeInStock($query)
    {
        return $query->where('stock', '>', 0);
    }
}
```

### Model de Pedido (Order)

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsTo;
use Illuminate\Database\Eloquent\Relations\BelongsToMany;

class Order extends Model
{
    protected $fillable = [
        'user_id',
        'status',
        'total',
        'shipping_address',
        'billing_address',
        'notes'
    ];

    protected $casts = [
        'total' => 'decimal:2',
    ];

    const STATUS_PENDING = 'pending';
    const STATUS_PROCESSING = 'processing';
    const STATUS_SHIPPED = 'shipped';
    const STATUS_DELIVERED = 'delivered';
    const STATUS_CANCELLED = 'cancelled';

    public function user(): BelongsTo
    {
        return $this->belongsTo(User::class);
    }

    public function products(): BelongsToMany
    {
        return $this->belongsToMany(Product::class)
            ->withPivot('quantity', 'price_at_purchase')
            ->withTimestamps();
    }

    public function calculateTotal(): void
    {
        $this->total = $this->products->sum(function ($product) {
            return $product->pivot->quantity * $product->pivot->price_at_purchase;
        });
        $this->save();
    }
}
```

## API Controllers

### ProductController

```php
<?php

namespace App\Http\Controllers\Api;

use App\Models\Product;
use App\Http\Controllers\Controller;
use App\Http\Requests\ProductStoreRequest;
use App\Http\Requests\ProductUpdateRequest;
use Illuminate\Http\JsonResponse;

class ProductController extends Controller
{
    public function index(): JsonResponse
    {
        $products = Product::with('category')
            ->active()
            ->inStock()
            ->paginate(20);

        return response()->json([
            'success' => true,
            'data' => $products
        ]);
    }

    public function show(int $id): JsonResponse
    {
        $product = Product::with('category')->findOrFail($id);

        return response()->json([
            'success' => true,
            'data' => $product
        ]);
    }

    public function store(ProductStoreRequest $request): JsonResponse
    {
        $product = Product::create($request->validated());

        return response()->json([
            'success' => true,
            'data' => $product,
            'message' => 'Product created successfully'
        ], 201);
    }

    public function update(ProductUpdateRequest $request, int $id): JsonResponse
    {
        $product = Product::findOrFail($id);
        $product->update($request->validated());

        return response()->json([
            'success' => true,
            'data' => $product,
            'message' => 'Product updated successfully'
        ]);
    }

    public function destroy(int $id): JsonResponse
    {
        $product = Product::findOrFail($id);
        $product->delete();

        return response()->json([
            'success' => true,
            'message' => 'Product deleted successfully'
        ]);
    }
}
```

### OrderController com Lógica de Negócio

```php
<?php

namespace App\Http\Controllers\Api;

use App\Models\Order;
use App\Models\Product;
use App\Http\Controllers\Controller;
use App\Http\Requests\OrderStoreRequest;
use Illuminate\Http\JsonResponse;
use Illuminate\Support\Facades\DB;

class OrderController extends Controller
{
    public function index(): JsonResponse
    {
        $orders = Order::with(['user', 'products'])
            ->where('user_id', auth()->id())
            ->latest()
            ->paginate(20);

        return response()->json([
            'success' => true,
            'data' => $orders
        ]);
    }

    public function store(OrderStoreRequest $request): JsonResponse
    {
        $validated = $request->validated();

        $order = DB::transaction(function () use ($validated) {
            $order = Order::create([
                'user_id' => auth()->id(),
                'status' => Order::STATUS_PENDING,
                'shipping_address' => $validated['shipping_address'],
                'billing_address' => $validated['billing_address'] ?? $validated['shipping_address'],
                'notes' => $validated['notes'] ?? null,
            ]);

            foreach ($validated['items'] as $item) {
                $product = Product::findOrFail($item['product_id']);

                if ($product->stock < $item['quantity']) {
                    throw new \Exception("Insufficient stock for {$product->name}");
                }

                $order->products()->attach($product->id, [
                    'quantity' => $item['quantity'],
                    'price_at_purchase' => $product->price,
                ]);

                $product->decrement('stock', $item['quantity']);
            }

            $order->calculateTotal();

            return $order;
        });

        return response()->json([
            'success' => true,
            'data' => $order->load('products'),
            'message' => 'Order created successfully'
        ], 201);
    }

    public function show(int $id): JsonResponse
    {
        $order = Order::with(['user', 'products.category'])
            ->where('user_id', auth()->id())
            ->findOrFail($id);

        return response()->json([
            'success' => true,
            'data' => $order
        ]);
    }
}
```

## Form Requests para Validação

```php
<?php

namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;
use Illuminate\Contracts\Validation\Validator;
use Illuminate\Http\Exceptions\HttpResponseException;

class OrderStoreRequest extends FormRequest
{
    public function authorize(): bool
    {
        return true;
    }

    public function rules(): array
    {
        return [
            'shipping_address' => 'required|string|max:500',
            'billing_address' => 'nullable|string|max:500',
            'notes' => 'nullable|string|max:1000',
            'items' => 'required|array|min:1',
            'items.*.product_id' => 'required|integer|exists:products,id',
            'items.*.quantity' => 'required|integer|min:1|max:99',
        ];
    }

    public function messages(): array
    {
        return [
            'items.required' => 'At least one item is required',
            'items.*.product_id.exists' => 'One or more products do not exist',
        ];
    }

    protected function failedValidation(Validator $validator)
    {
        throw new HttpResponseException(response()->json([
            'success' => false,
            'errors' => $validator->errors()
        ], 422));
    }
}
```

## Migrations

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('products', function (Blueprint $table) {
            $table->id();
            $table->foreignId('category_id')->constrained()->onDelete('restrict');
            $table->string('name');
            $table->text('description')->nullable();
            $table->decimal('price', 10, 2);
            $table->unsignedInteger('stock')->default(0);
            $table->string('sku')->unique();
            $table->boolean('is_active')->default(true);
            $table->timestamps();

            $table->index(['is_active', 'stock']);
            $table->index('category_id');
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('products');
    }
};
```

## Routes API

```php
<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\Api\ProductController;
use App\Http\Controllers\Api\OrderController;
use App\Http\Controllers\Api\AuthController;

Route::prefix('v1')->group(function () {
    // Autenticação
    Route::post('/register', [AuthController::class, 'register']);
    Route::post('/login', [AuthController::class, 'login']);

    // Rotas protegidas
    Route::middleware('auth:sanctum')->group(function () {
        // Produtos (público para leitura, restrito para escrita)
        Route::get('/products', [ProductController::class, 'index']);
        Route::get('/products/{id}', [ProductController::class, 'show']);

        // Apenas admin
        Route::middleware('admin')->group(function () {
            Route::post('/products', [ProductController::class, 'store']);
            Route::put('/products/{id}', [ProductController::class, 'update']);
            Route::delete('/products/{id}', [ProductController::class, 'destroy']);
        });

        // Pedidos (protegidos)
        Route::get('/orders', [OrderController::class, 'index']);
        Route::post('/orders', [OrderController::class, 'store']);
        Route::get('/orders/{id}', [OrderController::class, 'show']);
    });
});
```

## Seeder para Dados de Teste

```php
<?php

namespace Database\Seeders;

use App\Models\Product;
use App\Models\Category;
use Illuminate\Database\Seeder;

class ProductSeeder extends Seeder
{
    public function run(): void
    {
        $electronics = Category::create(['name' => 'Electronics']);
        $clothing = Category::create(['name' => 'Clothing']);

        Product::create([
            'name' => 'Wireless Headphones',
            'description' => 'High-quality wireless headphones with noise cancellation',
            'price' => 199.99,
            'stock' => 50,
            'sku' => 'WH-001',
            'category_id' => $electronics->id,
        ]);

        Product::create([
            'name' => 'Cotton T-Shirt',
            'description' => 'Premium cotton t-shirt',
            'price' => 29.99,
            'stock' => 100,
            'sku' => 'TS-001',
            'category_id' => $clothing->id,
        ]);
    }
}
```

## Stack Tecnológico

| Componente | Tecnologia | Propósito |
|-----------|------------|-----------|
| Framework | Laravel 10+ | Backend framework |
| Auth | Laravel Sanctum | API authentication |
| ORM | Eloquent | Database abstraction |
| Validation | Form Requests | Input validation |
| Database | MySQL/MariaDB | Persistência |
| Testing | PHPUnit | Unit/Feature tests |

## Conceitos Demonstrados

1. **RESTful Design**: CRUD completo com verbos HTTP corretos
2. **Eloquent Relationships**: one-to-many, many-to-many com pivot tables
3. **Transactions**: Garantia de consistência em operações complexas
4. **Form Requests**: Validação declarativa e reutilizável
5. **API Resources**: Transformação consistente de dados
6. **Middleware**: Autenticação e autorização
7. **Migrations**: Versionamento de schema

## Conclusão

O **LARAVEL-ECOMMERCE-API-PROJECT** demonstra proficiência em Laravel e arquitetura de APIs RESTful. O código demonstra domínio de Eloquent, migrations, seeding, validação e organização em camadas — habilidades essenciais para aplicações enterprise em PHP.

**Repositório**: [github.com/albertguedes/LARAVEL-ECOMMERCE-API-PROJECT](https://github.com/albertguedes/LARAVEL-ECOMMERCE-API-PROJECT)
