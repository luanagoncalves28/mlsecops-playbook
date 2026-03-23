# Guia do Primeiro Mês — MLSecOps Engineer

## Para que serve este guia

O primeiro mês é a janela de mapeamento. Não é o momento de implementar, refatorar ou propor grandes mudanças. É o momento de entender o sistema como ele é — não como deveria ser.

Ao final do primeiro mês, você deve ter um mapa claro de: o que existe, o que está funcionando, o que é risco real, e onde está a dívida técnica mais urgente.

---

## Semana 1 — Orientação e Acesso

### Objetivos
- [ ] Completar todos os processos de onboarding administrativo
- [ ] Obter acesso aos sistemas principais (com nível correto — não sobre-provisionado)
- [ ] Ler documentação de arquitetura existente (se houver)
- [ ] Mapear quem são os times adjacentes: Data Engineering, Platform, Compliance, CISO
- [ ] Iniciar o Documento Vivo da Empresa

### O que observar
- Como é feita a gestão de acesso? Tem IAM, principípio de menor privilégio, revisões periódicas?
- Onde estão os modelos ativos? Quantos? Em quais sistemas?
- Existe alguma documentação de segurança de ML? Qual foi a última atualização?

### Entregavel esperado
- Documento Vivo iniciado com: empresa, produto, times, modelos identificados e primeiras observações

---

## Semana 2 — Mergulho Técnico

### Objetivos
- [ ] Entender o pipeline de ML de ponta a ponta: ingestão → feature engineering → treino → validação → deployment → monitoramento
- [ ] Identificar onde cada estágio roda (infra, cloud, ferramentas)
- [ ] Mapear pontos de controle existentes: onde há review, aprovação, auditoria?
- [ ] Entender como o modelo vai para produção hoje — o processo real, não o ideal

### Perguntas técnicas para aprofundar
- O modelo é versionado? Onde? Como?
- Features de treino e inferencia são as mesmas? Como é garantido?
- Existe monitoramento de data drift e model drift? Com quais ferramentas?
- O pipeline de CI/CD é automatizado? Onde estão os segredos (secrets)? Como são gerenciados?
- Existe SBOM (Software Bill of Materials) para dependências Python/ML?

### Entregavel esperado
- Diagrama ou descrição do pipeline mapeado (pode ser texto no Documento Vivo)
- Lista de lacunas técnicas identificadas (sem propor solucao ainda — só registrar)

---

## Semana 3 — Avaliação de Risco e Conformidade

### Objetivos
- [ ] Identificar o contexto regulatório da empresa (BCB, CMN, LGPD, EU AI Act?)
- [ ] Verificar se existe documentação de conformidade para os modelos ativos
- [ ] Entender o histórico de incidentes: teve algum? Como foi resolvido? Está documentado?
- [ ] Identificar os modelos de maior risco: quais afetam decisões críticas (crédito, fraude, saude?)

### Análise de risco rápida (para cada modelo crítico)
- Qual é o impacto se o modelo falhar? (financeiro, regulatório, reputacional)
- Qual é o impacto se o modelo for comprometido por atacante?
- Existe plano de failsafe ou fallback?
- Qual é o SLA de disponibilidade? Está sendo cumprido?

### Entregavel esperado
- Gap Analysis preliminar (template em fase-4-operacional): o que existe vs. o que falta em termos de controles

---

## Semana 4 — Definição de Prioridades e Primeiras Ações

### Objetivos
- [ ] Consolidar o mapa de risco com o gestor direto
- [ ] Propor um plano de 90 dias: o que será feito, em qual ordem, com qual justificativa
- [ ] Identificar o quick win de maior impacto com menor esforço (o que dá pra resolver em 2 semanas e gera visibilidade?)
- [ ] Alinhar expectativas de output com o time

### Critérios para priorizar
1. Risco regulatório (penalidade ativa ou possível)
2. Superfície de ataque exposta sem controle
3. Modelo crítico sem monitoramento adequado
4. Pipeline sem rastreabilidade de artefatos
5. Dependências desatualizadas com CVEs conhecidos

### Entregavel esperado
- Plano de 90 dias rascunhado e alinhado com o gestor
- Primeiro Registro de Decisão documentado (por quê começar por essa prioridade, não por outra)

---

## Indicadores de que o primeiro mês foi bem executado

- [ ] Você consegue descrever o pipeline completo sem precisar consultar ninguém
- [ ] Você sabe quais modelos estão em produção e qual é o risco de cada um
- [ ] Você tem um Documento Vivo preenchido com contexto real da empresa
- [ ] Você tem um Gap Analysis preliminar documentado
- [ ] Você já identificou o maior risco não resolvido e tem um plano para ele
- [ ] Seu gestor e time confiam que você entende o contexto antes de propor mudanças

---

## Princípio do primeiro mês

> Mapear antes de agir. Entender antes de propor. Respeitar o que já existe antes de mudar.

O MLSecOps Engineer que age antes de entender o contexto cria mais problemas do que resolve.

---

*Criado: março 2026*
*Repositório: mlsecops-playbook (privado)*
*Localização: fase-1-identidade/guia-primeiro-mes.md*
