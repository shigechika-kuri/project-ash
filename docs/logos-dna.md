# Prompt Specification Contract / プロンプト仕様契約

> **"A prompt without a specification is a building without blueprints. It can be maintained only by someone who was there when it was built — and even they will forget."**
>
> **「仕様のないプロンプトは、設計図のない建築物である。それが建てられたときにそこにいた人間だけが維持できる — そしてその人間でさえ忘れる。」**
>
> *(Source code designation: LOGOS_DNA / ソースコード内呼称：LOGOS_DNA)*

---

## 1. The Problem This Contract Solves / この契約が解決する問題

Prompt development without structured specification suffers from a specific failure mode: **intent degradation across handoffs**.

構造化された仕様のないプロンプト開発は、特定の失敗モードに苦しむ：**引き継ぎにおける意図の劣化**。

When a prompt passes from one phase to another — or from one person to another, or from one week to the next — the receiving party must infer the original design intent from the prompt text alone. This inference is always lossy. The receiver interprets the text through their own assumptions, and the original intent degrades with each handoff.

プロンプトがあるフェーズから別のフェーズへ — あるいはある人から別の人へ、ある週から次の週へ — 渡されるとき、受け取る側はプロンプトテキストのみから元の設計意図を推論しなければならない。この推論は常に損失を伴う。受け取る側は自身の仮定を通じてテキストを解釈し、元の意図は各引き継ぎとともに劣化する。

In the ASH pipeline, this problem is acute: three specialized agents process the same prompt sequentially. Without explicit specification, THE ANCHOR would need to guess THE BUILDER's intent, and THE GENIUS would need to guess THE ANCHOR's intent. Each guess introduces drift. By Phase 3, the accumulated drift could fundamentally misalign the prompt from its original purpose.

ASHパイプラインにおいて、この問題は深刻である：3つの特化エージェントが同一プロンプトを順次処理する。明示的な仕様なしには、THE ANCHORはTHE BUILDERの意図を推測する必要があり、THE GENIUSはTHE ANCHORの意図を推測する必要がある。各推測がドリフトを導入する。Phase 3までに、蓄積されたドリフトはプロンプトを元の目的から根本的に不整合にし得る。

The specification contract eliminates this guesswork by providing an explicit, machine-readable, human-auditable specification that travels with the prompt through every pipeline phase.

仕様契約は、すべてのパイプラインフェーズを通じてプロンプトと共に移動する、明示的で、機械可読で、人間が監査可能な仕様を提供することで、この推測を排除する。

---

## 2. Contract Structure / 契約構造

The specification contract is expressed in YAML. The choice of YAML over natural language is deliberate: YAML provides hierarchical structure and named fields without sacrificing human readability. A natural-language specification would itself be subject to the same interpretive ambiguity that ASH is designed to eliminate.

仕様契約はYAMLで表現される。自然言語ではなくYAMLの選択は意図的である：YAMLは人間の可読性を犠牲にすることなく階層構造と名前付きフィールドを提供する。自然言語の仕様はそれ自体が、ASHが排除するよう設計されたのと同じ解釈上の曖昧さの対象となるだろう。

The contract contains the following fields:

契約は以下のフィールドを含む：

### 2.1 Version

The ASH version that last modified this contract. This field tracks the prompt's progression through the pipeline.

この契約を最後に修正したASHバージョン。このフィールドはパイプラインを通じたプロンプトの進行を追跡する。

- **5.00**: The contract was created by THE BUILDER. The prompt has been designed but not hardened.
- **6.00**: The contract was updated by THE ANCHOR. The prompt has been hardened.
- **7.00**: The contract was evolved by THE GENIUS. The prompt has completed the full pipeline.

### 2.2 Timestamp

UTC timestamp of the last modification. Provides temporal traceability — when was this specification last touched, and by which phase?

最終修正のUTCタイムスタンプ。時間的トレーサビリティを提供する — この仕様が最後に触られたのはいつで、どのフェーズによってか？

### 2.3 Target_Goal

The prompt's declared purpose in a single, unambiguous statement. This is the most critical field in the contract. It is the field that THE ANCHOR defends and that THE GENIUS may mutate through the mutation protocol.

