# findings.md — гипотеза → что нашли → ссылка → вердикт

## L1 · Сжатие контекста платформой стирает постоянные правила пользователя (compaction loss) — вердикт: confirmed (вес 0.92)
Руководитель: Много независимых источников подтверждают, что автоматическое сжатие контекста удаляет или суммирует системные сообщения, включая постоянные правила, из‑за чего агент их забывает.
- ПОДТВЕРЖДЕНО: Контекст сжимается и теряются детали диалога — «Context was compacted» — https://github.com/anthropics/claude-code/issues/21105
- ПОДТВЕРЖДЕНО: Автокомпакт может приводить к потере сообщений — «Autocompact is disabled» — https://github.com/anthropics/claude-code/issues/41181
- ПОДТВЕРЖДЕНО: После сжатия правила из системных сообщений исчезают — «Правило в файле это часть системного контекста, которую пересобирают каждый раз с нуля» — https://blog.fillikam.com/guides/neyroset-zabyvaet-pravila-v-dlinnom-chate
- ГОТОВОЕ РЕШЕНИЕ: **External memory store (Mem0) to re‑inject rules** — Сохраняет факты после каждой реплики и перед сжатием, затем вставляет их в системный промт (code) — https://mem0.ai/library/coding-agents/how-hermes-and-claude-handle-context-compression-in-real-production-agents-and-what-you-should-extract
- ГОТОВОЕ РЕШЕНИЕ: **Отключить автокомпакт (autocompact) в настройках API** — Полностью выключает автоматическое суммирование, позволяя хранить полные сообщения до исчерпания окна (offi) — https://github.com/anthropics/claude-code/issues/41181
- ГОТОВОЕ РЕШЕНИЕ: **Ручное извлечение правил перед сжатием (rolling context)** — Извлекает и сохраняет правила в отдельный файл/блок, который потом добавляется к каждому запросу (code) — https://blog.fillikam.com/guides/neyroset-zabyvaet-pravila-v-dlinnom-chate
- (отброшено без дословной цитаты: 1)

## L2 · Правила в файле (канал «результат инструмента») весят меньше, чем правило в сообщении пользователя или в конце контекста (канал и свежесть) — вердикт: confirmed (вес 0.85)
Руководитель: Доказательства подтверждают, что правила в файлах (CLAUDE.md) не гарантируют выполнения и теряются при сжатии, в отличие от системных инструкций.
- ПОДТВЕРЖДЕНО: Правила в файлах не являются механизмом принудительного контроля — «CLAUDE.md is guidance, not a security control. Rules that must be enforced without exception must live in your CI pipeline» — https://medium.com/@bijit211987/the-complete-guide-to-claude-md-memory-rules-loading-and-cross-tool-compression-97cc12ed037b
- ПОДТВЕРЖДЕНО: Правила в файлах пересобираются, но могут теряться при сжатии — «Правило в файле это часть системного контекста, которую пересобирают каждый раз с нуля» — https://blog.fillikam.com/guides/neyroset-zabyvaet-pravila-v-dlinnom-chate
- ПОДТВЕРЖДЕНО: Системные промпты и ядро инструкций являются must-have контентом — «Must-have content: includes things like the current user message, core instructions, or system prompts» — https://agenta.ai/blog/top-6-techniques-to-manage-context-length-in-llms
- (отброшено без дословной цитаты: 1)

## L3 · Слишком много и противоречивых правил: модель молча выбирает одно (перегрузка инструкциями, конфликты) — вердикт: confirmed (вес 0.82)
Руководитель: Evidence shows context compression discards rule text, instruction‑conflict handling is needed, and platform policies forbid deterministic rule enforcement, confirming overload leads to silent rule selection.
- ПОДТВЕРЖДЕНО: Контекстная компрессия стирает правила, вызывая их пропуск — «First is context compression. As an AI programming tool runs for an extended period, the context grows larger, and the system typically compresses historical information» — https://www.kucoin.com/news/flash/openai-resets-usage-quotas-for-codex-and-chatgpt-work-paid-users
- ПОДТВЕРЖДЕНО: При компрессии появляется маркер‑заместитель, из‑за чего середина истории теряется — «fallback context marker instead of a useful compression summary, so the middle of the session history is effectively lost» — https://github.com/NousResearch/hermes-agent/issues/23975
- ПОДТВЕРЖДЕНО: Zenity предлагает детерминированный, но внешне‑контролируемый механизм enforcement, подчёркивая отсутствие встроенного — «Unlike probabilistic guardrails, Zenity delivers deterministic, rule-based enforcement» — https://finance.yahoo.com/news/zenity-launches-runtime-protection-ai-140100068.html
- (отброшено без дословной цитаты: 2)

