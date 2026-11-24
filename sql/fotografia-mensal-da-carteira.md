# Fotografia mensal da carteira

Para saber quantas assinaturas estavam ativas em cada mês, cruze um calendário com as assinaturas e teste as datas (BigQuery):

```sql
SELECT
  m.mes,
  COUNTIF(a.data_inicio < m.mes
          AND (a.data_cancelamento IS NULL OR a.data_cancelamento >= m.mes)) AS ativas_inicio,
  COUNTIF(DATE_TRUNC(a.data_inicio, MONTH) = m.mes)                          AS novas,
  COUNTIF(DATE_TRUNC(a.data_cancelamento, MONTH) = m.mes)                    AS cancelamentos
FROM UNNEST(GENERATE_DATE_ARRAY('2025-01-01', '2026-10-01', INTERVAL 1 MONTH)) AS m
CROSS JOIN assinaturas a
GROUP BY m.mes;
```

**Churn do mês** = `cancelamentos / ativas_inicio`. Deixe registrado como tratar quem entra e cancela no mesmo mês, porque cada área costuma contar de um jeito.

Exemplo completo: [analise-assinaturas-saude](https://github.com/Clevilson/analise-assinaturas-saude).
