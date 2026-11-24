# Ler uma planilha do Google Sheets com pandas

Para planilhas **compartilhadas por link** (somente leitura), o jeito mais simples é exportar como CSV:

```python
import pandas as pd

planilha_id = "ID_DA_PLANILHA"
aba_gid = "0"  # número que aparece depois de gid= na URL da aba
url = f"https://docs.google.com/spreadsheets/d/{planilha_id}/export?format=csv&gid={aba_gid}"
df = pd.read_csv(url)
```

Para planilhas privadas, use autenticação OAuth (`google-auth` + `gspread`). **Nunca suba para o GitHub** o `client_secret*.json` nem o `token.json`: coloque esses arquivos no `.gitignore`.
