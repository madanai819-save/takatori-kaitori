# 高価買取タカトル 公式サイト

大阪府枚方市・宮之阪駅徒歩2分の買取専門店「高価買取タカトル」の公式サイトです。
Vanilla HTML / CSS / JavaScriptのみで構成された静的サイトで、Netlifyでの公開を前提としています。

## ファイル構成

| ファイル | 役割 | 状態 |
| --- | --- | --- |
| `index.html` | トップページ（本体） | 公開用に修正済み |
| `thanks.html` | お問い合わせ送信完了ページ | 新規作成済み（`noindex`設定済み） |
| `images/storefront.jpg` | ファーストビューの店舗外観写真（1200×900px推奨） | **未配置。要アップロード** |
| `favicon.png` | ファビコン | **未配置。要アップロード** |
| `apple-touch-icon.png` | iOSホーム画面アイコン | **未配置。要アップロード** |
| `ogp.jpg` | SNSシェア用OGP画像（1200×630px推奨） | **未配置。要アップロード** |
| `タカとる.html` / `タカとる_backup.html` | 旧バージョンの下書き | 参考用。LINEリンクが `href="#"` のままなど古い不具合が残っているため、**公開フォルダには含めない**ことを推奨します |

画像はダミー画像を自動生成していません。`storefront.jpg`は`index.html`と同じ階層にある`images`フォルダの中（`images/storefront.jpg`）に配置してください。`favicon.png`・`apple-touch-icon.png`・`ogp.jpg`は従来通り`index.html`と同じ階層（ルート直下）に配置してください。
`storefront.jpg` が未配置でも、`index.html` 側で`onerror`によりフォールバックする実装になっているため、レイアウトが大きく崩れることはありません。

## Netlify Forms の設定手順（フォーム通知）

お問い合わせフォームは `data-netlify="true"` でNetlify Formsを利用する構成にしていますが、**通知先メールアドレスはHTMLだけでは設定できません**。以下の手順でNetlify管理画面から設定してください。

1. Netlify管理画面を開く
2. `Site configuration` → `Notifications` → `Form submission notifications`
3. `Add notification` → `Email notification` を選択
4. 対象フォームで `contact` を選択
5. 通知先メールアドレスに `takatoru.0801@gmail.com` を入力して保存

同じ手順は `index.html` 内のフォーム直前にもHTMLコメントで記載しています。

フォーム送信後は `action="/thanks.html"` により `thanks.html` へ遷移します。初回デプロイ後、Netlifyの管理画面で対象フォーム（`contact`）が検出されているか必ず確認してください。

## LINE公式アカウント

すべてのLINE関連リンク（ヘッダー・ファーストビュー・各CTA・固定フッター）は `https://lin.ee/ST5vdcT` に統一しました。
URLを変更する場合は、`index.html` 末尾のJavaScript内にある以下の1行のみ書き換えれば、ページ内のすべてのLINEリンクに反映されます。

```js
var LINE_URL = 'https://lin.ee/ST5vdcT';
```

## 公開前に人間が確認・対応すべき項目

- [ ] `storefront.jpg` / `favicon.png` / `apple-touch-icon.png` / `ogp.jpg` の実画像を配置する
- [ ] Netlify管理画面でフォーム通知先メール（`takatoru.0801@gmail.com`）を設定する
- [ ] 初回デプロイ後、実際にテスト送信してNetlify Forms側で受信・`thanks.html`への遷移を確認する
- [ ] 「最近の買取実績」セクション（`#results`、現在 `hidden` 属性で非表示）に実データが揃い次第、仮データを実データへ差し替えて `hidden` 属性を削除する
- [ ] 「お客様の声」の3枠（現在 `hidden` 属性で非表示）は、掲載許可を得たお客様の声のみ差し替えて `hidden` 属性を削除する
- [ ] Googleビジネスプロフィールの実URLを、「お客様の声」セクションの「Google口コミを見る」リンクに設定する（現在は店名でのGoogle検索リンクを仮設定）
- [ ] Googleマップの埋め込みiframe（アクセスセクションにコメントで記載）を実際の埋め込みURLに差し替える（現在は住所検索リンクのみ機能）
- [ ] 古物商許可番号・代表者名・プライバシーポリシー・特定商取引法に関する表記・利用規約のURLが確定次第、フッター内のHTMLコメント箇所に追記する（`index.html` フッター参照）
- [ ] 構造化データ（`PawnShop`）内の緯度・経度が実際の店舗位置と一致するか確認する
- [ ] 店舗・スタッフ紹介セクションの店内・スタッフ写真を実際の写真に差し替える

## 動作確認済みの内容

- HTMLタグの対応関係（開閉漏れなし）
- 構造化データ（PawnShop / FAQPage）2件のJSON構文
- スマートフォン幅375px・タブレット幅768px・PC幅1440pxでの横スクロールなし
- LINEリンク7箇所すべてが `https://lin.ee/ST5vdcT` に統一されていること
- 電話リンク（`tel:0728086532`）
- FAQのアコーディオン開閉・`aria-expanded`切り替え
- お問い合わせフォームの必須項目バリデーション（お名前・連絡方法・個人情報同意はネイティブHTML5バリデーション、電話番号またはメールアドレスのいずれか必須はJavaScriptバリデーション）で、条件を満たせばNetlifyへ通常どおりPOST送信されること
