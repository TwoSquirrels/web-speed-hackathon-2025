# Web Speed Hackathon 攻略用 Claude Code 設定

## 攻略ドキュメント (`scraps/`)

**競技中は `scraps/checklist.md` を上から順に実行することがメインの作業。**
他のドキュメントは必要に応じて参照する。

### [`scraps/checklist.md`](./scraps/checklist.md)

競技中に上から順に実行する実践手順書 (Phase 0〜8)。コマンド例・コードスニペット付き。

| Phase | 内容 | 読むタイミング |
|-------|------|------------|
| Phase 0 | 準備・初期計測 | **競技開始直後** |
| Phase 1 | ビルド設定修正・Vite 移行 | Phase 0 完了後すぐ |
| Phase 2 | バンドルサイズ削減 | Phase 1 完了後 |
| Phase 3 | 意図的な遅延の除去 | Phase 2 完了後 |
| Phase 4 | アセット最適化 | Phase 3 完了後 |
| Phase 5 | バックエンド・ネットワーク最適化 | Phase 4 完了後 |
| Phase 6 | CDN / インフラ | Phase 5 完了後 |
| Phase 7 | React レンダリング最適化 | Phase 6 完了後 |
| Phase 8 | 最終確認 | **競技終了 30 分前に必ず** |

### [`scraps/README.md`](./scraps/README.md)

WSH の概要・戦略・スコア計算式・メトリクス別対策・ツールリファレンス。

- **スコア計算式を確認したい**とき (年度ごとに異なる)
- **メトリクス (TBT/LCP/CLS/FCP/INP) の改善方針**を確認したいとき
- **インフラ選択** (Cloudflare/Heroku/VPS) の実績を確認したいとき
- **ライブラリ代替一覧** (moment→day.js 等) を確認したいとき
- **FFmpeg・画像・フォントのコマンド例**を確認したいとき
- **バンドルサイズ目標値**を確認したいとき

### [`scraps/traps.md`](./scraps/traps.md)

失格パターン・毎年仕込まれる罠の一覧。

- **失格を避けたい**とき (競技中・最終確認前に必ず読む)
- **「なぜかスコアが上がらない」「テストが落ちる」**とき
- **毎年の仕込みパターン** (ReDoS・p-min-delay・スクロール位置保存) を確認したいとき

### [`scraps/years.md`](./scraps/years.md)

2020〜2025 年の年度別アプリ詳細・仕込み問題・参加記まとめ。

- **今年の傾向を読みたい**とき (事前学習・テーマ予想)
- **「過去に似た問題があったか」**を調べたいとき
- **具体的な仕込みの手口**を把握したいとき

### [`scraps/urls.md`](./scraps/urls.md)

参考にした記事・参加記の URL 一覧。詳細を調べたいときに参照する。

## インストール済みスキル

以下のスキルがインストールされている。**該当するタスクが発生したら積極的に呼び出すこと。**

スキルが見つからない・動作しない場合は以下を実行する:

```bash
pnpm dlx skills experimental_install
```

Claude Code など `.agents/skills/` を参照しない AI エージェントを使っている場合は、必要に応じてシンボリックリンクを貼る:

```bash
ln -s ../.agents/skills .claude/skills
```

`.agents/skills/` や `.claude/skills/` が `.gitignore` に含まれていない場合は追加する:

```
.agents/skills/
.claude/skills/
```

### Vite 移行・ビルド設定

| シチュエーション | 呼び出すスキル |
|--------------|-------------|
| webpack → Vite 移行、vite.config.ts の設定、Rolldown 対応 | `vite` (antfu/skills) |

### パフォーマンス最適化 (全般)

| シチュエーション | 呼び出すスキル |
|--------------|-------------|
| 画像・フォント・アニメーション・バンドルを網羅的に最適化する | `optimize` (pbakaus/impeccable) |
| フロント＋バックエンドのパフォーマンスチェックリストを適用する | `performance-optimization` (supercent-io/skills-template) |
| Web パフォーマンス全般の改善方針を確認する | `web-performance-optimization` (sickn33/antigravity-awesome-skills) |

### Lighthouse / Core Web Vitals

| シチュエーション | 呼び出すスキル |
|--------------|-------------|
| LCP・INP・CLS の改善方針を確認する | `core-web-vitals` (addyosmani/web-quality-skills) |
| 読み込み・ランタイムのパフォーマンスを深掘りする | `performance` (addyosmani/web-quality-skills) |
| Web 品質を総合的に監査する | `web-quality-audit` (addyosmani/web-quality-skills) |
| モダン Web 標準・ベストプラクティスを確認する | `best-practices` (addyosmani/web-quality-skills) |

### React 最適化

| シチュエーション | 呼び出すスキル |
|--------------|-------------|
| React の再レンダリング・バンドル・async waterfall を最適化する | `vercel-react-best-practices` (vercel-labs/agent-skills) |

### アセット最適化

| シチュエーション | 呼び出すスキル |
|--------------|-------------|
| FFmpeg で動画・音声を変換・圧縮・HLS 化する | `ffmpeg` (digitalsamba/claude-code-video-toolkit) |

### DB 最適化

| シチュエーション | 呼び出すスキル |
|--------------|-------------|
| SQL クエリ・インデックス・N+1 を最適化する | `sql-optimization-patterns` (wshobson/agents) |
