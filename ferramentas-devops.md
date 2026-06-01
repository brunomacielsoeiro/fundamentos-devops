# 🧰 Ferramentas DevOps — Ecossistema Completo

## Visão Geral por Categoria

```
┌─────────────────────────────────────────────────────────────────┐
│                    ECOSSISTEMA DevOps                             │
│                                                                   │
│  PLAN        CODE        BUILD       TEST        RELEASE         │
│  ────        ────        ─────       ────        ───────         │
│  Jira        Git         Docker      Jest        Git Tags        │
│  Trello      GitHub      Maven       pytest      SemVer          │
│  Linear      GitLab      Gradle      Selenium    GitHub Releases │
│                          npm/yarn    Cypress                     │
│                                                                   │
│  DEPLOY      OPERATE     MONITOR     SECURITY                    │
│  ──────      ───────     ───────     ────────                    │
│  Terraform   Kubernetes  Prometheus  Snyk                        │
│  CloudForm.  AWS ECS     Grafana     Trivy                       │
│  Ansible     Docker      CloudWatch  SonarQube                   │
│  ArgoCD      Linux       Datadog     OWASP ZAP                   │
│                                                                   │
└─────────────────────────────────────────────────────────────────┘
```

---

## 1. Controle de Versão

| Ferramenta | Tipo | Uso |
|-----------|------|-----|
| **Git** | Distribuído | Versionamento de código e IaC |
| **GitHub** | Plataforma | Hospedagem, PRs, Actions |
| **GitLab** | Plataforma | CI/CD integrado, self-hosted |
| **Bitbucket** | Plataforma | Integração com Jira (Atlassian) |

---

## 2. CI/CD (Pipelines)

| Ferramenta | Tipo | Destaque |
|-----------|------|----------|
| **GitHub Actions** | SaaS | Integrado ao GitHub, YAML simples |
| **GitLab CI** | SaaS/Self | CI/CD nativo no GitLab |
| **Jenkins** | Self-hosted | Flexível, muitos plugins |
| **AWS CodePipeline** | SaaS | Integrado ao ecossistema AWS |
| **CircleCI** | SaaS | Rápido, bom para open source |
| **ArgoCD** | GitOps | Deploy declarativo para Kubernetes |

### Comparação rápida

| Aspecto | GitHub Actions | Jenkins | GitLab CI |
|---------|---------------|---------|-----------|
| Setup | Zero (já no GitHub) | Instalar servidor | Zero (já no GitLab) |
| Config | YAML | Groovy/YAML | YAML |
| Custo | Free tier generoso | Gratuito (infra sua) | Free tier |
| Manutenção | Nenhuma | Alta | Baixa |
| Ecossistema | Marketplace | Plugins | Built-in |

---

## 3. Containers e Orquestração

| Ferramenta | Função | Quando usar |
|-----------|--------|-------------|
| **Docker** | Criar e rodar containers | Sempre (padrão) |
| **Docker Compose** | Multi-container local | Desenvolvimento |
| **Kubernetes** | Orquestração em escala | Produção (muitos containers) |
| **AWS ECS** | Orquestração gerenciada | AWS sem K8s |
| **AWS Fargate** | Serverless containers | Sem gerenciar servidores |

---

## 4. Infraestrutura como Código (IaC)

| Ferramenta | Tipo | Cloud |
|-----------|------|-------|
| **Terraform** | Declarativo, multi-cloud | AWS, GCP, Azure |
| **CloudFormation** | Declarativo, AWS-only | AWS |
| **Ansible** | Imperativo/Declarativo | Qualquer (SSH) |
| **Pulumi** | Programático (TypeScript, Python) | Multi-cloud |
| **CDK** | Programático (AWS) | AWS |

### Quando usar cada um

| Cenário | Ferramenta |
|---------|-----------|
| Multi-cloud | Terraform |
| Apenas AWS | CloudFormation ou CDK |
| Configuração de servidores | Ansible |
| Equipe que prefere código real | Pulumi ou CDK |

---

## 5. Monitoramento e Observabilidade

| Ferramenta | Tipo | Foco |
|-----------|------|------|
| **Prometheus** | Open source | Métricas (pull-based) |
| **Grafana** | Open source | Dashboards e visualização |
| **CloudWatch** | AWS | Métricas + Logs + Alarmes |
| **Datadog** | SaaS | Observabilidade completa |
| **ELK Stack** | Open source | Logs (Elasticsearch + Logstash + Kibana) |
| **Jaeger** | Open source | Distributed tracing |

---

## 6. Segurança (DevSecOps)

| Ferramenta | Tipo | O que faz |
|-----------|------|-----------|
| **Snyk** | SaaS | Vulnerabilidades em dependências |
| **Trivy** | Open source | Scan de containers e IaC |
| **SonarQube** | Self/SaaS | Qualidade e segurança de código |
| **OWASP ZAP** | Open source | Testes de segurança web |
| **AWS GuardDuty** | AWS | Detecção de ameaças |
| **Checkov** | Open source | Scan de IaC (Terraform, CloudFormation) |

---

## 7. Comunicação e Colaboração

| Ferramenta | Uso em DevOps |
|-----------|--------------|
| **Slack** | Alertas, notificações de pipeline |
| **PagerDuty** | On-call, escalação de incidentes |
| **Confluence** | Documentação, runbooks |
| **Jira** | Tracking de tarefas e bugs |

---

## Mapa Mental

```
                         DevOps Tools
                              │
          ┌───────────────────┼───────────────────┐
          │                   │                   │
       DEVELOP             DELIVER             OPERATE
          │                   │                   │
    ┌─────┼─────┐      ┌─────┼─────┐      ┌─────┼─────┐
    │     │     │      │     │     │      │     │     │
   Git  Docker Test  CI/CD  IaC  Deploy  K8s  Monitor  Security
    │     │     │      │     │     │      │     │       │
 GitHub  Compose Jest Actions Terraform ArgoCD ECS Prometheus Trivy
 GitLab         pytest Jenkins CloudForm.      Grafana  Snyk
                       GitLab  Ansible         CloudWatch
```

---

## Resumo: Stack Recomendada para Iniciantes

| Categoria | Ferramenta | Por quê |
|-----------|-----------|---------|
| Versionamento | Git + GitHub | Padrão da indústria |
| CI/CD | GitHub Actions | Zero setup, gratuito |
| Containers | Docker | Obrigatório |
| IaC | Terraform | Multi-cloud, mais demandado |
| Monitoramento | Prometheus + Grafana | Open source, padrão |
| Segurança | Trivy + Snyk | Gratuitos, fáceis |
