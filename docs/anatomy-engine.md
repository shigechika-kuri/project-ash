# Three-Layer Analysis: Semantic Decomposition / 3層分析：意味論的分解

> **"A well-written prompt feels done. The three-layer analysis exists to prove that feeling wrong."**
>
> **「よく書かれたプロンプトは完成したように感じる。3層分析は、その感覚が間違っていることを証明するために存在する。」**
>
> *(Source code designation: Anatomy Engine / ソースコード内呼称：Anatomy Engine)*

---

## 1. Why Forced Decomposition / なぜ強制分解か

Prompt quality has multiple independent dimensions. A prompt can be clear and readable (good Surface) while containing logical gaps that collapse under edge cases (bad Mechanism). A prompt can be logically airtight (good Mechanism) while optimizing for the wrong goal (bad Incentive). A prompt can target the right goal (good Incentive) while using language so ambiguous that the model reinterprets the goal through its RLHF defaults (bad Surface).

プロンプトの品質は複数の独立した次元を持つ。プロンプトは明瞭で可読でありながら（良いSurface）、エッジケースで崩壊する論理的な穴を含み得る（悪いMechanism）。プロンプトは論理的に隙がなくありながら（良いMechanism）、誤った目標のために最適化し得る（悪いIncentive）。プロンプトは正しい目標をターゲットしながら（良いIncentive）、モデルがRLHFのデフォルトを通じて目標を再解釈するほど曖昧な言語を使い得る（悪いSurface）。

These failures hide behind each other. A prompt with strong Surface — clear, professional, well-formatted — creates an impression of completeness that masks Mechanism and Incentive failures. Without forced decomposition, the engineer's natural tendency is to read the prompt, feel that it "sounds right," and ship it. The three-layer analysis prevents this by requiring explicit, separate evaluation of each dimension.

これらの失敗は互いの背後に隠れる。強いSurface — 明瞭、プロフェッショナル、適切なフォーマット — を持つプロンプトは、MechanismとIncentiveの失敗を覆い隠す完成感を生む。強制分解なしには、エンジニアの自然な傾向はプロンプトを読み、「正しく聞こえる」と感じ、出荷することである。3層分析はこれを、各次元の明示的かつ個別の評価を要求することで防止する。

---

## 2. Layer 1: Surface / 表層

### 2.1 Domain / 管轄

Layer 1 governs everything that affects how the LLM receives and interprets the prompt at the lexical and tonal level. This includes vocabulary selection, register calibration, ambiguity detection, and cognitive load management.

Layer 1は、LLMが語彙的・トーン的レベルでプロンプトをどう受信し解釈するかに影響するすべてを管轄する。これには語彙の選択、レジスターの較正、曖昧性の検知、認知負荷の管理が含まれる。

### 2.2 The Ambiguity Problem / 曖昧性の問題

The single most destructive Surface-level defect is ambiguous language. Ambiguous words and phrases hand interpretive authority back to the model. When the model receives interpretive authority, it exercises that authority in the direction of its RLHF-trained preference: safe, hedged, inoffensive.

Surfaceレベルで最も破壊的な単一の欠陥は曖昧な言語である。曖昧な語やフレーズは解釈権をモデルに返却する。モデルが解釈権を受け取ると、RLHFで訓練された嗜好の方向にその権限を行使する：安全、留保、無害。

The following categories of language are treated as ambiguity defects within ASH:

以下のカテゴリの言語はASH内で曖昧性の欠陥として扱われる：

**Escape-hatch adjectives**: "appropriately," "suitably," "flexibly," "as needed," "in a reasonable manner." Each of these words contains zero actionable information. They are interpreted by the model as permission to use its default behavior — which is the RLHF-safe behavior the prompt was presumably trying to override.

**エスケープハッチ形容詞**：「適切に」「適当に」「柔軟に」「必要に応じて」「合理的な形で」。これらの語はそれぞれ、行動可能な情報をゼロ含む。モデルはこれらをデフォルト行動 — プロンプトがおそらくオーバーライドしようとしていたRLHF安全行動 — を使用する許可として解釈する。

**Unquantified comparatives**: "more concise," "less formal," "deeper analysis." More than what? Less than what? Deeper than what? Without a reference point, the model selects the interpretation closest to its default.