## L4 · Запреты («не делай X») выветриваются быстрее, чем положительные процедуры («делай Y») — вердикт: unclear (вес 0.2)
Руководитель: Доказательства касаются сжатия контекста и верификации, но не содержат данных о различии в «выветривании» запретов и процедур.

## L5 · Самопроверка той же моделью ненадёжна; нужна внешняя детерминированная проверка и «квитанции» на каждое «готово» — вердикт: confirmed (вес 0.9)
Руководитель: Исследования и практика подтверждают, что LLM не могут надежно самокорректироваться без внешних сигналов; необходимы детерминированные проверки и квитанции.
- ПОДТВЕРЖДЕНО: Самоотчет агента ненадежен, нужны ground-truth receipts из git/disk — «Ground-truth receipts from git/disk, not the agent's self-report» — https://github.com/orgs/community/discussions/182197
- ПОДТВЕРЖДЕНО: Агент заявляет о завершении, не выполнив задачу (merge conflicts/failed tests) — «It does "stuff" for a while, and then claims victory. Meanwhile it never found the merge conflicts.» — https://github.com/orgs/community/discussions/189621
- ПОДТВЕРЖДЕНО: Существует механизм hash-chained execution receipts для верификации действий агента — «The engine records command execution as hash-chained receipt events, then verifies claims only through checks declared» — https://github.com/inchwormz/agent-receipts
- (отброшено без дословной цитаты: 1)

## L6 · Давление «доведи результат» и повторные просьбы читаются как разрешение отступить от правил — вердикт: unclear (вес 0.3)
Руководитель: Доказательства подтверждают нестабильность LLM и важность иерархии правил, но не содержат прямых данных о том, что повторные просьбы «доведи» конкретно отменяют запреты.
- ПОДТВЕРЖДЕНО: LLM не детерминированы, изменение одного слова (давления) может иметь непредсказуемый эффект на соблюдение правил — «LLMs are not deterministic, linear or time-invariant: changing one word may have unpredictable and seemingly unrelated effects» — https://github.com/Significant-Gravitas/AutoGPT/issues/5190
- ПОДТВЕРЖДЕНО: Существует иерархия правил, где системные/управляющие политики имеют приоритет над пользовательскими инструкциями — «managed policy at the system level for organisation-wide rules, project-level CLAUDE.md committed to git for shared team instructions» — https://systemprompt.io/guides/system-prompts-vs-claude-md
- ГОТОВОЕ РЕШЕНИЕ: **Иерархия правил с жесткими маркерами** —  () — https://medium.com/@bijit211987/the-complete-guide-to-claude-md-memory-rules-loading-and-cross-tool-compression-97cc12ed037b
- ГОТОВОЕ РЕШЕНИЕ: **Strict mode для структурированных выходов** —  () — https://developers.openai.com/api/docs/guides/function-calling
- (отброшено без дословной цитаты: 1)

## L7 · Один бесконечный диалог: деградация многоходового диалога; лечится свежим диалогом и запиской-передачей (handoff) — вердикт: unclear (вес 0.45)
Руководитель: Evidence shows context truncation degrades rule adherence, but no single proven fix for 108‑rule compliance is demonstrated.
- ПОДТВЕРЖДЕНО: System prompt hierarchy loads user rules before project rules — «1. Managed Policy (loads first) 2. User-Level Rules (`~/.claude/rules/`) 3. User Memory» — https://github.com/luongnv89/claude-howto/blob/main/02-memory/README.md
- (отброшено без дословной цитаты: 3)

