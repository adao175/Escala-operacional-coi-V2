# Escala Operacional (COI) — publicação no GitHub Pages

## Estrutura deste repositório

```
index.html     → a página (visão, edição, relatórios) — quase não muda
dados.json     → o cadastro de operadores + as escalas geradas — muda toda vez que você publica algo
.nojekyll      → avisa o GitHub Pages pra servir os arquivos como estão, sem processar
README.md      → este arquivo
```

Quando alguém abre o site, o `index.html` busca o `dados.json` automaticamente
(sem usar cache do navegador) e mostra a escala que estiver lá. **Todo mundo
que acessa o link vê os mesmos dados**, porque todos estão lendo o mesmo
`dados.json` publicado no repositório — não é algo salvo no navegador de cada
pessoa.

## Configurar o GitHub Pages (só uma vez)

1. Crie um repositório novo (ou use um existente) e suba estes 4 arquivos na
   raiz, na branch `main`.
2. No repositório: **Settings → Pages**.
3. Em "Build and deployment" → Source: **Deploy from a branch**.
4. Branch: **main**, pasta: **/ (root)**. Salvar.
5. Em alguns minutos o GitHub mostra o link do site (algo como
   `https://SEU_USUARIO.github.io/NOME_DO_REPO/`). É esse link que você
   compartilha com o pessoal da empresa.

## Como publicar uma atualização da escala

Isso é tudo manual e não precisa de nenhum token, senha mestre ou script —
só você (ou quem tiver acesso de escrita no repositório) consegue publicar,
porque quem decide isso é o próprio GitHub, através da permissão do
repositório.

1. Abra o site (ou o `index.html` localmente), clique em **Editar escala**,
   faça suas alterações (gerar escala, editar células, cadastro de
   operadores, ausências etc.) normalmente.
2. Clique em **Salvar arquivo** (dentro do menu **Tools**, ou o atalho de
   "Salvar alterações" pra guardar rascunho só no seu navegador enquanto
   ainda está mexendo).
3. No popup, marque **todos os meses** que quer que continuem valendo pro
   site publicado (por padrão já vêm todos marcados) e confirme. Isso baixa
   um arquivo tipo `escala_coi_6_meses.json`.
4. Renomeie esse arquivo baixado para **`dados.json`** (exatamente esse
   nome, minúsculo).
5. Suba esse arquivo pro repositório, sobrescrevendo o `dados.json` que já
   está lá. Duas formas de fazer isso:
   - **Pelo site do GitHub** (mais simples): abra o repositório no
     github.com, entre na pasta, clique em "Add file → Upload files",
     arraste o `dados.json` novo, escreva uma mensagem tipo "Escala
     atualizada 28/08" e clique em "Commit changes".
   - **Pelo terminal/git** (se preferir): `git add dados.json`,
     `git commit -m "Escala atualizada"`, `git push`.
6. Pronto. O GitHub Pages redesenha o site sozinho, geralmente em menos de 1
   minuto. Quem recarregar a página já vê a versão nova — não precisa de
   deploy manual, build, nem nada além desse commit.

## Sobre cache

O `index.html` já busca o `dados.json` sempre "sem cache" (com um parâmetro
que muda a cada carregamento), então o navegador de quem acessa não vai
travar numa versão antiga do `dados.json`. O único atraso possível é o
tempinho normal que o próprio GitHub Pages leva pra propagar um commit novo
(quase sempre menos de 1 minuto, raramente passa de poucos minutos).

## Sobre o login de "Editar escala"

O botão "Editar escala" (usuário/senha, ou a senha mestre pra cadastrar um
novo admin) é só uma trava de conveniência dentro do próprio navegador de
quem está editando — evita clique acidental, não é uma segurança de verdade,
porque o código-fonte da página é público (qualquer um pode ver o código
com "Ver código-fonte"). Quem realmente decide o que fica público pra
empresa inteira é **quem tem permissão de escrita no repositório do
GitHub** — é esse commit do `dados.json` (passo 5 acima) que é o controle
de acesso real. Se quiser trocar a senha mestre (`SENHA_MESTRE`, hoje
`Coi@mestre`) por algo só seu, é só editar essa linha no `index.html` antes
de publicar.

## ⚠️ Sobre o index.html antigo

Se você já tinha publicado uma versão anterior desse site com um token do
GitHub (`ghp_...`) escrito no código — **revogue esse token agora** em
https://github.com/settings/tokens, se ainda não revogou. Ele ficou visível
pra qualquer visitante do site (bastava "Ver código-fonte"). O modelo novo
(esse aqui) não usa nenhum token: publicar é sempre um commit feito por
você, fora do navegador de quem visita o site.