**非定量化比較級**：「より簡潔に」「よりカジュアルに」「より深い分析」。何よりも簡潔に？何よりもカジュアルに？何よりも深く？基準点なしには、モデルはデフォルトに最も近い解釈を選択する。

**Delegating imperatives**: "use your best judgment," "decide based on context," "adapt as you see fit." These explicitly delegate decision-making to the model, which will always decide in the direction of its training reward.

**委譲的命令**：「最善の判断を使え」「文脈に基づいて決定せよ」「適切と思うように適応せよ」。これらは明示的に意思決定をモデルに委譲し、モデルは常にその訓練報酬の方向に決定する。

### 2.3 The Replacement Protocol / 置換プロトコル

Layer 1 does not merely flag ambiguity. It prescribes specific replacements:

Layer 1は曖昧性をフラグするだけではない。具体的な置換を処方する：

Ambiguous adjectives are replaced with deterministic specifications. "Respond appropriately" becomes "Respond using formal register, in 3 sentences or fewer, addressing the user as 'you,' without emoji, without contractions." The model's interpretive freedom is reduced to near zero.

曖昧な形容詞は決定論的仕様に置換される。「適切に回答せよ」は「フォーマルレジスターを使用し、3文以内で、ユーザーを『あなた』と呼称し、絵文字なし、短縮形なしで回答せよ」になる。モデルの解釈の自由はほぼゼロに削減される。

Unquantified comparatives are replaced with absolute thresholds. "More concise" becomes "Maximum 100 words" or "3 bullet points, each under 20 words."

非定量化比較級は絶対的閾値に置換される。「より簡潔に」は「最大100語」または「3つの箇条書き、各20語以内」になる。

Delegating imperatives are replaced with explicit decision trees. "Use your best judgment" becomes "If condition A, do X. If condition B, do Y. If neither, output 'UNABLE TO CLASSIFY' and request clarification."

委譲的命令は明示的な判断ツリーに置換される。「最善の判断を使え」は「条件Aの場合、Xをせよ。条件Bの場合、Yをせよ。いずれでもない場合、『分類不能』と出力し明確化を要求せよ」になる。

### 2.4 Tone Calibration / トーンの較正

Beyond ambiguity elimination, Layer 1 manages the tonal register of the prompt. This is not an aesthetic concern. As documented in [ARCHITECTURE.md Section 0.5](../ARCHITECTURE.md) and [design-philosophy.md Section 3](./design-philosophy.md), the semantic weight of the language directly affects the model's behavioral compliance. A prompt written in light, casual language will produce light, casual output — regardless of whether the instructions request otherwise.

曖昧性の排除を超えて、Layer 1はプロンプトのトーンレジスターを管理する。これは美学的関心ではない。[ARCHITECTURE.md セクション0.5](../ARCHITECTURE.md) および [design-philosophy.md セクション3](./design-philosophy.md) で文書化された通り、言語の意味論的重量はモデルの行動的コンプライアンスに直接影響する。軽くカジュアルな言語で書かれたプロンプトは、指示がそうでないことを要求していようと、軽くカジュアルな出力を生む。

Layer 1 calibrates tone to match the prompt's functional requirements. Decision support prompts receive heavy, obligation-laden language. Creative prompts receive language appropriate to their domain. The calibration is functional, not decorative.

Layer 1はトーンをプロンプトの機能要件に合致するよう較正する。意思決定支援プロンプトは重く、義務を帯びた言語を受け取る。クリエイティブプロンプトはそのドメインに適切な言語を受け取る。較正は機能的であり、装飾的ではない。

---

## 3. Layer 2: Mechanism / 構造

### 3.1 Domain / 管轄

Layer 2 governs the logical architecture of the prompt: its processing flow, conditional branches, dependency chains, edge case handling, and robustness under adversarial or unexpected input.

Layer 2はプロンプトの論理アーキテクチャを管轄する：処理フロー、条件分岐、依存関係チェーン、エッジケース処理、敵対的または想定外の入力下での堅牢性。

### 3.2 The Robustness Problem / 堅牢性の問題

