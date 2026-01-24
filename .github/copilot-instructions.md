# GitHub Copilot Instructions

## プロジェクト概要
jao Minecraft Serverの公式Discordサーバ『jao Gamers Club』用のDiscord Bot。TypeScriptで実装されており、翻訳、テキスト変換、誕生日管理、ゲーム関連コマンドなど多数の機能を提供します。

## 共通ルール
- 会話は日本語で行う。
- PR とコミットは Conventional Commits に従う。
- PR タイトルとコミット本文の言語: PR タイトルは Conventional Commits 形式（英語推奨）。PR 本文は日本語。コミットは Conventional Commits 形式（description は日本語）。
- 日本語と英数字の間には半角スペースを入れる。
- 既存のプロジェクトルールがある場合はそれを優先する。

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

## テスト方針
- 新機能や修正には適切なテストを追加する。

## セキュリティ / 機密情報
- 認証情報やトークンはコミットしない。
- ログに機密情報を出力しない。

## ドキュメント更新
- 実装確定後、同一コミットまたは追加コミットで更新する。
- README、API ドキュメント、コメント等は常に最新状態を保つ。

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
