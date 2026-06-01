# 📖 Conceitos de DevOps

## 1. O que é DevOps?

DevOps é uma **cultura e conjunto de práticas** que integra desenvolvimento (Dev) e operações (Ops), com foco em automação, colaboração e entrega contínua de software com qualidade.

### Não é apenas ferramenta

```
DevOps = Cultura + Práticas + Ferramentas
              │         │          │
              │         │          └── Docker, Terraform, Jenkins...
              │         └── CI/CD, IaC, Monitoring...
              └── Colaboração, responsabilidade compartilhada, feedback
```

---

## 2. Pilares do DevOps (CALMS)

| Pilar | Significado | Na prática |
|-------|-------------|-----------|
| **C**ulture | Cultura de colaboração | Dev e Ops trabalham juntos |
| **A**utomation | Automatizar tudo que for possível | CI/CD, IaC, testes |
| **L**ean | Eliminar desperdício | Processos enxutos, feedback rápido |
| **M**easurement | Medir tudo | Métricas, DORA, SLIs/SLOs |
| **S**haring | Compartilhar conhecimento | Documentação, post-mortems |

---

## 3. Antes vs Depois do DevOps

| Aspecto | Modelo Tradicional | DevOps |
|---------|-------------------|--------|
| Deploy | Manual, mensal | Automatizado, diário |
| Equipes | Silos separados | Colaboração contínua |
| Feedback | Semanas/meses | Minutos (CI/CD) |
| Infraestrutura | Manual (console) | Código (IaC) |
| Incidentes | Culpa individual | Post-mortem sem culpa |
| Testes | Manual, no final | Automatizado, contínuo |
| Rollback | Horas/dias | Minutos (automático) |

---

## 4. Práticas DevOps

### Integração Contínua (CI)

Desenvolvedores integram código frequentemente, com testes automáticos a cada push.

### Entrega Contínua (CD)

Código aprovado nos testes é automaticamente preparado para deploy em produção.

### Infraestrutura como Código (IaC)

Infraestrutura definida em arquivos versionados (Terraform, CloudFormation).

### Monitoramento e Observabilidade

Métricas, logs e traces coletados continuamente para detectar problemas.

### Feedback Loops

```
┌──────────┐     ┌──────────┐     ┌──────────┐
│  Código  │────►│  Deploy  │────►│ Produção │
└──────────┘     └──────────┘     └────┬─────┘
      ▲                                 │
      │         Feedback rápido         │
      └─────────────────────────────────┘
         Métricas, alertas, logs
```

---

## 5. DORA Metrics

As 4 métricas que medem a performance de equipes DevOps:

| Métrica | O que mede | Elite | Low |
|---------|-----------|-------|-----|
| **Deployment Frequency** | Frequência de deploys | Múltiplas/dia | Mensal |
| **Lead Time for Changes** | Tempo do commit ao deploy | < 1 hora | > 1 mês |
| **Change Failure Rate** | % de deploys que causam falha | < 5% | > 45% |
| **Time to Restore** | Tempo para recuperar de falha | < 1 hora | > 1 semana |

---

## 6. DevOps vs SRE vs Platform Engineering

| Aspecto | DevOps | SRE | Platform Engineering |
|---------|--------|-----|---------------------|
| Foco | Cultura + práticas | Confiabilidade | Ferramentas internas |
| Origem | Comunidade | Google | Evolução de DevOps |
| Métrica chave | DORA metrics | SLIs/SLOs/Error Budget | Developer Experience |
| Quem pratica | Todos | Time dedicado | Time de plataforma |

---

## 7. "You build it, you run it"

Princípio fundamental: quem desenvolve é responsável por operar em produção.

```
ANTES:                              DEPOIS (DevOps):
Dev → "Tá pronto, joga pra Ops"    Dev → "Eu desenvolvo, eu monitoro,
Ops → "Quebrou, culpa do Dev"              eu corrijo, eu aprendo"
```

### Benefícios

- Desenvolvedores entendem o impacto do código em produção
- Incentiva código mais resiliente e observável
- Feedback direto do ambiente real
- Menos "jogar por cima do muro"

---

## Resumo Visual

```
┌─────────────────────────────────────────────────────────────┐
│                    DevOps - CONCEITOS                         │
│                                                              │
│  CULTURA            PRÁTICAS           MÉTRICAS              │
│  ──────             ────────           ────────              │
│  • Colaboração      • CI/CD            • Deploy Frequency    │
│  • Sem silos        • IaC              • Lead Time           │
│  • Responsabilidade • Monitoring       • Change Failure Rate │
│    compartilhada    • Automation       • Time to Restore     │
│  • Feedback rápido  • Testing                                │
│  • Melhoria         • GitOps                                 │
│    contínua                                                  │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```
