# n8n × Gemini 実践 AI エージェント研修

## 営業提案 AI エージェントを作りながら学ぶ Tool Calling / Human-in-the-loop

n8n と Gemini を利用して、**企業業務で活用できる AI エージェントを段階的に構築する実践型研修教材**です。

単に LLM へプロンプトを送り文章を生成するのではなく、

- Workflow
- LLM
- AI Agent
- Tool Calling
- Human-in-the-loop
- 外部サービス連携

までを段階的に実装しながら、**「通常の業務自動化」と「AI エージェント」の違いを理解すること**を目的としています。

題材として、営業担当者の商談準備を支援する  
**「営業提案 AI エージェント」** を構築します。

---

## 🎯 この教材のゴール

最終的に、次のような AI エージェントを構築します。

```text
営業担当者
    ↓
「株式会社○○との初回商談を準備して」
    ↓
n8n
    ↓
AI Agent（Gemini）
    │
    ├─ Tool：企業情報を調査
    ├─ Tool：顧客課題を分析
    ├─ Tool：営業提案を作成
    ├─ Tool：商談情報を記録
    └─ Tool：担当者へ通知
    │
    ↓
AIが目的・状況に応じて
必要なToolを選択
    ↓
営業提案・次のアクションを生成
    ↓
Human-in-the-loop
    ↓
人間による承認
   ↙        ↘
承認        却下
 ↓
外部サービスへ反映
```

重要なのは、処理を単純に上から順番に実行するだけではなく、

> **AI Agent 自身が、目的達成のためにどの Tool を使用するか判断する**

ことです。

---

## 💡 なぜ最初に「普通の Workflow」を学ぶのか

AI Agent を理解するには、まず通常の Workflow との違いを理解する必要があります。

### 通常の Workflow

```text
入力
 ↓
処理A
 ↓
If
↙  ↘
A   B
```

処理順序や判断条件は、**人間があらかじめ設計**します。

### AI Agent

```text
ユーザーの目的
      ↓
   AI Agent
   ↙   ↓   ↘
Tool A Tool B Tool C
```

AI Agent では、LLM が目的や状況を解釈し、**必要な Tool を選択**します。

本教材ではこの違いを、実際に n8n を操作しながら体験します。

---

## 📚 カリキュラム

| Lesson                                         | 内容                                   | 状態        |
| ---------------------------------------------- | -------------------------------------- | ----------- |
| [Lesson 01](./docs/lesson01-setup.md)          | n8n Community Edition の環境構築       | ✅ 完成     |
| [Lesson 02](./docs/lesson02-basic-workflow.md) | 基本 Workflow / JSON / Expression / If | ✅ 完成     |
| Lesson 03                                      | Gemini を n8n に接続する               | 🚧 制作予定 |
| Lesson 04                                      | AI Agent を構築する                    | 🚧 制作予定 |
| Lesson 05                                      | Tool Calling を実装する                | 🚧 制作予定 |
| Lesson 06                                      | Human-in-the-loop を実装する           | 🚧 制作予定 |
| Lesson 07                                      | Google Sheets / Slack 等と連携する     | 🚧 制作予定 |
| Lesson 08                                      | 営業提案 AI エージェント完成・発展演習 | 🚧 制作予定 |

---

## 🧠 この教材で学べること

### n8n / Workflow

- Trigger と Node
- Node 間のデータ受け渡し
- JSON
- Expression
- 条件分岐
- Workflow の Import / Export

### 生成 AI

- Gemini との API 連携
- LLM への入力と出力
- Prompt 設計
- 構造化されたデータの利用

### AI Agent

- Workflow と AI Agent の違い
- Agent の役割
- Tool Calling
- Tool 設計
- Agent による Tool 選択

### AI ガバナンス

- Human-in-the-loop
- AI による外部操作の制御
- 人間による承認
- Credential / API キーの安全な管理

---

## 🏗️ 現在の実装

現在、Lesson 02 まで実装済みです。

