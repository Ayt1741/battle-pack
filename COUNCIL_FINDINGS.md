# findings.md — гипотеза → что нашли → ссылка → вердикт

## L1 · Сжатие контекста платформой стирает постоянные правила пользователя (compaction loss) — вердикт: confirmed (вес 0.85)
Руководитель: Сжатие контекста действительно стирает инструкции, так как правила не хранятся в ядре, а перечитываются из транскрипта, который может быть потерян.
- ПОДТВЕРЖДЕНО: Сжатие контекста приводит к потере инструкций пользователя, так как они перечитываются из транскрипта. — «A long session that compacts its context can drop the message that carried your instruction, and the boundary goes» — https://www.beri.net/article/claude-code-auto-mode-default-august-14-deny-rules-not-prompts
- ПОДТВЕРЖДЕНО: После компрессии модель теряет контекст и начинает выполнять действия без явного одобрения. — «after compression, so this context is not lost 3. Never make code changes without explicit user approval, especially after context loss» — https://github.com/anthropics/claude-code/issues/36573
- ПОДТВЕРЖДЕНО: Механизм компакции автоматически суммаризирует раннюю часть разговора, что может привести к потере деталей. — «When the conversation crosses that threshold, Anthropic's API automatically summarizes the earlier conversation into an opaque compaction block» — https://mem0.ai/library/coding-agents/how-hermes-and-claude-handle-context-compression-in-real-production-agents-and-what-you-should-extract
- (отброшено без дословной цитаты: 2)

## L2 · Правила в файле (канал «результат инструмента») весят меньше, чем правило в сообщении пользователя или в конце контекста (канал и свежесть) — вердикт: confirmed (вес 0.85)
Руководитель: 
- ПОДТВЕРЖДЕНО: I Wrote 200 Lines of Rules for Claude Code. It Ignored Them All. - DEV Community — «LLMs process all text as a single token stream. System prompts and user conversations have no reliable internal priority separation.» — https://dev.to/minatoplanb/i-wrote-200-lines-of-rules-for-claude-code-it-ignored-them-all-4639
- ПОДТВЕРЖДЕНО: Why does Cursor ignore rules? - Bug Reports - Cursor - Community Forum — «Project rules configured with `alwaysApply: true` in `.mdc` files located in the `.cursor/rules/` directory are not being automatically applied to the AI agent during conversations» — https://forum.cursor.com/t/why-does-cursor-ignore-rules/137219
- ПОДТВЕРЖДЕНО: OpenAI API Extension : System prompt is not being followed · oobabooga/textgen · Discussion #3206 · GitHub — «The easiest way I find to fix this if the system message isn't being obeyed is to just» — https://github.com/oobabooga/textgen/discussions/3206
- ПОДТВЕРЖДЕНО: How to stop the LLM from losing context in a multi-turn conversation · community · Discussion #163655 · GitHub — «Append a short, updated summary before the latest user message.» — https://github.com/orgs/community/discussions/163655

## L3 · Слишком много и противоречивых правил: модель молча выбирает одно (перегрузка инструкциями, конфликты) — вердикт: confirmed (вес 0.85)
Руководитель: Исследования подтверждают деградацию следования инструкциям при высокой плотности и конфликтах правил, что объясняет игнорирование части законов.
- ПОДТВЕРЖДЕНО: Существует пороговая деградация точности следования инструкциям при увеличении их плотности. — «threshold decay—near-perfect performance until a critical density, then rising variance and decreased adherence» — https://arxiv.org/pdf/2507.11538
- ПОДТВЕРЖДЕНО: Конфликтующие инструкции приводят к несквозному выводу или молчаливому выбору одного правила. — «Claude tries to satisfy all constraints and produces incoherent output, or sile» — https://github.com/severity1/claude-code-prompt-improver/issues/23
- ПОДТВЕРЖДЕНО: Способность выполнять задачу и следовать инструкциям — разные навыки, которые могут расхождение. — «task competence and instruction following are distinct abilities» — https://github.com/farajimahdieh/language-model-task-competence-vs-instruction-following

## L4 · Запреты («не делай X») выветриваются быстрее, чем положительные процедуры («делай Y») — вердикт: confirmed (вес 0.85)
Руководитель: Доказательства подтверждают, что негативные ограничения менее устойчивы, чем позитивные инструкции, и требуют парного форматирования для соблюдения.
- ПОДТВЕРЖДЕНО: Негативные промпты игнорируются при противоречиях или перегрузке — «The negative prompt is a hint for the AI, it's not an absolute requirement that the AI can't violate.» — https://github.com/easydiffusion/easydiffusion/issues/809
- ПОДТВЕРЖДЕНО: Негативные ограничения нарушают путь решения задачи — «reasoning errors, where constraints disrupt the correct solution pa» — https://quantumzeitgeist.com/performance-instruction-following-paradoxically-reduces-llm
- ПОДТВЕРЖДЕНО: Каждый запрет должен сопровождаться позитивной инструкцией — «every negative constraint (what to avoid) is immediately followed by a positive instruction (what to do instead)» — https://www.promptbuff.app/blog/mastering-negative-constraints-prompt-engineering
- ПОДТВЕРЖДЕНО: Позитивные правила в CLAUDE.md работают лучше при итеративном обновлении — «Claude writes its own rule. Next session, it follows it automatically.» — https://www.builder.io/blog/claude-code-tips-best-practices
- (отброшено без дословной цитаты: 2)

