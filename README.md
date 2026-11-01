# emondesu.github.io

全アプリ共通の開発者サイト。ビルド工程のない静的ファイルだけで構成し、フォルダをそのまま置けばどのホスティングでも同じ状態で公開できるようにしている。

公開 URL: https://emondesu.github.io/

## 構成

```
├── index.html     # 開発者トップ（アプリ一覧）
├── app-ads.txt    # AdMob の販売者認証。全アプリ共通（下記）
├── .nojekyll      # GitHub Pages の Jekyll 処理を止め、置いたファイルをそのまま配信させる
├── .github/ISSUE_TEMPLATE/  # 問い合わせ窓口（全アプリ共通・アプリ選択つき）
├── spotpocket/    # SpotPocket: index.html（LP）・support.html・privacy.html・assets/
├── ponsa/         # Ponsa: privacy.html（ponsa リポジトリの Actions が store/privacy-policy.html から自動同期）
├── qrcodechecker/ # QRCodeChecker: privacy.html（qrCodeChecker リポジトリの Actions が docs/PrivacyPolicy.md を HTML 化して自動同期）
└── <旧パス>/      # 旧 URL 用（下記「旧 URL」）。触らない
```

問い合わせ: https://github.com/emondesu/emondesu.github.io/issues （全アプリ共通）

## 旧 URL（2026-11-01 移転）

各アプリのページは 2026-11-01 にアプリ別リポジトリから移した。旧 URL は配布済みアプリと App Store に登録済みのため、**このリポジトリの旧パスに転送ページを置いて生かしている**（アプリ別リポジトリの Pages は停止済み。GitHub Pages では、同名のプロジェクトサイトが無いパスはこのユーザーサイトから配信される）。

| アプリ | 新しい URL（正） | 旧 URL（このリポジトリの旧パスで転送） |
|---|---|---|
| SpotPocket | `/spotpocket/`・`/spotpocket/support.html`・`/spotpocket/privacy.html` | `/spotpocket-pages/`・`/spotpocket-pages/support.html`・`/spotpocket-pages/privacy.html` |
| Ponsa | `/ponsa/privacy.html` | `/ponsa-public/privacy-policy.html` |
| QRCodeChecker | `/qrcodechecker/privacy.html` | `/qrcodechecker-support/` |

- **`spotpocket-pages/config/remote-flags.json` は転送ページではなく本物**。SpotPocket の遠隔停止スイッチで、配布済みアプリがこの URL を直接読む。**消さない・移さない**。止め方は SpotPocket リポジトリの `docs/reference/metadata-policy.md`
- 旧パスの HTML には `<!-- legacy-path: served from emondesu.github.io -->` の目印がある（どちらのリポジトリから配信されているかの確認用）
- **旧パスのフォルダ名と同じ名前のリポジトリで Pages を有効にしないこと**（プロジェクトサイトが優先され、旧 URL と停止スイッチが乗っ取られる）
- SpotPocket のプライバシーポリシーの原稿は SpotPocket リポジトリの `appstore/privacy-policy.md`。本文を変えたら `spotpocket/privacy.html` も更新する（二重管理）

## 旧リポジトリの削除

`spotpocket-pages`・`ponsa-public`・`qrcodechecker-support` は 2026-11-01 時点で Pages 停止済み・どこからも使われていない（旧 URL は上記のとおりこのリポジトリから配信）。削除はリポジトリの Settings → Delete this repository（または `gh auth refresh -s delete_repo` のうえ `gh repo delete emondesu/<name>`）。削除前の確認:

1. 旧 URL が目印つきで返ること: `curl -s https://emondesu.github.io/spotpocket-pages/ | grep legacy-path`（ponsa-public・qrcodechecker-support も同様）と `curl -s https://emondesu.github.io/spotpocket-pages/config/remote-flags.json`
2. 同期 Actions がこのリポジトリに向いていること（ponsa: main 反映済み／qrCodeChecker: `site-migration` ブランチを main へ取り込み済みか）と、各リポジトリの PAT シークレット（`PONSA_PUBLIC_PAT`・`SYNC_PAT`）がこのリポジトリに書き込めること
3. **`spotpocket-pages` だけの注意**: 配布済みの SpotPocket（2026-11 以前のビルド）の設定画面「お問い合わせ」は `github.com/emondesu/spotpocket-pages/issues` を直接開く。削除するとこのリンクは 404 になる（Issues は過去 0 件。新しいビルドは共通サイトの Issues を開く）。気になるなら、新リンク入りのバージョンが行き渡ってから削除する

## app-ads.txt

- AdMob はアプリの App Store「マーケティング URL」のドメイン直下（`https://emondesu.github.io/app-ads.txt`）だけを見に行く。サブフォルダの下に置いても認識されない
- 同じ AdMob アカウント（`pub-7958257358584771`）のアプリなら、この1行で全アプリ分を兼ねる。アプリが増えても行を足す必要はない。各アプリのマーケティング URL をこのドメインの下に揃えること
- 中身は公開前提の情報のみ（パブリッシャー ID・Google の認証 ID）。秘密情報ではない
- 別の広告ネットワークを足すときは、そのネットワークが案内する行を追記する

## アプリを追加する

1. `<app>/` フォルダを作り、`privacy.html` 等を置く（既存アプリのページをコピーして文言を差し替える）
2. `index.html` の一覧に1項目足す
3. App Store Connect のプライバシーポリシー URL・サポート URL・マーケティング URL をこのドメインの下に設定する

URL を一度 App Store やアプリ本体に登録したら、ページを動かさないこと（動かすなら、このリポジトリの旧パスに転送ページを残す）。

## 別のホスティングへ公開する

ビルドは不要。リポジトリのルートをそのまま公開ディレクトリにする。

| 公開先 | 設定 |
|---|---|
| GitHub Pages（現行） | リポジトリ名 `emondesu.github.io` の main ブランチ / ルートから自動公開 |
| Cloudflare Pages / Netlify | リポジトリを接続し、ビルドコマンド: なし、公開ディレクトリ: `/`（ルート） |
| 任意の Web サーバー・S3 等 | ファイル一式をドキュメントルートへコピー |

**注意: ファイルは持ち運べるが URL は持ち運べない。** `emondesu.github.io` のアドレスは GitHub を離れると使えなくなり、App Store に登録した URL やアプリに埋め込んだ URL が切れる。ホスティングを移す可能性があるなら、先に独自ドメインを取り、そのドメインで公開・登録しておくこと（独自ドメインなら裏の公開先を替えても URL は変わらない）。