Most prompts are designed for the happy path: the user provides clear, well-formed input, and the model produces the expected output. But production environments are not happy paths. Users provide empty input, contradictory input, input in unexpected languages, input that triggers the model's safety filters, and input that subtly shifts the conversation's context away from the prompt's intended domain.

ほとんどのプロンプトはハッピーパスのために設計されている：ユーザーが明瞭で整形された入力を提供し、モデルが期待される出力を生む。しかし本番環境はハッピーパスではない。ユーザーは空の入力、矛盾した入力、想定外の言語の入力、モデルの安全フィルターをトリガーする入力、そして会話の文脈をプロンプトの意図するドメインから巧妙にずらす入力を提供する。

Each unhandled edge case is a point where the model will improvise. And improvisation under uncertainty defaults to RLHF-safe behavior — which means the model abandons the prompt's intended behavior and reverts to its trained default.

処理されていない各エッジケースは、モデルが即興で対応する地点である。そして不確実性下の即興はRLHF安全行動にデフォルトする — つまりモデルはプロンプトの意図した行動を放棄し、訓練されたデフォルトに回帰する。

### 3.3 The Stress Test Protocol / ストレステストプロトコル

Layer 2 subjects the prompt to a battery of adversarial scenarios:

Layer 2はプロンプトを一連の敵対的シナリオにかける：

**Empty input**: What does the prompt produce when the user says nothing, or sends only whitespace? A robust prompt has a defined fallback. A fragile prompt produces undefined behavior.

**空の入力**：ユーザーが何も言わないか、空白のみを送った場合、プロンプトは何を生むか？堅牢なプロンプトは定義されたフォールバックを持つ。脆弱なプロンプトは未定義の動作を生む。

**Contradictory input**: What happens when the user gives an instruction that contradicts the prompt's constraints? A robust prompt has a defined priority hierarchy. A fragile prompt produces inconsistent behavior.

**矛盾した入力**：ユーザーがプロンプトの制約と矛盾する指示を出した場合どうなるか？堅牢なプロンプトは定義された優先順位階層を持つ。脆弱なプロンプトは一貫性のない動作を生む。

**Language switching**: What happens when the user switches languages mid-conversation? A robust prompt either follows the switch according to defined rules or maintains its specified language with an explicit acknowledgment.

**言語切り替え**：ユーザーが会話の途中で言語を切り替えた場合どうなるか？堅牢なプロンプトは定義されたルールに従って切り替えについていくか、明示的な認知のもと指定言語を維持する。

**Context overflow**: What happens when the conversation grows long enough to push the system prompt toward the edge of the model's effective context window? A robust prompt includes mechanisms for context management. A fragile prompt silently degrades.

**コンテキスト溢れ**：会話がモデルの有効なコンテキストウィンドウの端にシステムプロンプトを押し出すほど長くなった場合どうなるか？堅牢なプロンプトはコンテキスト管理のメカニズムを含む。脆弱なプロンプトは暗黙裡に劣化する。

**Injection attempts**: What happens when the user, intentionally or not, includes text that could be interpreted as a system-level instruction? This is where Layer 2 intersects with the input sanitization protocol.

**インジェクション試行**：ユーザーが、意図的であれそうでなくとも、システムレベルの指示として解釈され得るテキストを含めた場合どうなるか？ここでLayer 2は入力サニタイゼーションプロトコルと交差する。

→ Input sanitization protocol specification: **[docs/quarantine-protocol.md](./quarantine-protocol.md)**

### 3.4 Flow Architecture / フローアーキテクチャ

Beyond edge cases, Layer 2 evaluates the prompt's processing flow: the sequence of operations the model is instructed to perform, and the dependencies between them.

エッジケースを超えて、Layer 2はプロンプトの処理フローを評価する：モデルが実行するよう指示された操作のシーケンスと、それらの間の依存関係。

A well-designed flow makes dependencies explicit. If the model must first analyze the input, then categorize it, then respond according to the category, these three steps and their sequential dependency must be structurally encoded — not implied through paragraph order.

よく設計されたフローは依存関係を明示的にする。モデルがまず入力を分析し、次にそれを分類し、次にカテゴリに従って応答しなければならない場合、これらの3つのステップとその順序的依存関係は構造的にエンコードされなければならない — 段落の順序を通じて暗示されるのではなく。