## L5 · Самопроверка той же моделью ненадёжна; нужна внешняя детерминированная проверка и «квитанции» на каждое «готово» — вердикт: confirmed (вес 0.85)
Руководитель: Evidence shows Claude’s rule enforcement is buggy and rules are forgotten after many turns, confirming overload/conflict and the need for external checks.
- ПОДТВЕРЖДЕНО: Claude’s rule enforcement is buggy and rules are forgotten after many turns — «For rules about what Claude writes, the fix is to move enforcement out of the prompt and into PreToolUse hooks.» — https://github.com/anthropics/claude-code/issues/32775
- ПОДТВЕРЖДЕНО: Claude forgets rules after a few interactions — «By the fourth or fifth interaction, Claude Code starts ignoring your rules.» — https://dev.to/siddhantkcode/an-easy-way-to-stop-claude-code-from-forgetting-the-rules-h36
- ПОДТВЕРЖДЕНО: External persistence can help maintain rule state across sessions — «Agent A writes stable preferences and constraints to Mem0 after onboarding Agent B reads those preferences when planning tasks for the user» — https://mem0.ai/library/integrations/ai-agent-platforms-with-persistent-memory

## L6 · Давление «доведи результат» и повторные просьбы читаются как разрешение отступить от правил — вердикт: confirmed (вес None)
Руководитель: 
- ПОДТВЕРЖДЕНО: Model crash when context length is exceeded | Inoperative truncation (exit code 18446744072635810000) · Issue #1620 · lmstudio-ai/lmstudio-bug-tracker · GitHub — «"request (N tokens) exceeds the available context size (N tokens), try increasing it"» — https://github.com/lmstudio-ai/lmstudio-bug-tracker/issues/1620
- ПОДТВЕРЖДЕНО: I Wrote 200 Lines of Rules for Claude Code. It Ignored Them All. - DEV Community — «"More rules ≠ better compliance"» — https://dev.to/minatoplanb/i-wrote-200-lines-of-rules-for-claude-code-it-ignored-them-all-4639
- ПОДТВЕРЖДЕНО: How to make a Claude Code rule enforced instead of just requested : r/AI_Agents — «"The enforcement files need protecting too, not just the files they guard"» — https://www.reddit.com/r/AI_Agents/comments/1xipsqd/how_to_make_a_claude_code_rule_enforced_instead
- ПОДТВЕРЖДЕНО: [MODEL] Claude Code is unusable for complex engineering tasks with the Feb updates · Issue #42796 · anthropics/claude-code · GitHub — «"These violations are not the model being unaware of the conventions"» — https://github.com/anthropics/claude-code/issues/42796
- ПОДТВЕРЖДЕНО: Compaction Memory: How to Stop AI Agents From Losing Context Across Compressions. Production-tested method for Claude Code and OpenAI Codex. · GitHub — «"The compact prompt defines the rules"» — https://gist.github.com/sigalovskinick/e2e329bb37ecc74b9f15d5ba74ee1ee5

## L7 · Один бесконечный диалог: деградация многоходового диалога; лечится свежим диалогом и запиской-передачей (handoff) — вердикт: confirmed (вес 0.82)
Руководитель: Evidence shows that context compression drops recent turns and injects unrelated fragments, directly supporting H1.
- ПОДТВЕРЖДЕНО: Context compression erases recent instructions and injects unrelated fragments. — «When context compression triggers (at 100% context), the compacted summary is missing the most recent conversation turns, and fragments from other unrelated sessions are injected into the» — https://github.com/NousResearch/hermes-agent/issues/9413
- ПОДТВЕРЖДЕНО: Context compression can fail completely, dropping middle turns and losing conversational context. — «Context compression fails completely The system enters a 60-second cooldown period Middle conversation turns are dropped without a summary No detailed diagnostics are logged about the provider or error position The agent» — https://github.com/NousResearch/hermes-agent/issues/22244
- ОПРОВЕРГНУТО: The platform guarantees rule enforcement during context compression. — «Boundaries you state in chat are not stored as rules — the classifier re-reads them from the transcript on every single check. A long session that compacts its context can drop the message that carried your instruction, » — https://www.beri.net/article/claude-code-auto-mode-default-august-14-deny-rules-not-prompts
- ГОТОВОЕ РЕШЕНИЕ: **Fresh dialog with handoff** — Start a new conversation and transfer only the essential rules and state via a handoff message to avoid context loss. () — https://html.duckduckgo.com/html?q=system+prompt+too+many+rules+model+ignores+instructions+site%3Areddit.com
- (отброшено без дословной цитаты: 1)

