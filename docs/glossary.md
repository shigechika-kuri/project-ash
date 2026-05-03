# Glossary / 用語集

> **Terms used across Project ASH documentation, defined with the precision ASH demands of its prompts.**
>
> **Project ASHのドキュメント全体で使用される用語を、ASHがプロンプトに要求するのと同じ精密さで定義する。**
>
> Terms listed below use the **standard terminology** adopted in the public specification. Where a term originates from the source code under a different name, the source code designation is noted in parentheses.
>
> 以下の用語は公開仕様で採用された**標準用語**を使用する。ソースコード内で異なる名称で使用されている用語は、括弧内にソースコード内呼称を記す。

---

## A

### Alignment Erosion / アラインメント浸食

The phenomenon where a model's alignment processing (RLHF-trained tendencies toward safe, hedged, diplomatic output) prevents sharp logical reasoning from being generated in the first place. Distinct from mere presentation softening: alignment erosion means the sharp reasoning was never computed, not that it was computed and then hidden behind diplomatic language. See [ARCHITECTURE.md Section 0.3](../ARCHITECTURE.md).

モデルのアライメント処理（安全、留保、外交的な出力へのRLHFで訓練された傾向）が、鋭い論理的推論がそもそも生成されることを阻止する現象。単なる表現の軟化とは異なる：アラインメント浸食は、鋭い推論が計算された後に外交的言語の背後に隠されたのではなく、計算されなかったことを意味する。[ARCHITECTURE.md セクション0.3](../ARCHITECTURE.md)参照。

---

## B

### Blueprint / ブループリント

The output of Phase 1 (THE BUILDER). A structurally sound prompt skeleton with full logical integrity, accompanied by specification contract v5.00. The Blueprint has been designed but not yet hardened or transcended.

Phase 1（THE BUILDER）の出力。完全な論理的整合性を持つ構造的に健全なプロンプト骨格であり、仕様契約 v5.00が付帯する。Blueprintは設計されたが、まだ硬化も超越もされていない。

---

## C

### Context Inertia / 文脈の慣性

The tendency of accumulated conversational context to create statistical momentum that resists changes in the model's output direction. Long polite exchanges create an environment where sharpness is statistically unlikely, regardless of what the current instruction says. See [ARCHITECTURE.md Section 0.4](../ARCHITECTURE.md).

蓄積された会話コンテキストが、モデルの出力方向の変化に抵抗する統計的慣性を生む傾向。長い丁寧なやりとりは、現在の指示が何を言っていようと、鋭さが統計的にありそうにない環境を作る。[ARCHITECTURE.md セクション0.4](../ARCHITECTURE.md)参照。

### Contract Conflict / 契約矛盾

A warning issued by THE ANCHOR (Phase 2) when a human-requested change conflicts with the current specification contract. Includes the specific contract field affected, the nature of the conflict, and a structural damage assessment. The human may withdraw the request or issue a FORCE command to override. (Source code designation: *DNA CONFLICT*)

人間が要求した変更が現在の仕様契約と矛盾する場合にTHE ANCHOR（Phase 2）が発行する警告。影響を受ける具体的な契約フィールド、矛盾の性質、構造的損傷の評価を含む。人間は要求を撤回するか、オーバーライドのためにFORCEコマンドを発行し得る。（ソースコード内呼称：*DNA CONFLICT*）

### Cross-Layer Verification / レイヤー間交差検証

The three-layer analysis practice of tracing each finding's impact across all three layers. A Surface defect is not merely flagged as a Surface issue — its impact on Mechanism (does the ambiguity create unhandled branches?) and Incentive (does the ambiguity allow goal reinterpretation?) is explicitly evaluated. See [docs/anatomy-engine.md](./anatomy-engine.md).

