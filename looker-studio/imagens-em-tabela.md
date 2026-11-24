# Mostrar imagens em uma tabela do Looker Studio

Crie um campo calculado com a função `IMAGE`:

```
IMAGE(foto_url, nome)
```

- O link precisa ser **público e direto para o arquivo**. Para arquivos do Google Drive, converta o link de compartilhamento
  `https://drive.google.com/file/d/ID/view` para `https://lh3.googleusercontent.com/d/ID`.
- Ícones condicionais (medalhas, setas) funcionam com `CASE`:

```
IMAGE(CASE posicao WHEN 1 THEN "url_ouro" WHEN 2 THEN "url_prata" WHEN 3 THEN "url_bronze" END, "medalha")
```

- Imagens PNG com fundo transparente ficam bem tanto em temas claros quanto escuros.
