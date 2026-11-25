# queima.shopee

App de **achados ultra baratos / queima de estoque** no estilo Shopee: feed infinito de ofertas
com filtros de preço, frete grátis, cupom, busca e ordenação. Cada card abre a busca do produto
no site da Shopee.

## Como funciona

- `src/lib/deals.ts` — catálogo local (80 produtos) e gerador determinístico de ofertas
  infinitas. Não faz requisição nenhuma: por isso o feed nunca esgota.
- `src/` — React + Vite: filtros, busca com debounce, scroll infinito, animações e layout
  responsivo.
- `deploy/worker.js` — Worker que só serve os assets estáticos do build.

## Rodar local

```bash
npm install
npm run dev          # http://127.0.0.1:5183
npm run build        # gera dist/
```

## Publicar

### Freebuff Sites

Manifesto em `freebuff.deploy.json` (assets em `dist` + `deploy/worker.js`).

### Netlify

Site 100% estático: `netlify.toml` já configura build e fallback de SPA.

```bash
npm run build
netlify deploy --prod --dir=dist
```

## Preços reais da Shopee

As ofertas deste app são ilustrativas (geradas localmente) e os links levam à busca oficial na
Shopee. Para exibir preço, estoque e foto **reais** é necessário o **App ID + Secret da API de
Afiliados da Shopee** (`open-api.affiliate.shopee.com.br/graphql`): o site bloqueia acesso direto
(403) e não existe API pública sem credencial. Com as chaves, o backend troca o catálogo local
pelo feed real, mantendo o mesmo layout.
