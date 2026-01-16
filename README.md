# Landing page de Psicanálise (estática, com GitHub como "banco de dados")

Este projeto é uma **one-page** moderna, acessível e responsiva para atendimento **psicanalítico online**. O conteúdo dinâmico (serviços, depoimentos e FAQ) é carregado de arquivos JSON na pasta `data/` — você edita esses arquivos direto no GitHub, que funciona como seu **CMS/banco de dados**.

## Funcionalidades
- ⚡️ Site estático rápido (HTML/CSS/JS puro)
- 🧩 Conteúdo dinâmico via `data/*.json`
- 🛡️ Acessível (semântica, contraste, navegação por teclado)
- 🔍 SEO (Open Graph + JSON-LD)
- 📱 Responsivo (mobile-first)
- 📞 CTA para WhatsApp e e-mail

## Como usar

1. **Crie um repositório no GitHub** (público ou privado).
2. Envie (upload) os arquivos deste projeto para a raiz do repositório.
3. Acesse **Settings ▸ Pages** e em **Build and deployment** escolha:
   - **Source**: *Deploy from a branch* (branch `main`, pasta `/`), ou
   - **GitHub Actions** usando o workflow incluso (veja abaixo).
4. Aguarde a publicação. Seu site ficará acessível em `https://SEU_USUARIO.github.io/NOME_DO_REPO/`.

> **Dica:** Edite os placeholders em `index.html` (`{{NOME_DA_PROFISSIONAL}}`, `{{EMAIL}}`, `{{DDD_NUMERO}}`, etc.).

## Editando conteúdo (GitHub = banco de dados)

- Abra `data/services.json`, `data/testimonials.json` e `data/faq.json` no próprio GitHub e clique em **Edit**.
- Confirme com **Commit changes**. O site lê esses arquivos em tempo de execução (via `fetch`), então alterações aparecem assim que você recarrega a página.

### Estrutura dos arquivos JSON
- `data/services.json` – lista de serviços com `titulo`, `descricao`, `preco`, `topicos`.
- `data/testimonials.json` – depoimentos com `texto`, `autor` (iniciais) e `idade` (opcional).
- `data/faq.json` – perguntas frequentes com `pergunta` e `resposta`.

> **Privacidade:** publique apenas depoimentos **anônimos** e com consentimento. Evite dados sensíveis.

## WhatsApp com mensagem pronta
Em `index.html`, substitua `{{DDD_NUMERO}}` por algo como `55SEU_DDI_DDD_NUMERO` (ex.: `5551999999999`) e `{{MENSAGEM_URLENC}}` por uma mensagem URL-encoded (o texto padrão pode ser: `Olá! Gostaria de agendar uma conversa inicial.` → `Ol%C3%A1!%20Gostaria%20de%20agendar%20uma%20conversa%20inicial.`).

## Deploy via GitHub Actions (opcional)
O arquivo `.github/workflows/pages.yml` já está configurado para publicar no GitHub Pages. Ative em **Settings ▸ Pages ▸ Build and deployment ▸ GitHub Actions** e rode o workflow.

## Formulário gravando no GitHub (opcional)
Se quiser **registrar solicitações** diretamente no GitHub (usando o GitHub como banco de dados), recomenda-se um **endpoint serverless** que crie uma *Issue* no repositório. Fluxo sugerido:

1. Crie um **token de acesso** (PAT) com escopos finos (apenas `issues:write`) ou instale um **GitHub App**.
2. Hospede um endpoint (Cloudflare Workers / Vercel Functions / Netlify Functions).
3. No endpoint, receba os campos do formulário e chame a API `POST /repos/:owner/:repo/issues` para abrir uma nova issue com título e corpo contendo os dados do lead.
4. No site, faça `fetch` para **seu** endpoint (nunca diretamente para a API do GitHub com o token no front-end!).

> Essa abordagem mantém o GitHub como armazenamento (Issues) e não expõe segredos no navegador.

## Personalização
- Cores e tipografia em `assets/css/styles.css`.
- Textos de seções em `index.html`.
- Imagens: substitua os placeholders na pasta `images/` e nos `src`.

## Licenças
- As imagens de exemplo são do Unsplash (uso livre). Substitua por suas fotos/logotipo.
- O código desta landing page é de uso livre para fins comerciais.
