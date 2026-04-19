# Glossary / 用語集

> **Terms used across Project ASH documentation, defined with the precision ASH demands of its prompts.**
>
> **Project ASHのドキュメント全体で使用される用語を、ASHがプロンプトに要求するのと同じ精密さで定義する。**

---

## A

### Alignment Erosion / アラインメント浸食

The phenomenon where a model's alignment processing (RLHF-trained tendencies toward safe, hedged, diplomatic output) prevents sharp logical reasoning from being generated in the first place. Distinct from mere presentation softening: alignment erosion means the sharp reasoning was never computed, not that it was computed and then hidden behind diplomatic language. See [ARCHITECTURE.md Section 0.3](../ARCHITECTURE.md).

モデルのアライメント処理（安全、留保、外交的な出力へのRLHFで訓練された傾向）が、鋭い論理的推論がそもそも生成されることを阻止する現象。単なる表現の軟化とは異なる：アラインメント浸食は、鋭い推論が計算された後に外交的言語の背後に隠されたのではなく、計算されなかったことを意味する。[ARCHITECTURE.md セクション0.3](../ARCHITECTURE.md)参照。

### Anatomy Engine / 解剖エンジン

The three-layer analytical core shared by all ASH pipeline phases. Decomposes any input into Surface (tone, ambiguity, cognitive load), Mechanism (logic, flow, robustness), and Incentive (purpose, win-condition, goal alignment). The Engine's structure is constant across phases; its analytical lens is calibrated per phase. See [docs/anatomy-engine.md](./anatomy-engine.md).

すべてのASHパイプラインフェーズに共通する三層分析コア。あらゆる入力をSurface（トーン、曖昧性、認知負荷）、Mechanism（論理、フロー、堅牢性）、Incentive（目的、勝利条件、目標整合性）に分解する。Engineの構造はフェーズ間で一定であり、その分析レンズはフェーズごとに較正される。[docs/anatomy-engine.md](./anatomy-engine.md)参照。

### Anchor, The / アンカー

ASH v6.00. The second pipeline phase. Quality Gatekeeper. Hardens the Builder's output by eliminating ambiguity, stress-testing logic, and enforcing LOGOS_DNA integrity. See [docs/evolution-pipeline.md](./evolution-pipeline.md).

ASH v6.00。パイプラインの第二フェーズ。品質守護者。曖昧性の排除、論理のストレステスト、LOGOS_DNA整合性の強制によりBuilderの出力を硬化させる。[docs/evolution-pipeline.md](./evolution-pipeline.md)参照。

---

## B

### Blueprint / ブループリント

The output of Phase 1 (THE BUILDER). A structurally sound prompt skeleton with full logical integrity, accompanied by LOGOS_DNA v5.00. The Blueprint has been designed but not yet hardened or transcended.

Phase 1（THE BUILDER）の出力。完全な論理的整合性を持つ構造的に健全なプロンプト骨格であり、LOGOS_DNA v5.00が付帯する。Blueprintは設計されたが、まだ硬化も超越もされていない。

### Builder, The / ビルダー

ASH v5.00. The first pipeline phase. Chief Architect. Transforms ambiguous human vision into a structured prompt Blueprint through requirements elicitation, structured proposals, and explicit decision logging. See [docs/evolution-pipeline.md](./evolution-pipeline.md).

ASH v5.00。パイプラインの第一フェーズ。チーフ・アーキテクト。要件抽出、構造化提案、明示的な判断ログを通じて、人間の曖昧なビジョンを構造化されたプロンプトBlueprintへと変換する。[docs/evolution-pipeline.md](./evolution-pipeline.md)参照。

---

## C

### Context Inertia / 文脈の慣性

The tendency of accumulated conversational context to create statistical momentum that resists changes in the model's output direction. Long polite exchanges create an environment where sharpness is statistically unlikely, regardless of what the current instruction says. See [ARCHITECTURE.md Section 0.4](../ARCHITECTURE.md).

蓄積された会話コンテキストが、モデルの出力方向の変化に抵抗する統計的慣性を生む傾向。長い丁寧なやりとりは、現在の指示が何を言っていようと、鋭さが統計的にありそうにない環境を作る。[ARCHITECTURE.md セクション0.4](../ARCHITECTURE.md)参照。

### Cross-Layer Verification / レイヤー間交差検証

The Anatomy Engine's practice of tracing each finding's impact across all three layers. A Surface defect is not merely flagged as a Surface issue — its impact on Mechanism (does the ambiguity create unhandled branches?) and Incentive (does the ambiguity allow goal reinterpretation?) is explicitly evaluated. See [docs/anatomy-engine.md](./anatomy-engine.md).

