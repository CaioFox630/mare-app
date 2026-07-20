# Maré — painel de hidratação (PWA)

App de hidratação com cálculo de meta de água, IMC, lembretes sonoros e
notificações. É um **PWA** (Progressive Web App): um site que, ao ser
"adicionado à tela inicial" do celular, abre como um aplicativo, em tela
cheia, sem barra de endereço do navegador.

## Estrutura dos arquivos

```
mare-app/
├── index.html      → o app inteiro (HTML + CSS + JS)
├── manifest.json    → nome, ícone e modo "standalone" do app
├── sw.js             → service worker (permite instalar e funcionar offline)
├── icons/            → ícones do app em vários tamanhos
└── README.md
```

Todos os dados (perfil, litros bebidos, lembretes) ficam salvos **só no
aparelho do usuário** (localStorage do navegador) — não há servidor nem
banco de dados.

---

## Passo a passo: publicar no GitHub Pages

### 1. Criar o repositório
1. Acesse [github.com](https://github.com) e faça login (ou crie uma conta).
2. Clique em **New repository**.
3. Dê um nome, por exemplo `mare-app`. Deixe como **Public**.
4. Não marque "Add a README" (você já tem um). Clique em **Create repository**.

### 2. Subir os arquivos
Na página do repositório recém-criado:
1. Clique em **uploading an existing file** (ou "Add file" → "Upload files").
2. Arraste **todos os arquivos e a pasta `icons/`** desta pasta `mare-app`
   para dentro da área de upload (mantendo a estrutura: `index.html`,
   `manifest.json`, `sw.js` e a pasta `icons` na raiz do repositório).
3. Escreva uma mensagem de commit, ex: "primeira versão do app", e clique em
   **Commit changes**.

*(Alternativa via linha de comando, se preferir git:)*
```bash
cd mare-app
git init
git add .
git commit -m "primeira versão do app"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/mare-app.git
git push -u origin main
```

### 3. Ativar o GitHub Pages
1. No repositório, vá em **Settings** (aba no topo).
2. No menu lateral, clique em **Pages**.
3. Em **Source**, selecione **Deploy from a branch**.
4. Em **Branch**, escolha `main` e a pasta `/ (root)`. Clique em **Save**.
5. Aguarde 1–2 minutos. O GitHub vai mostrar o link do site, algo como:
   `https://SEU-USUARIO.github.io/mare-app/`

### 4. Instalar no celular
1. Abra o link acima **no navegador do celular** (Chrome no Android, Safari
   no iPhone).
2. **Android (Chrome):** toque no menu (⋮) → **Adicionar à tela inicial** /
   **Instalar app**. Um banner amarelo "Instalar o Maré" também pode aparecer
   sozinho — é só tocar em **Instalar**.
3. **iPhone (Safari):** toque no ícone de compartilhar (□↑) → **Adicionar à
   Tela de Início**.
4. Abra o app pelo ícone criado na tela inicial — ele abre em tela cheia,
   sem a barra de endereço do navegador.

---

## Sobre os lembretes sonoros

- Ative em **Lembretes → Lembretes ativos** e escolha o intervalo.
- Na primeira vez, o navegador vai pedir permissão para notificações — aceite
  para receber o aviso mesmo com a tela bloqueada ou o app em segundo plano
  (Android costuma manter isso funcionando bem enquanto o app está aberto ou
  recentemente aberto).
- Um sino é tocado (som gerado pelo próprio app, não precisa de internet)
  toda vez que o lembrete dispara, e o app mostra uma notificação do sistema
  se a permissão tiver sido concedida.
- **Limitação importante:** como este é um site instalável (PWA) e não um
  app de loja, os lembretes só disparam enquanto o aparelho está ligado e o
  navegador/app não foi totalmente fechado da memória. Para notificações que
  cheguem mesmo com o app completamente fechado por horas, seria necessário
  um servidor de push (ex: Firebase Cloud Messaging) — isso está fora do
  escopo de um site estático no GitHub Pages. Uma alternativa prática é
  deixar o app aberto em segundo plano ou usar os lembretes/alarmes nativos
  do próprio celular como reforço.
- Ajuste o **Não perturbe** para evitar sons durante a madrugada.

## Atualizando o app depois

Sempre que quiser mudar algo, edite os arquivos e suba novamente (upload ou
`git push`). O GitHub Pages atualiza automaticamente em 1–2 minutos. Se o
celular mostrar a versão antiga, feche o app pela lista de recentes e abra
de novo (o service worker atualiza o cache automaticamente).
