# Deduplicar registros com QUALIFY

Sistemas de origem costumam mandar várias versões da mesma linha. Para ficar só com a mais recente de cada chave:

```sql
SELECT *
FROM meu_dataset.cobrancas_raw
WHERE TRUE  -- o BigQuery exige WHERE, GROUP BY ou HAVING junto com QUALIFY
QUALIFY ROW_NUMBER() OVER (
  PARTITION BY id_cobranca
  ORDER BY atualizado_em DESC
) = 1;
```

Sem `QUALIFY`, seria preciso uma subconsulta com `ROW_NUMBER()` e depois `WHERE rn = 1`. O resultado é o mesmo, mas o código fica mais longo.