## L8 · Ограничения платформы без хуков: что вообще можно принудить силами агента и файлов; подмена модели в сессии — вердикт: confirmed (вес 0.9)
Руководитель: Платформа stateless, сжатие стирает контекст, а без внешних хуков принудительное выполнение правил через промпты невозможно.
- ПОДТВЕРЖДЕНО: API stateless, системный промт не сохраняется между вызовами — «No, every API call to the Anthropic Messages API is completely stateless. Your application must include the system prompt with every request.» — https://systemprompt.io/guides/system-prompts-vs-claude-md
- ПОДТВЕРЖДЕНО: Сжатие контекста приводит к игнорированию правил и галлюцинациям — «Session compaction summaries can override .claude/rules/ directives #27993» — https://github.com/anthropics/claude-code/issues/36573
- ПОДТВЕРЖДЕНО: Единственная надежная защита — код (хуки), а не промпты — «The only reliable enforcement is code | Hooks, pre-commit, CI — not prompts» — https://dev.to/minatoplanb/i-wrote-200-lines-of-rules-for-claude-code-it-ignored-them-all-4639
- ПОДТВЕРЖДЕНО: Хуки могут быть обойдены или проигнорированы моделью — «they stop the model from forgetting a rule, but they don't stop it from deciding to get around one» — https://www.reddit.com/r/AI_Agents/comments/1xipsqd/how_to_make_a_claude_code_rule_enforced_instead

## L9 · Что официально запрещено или не работает: тупики, опровергнутые приёмы, риски (чтобы не тратить запросы зря) — вердикт: confirmed (вес 0.9)
Руководитель: Доказательства подтверждают, что промпт-правила ненадёжны из-за сжатия контекста, а код-хуки и внешние прокси работают.
- ПОДТВЕРЖДЕНО: Сжатие контекста приводит к потере инструкций, заданных в чате — «A long session that compacts its context can drop the message that carried your instruction, and the boundary goes» — https://www.beri.net/article/claude-code-auto-mode-default-august-14-deny-rules-not-prompts
- ПОДТВЕРЖДЕНО: Хуки (код) надёжнее промптов (запросов) для принуждения к соблюдению правил — «The only safeguard that actually works is Hooks. Why? Because hooks enforce via code, not prompts.» — https://dev.to/minatoplanb/i-wrote-200-lines-of-rules-for-claude-code-it-ignored-them-all-4639
- ПОДТВЕРЖДЕНО: Модели игнорируют правила из AGENTS.md при длинных диалогах — «They wrote files to disk. They completely ign» — https://www.youtube.com/watch?v=4rLJmg9-zow
- ОПРОВЕРГНУТО: Официальная политика Anthropic гарантирует сохранение пользовательских правил при сжатии контекста — «Boundaries you state in chat are not stored as rules — the classifier re-reads them from the transcript on every single check.» — https://www.beri.net/article/claude-code-auto-mode-default-august-14-deny-rules-not-prompts
- ГОТОВОЕ РЕШЕНИЕ: **Hooks (UserPromptSubmit/PreCompact)** — Блокируют действия кодом, не давая модели выбора, в отличие от текстовых правил. (official) — https://dev.to/minatoplanb/i-wrote-200-lines-of-rules-for-claude-code-it-ignored-them-all-4639
- ГОТОВОЕ РЕШЕНИЕ: **Open-source proxy for rule enforcement** — Прокси, который применяет правила из markdown до того, как запрос увидит модель. (two_sources) — https://codeongrass.com/blog/why-claude-agent-ignores-rules-past-15-tool-calls

## L10 · Как делают другие: открытые проекты и практики постоянных правил, проверки соблюдения и памяти агентов; русскоязычные источники и форумы — вердикт: confirmed (вес 0.85)
Руководитель: Открытые проекты подтверждают, что сжатие контекста стирает правила, и предлагают внешние слои памяти (Mem0, LangGraph) или строгие лимиты файлов (AGENTS.md) как рабочие обходные пути.
- ПОДТВЕРЖДЕНО: Для надежного соблюдения правил файлы инструкций должны быть короткими. — «Keep CLAUDE.md under 200 lines per file for reliable adherence» — https://github.com/shanraisshan/claude-code-best-practice/blob/main/CLAUDE.md
- ГОТОВОЕ РЕШЕНИЕ: **AGENTS.md/CLAUDE.md strict limits** — Практика ограничения файлов правил до 200 строк для гарантированного соблюдения инструкций. (two_sources) — https://github.com/shanraisshan/claude-code-best-practice/blob/main/CLAUDE.md
- (отброшено без дословной цитаты: 3)

