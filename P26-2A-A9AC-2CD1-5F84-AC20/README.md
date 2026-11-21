# Projeto #11: Controle Financeiro Pessoal

- **Modalidade:** Projeto Oficial Sorteado (Valendo 100 pontos)
- **Estudante:** Gabriel Teixeira Scholles
- **Turma:** 2A
- **Chave Única:** `P26-2A-A9AC-2CD1-5F84-AC20`
- **URL_CLOUDFLARE:** https://trabalho-financeiro-pessoal.pages.dev

---

## Especificação do Projeto

Desenvolva uma aplicação de livro-caixa para registro de receitas e despesas categorizadas. A interface em HTML e JavaScript puro deve apresentar formulários com validação de tipos monetários, filtros por mês/categoria e um painel superior que resume o saldo líquido atual do usuário autenticado via Discord.

Todas as transações financeiras são gravadas no banco de dados Cloudflare D1 associadas à credencial OAuth2 do estudante. Além das operações básicas de criação, leitura, atualização e exclusão (CRUD), o código JavaScript no cliente deve construir gráficos de barras horizontais ou colunas utilizando exclusivamente elementos <div> e estilização CSS proporcional aos percentuais gastos em cada categoria.

---

## Como Publicar esta Subpasta no Cloudflare Pages + D1 + Discord OAuth2

1. No painel da Cloudflare (**Workers & Pages** → **Create** → **Pages** → **Connect to Git**), selecione o seu fork do repositório `Avalia2026-2`.
2. Configure os parâmetros de build apontando para esta subpasta:
   - **Root directory (Diretório raiz):** `P26-2A-A9AC-2CD1-5F84-AC20`
   - **Build command:** *(deixe em branco — HTML/CSS/JS puro)*
   - **Build output directory:** `public`
3. Crie o banco de dados D1 e aplique a migração inicial (no terminal do laboratório usando Scoop):
   ```powershell
   cd P26-2A-A9AC-2CD1-5F84-AC20
   npx.cmd wrangler d1 create db-p26-2a-a9ac-2cd1-5f84-ac20
   # Copie o database_id gerado para o arquivo wrangler.jsonc e execute:
   npx.cmd wrangler d1 migrations apply DB --remote
   ```
4. **Vincule o Banco D1 ao seu Cloudflare Pages (Obrigatório para ativar env.DB):**
   - No painel da Cloudflare: acesse seu projeto Pages → **Settings** → **Functions** → **D1 database bindings**.
   - Clique em **Add binding**:
     - **Variable name:** `DB`
     - **D1 database:** selecione o banco que você criou (`db-p26-2a-a9ac-2cd1-5f84-ac20`).
5. **Configuração do Discord OAuth2 (Obrigatório para autenticação real):**
   - Acesse o **Discord Developer Portal** (https://discord.com/developers/applications) e crie uma nova Application.
   - Na aba **OAuth2**:
     - Copie o **Client ID** e gere o **Client Secret**.
     - Em **Redirects**, adicione a URL exata do deploy:
       `https://p26-2a-a9ac-2cd1-5f84-ac20.pages.dev/api/auth/discord/callback`
   - No painel do seu projeto no Cloudflare Pages:
     - Acesse **Settings** → **Environment variables**.
     - Adicione as variáveis de ambiente:
       - `DISCORD_CLIENT_ID`
       - `DISCORD_CLIENT_SECRET`
6. Atualize o campo **URL_CLOUDFLARE** no topo deste `README.md` com o endereço público gerado pela Cloudflare.
7. Na raiz do repositório, execute `node validar-local.mjs P26-2A-A9AC-2CD1-5F84-AC20` para validar todos os critérios antes de fazer o commit e abrir o Pull Request.
