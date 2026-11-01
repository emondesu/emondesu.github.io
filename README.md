# emondesu.github.io

全アプリ共通の開発者サイト。ビルド工程のない静的ファイルだけで構成し、フォルダをそのまま置けばどのホスティングでも同じ状態で公開できるようにしている。

公開 URL: https://emondesu.github.io/

## 構成

```
├── index.html     # 開発者トップ（アプリ一覧）
├── app-ads.txt    # AdMob の販売者認証。全アプリ共通（下記）
├── .nojekyll      # GitHub Pages の Jekyll 処理を止め、置いたファイルをそのまま配信させる
├── spotpocket/    # SpotPocket: index.html（LP）・support.html・privacy.html・assets/
├── ponsa/         # Ponsa: privacy.html
└── qrcodechecker/ # QRCodeChecker: privacy.html
```

各アプリのページは 2026-11-01 にアプリ別リポジトリから移した。

| アプリ | 新しい URL（正） | 旧 URL（転送ページとして残置） |
|---|---|---|
| SpotPocket | `/spotpocket/`・`/spotpocket/support.html`・`/spotpocket/privacy.html` | `/spotpocket-pages/`・`/spotpocket-pages/support.html`・`/spotpocket-pages/privacy.html` |
| Ponsa | `/ponsa/privacy.html` | `/ponsa-public/privacy-policy.html` |
| QRCodeChecker | `/qrcodechecker/privacy.html` | `/qrcodechecker-support/` |

- 旧 URL は配布済みアプリと App Store に登録済みのため、旧リポジトリに転送ページ（meta refresh）を置いて残している。**旧リポジトリは削除しないこと**
- **SpotPocket の遠隔停止スイッチ `remote-flags.json` は移していない**。配布済みアプリが `https://emondesu.github.io/spotpocket-pages/config/remote-flags.json` を直接読むため、正は旧リポジトリ `spotpocket-pages` の `config/` のまま（転送ページでは JSON を読めない）
- 問い合わせ先の GitHub Issues は各旧リポジトリのまま（`spotpocket-pages/issues`・`qrcodechecker-support/issues`）
- SpotPocket のプライバシーポリシーの原稿は SpotPocket リポジトリの `appstore/privacy-policy.md`。本文を変えたら `spotpocket/privacy.html` も更新する（二重管理）

## app-ads.txt

- AdMob はアプリの App Store「マーケティング URL」のドメイン直下（`https://emondesu.github.io/app-ads.txt`）だけを見に行く。サブフォルダの下に置いても認識されない
- 同じ AdMob アカウント（`pub-7958257358584771`）のアプリなら、この1行で全アプリ分を兼ねる。アプリが増えても行を足す必要はない。各アプリのマーケティング URL をこのドメインの下に揃えること
- 中身は公開前提の情報のみ（パブリッシャー ID・Google の認証 ID）。秘密情報ではない
- 別の広告ネットワークを足すときは、そのネットワークが案内する行を追記する

## アプリを追加する

1. `<app>/` フォルダを作り、`privacy.html` 等を置く（既存アプリのページをコピーして文言を差し替える）
2. `index.html` の一覧に1項目足す
3. App Store Connect のプライバシーポリシー URL・サポート URL・マーケティング URL をこのドメインの下に設定する

URL を一度 App Store やアプリ本体に登録したら、ページを動かさないこと（動かすなら旧 URL に転送ページを残す）。

## 別のホスティングへ公開する

ビルドは不要。リポジトリのルートをそのまま公開ディレクトリにする。

| 公開先 | 設定 |
|---|---|
| GitHub Pages（現行） | リポジトリ名 `emondesu.github.io` の main ブランチ / ルートから自動公開 |
| Cloudflare Pages / Netlify | リポジトリを接続し、ビルドコマンド: なし、公開ディレクトリ: `/`（ルート） |
| 任意の Web サーバー・S3 等 | ファイル一式をドキュメントルートへコピー |

**注意: ファイルは持ち運べるが URL は持ち運べない。** `emondesu.github.io` のアドレスは GitHub を離れると使えなくなり、App Store に登録した URL やアプリに埋め込んだ URL が切れる。ホスティングを移す可能性があるなら、先に独自ドメインを取り、そのドメインで公開・登録しておくこと（独自ドメインなら裏の公開先を替えても URL は変わらない）。
