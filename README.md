# emondesu.github.io

全アプリ共通の開発者サイト。ビルド工程のない静的ファイルだけで構成し、フォルダをそのまま置けばどのホスティングでも同じ状態で公開できるようにしている。

公開 URL: https://emondesu.github.io/

## 構成

```
├── index.html     # 開発者トップ（アプリ一覧）
├── app-ads.txt    # AdMob の販売者認証。全アプリ共通（下記）
├── .nojekyll      # GitHub Pages の Jekyll 処理を止め、置いたファイルをそのまま配信させる
└── <app>/         # アプリごとのページ（privacy.html / support.html など）
```

## app-ads.txt

- AdMob はアプリの App Store「マーケティング URL」のドメイン直下（`https://emondesu.github.io/app-ads.txt`）だけを見に行く。サブフォルダの下に置いても認識されない
- 同じ AdMob アカウント（`pub-7958257358584771`）のアプリなら、この1行で全アプリ分を兼ねる。アプリが増えても行を足す必要はない。各アプリのマーケティング URL をこのドメインの下に揃えること
- 中身は公開前提の情報のみ（パブリッシャー ID・Google の認証 ID）。秘密情報ではない
- 別の広告ネットワークを足すときは、そのネットワークが案内する行を追記する

## アプリを追加する

1. `<app>/` フォルダを作り、`privacy.html` 等を置く（既存アプリのページをコピーして文言を差し替える）
2. `index.html` の一覧に1項目足す
3. App Store Connect のプライバシーポリシー URL・サポート URL・マーケティング URL をこのドメインの下に設定する

既存アプリのページ（`spotpocket-pages` / `ponsa-public` / `qrcodechecker-support` の各リポジトリ）は、アプリ本体や App Store に URL が登録済みのため現状維持。移すときは App Store の URL 変更（新バージョンの提出が必要）とセットで行う。

## 別のホスティングへ公開する

ビルドは不要。リポジトリのルートをそのまま公開ディレクトリにする。

| 公開先 | 設定 |
|---|---|
| GitHub Pages（現行） | リポジトリ名 `emondesu.github.io` の main ブランチ / ルートから自動公開 |
| Cloudflare Pages / Netlify | リポジトリを接続し、ビルドコマンド: なし、公開ディレクトリ: `/`（ルート） |
| 任意の Web サーバー・S3 等 | ファイル一式をドキュメントルートへコピー |

**注意: ファイルは持ち運べるが URL は持ち運べない。** `emondesu.github.io` のアドレスは GitHub を離れると使えなくなり、App Store に登録した URL やアプリに埋め込んだ URL が切れる。ホスティングを移す可能性があるなら、先に独自ドメインを取り、そのドメインで公開・登録しておくこと（独自ドメインなら裏の公開先を替えても URL は変わらない）。
