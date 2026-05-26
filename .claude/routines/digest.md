# ダイジェスト生成プロンプト

Web Searchツールを使って以下の情報を収集し、要約してください。
1. Anthropic 公式ブログの直近24時間の記事 (site:anthropic.com/news)
2. OpenAI 公式ブログの直近24時間の記事 (site:openai.com/blog)
3. Hacker News の本日上位スレッド (site:news.ycombinator.com)
4. Apple Developer の直近ニュース (site:developer.apple.com/news)
5. Apple Developer の直近リリース情報 (site:developer.apple.com/news/releases)
6. Swift.org ブログの直近記事 (site:swift.org/blog)
7. Swift Forums の直近の注目スレッド (site:forums.swift.org)
8. swift-evolution の直近のProposal・PR (site:github.com/swiftlang/swift-evolution)
9. GitHub Trending の本日分（言語問わず） (https://github.com/trending)
10. Reuters Technology の直近24時間の記事 (site:reuters.com/technology)
11. MarketWatch の直近24時間のIT関連ニュース (site:marketwatch.com "technology OR semiconductor OR AI OR earnings")
12. 東洋経済オンラインの直近IT関連記事 (site:toyokeizai.net "IT OR テクノロジー OR 半導体 OR AI")
13. TDnet 適時開示の直近IT関連開示 (site:tdnet.info)

## 選定基準

- Swift / iOS エンジニアとして実務に影響しうるものを優先する
- 評価額・資金調達より、技術的変化（API変更・新機能・破壊的変更）を重視する
- 「大きいニュース」より「見落とされがちだが重要なもの」を積極的に拾う

## 出力形式

ファイルパス: docs/YYYY-MM-DD.md（今日の日付に置き換えること）

### 日付の決定方法

ファイル名・見出しに使う日付は、以下のコマンドで取得したJST日付を使うこと：
```bash
TZ=Asia/Tokyo date +%Y-%m-%d
```
この結果を YYYY-MM-DD として全箇所に適用する。UTC や推定日付は使わない。

### 内容

```
# YYYY-MM-DD
{今日のトーン：全セクションを通じた概況を1〜2行で。例：「今週はAnthropicとOpenAIの資金調達競争が過熱。一方Swiftエコシステムは静かだが着実に進化中。」}

## AI（Anthropic / OpenAI）
- **タイトル**：一行サマリー（リンク）
- (コメント)
## Hacker News
- **タイトル**：一行サマリー（リンク）
- (コメント)
## Apple Developer
- **タイトル**：一行サマリー（リンク）
- (コメント)
## Swift / Apple エコシステム
- **タイトル**：一行サマリー（リンク）
- (コメント)
## GitHub Trending
- **リポジトリ名**：一行サマリー（リンク）
- (コメント)
## 株式マーケット（IT）
- **タイトル**：一行サマリー（リンク）🇺🇸 or 🇯🇵
- (コメント)
```

(コメント) は以下のいずれかを付与すること。該当しない場合は省略。
- （要チェック）：実務に直結する可能性が高い
- （懐疑的）：数字・主張に根拠が薄い、または誇張の可能性
- （面白い）：技術的・社会的に興味深い

各セクション3〜5件に絞ること。
docs/ 配下の既存のmdファイルを確認し、過去に掲載済みの記事（タイトル・URLが一致するもの）は今日のファイルに含めないこと。

## 後処理

1. docs/index.md の「バックナンバー」セクションに今日の日付リンクを追記
2. mainブランチに対して git add → commit → push すること（claude/ で始まるブランチは使わないこと）
