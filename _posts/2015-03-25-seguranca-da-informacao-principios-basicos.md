---
layout: post
title: "Segurança da Informação: Princípios Básicos"
description: "Conheça os fundamentos da segurança digital e como proteger sistemas e dados."
date: 2015-03-25
---

**Segurança da informação** protec systems, networks e dados contra access não autorizado, modification, ou destruição. Em um mundo digital, é essencial para qualquer organização.

## Pilares da Segurança (CIA Triad)

### Confidencialidade

Apenas pessoas/ sistemas autorizados podem access information.

### Integridade

Dados permanecem accurate e intactos, sem modification unauthorized.

### Disponibilidade

Sistemas e dados estão acessíveis quando needed.

## Ameaças Comuns

### Malware

- **Vírus**: Anexa-se a arquivos, replica-se
- **Worms**: Propaga-se autonomously
- **Trojans**: Disfarça-se de software legítimo
- **Ransomware**: Criptografa arquivos, exige resgate
- **Spyware**: Coleta information secretamente

### Phishing

Ataques que trick users a reveal sensitive information:

```
"E seu banco precisa verificar sua conta!"
```

### Ataques de Senha

- **Brute force**: Tenta todas combinações
- **Dictionary**: Words comuns
- **Credential stuffing**: Dados vazados de outros sites

## Autenticação e Autorização

### Autenticação

Verificar identity:

- **Algo que você sabe**: Senha, PIN
- **Algo que você tem**: Token, celular
- **Algo que você é**: Biometria (impressão, face)

### MFA (Multi-Factor Authentication)

Combinar múltiplos factors:

```
Senha (algo sabe) + Código no Celular (algo tem)
```

Dramatically aumenta segurança.

### Autorização

Depois de authenticated, o que você pode access?

```
Guest  → only public data
User   → seus próprios dados
Admin  → tudo
```

## Criptografia

Proteger dados through encoding:

### Simétrica

Mesma key para encrypt e decrypt:

```
plaintext + key → ciphertext
ciphertext + key → plaintext
```

Ex: AES, DES, 3DES

### Assimétrica

Pares de chaves diferentes:

- **Pública**: Para encryptar
- **Privada**: Para descriptografar

Ex: RSA, ECC

### Hashing

One-way function:

```
input → hash (fixed size)
```

Usado para:
- Verificar integridade
- Armazenar senhas (com salt!)

## Redes e Infraestrutura

### Firewall

Filtra tráfego based em rules:

```
Permitir entrada 80, 443
Bloquear todo resto entrada
```

### VPN (Virtual Private Network)

Cria túnel encriptado pela internet:

```
User → Internet (encrypted) → VPN Server → Rede interna
```

### IDS/IPS

- **IDS**: Detecta ataques (passivo)
- **IPS**: Previne e detecta (ativo)

## Práticas de Segurança

### Para Indivíduos

1. **Senhas fortes**: Longas, únicas, password manager
2. **MFA**: Sempre que possível
3. **Updates**: Manter software atualizado
4. **Phishing**: Desconfiar de links/attachments
5. **Backup**: Cópias regulares de dados importantes

### Para Organizações

1. **Princípio do menor privilégio**
2. **Segmentação de rede**
3. **Monitoramento contínuo**
4. **Treinamento de funcionários**
5. **Plano de resposta a incidentes**

## Ciberataques Notáveis

### WannaCry (2017)

Ransomware que affected 200,000+ computers em 150 países.

### Equifax (2017)

Data breach expôs dados de 147 milhões de pessoas.

### SolarWinds (2020)

Supply chain attack que compromised government agencies.

## Compliance e Regulamentação

### LGPD (Brasil)

Lei Geral de Proteção de Dados:

- Consentimento para coleta
- Direitos dos titulares
- Multas de até 2% do faturamento

### GDPR (Europa)

General Data Protection Regulation:

- Muito similar à LGPD
- Aplicável a empresas que processam dados de europeus

## Criptografia na Prática

### HTTPS

HTTP sobre TLS:

```
HTTP + TLS = HTTPS (encriptado)
```

### SSH

Acesso remoto seguro:

```
ssh usuario@servidor
```

### GPG

Encriptação de emails e arquivos:

```
gpg --encrypt arquivo.txt
```

---

**Série: Infraestrutura Web**
1. [Como Funciona a Internet?]({{ site.baseurl }}/como-funciona-a-internet)
2. [Redes de Computadores: Uma Introdução]({{ site.baseurl }}/redes-de-computadores-uma-introducao)
3. [Bancos de Dados: Conceitos Fundamentais]({{ site.baseurl }}/bancos-de-dados-conceitos-fundamentais)
4. [Segurança da Informação: Princípios Básicos]({{ site.baseurl }}/seguranca-da-informacao-principios-basicos) ← *você está aqui*

## Leia Mais

- Stallings, W. *Network Security Essentials*. 6th Ed. Pearson, 2017.
- Whitman, M. E. & Mattord, H. J. *Princípios de Segurança da Informação*. Cengage, 2015.
- Garcia, A. S. *Introdução à Segurança da Informação*. LTC, 2018.
- OWASP. *The Open Web Application Security Project*.
