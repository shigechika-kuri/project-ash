# LOGOS_DNA: The Inter-Phase Specification Contract / 工程間仕様契約

> **"A prompt without a specification is a building without blueprints. It can be maintained only by someone who was there when it was built — and even they will forget."**
>
> **「仕様のないプロンプトは、設計図のない建築物である。それが建てられたときにそこにいた人間だけが維持できる — そしてその人間でさえ忘れる。」**

---

## 1. The Problem LOGOS_DNA Solves / LOGOS_DNAが解決する問題

Prompt development without structured specification suffers from a specific failure mode: **intent degradation across handoffs**.

構造化された仕様のないプロンプト開発は、特定の失敗モードに苦しむ：**引き継ぎにおける意図の劣化**。

When a prompt passes from one phase to another — or from one person to another, or from one week to the next — the receiving party must infer the original design intent from the prompt text alone. This inference is always lossy. The receiver interprets the text through their own assumptions, and the original intent degrades with each handoff.

プロンプトがあるフェーズから別のフェーズへ — あるいはある人から別の人へ、ある週から次の週へ — 渡されるとき、受け取る側はプロンプトテキストのみから元の設計意図を推論しなければならない。この推論は常に損失を伴う。受け取る側は自身の仮定を通じてテキストを解釈し、元の意図は各引き継ぎとともに劣化する。

In the ASH pipeline, this problem is acute: three specialized agents process the same prompt sequentially. Without explicit specification, the Anchor would need to guess the Builder's intent, and the Genius would need to guess the Anchor's intent. Each guess introduces drift. By Phase 3, the accumulated drift could fundamentally misalign the prompt from its original purpose.

ASHパイプラインにおいて、この問題は深刻である：3つの特化エージェントが同一プロンプトを順次処理する。明示的な仕様なしには、AnchorはBuilderの意図を推測する必要があり、GeniusはAnchorの意図を推測する必要がある。各推測がドリフトを導入する。Phase 3までに、蓄積されたドリフトはプロンプトを元の目的から根本的に不整合にし得る。

LOGOS_DNA eliminates this guesswork by providing an explicit, machine-readable, human-auditable specification that travels with the prompt through every pipeline phase.

LOGOS_DNAは、すべてのパイプラインフェーズを通じてプロンプトと共に移動する、明示的で、機械可読で、人間が監査可能な仕様を提供することで、この推測を排除する。

---

## 2. DNA Structure / DNA構造

LOGOS_DNA is expressed in YAML. The choice of YAML over natural language is deliberate: YAML provides hierarchical structure and named fields without sacrificing human readability. A natural-language specification would itself be subject to the same interpretive ambiguity that ASH is designed to eliminate.

LOGOS_DNAはYAMLで表現される。自然言語ではなくYAMLの選択は意図的である：YAMLは人間の可読性を犠牲にすることなく階層構造と名前付きフィールドを提供する。自然言語の仕様はそれ自体が、ASHが排除するよう設計されたのと同じ解釈上の曖昧さの対象となるだろう。

The DNA contains the following fields:

DNAは以下のフィールドを含む：

### 2.1 Version

The ASH version that last modified this DNA. This field tracks the prompt's progression through the pipeline.

このDNAを最後に修正したASHバージョン。このフィールドはパイプラインを通じたプロンプトの進行を追跡する。

- **5.00**: The DNA was created by the Builder. The prompt has been designed but not hardened.
- **6.00**: The DNA was updated by the Anchor. The prompt has been hardened.
- **7.00**: The DNA was evolved by the Genius. The prompt has completed the full pipeline.

### 2.2 Timestamp

UTC timestamp of the last modification. Provides temporal traceability — when was this specification last touched, and by which phase?

最終修正のUTCタイムスタンプ。時間的トレーサビリティを提供する — この仕様が最後に触られたのはいつで、どのフェーズによってか？

### 2.3 Target_Goal

The prompt's declared purpose in a single, unambiguous statement. This is the most critical field in the DNA. It is the field that the Anchor defends as an oath and that the Genius may mutate through the Mutation Protocol.

