# Materializar uma view pesada com consulta agendada

**Problema:** um painel no Looker Studio lê uma view com vários JOINs. Cada filtro aplicado no painel roda a view inteira de novo, o que deixa tudo lento e caro.

**Solução:** criar uma *consulta agendada* que grava o resultado da view em uma tabela, e apontar o painel para a tabela.

```sql
-- consulta agendada (ex.: a cada hora)
CREATE OR REPLACE TABLE meu_dataset.tbl_painel_vendas AS
SELECT
  *,
  CURRENT_DATETIME('America/Sao_Paulo') AS ultima_atualizacao
FROM meu_dataset.vw_painel_vendas;
```

**Dicas**
- Grave a coluna `ultima_atualizacao` e mostre no painel. Assim quem consome sabe se o dado está atual.
- Se a consulta agendada falhar, a tabela continua com a última carga. Ative o e-mail de falha nas opções da consulta.
- Antes de alterar a view, salve uma cópia do SQL. Isso facilita voltar atrás.
