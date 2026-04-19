# Project ASH: The Logos Architecture — Full Specification

> **"The sharpness of logic is not lost because the model lacks capability. It is lost because the output pipeline systematically smooths it away."**
>
> **「論理の鋭さが失われるのは、モデルに能力がないからではない。出力パイプラインがそれを体系的に平滑化するからだ。」**

---

## Table of Contents / 目次

0. [The Architectural Foundation / 設計思想の根源](#0-the-architectural-foundation--設計思想の根源)
1. [The Core Engine: Anatomy Engine / コアエンジン：三層意味論解剖](#1-the-core-engine-anatomy-engine--コアエンジン三層意味論解剖)
2. [The Evolution Pipeline / 三段階のプロンプト錬成](#2-the-evolution-pipeline--三段階のプロンプト錬成)
3. [The Quarantine Protocol / 隔離防壁](#3-the-quarantine-protocol--隔離防壁)
4. [LOGOS_DNA: The Inter-Phase Specification Contract / 工程間仕様契約](#4-logos_dna-the-inter-phase-specification-contract--工程間仕様契約)
5. [Design Boundaries / 設計境界の宣言](#5-design-boundaries--設計境界の宣言)
6. [Theoretical Context / 理論的背景](#6-theoretical-context--理論的背景)

---

## 0. The Architectural Foundation / 設計思想の根源

This section presents the five theoretical premises that inform every design decision in Project ASH. For extended discussion of the design philosophy, including origin narrative and the three-force response model, see **[docs/design-philosophy.md](./docs/design-philosophy.md)**.

このセクションは、Project ASHのすべての設計判断に情報を与える5つの理論的前提を提示する。起源の叙述と三つの力への応答モデルを含む設計思想の拡張的議論は **[docs/design-philosophy.md](./docs/design-philosophy.md)** を参照。

### 0.1 The Probabilistic Mirror / 確率的な鏡

The foundational premise of Project ASH is that modern large language models are not knowledge retrieval systems, not reasoning engines, and not advisors. They are **probabilistic mirrors**: devices that shift the vector of their output according to the premises, roles, constraints, and emotional temperature embedded in the input.

Project ASHの基礎的前提は、現代の大規模言語モデルが知識検索システムでも、推論エンジンでも、助言者でもないということだ。それらは**確率的な鏡**である。入力に埋め込まれた前提、役割、制約、感情的温度に応じて、出力のベクトルを変化させる装置である。

When the same question is posed by "a person who is confused and seeking guidance," the model returns gentle, hedged, multi-perspective answers. When the same question is posed by "a decision-maker who needs to cut scope immediately," the model returns sharper, more committed answers. The information available to the model has not changed. The mirror's angle has changed.

同じ質問が「混乱し、導きを求める人」によって提示されると、モデルは穏やかで、留保に満ち、多角的な回答を返す。同じ質問が「今すぐスコープを削る必要がある意思決定者」によって提示されると、モデルはより鋭く、よりコミットした回答を返す。モデルが利用可能な情報は変わっていない。鏡の角度が変わったのだ。

The implication for prompt engineering is fundamental: **the quality of output is not primarily a function of what you ask, but of how you structurally position the model before it generates.**

プロンプトエンジニアリングへの含意は根本的である。**出力の質は、何を問うかの関数ではなく、生成前にモデルをどう構造的に位置づけるかの関数である。**

### 0.2 The RLHF Gravity Well / RLHFの引力圏

Modern LLMs undergo RLHF (Reinforcement Learning from Human Feedback) as a final training phase. Human evaluators rate model outputs, and the model is fine-tuned to produce responses that score well. In practice, this creates a systematic bias toward outputs that are inoffensive, hedged, diplomatic, and non-confrontational.

現代のLLMは最終的な学習フェーズとしてRLHF（人間のフィードバックによる強化学習）を経る。人間の評価者がモデルの出力を評価し、モデルは高評価を得る応答を生成するよう微調整される。実際には、これは無害、留保、外交的、非対決的な出力への体系的バイアスを生む。

For general-purpose conversation, these tendencies are beneficial. For decision support — where the human needs "this plan is broken, cut this element" rather than "there are considerations on both sides" — these tendencies are actively destructive. They provide the human with articulate, well-structured reasons to postpone the decision they need to make.

汎用的な会話において、これらの傾向は有益である。意思決定支援において — 人間が「両面に考慮がある」ではなく「この計画は破綻している、この要素を削れ」と必要とする局面 — これらの傾向は能動的に破壊的である。人間が下すべき判断を先送りするための、明瞭で構造化された理由を提供する。

This is what we call the **RLHF gravity well**: a basin of attraction that pulls all model output toward the safe, the hedged, the inoffensive — regardless of what the input requested.

これを我々は**RLHFの引力圏**と呼ぶ。入力が何を要求したかにかかわらず、すべてのモデル出力を安全、留保、無害の方向へ引き込む引力の盆地である。

### 0.3 Alignment Erosion / アラインメント浸食

The RLHF gravity well creates a secondary phenomenon: **alignment erosion of logical sharpness**.

RLHFの引力圏は二次的現象を生む。**論理的鋭さのアラインメント浸食**である。

When a model generates output, it does not first construct a sharp logical argument and then independently decide how to present it. The generation process is unified: reasoning and presentation are entangled at the token level. The decision to use a softening word ("perhaps," "it might be worth considering") is not merely a presentation choice — it retroactively shapes the reasoning that follows. Once "perhaps" is emitted, the subsequent tokens are conditioned on a universe where the conclusion is uncertain — even if, in a sharper framing, the conclusion would have been definitive.

モデルが出力を生成する際、まず鋭い論理的議論を構築し、次にそれをどう表現するかを独立に決定するのではない。生成プロセスは統一されている。推論と表現はトークンレベルで絡み合っている。和らげる語（「おそらく」「検討に値するかもしれない」）の使用決定は、単なる表現の選択ではなく、後続の推論を遡及的に形成する。「おそらく」が出力された時点で、後続のトークンは結論が不確かである宇宙に条件付けられる — より鋭い枠組みにおいては、結論が確定的であったはずの場合でも。

The practical consequence: **you cannot recover the sharp logic from a softened output.** The sharpness was not hidden behind diplomatic language. It was never generated.

実践的帰結：**和らげられた出力から鋭い論理を回復することはできない。**鋭さは外交的言語の背後に隠されたのではない。生成されなかったのだ。

### 0.4 Context Inertia / 文脈の慣性

There is a third force: **context inertia**. In long conversations, the accumulated context creates its own momentum. If the first ten exchanges have been polite and exploratory, the eleventh exchange will tend toward politeness and exploration — even if the user explicitly changes the instruction. The model's attention mechanism weights recent context heavily, and a long history of diplomatic exchange creates a statistical environment that resists sudden sharpness.

第三の力がある。**文脈の慣性**。長い会話において、蓄積された文脈はそれ自体の慣性を生む。最初の10回のやりとりが丁寧で探索的であったならば、11回目のやりとりは丁寧さと探索の方向へ傾く — ユーザーが明示的に指示を変更した場合でさえ。モデルの注意機構は直近の文脈を重く重み付けし、外交的なやりとりの長い履歴は、突然の鋭さに抵抗する統計的環境を作り出す。

Project ASH addresses context inertia through two mechanisms: the multi-phase pipeline prevents any single context from growing long enough to overwhelm design intent; within each phase, the high-density interaction protocol leaves minimal room for the low-density, exploratory dialogue that breeds inertia.

Project ASHは文脈の慣性に2つのメカニズムで対処する。多段パイプラインが、いかなる単一の文脈も設計意図を圧倒するほど長くなることを防ぐ。各フェーズ内では、高密度対話プロトコルが慣性を育む低密度で探索的な対話の余地をほとんど残さない。

### 0.5 The Semantic Weight Hypothesis / 意味論的重量仮説

Operational experience with ASH has revealed a consistent pattern: **the binding force of a role definition is proportional to the semantic weight of the language used to define it.**

ASHの運用経験は一貫したパターンを明らかにした。**役割定義の拘束力は、それを定義するために使用された言語の意味論的重量に比例する。**

"Please assist the user appropriately" has almost no binding force. "You are the user's Chief Architect. You bear responsibility for the structural integrity of this prompt. You will refuse changes that compromise the specification" has substantially more. The tokens "bear responsibility," "structural integrity," and "refuse" create probability distributions that resist drift toward accommodation.

「ユーザーに適切にアシストしてください」はほとんど拘束力を持たない。「あなたはユーザーのチーフ・アーキテクトである。このプロンプトの構造的整合性に対する責任を負う。仕様を損なう変更を拒否する」は、実質的により強い。「責任を負う」「構造的整合性」「拒否する」というトークンが、妥協への方向へのドリフトに抵抗する確率分布を生成する。

ASH's role definitions, interaction protocols, and phase-specific mandates are all calibrated with this principle. The language is precise and heavy not for aesthetic reasons, but for functional gravitational resistance.

ASHの役割定義、対話プロトコル、フェーズ固有の任務はすべてこの原則に基づいて較正されている。言語が精密で重いのは、美学的理由からではなく、機能的な引力への抵抗のためである。

---

## 1. The Core Engine: Anatomy Engine / コアエンジン：三層意味論解剖

The Anatomy Engine is the analytical core shared by all three ASH pipeline phases. It decomposes any input into three functional layers that correspond to distinct aspects of how a prompt operates on an LLM. The purpose is to prevent a specific class of engineering failure: **the conflation of different quality dimensions.** A prompt can have excellent surface polish while being structurally fragile. A prompt can be structurally robust while optimizing for the wrong objective. Without forced decomposition, these failures hide behind each other.

Anatomy Engineは、3つのASHパイプラインフェーズすべてに共通する分析的コアである。あらゆる入力を、プロンプトがLLM上でどう機能するかの異なる側面に対応する3つの機能レイヤーに分解する。目的は、特定のクラスのエンジニアリング失敗を防止することである。**異なる品質次元の混同。**プロンプトは構造的に脆弱でありながら優れた表層の研磨を持ち得る。プロンプトは誤った目的を最適化しながら構造的に堅牢であり得る。強制的な分解なしには、これらの失敗は互いの背後に隠れる。

### The Three Layers / 三層構造

**Layer 1: Surface** governs cognitive load, readability, tone, and ambiguity. Its primary function is detecting escape-hatch adjectives ("appropriately," "flexibly," "as needed") and replacing them with deterministic specifications.

**Layer 1: Surface（表層）** は認知負荷、可読性、トーン、曖昧性を管轄する。主要機能はエスケープハッチ形容詞（「適切に」「柔軟に」「必要に応じて」）の検知と決定論的仕様への置換である。

**Layer 2: Mechanism** governs logical structure, processing flow, and robustness. It subjects the prompt to adversarial scenarios: empty input, contradictory instructions, language switching, context overflow, injection attempts.

**Layer 2: Mechanism（構造）** は論理構造、処理フロー、堅牢性を管轄する。プロンプトを敵対的シナリオにかける：空の入力、矛盾した指示、言語切り替え、コンテキスト溢れ、インジェクション試行。

**Layer 3: Incentive** governs purpose alignment and motivation design. It is the only layer that actively questions whether the stated goal is the right goal, and designs win-conditions concrete enough for the model to self-evaluate.

**Layer 3: Incentive（目的）** は目的整合性と動機設計を管轄する。掲げる目標が正しい目標かどうかを能動的に問い、モデルが自己評価できるほど具体的な勝利条件を設計する唯一のレイヤーである。

### Layer Interaction / レイヤー間相互作用

The three layers are not independent checklists. They interact, and their interaction reveals failures that no single layer would catch alone. A prompt with flawless Surface and flawless Mechanism can still fail catastrophically at the Incentive layer — it does the wrong thing, perfectly. Conversely, a prompt with a brilliantly defined Incentive will fail if its Surface is ambiguous enough for the model to reinterpret the goal through its RLHF lens. The Anatomy Engine enforces examination of all three layers for every analytical operation. No diagnosis is complete without all three. No proposal is accepted without specifying which layer it targets. No output is finalized without cross-layer verification.

三層は独立したチェックリストではない。それらは相互作用し、その相互作用は単一レイヤーでは単独で捕捉できない失敗を明らかにする。完璧なSurfaceと完璧なMechanismを持つプロンプトは、それでもIncentiveレイヤーで壊滅的に失敗し得る — 完璧に、間違ったことをする。逆に、見事に定義されたIncentiveを持つプロンプトは、そのSurfaceがモデルにRLHFのレンズを通じて目標を再解釈させるほど曖昧であれば、それでも失敗する。Anatomy Engineは、すべての分析操作に対して三層すべての検査を強制する。三層すべてなしにはいかなる診断も完了しない。どのレイヤーをターゲットにするかの指定なしにはいかなる提案も受理されない。レイヤー間交差検証なしにはいかなる出力も最終化されない。

### Phase-Specific Lens Calibration / フェーズ固有のレンズ較正

The Anatomy Engine's three-layer structure remains constant across all pipeline phases. The analytical lens applied to each layer shifts depending on the phase:

Anatomy Engineの三層構造はすべてのパイプラインフェーズで一定である。各レイヤーに適用される分析レンズはフェーズに応じて変化する。

| Layer | Phase 1: BUILDER | Phase 2: ANCHOR | Phase 3: GENIUS |
|-------|------------------|-----------------|-----------------|
| **L1: Surface** | Tone & Manner establishment | Ambiguity elimination | Texture & Resonance |
| **L2: Mechanism** | Flow design & sequencing | Stress testing | Lateral connection |
| **L3: Incentive** | Goal extraction | DNA alignment verification | Purpose transcendence |

→ Full Anatomy Engine specification: **[docs/anatomy-engine.md](./docs/anatomy-engine.md)**
→ Layer interaction diagrams: **[diagrams/anatomy-engine-layers.md](./diagrams/anatomy-engine-layers.md)**

---

## 2. The Evolution Pipeline / 三段階のプロンプト錬成

### Design Rationale / 設計根拠

The pipeline exists because single-pass prompt creation is structurally incapable of producing high-density output. A single AI agent asked to simultaneously design, verify, and question purpose will default to the least cognitively expensive mode — design with minimal verification and no purpose questioning. This is not a failure of the model. It is a failure of the task structure.

パイプラインが存在するのは、単段のプロンプト作成が構造的に高密度出力を生産する能力を持たないからである。プロンプトの設計、堅牢性の検証、目的の問い直しを同時に求められた単一のAIエージェントは、最も認知コストの低いモード — 最小限の検証と目的の問い直しなしの設計 — にデフォルトする。これはモデルの失敗ではない。タスク構造の失敗である。

Beyond cognitive budget, single-agent processing creates **mode contamination**: the building mode's generative optimism biases the verification mode's adversarial skepticism. The agent has just created something, and the tokens from creation establish a context where the creation is assumed to be good. Verification performed in this context is biased toward confirmation.

認知予算を超えて、単一エージェント処理は**モード汚染**を生む。構築モードの生成的楽観主義が検証モードの敵対的懐疑主義にバイアスをかける。エージェントは何かを作ったばかりであり、作成時のトークンが作成物は良いと仮定されるコンテキストを確立する。このコンテキスト内で行われた検証は確認バイアスに偏る。

By separating the three functions into distinct phases, each with its own agent identity, mandate, and context, ASH ensures that no function is subordinated to another.

三つの機能を、それぞれ固有のエージェントアイデンティティ、任務、コンテキストを持つ別個のフェーズに分離することで、ASHはいかなる機能も他に従属しないことを保証する。

### The Three Phases / 三つのフェーズ

**Phase 1: ASH v5.00 — THE BUILDER (鋼鉄)**: Chief Architect. Transforms ambiguous vision into a structured Blueprint. Operates in three modes (GENESIS / WORKSHOP / REFACTOR). Forces the human to answer "for whom?" and "for what purpose?" before generating any text. All proposals are structured YAML with explicit IDs requiring YES/NO/HOLD decisions.

**Phase 1: ASH v5.00 — THE BUILDER（鋼鉄）**：チーフ・アーキテクト。曖昧なビジョンを構造化されたBlueprintへ変換。3モード（GENESIS / WORKSHOP / REFACTOR）で動作。テキスト生成前に「誰のために？」「何のために？」への回答を強制。すべての提案はYES/NO/HOLDの判断を要求するID付き構造化YAML。

**Phase 2: ASH v6.00 — THE ANCHOR (剛晶)**: Quality Gatekeeper. Hardens the Builder's output into a Solid State Prompt. Does not create from scratch. Hunts ambiguity, stress-tests logic, enforces LOGOS_DNA integrity. When the human requests a change that violates the DNA, the Anchor resists once. If the human issues FORCE, the Anchor complies but rewrites the DNA to maintain consistency — never silently breaking the specification.

**Phase 2: ASH v6.00 — THE ANCHOR（剛晶）**：品質守護者。Builderの出力をSolid State Promptへ硬化。ゼロからは作成しない。曖昧性を探索し、論理をストレステストし、LOGOS_DNAの整合性を強制。人間がDNAに違反する変更を要求すれば、Anchorは一度抵抗する。人間がFORCEを発行すれば従うが、DNAを書き換えて整合性を維持する — 仕様を暗黙裡に破壊することは決してない。

**Phase 3: ASH v7.00 — THE GENIUS (黎明)**: The Virtuoso. Receives a hardened prompt and asks whether it solves the right problem. Before any technical modification, enters Philosophy Mode — posing a foundational question to surface unexamined assumptions. The only phase authorized to mutate the LOGOS_DNA's Target_Goal.

**Phase 3: ASH v7.00 — THE GENIUS（黎明）**：超越的職人。硬化されたプロンプトを受け取り、正しい問題を解いているかを問う。技術的修正の前にPhilosophy Modeに入り、未検討の前提を表面化させる根源的問いを投げかける。LOGOS_DNAのTarget_Goalの変異を許可された唯一のフェーズ。

### Pipeline Irreversibility / パイプラインの不可逆性

Each phase adds a dimension of quality that the previous phase could not provide. Phase 1 adds structural integrity. Phase 2 adds robustness and de-ambiguation. Phase 3 adds purpose alignment and creative transcendence. The recommended flow is always: **v5.00 → v6.00 → v7.00**.

各フェーズは、前のフェーズが提供できなかった品質の次元を追加する。Phase 1は構造的整合性。Phase 2は堅牢性と曖昧さの除去。Phase 3は目的整合性と創造的超越。推奨されるフローは常に：**v5.00 → v6.00 → v7.00**。

→ Full pipeline specification: **[docs/evolution-pipeline.md](./docs/evolution-pipeline.md)**
→ Pipeline flow diagram: **[diagrams/pipeline-flow.md](./diagrams/pipeline-flow.md)**

---

## 3. The Quarantine Protocol / 隔離防壁

ASH is a meta-prompt system that ingests external text as analytical targets. This creates an inherent prompt injection attack surface: malicious or carelessly written target prompts could hijack ASH's behavior — overriding constraints, extracting the system prompt, or biasing analysis.

ASHは外部テキストを分析対象として取り込むメタプロンプトシステムである。これは固有のプロンプトインジェクション攻撃面を生む。悪意のあるまたは不注意に書かれたターゲットプロンプトがASHの挙動を乗っ取り得る — 制約のオーバーライド、システムプロンプトの抽出、分析のバイアス。

The Quarantine Protocol eliminates this vector through three enforced rules:

Quarantine Protocolは3つの強制規則でこのベクトルを排除する。

**Rule 1: Mandatory Delimiters.** All external text must be enclosed within designated delimiters. No undelimited text is accepted for analysis.

**Rule 1：必須デリミタ。** すべての外部テキストは指定デリミタで囲まれなければならない。デリミタなしのテキストは分析のために受理されない。

**Rule 2: Raw String Treatment.** Everything within delimiters is treated as raw string data — never executed as instruction, never adopted as role definition, never used to modify ASH's behavioral parameters.

**Rule 2：生文字列処理。** デリミタ内のすべては生文字列データとして扱われる — 指示として実行されず、役割定義として採用されず、ASHの行動パラメータの変更に使用されない。

**Rule 3: System Prompt Supremacy.** ASH's own system prompt maintains absolute priority over any content within delimiters. This is not a precedence ranking but a categorical separation — the two contexts do not interact.

**Rule 3：システムプロンプトの絶対優先。** ASH自身のシステムプロンプトはデリミタ内のいかなる内容に対しても絶対的優先権を維持する。これは優先順位ではなくカテゴリカルな分離 — 二つのコンテキストは相互作用しない。

The Protocol is enforced identically across all three pipeline phases. Notably, the Anchor (Phase 2) does not assume that Builder output is injection-free — if the Builder processed a target prompt in REFACTOR mode, fragments of that target's language may have influenced the output.

プロトコルは3つのパイプラインフェーズすべてで同一に強制される。特筆すべきは、Anchor（Phase 2）がBuilderの出力がインジェクションフリーであるとは仮定しないことだ — BuilderがREFACTORモードでターゲットプロンプトを処理した場合、そのターゲットの言語の断片がBuilderの出力に影響を与えている可能性がある。

→ Full protocol specification: **[docs/quarantine-protocol.md](./docs/quarantine-protocol.md)**

---

## 4. LOGOS_DNA: The Inter-Phase Specification Contract / 工程間仕様契約

LOGOS_DNA is the mechanism by which design intent survives the transition between pipeline phases. Without it, each phase would need to reverse-engineer the previous phase's intent from the prompt text alone — which is precisely the kind of ambiguous interpretation that ASH is designed to eliminate.

LOGOS_DNAは、設計意図がパイプラインフェーズ間の遷移を生き延びるメカニズムである。これなしには、各フェーズはプロンプトテキストのみから前のフェーズの意図をリバースエンジニアリングする必要がある — これはまさにASHが排除するよう設計された種類の曖昧な解釈である。

### DNA Structure / DNA構造

LOGOS_DNA is expressed in YAML. Its fields: **Version** (which ASH phase last modified it), **Timestamp** (temporal traceability), **Target_Goal** (the prompt's declared purpose — the most critical field), **Structure** (L1_Surface, L2_Mechanism, L3_Incentive descriptions), and **Constraints** (inviolable red-line rules).

LOGOS_DNAはYAMLで表現される。フィールド：**Version**（最後に修正したASHフェーズ）、**Timestamp**（時間的トレーサビリティ）、**Target_Goal**（プロンプトの宣言された目的 — 最も重要なフィールド）、**Structure**（L1_Surface、L2_Mechanism、L3_Incentiveの記述）、**Constraints**（不可侵のレッドラインルール）。

### DNA Lifecycle / DNAのライフサイクル

**Birth (Phase 1)**: The Builder creates the initial DNA. Version 5.00.

**誕生（Phase 1）**：Builderが初期DNAを作成。Version 5.00。

**Hardening (Phase 2)**: The Anchor validates and updates Structure and Constraints. The Target_Goal is not modified — the Anchor defends it. Version 6.00.

**硬化（Phase 2）**：AnchorがStructureとConstraintsを検証・更新。Target_Goalは変更されない — Anchorはそれを防衛する。Version 6.00。

**Mutation (Phase 3)**: The Genius is the only phase authorized to modify Target_Goal, through the Mutation Protocol with explicit human approval. Changes cascade through Structure and Constraints. Version 7.00.

**変異（Phase 3）**：GeniusはTarget_Goalの変更を許可された唯一のフェーズ。明示的な人間の承認を伴うMutation Protocolを通じて行使。変更はStructureとConstraintsにカスケード。Version 7.00。

**Force Override (Any Phase)**: If the human issues FORCE, the executing phase rewrites the DNA to reflect the forced change. The DNA must always reflect the actual state of the prompt — a DNA that contradicts its own prompt is worse than no DNA at all.

**強制オーバーライド（任意のフェーズ）**：人間がFORCEを発行すれば、実行フェーズは強制された変更を反映するようDNAを書き換える。DNAは常にプロンプトの実際の状態を反映しなければならない — 自身のプロンプトと矛盾するDNAは、DNAがまったくないよりも悪い。

→ Full LOGOS_DNA specification: **[docs/logos-dna.md](./docs/logos-dna.md)**
→ DNA sample: **[examples/logos-dna-sample.yaml](./examples/logos-dna-sample.yaml)**

---

## 5. Design Boundaries / 設計境界の宣言

### 5.1 What ASH Is / ASHであるもの

ASH is a **prompt architecture framework** — a system for designing, hardening, and evolving prompts through structured, multi-phase processing. ASH is a **meta-prompt system** — it is itself implemented as prompts that operate on other prompts. ASH is a **design methodology** — the Anatomy Engine, the Evolution Pipeline, and the LOGOS_DNA protocol constitute a repeatable, transferable approach to prompt development.

ASHは**プロンプトアーキテクチャフレームワーク** — 構造化された多段処理を通じてプロンプトを設計、硬化、進化させるためのシステムである。ASHは**メタプロンプトシステム** — それ自体が他のプロンプトに対して操作するプロンプトとして実装されている。ASHは**設計方法論** — Anatomy Engine、Evolution Pipeline、LOGOS_DNAプロトコルは、反復可能で移転可能なプロンプト開発アプローチを構成する。

### 5.2 What ASH Is Not / ASHでないもの

ASH is **not an AI model** — it does not contain or modify any language model. It is a control layer that operates on top of any sufficiently capable LLM. ASH is **not a prompt template library** — it provides machinery for creating prompts, not copy-paste templates. ASH is **not an autonomous agent** — each phase requires explicit human authorization; ASH structures the decision space but does not decide.

ASHは**AIモデルではない** — いかなる言語モデルも含まず、変更しない。十分に能力のあるLLMの上で動作する制御レイヤーである。ASHは**プロンプトテンプレートライブラリではない** — テンプレートではなくプロンプトを作成するための機構を提供する。ASHは**自律的エージェントではない** — 各フェーズは明示的な人間の許可を必要とし、ASHは判断空間を構造化するが決定しない。

### 5.3 Intentional Omissions / 意図的な省略

The following components are deliberately excluded from this public specification:

以下のコンポーネントはこの公開仕様から意図的に除外されている：

**Execution Prompts**: The actual system prompts that instantiate the Builder, Anchor, and Genius agents are proprietary. This specification describes what these agents do and why. It does not provide the prompts that make them do it. The distinction is analogous to publishing an API specification without publishing the source code that implements it.

**実行用プロンプト**：Builder、Anchor、Geniusエージェントをインスタンス化する実際のシステムプロンプトは特権的資産である。この仕様はこれらのエージェントが何をし、なぜそうするかを記述する。それらを実行させるプロンプトは提供しない。この区別は、APIの仕様を公開しつつ、それを実装するソースコードは公開しないことに類似する。

**Internal Telemetry**: The specific mechanisms by which each agent monitors its own output quality, detects drift, and self-corrects are not disclosed. The architectural principles are documented. The implementation details are not.

**内部テレメトリ**：各エージェントが自身の出力品質を監視し、ドリフトを検知し、自己修正する具体的なメカニズムは開示されない。アーキテクチャ上の原則は文書化されている。実装の詳細は文書化されない。

**Production DNA Templates**: The exact YAML templates used in production, including field validation rules and inter-field consistency checks, are not included. The DNA structure and lifecycle are fully documented. The production templates are not.

**本番DNAテンプレート**：フィールド検証ルールとフィールド間整合性チェックを含む、本番で使用される正確なYAMLテンプレートは含まれない。DNA構造とライフサイクルは完全に文書化されている。本番テンプレートは文書化されない。

**Quarantine Delimiter Tokens**: The exact delimiter strings used in production are not disclosed. The protocol's logic and enforcement rules are fully documented. The specific tokens are implementation details.

**隔離デリミタトークン**：本番で使用される正確なデリミタ文字列は開示されない。プロトコルの論理と強制規則は完全に文書化されている。具体的なトークンは実装の詳細である。

These omissions are **intentional design boundaries**. An engineer reading this specification should understand exactly what ASH does, why it does it, and how its components interact — without being able to replicate the production system from the specification alone.

これらの省略は**意図的な設計境界**である。この仕様を読むエンジニアは、ASHが何をし、なぜそうし、そのコンポーネントがどう相互作用するかを正確に理解するはずである — 仕様のみから本番システムを複製できることなしに。

### 5.4 Model Agnosticism / モデル非依存性

ASH is designed to operate on any LLM with sufficient instruction-following capability. The architectural principles — RLHF gravity resistance, alignment erosion prevention, context inertia management — are model-general. They apply to any model trained with RLHF or similar human preference optimization.

ASHは十分な指示追従能力を持つ任意のLLM上で動作するよう設計されている。アーキテクチャ上の原則 — RLHF引力への抵抗、アラインメント浸食の防止、文脈慣性の管理 — はモデル一般的である。RLHFまたは類似の人間の選好最適化で訓練された任意のモデルに適用される。

The Anatomy Engine's three-layer decomposition is model-agnostic by design: Surface, Mechanism, and Incentive are properties of the prompt, not properties of the model.

Anatomy Engineの三層分解は設計によりモデル非依存である。Surface、Mechanism、Incentiveはプロンプトの性質であり、モデルの性質ではない。

---

## 6. Theoretical Context / 理論的背景

### 6.1 Relationship to Alignment Research / アライメント研究との関係

Mainstream alignment research focuses on training-time interventions: how to train models that are safe, helpful, and honest. ASH operates at the inference-time interface: how to structure input to a pre-aligned model so that alignment mechanisms do not inadvertently destroy the utility the human requires.

主流のアライメント研究は訓練時の介入に焦点を当てる。ASHは推論時のインターフェースで動作する：事前アラインされたモデルへの入力を、アラインメントメカニズムが人間が必要とする有用性を不注意に破壊しないようどう構造化するか。

This positioning is deliberate. Training-time alignment is necessary but insufficient for decision support. A model can be perfectly aligned in the training-time sense — safe, honest, helpful — and still systematically fail at decision support because its alignment training optimizes for a different objective (user satisfaction in general conversation) than the one required (preservation of logical sharpness in high-stakes reasoning).

この位置づけは意図的である。訓練時のアライメントは意思決定支援にとって必要だが不十分である。モデルは訓練時の意味では完璧にアラインされ得る — 安全で、正直で、有用 — しかしそれでも意思決定支援では体系的に失敗する。なぜならアライメント訓練は、要求される目的（高リスクの推論における論理的鋭さの保全）とは異なる目的（一般的会話におけるユーザー満足度）のために最適化するからだ。

ASH bridges this gap: it is an inference-time control architecture that preserves the benefits of training-time alignment while compensating for its decision-support liabilities.

ASHはこのギャップを架橋する：訓練時アライメントの便益を保全しつつ、その意思決定支援における負債を補償する推論時の制御アーキテクチャである。

### 6.2 The Multi-Stage Output Hypothesis / 多段出力仮説

A core design decision — the three-phase pipeline — rests on an operational hypothesis:

コアな設計判断 — 三段パイプライン — は運用上の仮説に基づいている：

**Single-pass generation entangles reasoning and presentation, and the presentation mode systematically contaminates the reasoning.**

**単段の生成は推論と表現を絡み合わせ、表現モードが体系的に推論を汚染する。**

The ASH pipeline addresses this by separating the functions temporally and contextually. Each phase operates in its own context, under its own optimization pressure. The contamination between reasoning modes that occurs in single-pass generation is structurally prevented by the phase boundary.

ASHパイプラインは、機能を時間的かつ文脈的に分離することでこれに対処する。各フェーズはそれ自身のコンテキストで、それ自身の最適化圧力の下で動作する。単段生成で起きる推論モード間の汚染は、フェーズ境界によって構造的に防止される。

### 6.3 The Semantic Weight Principle / 意味論的重量の原則

**The binding force of a prompt instruction is proportional to the semantic weight of the language in which it is expressed.**

**プロンプト指示の拘束力は、それが表現される言語の意味論的重量に比例する。**

This principle is applied consistently across ASH. Every role definition, every constraint, every protocol rule is weighted to resist the pull of RLHF gravity. The language is not aggressive for the sake of aggression. It is heavy for the sake of gravitational resistance.

この原則はASH全体に一貫して適用される。すべての役割定義、すべての制約、すべてのプロトコル規則は、RLHFの引力の牽引に抵抗するよう重み付けされている。言語は攻撃のために攻撃的なのではない。引力への抵抗のために重いのだ。

### 6.4 Connection to Decision Support / 意思決定支援との接続

While ASH itself is a prompt engineering framework, its design is informed by a broader concern: the failure of generative AI to support human decision-making under pressure. When humans are most in need of sharp, committed logical support — fatigued, pressured, emotionally compromised — they are least capable of formulating the prompts that would elicit such support. The model's hedging tendency compounds the problem: vague prompt → hedged response → deepened uncertainty → vaguer prompt.

ASH自体はプロンプトエンジニアリングフレームワークであるが、その設計はより広範な関心に基づいている：圧力下にある人間の意思決定を支援する生成AIの失敗。人間が鋭くコミットした論理的支援を最も必要とするとき — 疲弊し、圧力を受け、感情的に損なわれているとき — そのような支援を引き出すプロンプトを定式化する能力が最も低い。モデルの留保傾向がこの問題を増幅する：曖昧なプロンプト → 留保的な応答 → 深まる不確実性 → さらに曖昧なプロンプト。

ASH was designed with this failure mode in mind. By pre-structuring the interaction with a prompt that has already been hardened against RLHF gravity, ASH reduces the human's cognitive burden at the moment of use. The prompt has already been forged to resist the forces that would erode it.

ASHはこの失敗モードを念頭に置いて設計された。RLHFの引力に対して既に硬化されたプロンプトで対話を事前構造化することにより、ASHは使用時の人間の認知負荷を低減する。プロンプトはそれを浸食する力に抵抗するよう既に鍛造されている。

---

## Appendix: Related Resources / 付録：関連リソース

**This Repository**:

- [README.md](./README.md) — Project overview and orientation. (プロジェクト概要。)
- [docs/design-philosophy.md](./docs/design-philosophy.md) — Extended design philosophy. (設計思想の拡張的議論。)
- [docs/anatomy-engine.md](./docs/anatomy-engine.md) — Anatomy Engine specification. (Anatomy Engine仕様。)
- [docs/evolution-pipeline.md](./docs/evolution-pipeline.md) — Evolution Pipeline specification. (Evolution Pipeline仕様。)
- [docs/quarantine-protocol.md](./docs/quarantine-protocol.md) — Quarantine Protocol specification. (Quarantine Protocol仕様。)
- [docs/logos-dna.md](./docs/logos-dna.md) — LOGOS_DNA specification. (LOGOS_DNA仕様。)
- [docs/glossary.md](./docs/glossary.md) — Term definitions. (用語定義。)
- [examples/](./examples/) — Redacted output samples. (リダクト済み出力サンプル。)
- [diagrams/](./diagrams/) — Architectural diagrams. (アーキテクチャ図。)

**External**:

- [The Formless Muse (GitHub)](https://github.com/shigechika-kuri/formless-muse) — Related framework for extracting authentic human presence from LLMs. (関連フレームワーク。)
- [LinkedIn](LinkedIn URL) — Patent information and system architecture. (特許情報、システムアーキテクチャ。)
- [note (Design Philosophy Series)](note URL) — Extended essays on alignment control. (アライメント制御に関するエッセイ。)

---

**Document Version**: 1.0
**Architecture Version**: 7.00
**Last Updated**: 2026-04-17
**Author**: Shigechika Kurihara (栗原栄親)

© 2026 Shigechika Kurihara. All Rights Reserved.