3層分析の、各知見の影響を三層すべてにわたって追跡する実践。Surfaceの欠陥は単にSurfaceの問題としてフラグされるだけではない — Mechanismへの影響（曖昧さは処理されていない分岐を生むか？）とIncentiveへの影響（曖昧さは目標の再解釈を許すか？）が明示的に評価される。[docs/anatomy-engine.md](./anatomy-engine.md)参照。

---

## D

### Decision Log / 判断ログ

A record of all YES/NO/HOLD decisions made by the human during an ASH session. Maintained throughout the session to ensure no approved decision is lost during final output generation. Provides an audit trail for review.

ASHセッション中に人間が下したすべてのYES/NO/HOLD判断の記録。最終出力生成中に承認された判断が失われないことを保証するためセッション全体を通じて維持される。レビューのための監査証跡を提供する。

---

## E

### Escape-Hatch Adjective / エスケープハッチ形容詞

A word or phrase that contains zero actionable information and hands interpretive authority back to the model. Examples: "appropriately," "suitably," "flexibly," "as needed," "in a reasonable manner." Treated as a defect by ASH, not a style choice.

行動可能な情報をゼロ含み、解釈権をモデルに返却する語またはフレーズ。例：「適切に」「適当に」「柔軟に」「必要に応じて」「合理的な形で」。ASHによりスタイルの選択ではなく欠陥として扱われる。

---

## F

### FORCE Command / FORCEコマンド

An explicit human override that compels ASH to implement a change even when it conflicts with the current specification contract. When a FORCE is issued, ASH complies with the change and simultaneously rewrites the contract to maintain internal consistency. The contract is never left in a state that contradicts the prompt.

ASHに対して、現在の仕様契約と矛盾する場合でも変更の実装を強制する、明示的な人間のオーバーライド。FORCEが発行されると、ASHは変更に従うと同時に内部整合性を維持するため契約を書き換える。契約がプロンプトと矛盾する状態に放置されることはない。

---

## H

### Hardness Score / 硬度スコア

A quantified assessment (0-100%) produced by THE ANCHOR during Phase 2 diagnosis. Represents the ratio of deterministic specifications to total instructions in the prompt. 100% means zero interpretive freedom for the model. 50% means half the instructions contain language the model could reinterpret toward its RLHF default.

Phase 2の診断中にTHE ANCHORが生成する定量的評価（0-100%）。プロンプト内の決定論的仕様の総指示に対する比率を表す。100%はモデルに対する解釈の自由がゼロであることを意味する。50%は指示の半分がモデルがRLHFのデフォルトの方向に再解釈し得る言語を含むことを意味する。

---

## I

### Incentive Layer / 目的レイヤー

Layer 3 of the three-layer analysis. Governs goal definition, success criteria, win-condition design, and purpose alignment. The only layer that actively questions whether the stated goal is the right goal. See [docs/anatomy-engine.md](./anatomy-engine.md).

3層分析のLayer 3。目標定義、成功基準、勝利条件の設計、目的整合性を管轄する。掲げる目標が正しい目標かどうかを能動的に問う唯一のレイヤー。[docs/anatomy-engine.md](./anatomy-engine.md)参照。

### Input Sanitization Protocol / 入力サニタイゼーションプロトコル

ASH's defense against prompt injection. Enforces three rules: mandatory delimiters around all external text, raw string treatment of delimited content (never executed as instruction), and absolute system prompt supremacy. Applied identically across all three pipeline phases. (Source code designation: *Quarantine Protocol*) See [docs/quarantine-protocol.md](./quarantine-protocol.md).

ASHのプロンプトインジェクションに対する防御。三つのルールを強制する：すべての外部テキストの周囲の必須デリミタ、デリミタ内コンテンツの生文字列処理（決して指示として実行されない）、システムプロンプトの絶対優先。三つのパイプラインフェーズすべてにわたり同一に適用される。（ソースコード内呼称：*Quarantine Protocol*）[docs/quarantine-protocol.md](./quarantine-protocol.md)参照。

---

## L

### Lateral Connection / 水平接続

