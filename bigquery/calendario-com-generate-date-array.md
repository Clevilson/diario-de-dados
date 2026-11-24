# Gerar um calendário de meses sem tabela auxiliar

Útil para garantir que meses **sem vendas** apareçam no resultado (com zero) e para "fotografar" a carteira mês a mês.

```sql
SELECT mes
FROM UNNEST(GENERATE_DATE_ARRAY('2025-01-01', CURRENT_DATE(), INTERVAL 1 MONTH)) AS mes;
```

Depois é só fazer `LEFT JOIN` com os fatos agregados por mês e usar `COALESCE(vendas, 0)`.
