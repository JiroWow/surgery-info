# 手術資料チャット

顎矯正手術の病院資料をもとに、家族が自然言語で質問できるチャットボット。

## セットアップ

### 1. Gemini APIキーを取得
[Google AI Studio](https://aistudio.google.com/apikey) でAPIキーを取得する。

### 2. index.html を編集

`index.html` の先頭付近にある2行を書き換える:

```js
const GEMINI_API_KEY  = "AIzaSy...";     // ← 取得したAPIキー
const ACCESS_PASSWORD = "任意のパスワード"; // ← 家族に共有するパスワード
```

### 3. GitHub Pagesを有効化

Settings → Pages → Source: `main` branch / `/(root)` → Save

数分後に `https://<username>.github.io/surgery-docs/` が発行される。

### 4. URLを家族に共有

---

## 資料を追加する（OCR）

写真をClaudeとのConversationに貼り付けて「documents.jsonのchunk形式で出力して」と依頼。
出力されたchunksを `documents.json` に追記してpushする。

### chunk形式

```json
{
  "id": 1,
  "source": "術前説明書 p.1",
  "text": "Claudeが要約した内容…",
  "categories": ["術前準備", "食事制限"]
}
```

カテゴリは以下から選ぶ（複数可）:
- `術前準備` / `手術当日` / `食事制限` / `入院準備` / `退院後` / `その他`

---

## モデル

`gemini-2.5-flash-lite`（無料枠: RPM最大・RPD 1,500）