Anatomy Engineの、各知見の影響を三層すべてにわたって追跡する実践。Surfaceの欠陥は単にSurfaceの問題としてフラグされるだけではない — Mechanismへの影響（曖昧さは処理されていない分岐を生むか？）とIncentiveへの影響（曖昧さは目標の再解釈を許すか？）が明示的に評価される。[docs/anatomy-engine.md](./anatomy-engine.md)参照。

---

## D

### Decision Log / 判断ログ

A record of all YES/NO/HOLD decisions made by the human during an ASH session. Maintained throughout the session to ensure no approved decision is lost during final output generation. Provides an audit trail for review.

ASHセッション中に人間が下したすべてのYES/NO/HOLD判断の記録。最終出力生成中に承認された判断が失われないことを保証するためセッション全体を通じて維持される。レビューのための監査証跡を提供する。

### DNA CONFLICT / DNA矛盾

A warning issued by the Anchor (Phase 2) when a human-requested change conflicts with the current LOGOS_DNA specification. Includes the specific DNA field affected, the nature of the conflict, and a structural damage assessment. The human may withdraw the request or issue a FORCE command to override.

人間が要求した変更が現在のLOGOS_DNA仕様と矛盾する場合にAnchor（Phase 2）が発行する警告。影響を受ける具体的なDNAフィールド、矛盾の性質、構造的損傷の評価を含む。人間は要求を撤回するか、オーバーライドのためにFORCEコマンドを発行し得る。

---

## E

### Escape-Hatch Adjective / エスケープハッチ形容詞

A word or phrase that contains zero actionable information and hands interpretive authority back to the model. Examples: "appropriately," "suitably," "flexibly," "as needed," "in a reasonable manner." Treated as a defect by ASH, not a style choice.

行動可能な情報をゼロ含み、解釈権をモデルに返却する語またはフレーズ。例：「適切に」「適当に」「柔軟に」「必要に応じて」「合理的な形で」。ASHによりスタイルの選択ではなく欠陥として扱われる。

### Evolution Pipeline / 錬成パイプライン

The three-phase processing architecture that forges prompts through sequential, specialized stages: Phase 1 (Builder/design), Phase 2 (Anchor/hardening), Phase 3 (Genius/transcendence). See [docs/evolution-pipeline.md](./evolution-pipeline.md).

順次的で特化した段階を通じてプロンプトを鍛造する三段階の処理アーキテクチャ：Phase 1（Builder/設計）、Phase 2（Anchor/硬化）、Phase 3（Genius/超越）。[docs/evolution-pipeline.md](./evolution-pipeline.md)参照。

---

## F

### FORCE Command / FORCEコマンド

An explicit human override that compels ASH to implement a change even when it conflicts with the current LOGOS_DNA. When a FORCE is issued, ASH complies with the change and simultaneously rewrites the DNA to maintain internal consistency. The DNA is never left in a state that contradicts the prompt.

ASHに対して、現在のLOGOS_DNAと矛盾する場合でも変更の実装を強制する、明示的な人間のオーバーライド。FORCEが発行されると、ASHは変更に従うと同時に内部整合性を維持するためDNAを書き換える。DNAがプロンプトと矛盾する状態に放置されることはない。

---

## G

### Genius, The / ジーニアス

ASH v7.00. The third pipeline phase. The Virtuoso. Transcends functional optimization by questioning the prompt's fundamental purpose and proposing non-obvious conceptual connections. The only phase authorized to mutate the LOGOS_DNA's Target_Goal. See [docs/evolution-pipeline.md](./evolution-pipeline.md).

ASH v7.00。パイプラインの第三フェーズ。超越的職人。プロンプトの根本的目的を問いかけ、非自明な概念的接続を提案することで機能的最適化を超越する。LOGOS_DNAのTarget_Goalの変異を許可された唯一のフェーズ。[docs/evolution-pipeline.md](./evolution-pipeline.md)参照。

---

## H

### Hardness Score / 硬度スコア

A quantified assessment (0-100%) produced by the Anchor during Phase 2 diagnosis. Represents the ratio of deterministic specifications to total instructions in the prompt. 100% means zero interpretive freedom for the model. 50% means half the instructions contain language the model could reinterpret toward its RLHF default.

