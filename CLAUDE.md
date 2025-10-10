# Claude Code Project Context

## Project Overview
UNSON OS市場調査プレイブック (PB-000) を実行するための専門的なマーケットリサーチプロジェクト。Instagram APIとGemini DeepSearch MCPを活用し、ペルソナ分析から競合分析、ソリューション開発まで一貫したワークフローを提供。

## Project Structure
```
├── .claude/commands/          # カスタムスラッシュコマンド
├── executions/                # 実行履歴とデリバラブル
│   └── YYYYMMDD_HHMMSS_*/    # タイムスタンプ付き実行フォルダ
├── agents/                    # 専門エージェント定義
├── langgraph-deepsearch-mcp/  # Gemini DeepSearch MCP
└── docs/                      # ドキュメント

## Key Technologies
- **Instagram Analysis**: Apify Instagram API (実データ分析)
- **Competitive Research**: Gemini DeepSearch MCP (LangGraph統合)
- **Agents**: 7つの専門エージェント (persona-analyzer, competitive-analyzer, issue-detector, idea-generator, positioning-integrator, quality-assurance, data-manager)

## Critical Workflows

### 1. PB-000 Complete Pipeline
```bash
/pb000-mcp-auto  # フル自動実行（全5フェーズ + QA）
/pb000           # マニュアル実行
```

### 2. Individual Phases
- `/persona` - Phase1: Instagram実データからペルソナ分析
- `/issues` - Phase2: 思い込み・課題検知
- `/ideas` - Phase3: ソリューションアイデア生成
- `/competitive` - Phase4: 競合・市場分析（DeepSearch）
- `/positioning` - Phase5: ポジショニング設計・最終統合

### 3. Quality Gates
```bash
/quality  # 品質保証チェック実行
```

## Agent Usage Patterns

### MUST USE Agents
1. **persona-analyzer**: Instagram分析時は必須（WebFetch + Apify API）
2. **competitive-analyzer**: 競合調査時は必須（DeepSearch MCP）
3. **positioning-integrator**: 最終統合時は必須（全フェーズ統合）
4. **quality-assurance**: 完了確認時は必須（QA Report生成）

### Agent Selection Logic
```
Instagram分析 → persona-analyzer
競合/市場調査 → competitive-analyzer
課題深掘り → issue-detector
アイデア創出 → idea-generator
最終統合 → positioning-integrator
品質確認 → quality-assurance
データ管理 → data-manager
```

## Environment Variables Required
```bash
APIFY_API_TOKEN=<Instagram API用>
GOOGLE_API_KEY=<Gemini DeepSearch用>
```

## File Naming Conventions
- `01_persona_insights.md` - ペルソナ分析結果
- `02_persona_profiles.md` - 詳細ペルソナプロファイル
- `03_issue_analysis.md` - 課題分析
- `04_solution_ideas.md` - ソリューションアイデア
- `05_competitive_analysis.md` - 競合分析
- `06_market_analysis.md` - 市場分析
- `07_positioning_strategy.md` - ポジショニング戦略
- `08_lp_messaging.md` - LP用メッセージング
- `QA_Report.md` - 品質保証レポート

## Best Practices

### DO
- 必ず適切なエージェントを使用（上記MUST USEリスト参照）
- 実行前に`/data-setup`でフォルダセットアップ
- 各フェーズ完了後に`/quality`で品質確認
- Instagram分析では必ず実際の投稿データを使用
- DeepSearchは最新情報取得に活用

### DON'T
- エージェントを使わず直接ツールを呼ばない
- 架空のInstagramデータを使用しない
- MCPツールが利用可能なのにWebSearchを使わない
- QAチェックリストを無視しない
- 実行履歴を`executions/`外に保存しない

## MCP Integration
```bash
# DeepSearch MCP Tools
- mcp__langgraph-deep-search__deep_search    # 徹底調査
- mcp__langgraph-deep-search__quick_search   # クイック検索
```

## Performance Optimization
- 並列実行: 独立したフェーズは並列Agent起動
- キャッシュ活用: DeepSearch結果の再利用
- ファイル管理: Glob/Grepで効率的検索
- エージェント特化: 汎用agentより専門agentを優先

## Quality Criteria
各デリバラブルは以下を満たす必要がある:
- ✅ 実データ/実調査に基づいている
- ✅ 具体的な数値・引用・ソースを含む
- ✅ 抽象論ではなく実践的な提案
- ✅ MVV/課題との整合性がある
- ✅ 差別化要素が明確

## Common Issues & Solutions
| Issue | Solution |
|-------|----------|
| Instagram API失敗 | `APIFY_API_TOKEN`確認、persona-analyzer使用 |
| DeepSearch未使用 | competitive-analyzerで`deep_search`実行 |
| 抽象的な分析 | 実データ要求を明示、QA基準参照 |
| エージェント未使用 | タスク内容に応じた専門エージェント選択 |

## Success Metrics
- 全8ファイル生成完了
- QAレポートで全項目合格
- 実データ/実調査に基づく具体性
- LP用メッセージング完成