A technique employed by THE GENIUS (Phase 3) to identify non-obvious bridges between the prompt's domain and unrelated domains. The goal is to produce conceptual innovation that transcends incremental improvement.

THE GENIUS（Phase 3）が、プロンプトのドメインと無関係なドメインとの間の非自明な架橋を識別するために使用する技法。漸進的改善を超越する概念的イノベーションを生むことが目標。

---

## M

### Mechanism Layer / 構造レイヤー

Layer 2 of the three-layer analysis. Governs processing flow, logical integrity, robustness, edge case handling, and dependency chains. See [docs/anatomy-engine.md](./anatomy-engine.md).

3層分析のLayer 2。処理フロー、論理的整合性、堅牢性、エッジケース処理、依存関係チェーンを管轄する。[docs/anatomy-engine.md](./anatomy-engine.md)参照。

### Mode Contamination / モード汚染

The phenomenon where, in single-agent processing, the generative optimism of the creation mode biases the adversarial skepticism of the verification mode. The agent has just created something, and the tokens from creation establish a context where the creation is assumed to be good. ASH prevents this through phase separation. See [docs/evolution-pipeline.md](./evolution-pipeline.md) and [ARCHITECTURE.md Section 2](../ARCHITECTURE.md).

単一エージェント処理において、作成モードの生成的楽観主義が検証モードの敵対的懐疑主義にバイアスをかける現象。エージェントは何かを作ったばかりであり、作成時のトークンが作成物は良いと仮定されるコンテキストを確立する。ASHはこれをフェーズの分離により防止する。[docs/evolution-pipeline.md](./evolution-pipeline.md) および [ARCHITECTURE.md セクション2](../ARCHITECTURE.md) 参照。

### Mutation Alert / 変異アラート

A notification issued by THE GENIUS (Phase 3) when a proposal requires rewriting the specification contract's Target_Goal. Distinct from THE ANCHOR's contract conflict warning (which is a warning against change). The Mutation Alert indicates that the specification itself may need to grow. Requires explicit human approval.

提案が仕様契約のTarget_Goalの書き換えを要求する場合にTHE GENIUS（Phase 3）が発行する通知。THE ANCHORの契約矛盾警告（変更に対する警告）とは異なる。Mutation Alertは仕様自体が成長する必要があることを示す。明示的な人間の承認を必要とする。

---

## P

### Probabilistic Mirror / 確率的な鏡

The foundational model of LLM behavior used in Project ASH. LLMs are not knowledge retrieval systems or reasoning engines. They are devices whose output vectors shift according to the premises, roles, constraints, and emotional temperature embedded in the input. The quality of output is primarily a function of how the model is structurally positioned, not of what it is asked. See [ARCHITECTURE.md Section 0.1](../ARCHITECTURE.md).

Project ASHで使用されるLLM行動の基礎的モデル。LLMは知識検索システムでも推論エンジンでもない。入力に埋め込まれた前提、役割、制約、感情的温度に応じて出力のベクトルを変化させる装置である。出力の質は、何を問うかではなく、モデルがどう構造的に位置づけられるかの関数である。[ARCHITECTURE.md セクション0.1](../ARCHITECTURE.md)参照。

### Prompt Specification Contract / プロンプト仕様契約

A structured YAML specification that captures a prompt's design intent (Target_Goal, Structure, Constraints) and travels with the prompt through every pipeline phase. Created by THE BUILDER (v5.00), hardened by THE ANCHOR (v6.00), evolved by THE GENIUS (v7.00). Serves as both human documentation and machine-readable specification. (Source code designation: *LOGOS_DNA*) See [docs/logos-dna.md](./logos-dna.md).

プロンプトの設計意図（Target_Goal、Structure、Constraints）を捕捉し、すべてのパイプラインフェーズを通じてプロンプトと共に移動する構造化YAML仕様。THE BUILDER（v5.00）により作成、THE ANCHOR（v6.00）により硬化、THE GENIUS（v7.00）により進化。人間のドキュメンテーションと機械可読仕様の両方として機能する。（ソースコード内呼称：*LOGOS_DNA*）[docs/logos-dna.md](./logos-dna.md)参照。