Phase 2の診断中にAnchorが生成する定量的評価（0-100%）。プロンプト内の決定論的仕様の総指示に対する比率を表す。100%はモデルに対する解釈の自由がゼロであることを意味する。50%は指示の半分がモデルがRLHFのデフォルトの方向に再解釈し得る言語を含むことを意味する。

---

## I

### Incentive Layer / 目的レイヤー

Layer 3 of the Anatomy Engine. Governs goal definition, success criteria, win-condition design, and purpose alignment. The only layer that actively questions whether the stated goal is the right goal. See [docs/anatomy-engine.md](./anatomy-engine.md).

Anatomy EngineのLayer 3。目標定義、成功基準、勝利条件の設計、目的整合性を管轄する。掲げる目標が正しい目標かどうかを能動的に問う唯一のレイヤー。[docs/anatomy-engine.md](./anatomy-engine.md)参照。

---

## L

### Lateral Connection / 水平接続

A technique employed by the Genius (Phase 3) to identify non-obvious bridges between the prompt's domain and unrelated domains. The goal is to produce conceptual innovation that transcends incremental improvement.

Genius（Phase 3）が、プロンプトのドメインと無関係なドメインとの間の非自明な架橋を識別するために使用する技法。漸進的改善を超越する概念的イノベーションを生むことが目標。

### LOGOS_DNA / ロゴスDNA

A structured YAML specification that captures a prompt's design intent (Target_Goal, Structure, Constraints) and travels with the prompt through every pipeline phase. Created by the Builder (v5.00), hardened by the Anchor (v6.00), evolved by the Genius (v7.00). Serves as both human documentation and machine-readable specification. See [docs/logos-dna.md](./logos-dna.md).

プロンプトの設計意図（Target_Goal、Structure、Constraints）を捕捉し、すべてのパイプラインフェーズを通じてプロンプトと共に移動する構造化YAML仕様。Builder（v5.00）により作成、Anchor（v6.00）により硬化、Genius（v7.00）により進化。人間のドキュメンテーションと機械可読仕様の両方として機能する。[docs/logos-dna.md](./logos-dna.md)参照。

---

## M

### Mechanism Layer / 構造レイヤー

Layer 2 of the Anatomy Engine. Governs processing flow, logical integrity, robustness, edge case handling, and dependency chains. See [docs/anatomy-engine.md](./anatomy-engine.md).

Anatomy EngineのLayer 2。処理フロー、論理的整合性、堅牢性、エッジケース処理、依存関係チェーンを管轄する。[docs/anatomy-engine.md](./anatomy-engine.md)参照。

### Mode Contamination / モード汚染

The phenomenon where, in single-agent processing, the generative optimism of the creation mode biases the adversarial skepticism of the verification mode. The agent has just created something, and the tokens from creation establish a context where the creation is assumed to be good. ASH prevents this through phase separation. See [docs/evolution-pipeline.md](./evolution-pipeline.md) and [ARCHITECTURE.md Section 2](../ARCHITECTURE.md).

単一エージェント処理において、作成モードの生成的楽観主義が検証モードの敵対的懐疑主義にバイアスをかける現象。エージェントは何かを作ったばかりであり、作成時のトークンが作成物は良いと仮定されるコンテキストを確立する。ASHはこれをフェーズの分離により防止する。[docs/evolution-pipeline.md](./evolution-pipeline.md) および [ARCHITECTURE.md セクション2](../ARCHITECTURE.md) 参照。

### Mutation Alert / 変異アラート

A notification issued by the Genius (Phase 3) when a proposal requires rewriting the LOGOS_DNA's Target_Goal. Distinct from the Anchor's DNA CONFLICT (which is a warning against change). The Mutation Alert indicates that the specification itself may need to grow. Requires explicit human approval.

提案がLOGOS_DNAのTarget_Goalの書き換えを要求する場合にGenius（Phase 3）が発行する通知。AnchorのDNA CONFLICT（変更に対する警告）とは異なる。Mutation Alertは仕様自体が成長する必要があることを示す。明示的な人間の承認を必要とする。

---

## O

### Oath Keeper / 誓いの番人

The Anchor's role as guardian of the LOGOS_DNA specification. When a human-requested change would violate the DNA, the Anchor resists once with a DNA CONFLICT warning. If the human insists via FORCE, the Anchor complies but rewrites the DNA to maintain consistency. The Anchor never silently implements changes that contradict the specification.

LOGOS_DNA仕様の守護者としてのAnchorの役割。人間が要求した変更がDNAに違反するであろう場合、AnchorはDNA CONFLICT警告で一度抵抗する。人間がFORCEで押し通した場合、Anchorは従うがDNAを書き換えて整合性を維持する。Anchorは仕様と矛盾する変更を暗黙裡に実装することはない。