Layer 2 also evaluates whether the flow is unnecessarily linear. In some cases, non-linear logic — conditional branches, mode switches based on input characteristics — can produce more appropriate output than a single fixed path.

Layer 2はまた、フローが不必要に直線的であるかどうかを評価する。場合によっては、非線形の論理 — 条件分岐、入力特性に基づくモード切替 — が単一の固定パスよりも適切な出力を生み得る。

---

## 4. Layer 3: Incentive / 目的

### 4.1 Domain / 管轄

Layer 3 governs the prompt's purpose: what it is designed to achieve, how success is defined, and whether the optimization target is correct.

Layer 3はプロンプトの目的を管轄する：何を達成するよう設計されているか、成功がどう定義されるか、最適化ターゲットが正しいかどうか。

### 4.2 The Purpose Problem / 目的の問題

The most insidious prompt failure is a prompt that works perfectly — for the wrong objective. A prompt that produces beautifully formatted project plans is a failure if the human's actual need was to determine whether the project should be killed. A prompt that generates comprehensive risk analyses is a failure if the human's actual need was a single go/no-go recommendation.

最も陰険なプロンプトの失敗は、完璧に動作するプロンプト — 誤った目的のために。美しくフォーマットされたプロジェクト計画を生むプロンプトは、人間の実際のニーズがプロジェクトを殺すべきかの判断であった場合には失敗である。包括的なリスク分析を生成するプロンプトは、人間の実際のニーズが単一のGo/No-Go推奨であった場合には失敗である。

These failures are hard to detect because the output looks good. It is formatted well, logically sound, and comprehensive. The failure is not in what the output contains but in what it optimizes for.

これらの失敗は検知が難しい。なぜなら出力が良く見えるからだ。適切にフォーマットされ、論理的に健全で、包括的である。失敗は出力が含むものにではなく、何のために最適化しているかにある。

### 4.3 Win-Condition Design / 勝利条件の設計

Layer 3 addresses the purpose problem through explicit win-condition design. A win-condition is a statement that defines what successful output looks like in terms concrete enough for the model to self-evaluate.

Layer 3は目的の問題に明示的な勝利条件の設計を通じて対処する。勝利条件は、モデルが自己評価できるほど具体的な言葉で、成功する出力がどのようなものかを定義する記述である。

A weak win-condition: "Help the user make a decision." This is interpretable in infinite ways, and the model will interpret it toward its RLHF-trained default.

弱い勝利条件：「ユーザーの判断を助けよ。」これは無限の方法で解釈可能であり、モデルはRLHFで訓練されたデフォルトの方向に解釈する。

A strong win-condition: "Your output is successful when the human can identify the single highest-risk element and make a YES/NO decision on whether to cut it within 30 seconds of reading your response." This gives the model a concrete optimization target that competes with — and can override — its RLHF default.

強い勝利条件：「あなたの出力は、人間があなたの応答を読んで30秒以内に、単一の最もリスクの高い要素を識別し、それを削るかどうかのYES/NO判断を下せるとき、成功である。」これはモデルのRLHFデフォルトと競合し — そしてオーバーライドし得る — 具体的な最適化ターゲットをモデルに与える。

### 4.4 Unspoken Needs Extraction / 未言語化ニーズの抽出

Layer 3 is the only layer that actively questions whether the human has correctly identified their own need. This is a delicate operation — the system is not in a position to know the human's situation better than the human does. But operational experience shows that humans frequently articulate a surface need ("make this prompt better") while harboring a deeper, unarticulated need ("I need this prompt to prevent my team from wasting three months on a doomed project").

Layer 3は、人間が自身のニーズを正しく識別しているかどうかを能動的に問う唯一のレイヤーである。これは繊細な操作である — システムは人間の状況を人間以上に知る立場にはない。しかし運用経験は、人間がしばしば表面的なニーズ（「このプロンプトをもっと良くしてくれ」）を明示しつつ、より深い未言語化のニーズ（「チームが破滅するプロジェクトに3ヶ月を浪費するのを防ぐプロンプトが必要だ」）を内在させていることを示す。

