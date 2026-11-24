# Tabela externa do Google Sheets: prática, mas frágil

Dá para consultar uma planilha direto no BigQuery criando uma **tabela externa** (Criar tabela → Origem: Google Drive → formato Google Sheets). É ótimo para metas, de-para e cadastros mantidos pela área de negócio.

```sql
SELECT unidade, mes, SAFE_CAST(meta AS INT64) AS meta
FROM meu_dataset.ext_metas
WHERE meta IS NOT NULL;
```

**Cuidados**
- **Se a planilha ficar inacessível** (permissão removida, arquivo movido), toda view que a usa falha, e o painel para de atualizar.
- Defina o intervalo (ex.: `Página1!A:D`) e quantas linhas de cabeçalho pular. Assim, colunas extras na planilha não quebram o esquema.
- Trate tipos com `SAFE_CAST`: em planilha, alguém sempre digita "10%" ou "-" numa coluna numérica.
- Para dados críticos, materialize uma cópia em tabela nativa (ver [materializar view](materializar-view-com-consulta-agendada.md)).
