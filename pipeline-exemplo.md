# 🚀 Pipeline Exemplo — GitHub Actions

## 1. Pipeline Básico (CI)

```yaml
name: CI Pipeline

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout do código
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Instalar dependências
        run: npm ci

      - name: Lint
        run: npm run lint

      - name: Testes unitários
        run: npm test

      - name: Build
        run: npm run build
```

### O que cada etapa faz

| Etapa | Propósito |
|-------|-----------|
| `checkout` | Baixa o código do repositório |
| `setup-node` | Instala Node.js com cache |
| `npm ci` | Instala dependências (lock file) |
| `npm run lint` | Verifica qualidade do código |
| `npm test` | Executa testes automatizados |
| `npm run build` | Compila a aplicação |

---

## 2. Pipeline Completo (CI + CD)

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [main]

env:
  AWS_REGION: us-east-1
  ECR_REPOSITORY: minha-app

jobs:
  # ─────────────────────────────────────────────
  # JOB 1: Build e Testes
  # ─────────────────────────────────────────────
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Instalar dependências
        run: pip install -r requirements.txt

      - name: Lint
        run: flake8 .

      - name: Testes
        run: pytest --cov=app tests/

      - name: Security scan
        run: pip install safety && safety check

  # ─────────────────────────────────────────────
  # JOB 2: Build Docker Image
  # ─────────────────────────────────────────────
  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Build Docker image
        run: docker build -t $ECR_REPOSITORY:${{ github.sha }} .

      - name: Tag como latest
        run: docker tag $ECR_REPOSITORY:${{ github.sha }} $ECR_REPOSITORY:latest

  # ─────────────────────────────────────────────
  # JOB 3: Deploy em Staging
  # ─────────────────────────────────────────────
  deploy-staging:
    needs: build
    runs-on: ubuntu-latest
    environment: staging
    steps:
      - uses: actions/checkout@v4

      - name: Deploy para Staging
        run: echo "Deploying to staging..."

      - name: Smoke tests
        run: echo "Running smoke tests against staging..."

  # ─────────────────────────────────────────────
  # JOB 4: Deploy em Produção (manual approval)
  # ─────────────────────────────────────────────
  deploy-prod:
    needs: deploy-staging
    runs-on: ubuntu-latest
    environment: production  # Requer aprovação manual
    steps:
      - uses: actions/checkout@v4

      - name: Deploy para Produção
        run: echo "Deploying to production..."

      - name: Health check
        run: echo "Verifying production health..."
```

### Fluxo visual

```
push main
    │
    ▼
┌────────┐     ┌────────┐     ┌──────────────┐     ┌──────────────┐
│  Test  │────►│ Build  │────►│Deploy Staging│────►│ Deploy Prod  │
│        │     │ Docker │     │  (auto)      │     │ (aprovação)  │
└────────┘     └────────┘     └──────────────┘     └──────────────┘
```

---

## 3. Pipeline com Terraform (IaC)

```yaml
name: Terraform CI/CD

on:
  push:
    branches: [main]
    paths: ['infra/**']
  pull_request:
    paths: ['infra/**']

jobs:
  terraform:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: infra/

    steps:
      - uses: actions/checkout@v4

      - name: Setup Terraform
        uses: hashicorp/setup-terraform@v3
        with:
          terraform_version: 1.7.0

      - name: Terraform Init
        run: terraform init

      - name: Terraform Format Check
        run: terraform fmt -check

      - name: Terraform Validate
        run: terraform validate

      - name: Terraform Plan
        run: terraform plan -out=tfplan

      # Deploy apenas na main (não em PRs)
      - name: Terraform Apply
        if: github.ref == 'refs/heads/main'
        run: terraform apply -auto-approve tfplan
```

---

## 4. Conceitos Importantes

### Triggers (`on`)

| Trigger | Quando executa |
|---------|---------------|
| `push` | Código enviado para branch |
| `pull_request` | PR aberto/atualizado |
| `schedule` | Cron (ex: diário) |
| `workflow_dispatch` | Manual (botão) |
| `release` | Release publicada |

### Environments

```yaml
environment: production  # Requer aprovação no GitHub
```

Configurar em: Settings → Environments → Add protection rules

### Secrets

```yaml
# Nunca hardcode credenciais!
- name: Login AWS
  uses: aws-actions/configure-aws-credentials@v4
  with:
    aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
    aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    aws-region: us-east-1
```

### Cache (acelerar pipeline)

```yaml
- uses: actions/cache@v4
  with:
    path: ~/.npm
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
```

---

## 5. Boas Práticas de Pipeline

| Prática | Por quê |
|---------|---------|
| Falhar rápido (lint primeiro) | Feedback em segundos |
| Cache de dependências | Pipeline mais rápido |
| Paralelizar jobs independentes | Reduz tempo total |
| Usar `needs` para dependências | Garante ordem |
| Secrets nunca no código | Segurança |
| Environments com aprovação | Gate para produção |
| Notificar em falha | Dev corrige rápido |

---

## Resumo

```
┌─────────────────────────────────────────────────────────────┐
│              GITHUB ACTIONS - ESTRUTURA                       │
│                                                              │
│  on:              → Quando executar (trigger)                │
│  jobs:            → O que executar (paralelizável)           │
│    steps:         → Como executar (sequencial)               │
│      uses:        → Action pronta (marketplace)              │
│      run:         → Comando shell                            │
│  needs:           → Dependência entre jobs                   │
│  environment:     → Gate de aprovação                        │
│  secrets:         → Credenciais seguras                      │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```
