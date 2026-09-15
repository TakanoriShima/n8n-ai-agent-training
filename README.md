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
AI が目的・状況に応じて
必要な Tool を選択
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

AI Agent では、LLM が目的や状況を解釈し、**利用可能な Tool の中から必要なものを選択**できます。

本教材ではこの違いを、実際に n8n を操作しながら体験します。

---

## 📚 カリキュラム

| Lesson                                             | 内容                                   | 主な学習テーマ                                 | 状態        |
| -------------------------------------------------- | -------------------------------------- | ---------------------------------------------- | ----------- |
| [Lesson 01](./docs/lesson01-setup.md)              | n8n Community Edition の環境構築       | Docker / n8n                                   | ✅ 完成     |
| [Lesson 02](./docs/lesson02-basic-workflow.md)     | 基本 Workflow の構築                   | Trigger / JSON / Expression / If               | ✅ 完成     |
| [Lesson 03](./docs/lesson03-gemini-integration.md) | Gemini を n8n に接続する               | Gemini API / LLM / Prompt                      | ✅ 完成     |
| [Lesson 04](./docs/lesson04-ai-agent.md)           | AI Agent を構築する                    | AI Agent / Chat Model / Tool なし Agent の限界 | ✅ 完成     |
| Lesson 05                                          | Tool Calling を実装する                | Tool / Tool Calling / Agent による Tool 選択   | 🚧 制作予定 |
| Lesson 06                                          | Human-in-the-loop を実装する           | 承認 / 却下 / AI ガバナンス                    | 🚧 制作予定 |
| Lesson 07                                          | Google Sheets / Slack 等と連携する     | 外部サービス / 業務システム連携                | 🚧 制作予定 |
| Lesson 08                                          | 営業提案 AI エージェント完成・発展演習 | Agent 設計 / 業務適用                          | 🚧 制作予定 |

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
- 動的データの利用
- LLM を業務 Workflow に組み込む方法

### AI Agent

- Workflow と AI Agent の違い
- AI Agent と Chat Model の関係
- Agent の役割
- Tool Calling
- Tool 設計
- Agent による Tool 選択
- Tool を持たない Agent の限界

### AI ガバナンス

- Human-in-the-loop
- AI による外部操作の制御
- 人間による承認
- Credential / API キーの安全な管理

---

## 🏗️ 現在の実装

現在、**Lesson 04 まで実装済み**です。

### Lesson 02：通常の Workflow

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

営業担当者・商談先企業・依頼内容を構造化データとして作成し、企業名が入力されているかを If Node で判定します。

ここでは AI を使用せず、**人間が定義したルールによって処理を分岐する従来型 Workflow** を構築しています。

### Lesson 03：Gemini を Workflow から呼び出す

```text
Manual Trigger
      ↓
 Edit Fields
      ↓
Google Gemini
(Message a model)
      ↓
営業提案を生成
```

![Lesson 03 Gemini Workflow](./docs/images/32_n8n_gemini_workflow_success.png)

Edit Fields で作成した業務データを Gemini へ渡し、営業担当者向けの初回商談準備を生成します。

ここでは、**通常の Workflow の一処理として LLM を利用する方法**を学びます。

### Lesson 04：AI Agent を構築する

Lesson 04 では、Gemini を直接呼び出す構成から AI Agent を中心とした構成へ発展させます。

```text
Manual Trigger
      ↓
 Edit Fields
      ↓
   AI Agent
      │
      └── Google Gemini Chat Model
```

![Lesson 04 AI Agent](./docs/images/46_n8n_ai_agent_workflow_success.png)

AI Agent の Chat Model として Gemini を接続し、営業担当者の目的をもとに初回商談の準備内容を生成します。

さらに、あえて Tool を接続しない状態で、

```text
株式会社サンプル製造の最新の企業情報を調査し、
その情報をもとに初回商談の提案を作成してください
```

という指示を与えました。

![AI Agent Without Tools](./docs/images/48_n8n_ai_agent_without_tools.png)

この実験から、

> **AI Agent を利用するだけで、外部情報を自由に取得できるようになるわけではない**

ことを確認します。

現在の Agent は次の状態です。

```text
             AI Agent
                │
       ┌────────┼────────┐
       ↓        ↓        ↓
 Chat Model   Memory    Tool
       │        ×        ×
    Gemini
```

Agent が外部の情報やシステムを利用する能力は、接続された Tool によって拡張されます。

この「Tool を持たない Agent の限界」を理解したうえで、Lesson 05 の Tool Calling へ進みます。

---

## 📦 Workflow サンプル

各 Lesson で完成した Workflow は JSON として保存しています。

```text
workflows/
├─ 01-basic-workflow.json
├─ 02-gemini-integration.json
└─ 03-ai-agent.json
```

Lesson を見ながら自分で Workflow を作成したあと、JSON を n8n へ Import して完成版と比較できます。

Workflow JSON には API キー本体を保存せず、Credential は n8n 側で管理します。

---

## 🖥️ 開発・実習環境

本教材は以下の環境で制作・動作確認しています。

- Windows 11
- WSL2
- Ubuntu 24.04
- Docker Desktop
- Docker Compose
- n8n Community Edition
- Gemini API

n8n は Docker コンテナ上で実行します。

教材、スクリーンショット、Workflow JSON などは Windows 側のプロジェクトディレクトリで Git 管理します。

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
│  ├─ lesson03-gemini-integration.md
│  ├─ lesson04-ai-agent.md
│  │
│  └─ images/
│     ├─ 01_n8n_owner_account_setup.png
│     ├─ ...
│     └─ 48_n8n_ai_agent_without_tools.png
│
└─ workflows/
   ├─ 01-basic-workflow.json
   ├─ 02-gemini-integration.json
   └─ 03-ai-agent.json
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

Gemini API の認証情報は n8n の Credential として管理し、API キーそのものを Workflow JSON や Markdown へ直接記述しない構成とします。

Workflow を GitHub へ公開する前には、Export した JSON に秘密情報が含まれていないことを確認します。

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

という発展を、一つの営業業務を題材として連続的に体験できる構成としています。

### 「できること」だけでなく「できないこと」も確認する

本教材では、成功する操作だけでなく、AI Agent の制約も実際に確認します。

Lesson 04 では Tool を持たない Agent に外部情報の調査を要求することで、

```text
AI Agent
≠
自動的にあらゆる外部情報へアクセスできるAI
```

という点を実験から理解します。

そのうえで Tool を追加し、Agent の能力がどのように変化するのかを後続 Lesson で比較します。

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

**現在：Lesson 04 完成**

ここまでに、

```text
Lesson 01
n8n 環境構築
      ↓
Lesson 02
通常の Workflow
      ↓
Lesson 03
Gemini / LLM 連携
      ↓
Lesson 04
AI Agent + Gemini
```

まで実装しました。

次の実装：

> **Lesson 05 — Tool Calling を実装する**

Lesson 05 では、AI Agent に実際の Tool を接続します。

```text
                AI Agent
                   │
         ┌─────────┴─────────┐
         ↓                   ↓
Gemini Chat Model           Tool
         │                   │
      推論・生成          外部処理
         └─────────┬─────────┘
                   ↓
                結果生成
```

Lesson 04 の **「Tool を持たない Agent」** と比較することで、

**AI Agent が利用可能な Tool を選択・実行する Tool Calling の仕組み**

を実装を通して学びます。