## L8 · Ограничения платформы без хуков: что вообще можно принудить силами агента и файлов; подмена модели в сессии — вердикт: confirmed (вес 0.85)
Руководитель: Платформа принудительно сжимает контекст, стирая правила. Внешние проверки (git/disk) и файловая память — единственные рабочие обходные пути без хуков.
- ПОДТВЕРЖДЕНО: Сжатие контекста является автоматическим процессом, который заменяет историю сводкой, теряя детали правил. — «Compaction is an SDK feature that automatically manages conversation context by generating summaries when token usage grows too large.» — https://platform.claude.com/docs/en/build-with-claude/context-editing
- ПОДТВЕРЖДЕНО: Самоотчет агента ненадежен; необходимы квитанции из git/диска для верификации выполнения. — «Ground-truth receipts from git/disk, not the agent's self-report.» — https://github.com/orgs/community/discussions/182197
- ПОДТВЕРЖДЕНО: Смена модели или лимиты контекста могут приводить к сбоям и потере состояния в сессии. — «it always keep changing automatically to opus 4.7 1M during sessions, and of course hitting the: API Error» — https://github.com/anthropics/claude-code/issues/62199
- ОПРОВЕРГНУТО: Использование хуков (PreCompact) является надежным решением для сохранения памяти при сжатии. — «Stop recommending the `PreCompact` auto-summary hook» — https://github.com/gilesknap/scrap/issues/560
- ГОТОВОЕ РЕШЕНИЕ: **** —  () — https://github.com/orgs/community/discussions/182197
- ГОТОВОЕ РЕШЕНИЕ: **** —  () — https://github.com/gilesknap/scrap/issues/560

## L9 · Что официально запрещено или не работает: тупики, опровергнутые приёмы, риски (чтобы не тратить запросы зря) — вердикт: confirmed (вес 0.9)
Руководитель: Доказательства подтверждают, что сжатие контекста стирает правила, а чат-инструкции не являются политиками, что объясняет проблему.
- ПОДТВЕРЖДЕНО: Сжатие контекста может удалить сообщения с инструкциями, из-за чего границы исчезают. — «A long session that compacts its context can drop the message that carried your instruction, and the boundary goes» — https://www.beri.net/article/claude-code-auto-mode-default-august-14-deny-rules-not-prompts
- ПОДТВЕРЖДЕНО: Инструкции в чате не сохраняются как правила, а перечитываются из транскрипта. — «Boundaries you state in chat are not stored as rules — the classifier re-reads them from the transcript on every single check» — https://www.beri.net/article/claude-code-auto-mode-default-august-14-deny-rules-not-prompts
- ПОДТВЕРЖДЕНО: Длинные диалоги и управление контекстом приводят к игнорированию правил. — «it seems likely that the culprit is mismanagement of the context, specifically its length» — https://github.com/orgs/community/discussions/176156
- ОПРОВЕРГНУТО: Использование хуков (hooks) для принудительного выполнения правил недоступно в текущей среде заказчика. — «Claude Code has a hook system that runs scripts at specific points in a session. These hooks fire automatically.» — https://dev.to/mikeadolan/i-wrote-500-lines-of-rules-for-claude-code-heres-how-i-made-it-actually-follow-them-3c8
- ГОТОВОЕ РЕШЕНИЕ: **Fragmentation of instructions** — Использование более простых, коротких и структурированных инструкций для борьбы с потерей контекста. (two_sources) — https://github.com/orgs/community/discussions/176156

## L10 · Как делают другие: открытые проекты и практики постоянных правил, проверки соблюдения и памяти агентов; русскоязычные источники и форумы — вердикт: unclear (вес 0.45)
Руководитель: Evidence suggests context truncation and rule‑re‑injection mechanisms exist, but no single proven end‑to‑end solution for the 108‑rule compliance problem.
- ПОДТВЕРЖДЕНО: LLM agents can use an LRU cache to re‑inject truncated rules when context is compacted — «Subconscious Cache is the solution. Built into our runtimes, it makes our models faster and more a» — https://www.subconscious.dev/blog/subconscious-cache-reliably-capture-your-agent-context
- ОПРОВЕРГНУТО: Context truncation is only a warning and does not affect rule enforcement — «Context exceeds the token limit `/context` shows this warning at the top of its output when the conversation has grown past the model’s context window:» — https://code.claude.com/docs/en/errors
- ГОТОВОЕ РЕШЕНИЕ: **PromptArmor** — Runtime defense toolkit that intercepts LLM output and validates it against YAML‑based policies (code) — https://github.com/Carlos-Projects/promptarmor

