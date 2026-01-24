# CLAUDE.md

## 目的
- Claude Code の作業方針とプロジェクト固有ルールを示す。

## 判断記録のルール
- 判断は必ずレビュー可能な形で記録する。
  1. 判断内容の要約
  2. 検討した代替案
  3. 採用しなかった案とその理由
  4. 前提条件・仮定・不確実性
  5. 他エージェントによるレビュー可否
- 前提・仮定・不確実性を明示し、仮定を事実のように扱わない。

## プロジェクト概要
jao Minecraft Serverの公式Discordサーバ『jao Gamers Club』用のDiscord Bot。TypeScriptで実装されており、翻訳、テキスト変換、誕生日管理、ゲーム関連コマンドなど多数の機能を提供します。

### 技術スタック
- **言語**: TypeScript, JavaScript, Python (requirements.txt)
- **フレームワーク**: discord.js (Discord API Client), node-cron (Task scheduling), axios (HTTP client), cheerio (HTML parsing), Jest (Testing framework)
- **パッケージマネージャー**: pnpm@10.10.0+sha512...
- **主要な依存関係**:
  - discord.js:14.19.2
  - @book000/eslint-config:1.8.59
  - @book000/node-utils:1.14.96
  - @napi-rs/canvas:0.1.68
  - axios:1.9.0
  - cheerio:1.0.0
  - detectlanguage:2.1.0
  - node-cron:3.0.3
  - typescript:5.8.3
  - eslint:9.25.1

## 重要ルール
- 会話言語: 日本語
- PR とコミットは Conventional Commits に従う。
- PR タイトルとコミット本文の言語: PR タイトルは Conventional Commits 形式（英語推奨）。PR 本文は日本語。コミットは Conventional Commits 形式（description は日本語）。
- コメント言語: 日本語
- エラーメッセージ: 英語
- 日本語と英数字の間には半角スペースを挿入する。
- 既存のプロジェクトルールがある場合はそれを優先する。

## 環境のルール
- ブランチ命名は Conventional Branch に従う。
- GitHub リポジトリを調査する場合はテンポラリディレクトリに `git clone` して検索する。
- Windows 環境では Git Bash を使用する。
- Renovate の既存 PR には追加コミットしない。

## Git Worktree
- 使う場合は `.bare/<branch>` 構成で作成する。

## ブラウザ操作
- 座標ではなくセレクターで要素を特定する。
- 実装と画面の差異を確認し、必要に応じて実装を改善する。

## コード改修時のルール
- 既存のエラーメッセージで先頭に絵文字がある場合、全体で統一する。
- TypeScript 使用時は `skipLibCheck` で回避しない。
- 関数やインターフェースには docstring（JSDoc など）を記載する。

