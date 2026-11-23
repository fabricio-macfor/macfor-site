# Site Macfor · v3.18

Home do site institucional da [Macfor](https://www.macfor.com.br): um único `index.html` (HTML, CSS, JS e imagens embutidos) e os filmes dos cases em `assets/v/`.

Site estático: um único `index.html` (HTML, CSS, JS e imagens embutidos) e a pasta `assets/v/` com o vídeo de abertura e os filmes completos dos cases. Não precisa de build, banco nem servidor de aplicação.

## O que muda em relação à v3.14
- Cores do Sistema Macfor 2.1 (azul #0CA9F9, Agro #13C6A0, Health #9149FB, Hub #DC3A4D, neutros #111116 / #5C5C66 / #E5E5EA / #F5F5F7, fundo branco).
- Logo da Macfor no topo trocado pelo SVG oficial da ID nova.
- Grade de clientes com 34 marcas, todas no mesmo peso visual.
- Fontes, estrutura, textos, cases, vídeo de abertura e páginas: iguais à v3.14.

## Como publicar
1. Suba a pasta inteira para a raiz do domínio (Netlify, Vercel, Cloudflare Pages, S3/CloudFront, Apache/Nginx, GitHub Pages).
2. Mantenha a estrutura:
   ```
   index.html
   assets/v/abertura.mp4
   assets/v/*_full.mp4, institucional_full.mp4, mrsfem_filme2.mp4
   ```
3. Os vídeos são chamados por caminho relativo (`assets/v/...`). Se publicar numa subpasta, mantenha `assets/` ao lado do `index.html`.

## Recomendações
- gzip/brotli para `.html` (o index tem ~26 MB por causa das imagens em base64; comprimido cai bastante).
- Cache longo para `assets/v/*.mp4` (`Cache-Control: public, max-age=31536000`).
- HTTPS.

## Dependências externas
- Fontes: Google Fonts (Inter Tight e JetBrains Mono), as mesmas da v3.14.
- Botão Carreiras: https://jobs.quickin.io/macfor/jobs
- Logos de terceiros: confirmar com os clientes antes de publicar.

## Teste rápido
Abra por um servidor, não por `file://`: `npx serve .` ou `python3 -m http.server`, e acesse `http://localhost:3000` (ou `:8000`).

## Rota /blog (v3.18)
- O site não tem mais botão de blog no rodapé. A página de blog (News) continua existindo e abre direto em `seudominio/blog` (ou `#blog`), sem passar pelo vídeo de abertura.
- O servidor precisa entregar o index.html quando alguém acessar /blog:
  - Cloudflare Pages / Netlify: o arquivo `_redirects` que já vai na raiz resolve.
  - Nginx: `location = /blog { try_files /index.html =404; }`
  - Apache (.htaccess): `RewriteRule ^blog/?$ index.html [L]`