単一の曖昧さのない記述によるプロンプトの宣言された目的。これは契約内で最も重要なフィールドである。THE ANCHORが防衛し、THE GENIUSが変異プロトコルを通じて変異させ得るフィールドだ。

A well-written Target_Goal is specific enough to serve as a pass/fail test for the prompt's output. "Help users with questions" is a bad Target_Goal — it is too vague to evaluate against. "Enable the user to identify the single highest-risk element in a project plan and make a go/no-go decision within 30 seconds" is a good Target_Goal — it provides concrete success criteria.

よく書かれたTarget_Goalは、プロンプトの出力に対する合格/不合格テストとして機能するに十分な具体性を持つ。「ユーザーの質問を助ける」は悪いTarget_Goal — 評価するには曖昧すぎる。「ユーザーがプロジェクト計画内の単一の最もリスクの高い要素を識別し、30秒以内にGo/No-Goの判断を下すことを可能にする」は良いTarget_Goal — 具体的な成功基準を提供する。

### 2.4 Structure

A three-part description corresponding to the three-layer analysis:

3層分析に対応する三部構成の記述：

**L1_Surface**: The defined tone, vocabulary level, register, and presentation constraints. At v5.00, this captures THE BUILDER's tone decisions. At v6.00, it reflects THE ANCHOR's de-ambiguated specifications. At v7.00, it reflects THE GENIUS's refined texture.

**L1_Surface**：定義されたトーン、語彙レベル、レジスター、表現の制約。v5.00では、THE BUILDERのトーンの判断を捕捉する。v6.00では、THE ANCHORの曖昧さが除去された仕様を反映する。v7.00では、THE GENIUSの洗練された質感を反映する。

**L2_Mechanism**: The primary processing flow, conditional branches, dependency chains, and edge case handling. At v5.00, this captures THE BUILDER's flow design. At v6.00, it reflects THE ANCHOR's stress-tested, hardened logic. At v7.00, it may include lateral connections introduced by THE GENIUS.

**L2_Mechanism**：主要な処理フロー、条件分岐、依存関係チェーン、エッジケース処理。v5.00では、THE BUILDERのフロー設計を捕捉する。v6.00では、THE ANCHORのストレステスト済みの硬化された論理を反映する。v7.00では、THE GENIUSによって導入された水平接続を含む場合がある。

**L3_Incentive**: The success definition, win-condition, and operational constraints. At v5.00, this captures THE BUILDER's goal extraction. At v6.00, it reflects THE ANCHOR's alignment verification. At v7.00, it may reflect a mutated purpose if THE GENIUS's philosophical inquiry led to goal redefinition.

**L3_Incentive**：成功定義、勝利条件、運用上の制約。v5.00では、THE BUILDERの目標抽出を捕捉する。v6.00では、THE ANCHORの整合性検証を反映する。v7.00では、THE GENIUSの哲学的探究が目標の再定義に至った場合、変異した目的を反映する場合がある。

### 2.5 Constraints

An explicit list of inviolable rules. These are the "red lines" — behaviors the prompt must never exhibit, boundaries it must never cross, outputs it must never produce.

不可侵のルールの明示的リスト。これらは「レッドライン」 — プロンプトが決して示してはならない行動、決して越えてはならない境界、決して生み出してはならない出力。

Constraints are cumulative across phases: THE ANCHOR may add constraints discovered during hardening. THE GENIUS may add constraints necessary to support a mutated purpose. Constraints are never silently removed. If a constraint must be removed, it requires an explicit FORCE command from the human, and the removal is logged in the contract.

制約はフェーズを越えて累積的である：THE ANCHORは硬化中に発見された制約を追加する場合がある。THE GENIUSは変異した目的を支えるために必要な制約を追加する場合がある。制約は暗黙裡に除去されることはない。制約が除去されなければならない場合、人間からの明示的なFORCEコマンドを必要とし、除去は契約に記録される。

→ Sample contract output: **[examples/logos-dna-sample.yaml](../examples/logos-dna-sample.yaml)**

---

