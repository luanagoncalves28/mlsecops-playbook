# Monitoramento de Modelos em Producao

## Por que Monitorar

Modelos de ML degradam ao longo do tempo porque o mundo muda. O que funcionou ontem pode falhar amanha. Monitoramento continuo e essencial para:
- Detectar degradacao de performance antes de impactar negocio
- Identificar ataques adversariais
- Garantir compliance regulatorio (CMN 5.274, BCB 538)
- Detectar bias emergente em producao

---

## Tipos de Drift

| Tipo | O que muda | Exemplo | Impacto |
|------|------------|---------|--------|
| **Data Drift** | Distribuicao das features muda | Perfil de cliente muda pos-pandemia | Modelo ve dados diferentes do treinamento |
| **Concept Drift** | Relacao entre features e target muda | Comportamento de fraude evolui | Modelo aprende padroes obsoletos |
| **Label Drift** | Distribuicao das labels muda | Taxa de fraude aumenta | Threshold desatualizado |
| **Prediction Drift** | Distribuicao das predicoes muda | Mais transacoes marcadas como fraude | Sintoma de data/concept drift |
| **Model Decay** | Performance geral degrada | Accuracy cai de 95% para 88% | Necessidade de re-treino |

---

## Metricas de Monitoramento

### Metricas de Performance
```python
# Metricas para monitorar (calculadas com labels atrasados)
performance_metrics = {
    'precision': TP / (TP + FP),
    'recall': TP / (TP + FN),
    'f1_score': 2 * precision * recall / (precision + recall),
    'auc_roc': area_under_roc_curve,
    'false_positive_rate': FP / (FP + TN)  # Critico para fraude
}
```

### Metricas de Drift de Dados
- **KS Test**: Kolmogorov-Smirnov para distribuicoes univariadas
- **PSI** (Population Stability Index): Mudanca na distribuicao de features
- **Jensen-Shannon Divergence**: Distancia entre distribuicoes
- **Chi-Square**: Para variaveis categoricas

### Metricas Operacionais
- Latencia de inferencia (p50, p95, p99)
- Throughput (predicoes por segundo)
- Taxa de erros da API
- Disponibilidade do endpoint

### Metricas de Seguranca
- Taxa de inputs anomalos (potenciais adversariais)
- Tentativas de acesso nao autorizado ao endpoint
- Requisicoes com features fora do range historico
- Distribuicao de scores (drift na saida)

---

## Stack de Monitoramento

### Evidently AI
```python
import evidently
from evidently.report import Report
from evidently.metric_preset import DataDriftPreset, ClassificationPreset

# Relatorio de drift
report = Report(metrics=[
    DataDriftPreset(),
    ClassificationPreset()
])

report.run(
    reference_data=train_data,
    current_data=production_data_last_week
)
report.save_html('drift_report.html')
```

### Alertas com Grafana/Prometheus
```yaml
# prometheus-rules.yaml
groups:
  - name: ml_model_alerts
    rules:
      - alert: ModelF1Degradation
        expr: ml_model_f1_score < 0.85
        for: 1h
        labels:
          severity: warning
        annotations:
          summary: "F1 score below threshold"
      
      - alert: HighFalsePositiveRate
        expr: ml_false_positive_rate > 0.05
        for: 30m
        labels:
          severity: critical
        annotations:
          summary: "FPR above 5% - possible model attack or drift"
```

---

## Politica de Re-treinamento

### Triggers Automaticos
- F1 score cai abaixo de threshold definido
- PSI > 0.2 para features criticas
- Data drift detectado em mais de 30% das features
- Intervalo de tempo (ex: re-treino mensal obrigatorio)

### Processo de Re-treinamento Seguro
```
1. Trigger detectado -> notificacao ao time
2. Analise de causa raiz (drift ou ataque?)
3. Coleta de novos dados de treinamento
4. Validacao de qualidade e integridade dos novos dados
5. Re-treinamento com validacao
6. Comparacao: novo modelo vs modelo em producao
7. Security gate: testes adversariais, fairness
8. Aprovacao formal
9. Deploy progressivo (canary)
10. Monitoramento intensivo pos-deploy
```

---

## Ferramentas de Monitoramento

| Ferramenta | Tipo | Melhor Para | Open Source |
|------------|------|-------------|-------------|
| **Evidently AI** | Data/model drift | Python, batch | Sim |
| **Arize AI** | ML observability | Producao, real-time | Nao |
| **WhyLabs** | Data monitoring | Privacidade first | Parcial |
| **Grafana** | Metricas operacionais | Dashboards, alertas | Sim |
| **Prometheus** | Time series metrics | Coleta de metricas | Sim |
| **Vertex AI Monitoring** | GCP-native | Integracao GCP | Nao |

---

## Monitoramento de Fairness

```python
from aif360.metrics import ClassificationMetric

# Calcular fairness por grupo demografico
fairness_metric = ClassificationMetric(
    dataset_true=test_data,
    dataset_pred=predictions,
    privileged_groups=[{'age_group': 'adult'}],
    unprivileged_groups=[{'age_group': 'elderly'}]
)

# Metricas
print(f'Equal Opportunity Diff: {fairness_metric.equal_opportunity_difference()}')
print(f'Average Odds Difference: {fairness_metric.average_odds_difference()}')
# Threshold: < 0.1 para ambas as metricas
```

---

## Checklist de Monitoramento

- [ ] Dashboard de performance operacional (Grafana)
- [ ] Alertas de degradacao de F1/Precision/Recall
- [ ] Monitoramento de drift semanal (Evidently)
- [ ] Metricas de latencia p99 < 200ms
- [ ] Logs de predicoes criticas retidos 5 anos
- [ ] Relatorio de fairness mensal
- [ ] Processo de re-treinamento documentado
- [ ] Alertas de inputs anomalos (adversarial detection)