### コーディング規約
- **eslint_config**: eslint.config.mjs - extends @book000/eslint-config (custom shared config)
- **prettier_config**: .prettierrc.yml: printWidth=80, singleQuote, semi=false, trailingComma=es5, bracketSpacing=true, endOfLine=lf
- **typescript**: target: es2020, module: commonjs, strict: true, strict checks enabled (noImplicitAny, noUnusedLocals, noUnusedParameters, noImplicitReturns, noFallthroughCasesInSwitch), sourceMap: true, incremental: true, declaration: true
- **code_style**:
  - 80-character line width
  - Single quotes for strings
  - No semicolons
  - ES5 trailing commas
  - Bracket spacing enabled
  - LF line endings
  - Strict TypeScript mode enforced
  - Path alias: @/* -> src/*
  - Class-based command and event handlers
  - Permission-based command access control

## 相談ルール
- Codex CLI: 実装レビュー、局所設計、整合性確認に使う。
- Gemini CLI: 外部仕様や最新情報の確認に使う。
- 他エージェントの指摘は黙殺せず、採用または理由を明記して不採用とする。

### 開発コマンド
```bash
# install
pnpm install

# build
tsc (TypeScript compilation to dist/)

# test
jest --runInBand --passWithNoTests --detectOpenHandles --forceExit

# lint
run-z lint:prettier,lint:eslint,lint:tsc

# format
run-z fix:prettier fix:eslint

# dev
tsx watch ./src/main.ts

# other commands
pnpm start (Start production server with tsx)
pnpm lint:prettier (Check formatting)
pnpm lint:eslint (Check code quality)
pnpm lint:tsc (TypeScript type check)
pnpm fix:prettier (Format code)
```

### プロジェクト構造
**ルートファイル:**
- `package.json`
- `pnpm-lock.yaml`
- `tsconfig.json`
- `.prettierrc.yml`
- `eslint.config.mjs`
- `.node-version`
- `.depcheckrc.json`
- `.fixpackrc`
- `Dockerfile`
- `compose.yaml`

**主要ディレクトリ:**
- `src/ (Source code)`
- `src/commands/ (Slash commands)`
- `src/events/ (Event handlers)`
- `src/features/ (Feature modules)`
- `src/jobs/ (Scheduled jobs)`
- `src/tasks/ (Async tasks)`
- `assets/ (Static assets)`
- `docs/ (Documentation)`
- `scripts/ (Utility scripts)`
- `.github/workflows/ (CI/CD)`

## 実装パターン
- 既存のコードパターンに従う。
- プロジェクト固有の実装ガイドラインがある場合はそれに従う。

## テスト
- 方針: 変更内容に応じてテストを追加する。

## ドキュメント更新ルール
- 更新タイミング: 実装確定後、同一コミットまたは追加コミットで更新する。
- README、API ドキュメント、コメント等は常に最新状態を保つ。

## 作業チェックリスト

### 新規改修時
1. プロジェクトを理解する。
2. 作業ブランチが適切であることを確認する。
3. 最新のリモートブランチに基づいた新規ブランチであることを確認する。
4. PR がクローズされた不要ブランチが削除済みであることを確認する。
5. 指定されたパッケージマネージャーで依存関係をインストールする。

### コミット・プッシュ前
1. Conventional Commits に従っていることを確認する。
2. センシティブな情報が含まれていないことを確認する。
3. Lint / Format エラーがないことを確認する。
4. 動作確認を行う。

### PR 作成前
1. PR 作成の依頼があることを確認する。
2. センシティブな情報が含まれていないことを確認する。
3. コンフリクトの恐れがないことを確認する。

### PR 作成後
1. コンフリクトがないことを確認する。
2. PR 本文が最新状態のみを網羅していることを確認する。
3. `gh pr checks <PR ID> --watch` で CI を確認する。
4. Copilot レビューに対応し、コメントに返信する。
5. Codex のコードレビューを実施し、指摘対応を行う。
6. PR 本文の崩れがないことを確認する。

## リポジトリ固有
- **type: Discord Bot (Multi-purpose utility bot)**
- **target_server: jao Gamers Club (Official Discord server for jao Minecraft Server)**
- **uses: discord.js v14 (Modern Discord API library)**
- **uses: @book000/eslint-config (Shared ESLint config from same author)**
- **uses: @book000/node-utils (Shared utilities from same author)**
- **deployment: Docker container with Node.js 22-alpine**
- **timezone: Asia/Tokyo configured in Docker**
- **config_management: JSON-based configuration at /data/config.json**
- **command_prefix: Slash commands (/) based**
- **features: 30+ commands (translation, text transforms, birthday, image search, etc.)**
- **features: Multiple event handlers (greeting, pin reactions, meeting votes, etc.)**
- **features: Scheduled jobs and cron tasks**
- **features: Permission-based command access control**
- **features: Image canvas support (@napi-rs/canvas)**
- **features: Multi-language detection (detectlanguage library)**
- **bot_intents: Guilds, GuildMessages, GuildMembers, GuildMessageReactions, MessageContent**
- **node_version: 22.14.0 (from .node-version)**
- **package_manager_version: pnpm@10.10.0**
- **package_format: private package (not published to npm)**
- **output_dir: dist/main.js**
- **testing: Jest with ts-jest transform**
- **ci_workflows: add-reviewer, add-viewer, console-log-error, doc-build, doc-deploy, docker, jaotan-review, nodejs-ci-pnpm**
- **devcontainer: Available for standardized development environment**
- **repository_url: git@github.com:jaoafa/jaotan.ts.git**