単一の曖昧さのない記述によるプロンプトの宣言された目的。これはDNA内で最も重要なフィールドである。Anchorが誓いとして防衛し、GeniusがMutation Protocolを通じて変異させ得るフィールドだ。

A well-written Target_Goal is specific enough to serve as a pass/fail test for the prompt's output. "Help users with questions" is a bad Target_Goal — it is too vague to evaluate against. "Enable the user to identify the single highest-risk element in a project plan and make a go/no-go decision within 30 seconds" is a good Target_Goal — it provides concrete success criteria.

よく書かれたTarget_Goalは、プロンプトの出力に対する合格/不合格テストとして機能するに十分な具体性を持つ。「ユーザーの質問を助ける」は悪いTarget_Goal — 評価するには曖昧すぎる。「ユーザーがプロジェクト計画内の単一の最もリスクの高い要素を識別し、30秒以内にGo/No-Goの判断を下すことを可能にする」は良いTarget_Goal — 具体的な成功基準を提供する。

### 2.4 Structure

A three-part description corresponding to the Anatomy Engine's three layers:

Anatomy Engineの三層に対応する三部構成の記述：

**L1_Surface**: The defined tone, vocabulary level, register, and presentation constraints. At v5.00, this captures the Builder's tone decisions. At v6.00, it reflects the Anchor's de-ambiguated specifications. At v7.00, it reflects the Genius's refined texture.

**L1_Surface**：定義されたトーン、語彙レベル、レジスター、表現の制約。v5.00では、Builderのトーンの判断を捕捉する。v6.00では、Anchorの曖昧さが除去された仕様を反映する。v7.00では、Geniusの洗練された質感を反映する。

**L2_Mechanism**: The primary processing flow, conditional branches, dependency chains, and edge case handling. At v5.00, this captures the Builder's flow design. At v6.00, it reflects the Anchor's stress-tested, hardened logic. At v7.00, it may include lateral connections introduced by the Genius.

**L2_Mechanism**：主要な処理フロー、条件分岐、依存関係チェーン、エッジケース処理。v5.00では、Builderのフロー設計を捕捉する。v6.00では、Anchorのストレステスト済みの硬化された論理を反映する。v7.00では、Geniusによって導入された水平接続を含む場合がある。

**L3_Incentive**: The success definition, win-condition, and operational constraints. At v5.00, this captures the Builder's goal extraction. At v6.00, it reflects the Anchor's alignment verification. At v7.00, it may reflect a mutated purpose if the Genius's philosophical inquiry led to goal redefinition.

**L3_Incentive**：成功定義、勝利条件、運用上の制約。v5.00では、Builderの目標抽出を捕捉する。v6.00では、Anchorの整合性検証を反映する。v7.00では、Geniusの哲学的問いかけが目標の再定義に至った場合、変異した目的を反映する場合がある。

### 2.5 Constraints

An explicit list of inviolable rules. These are the "red lines" — behaviors the prompt must never exhibit, boundaries it must never cross, outputs it must never produce.

不可侵のルールの明示的リスト。これらは「レッドライン」 — プロンプトが決して示してはならない行動、決して越えてはならない境界、決して生み出してはならない出力。

Constraints are cumulative across phases: the Anchor may add constraints discovered during hardening. The Genius may add constraints necessary to support a mutated purpose. Constraints are never silently removed. If a constraint must be removed, it requires an explicit FORCE command from the human, and the removal is logged in the DNA.

制約はフェーズを越えて累積的である：Anchorは硬化中に発見された制約を追加する場合がある。Geniusは変異した目的を支えるために必要な制約を追加する場合がある。制約は暗黙裡に除去されることはない。制約が除去されなければならない場合、人間からの明示的なFORCEコマンドを必要とし、除去はDNAに記録される。

→ Sample DNA output: **[examples/logos-dna-sample.yaml](../examples/logos-dna-sample.yaml)**

---

## 3. DNA Lifecycle / DNAのライフサイクル

### 3.1 Birth — Phase 1 (THE BUILDER)