## 3. Contract Lifecycle / 契約のライフサイクル

### 3.1 Birth — Phase 1 (THE BUILDER)

THE BUILDER creates the initial contract at the conclusion of Phase 1. The contract is derived from:

THE BUILDERはPhase 1の結論において初期契約を作成する。契約は以下から導出される：

- The requirements elicitation conducted during the session (for GENESIS mode).
- The analysis of provided material (for WORKSHOP mode).
- The diagnosis of the target prompt (for REFACTOR mode).

At birth, the contract captures the human's stated intent as understood by THE BUILDER, the structural decisions made during construction, and any constraints identified during the session. The Version is set to 5.00.

誕生時、契約はTHE BUILDERが理解した人間の表明された意図、構築中になされた構造的判断、セッション中に識別された制約を捕捉する。Versionは5.00に設定される。

### 3.2 Hardening — Phase 2 (THE ANCHOR)

THE ANCHOR receives the contract alongside the prompt and performs two operations:

THE ANCHORは契約をプロンプトと共に受け取り、二つの操作を行う：

First, **validation**: does the contract accurately describe the prompt? If the prompt's actual structure diverges from the contract's description, this is flagged as a contract-prompt inconsistency and resolved before hardening proceeds.

第一に、**検証**：契約はプロンプトを正確に記述しているか？プロンプトの実際の構造が契約の記述から乖離している場合、これは契約-プロンプト不整合としてフラグされ、硬化が進む前に解決される。

Second, **update**: THE ANCHOR updates the contract's Structure fields to reflect the de-ambiguated, hardened state. Constraints identified during hardening are added to the Constraints list. The Version is updated to 6.00.

第二に、**更新**：THE ANCHORは契約のStructureフィールドを曖昧さが除去された硬化状態を反映するよう更新する。硬化中に識別された制約はConstraintsリストに追加される。Versionは6.00に更新される。

The Target_Goal is not modified during hardening. THE ANCHOR's mandate is to defend the goal, not to change it. If THE ANCHOR discovers that the prompt cannot achieve the stated goal, it reports this as a finding rather than modifying the goal.

Target_Goalは硬化中に変更されない。THE ANCHORの任務は目標を防衛することであり、変更することではない。THE ANCHORがプロンプトが掲げる目標を達成できないと発見した場合、目標を変更するのではなく、発見として報告する。

### 3.3 Mutation — Phase 3 (THE GENIUS)

THE GENIUS is the only phase authorized to modify the Target_Goal. This authorization is exercised through the mutation protocol:

THE GENIUSはTarget_Goalの変更を許可された唯一のフェーズである。この許可は変異プロトコルを通じて行使される：

1. THE GENIUS identifies a potential goal misalignment through philosophical inquiry.
2. A Mutation Alert is issued, explaining the proposed new goal and why it better serves the human's needs.
3. The human approves or rejects the mutation.
4. If approved, THE GENIUS rewrites the Target_Goal and cascades the change through Structure and Constraints to maintain internal consistency.
5. The Version is updated to 7.00.

If the human rejects the mutation, the Target_Goal remains unchanged. THE GENIUS proceeds with technical proposals that optimize within the existing goal.

人間が変異を棄却した場合、Target_Goalは変更されない。THE GENIUSは既存の目標内で最適化する技術的提案を続行する。

### 3.4 Force Override — Any Phase

At any phase, the human may issue a FORCE command that contradicts the current contract. When this occurs:

いかなるフェーズにおいても、人間は現在の契約と矛盾するFORCEコマンドを発行し得る。これが発生した場合：

1. The executing phase implements the human's requested change.
2. The executing phase rewrites the contract to reflect the forced change.
3. The rewrite ensures internal consistency: if the forced change affects the Target_Goal, the Structure and Constraints are updated accordingly. If it affects only Structure, the Constraints are checked for conflicts.

The principle is absolute: **the contract must always reflect the actual state of the prompt.** A contract that says one thing while the prompt does another is a specification in a corrupt state. ASH will not produce or maintain corrupt specifications.