```text
Manual Trigger
      ↓
 Edit Fields
      ↓
     If
   ↙    ↘
 true  false
```

![Lesson 02 Basic Workflow](./docs/images/20_n8n_basic_workflow_complete.png)

この Workflow では、

1. 営業担当者
2. 商談先企業
3. 営業担当者からの依頼

を構造化データとして作成し、企業名が入力されているかを If Node で判定します。

ここではまだ AI を使用していません。

**人間が定義したルールで判断する従来型 Workflow**を理解したうえで、後続 Lesson から AI Agent へ発展させます。

---

## 📦 Workflow サンプル

完成した Workflow は JSON として保存しています。

```text
workflows/
└─ 01-basic-workflow.json
```

Lesson を見ながら自分で Workflow を作成したあと、JSON を n8n へ Import して完成版と比較できます。

---

## 🖥️ 開発・実習環境

本教材は以下の環境で制作・動作確認しています。

- Windows 10
- WSL2
- Ubuntu 24.04
- Docker Desktop
- Docker Compose
- n8n Community Edition
- Gemini API（後続 Lesson で使用予定）

n8n は Docker コンテナ上で実行します。

教材、スクリーンショット、Workflow JSON などは Git で管理します。

---

## 📁 Repository Structure

```text
n8n-ai-agent/
│
├─ README.md
├─ compose.yaml
├─ .gitignore
│
├─ docs/
│  ├─ lesson01-setup.md
│  ├─ lesson02-basic-workflow.md
│  │
│  └─ images/
│     ├─ 01_n8n_owner_account_setup.png
│     ├─ ...
│     └─ 20_n8n_basic_workflow_complete.png
│
└─ workflows/
   └─ 01-basic-workflow.json
```

---

## 🚀 n8n の起動

Docker Desktop を起動した状態で、プロジェクトディレクトリから実行します。

```powershell
docker compose up -d
```

ブラウザから次へアクセスします。

```text
http://localhost:5678
```

停止する場合は、

```powershell
docker compose down
```

を実行します。

詳しい環境構築手順は、

➡️ [Lesson 01：n8n の環境構築](./docs/lesson01-setup.md)

を参照してください。

---

## 🔐 セキュリティについて

API キー、パスワード、Credential などの秘密情報は GitHub へ登録しません。

後続 Lesson で Gemini API 等を利用する場合も、Credential や環境変数を利用し、秘密情報を Workflow JSON や Markdown へ直接記述しない構成とします。

`.env` などの秘密情報を含むファイルは `.gitignore` の対象とします。

---

## 👨‍🏫 研修教材としての設計

本リポジトリは、完成した AI Agent を公開するだけではなく、**受講者が段階的に仕組みを理解できる研修教材**として設計しています。

各 Lesson では、

1. 概念を理解する
2. n8n で実際に操作する
3. INPUT / OUTPUT を確認する
4. なぜその処理が必要なのか考える
5. 演習で設定を変更する
6. 完成 Workflow と比較する

という流れで学習します。

特に、

```text
Workflow
   ↓
LLM
   ↓
AI Agent
   ↓
Tool Calling
   ↓
Human-in-the-loop
```

という発展を、一つの営業業務を題材として連続的に体験できる構成を目指しています。

---

## 🔄 発展例

本教材で学ぶ AI Agent の設計は、営業業務以外にも応用できます。

例えば、

- 社内問い合わせ対応 AI Agent
- 新人教育・OJT 支援 AI Agent
- 採用支援 AI Agent
- 業務改善提案 AI Agent
- AI 研修設計 Agent

などへ展開できます。

最終演習では、受講者自身の業務を題材に、

> **「どの業務を Workflow にし、どの判断を AI Agent へ任せ、どこに人間の承認を入れるべきか」**

を設計することを目標とします。

---

## 📌 Project Status

**現在：Lesson 02 完成**

次の実装：

> **Lesson 03 — Gemini を n8n に接続する**

ここから、通常の Workflow に LLM を組み込み、最終的な AI Agent / Tool Calling へ発展させます。
