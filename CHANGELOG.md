# Changelog / 変更履歴

All notable changes to Project ASH are documented in this file.

Project ASHへのすべての重要な変更はこのファイルに記録される。

---

## [7.00] — 2026-04-17

### Architecture Release / アーキテクチャリリース

**Status**: Public Architectural Specification — Initial Release.

**ステータス**：公開アーキテクチャ仕様 — 初期リリース。

**What is released / リリースされたもの**:

- Full architectural specification (ARCHITECTURE.md) covering: the probabilistic mirror model, RLHF gravity analysis, alignment erosion theory, context inertia management, and the semantic weight hypothesis. (完全なアーキテクチャ仕様（ARCHITECTURE.md）：確率的な鏡モデル、RLHFの引力分析、アラインメント浸食理論、文脈慣性管理、意味論的重量仮説を網羅。)
- Anatomy Engine specification: three-layer semantic decomposition (Surface, Mechanism, Incentive) with cross-layer verification and phase-specific lens calibration. (Anatomy Engine仕様：レイヤー間交差検証とフェーズ固有レンズ較正を伴う三層意味論解剖（Surface、Mechanism、Incentive）。)
- Evolution Pipeline specification: three-phase prompt forging (v5.00 THE BUILDER, v6.00 THE ANCHOR, v7.00 THE GENIUS) with irreversibility principle and mode contamination prevention. (Evolution Pipeline仕様：不可逆性原則とモード汚染防止を伴う三段階プロンプト鍛造（v5.00 THE BUILDER、v6.00 THE ANCHOR、v7.00 THE GENIUS）。)
- Quarantine Protocol specification: prompt injection defense through mandatory delimiters, raw string treatment, and system prompt supremacy. (Quarantine Protocol仕様：必須デリミタ、生文字列処理、システムプロンプト絶対優先によるプロンプトインジェクション防御。)
- LOGOS_DNA specification: inter-phase specification contract with birth, hardening, mutation, and force override lifecycle. (LOGOS_DNA仕様：誕生、硬化、変異、強制オーバーライドのライフサイクルを持つ工程間仕様契約。)
- Design philosophy documentation. (設計思想ドキュメンテーション。)
- Glossary of terms. (用語集。)
- Redacted output examples: diagnostic report, structured proposal block, LOGOS_DNA sample. (リダクト済み出力例：診断レポート、構造化提案ブロック、LOGOS_DNAサンプル。)
- Architectural diagrams in Mermaid format: system overview, pipeline flow, Anatomy Engine layer structure. (Mermaidフォーマットのアーキテクチャ図：システム全体図、パイプラインフロー、Anatomy Engineレイヤー構造。)

**What is NOT released / リリースされていないもの**:

- Execution prompts (v5.00, v6.00, v7.00 system prompts). (実行用プロンプト（v5.00、v6.00、v7.00システムプロンプト）。)
- Internal telemetry and self-correction logic. (内部テレメトリと自己修正ロジック。)
- Production LOGOS_DNA templates. (本番LOGOS_DNAテンプレート。)
- Quarantine delimiter token specifications. (隔離デリミタトークン仕様。)

These are intentional design boundaries. See [ARCHITECTURE.md Section 5](./ARCHITECTURE.md) for the full boundary declaration.

これらは意図的な設計境界である。完全な境界宣言は[ARCHITECTURE.md セクション5](./ARCHITECTURE.md)参照。

---

## Version History / バージョン履歴

### Internal Development Milestones / 内部開発マイルストーン

The following milestones represent the internal development history of the ASH system. They are documented here for context. The artifacts from these phases are not publicly released.

以下のマイルストーンはASHシステムの内部開発履歴を表す。文脈のためにここに記録される。これらのフェーズからの成果物は公開されない。

**v5.00 — THE BUILDER**: Initial implementation of the Chief Architect agent. Established the Anatomy Engine's three-layer structure, the GENESIS/WORKSHOP/REFACTOR mode system, the structured YAML proposal format, and the LOGOS_DNA birth protocol.

**v5.00 — THE BUILDER**：チーフ・アーキテクトエージェントの初期実装。Anatomy Engineの三層構造、GENESIS/WORKSHOP/REFACTORモードシステム、構造化YAML提案フォーマット、LOGOS_DNA誕生プロトコルを確立。

**v6.00 — THE ANCHOR**: Implementation of the Quality Gatekeeper agent. Added Hardness Score quantification, the Oath Keeper mechanism (DNA defense with FORCE override), ambiguity-specific Layer 1 lens, and stress-test-specific Layer 2 lens.

**v6.00 — THE ANCHOR**：品質守護者エージェントの実装。Hardness Scoreの定量化、誓いの番人メカニズム（FORCEオーバーライドを伴うDNA防衛）、曖昧性特化のLayer 1レンズ、ストレステスト特化のLayer 2レンズを追加。

**v7.00 — THE GENIUS**: Implementation of the Virtuoso agent. Added Philosophy Mode, Mutation Protocol (DNA Target_Goal evolution), lateral connection lens for Layer 2, and purpose transcendence lens for Layer 3.

**v7.00 — THE GENIUS**：超越的職人エージェントの実装。Philosophy Mode、Mutation Protocol（DNA Target_Goal進化）、Layer 2の水平接続レンズ、Layer 3の目的超越レンズを追加。

**Cross-version**: Quarantine Protocol implemented as a cross-cutting concern across all three versions. Bilingual UI (Japanese/English) standardized. NO COMPRESSION principle enforced as a system-wide invariant.

**バージョン横断**：Quarantine Protocolを三つのバージョンすべてにわたる横断的関心事として実装。バイリンガルUI（日本語/英語）を標準化。NO COMPRESSION原則をシステム全体の不変条件として強制。

---

**Document Version**: 1.0
**Author**: Shigechika Kurihara (栗原栄親)

© 2026 Shigechika Kurihara. All Rights Reserved.
