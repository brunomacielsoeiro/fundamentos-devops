# ⚙️ Fundamentos de DevOps

> Projeto de estudos sobre cultura e práticas DevOps, abordando automação, integração contínua, entrega contínua, pipelines e ferramentas do ecossistema. Atividade acadêmica para cumprimento de horas complementares.

---

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [O que você vai aprender](#o-que-você-vai-aprender)
- [Estrutura do Repositório](#estrutura-do-repositório)
- [Ciclo DevOps](#ciclo-devops)
- [Conexão com outros projetos](#conexão-com-outros-projetos)
- [Referências](#referências)

---

## Sobre o Projeto

DevOps é a cultura que une **desenvolvimento** e **operações** para entregar software com mais velocidade, qualidade e confiabilidade. Este repositório documenta os fundamentos necessários para entender e aplicar práticas DevOps em projetos reais.

### Por que DevOps é importante?

- Reduz o tempo entre escrever código e entregar valor ao usuário
- Automatiza processos repetitivos e propensos a erro
- Melhora a colaboração entre equipes
- É requisito em praticamente toda vaga de infraestrutura e backend

---

## O que você vai aprender

| Tema | Arquivo | Descrição |
|------|---------|-----------|
| Conceitos DevOps | [conceitos-devops.md](./conceitos-devops.md) | Cultura, princípios, pilares |
| CI/CD | [cicd.md](./cicd.md) | Integração e entrega contínua |
| Fluxo CI/CD | [fluxo-cicd.md](./fluxo-cicd.md) | Pipeline passo a passo com diagrama |
| Ferramentas | [ferramentas-devops.md](./ferramentas-devops.md) | Ecossistema de ferramentas por categoria |
| Pipeline Exemplo | [pipeline-exemplo.md](./pipeline-exemplo.md) | GitHub Actions na prática |

---

## Estrutura do Repositório

```
fundamentos-devops/
├── README.md              ← Este arquivo (visão geral)
├── conceitos-devops.md    ← Cultura e princípios
├── cicd.md                ← CI/CD detalhado
├── fluxo-cicd.md          ← Fluxo com diagrama
├── ferramentas-devops.md  ← Ferramentas por categoria
├── pipeline-exemplo.md    ← Exemplo prático (GitHub Actions)
├── CONTRIBUTING.md        ← Guia de contribuição
└── LICENSE
```

---

## Ciclo DevOps

```
        ┌─────────────────────────────────────────────┐
        │              CICLO DevOps (∞)                 │
        │                                              │
        │    PLAN → CODE → BUILD → TEST                │
        │      ▲                       │               │
        │      │                       ▼               │
        │   MONITOR ← OPERATE ← DEPLOY ← RELEASE      │
        │                                              │
        └─────────────────────────────────────────────┘

        ├──────── DEV ────────┤├──────── OPS ─────────┤
```

| Fase | Atividade | Ferramenta |
|------|-----------|-----------|
| Plan | Planejamento e backlog | Jira, GitHub Issues |
| Code | Desenvolvimento | Git, VS Code |
| Build | Compilação/empacotamento | Docker, Maven, npm |
| Test | Testes automatizados | Jest, pytest, Selenium |
| Release | Versionamento | Git tags, SemVer |
| Deploy | Entrega em ambiente | Terraform, CloudFormation |
| Operate | Manutenção e escala | Kubernetes, AWS |
| Monitor | Observabilidade | Prometheus, Grafana, CloudWatch |

---

## Conexão com outros projetos

| Projeto | Relação com DevOps |
|---------|-------------------|
| `estudos-git` | Versionamento (base de CI/CD) |
| `containers-docker-fundamentos` | Empacotamento de aplicações |
| `terraform-aws-infra` | IaC — infraestrutura automatizada |
| `cloudformation-aws-infra` | IaC — provisionamento declarativo |
| `observabilidade-infra` | Monitoramento e alertas |
| `k8s-resource-report` | Orquestração de containers |

---

## Referências

- [The DevOps Handbook](https://itrevolution.com/the-devops-handbook/)
- [Google SRE Book (gratuito)](https://sre.google/sre-book/table-of-contents/)
- [AWS DevOps](https://aws.amazon.com/devops/)
- [GitHub Actions Docs](https://docs.github.com/en/actions)
- [DORA Metrics](https://dora.dev/)

---

## 📄 Licença

MIT License
