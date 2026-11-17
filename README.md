# Links únicos para baixar os apps Saquarema

Um link por app. Cada página detecta o dispositivo e redireciona:

- **iPhone / iPad** → App Store
- **Android** → Google Play
- **Desktop** → página com os dois botões e um QR code que aponta para o próprio link

| App | Pasta | Link (após publicar) |
|---|---|---|
| Saquarema Cartão | `cartao/` | `https://SEU-USUARIO.github.io/SEU-REPO/cartao/` |
| Saquarema Estabelecimento | `estabelecimento/` | `https://SEU-USUARIO.github.io/SEU-REPO/estabelecimento/` |

A raiz (`index.html`) lista os dois apps e não redireciona.

## Configurar

Os links das lojas ficam no bloco `CONFIG`, no topo de `cartao/index.html` e de `estabelecimento/index.html`:

```js
var CONFIG = {
  appName: "Saquarema Cartão",
  ios: "https://apps.apple.com/us/app/saquarema-cart%C3%A3o/id6769044226",
  android: "https://play.google.com/store/apps/details?id=programa.saquarema.cartao"
};
```

Opcional: coloque um `icon.png` (512x512) dentro da pasta de cada app para exibir o ícone. Se não houver, a imagem é escondida.

Para adicionar outro app, copie uma das pastas, renomeie e edite o `CONFIG`.

## Publicar no GitHub Pages

1. Crie um repositório no GitHub (ex.: `apps-saquarema`) e suba estes arquivos na branch `main`.
2. Em **Settings → Pages**, em *Source* escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`.
3. Em 1 ou 2 minutos o link fica disponível em `https://SEU-USUARIO.github.io/apps-saquarema/`.

```bash
git init
git add .
git commit -m "Página de redirect para as lojas"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/apps-saquarema.git
git push -u origin main
```

### Domínio próprio (opcional)

Para usar algo como `app.seudominio.com.br`:

1. Crie um arquivo `CNAME` na raiz contendo só o domínio (ex.: `app.seudominio.com.br`).
2. No DNS do domínio, crie um registro **CNAME** apontando `app` para `SEU-USUARIO.github.io`.
3. Em **Settings → Pages**, informe o domínio e marque **Enforce HTTPS**.

## Testar

- No celular: abra o link e veja se cai na loja certa.
- No desktop: deve aparecer a página com os botões e o QR code.
- Para ver a página sem redirecionar, mesmo no celular: adicione `?noredirect=1` ao final do link.
- No Chrome DevTools, o modo de dispositivo (Ctrl/Cmd + Shift + M) simula iPhone e Android.

## Observações

- O redirect roda no navegador via JavaScript. O GitHub Pages não permite redirect no servidor; para isso seria preciso uma Edge Function (Vercel, Cloudflare Workers etc.).
- Quem abre o link pelo navegador interno do Instagram ou do WhatsApp também é redirecionado normalmente, porque o User-Agent continua sendo de iOS ou Android.
- Se depois quiser que o link abra o app quando ele já estiver instalado, dá para adicionar Universal Links / App Links neste mesmo domínio (arquivos em `.well-known/`).
