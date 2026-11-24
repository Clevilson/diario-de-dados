# Ranking dentro de cada grupo com ROW_NUMBER

Top 5 vendedores **por mês**, ordenados pelo atingimento da meta:

```sql
SELECT *
FROM (
  SELECT
    mes, vendedor, vendas, meta,
    ROUND(100 * vendas / meta, 1) AS atingimento_pct,
    ROW_NUMBER() OVER (PARTITION BY mes ORDER BY vendas / meta DESC, vendas DESC) AS posicao
  FROM vendas_x_meta
)
WHERE posicao <= 5;
```

- `ROW_NUMBER` não repete posições. Use `RANK` se empates devem dividir a posição.
- Sempre coloque um **critério de desempate** no `ORDER BY`. Sem ele, a posição pode mudar a cada execução.
- Com a posição calculada no SQL, o painel só precisa filtrar `posicao <= 5`. Isso é mais simples do que montar o ranking dentro da ferramenta de BI.
