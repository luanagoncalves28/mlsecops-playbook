# Guia do Primeiro Dia — MLSecOps Engineer

## Para que serve este guia

Este guia é para ser lido na manhã do primeiro dia num novo emprego. Ele não é um roteiro de onboarding genérico. É um protocolo de operação para quem já sabe o que faz e precisa calibrar como se posicionar com maturidade desde a chegada.

O objetivo do primeiro dia não é impressionar. É escutar, mapear e calibrar.

---

## Antes de entrar no escritório

**Revise o contexto da empresa:**
- Qual é o produto principal? Onde o ML é crítico?
- Que tipo de dados eles processam? (dados de pagamento, saúde, identidade?)
- Qual é a exposição regulatória? (Fintech = BCB/CMN/LGPD, Saúde = LGPD + Anvisa, etc.)
- Houve incidentes públicos recentes envolvendo a empresa?

**Abra o Documento Vivo da Empresa** (template em fase-4-operacional) e deixe pronto para preencher.

---

## Primeiras 2 horas

### O que fazer
- Apresentar-se com brevidade e clareza: nome, papel, de onde vem, o que vai fazer
- Não fazer declaracões sobre o que vai mudar ou o que está errado
- Ouvir mais do que falar
- Observar dinâmicas de equipe: quem toma decisões, quem é consultado informalmente, quem é cético

### O que não fazer
- Não questionar decisões de arquitetura que você ainda não entende o contexto completo
- Não demonstrar que já tem solucao para problemas que você ainda não conhece
- Não pedir acesso a sistemas prod antes de entender a governança de acesso da empresa

---

## Perguntas que você deve fazer no primeiro dia

### Para o Tech Lead ou Engenheiro Sênior
- "Como é o pipeline de ML hoje — da coleta de dados até o modelo em produção?"
- "Qual é o processo de review antes de um modelo ir pra prod?"
- "Onde estão os maiores pontos de atenção técnica hoje?"
- "Tem algum incidente recente que seria útil eu entender?"

### Para o gestor direto
- "Qual é o output esperado de mim nos próximos 90 dias?"
- "Quem são os stakeholders mais importantes do meu trabalho fora do time técnico?"
- "Tem algo urgente que eu deveria saber antes de qualquer coisa?"

### Para o time de dados/ML (se houver)
- "Quais modelos estão ativos em produção hoje?"
- "Como é feito o monitoramento deles?"
- "Quando foi a última vez que algum modelo foi retreinado? Por quê?"

---

## O que registrar no Documento Vivo

Ao final do primeiro dia, documente:
- Nomes e papéis das pessoas que você conheceu
- Estrutura de time que você mapeou (não o organograma — a estrutura real de quem decide o quê)
- Tecnologias mencionadas (mesmo de passagem)
- Dúvidas que ficaram abertas
- Primeira impressão do estado da segurança (sem julgamentos — observações)

---

## Postura que você precisa comunicar sem dizer explicitamente

| O que você quer que percebam | Como demonstrar |
|---|---|
| Você sabe ML e Security em profundidade | Fazendo perguntas técnicas precisas, não afirmações vagas |
| Você entende o contexto de negócio | Perguntando sobre impacto de falha, não só sobre arquitetura |
| Você é alguém que construói, não só audita | Mostrando curiosidade sobre o pipeline, não só sobre riscos |
| Você respeita o trabalho que já foi feito | Não questionando decisões passadas sem entender o contexto |

---

## Princípio do primeiro dia

> O primeiro dia é para escutar. A segunda semana é para entender. O primeiro mês é para mapear. Depois disso, você age com contexto.

Quem chega com julgamentos no primeiro dia perde a confianca que levaria meses para construir.

---

*Criado: março 2026*
*Repositório: mlsecops-playbook (privado)*
*Localização: fase-1-identidade/guia-primeiro-dia.md*
