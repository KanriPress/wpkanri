# WPKanri

[![Release](https://img.shields.io/github/v/release/KanriPress/wpkanri?label=latest)](https://github.com/KanriPress/wpkanri/releases/latest)
[![License: GPL v2+](https://img.shields.io/badge/license-GPL%20v2%2B-blue)](./license.txt)
[![WordPress 6.0+](https://img.shields.io/badge/WordPress-6.0%2B-21759b)](https://wordpress.org/)
[![PHP 7.4+](https://img.shields.io/badge/PHP-7.4%20--%208.5-777bb4)](https://www.php.net/)

**WordPress connector plugin for KanriPress Helper** — 管理サイドのクラウド保守サービスへ WordPress サイトを 1 クリックで接続する軽量コネクタプラグイン。

> 本体サービスは [helper.kanripress.com](https://helper.kanripress.com) で提供されます。本リポジトリはプラグイン単体の配信を担います。

---

## ダウンロード

👉 **[最新版 `wpkanri.zip` をダウンロード](https://github.com/KanriPress/wpkanri/releases/latest)**

WordPress 管理画面で「プラグイン → 新規追加 → プラグインのアップロード」から ZIP を選択してインストールしてください。インストール後は WP 標準の更新通知で自動的に新しいバージョンの案内が届きます。

将来は WordPress.org プラグインディレクトリからも配信予定です。

---

## 主な機能

- ✅ **ワンクリック接続** — OAuth 風リダイレクトで API キー自動発行
- ✅ **コアチェックサム改ざんスキャン** — wp-admin / wp-includes を wp.org チェックサム DB と照合
- ✅ **ヘルスエンドポイント** — `/wp-json/wpkanri/v1/health` で外部死活監視
- ✅ **Core Web Vitals (RUM)** — web-vitals.js による LCP / INP / CLS / FCP / TTFB 自動収集
- ✅ **PHP エラー監視** — E_WARNING + Fatal を非ブロッキングで送信、AI 解析付き
- ✅ **CO2 トラッキング** — ページ転送バイト数からカーボン計測
- ✅ **ホワイトラベル対応** — 定数で通知・ブランド名を差し替え可能
- ✅ **自動更新** — Plugin Update Checker 経由で GitHub Releases を監視

---

## 動作環境

| 項目 | 最低要件 | 動作確認済み |
|---|---|---|
| WordPress | 6.0 | 6.9.x (全パッチリリース対応) |
| PHP | 7.4 | 7.4 / 8.0 / 8.2 / 8.4 / 8.5 |

---

## インストール手順

1. [最新リリース](https://github.com/KanriPress/wpkanri/releases/latest) から `wpkanri.zip` をダウンロード
2. WordPress 管理画面 → **プラグイン** → **新規追加** → **プラグインのアップロード**
3. ZIP を選択して「今すぐインストール」→「プラグインを有効化」
4. 有効化直後に「設定 → WPKanri」へ誘導されます
5. 「接続する」ボタンで KanriPress Helper にリダイレクトされ、承認すると API キーが自動発行されます
6. 「今すぐスキャン」で初回改ざんスキャンを実行

---

## エージェンシー向けカスタマイズ

`wp-config.php` に以下の定数を定義することで、顧客側への露出を抑えられます:

```php
// 全画面の通知・有効化リダイレクト・KanriPress 文言を非表示
define( 'WPKANRI_WHITELABEL', true );

// 設定画面上のブランド名を差し替え
define( 'WPKANRI_BRAND_NAME', 'My Agency Care' );
define( 'WPKANRI_BRAND_DESCRIPTION', 'サイトを My Agency の保守クラウドに接続します。' );

// 自動更新をフォーク先から取得
define( 'WPKANRI_GITHUB_REPO', 'my-agency/my-fork' );

// 自動更新を完全に無効化
define( 'WPKANRI_DISABLE_AUTO_UPDATE', true );
```

または mu-plugin からフィルター経由で:

```php
add_filter( 'wpkanri_whitelabel_mode', '__return_true' );
add_filter( 'wpkanri_brand_name', fn() => 'My Agency Care' );
```

---

## 開発・ビルド

本リポジトリはリリース成果物の配信拠点です。ソースの直接編集は親モノレポ ([KanriPress/kanripress-helper](https://github.com/KanriPress/kanripress-helper)) 側で行い、`plugin-vX.Y.Z` タグ push で GitHub Actions が `wpkanri.zip` を生成してこのリポの Releases に添付します。

リリースフロー:

```bash
# モノレポ側で
git tag plugin-v0.0.4
git push origin plugin-v0.0.4
# → wpkanri.zip が自動ビルド＆Release 作成
```

---

## ライセンス

[GPL v2 or later](./license.txt) — WordPress 本体と同ライセンス。商用利用可。

同梱ライブラリ:

- [Plugin Update Checker](https://github.com/YahnisElsts/plugin-update-checker) v5.6 (MIT License) — 自動更新機構
- [web-vitals](https://github.com/GoogleChrome/web-vitals) v4 (Apache-2.0) — Core Web Vitals 計測

---

## サポート

- 🐛 [Issue を報告](https://github.com/KanriPress/wpkanri/issues)
- 🌐 [KanriPress Helper](https://helper.kanripress.com)
