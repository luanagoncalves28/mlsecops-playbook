# CIS Controls v8

## O que e

Conjunto de 18 controles priorizados de ciberseguranca desenvolvidos pelo Center for Internet Security (CIS). Representa as acoes defensivas mais eficazes e essenciais. URL: https://www.cisecurity.org/controls | Versao: CIS Controls v8 (2021)

---

## Os 18 Controles CIS

| # | Controle | Grupo de Implementacao |
|---|----------|------------------------|
| 1 | Inventario e Controle de Ativos Corporativos | IG1, IG2, IG3 |
| 2 | Inventario e Controle de Ativos de Software | IG1, IG2, IG3 |
| 3 | Protecao de Dados | IG1, IG2, IG3 |
| 4 | Configuracao Segura de Ativos e Software | IG1, IG2, IG3 |
| 5 | Gestao de Contas | IG1, IG2, IG3 |
| 6 | Gestao de Controle de Acesso | IG1, IG2, IG3 |
| 7 | Gestao Continua de Vulnerabilidades | IG2, IG3 |
| 8 | Gestao de Log de Auditoria | IG1, IG2, IG3 |
| 9 | Protecoes de Email e Navegador Web | IG1, IG2, IG3 |
| 10 | Defesas contra Malware | IG1, IG2, IG3 |
| 11 | Recuperacao de Dados | IG1, IG2, IG3 |
| 12 | Gestao de Infraestrutura de Rede | IG2, IG3 |
| 13 | Monitoramento e Defesa de Rede | IG2, IG3 |
| 14 | Conscientizacao de Seguranca e Treinamento de Habilidades | IG1, IG2, IG3 |
| 15 | Gestao de Provedores de Servicos | IG2, IG3 |
| 16 | Seguranca de Aplicacoes | IG2, IG3 |
| 17 | Gestao de Resposta a Incidentes | IG2, IG3 |
| 18 | Teste de Penetracao | IG3 |

---

## Grupos de Implementacao (IG)

| IG | Perfil | Aplicacao MLSecOps |
|----|--------|--------------------|
| IG1 | Pequenas empresas, recursos limitados | Controles basicos essenciais |
| IG2 | Empresas medias, dados sensiveis | + Controles para ambientes de ML |
| IG3 | Grandes empresas, dados criticos | Todos os controles, incluindo pen test |

---

## Controles Mais Relevantes para MLSecOps

### Controle 1 - Inventario de Ativos
**Aplicacao ML:**
- Catalogar todos os modelos em producao (model registry)
- Inventario de datasets com classificacao de sensibilidade
- Rastrear endpoints de inferencia e APIs
- Registrar dependencias de bibliotecas ML

**Ferramentas:** MLflow Model Registry, DVC, Neptune.ai

### Controle 3 - Protecao de Dados
**Aplicacao ML:**
- Classificar datasets por nivel de sensibilidade (PII, financeiro)
- Criptografar dados de treinamento em repouso (AES-256)
- Mascaramento de dados sensiveis em logs de treinamento
- Data minimization: usar apenas dados necessarios
- Controles de retencao e exclusao de datasets

**Ferramentas:** Google Cloud DLP, AWS Macie, Azure Purview

### Controle 5 - Gestao de Contas
**Aplicacao ML:**
- Service accounts dedicadas por pipeline de ML
- Principio do menor privilegio para acesso a dados de treinamento
- MFA para acesso a model registry e artifact stores
- Rotacao de credentials de acesso a datasets

**Ferramentas:** HashiCorp Vault, GCP IAM, AWS IAM

### Controle 6 - Controle de Acesso
**Aplicacao ML:**
- RBAC para model registry (viewer, developer, deployer)
- Controle de quem pode re-treinar modelos em producao
- Aprovacoes obrigatorias para deploy de novos modelos
- Segregacao: acesso a dados de treinamento vs dados de producao

### Controle 7 - Gestao de Vulnerabilidades
**Aplicacao ML:**
- Scan regular de dependencias ML (pip-audit, safety, Snyk)
- Atualizacao de bibliotecas com CVEs criticos
- Verificacao de modelos pre-treinados (adversarial robustness)
- Avaliacao periodica de bias e fairness

**Ferramentas:** Snyk, Dependabot, pip-audit, ART (Adversarial Robustness Toolbox)

### Controle 8 - Log de Auditoria
**Aplicacao ML:**
- Log de todas as predicoes em producao (com features de entrada)
- Rastreamento de quem fez deploy de qual versao de modelo
- Auditoria de acesso a datasets de treinamento
- Retencao de logs conforme regulacao (BCB: minimo 5 anos)
- Logs imutaveis para compliance

**Ferramentas:** ELK Stack, Cloud Logging (GCP), CloudTrail (AWS)

### Controle 16 - Seguranca de Aplicacoes
**Aplicacao ML:**
- Validacao e sanitizacao de inputs antes de inferencia
- Rate limiting em APIs de ML para prevenir model extraction
- Autenticacao e autorizacao em endpoints de predicao
- Testes de seguranca pre-deploy (adversarial inputs)
- OWASP ML Top 10 como checklist de seguranca

### Controle 17 - Resposta a Incidentes
**Aplicacao ML:**
- Playbooks especificos para incidentes de ML:
  - Data poisoning detectado
  - Model performance degradation suspeita
  - Acesso nao autorizado a modelos/dados
  - Adversarial attack em producao
- Definicao de SLAs de resposta por severidade

---

## Mapeamento CIS Controls x Frameworks ML

| CIS Control | NIST CSF | MITRE ATLAS | OWASP ML |
|-------------|----------|-------------|----------|
| 1 (Inventario) | IDENTIFY | - | - |
| 3 (Dados) | PROTECT | AML.T0037 | ML05 |
| 7 (Vulnerabilidades) | IDENTIFY | AML.T0043 | ML06 |
| 8 (Logs) | DETECT | AML.T0047 | ML09 |
| 16 (App Sec) | PROTECT | AML.T0015 | ML01 |
| 17 (Resposta) | RESPOND | - | ML10 |

---

## Mapeamento Regulatorio BR

- **BCB Circular 3.909/2018**: Controles 8, 17 (logs e resposta a incidentes ciberneticos)
- **LGPD**: Controles 3, 5, 6 (protecao de dados pessoais em datasets)
- **CMN 4.557/2017**: Controles 1, 7 (inventario e gestao de riscos)
- **CMN 5.274/2025**: Controles 1, 8, 16 (governanca e auditabilidade de IA)