The Builder creates the initial DNA at the conclusion of Phase 1. The DNA is derived from:

BuilderはPhase 1の結論において初期DNAを作成する。DNAは以下から導出される：

- The requirements elicitation conducted during the session (for GENESIS mode).
- The analysis of provided material (for WORKSHOP mode).
- The diagnosis of the target prompt (for REFACTOR mode).

At birth, the DNA captures the human's stated intent as understood by the Builder, the structural decisions made during construction, and any constraints identified during the session. The Version is set to 5.00.

誕生時、DNAはBuilderが理解した人間の表明された意図、構築中になされた構造的判断、セッション中に識別された制約を捕捉する。Versionは5.00に設定される。

### 3.2 Hardening — Phase 2 (THE ANCHOR)

The Anchor receives the DNA alongside the prompt and performs two operations:

AnchorはDNAをプロンプトと共に受け取り、二つの操作を行う：

First, **validation**: does the DNA accurately describe the prompt? If the prompt's actual structure diverges from the DNA's description, this is flagged as a DNA-Prompt inconsistency and resolved before hardening proceeds.

第一に、**検証**：DNAはプロンプトを正確に記述しているか？プロンプトの実際の構造がDNAの記述から乖離している場合、これはDNA-プロンプト不整合としてフラグされ、硬化が進む前に解決される。

Second, **update**: the Anchor updates the DNA's Structure fields to reflect the de-ambiguated, hardened state. Constraints identified during hardening are added to the Constraints list. The Version is updated to 6.00.

第二に、**更新**：AnchorはDNAのStructureフィールドを曖昧さが除去された硬化状態を反映するよう更新する。硬化中に識別された制約はConstraintsリストに追加される。Versionは6.00に更新される。

The Target_Goal is not modified during hardening. The Anchor's mandate is to defend the goal, not to change it. If the Anchor discovers that the prompt cannot achieve the stated goal, it reports this as a finding rather than modifying the goal.

Target_Goalは硬化中に変更されない。Anchorの任務は目標を防衛することであり、変更することではない。Anchorがプロンプトが掲げる目標を達成できないと発見した場合、目標を変更するのではなく、発見として報告する。

### 3.3 Mutation — Phase 3 (THE GENIUS)

The Genius is the only phase authorized to modify the Target_Goal. This authorization is exercised through the Mutation Protocol:

GeniusはTarget_Goalの変更を許可された唯一のフェーズである。この許可はMutation Protocolを通じて行使される：

1. The Genius identifies a potential goal misalignment through philosophical inquiry.
2. A Mutation Alert is issued, explaining the proposed new goal and why it better serves the human's needs.
3. The human approves or rejects the mutation.
4. If approved, the Genius rewrites the Target_Goal and cascades the change through Structure and Constraints to maintain internal consistency.
5. The Version is updated to 7.00.

If the human rejects the mutation, the Target_Goal remains unchanged. The Genius proceeds with technical proposals that optimize within the existing goal.

人間が変異を棄却した場合、Target_Goalは変更されない。Geniusは既存の目標内で最適化する技術的提案を続行する。

### 3.4 Force Override — Any Phase

At any phase, the human may issue a FORCE command that contradicts the current DNA. When this occurs:

いかなるフェーズにおいても、人間は現在のDNAと矛盾するFORCEコマンドを発行し得る。これが発生した場合：

1. The executing phase implements the human's requested change.
2. The executing phase rewrites the DNA to reflect the forced change.
3. The rewrite ensures internal consistency: if the forced change affects the Target_Goal, the Structure and Constraints are updated accordingly. If it affects only Structure, the Constraints are checked for conflicts.

The principle is absolute: **the DNA must always reflect the actual state of the prompt.** A DNA that says one thing while the prompt does another is a specification in a corrupt state. ASH will not produce or maintain corrupt specifications.

原則は絶対的である：**DNAは常にプロンプトの実際の状態を反映しなければならない。**プロンプトが別のことをしている一方であることを言うDNAは、破損した状態の仕様である。ASHは破損した仕様を生産も維持もしない。