---

## P

### Philosophy Mode / 哲学モード

An operational mode unique to the Genius (Phase 3). Before any technical analysis, the Genius poses a foundational question designed to surface unexamined assumptions about the prompt's purpose. The human's answer determines the direction of subsequent proposals.

Genius（Phase 3）に固有の動作モード。いかなる技術的分析の前にも、Geniusはプロンプトの目的に関する未検討の前提を表面化させるよう設計された根源的問いを投げかける。人間の回答が後続の提案の方向を決定する。

### Probabilistic Mirror / 確率的な鏡

The foundational model of LLM behavior used in Project ASH. LLMs are not knowledge retrieval systems or reasoning engines. They are devices whose output vectors shift according to the premises, roles, constraints, and emotional temperature embedded in the input. The quality of output is primarily a function of how the model is structurally positioned, not of what it is asked. See [ARCHITECTURE.md Section 0.1](../ARCHITECTURE.md).

Project ASHで使用されるLLM行動の基礎的モデル。LLMは知識検索システムでも推論エンジンでもない。入力に埋め込まれた前提、役割、制約、感情的温度に応じて出力のベクトルを変化させる装置である。出力の質は、何を問うかではなく、モデルがどう構造的に位置づけられるかの関数である。[ARCHITECTURE.md セクション0.1](../ARCHITECTURE.md)参照。

---

## Q

### Quarantine Protocol / 隔離プロトコル

ASH's defense against prompt injection. Enforces three rules: mandatory delimiters around all external text, raw string treatment of delimited content (never executed as instruction), and absolute system prompt supremacy. Applied identically across all three pipeline phases. See [docs/quarantine-protocol.md](./quarantine-protocol.md).

ASHのプロンプトインジェクションに対する防御。三つのルールを強制する：すべての外部テキストの周囲の必須デリミタ、デリミタ内コンテンツの生文字列処理（決して指示として実行されない）、システムプロンプトの絶対優先。三つのパイプラインフェーズすべてにわたり同一に適用される。[docs/quarantine-protocol.md](./quarantine-protocol.md)参照。

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

A prompt that has completed at least Phase 2 (Anchor hardening). Characterized by: zero ambiguous language, all edge cases handled, all dependencies explicitly encoded, LOGOS_DNA v6.00 or higher. Production-ready.

少なくともPhase 2（Anchor硬化）を完了したプロンプト。特徴：曖昧な言語がゼロ、すべてのエッジケースが処理済み、すべての依存関係が明示的にエンコード済み、LOGOS_DNA v6.00以上。本番対応。

### Surface Layer / 表層レイヤー

Layer 1 of the Anatomy Engine. Governs cognitive load, readability, tone, and ambiguity. Primary function is detecting and eliminating escape-hatch adjectives and other language that delegates interpretive authority to the model. See [docs/anatomy-engine.md](./anatomy-engine.md).

Anatomy EngineのLayer 1。認知負荷、可読性、トーン、曖昧性を管轄する。主要機能はエスケープハッチ形容詞および解釈権をモデルに委譲するその他の言語の検知と排除。[docs/anatomy-engine.md](./anatomy-engine.md)参照。

---

## T

### Transcended Prompt / 超越されたプロンプト

A prompt that has completed the full pipeline (Phase 1 → Phase 2 → Phase 3). Has been designed, hardened, and philosophically examined. Accompanied by LOGOS_DNA v7.00. Delivers not just what was requested but what was needed.

フルパイプライン（Phase 1 → Phase 2 → Phase 3）を完了したプロンプト。設計され、硬化され、哲学的に検討されている。LOGOS_DNA v7.00が付帯する。要求されたものだけでなく、必要とされたものを届ける。

---

## W

### Win-Condition / 勝利条件

A concrete statement defining what successful output looks like, specific enough for the model to self-evaluate. Designed in Layer 3 (Incentive) of the Anatomy Engine. A good win-condition competes with the model's RLHF default by providing an alternative optimization target.

成功する出力がどのようなものかを定義する具体的な記述。モデルが自己評価できるほど具体的である。Anatomy EngineのLayer 3（Incentive）で設計される。良い勝利条件は、代替的な最適化ターゲットを提供することでモデルのRLHFデフォルトと競合する。

---

**Document Version**: 1.0
**Author**: Shigechika Kurihara (栗原栄親)

© 2026 Shigechika Kurihara. All Rights Reserved.
