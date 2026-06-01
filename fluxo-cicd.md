# 🔁 Fluxo de CI/CD — Passo a Passo

## Visão Geral

```
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│  CODE    │───►│  BUILD   │───►│  TEST    │───►│ RELEASE  │───►│  DEPLOY  │───►│ MONITOR  │
│          │    │          │    │          │    │          │    │          │    │          │
│ git push │    │ compile  │    │ unit     │    │ tag      │    │ staging  │    │ metrics  │
│          │    │ package  │    │ integr.  │    │ version  │    │ prod     │    │ logs     │
│          │    │ docker   │    │ security │    │          │    │          │    │ alerts   │
└──────────┘    └──────────┘    └──────────┘    └──────────┘    └──────────┘    └──────────┘
```

---

## Etapa 1: CODE (Desenvolvimento)

### O que acontece

1. Desenvolvedor cria branch (`feature/nova-funcionalidade`)
2. Escreve código + testes
3. Faz commit seguindo Conventional Commits
4. Abre Pull Request

### Trigger do pipeline

```
git push origin feature/login
    │
    └──► Pipeline CI é acionado automaticamente
```

---

## Etapa 2: BUILD (Construção)

### O que acontece

1. Código é baixado (checkout)
2. Dependências são instaladas
3. Aplicação é compilada/empacotada
4. Imagem Docker é construída (se aplicável)

```bash
# Exemplo de etapas de build
npm install          # Instalar dependências
npm run build        # Compilar/empacotar
docker build -t app . # Construir imagem
```

### Artefatos gerados

| Tipo | Exemplo | Destino |
|------|---------|---------|
| Binário | `app.jar`, `dist/` | Artifact storage |
| Imagem Docker | `app:1.2.3` | Container Registry |
| Package | `app-1.2.3.tgz` | npm/PyPI |

---

## Etapa 3: TEST (Testes)

### Pirâmide de testes

```
        ┌───────┐
        │  E2E  │         Poucos, lentos, caros
        ├───────┤
        │ Integ.│         Médios
        ├───────┤
        │ Unit  │         Muitos, rápidos, baratos
        └───────┘
```

### Tipos executados no pipeline

| Tipo | O que testa | Tempo | Exemplo |
|------|------------|-------|---------|
| Lint | Estilo de código | ~10s | ESLint, Flake8 |
| Unit | Funções isoladas | ~30s | Jest, pytest |
| Integration | Componentes juntos | ~2min | Testcontainers |
| Security | Vulnerabilidades | ~1min | Snyk, Trivy |
| E2E | Fluxo completo | ~5min | Cypress, Selenium |

### Gate de qualidade

```
Testes passaram?
├── ✅ SIM → Continua para Release
└── ❌ NÃO → Pipeline falha, dev é notificado
```

---

## Etapa 4: RELEASE (Versionamento)

### Semantic Versioning (SemVer)

```
MAJOR.MINOR.PATCH
  │     │     │
  │     │     └── Bug fix (compatível)
  │     └── Nova feature (compatível)
  └── Breaking change (incompatível)

Exemplos: 1.0.0 → 1.0.1 → 1.1.0 → 2.0.0
```

### O que acontece

1. Tag de versão é criada (`v1.2.3`)
2. Changelog é gerado automaticamente
3. Artefato é publicado no registry
4. Release notes são criadas no GitHub

---

## Etapa 5: DEPLOY (Entrega)

### Fluxo de promoção

```
┌──────────┐         ┌──────────────┐         ┌──────────┐
│   DEV    │ ──────► │   STAGING    │ ──────► │   PROD   │
│          │  Auto   │              │  Manual  │          │
│ Testes   │         │ Testes de    │  ou Auto │ Usuários │
│ unitários│         │ aceitação    │         │ finais   │
└──────────┘         └──────────────┘         └──────────┘
```

### Ferramentas de deploy

| Ferramenta | Tipo | Uso |
|-----------|------|-----|
| Terraform | IaC | Provisionar infra |
| ArgoCD | GitOps | Deploy em K8s |
| AWS CodeDeploy | Managed | Deploy em EC2/ECS |
| Helm | Package manager | Deploy em K8s |

---

## Etapa 6: MONITOR (Observabilidade)

### O que monitorar após deploy

| Métrica | Ferramenta | Alarme |
|---------|-----------|--------|
| Error rate | Prometheus/CloudWatch | > 1% |
| Latência P99 | Grafana | > 500ms |
| CPU/Memória | CloudWatch | > 80% |
| Disponibilidade | Uptime monitor | < 99.9% |

### Feedback loop

```
Deploy → Monitor → Alerta → Investigar → Fix → Deploy → ...
```

---

## Pipeline Completo (Diagrama)

```
┌─────────────────────────────────────────────────────────────────┐
│                    PIPELINE CI/CD COMPLETO                        │
│                                                                   │
│  ┌─────┐   ┌───────┐   ┌──────┐   ┌────────┐   ┌──────────┐   │
│  │Push │──►│ Build │──►│ Test │──►│Release │──►│  Deploy  │   │
│  └─────┘   └───────┘   └──────┘   └────────┘   └──────────┘   │
│     │          │           │           │             │           │
│     │          │           │           │             ▼           │
│     │          │           │           │      ┌──────────┐      │
│     │          │           │           │      │ Monitor  │      │
│     │          │           │           │      └────┬─────┘      │
│     │          │           │           │           │             │
│     ◄──────────┴───────────┴───────────┴───────────┘             │
│                      Feedback Loop                                │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

---

## Tempo típico de um pipeline

| Etapa | Tempo | Se falhar |
|-------|-------|-----------|
| Checkout | ~5s | Problema de rede/permissão |
| Install deps | ~30s | Dependência quebrada |
| Lint | ~10s | Código fora do padrão |
| Build | ~1min | Erro de compilação |
| Unit tests | ~30s | Lógica quebrada |
| Integration tests | ~2min | Serviço externo falhou |
| Security scan | ~1min | Vulnerabilidade encontrada |
| Deploy staging | ~2min | Infra com problema |
| E2E tests | ~5min | Fluxo quebrado |
| Deploy prod | ~2min | Rollback automático |
| **Total** | **~15min** | — |
