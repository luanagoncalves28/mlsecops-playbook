# Guia de Comunicação por Audiência — MLSecOps Engineer

## Para que serve este guia

O trabalho técnico que não é comunicado com clareza para a audiência certa não existe para a organização. Este guia define como traduzir o mesmo trabalho de MLSecOps em linguagens diferentes, dependendo de com quem você está falando.

**Regra central:** a mesma informação, apresentada de formas diferentes, produz resultados diferentes. Você não está simplificando — está traduzindo.

---

## Audiência 1 — Tech Lead / Engenheiro Sênior

### O que eles precisam saber
Impacto técnico, viabilidade de implementação, dívida técnica e trade-offs.

### O que eles não querem
Jargão de gestão de risco sem substância técnica. Pedidos vagos de "melhorar a segurança".

### Como falar
- Seja específico: nome do controle, ferramenta, flag de configuração
- Mostre o trade-off: "Se implementarmos SLSA Level 2, o CI/CD fica 15% mais lento, mas eliminamos o vetor de substituição de artefato"
- Antecipe perguntas técnicas: já tenha a resposta antes de apresentar
- Mostre que entende a complexidade do sistema antes de propor alterações

### Template de conversa
```
Identifiquei que [componente X] não tem [controle Y].
O risco é [ataque Z, com probabilidade W e impacto V].
Proponho implementar [solucao] usando [ferramenta/framework].
Estimativa: [tempo] de trabalho. Impacto no pipeline: [descricao].
Quer que eu prototype ou prefere revisar a arquitetura primeiro?
```

---

## Audiência 2 — CISO / Head de Segurança

### O que eles precisam saber
Superfície de ataque, controles existentes, lacunas, plano de correção e timeline.

### O que eles não querem
Detalhes de implementação técnica sem contexto de risco. Problemas sem proposta de solução.

### Como falar
- Use frameworks conhecidos: MITRE ATLAS, OWASP ML Top 10, NIST AI RMF
- Quantifique o risco quando possível: impacto financeiro, regulatório, reputacional
- Apresente o estado atual e o estado desejado
- Tenha um plano de ação com timeline realista

### Template de conversa
```
No modelo [X], identificamos exposicao ao vetor [ATLAS TTP Y].
O controle mitigador [Z] não está implementado.
Risco: [descricao de impacto]. Regulatorio: [referencia a norma].
Plano: implementar [controle] em [prazo], com responsavel [pessoa/time].
Aprovacao necessaria: [o que precisa ser desbloqueado].
```

---

## Audiência 3 — DPO / Compliance / Juridico

### O que eles precisam saber
Conformidade com legislação (LGPD, BCB, CMN), dados pessoais envolvidos, riscos de violacao e documentação de controles.

### O que eles não querem
Jargão técnico de ML. Descrições de arquitetura sem relacão com obrigações legais.

### Como falar
- Mapeie explicitamente: qual dado pessoal, qual base legal, qual finalidade
- Referencie artigos específicos (LGPD Art. 46, CMN 5.274/2025, BCB Resolution 85)
- Documente quais controles existem e como eles protegem os dados
- Apresente o que seria reportado em caso de incidente e em quanto tempo

### Template de conversa
```
O modelo [X] processa [tipo de dado pessoal] com base legal [X do LGPD].
A finalidade é [Y]. O dado é retido por [prazo].
Controles de proteção ativos: [lista].
Em caso de incidente: o protocolo é [descricao], com notificacao a ANPD em [prazo].
Documentacao de conformidade disponivel em: [local].
```

---

## Audiência 4 — CEO / CFO / Diretoria

### O que eles precisam saber
Risco de negócio, custo de inacão, custo de ação e impacto no produto/receita.

### O que eles não querem
Detalhes técnicos. Jargão de segurança sem traducão para impacto de negócio.

### Como falar
- Comece pelo risco de negócio: "Se esse modelo for comprometido, o impacto é X"
- Use linguagem de custo e oportunidade: "Implementar esse controle custa Y. Não implementar nos expõe a um risco de Z"
- Referencie regulacão como risco concreto: "O BCB pode aplicar multa de até R$50M por inadequacão nesse tipo de sistema"
- Apresente a decisao que precisa ser tomada, não o problema em detalhes

### Template de conversa
```
Temos um modelo critico [X] que [descricao do risco em linguagem de negocio].
Se explorado, o impacto estimado é [financeiro/reputacional/regulatorio].
Proposta: investir [valor/tempo] em [controle], reduzindo esse risco para [nivel aceitavel].
Decisao necessaria: [o que você precisa que eles aprovem].
```

---

## Regras gerais de comunicacao

| Situacao | Regra |
|---|---|
| Problema sem solucao | Nunca apresente sem pelo menos uma proposta inicial |
| Jargao tecnico | Sempre defina na primeira vez que usar, mesmo com tech lead |
| Urgencia | Separe: "urgente" = precisa de atencao esta semana. "Critico" = pode causar dano imediato |
| Discordancias | Apresente dados, nao opinioes. "Os dados mostram X" > "Eu acho que X" |
| Escalacao | So escale com contexto completo: o que e, qual e o risco, o que voce ja tentou |

---

*Criado: marco 2026*
*Repositorio: mlsecops-playbook (privado)*
*Localizacao: fase-1-identidade/guia-comunicacao-por-audiencia.md*