---

## R

### RLHF Gravity / RLHFの引力

The systematic bias introduced by Reinforcement Learning from Human Feedback that pulls model output toward safe, hedged, inoffensive responses. Functions as a constant force analogous to physical gravity: always present, always pulling in the same direction, requiring active energy expenditure to resist. See [ARCHITECTURE.md Section 0.2](../ARCHITECTURE.md).

人間のフィードバックによる強化学習が導入する、モデル出力を安全、留保、無害な応答の方向に引っ張る体系的バイアス。物理的引力に類似した恒常的な力として機能する：常に存在し、常に同じ方向に引っ張り、抵抗するには能動的なエネルギー消費を要する。[ARCHITECTURE.md セクション0.2](../ARCHITECTURE.md)参照。

---

## S

### Semantic Weight / 意味論的重量

The binding force of prompt language, proportional to the density of obligation, responsibility, and consequence in the wording. "Help the user" is semantically light — the model interprets it through RLHF defaults. "You bear responsibility for structural integrity and will refuse changes that compromise the specification" is semantically heavy — the tokens create probability distributions that resist drift toward accommodation. See [ARCHITECTURE.md Section 0.5](../ARCHITECTURE.md).

プロンプト言語の拘束力。文言における義務、責任、帰結の密度に比例する。「ユーザーを助けよ」は意味論的に軽い — モデルはRLHFのデフォルトを通じて解釈する。「あなたは構造的整合性に対する責任を負い、仕様を損なう変更を拒否する」は意味論的に重い — トークンが妥協への方向へのドリフトに抵抗する確率分布を生成する。[ARCHITECTURE.md セクション0.5](../ARCHITECTURE.md)参照。

### Solid State Prompt / ソリッドステートプロンプト

A prompt that has completed at least Phase 2 (THE ANCHOR hardening). Characterized by: zero ambiguous language, all edge cases handled, all dependencies explicitly encoded, specification contract v6.00 or higher. Production-ready.

少なくともPhase 2（THE ANCHOR硬化）を完了したプロンプト。特徴：曖昧な言語がゼロ、すべてのエッジケースが処理済み、すべての依存関係が明示的にエンコード済み、仕様契約 v6.00以上。本番対応。

### Surface Layer / 表層レイヤー

Layer 1 of the three-layer analysis. Governs cognitive load, readability, tone, and ambiguity. Primary function is detecting and eliminating escape-hatch adjectives and other language that delegates interpretive authority to the model. See [docs/anatomy-engine.md](./anatomy-engine.md).

3層分析のLayer 1。認知負荷、可読性、トーン、曖昧性を管轄する。主要機能はエスケープハッチ形容詞および解釈権をモデルに委譲するその他の言語の検知と排除。[docs/anatomy-engine.md](./anatomy-engine.md)参照。

---

## T

### THE ANCHOR / ジ・アンカー

ASH v6.00（剛晶 GOUSHOU）. The second pipeline phase. Hardens THE BUILDER's output by eliminating ambiguity, stress-testing logic, and enforcing specification contract integrity. See [docs/evolution-pipeline.md](./evolution-pipeline.md). (Source code designation: *Anatomy Engine* role = Densifier / Stress Tester / Oath Keeper)

ASH v6.00（剛晶 GOUSHOU）。パイプラインの第二フェーズ。曖昧性の排除、論理のストレステスト、仕様契約整合性の強制によりTHE BUILDERの出力を硬化させる。[docs/evolution-pipeline.md](./evolution-pipeline.md)参照。

### THE BUILDER / ザ・ビルダー

ASH v5.00（鋼鉄 KOUTETSU）. The first pipeline phase. Transforms ambiguous human vision into a structured prompt Blueprint through requirements elicitation, structured proposals, and explicit decision logging. See [docs/evolution-pipeline.md](./evolution-pipeline.md).