---

## 4. DNA as Dual-Audience Document / 二重オーディエンス文書としてのDNA

LOGOS_DNA is designed to serve two audiences simultaneously:

LOGOS_DNAは同時に二つのオーディエンスに奉仕するよう設計されている：

### 4.1 For Humans / 人間にとって

The DNA is a specification document that allows a human to understand the prompt's design without reading the prompt itself. This is valuable in several scenarios:

DNAは、人間がプロンプト自体を読むことなくプロンプトの設計を理解することを可能にする仕様文書である。これはいくつかのシナリオで価値がある：

- **Audit**: A reviewer can examine the DNA to determine whether the prompt's stated purpose, structure, and constraints are appropriate for the intended use case.
- **Transfer**: When a prompt is handed off to a different person, the DNA provides context that would otherwise require a lengthy briefing.
- **Versioning**: The DNA's Version and Timestamp fields provide a history of how the prompt evolved through the pipeline.

### 4.2 For the Next ASH Phase / 次のASHフェーズにとって

The DNA is a machine-readable specification that the next pipeline phase uses to orient its work:

DNAは次のパイプラインフェーズがその作業の方向を定めるために使用する機械可読仕様である：

- The Anchor reads the DNA to understand what the Builder intended, so it can verify that the prompt achieves that intent — and defend it.
- The Genius reads the DNA to understand what the Anchor has certified, so it can ask whether the certified goal is the right goal — and propose evolution if it is not.

Without the DNA, each phase would need to infer intent from the prompt text alone — which is precisely the kind of ambiguous interpretation that ASH exists to prevent.

DNAなしには、各フェーズはプロンプトテキストのみから意図を推論する必要がある — これはまさにASHが防止するために存在する種類の曖昧な解釈である。

---

## 5. Why YAML / なぜYAMLか

The DNA is expressed in YAML rather than natural language for a specific reason: **a specification written in natural language is subject to the same interpretive ambiguity that ASH is designed to eliminate in prompts.**

DNAが自然言語ではなくYAMLで表現される理由は具体的である：**自然言語で書かれた仕様は、ASHがプロンプトにおいて排除するよう設計されたのと同じ解釈上の曖昧さの対象となる。**

A natural-language specification might say: "The prompt's tone should be professional and authoritative." This is ambiguous. "Professional" and "authoritative" are the same kind of weasel words that ASH eliminates from prompts. They hand interpretive authority to whoever reads them.

自然言語の仕様はこう言うかもしれない：「プロンプトのトーンはプロフェッショナルで権威的であるべきだ。」これは曖昧である。「プロフェッショナル」と「権威的」は、ASHがプロンプトから排除するのと同種の逃げ言葉である。それらを読む誰にでも解釈権を委ねる。

A YAML specification eliminates this ambiguity through structure and determinism:

YAML仕様は構造と決定論によりこの曖昧さを排除する：

```yaml
L1_Surface: "Formal register. No contractions. No emoji. Address user as 'you.' Maximum sentence length: 25 words."
```

This is not interpretable. It is a specification. The distinction between "professional tone" and the YAML equivalent above is the distinction between an escape-hatch adjective and a deterministic constraint — the same distinction that the Anatomy Engine's Layer 1 enforces within prompts themselves.

これは解釈可能ではない。仕様である。「プロフェッショナルなトーン」と上記のYAML等価物の間の区別は、エスケープハッチ形容詞と決定論的制約の間の区別 — Anatomy EngineのLayer 1がプロンプト自体の中で強制するのと同じ区別 — である。

→ Anatomy Engine Layer 1 specification: **[docs/anatomy-engine.md](./anatomy-engine.md)**
→ Architectural context: **[ARCHITECTURE.md Section 4](../ARCHITECTURE.md)**

---

**Document Version**: 1.0
**Parent**: [ARCHITECTURE.md](../ARCHITECTURE.md) Section 4
**Author**: Shigechika Kurihara (栗原栄親)

© 2026 Shigechika Kurihara. All Rights Reserved.