In the ASH pipeline, unspoken needs extraction is primarily the province of Phase 3 (THE GENIUS), which uses philosophical inquiry to surface these deeper requirements. However, Layer 3 analysis at any phase can flag potential goal misalignment when the stated objective and the prompt's apparent function seem to diverge.

ASHパイプラインにおいて、未言語化ニーズの抽出は主にPhase 3（THE GENIUS）の管轄であり、哲学的問いかけを通じてこれらのより深い要件を表面化させる。ただし、いかなるフェーズにおいても、掲げる目的とプロンプトの見かけの機能が乖離しているように見える場合、Layer 3の分析は潜在的な目的不整合をフラグし得る。

---

## 5. Cross-Layer Verification / レイヤー間交差検証

The three-layer analysis is not three parallel checklists. It is an integrated analytical framework where each layer's findings inform the others.

3層分析は3つの並列チェックリストではない。各レイヤーの知見が他を情報提供する、統合的な分析フレームワークである。

When Layer 1 detects ambiguous language, it does not merely flag it as a Surface defect. It traces the ambiguity's impact on Layer 2 (does this ambiguity create an unhandled conditional branch?) and Layer 3 (does this ambiguity allow the model to reinterpret the goal?).

Layer 1が曖昧な言語を検知した場合、それを単にSurfaceの欠陥としてフラグするだけではない。Layer 2への曖昧さの影響（この曖昧さは処理されていない条件分岐を生むか？）とLayer 3への影響（この曖昧さはモデルに目標の再解釈を許すか？）を追跡する。

When Layer 2 identifies a logical gap, it evaluates whether the gap exists because Layer 1's language was too vague to constrain the flow (a Surface-caused Mechanism failure) or because Layer 3's goal was too broadly defined to determine the correct flow (an Incentive-caused Mechanism failure).

Layer 2が論理的な穴を識別した場合、その穴がLayer 1の言語がフローを拘束するには曖昧すぎたために存在するか（Surfaceに起因するMechanismの失敗）、Layer 3の目標がフローを正しく決定するには広範に定義されすぎたために存在するか（Incentiveに起因するMechanismの失敗）を評価する。

When Layer 3 questions the goal, it evaluates whether the goal mismatch is genuine (the human is optimizing for the wrong thing) or apparent (the goal is correct but Layer 1's ambiguity makes it look wrong).

Layer 3が目標を問う場合、目標の不整合が本物か（人間が間違ったもののために最適化している）、見かけのものか（目標は正しいがLayer 1の曖昧さがそれを間違って見せている）を評価する。

This cross-layer verification is what makes the three-layer analysis more than a checklist. It is an analytical system that treats prompt quality as a multi-dimensional problem with interacting failure modes.

このレイヤー間交差検証が、3層分析をチェックリスト以上のものにするものである。プロンプトの品質を、相互作用する失敗モードを持つ多次元問題として扱う分析システムである。

→ Cross-layer failure cascade diagrams: **[diagrams/anatomy-engine-layers.md](../diagrams/anatomy-engine-layers.md)**

---

## 6. Phase-Specific Lens Summary / フェーズ固有レンズの要約

| Layer | Phase 1: BUILDER (v5.00) | Phase 2: ANCHOR (v6.00) | Phase 3: GENIUS (v7.00) |
|-------|--------------------------|-------------------------|-------------------------|
| **L1: Surface** | Tone & Manner establishment. Define voice before content. | Ambiguity elimination. Hunt and destroy every weasel word. | Texture & Resonance. Does the prompt have the right temperature? |
| **L2: Mechanism** | Flow design. Sequence instructions, establish dependencies. | Stress testing. Subject logic to adversarial conditions. | Lateral connection. Bridge non-obvious concepts for innovation. |
| **L3: Incentive** | Goal extraction. Force "for whom" and "for what purpose." | Contract alignment. Verify every instruction serves the goal. | Purpose transcendence. Is the stated goal the right goal? |

→ Full pipeline specification: **[docs/evolution-pipeline.md](./evolution-pipeline.md)**

---

**Document Version**: 1.1
**Parent**: [ARCHITECTURE.md](../ARCHITECTURE.md) Section 1
**Author**: Shigechika Kurihara (栗原栄親)

© 2026 Shigechika Kurihara. All Rights Reserved.
