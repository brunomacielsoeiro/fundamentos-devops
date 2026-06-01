# 🔄 CI/CD — Integração e Entrega Contínua

## 1. Integração Contínua (CI)

### O que é?

CI é a prática de **integrar código frequentemente** em um repositório compartilhado, com **testes automáticos** executados a cada integração.

### Fluxo

```
Developer → git push → Pipeline CI → Build → Testes → ✅ ou ❌
                                                         │
                                              ✅ Código integrado
                                              ❌ Notifica dev (corrigir)
```

### Princípios

| Princípio | Descrição |
|-----------|-----------|
| Commits frequentes | Integrar pelo menos 1x por dia |
| Build automatizado | Cada push dispara build |
| Testes automatizados | Unitários, integração, lint |
| Feedback rápido | Dev sabe em minutos se quebrou |
| Branch curta | Merge rápido para main |
| Fix imediato | Se quebrou, prioridade é corrigir |

### O que roda no CI?

```
┌─────────────────────────────────────────────────┐
│                 PIPELINE CI                       │
│                                                  │
│  1. Checkout ─► 2. Install ─► 3. Lint           │
│                                  │               │
│                                  ▼               │
│  6. Report ◄── 5. Coverage ◄── 4. Tests         │
│                                                  │
└─────────────────────────────────────────────────┘
```

| Etapa | Ferramenta | Propósito |
|-------|-----------|-----------|
| Lint | ESLint, Flake8 | Qualidade de código |
| Unit Tests | Jest, pytest | Lógica funciona |
| Integration Tests | Supertest, Testcontainers | Componentes integram |
| Security Scan | Snyk, Trivy | Vulnerabilidades |
| Coverage | Istanbul, Coverage.py | % de código testado |

---

## 2. Entrega Contínua (CD - Continuous Delivery)

### O que é?

CD garante que o código está **sempre pronto para deploy** em produção. O deploy pode ser manual (aprovação), mas o processo até lá é 100% automatizado.

### Fluxo

```
CI (build + test) → Staging Deploy → Testes de Aceitação → ✅ Pronto para PROD
                                                                    │
                                                          Aprovação manual
                                                                    │
                                                                    ▼
                                                              Deploy PROD
```

---

## 3. Deploy Contínuo (Continuous Deployment)

### Diferença de Continuous Delivery

| Aspecto | Continuous Delivery | Continuous Deployment |
|---------|--------------------|--------------------|
| Deploy em PROD | Manual (aprovação) | Automático |
| Risco | Menor (gate humano) | Maior (precisa de testes fortes) |
| Velocidade | Alta | Máxima |
| Requisito | Testes bons | Testes excelentes + feature flags |

```
Continuous Delivery:    CI → Staging → [Aprovação] → PROD
Continuous Deployment:  CI → Staging → Testes → PROD (automático)
```

---

## 4. Estratégias de Deploy

| Estratégia | Como funciona | Risco | Rollback |
|-----------|--------------|-------|----------|
| **Recreate** | Derruba tudo, sobe novo | 🔴 Downtime | Lento |
| **Rolling** | Atualiza instâncias gradualmente | 🟡 Médio | Médio |
| **Blue/Green** | Dois ambientes, troca DNS | 🟢 Zero downtime | Instantâneo |
| **Canary** | % pequeno recebe a nova versão | 🟢 Mínimo | Instantâneo |
| **Feature Flags** | Toggle no código | 🟢 Mínimo | Instantâneo |

### Blue/Green Deploy

```
ANTES:                          DEPOIS:
┌──────────┐                    ┌──────────┐
│  BLUE    │ ◄── DNS            │  BLUE    │ (standby)
│  (v1.0)  │                    │  (v1.0)  │
└──────────┘                    └──────────┘

┌──────────┐                    ┌──────────┐
│  GREEN   │ (standby)          │  GREEN   │ ◄── DNS
│  (v2.0)  │                    │  (v2.0)  │
└──────────┘                    └──────────┘
```

### Canary Deploy

```
100% tráfego → v1.0

Deploy canary:
├── 95% tráfego → v1.0
└──  5% tráfego → v2.0  ← Monitorar métricas

Se OK:
├── 50% tráfego → v1.0
└── 50% tráfego → v2.0

Se OK:
└── 100% tráfego → v2.0 ✅
```

---

## 5. Ambientes

| Ambiente | Propósito | Deploy |
|----------|-----------|--------|
| **DEV** | Desenvolvimento e testes locais | A cada push |
| **STAGING** | Réplica de produção para QA | Automático (CI) |
| **PROD** | Usuários finais | Manual ou automático |

```
DEV → STAGING → PROD
 │       │        │
 │       │        └── Aprovação manual (ou automático)
 │       └── Testes de aceitação passam
 └── Push na branch
```

---

## 6. Benefícios do CI/CD

| Benefício | Sem CI/CD | Com CI/CD |
|-----------|----------|-----------|
| Tempo de entrega | Semanas | Horas/minutos |
| Bugs em produção | Descobertos tarde | Pegos no pipeline |
| Deploy | Manual, arriscado | Automatizado, seguro |
| Rollback | Horas | Minutos |
| Confiança | Baixa ("será que vai quebrar?") | Alta (testes passaram) |

---

## Resumo

```
┌─────────────────────────────────────────────────────────────┐
│                      CI/CD                                    │
│                                                              │
│  CI (Integração)       CD (Entrega)       CD (Deploy)        │
│  ────────────────      ─────────────      ───────────        │
│  • Build automático    • Staging auto     • PROD automático  │
│  • Testes a cada push  • Pronto p/ PROD   • Sem gate humano  │
│  • Feedback rápido     • Gate manual      • Feature flags    │
│  • Fix imediato        • Testes aceitação • Canary/Blue-Green│
│                                                              │
└─────────────────────────────────────────────────────────────┘
```