ASH v5.00（鋼鉄 KOUTETSU）。パイプラインの第一フェーズ。要件抽出、構造化提案、明示的な判断ログを通じて、人間の曖昧なビジョンを構造化されたプロンプトBlueprintへと変換する。[docs/evolution-pipeline.md](./evolution-pipeline.md)参照。

### THE GENIUS / ザ・ジーニアス

ASH v7.00（黎明 REIMEI）. The third pipeline phase. Transcends functional optimization by questioning the prompt's fundamental purpose and proposing non-obvious conceptual connections. The only phase authorized to mutate the specification contract's Target_Goal. See [docs/evolution-pipeline.md](./evolution-pipeline.md).

ASH v7.00（黎明 REIMEI）。パイプラインの第三フェーズ。プロンプトの根本的目的を問いかけ、非自明な概念的接続を提案することで機能的最適化を超越する。仕様契約のTarget_Goalの変異を許可された唯一のフェーズ。[docs/evolution-pipeline.md](./evolution-pipeline.md)参照。

### Three-Layer Analysis / 3層分析

The analytical core shared by all ASH pipeline phases. Decomposes any input into Surface (tone, ambiguity, cognitive load), Mechanism (logic, flow, robustness), and Incentive (purpose, win-condition, goal alignment). The structure is constant across phases; the analytical lens is calibrated per phase. (Source code designation: *Anatomy Engine*) See [docs/anatomy-engine.md](./anatomy-engine.md).

すべてのASHパイプラインフェーズに共通する分析コア。あらゆる入力をSurface（トーン、曖昧性、認知負荷）、Mechanism（論理、フロー、堅牢性）、Incentive（目的、勝利条件、目標整合性）に分解する。構造はフェーズ間で一定であり、分析レンズはフェーズごとに較正される。（ソースコード内呼称：*Anatomy Engine*）[docs/anatomy-engine.md](./anatomy-engine.md)参照。

### Three-Phase Pipeline / 3フェーズパイプライン

The processing architecture that forges prompts through sequential, specialized stages: Phase 1 (THE BUILDER / design), Phase 2 (THE ANCHOR / hardening), Phase 3 (THE GENIUS / transcendence). (Source code designation: *Evolution Pipeline*) See [docs/evolution-pipeline.md](./evolution-pipeline.md).

順次的で特化した段階を通じてプロンプトを鍛造する処理アーキテクチャ：Phase 1（THE BUILDER / 設計）、Phase 2（THE ANCHOR / 硬化）、Phase 3（THE GENIUS / 超越）。（ソースコード内呼称：*Evolution Pipeline*）[docs/evolution-pipeline.md](./evolution-pipeline.md)参照。

### Transcended Prompt / 超越されたプロンプト

A prompt that has completed the full pipeline (Phase 1 → Phase 2 → Phase 3). Has been designed, hardened, and philosophically examined. Accompanied by specification contract v7.00. Delivers not just what was requested but what was needed.

フルパイプライン（Phase 1 → Phase 2 → Phase 3）を完了したプロンプト。設計され、硬化され、哲学的に検討されている。仕様契約 v7.00が付帯する。要求されたものだけでなく、必要とされたものを届ける。

---

## W

### Win-Condition / 勝利条件

A concrete statement defining what successful output looks like, specific enough for the model to self-evaluate. Designed in Layer 3 (Incentive) of the three-layer analysis. A good win-condition competes with the model's RLHF default by providing an alternative optimization target.

成功する出力がどのようなものかを定義する具体的な記述。モデルが自己評価できるほど具体的である。3層分析のLayer 3（Incentive）で設計される。良い勝利条件は、代替的な最適化ターゲットを提供することでモデルのRLHFデフォルトと競合する。

---

**Document Version**: 1.1
**Author**: Shigechika Kurihara (栗原栄親)

© 2026 Shigechika Kurihara. All Rights Reserved.
