# Compras Binho

Sistema de **compras e almoxarifado** da Binho Transportes (protótipo funcional), com publicação automática
do site e geração dos apps de **Android** e **iPhone** a partir do mesmo arquivo.

> **Mantenha este repositório PRIVADO.** O sistema traz dados reais dos fornecedores exportados do SSW
> (CPFs, contas bancárias, chaves PIX) e a chave de assinatura do app Android.

## O que tem aqui

```
compras-binho/
├── site/
│   ├── index.html            ← o sistema inteiro (um único arquivo)
│   ├── teste-camera.html     ← teste rápido da câmera ao vivo
│   └── _headers              ← libera a câmera e protege o site (Cloudflare Pages)
├── apps/
│   ├── android/              ← app Android (WebView com câmera liberada)
│   └── ios/                  ← app iPhone (WebView, TestFlight)
├── docs/
│   ├── PUBLICAR-SITE.md      ← publicar o site com login (Cloudflare Pages + Access)
│   ├── GUIA-ANDROID.md       ← gerar e instalar o APK
│   └── GUIA-IPHONE.md        ← conta Apple, TestFlight
├── scripts/atualizar-sistema.sh
└── .github/workflows/
    ├── site-cloudflare.yml   ← publica o site a cada envio
    ├── android-apk.yml       ← gera o APK a cada envio
    └── ios-testflight.yml    ← compila o app iPhone e envia ao TestFlight (manual)
```

`site/index.html` é a fonte única: os workflows copiam esse arquivo para dentro dos apps na hora do build.

## Passo 1 — Colocar no GitHub (sem linha de comando)

O jeito mais fácil é o **GitHub Desktop** (Windows ou Mac):

1. Crie uma conta em <https://github.com> e instale o **GitHub Desktop** (<https://desktop.github.com>).
2. Descompacte este pacote. No GitHub Desktop: **File > Add local repository**, escolha a pasta `compras-binho`
   e, quando ele avisar que não é um repositório, clique em **create a repository**.
3. Clique em **Publish repository**, deixe marcado **Keep this code private** e confirme.

Pelo site também funciona (**New repository > Private > uploading an existing file**, arrastando o conteúdo da pasta),
mas confira se a pasta oculta `.github` foi junto: sem ela os workflows não aparecem na aba **Actions**.
No Windows, ative "Itens ocultos" no Explorador de Arquivos antes de arrastar.

## Passo 2 — Ativar o que você precisa

| Quero | Faça | Precisa de |
|---|---|---|
| Usar no navegador do celular, com câmera ao vivo | [docs/PUBLICAR-SITE.md](docs/PUBLICAR-SITE.md) | Conta gratuita na Cloudflare |
| App Android com câmera liberada | [docs/GUIA-ANDROID.md](docs/GUIA-ANDROID.md) | Nada além do GitHub |
| App iPhone | [docs/GUIA-IPHONE.md](docs/GUIA-IPHONE.md) | Conta Apple Developer (US$ 99/ano) |

O workflow do Android roda sozinho depois do primeiro envio. O do site espera os segredos da Cloudflare;
até lá ele aparece com erro na aba Actions, avisando quais segredos faltam.

## Atualizar o sistema

1. Substitua `site/index.html` pela versão nova (ou `./scripts/atualizar-sistema.sh caminho/sistema-compras.html`).
2. No GitHub Desktop: escreva um resumo da mudança, **Commit to main** e **Push origin**.
3. Automático: o site é republicado e um APK novo é gerado. Para o iPhone, rode o workflow do TestFlight.

## Limites do protótipo

- Os dados ficam só na memória do navegador/app: recarregar volta aos dados de exemplo. Para uso definitivo falta
  um servidor com banco de dados e login próprio.
- Integrações com SSW e Mitra são simuladas; a lista de fornecedores é uma exportação do SSW embutida no arquivo.
