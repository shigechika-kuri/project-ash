# Design Philosophy / 設計思想

> **"The problem is not that AI lacks intelligence. The problem is that AI's safety mechanisms and the human's decision-making needs optimize for different objectives — and nobody told the human."**
>
> **「問題はAIに知性がないことではない。AIの安全機構と人間の意思決定ニーズが異なる目的のために最適化していること — そしてそのことを誰も人間に伝えていないことだ。」**

---

## 1. The Starting Point / 出発点

Project ASH did not begin as an engineering project. It began as a frustration.

Project ASHはエンジニアリングプロジェクトとして始まったのではない。苛立ちとして始まった。

The author's operational experience with generative AI in decision support contexts revealed a recurring pattern: the AI returned polished, well-structured, articulate responses that consistently failed to advance the decision the human needed to make. The responses were not wrong. They were not unhelpful in the general sense. They were simply optimized for a different objective than the one the human brought to the conversation.

著者の意思決定支援における生成AIの運用経験は、繰り返し現れるパターンを明らかにした。AIは研磨され、構造化され、明瞭な応答を返した。しかしそれは一貫して、人間が下すべき判断を前進させることに失敗した。応答は間違っていなかった。一般的な意味で無用でもなかった。単に、人間が会話に持ち込んだ目的とは異なる目的のために最適化されていた。

The human needed: "This plan is broken. Cut element X or it fails."

人間が必要としたのは：「この計画は破綻している。要素Xを削れ、さもなくば失敗する。」

The AI returned: "There are several considerations. On one hand, element X provides value in scenario A. On the other hand, resource constraints suggest careful prioritization. I recommend a balanced approach with stakeholder consultation."

AIが返したのは：「いくつかの考慮がある。一方で、要素Xはシナリオにおいて価値を提供する。他方で、リソース制約は慎重な優先順位付けを示唆する。ステークホルダーとの協議を含むバランスの取れたアプローチを推奨する。」

The human did not receive a wrong answer. The human received an answer optimized for a different question — a question the human did not ask but that the model's training made it prefer to answer.

人間は間違った答えを受け取ったのではない。人間が問わなかったが、モデルの訓練がモデルに答えることを好ませる、別の問いのために最適化された答えを受け取ったのだ。

This observation — that AI alignment and human decision needs can be structurally misaligned — is the origin of everything in Project ASH.

この観察 — AIのアラインメントと人間の意思決定ニーズが構造的に不整合であり得ること — がProject ASHのすべての起源である。

---

## 2. Three Forces That Erode Prompt Effectiveness / プロンプトの有効性を浸食する三つの力

Through iterative operation and analysis, the author identified three distinct forces that work against prompt effectiveness in decision support contexts. These forces are not bugs. They are features of the system — features that serve their intended purpose (safe, pleasant general conversation) while undermining a different purpose (sharp, committed decision support).

反復的な運用と分析を通じて、著者は意思決定支援の文脈でプロンプトの有効性に対して作用する3つの異なる力を識別した。これらの力はバグではない。システムのフィーチャーである — 意図された目的（安全で快適な一般会話）には奉仕しつつ、異なる目的（鋭くコミットした意思決定支援）を損なうフィーチャー。

For the technical definitions of each force — including the token-level mechanics and the probabilistic model — see [ARCHITECTURE.md Section 0](../ARCHITECTURE.md).

各力の技術的定義 — トークンレベルの機構と確率モデルを含む — は [ARCHITECTURE.md セクション0](../ARCHITECTURE.md) を参照。

### 2.1 RLHF Gravity / RLHFの引力

RLHF training creates a basin of attraction toward safe, hedged, inoffensive output. This basin exerts force on every token the model generates. The force is strongest when the model is uncertain — which is precisely when the human most needs committed, directional output.

RLHFの訓練は、安全で留保的で無害な出力への引力の盆地を生む。この盆地はモデルが生成するすべてのトークンに力を及ぼす。力はモデルが不確かなとき — すなわちまさに人間がコミットした方向性のある出力を最も必要とするとき — に最も強い。

The gravitational metaphor is intentional: like physical gravity, RLHF gravity is always present, always pulling in the same direction, and requires active energy expenditure to resist. A prompt that does not actively resist RLHF gravity will, over the course of a conversation, drift toward the basin.

引力のメタファーは意図的である。物理的な引力のように、RLHFの引力は常に存在し、常に同じ方向へ引っ張り、抵抗するには能動的なエネルギー消費を要する。RLHFの引力に能動的に抵抗しないプロンプトは、会話の経過とともに盆地へドリフトする。

### 2.2 Alignment Erosion / アラインメント浸食

Alignment processing does not merely soften the presentation of sharp logic. It prevents sharp logic from being generated in the first place. This is the most counterintuitive and most important insight underlying ASH's design.

アラインメント処理は鋭い論理の表現を和らげるだけではない。鋭い論理がそもそも生成されることを阻止する。これはASHの設計の基盤にある、最も直感に反し、最も重要な洞察である。

The practical consequence is that post-hoc extraction of sharp logic from a softened response is impossible. The sharpness was not stored somewhere and then papered over. It was structurally prevented from existing. This is why "just ask the AI to be more direct" fails as a strategy — the directness was not suppressed at the presentation layer. It was never computed at the reasoning layer.

実践的帰結は、和らげられた応答からの鋭い論理の事後的抽出が不可能だということだ。鋭さはどこかに保存され次に覆い隠されたのではない。存在することが構造的に阻止された。「AIにもっと直接的になれと頼めばいい」が戦略として失敗するのはこのためだ — 直接性は表現レイヤーで抑圧されたのではない。推論レイヤーで計算されなかったのだ。

### 2.3 Context Inertia / 文脈の慣性

