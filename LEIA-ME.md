# Master Green — Distribuidor de WhatsApp + Painel Admin

Sistema de **rodízio de WhatsApp** (round-robin): cada visitante que clica é
enviado para um número diferente, em ordem, distribuindo os contatos igualmente.
Um **painel admin** permite adicionar/remover números e ver quantos cliques cada
um recebeu.

## Arquivos
- `master-green-landing.html` — a landing page (página pública).
- `admin.html` — painel administrativo (acesso com senha).
- `firebase-config.js` — onde você cola a configuração do seu Firebase.
- `firestore.rules` — regras de segurança para colar no Firebase.

---

## Passo a passo (uma vez só)

### 1. Criar o projeto no Firebase
1. Acesse https://console.firebase.google.com e clique em **Adicionar projeto**.
2. Dê um nome (ex.: `master-green`) e conclua a criação (pode pular o Analytics).

### 2. Criar o banco (Firestore)
1. No menu lateral: **Criação → Firestore Database → Criar banco de dados**.
2. Escolha o modo **Produção** e uma região (ex.: `southamerica-east1` / São Paulo).

### 3. Colar as regras de segurança
1. Em **Firestore Database → Regras**.
2. Apague o conteúdo e cole **exatamente** o que está no arquivo `firestore.rules`.
3. Clique em **Publicar**.

### 4. Ativar o login do admin
1. No menu: **Criação → Authentication → Começar**.
2. Aba **Sign-in method** → ative **E-mail/senha**.
3. Aba **Users → Adicionar usuário**: cadastre seu e-mail e uma senha.
   (Esse será o login do painel `admin.html`.)

### 5. Pegar a configuração e colar no projeto
1. Clique no ⚙️ (ao lado de "Visão geral do projeto") → **Configurações do projeto**.
2. Em **Seus apps**, clique no ícone **Web** `</>` e registre um app (dê um apelido).
3. Copie o objeto `firebaseConfig` que aparece.
4. Abra o arquivo **`firebase-config.js`** e cole os valores nos campos correspondentes.

### 6. Publicar os arquivos
Suba os 4 arquivos (`master-green-landing.html`, `admin.html`,
`firebase-config.js` e — opcionalmente — este LEIA-ME) para sua hospedagem
estática (Netlify, Vercel, GitHub Pages, Hostinger, etc.), **na mesma pasta**.

> Importante: por usar módulos (`type="module"`), os arquivos precisam ser
> acessados por **http/https** (um servidor), não abrindo direto com duplo
> clique no `file://`. Para testar localmente, rode um servidor simples, ex.:
> `npx serve` ou `python -m http.server` dentro da pasta.

---

## Como usar
- **Cadastrar números:** abra `seusite.com/admin.html`, faça login e adicione os
  WhatsApps (rótulo + número com DDI/DDD, ex.: `5599999999999`).
- **Rodízio:** assim que houver números ativos, os botões da landing começam a
  distribuir os cliques automaticamente, um para cada número, em ordem.
- **Estatísticas:** o painel mostra, em tempo real, o total de cliques, quantos
  números estão ativos e qual está **indo mais** (🔥 Mais procurado), além da
  participação (%) de cada número.
- **Ativar/Desativar:** use o botão de liga/desliga para tirar um número do
  rodízio sem excluí-lo.

## Observações
- A distribuição é **igual (round-robin)**: cada clique vai para o próximo da fila.
- Se nenhum número estiver cadastrado/ativo, o botão usa um link de fallback
  (`https://wa.me/`) — cadastre ao menos um número para evitar isso.
- O plano gratuito do Firebase (Spark) é mais que suficiente para esse uso.