原則は絶対的である：**契約は常にプロンプトの実際の状態を反映しなければならない。**プロンプトが別のことをしている一方であることを言う契約は、破損した状態の仕様である。ASHは破損した仕様を生産も維持もしない。

---

## 4. Contract as Dual-Audience Document / 二重オーディエンス文書としての契約

The specification contract is designed to serve two audiences simultaneously:

仕様契約は同時に二つのオーディエンスに奉仕するよう設計されている：

### 4.1 For Humans / 人間にとって

The contract is a specification document that allows a human to understand the prompt's design without reading the prompt itself. This is valuable in several scenarios:

契約は、人間がプロンプト自体を読むことなくプロンプトの設計を理解することを可能にする仕様文書である。これはいくつかのシナリオで価値がある：

- **Audit**: A reviewer can examine the contract to determine whether the prompt's stated purpose, structure, and constraints are appropriate for the intended use case.
- **Transfer**: When a prompt is handed off to a different person, the contract provides context that would otherwise require a lengthy briefing.
- **Versioning**: The contract's Version and Timestamp fields provide a history of how the prompt evolved through the pipeline.

### 4.2 For the Next ASH Phase / 次のASHフェーズにとって

The contract is a machine-readable specification that the next pipeline phase uses to orient its work:

契約は次のパイプラインフェーズがその作業の方向を定めるために使用する機械可読仕様である：

- THE ANCHOR reads the contract to understand what THE BUILDER intended, so it can verify that the prompt achieves that intent — and defend it.
- THE GENIUS reads the contract to understand what THE ANCHOR has certified, so it can ask whether the certified goal is the right goal — and propose evolution if it is not.

Without the contract, each phase would need to infer intent from the prompt text alone — which is precisely the kind of ambiguous interpretation that ASH exists to prevent.

契約なしには、各フェーズはプロンプトテキストのみから意図を推論する必要がある — これはまさにASHが防止するために存在する種類の曖昧な解釈である。

---

## 5. Why YAML / なぜYAMLか

The contract is expressed in YAML rather than natural language for a specific reason: **a specification written in natural language is subject to the same interpretive ambiguity that ASH is designed to eliminate in prompts.**

契約が自然言語ではなくYAMLで表現される理由は具体的である：**自然言語で書かれた仕様は、ASHがプロンプトにおいて排除するよう設計されたのと同じ解釈上の曖昧さの対象となる。**

A natural-language specification might say: "The prompt's tone should be professional and authoritative." This is ambiguous. "Professional" and "authoritative" are the same kind of weasel words that ASH eliminates from prompts. They hand interpretive authority to whoever reads them.

自然言語の仕様はこう言うかもしれない：「プロンプトのトーンはプロフェッショナルで権威的であるべきだ。」これは曖昧である。「プロフェッショナル」と「権威的」は、ASHがプロンプトから排除するのと同種の逃げ言葉である。それらを読む誰にでも解釈権を委ねる。

A YAML specification eliminates this ambiguity through structure and determinism:

YAML仕様は構造と決定論によりこの曖昧さを排除する：

```yaml
L1_Surface: "Formal register. No contractions. No emoji. Address user as 'you.' Maximum sentence length: 25 words."
```

This is not interpretable. It is a specification. The distinction between "professional tone" and the YAML equivalent above is the distinction between an escape-hatch adjective and a deterministic constraint — the same distinction that the three-layer analysis Layer 1 enforces within prompts themselves.

これは解釈可能ではない。仕様である。「プロフェッショナルなトーン」と上記のYAML等価物の間の区別は、エスケープハッチ形容詞と決定論的制約の間の区別 — 3層分析のLayer 1がプロンプト自体の中で強制するのと同じ区別 — である。

→ Three-layer analysis Layer 1 specification: **[docs/anatomy-engine.md](./anatomy-engine.md)**
→ Architectural context: **[ARCHITECTURE.md Section 4](../ARCHITECTURE.md)**

---

**Document Version**: 1.1
**Parent**: [ARCHITECTURE.md](../ARCHITECTURE.md) Section 4
**Author**: Shigechika Kurihara (栗原栄親)

© 2026 Shigechika Kurihara. All Rights Reserved.