Long conversations accumulate statistical momentum. If the first twenty exchanges are polite, exploratory, and accommodating, the twenty-first exchange will tend in the same direction regardless of what the prompt says. Re-stating the system prompt is a common remedy, but it is often insufficient. The system prompt is a fixed declaration; the accumulated context is a dynamic force. The dynamic force tends to win over time.

長い会話は統計的な慣性を蓄積する。最初の20回のやりとりが丁寧で探索的で妥協的であれば、21回目のやりとりはプロンプトが何を言っていようと同じ方向に傾く。システムプロンプトの再提示は一般的な救済策であるが、しばしば不十分である。システムプロンプトは固定された宣言である。蓄積された文脈は動的な力である。動的な力は時間とともに勝つ傾向がある。

---

## 3. The ASH Response / ASHの応答

Project ASH responds to these three forces with three corresponding architectural decisions. Each force has a dedicated countermeasure. This one-to-one correspondence is not accidental — it is the organizing principle of the entire architecture.

Project ASHはこれら3つの力に対し、3つの対応するアーキテクチャ上の判断で応答する。各力に専用の対抗措置がある。この一対一の対応は偶然ではない — アーキテクチャ全体の組織原理である。

**Against RLHF Gravity → Semantic Weight.** ASH's role definitions, mandates, and constraints use language heavy enough to place the model's operational center of gravity outside the RLHF basin of attraction. The language is not aggressive for its own sake. It is gravitationally resistant by design. When ASH defines a role with language such as "treats ambiguous language the way a carpenter treats rotten wood," the tokens create a semantic space where accommodation is not the path of least resistance.

**RLHFの引力に対して → 意味論的重量。** ASHの役割定義、任務、制約は、モデルの運用上の重心をRLHFの引力盆地の外に置くに十分な重さの言語を使用する。言語はそれ自体のために攻撃的なのではない。設計により引力に抵抗する。ASHが「曖昧な言語を大工が腐った木材を扱うように扱う」といった言語で役割を定義するとき、トークンは妥協が最小抵抗の道ではない意味論的空間を生成する。

**Against Alignment Erosion → Multi-Phase Pipeline.** By separating construction, hardening, and transcendence into distinct contexts with distinct agents, ASH prevents the single-pass contamination where diplomatic presentation tokens corrupt reasoning tokens. Each phase operates under its own optimization pressure, in its own context, with its own mandate. THE BUILDER's creative optimism cannot bias THE ANCHOR's adversarial skepticism, because they operate in separate sessions with no shared context.

**アラインメント浸食に対して → 多段パイプライン。** 構築、硬化、超越を固有のエージェントを持つ別個のコンテキストに分離することで、ASHは外交的表現トークンが推論トークンを汚染する単段の汚染を防止する。各フェーズはそれ自身の最適化圧力の下、それ自身のコンテキストで、それ自身の任務のもとで動作する。THE BUILDERの創造的楽観主義はTHE ANCHORの敵対的懐疑主義にバイアスをかけ得ない。なぜなら共有コンテキストのない別個のセッションで動作するからだ。

**Against Context Inertia → High-Density Interaction Protocol.** Every exchange within an ASH session carries structural weight. Proposals are structured YAML with explicit IDs. Decisions require explicit YES/NO. Diagnostic reports follow fixed formats. This leaves minimal room for the low-density, exploratory exchanges that breed inertia. The conversation never drifts into pleasantries because the protocol does not permit pleasantries.

**文脈の慣性に対して → 高密度対話プロトコル。** ASHセッション内のすべてのやりとりは構造的な重みを持つ。提案はIDを持つ構造化YAMLである。判断は明示的なYES/NOを要求する。診断レポートは固定フォーマットに従う。これにより、慣性を育む低密度で探索的なやりとりの余地はほとんど残されない。会話は社交辞令に漂流しない。なぜならプロトコルが社交辞令を許容しないからだ。

---

## 4. The Prompt as Structural Control Interface / 構造的制御インターフェースとしてのプロンプト

The culmination of this philosophy is a redefinition of what a prompt is.

この思想の集大成は、プロンプトとは何かの再定義である。

In conventional usage, a prompt is a request: "Please help me with X." The human asks; the AI answers. The quality of the interaction depends on the quality of the question.

従来の用法では、プロンプトは依頼である。「Xを手伝ってください。」人間が問い、AIが答える。対話の質は問いの質に依存する。

In ASH's framework, a prompt is a **structural control interface**: a pre-engineered artifact that constrains the model's cognitive space, resists alignment erosion, manages context inertia, and ensures that the output optimizes for the human's actual objective rather than the model's trained preference.

ASHのフレームワークにおいて、プロンプトは**構造的制御インターフェース**である。モデルの認知空間を拘束し、アラインメント浸食に抵抗し、文脈の慣性を管理し、出力がモデルの訓練された嗜好ではなく人間の実際の目的のために最適化されることを保証する、事前に工学的に設計された成果物である。

This redefinition is not semantic play. It changes how prompts are created (through engineering, not improvisation), how they are evaluated (against structural criteria, not impressionistic quality), and how they are maintained (through specification continuity, not ad-hoc revision).

この再定義は意味論的な遊びではない。プロンプトがどう作られるか（即興ではなくエンジニアリングを通じて）、どう評価されるか（印象的な品質ではなく構造的基準に対して）、どう維持されるか（アドホックな改訂ではなく仕様の継続性を通じて）を変える。

Project ASH is the system that produces these artifacts.

Project ASHはこれらの成果物を生産するシステムである。

---

**Document Version**: 1.1
**Parent**: [ARCHITECTURE.md](../ARCHITECTURE.md) Section 0
**Author**: Shigechika Kurihara (栗原栄親)

© 2026 Shigechika Kurihara. All Rights Reserved.
