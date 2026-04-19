# Examples / 出力サンプル

> **"These samples show what ASH produces — not how it produces it."**
>
> **「これらのサンプルはASHが何を生産するかを示す — どう生産するかではなく。」**

---

## What This Directory Contains / このディレクトリに含まれるもの

This directory contains redacted output samples from ASH pipeline operations. They demonstrate the system's output format, analytical depth, and structural rigor.

このディレクトリはASHパイプライン操作からのリダクト済み出力サンプルを含む。システムの出力フォーマット、分析の深さ、構造的厳密さを実証する。

**Included samples**:

- **[diagnosis-sample.md](./diagnosis-sample.md)** — A sample diagnostic report produced by ASH upon receiving input for analysis. Shows the Anatomy Engine's three-layer decomposition in action. (ASHが分析のために入力を受け取った際に生成する診断レポートのサンプル。Anatomy Engineの三層分解が動作する様子を示す。)

- **[proposal-sample.yaml](./proposal-sample.yaml)** — A sample structured proposal block in YAML format. Shows how ASH presents modification proposals with explicit IDs, rationale, diff previews, and risk assessments. (YAMLフォーマットの構造化提案ブロックのサンプル。ASHがID、根拠、diffプレビュー、リスク評価を伴う修正提案をどう提示するかを示す。)

- **[logos-dna-sample.yaml](./logos-dna-sample.yaml)** — A sample LOGOS_DNA specification block. Shows the structured specification format that accompanies every ASH output. (LOGOS_DNA仕様ブロックのサンプル。すべてのASH出力に付帯する構造化仕様フォーマットを示す。)

## What This Directory Does NOT Contain / このディレクトリに含まれないもの

- No executable prompts. The system prompts that drive ASH's agents are proprietary. (実行可能なプロンプトはない。ASHのエージェントを駆動するシステムプロンプトは特権的資産である。)
- No complete session logs. The samples are isolated output fragments, not full interaction histories. (完全なセッションログはない。サンプルは隔離された出力断片であり、完全な対話履歴ではない。)
- No target prompts. The prompts that ASH analyzed to produce these samples are not included. (ターゲットプロンプトはない。ASHがこれらのサンプルを生成するために分析したプロンプトは含まれない。)

## How to Read These Samples / これらのサンプルの読み方

These samples are designed to answer the question: "What does it look like when ASH operates?"

これらのサンプルは「ASHが動作するとき、どのように見えるか？」という問いに答えるよう設計されている。

The diagnosis sample shows the Anatomy Engine's output: structured, layer-by-layer analysis with specific findings and actionable next steps. The proposal sample shows the decision-making interface: each change is presented as a discrete, identifiable unit with clear rationale and explicit risk. The DNA sample shows the specification format: the machine-readable, human-auditable contract that travels with the prompt.

診断サンプルはAnatomy Engineの出力を示す：具体的な知見と行動可能な次のステップを伴う、構造化されたレイヤーごとの分析。提案サンプルは意思決定インターフェースを示す：各変更は明確な根拠と明示的なリスクを伴う離散的で識別可能な単位として提示される。DNAサンプルは仕様フォーマットを示す：プロンプトと共に移動する機械可読で人間が監査可能な契約。

Together, they demonstrate that ASH is not a conversational assistant that gives advice about prompts. It is a structured engineering system that produces auditable, traceable artifacts.

合わせて、ASHがプロンプトについてアドバイスする会話型アシスタントではないことを実証する。監査可能でトレーサブルな成果物を生産する構造化されたエンジニアリングシステムである。

These three samples are not independent fragments. They are a snapshot of a single ASH pipeline scene: a prompt was submitted to the Anchor (v6.00), which diagnosed it at Hardness Score 41% with 11 findings across three layers (diagnosis-sample.md). Those findings were translated into five structured proposals with explicit rationale and inter-proposal dependencies (proposal-sample.yaml). After human approval, the hardened specification was output as LOGOS_DNA v6.00 — with all ambiguities resolved, all edge cases handled, and all constraints stated as deterministic rules (logos-dna-sample.yaml). Reading them in this order — diagnosis, then proposals, then DNA — traces the arc from problem identification through structured decision-making to specification output.

これら3つのサンプルは独立した断片ではない。ASHパイプラインの一場面のスナップショットである。あるプロンプトがAnchor（v6.00）に提出され、Hardness Score 41%、三層にわたる11の知見とともに診断された（diagnosis-sample.md）。それらの知見は、明示的な根拠と提案間の依存関係を伴う5つの構造化提案に変換された（proposal-sample.yaml）。人間の承認後、硬化された仕様がLOGOS_DNA v6.00として出力された — すべての曖昧さが解消され、すべてのエッジケースが処理され、すべての制約が決定論的ルールとして記述された状態で（logos-dna-sample.yaml）。診断、次に提案、次にDNAの順に読むことで、問題の識別から構造化された意思決定を経て仕様出力に至るアークをたどることができる。

---

**Document Version**: 1.0
**Author**: Shigechika Kurihara (栗原栄親)

© 2026 Shigechika Kurihara. All Rights Reserved.
