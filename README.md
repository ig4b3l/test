# GS.Fotografia — Site de Portfólio Profissional

Site estático de portfólio para fotógrafo profissional baseado em Brasília DF, hospedado no **GitHub Pages**.

---

## Estrutura de arquivos

```
/
├── index.html          ← Página principal (HTML + CSS + JS)
├── favicon.svg         ← Ícone da marca
├── robots.txt          ← Configuração para indexadores
├── sitemap.xml         ← Mapa do site (SEO)
├── README.md           ← Este arquivo
└── assets/
    └── img/
        ├── perfil.jpg          ← Foto de perfil (seção Sobre)
        ├── portfolio-1.jpg     ← Casamentos (1 a 6)
        ├── portfolio-2.jpg
        ├── portfolio-3.jpg
        ├── portfolio-4.jpg
        ├── portfolio-5.jpg
        ├── portfolio-6.jpg
        ├── casal-01.jpg        ← Ensaio de Casal (01 a 06)
        ├── casal-02.jpg
        ├── casal-03.jpg
        ├── casal-04.jpg
        ├── casal-05.jpg
        ├── casal-06.jpg
        ├── cha-01.jpg          ← Chá de Fralda (01 a 06)
        ├── cha-02.jpg
        ├── cha-03.jpg
        ├── cha-04.jpg
        ├── cha-05.jpg
        ├── cha-06.jpg
        ├── evento-01.jpg       ← Eventos (01 a 06)
        ├── evento-02.jpg
        ├── evento-03.jpg
        ├── evento-04.jpg
        ├── evento-05.jpg
        └── evento-06.jpg
```

---

## Como publicar no GitHub Pages

1. Crie um repositório no GitHub (ex: `gs-fotografia`)
2. Faça o upload de todos os arquivos para a branch `main`
3. Vá em **Settings → Pages**
4. Em *Source*, selecione **Deploy from a branch → main → / (root)**
5. Clique em **Save**
6. Aguarde alguns minutos — o site estará disponível em:
   `https://seu-usuario.github.io/gs-fotografia/`

> **Dica:** para usar um domínio próprio (ex: `www.gsfotografia.com.br`), crie um arquivo `CNAME` na raiz do projeto com o domínio desejado e configure o DNS do seu provedor para apontar para o GitHub Pages.

---

## Como adicionar ou trocar fotos

Basta substituir os arquivos na pasta `assets/img/` mantendo os mesmos nomes. As imagens são referenciadas diretamente no `index.html`.

Para **adicionar novas fotos** a uma categoria existente:

1. Coloque a imagem em `assets/img/` com um nome descritivo
2. No `index.html`, localize o bloco `<!-- Portfólio -->` correspondente à categoria
3. Copie um bloco `.portfolio-item` existente e atualize o `src` da imagem e o `aria-label`

Para **criar uma nova categoria**:

1. Adicione os itens com `data-cat="NomeCategoria"` no grid do portfólio
2. Adicione um novo botão de filtro: `<button class="filter-btn" data-cat="NomeCategoria">Nome</button>`
3. Adicione um novo card de serviço com `data-filter="NomeCategoria"` na seção de serviços

---

## Como integrar o formulário ao Google Sheets

O formulário já está preparado — basta seguir os passos:

1. Crie uma planilha no **Google Sheets**
2. Vá em **Extensões → Apps Script** e cole o código abaixo:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([
    new Date(),
    data.nome,
    data.email,
    data.telefone,
    data.servico,
    data.mensagem
  ]);
  return ContentService
    .createTextOutput(JSON.stringify({ status: 'ok' }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

3. Salve e clique em **Implantar → Nova implantação**
4. Tipo: **Aplicativo da Web** — Execute como: *Eu* — Quem tem acesso: *Qualquer pessoa*
5. Copie a URL gerada
6. No `index.html`, localize o comentário `INTEGRAÇÃO REAL COM GOOGLE SHEETS` e:
   - Descomente a linha `var ENDPOINT_URL = '...'` e cole a URL
   - Descomente o bloco `fetch()` dentro de `handleFormSubmit()`
   - Remova o bloco de simulação (`setTimeout`) logo abaixo

---

## Tecnologias utilizadas

| Recurso | Detalhe |
|---|---|
| HTML5 semântico | Estrutura acessível com roles e aria-labels |
| CSS3 puro | Variáveis CSS, Grid, Flexbox, animações |
| JavaScript ES5 | Sem frameworks, sem dependências externas |
| Google Fonts | Cormorant Garamond + Outfit |
| GitHub Pages | Hospedagem gratuita de sites estáticos |

---

## Contato

- **E-mail:** agranpolo1@gmail.com
- **WhatsApp:** (61) 99265-1106
- **Instagram:** [@igab.el](https://www.instagram.com/igab.el)
- **Localização:** Brasília DF — Brasil

---

© 2025 GS.Fotografia — Todos os direitos reservados
