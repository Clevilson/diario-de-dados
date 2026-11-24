# Os dados não mudaram? Pode ser cache

O Looker Studio guarda em cache o resultado das consultas. Depois de alterar uma view ou tabela no BigQuery, o painel pode continuar mostrando o resultado antigo.

- No **modo de edição**: menu ⋮ → **Atualizar dados**.
- Em cada fonte de dados dá para ajustar o **frescor dos dados** (por exemplo, de 12 horas para 15 minutos).
- Ao investigar uma divergência, compare primeiro com a consulta direta no BigQuery. Assim você sabe se o problema está no dado ou no painel.
