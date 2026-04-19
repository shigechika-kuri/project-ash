# System Overview Diagram / システム全体図

> **This diagram renders natively on GitHub using Mermaid. No external tools required.**
>
> **この図はMermaidを使用してGitHub上でネイティブにレンダリングされる。外部ツール不要。**

---

## Full Architecture / 全体アーキテクチャ

```mermaid
graph TB
    subgraph USER["👤 Human / 人間"]
        U_VISION["Ambiguous Vision<br>曖昧なビジョン"]
        U_DECISION["YES / NO / HOLD<br>Explicit Decisions<br>明示的判断"]
        U_FORCE["FORCE Command<br>強制コマンド"]
    end

    subgraph QUARANTINE["🛡️ Quarantine Protocol / 隔離防壁"]
        Q_DELIMIT["Mandatory Delimiters<br>必須デリミタ"]
        Q_RAW["Raw String Treatment<br>生文字列処理"]
        Q_SUPREME["System Prompt Supremacy<br>システムプロンプト絶対優先"]
    end

    subgraph ENGINE["⚙️ Anatomy Engine / 解剖エンジン"]
        L1["Layer 1: Surface<br>表層 — 認知負荷・曖昧性"]
        L2["Layer 2: Mechanism<br>構造 — 論理・堅牢性"]
        L3["Layer 3: Incentive<br>目的 — 目標・勝利条件"]
        L1 <--> L2
        L2 <--> L3
        L1 <--> L3
    end

    subgraph PIPELINE["🔨 Evolution Pipeline / 錬成パイプライン"]
        V5["Phase 1: ASH v5.00<br>THE BUILDER — 鋼鉄<br>Chief Architect"]
        V6["Phase 2: ASH v6.00<br>THE ANCHOR — 剛晶<br>Quality Gatekeeper"]
        V7["Phase 3: ASH v7.00<br>THE GENIUS — 黎明<br>The Virtuoso"]
    end

    subgraph DNA_SYSTEM["📋 LOGOS_DNA / 設計仕様契約"]
        DNA5["DNA v5.00<br>Blueprint Spec"]
        DNA6["DNA v6.00<br>Hardened Spec"]
        DNA7["DNA v7.00<br>Evolved Spec"]
    end

    subgraph OUTPUT["✅ Output / 成果物"]
        SSP["Solid State Prompt<br>高密度プロンプト"]
    end

    %% Human to Pipeline
    U_VISION --> V5
    U_DECISION --> V5
    U_DECISION --> V6
    U_DECISION --> V7
    U_FORCE -.->|"Override"| V6
    U_FORCE -.->|"Override"| V7

    %% Quarantine applies to all phases
    QUARANTINE -.->|"Enforced at<br>every phase"| V5
    QUARANTINE -.->|"Enforced at<br>every phase"| V6
    QUARANTINE -.->|"Enforced at<br>every phase"| V7

    %% Engine feeds all phases
    ENGINE -.->|"Analytical Core"| V5
    ENGINE -.->|"Analytical Core"| V6
    ENGINE -.->|"Analytical Core"| V7

    %% Pipeline flow with DNA
    V5 -->|"Prompt + DNA v5"| DNA5
    DNA5 -->|"Input to Phase 2"| V6
    V6 -->|"Prompt + DNA v6"| DNA6
    DNA6 -->|"Input to Phase 3"| V7
    V7 -->|"Prompt + DNA v7"| DNA7
    DNA7 --> SSP

    %% Styling
    style USER fill:#2d2d44,stroke:#a0a0c0,color:#fff
    style QUARANTINE fill:#3d1f1f,stroke:#e94560,color:#fff
    style ENGINE fill:#1f2d3d,stroke:#4ecdc4,color:#fff
    style PIPELINE fill:#1a1a2e,stroke:#f5a623,color:#fff
    style DNA_SYSTEM fill:#2d3d1f,stroke:#7bc67e,color:#fff
    style OUTPUT fill:#16213e,stroke:#53d769,color:#fff
```

## Reading Guide / 読み方ガイド

**Human (top)** provides the ambiguous vision and makes all explicit decisions throughout the pipeline. The FORCE command is a special override that compels any phase to comply with a change even when it conflicts with the LOGOS_DNA.

**Human（上部）**は曖昧なビジョンを提供し、パイプライン全体を通じてすべての明示的判断を下す。FORCEコマンドはLOGOS_DNAと矛盾する場合でもいかなるフェーズにも変更への準拠を強制する特別なオーバーライドである。

**Quarantine Protocol (left)** is not a phase. It is a cross-cutting security layer enforced at every pipeline phase. All external text passes through it before analysis.

**Quarantine Protocol（左）**はフェーズではない。すべてのパイプラインフェーズで強制される横断的セキュリティレイヤーである。すべての外部テキストは分析前にこれを通過する。

**Anatomy Engine (left-center)** is not a phase. It is the analytical core shared by all phases. The bidirectional arrows between layers represent cross-layer verification: each layer's findings inform the other two.

**Anatomy Engine（左中央）**はフェーズではない。すべてのフェーズに共有される分析コアである。レイヤー間の双方向矢印はレイヤー間交差検証を表す：各レイヤーの知見が他の二つに情報を提供する。

**Evolution Pipeline (center)** is the sequential processing path. Each phase receives input from the previous phase (accompanied by LOGOS_DNA) and produces output for the next.

**Evolution Pipeline（中央）**は順次的な処理パスである。各フェーズは前のフェーズからの入力（LOGOS_DNAが付帯）を受け取り、次のフェーズのための出力を生む。

**LOGOS_DNA (right-center)** travels with the prompt through every phase, accumulating specification data. v5.00 captures design intent. v6.00 captures hardened state. v7.00 captures evolved purpose.

**LOGOS_DNA（右中央）**はすべてのフェーズを通じてプロンプトと共に移動し、仕様データを蓄積する。v5.00は設計意図を捕捉する。v6.00は硬化状態を捕捉する。v7.00は進化した目的を捕捉する。

**Output (bottom)** is the final Solid State Prompt: high-density, de-ambiguated, purpose-aligned, accompanied by LOGOS_DNA v7.00.

**Output（下部）**は最終的なSolid State Prompt：高密度、曖昧さ除去済み、目的整合、LOGOS_DNA v7.00が付帯。

---

**Document Version**: 1.0
**Author**: Shigechika Kurihara (栗原栄親)

© 2026 Shigechika Kurihara. All Rights Reserved.
