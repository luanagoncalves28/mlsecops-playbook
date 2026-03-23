# NIST Cybersecurity Framework (CSF)

## O que e

Framework voluntario desenvolvido pelo NIST para ajudar organizacoes a gerenciar e reduzir riscos de ciberseguranca. URL: https://www.nist.gov/cyberframework | Versao: CSF 2.0 (2024)

---

## As 6 Funcoes Core (CSF 2.0)

| Funcao | Objetivo | Categorias-chave |
|--------|----------|------------------|
| GOVERN | Estabelecer estrategia e politicas de ciberseguranca | Contexto organizacional, Estrategia de risco, Papeis e responsabilidades |
| IDENTIFY | Entender ativos, riscos e vulnerabilidades | Gestao de ativos, Avaliacao de riscos, Ambiente de negocio |
| PROTECT | Implementar salvaguardas para limitar impacto | Controle de acesso, Conscientizacao, Seguranca de dados |
| DETECT | Identificar ocorrencia de eventos de ciberseguranca | Monitoramento continuo, Deteccao de anomalias |
| RESPOND | Agir apos deteccao de incidente | Planejamento de resposta, Comunicacao, Mitigacao |
| RECOVER | Restaurar capacidades apos incidente | Planejamento de recuperacao, Melhorias, Comunicacao |

---

## Aplicacao em MLSecOps

### GOVERN
- Politica de uso responsavel de IA/ML
- Definicao de apetite de risco para modelos em producao
- Papeis: ML Engineer, Security Engineer, Data Steward
- Compliance com LGPD, BCB, CMN aplicado a sistemas de ML

### IDENTIFY
- Inventario de modelos ML (model registry)
- Classificacao de dados de treinamento por sensibilidade
- Mapeamento de dependencias: datasets, pipelines, APIs
- Avaliacao de risco: data poisoning, model theft, adversarial inputs

### PROTECT
- Controle de acesso a dados de treinamento e modelos
- Criptografia de datasets sensiveis em repouso e transito
- Versionamento seguro com assinatura de artefatos (SLSA)
- Sanitizacao de inputs antes de inferencia
- Separacao de ambientes: dev, staging, producao

### DETECT
- Monitoramento de drift: data drift, concept drift, model drift
- Alertas de performance degradada (Evidently AI, Arize)
- Deteccao de anomalias em padroes de requisicao (adversarial probe)
- SIEM integrado com logs de inferencia e treinamento

### RESPOND
- Runbooks para incidentes de ML: model poisoning, data breach
- Rollback automatico de modelos comprometidos
- Isolamento de pipeline afetado
- Notificacao regulatoria (BCB, ANPD) conforme SLA

### RECOVER
- Restauracao de modelos a partir de versoes auditadas
- Re-treinamento com dados limpos apos data poisoning
- Post-mortem estruturado com licoes aprendidas
- Atualizacao de controles preventivos

---

## Tiers de Implementacao

| Tier | Nivel | Descricao para MLSecOps |
|------|-------|-------------------------|
| 1 | Parcial | Praticas ad hoc, sem processo formal de risco de ML |
| 2 | Risco Informado | Politicas existem mas nao sao amplamente adotadas |
| 3 | Repetivel | Processos formais, atualizados regularmente |
| 4 | Adaptativo | Gestao proativa, melhoria continua baseada em ameacas |

---

## Relacao com Outros Frameworks

- **NIST AI RMF**: Extensao especifica para sistemas de IA (GOVERN, MAP, MEASURE, MANAGE)
- **MITRE ATT&CK**: Tecnicas de ataque mapeadas para funcoes DETECT e RESPOND
- **MITRE ATLAS**: Ameacas especificas de ML mapeadas para IDENTIFY e PROTECT
- **OWASP ML Top 10**: Vulnerabilidades de ML cobertas por PROTECT
- **CIS Controls**: Controles tecnicos que implementam as funcoes do CSF

---

## Mapeamento Regulatorio BR

- **Resolucao CMN 4.557**: GOVERN + IDENTIFY (gestao de riscos financeiros)
- **BACEN Circular 3.909**: DETECT + RESPOND (incidentes ciberneticos)
- **LGPD**: PROTECT + IDENTIFY (dados pessoais em datasets de ML)
- **Resolucao CMN 5.274/2025**: GOVERN (governanca de algoritmos de IA)

---

## Ferramentas MLSecOps por Funcao

| Funcao CSF | Ferramentas |
|------------|-------------|
| GOVERN | Confluence (politicas), Jira (rastreabilidade), OPA (policy-as-code) |
| IDENTIFY | Great Expectations (qualidade de dados), dbt (linhagem), Terraform (IaC) |
| PROTECT | Vault (secrets), KMS (criptografia), Sigstore (assinatura de artefatos) |
| DETECT | Evidently AI, Arize, Grafana, Prometheus, ELK Stack |
| RESPOND | PagerDuty, runbooks automatizados, Argo Rollouts (rollback) |
| RECOVER | MLflow Model Registry, DVC (versionamento de dados), Backup GCS/S3 |
