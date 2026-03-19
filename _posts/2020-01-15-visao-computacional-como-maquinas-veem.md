---
layout: post
title: "Visão Computacional: Como Máquinas Veem"
description: "Entenda como algoritmos ensinam computadores a interpretar e entender imagens."
date: 2020-01-15
---

**Visão computacional** é o campo da inteligência artificial que permite aos computadores "verem" e interpretarem informações visuais — imagens e vídeos. De reconhecimento facial em smartphones a diagnósticos médicos assistidos por IA, visão computacional está transformando industries.

## O que é Visão Computacional?

Visão computacional dá aos computadores a ability to extract meaningful information from images and videos — mimicking and sometimes surpassing human visual perception.

### Diferença entre Visão Humana e Computacional

**Olhos humanos:**
- 100+ milhões de fotorreceptores
- Processamento paralelo massivo
- Anos de "treino" via evolution
- Intuição e context built-in

**Computadores:**
- Pixels (números em matrizes)
- Processamento sequencial (paralelo via GPUs)
- Precisam de explicit training
- Context precisa ser explicitly learned

## Como Computadores "Veem" Imagens?

### Representação Digital

Uma imagem é uma matrix de pixels:

```
[255, 128, 64, 32]
[128, 255, 64, 128]
[64, 64, 255, 64]
[32, 128, 64, 255]
```

Cada valor é typically 0-255 (intensidade de cor). Para color images, três channels (RGB) create a 3D tensor.

### Composição de uma Imagem Digital

```
Resolução: 1920 × 1080 pixels
Canais: RGB (3 canais)
Profundidade: 8 bits por canal
Tamanho: 1920 × 1080 × 3 bytes ≈ 6.2 MB
```

## Tarefas Fundamentais

### Classificação de Imagens

Determinar qual categoria/object a imagem contém:

```
Imagem → [Gato: 0.92, Cachorro: 0.05, Avião: 0.01, ...]
```

AlexNet (2012) revolucionou esta área usando deep learning.

### Localização (Object Detection)

Encontrar onde objects estão na imagem:

```
Imagem → [Gato em (x1,y1,x2,y2), Cachorro em (x1,y1,x2,y2)]
```

Algoritmos: YOLO, R-CNN, SSD.

### Segmentação

Classificar cada pixel da imagem:

- **Segmentação semântica**: Cada pixel é classificado (carro, estrada, céu)
- **Segmentação de instâncias**: Diferencia objects individuais da mesma classe

### Reconhecimento Facial

Identificar whose face está na imagem:

- Detectar face (onde)
- Identificar pessoa (quem)

Aplicações: desbloqueio de celular, tagging em fotos, segurança.

## Redes Neurais para Visão

### CNNs (Convolutional Neural Networks)

Arquitetura especializada para dados espaciais:

**Camadas convolucionais**:
- Aplicam filtros (kernels) que detectam features
- Filtros aprendem a detectar bordas, texturas, formas
- Hierarquia de features: bordas → texturas → objetos

**Pooling**:
- Reduz dimensionalidade
- Mantém informações importantes
- Translation invariance

**Fully Connected Layers**:
- Classificam based nas features extraídas

### Arquiteturas Importantes

**LeNet (1998)**: Pioneira, handwritten digit recognition
**AlexNet (2012)**: Revolução deep learning em visão
**VGG (2014)**: Simplicidade e profundidade
**ResNet (2015)**: Skip connections, enable training of very deep networks
**EfficientNet (2019)**: Balance accuracy e efficiency

### Transfer Learning em Visão

Semelhante a NLP, transfer learning é crucial:

1. CNN pré-treinada em ImageNet (14 milhões de imagens)
2. Fine-tune em dataset específico (ex: radiografias)
3. Bom resultado com poucos dados

## Aplicações Práticas

### Carros Autônomos

```
Câmeras → Detecção de pedestres → Detecção de faixas → Sistema de decisão
Radar/Lidar → Mapeamento 3D → Localização → Planejamento de rota
```

Múltiplas câmeras e sensores se complementam.

### Medicina

- Deteção de tumores em mammografias
- Análise de radiografias para COVID-19
- Segmentação de tumores em MRI
- Triagem de retinopatia diabética

### Agricultura

- Deteção de doenças em plantas
- Monitoramento de safras por drone
- Robôs de colheita automatizada

### Retail

- Cashier-less stores (Amazon Go)
- Análise de movimento de clientes
- Inventory management automatizado

### Segurança

- Reconhecimento facial em massa (controverso)
- Deteção de comportamentos suspeitos
- Leitura automática de placas

## Desafios

### Variação

- Iluminação diferente
- Ângulos variados
- Oclusões parciais
- Different scales

### Overfitting

CNNs podem memorize em vez de generalize. Data augmentation helps.

### Adversarial Examples

Padrões imperceptíveis para humanos que enganam classifiers completely:

```
Imagem de panda → panda com 99% confiança
+ ruído adversarial几乎 imperceptível →
→ gibão com 99% confiança
```

### Interpretabilidade

É difícil saber se CNN está "olhando para as coisas certas".

## Tendências Atuais

### Self-Supervised Learning

Aprender representations without labels:
- SimCLR, MoCo, BYOL

### Vision Transformers (ViT)

Aplicar arquitetura Transformer (revolucionou NLP) a imagens.

### Multimodal Learning

Combinar visão com linguagem:
- CLIP: aprender image-text pairs
- Visual Question Answering
- Image captioning

---

**Série: Redes Neurais**
1. [Redes Neurais Artificiais: Conceitos]({{ site.baseurl }}/redes-neurais-artificiais-conceitos)
2. [Deep Learning: Uma Introdução]({{ site.baseurl }}/deep-learning-uma-introducao)
3. [Processamento de Linguagem Natural]({{ site.baseurl }}/processamento-de-linguagem-natural)
4. [Visão Computacional: Como Máquinas Veem]({{ site.baseurl }}/visao-computacional-como-maquinas-veem) ← *você está aqui*

## Leia Mais

- Goodfellow, I., Bengio, Y. & Courville, A. *Deep Learning*. MIT Press, 2016.
- Szeliski, R. *Computer Vision: Algorithms and Applications*. 2nd Ed. Springer, 2022.
- Krizhevsky, A., Sutskever, I. & Hinton, G. "ImageNet Classification with Deep CNNs". *NeurIPS*, 2012.
- He, K. et al. "Deep Residual Learning for Image Recognition". *CVPR*, 2016.
