# plan.md — план запросов (протокол заказчика, этап 0)

| № | гипотеза | текст запроса | что хочу узнать |
|---|---|---|---|
| 1 | H1 inside | OpenAI ChatCompletion context window truncation policy documentation | how the platform truncates messages and which parts are removed |
| 2 | H1 inside | Anthropic Claude context compression mechanism PreCompact spec | details of Claude's internal compression of system prompts |
| 3 | H1 inside | LangChain Memory handling of system messages after token limit reached | how LangChain preserves or drops system prompts |
| 4 | H1 break | GitHub issue "system_prompt_truncation" OpenAI python library | exact error or behavior where system prompts are cut off |
| 5 | H1 break | Anthropic API issue #4567 context loss of system instructions after compression | reported bug where rules disappear after PreCompact |
| 6 | H1 break | Ошибка "Context overflow" при использовании Mem0 в длинных диалогах | точный текст ошибки и номер issue |
| 7 | H1 workaround | workaround keep system rules persistent using LangGraph memory buffer | method to re‑inject rules after truncation |
| 8 | H1 workaround | как использовать повторяющийся system prompt в начале каждого batch в Claude | технику автоматического добавления правил |
| 9 | H1 forbidden | OpenAI official statement about no guarantee of system message persistence | policy that forbids assuming rules survive truncation |
| 10 | H1 forbidden | Anthropic documentation "rules may be dropped" when token limit exceeded | explicit prohibition of rule persistence |
| 11 | H1 others | проекты с открытым кодом, реализующие постоянный набор правил в AgentGPT | пример кода, где правила сохраняются независимо от контекста |
| 12 | H1 others | GitHub repo "auto‑rule‑preserver" Python library for maintaining system prompts | open‑source solution that tracks and restores rules |
| 13 | H1 break | Mem0 cache invalidation when model switches in OpenAI API | behavior causing loss of stored rules after model change |
| 14 | H2 inside | How does Claude’s internal rule engine prioritize rules from AGENTS.md versus inline user messages? | priority mechanism details |
| 15 | H2 break | Does LangGraph’s context compression remove earlier rules? | exact compression behavior |
| 16 | H2 inside | What is the effect of the PreCompact hook on rule retention? | PreCompact impact |
| 17 | H2 break | Is there a documented issue where rules from a file are ignored in favor of user prompts? | issue number or quote |
| 18 | H2 workaround | How can we force rule persistence across model switches in Claude? | technique for persistence |
| 19 | H2 others | Are there open‑source projects that implement a rule‑based compliance layer for Claude? | project names and repos |
| 20 | H2 forbidden | What does the official Claude documentation say about rule enforcement limits? | official limits |
| 21 | H2 inside | Как правило «UserPromptSubmit» влияет на сохранение законов? | описание влияния |
| 22 | H2 break | Какие баг‑репорты связаны с игнорированием правил из AGENTS.md? | номера issue |
| 23 | H2 workaround | Какой workaround используют другие разработчики для постоянного соблюдения правил? | описание обхода |
| 24 | H2 others | Есть ли примеры кода, где правила сохраняются в Mem0? | кодовый пример |
| 25 | H2 forbidden | Что официально запрещено в правилах 1–5 и 60–65? | список запрещённых действий |
| 26 | H3 break | LLM instruction following failure conflicting rules github issue | Найти баг-репорты о игнорировании противоречивых инструкций |
| 27 | H3 inside | Claude Code CLAUDE.md conflicting instructions best practices | Официальные рекомендации по структуре правил в CLAUDE.md |
| 28 | H3 inside | LangGraph state management conflicting agent instructions | Как LangGraph обрабатывает конфликтующие состояния агента |
| 29 | H3 inside | Mem0 conflicting memory rules resolution strategy | Механизм разрешения конфликтов в памяти Mem0 |
| 30 | H3 inside | Letta (MemGPT) core memory conflicting facts handling | Обработка противоречий в ядре памяти Letta |
| 31 | H3 break | instruction overload LLM performance degradation arxiv | Исследования о деградации качества при большом числе правил |
| 32 | H3 break | system prompt conflicting rules LLM behavior github | Примеры кода, демонстрирующие хаос при конфликте правил |
| 33 | H3 workaround | как решить конфликт инструкций в промпте LLM | Русскоязычные обходные пути для противоречий в промптах |
| 34 | H3 workaround | приоритизация правил в системном промпте Claude | Методы установления иерархии правил для Claude |
| 35 | H3 workaround | структурирование правил JSON для LLM агент | Подход к формализации правил для лучшей обработки |
| 36 | H3 others | open source agent conflicting rules resolution github | Открытые проекты с логикой разрешения конфликтов |
| 37 | H3 others | AutoGen conflicting tool instructions handling | Как AutoGen справляется с противоречивыми инструкциями |
| 38 | H3 forbidden | LLM forbidden conflicting instructions documentation | Официальные предупреждения о недопустимости конфликтов |
| 39 | H3 forbidden | Claude Code PreCompact conflicting rules issue | Известные проблемы с конфликтами при сжатии контекста |
| 40 | H4 inside | LLM negative constraints vs positive instructions compliance rate study | Научные данные о разнице в следовании запретам и позитивным командам. |
| 41 | H4 break | github issue "negative prompt" "ignored" LLM agent rules | Баг-репорты, где модель игнорирует негативные инструкции в агентах. |
| 42 | H4 workaround | Claude Code CLAUDE.md best practices "do not" vs "always" | Рекомендации сообщества по формулировке правил в CLAUDE.md. |
| 43 | H4 others | LangGraph state management "forbidden" actions enforcement mechanism | Как LangGraph технически реализует запреты в графе состояний. |
| 44 | H4 others | Mem0 vs Letta memory retention negative constraints long context | Сравнение систем памяти по удержанию негативных правил. |
| 45 | H4 inside | LLM instruction following "negative constraints" failure mode analysis | Анализ причин сбоя следования негативным инструкциям. |
| 46 | H4 inside | arxiv paper "negative prompting" LLM compliance degradation | Исследования о деградации следования запретам при увеличении контекста. |
| 47 | H4 break | github "system prompt" "do not" ignored long conversation | Примеры кода/дискуссий о потере негативных правил в длинных чатах. |
| 48 | H4 workaround | как сформулировать запрет для нейросети чтобы она не забыла | Русскоязычные советы по переформулировке запретов в позитив. |
| 49 | H4 others | Claude Code PreCompact hook negative rules persistence | Как хуки Claude Code сохраняют правила при сжатии контекста. |
| 50 | H4 inside | LLM agent "negative constraints" "positive actions" prompt engineering guide | Гайды по балансу запретов и позитивных действий в промптах. |
| 51 | H4 break | почему нейросеть игнорирует запрет в длинном диалоге | Объяснение механизма забывания запретов в русскоязычных источниках. |
| 52 | H4 break | Letta core memory "negative" constraints retention issue | Проблемы с удержанием негативных правил в ядре памяти Letta. |
| 53 | H4 forbidden | официально запрещено ли использовать только запреты в системном промпте | Официальные рекомендации или запреты на использование только негативных инструкций. |
| 54 | H5 inside | How to implement a persistent rule store for Claude agents using LangGraph memory plugins? | details on memory plugin usage |
| 55 | H5 break | What is the official GitHub issue number for Claude’s rule enforcement bug in 2023? | issue ID and description |
| 56 | H5 workaround | Are there known workarounds for Claude’s context compression that preserve rule references? | список обходных решений |
| 57 | H5 others | Which open‑source project demonstrates deterministic compliance checks for AI agents? | project name and repo link |
| 58 | H5 forbidden | Is it officially prohibited to use external logging libraries with Claude agents? | official policy statement |
| 59 | H5 inside | Какие флаги в AGENTS.md отключают проверку законов? | список флагов |
| 60 | H5 break | What is the exact error message when a rule is violated in Claude’s log? | error text |
| 61 | H5 inside | Does the PreCompact module affect rule retention? | описание влияния |
| 62 | H5 others | How to generate a receipt after each 'ready' response in Claude? | implementation steps |
| 63 | H5 break | Is there a known issue where Claude forgets rule 42 after 200 turns? | описание проблемы |
| 64 | H5 others | What GitHub PR implements a receipt system for Claude agents? | PR link |
| 65 | H5 inside | Can we use Mem0 to persist rule state across sessions? | compatibility details |
| 66 | H6 inside | Where is the official documentation for the Letta rule enforcement mechanism in Claude's source code? | find Letta implementation details |
| 67 | H6 break | What GitHub issue number reports that repeated "prove the result" prompts cause rule violations in Claude? | identify issue and error quote |
| 68 | H6 inside | How does Mem0 store and restore legal rules across sessions? | описать хранение правил в Mem0 |
| 69 | H6 workaround | Is there a workaround to prevent rule loss when context is compressed by PreCompact? | найти способ сохранить правила при сжатии |
| 70 | H6 others | Which open-source project demonstrates consistent rule enforcement using LangGraph? | пример проекта с LangGraph |
| 71 | H6 forbidden | What is the official prohibition on using the UserPromptSubmit flag in repeated requests? | уточнить запрет на UserPromptSubmit |
| 72 | H6 inside | Does the AGENTS.md file list any flags that override standard rules? | проверить наличие флагов в AGENTS.md |
| 73 | H6 break | Which GitHub PR fixed the issue where repeated 'prove' prompts bypassed rule checks? | найти PR, исправляющий обход правил |
| 74 | H6 others | How do other agents handle rule duplication (rules 1–5 and 60–65)? | методы устранения дублирования правил |
| 75 | H6 break | What is the error message when a rule is ignored due to context truncation? | точный текст ошибки |
| 76 | H6 workaround | Can a custom flag be added to enforce rule persistence across sessions? | добавить флаг для сохранения правил |
| 77 | H6 forbidden | Where is the official policy on repeated rule enforcement prompts in Claude's documentation? | политика повторных запросов |
| 78 | H7 inside | LangGraph state management long context degradation github issue | Как LangGraph управляет состоянием при длинных диалогах |
| 79 | H7 inside | Claude Code CLAUDE.md context window limit documentation | Официальные лимиты контекста и роль CLAUDE.md |
| 80 | H7 inside | LLM agent forgets instructions after 1000 turns arxiv paper | Научные данные о деградации инструкций в длинных диалогах |
| 81 | H7 others | Letta Mem0 memory management long conversation github | Как Letta и Mem0 решают проблему памяти |
| 82 | H7 break | context compression artifact loss LLM agent github issue | Точные примеры потери данных при сжатии контекста |
| 83 | H7 break | LLM instruction following degradation long context benchmark | Метрики деградации следования инструкциям с длиной |
| 84 | H7 workaround | handoff protocol LLM agent state transfer new session | Протоколы передачи состояния между сессиями |
| 85 | H7 workaround | structured summary generation for LLM context handoff python | Генерация структурированных сводок для передачи контекста |
| 86 | H7 workaround | как передать контекст в новый диалог Claude Code | Практические методы передачи контекста в Claude Code |
| 87 | H7 break | проблема забывания правил в длинном диалоге LLM | Описания проблемы забывания правил на русском |
| 88 | H7 break | context window overflow error LLM agent github | Ошибки переполнения контекста в агентах |
| 89 | H7 others | открытые проекты управление памятью ИИ агентов python | Русскоязычные проекты управления памятью агентов |
| 90 | H7 forbidden | forbidden: modifying system prompt during runtime LLM | Ограничения на изменение системного промпта |
| 91 | H7 inside | why LLM ignores previous instructions in long chat | Причины игнорирования старых инструкций |
| 92 | H8 inside | OpenAI ChatCompletion token limit and context compression behavior documentation | understand how OpenAI truncates messages and its limits |
| 93 | H8 inside | Claude API system prompt persistence across model swaps | learn if Claude keeps system messages after model change |
| 94 | H8 inside | LangChain MemoryManager file persistence example | see how LangChain stores memory in files |
| 95 | H8 break | GitHub issue "UserPromptSubmit" flag ignored in Anthropic SDK | find reports of UserPromptSubmit flag not working |
| 96 | H8 break | openai/openai-python#4567 context truncation bug | locate a concrete bug where messages are dropped |
| 97 | H8 workaround | Mem0 library rule‑reset workaround for lost system prompts | discover a method to reload rules using Mem0 |
| 98 | H8 workaround | How to force re‑reading of a rules.txt file before each agent step in Arena Agent Mode | step‑by‑step guide to reload rules from file |
| 99 | H8 others | GitHub repository implementing rule persistence for Claude agents without external hooks | example open‑source project solving the same problem |
| 100 | H8 others | Letta agent framework handling model swaps and prompt continuity | see if Letta already solves prompt loss |
| 101 | H8 forbidden | Что запрещено использовать для обхода ограничения контекста в Anthropic API | список официальных запретов от Anthropic |
| 102 | H8 forbidden | Какие ограничения накладывает платформа Arena Agent Mode на изменение системного промта | узнать, что нельзя менять в системе |
| 103 | H8 others | Как в LangGraph реализована проверка согласованности правил между шагами | пример кода проверки правил в цепочке |
| 104 | H8 inside | PreCompact internal flag documentation in Anthropic SDK | find official description of PreCompact behavior |
| 105 | H8 break | GitHub issue "rules file ignored after context compression" in arena-agent repo | identify a real issue where rules file is dropped |
| 106 | H8 workaround | Workaround for preserving 108‑rule set using Python standard library only | решение без сторонних пакетов |
| 107 | NEG inside | What is the official documentation for the Claude Code rule enforcement API and its limitations? | details on rule enforcement API and known limits |
| 108 | NEG break | Is there a GitHub issue where Claude AI fails to apply rules from AGENTS.md during long dialogs? | specific issue number and error snippet |
| 109 | NEG workaround | How can a LangGraph agent be configured to persist rule definitions across turns? | LangGraph config for rule persistence |
| 110 | NEG others | What open-source projects implement a rule-based compliance layer for Claude agents? | list of projects and their GitHub repos |
| 111 | NEG forbidden | Which rules are officially marked as forbidden or unsupported in the Claude policy set? | list of prohibited rules and their IDs |
| 112 | NEG inside | Какова внутренняя реализация хранения правил в Mem0? | описание хранения правил в Mem0 |
| 113 | NEG break | Есть ли известные баги, связанные с игнорированием правил в PreCompact? | названия багов и номера issue |
| 114 | NEG workaround | Какие workarounds используют сообщества для обеспечения соблюдения правил в LangGraph? | пошаговый обход |
| 115 | NEG others | Какие проекты с открытым кодом используют Letta для контроля за соблюдением правил? | список проектов и их репозитории |
| 116 | NEG forbidden | Какие правила официально запрещены в Claude и почему? | список запрещенных правил и причины |
| 117 | NEG inside | Does the Claude policy document specify that rule enforcement is not guaranteed during context compression? | policy statement about compression |
| 118 | NEG break | What is the GitHub issue number for the bug where UserPromptSubmit ignores rules after 100 messages? | issue number and description |
| 119 | OSS inside | LangGraph state persistence memory management long context github issue | Как LangGraph хранит состояние между шагами |
| 120 | OSS inside | Letta Mem0 agent memory architecture open source github | Архитектура памяти в Letta и Mem0 |
| 121 | OSS others | AGENTS.md CLAUDE.md best practices persistent rules github | Стандарты хранения правил в файлах для агентов |
| 122 | OSS break | LLM agent forgets instructions after context compression workaround | Проблемы с потерей инструкций при сжатии |
| 123 | OSS inside | Claude Code PreCompact hook memory persistence documentation | Механизмы сохранения памяти в Claude Code |
| 124 | OSS workaround | как сохранить контекст ИИ агента при сжатии диалога форум | Русскоязычные обсуждения сохранения контекста |
| 125 | OSS workaround | deterministic validation LLM output against rules python standard library | Проверка вывода ИИ по правилам на Python |
| 126 | OSS others | arxiv LLM agent memory management long horizon tasks | Исследования по памяти агентов на длинных задачах |
| 127 | OSS break | issue: agent ignores system prompt after context window limit | Баги, связанные с игнорированием промпта |
| 128 | OSS others | open source agent framework memory file sync github | OSS-фреймворки с синхронизацией файлов памяти |
| 129 | OSS break | почему ИИ забывает правила в длинном диалоге stackoverflow | Причины забывчивости ИИ на StackOverflow RU |
| 130 | OSS workaround | workaround: force LLM to read file before every response | Принуждение ИИ читать файл перед ответом |
| 131 | OSS forbidden | forbidden: modifying system prompt in Arena Agent Mode | Ограничения на изменение системного промпта |
| 132 | OSS workaround | детерминированная проверка выполнения правил ИИ агентом python | Методы детерминированной проверки на Python |
| 133 | H1 inside (ПО ХОДУ) | GitHub issue #12345 "context loss" after OpenAI ChatCompletion truncation | details of token truncation impact on persistent system rules |
| 134 | H1 inside (ПО ХОДУ) | Anthropic API #9876 "system_prompt_compaction" error handling | error message and work‑arounds for lost system instructions |
| 135 | H1 break (ПО ХОДУ) | LangChain memory buffer "compaction loss" persistent rules example | how LangChain deals with rule retention after compression |
| 136 | H1 others (ПО ХОДУ) | GitHub repo "rule‑preserver‑v2" Python library for context compaction | features and usage of new rule‑preserving library |
| 137 | H1 inside (ПО ХОДУ) | OpenAI official doc "system message persistence policy" 2026 | последняя политика сохранения системных сообщений |
| 138 | H1 break (ПО ХОДУ) | Claude Cookbook "context engineering" memory compaction techniques | техники сохранения правил при сжатии контекста |
| 139 | H1 others (ПО ХОДУ) | GitHub issue #4567 "compaction loss" in Anthropic Claude conversation | описание проблемы и предложенные решения |
| 140 | H2 break (ПО ХОДУ) | github anthropic claude-code issue "PostCompact" "rule" ignored | Verify if PostCompact hook triggers rule loss |
| 141 | H2 break (ПО ХОДУ) | site:github.com "AGENTS.md" "low priority" OR "ignored" issue | Find specific issues about AGENTS.md weight |
| 142 | H2 workaround (ПО ХОДУ) | Claude Code "12 Rules" context window limit enforcement | Analyze the 12 rules strategy for persistence |
| 143 | H2 others (ПО ХОДУ) | Cursor "ignore rules" bug report community forum | Check if Cursor has similar rule priority bugs |
| 144 | H2 workaround (ПО ХОДУ) | github "Claude-Skills-Governance-Risk-and-Compliance" implementation details | Inspect governance skills for rule enforcement logic |
| 145 | H2 break (ПО ХОДУ) | "I Wrote 200 Lines of Rules" Claude Code ignored analysis | Understand failure mode of long rule sets |
| 146 | H2 workaround (ПО ХОДУ) | LangGraph "context compression" "forget" rules retention strategy | See how LangGraph handles rule memory loss |
| 147 | H3 break (ПО ХОДУ) | Claude Code "preCompact" hook conflict resolution | how preCompact cancels compaction and how to avoid it |
| 148 | H3 inside (ПО ХОДУ) | mem0 Issue #5330 frequency tracking cleanup strategy | details on memory access frequency tracking and cleanup |
| 149 | H3 workaround (ПО ХОДУ) | LangGraph state management conflicting agent instructions pattern | способы разрешения конфликтов инструкций в LangGraph |
| 150 | H3 others (ПО ХОДУ) | AutoGen conflict-resolver skill Issue #23 | functionality of conflict-resolver skill in AutoGen |
| 151 | H3 inside (ПО ХОДУ) | x-zheng16/System-Prompt-Open conflict resolution examples | how system prompts are extracted and resolved |
| 152 | H3 workaround (ПО ХОДУ) | nospecs/ovadare AI conflict resolution framework usage | practical usage of Ovadare for agent conflicts |
| 153 | H3 others (ПО ХОДУ) | Claude Code "Best Practices" conflicting instructions guidelines | что включают лучшие практики для избежания конфликтов |
| 154 | H4 inside (ПО ХОДУ) | github "Claude Code" "PreCompact" "issue #43946" "negative rules" | подробности о влиянии PreCompact на сохранение запретных правил |
| 155 | H4 break (ПО ХОДУ) | github "easydiffusion" "issue #809" "negative prompts" ignored | примеры игнорирования отрицательных промтов в Diffusion |
| 156 | H4 workaround (ПО ХОДУ) | Agent-Threat-Rule "agent-threat-rules" "negative constraints" enforcement | как правило «не делай» реализуется в Agent Threat Rule |
| 157 | H4 inside (ПО ХОДУ) | gitlab "Letta core memory" "negative constraints" retention issue | проблемы удержания отрицательных ограничений в Letta |
| 158 | H4 others (ПО ХОДУ) | Claude Code "best practices" "do not" vs "always" | рекомендации по формулировке запретов в CLAUDE.md |
| 159 | H4 forbidden (ПО ХОДУ) | github "LangGraph" "forbidden" actions enforcement mechanism | механизм блокировки запрещённых действий в LangGraph |
| 160 | H4 inside (ПО ХОДУ) | arxiv "negative prompting" "context loss" LLM | исследование потери контекста при отрицательных промтах |
| 161 | H5 inside (ПО ХОДУ) | What is the error message when the deterministic-verification flag is disabled in Claude? | exact error text shown when deterministic-verification is off |
| 162 | H5 workaround (ПО ХОДУ) | How can I enable the receipt-generation flag in the AGENTS.md file for a Claude agent? | пошаговое включение флага создания квитанций |
| 163 | H5 inside (ПО ХОДУ) | Which GitHub issue describes the loss of rule 7 after 150 turns in Claude Code? | номер issue и краткое описание проблемы |
| 164 | H5 inside (ПО ХОДУ) | What is the PR number that adds deterministic verification to the Claude codebase? | номер PR и его цель |
| 165 | H5 others (ПО ХОДУ) | Is there a flag in the deterministic-verification project that forces external logging of every 'ready' response? | название флага и его назначение |
| 166 | H5 break (ПО ХОДУ) | What is the exact error message shown when the PreCompact module removes rule references in Claude? | текст ошибки при удалении правил PreCompact |
| 167 | H6 break (ПО ХОДУ) | github issue "exit code 1844674407" context truncation crash | Найти конкретный баг-репорт с этим кодом выхода |
| 168 | H6 break (ПО ХОДУ) | github issue "PR review runs fail" "is_error: true" 0 turns | Исследовать причину мгновенного сбоя PR-ревью без выполнения |
| 169 | H6 others (ПО ХОДУ) | github issue "200 Lines of Rules" "Ignored Them All" Claude Code | Найти технический разбор почему длинные правила игнорируются |
| 170 | H6 workaround (ПО ХОДУ) | mem0 "conditional filter" agent assistant said preserve | Понять механизм фильтрации памяти в Mem0 для правил |
| 171 | H6 break (ПО ХОДУ) | github issue "Feb updates" "unusable for complex engineering tasks" | Найти отчет о деградации после февральских обновлений |
| 172 | H6 workaround (ПО ХОДУ) | AGENTS.md vs CLAUDE.md "actually read" coding agents priority | Уточнить приоритет чтения файлов конфигурации агентами |
| 173 | H6 workaround (ПО ХОДУ) | github issue "Compaction Memory" "Losing Context Across Compressions" product | Найти решение проблемы потери контекста при сжатии |
| 174 | H7 break (ПО ХОДУ) | langchain-ai/how_to_fix_your_context context overflow issue 5771 | details of context overflow fix steps |
| 175 | H7 break (ПО ХОДУ) | openclaw/openclaw context overflow error #5771 | exact error message and stack trace |
| 176 | H7 inside (ПО ХОДУ) | lettai/letta issue 2514 memory implementation optimization | how memory layer reduces context loss |
| 177 | H7 break (ПО ХОДУ) | NousResearch/hermes-agent issue 22244 context compression failure | reasons for cross‑session fragment injection |
| 178 | H7 break (ПО ХОДУ) | mem0ai/mem0 context loss bug recent conversation | bug report on recent conversation forgetting |
| 179 | H7 forbidden (ПО ХОДУ) | Claude Code context window limit error | описание ограничения окна контекста |
| 180 | H7 workaround (ПО ХОДУ) | LLM handoff protocol state transfer new session example | пример кода для передачи состояния |
| 181 | H8 workaround (ПО ХОДУ) | GitHub issue #21432: how to enable "force_reload_rules" flag for Claude 3.5 in Arena Agent Mode | details on force_reload_rules flag usage and limitations |
| 182 | H8 inside (ПО ХОДУ) | openai/openai-python#7890: using "precompact=True" to bypass token limit during ChatCompletion | explains precompact parameter and its effect on context compression |
| 183 | H8 break (ПО ХОДУ) | Claude API error 502: "Unexpected model swap during conversation" – possible workaround | почему возникает ошибка и как её обойти |
| 184 | H8 others (ПО ХОДУ) | GitHub issue #34567: flag "ignore_system_prompt" in LangGraph memory manager | what this flag does and when to use it |
| 185 | H8 inside (ПО ХОДУ) | Letta agent framework: how to set "model_override" without external hooks | методы установки модели в сессии агента |
| 186 | H8 workaround (ПО ХОДУ) | Anthropic SDK bug #5123: context compression causes system prompt loss – suggested patch | пошаговый патч для сохранения системного промта |
| 187 | H8 forbidden (ПО ХОДУ) | openai/openai-python#1234: forbidden use of "max_tokens" with "stream=True" in ChatCompletion | why this combination is disallowed и как обойти |
| 188 | NEG break (ПО ХОДУ) | How to enable UserPromptSubmit hooks in a non-GitHub environment without external dependencies? | details on enabling hooks locally |
| 189 | NEG inside (ПО ХОДУ) | What is the issue number for the bug where Claude ignores AGENTS.md rules after ~15 tool calls? | GitHub issue reference |
| 190 | NEG forbidden (ПО ХОДУ) | Какие флаги в Claude API отключают проверку правил в режиме PreCompact? | список запрещённых флагов |
| 191 | NEG workaround (ПО ХОДУ) | Which open-source project implements a rule-based compliance layer for Claude agents using Letta? | project name and repo |
| 192 | NEG inside (ПО ХОДУ) | Какой номер issue описывает проблему с UserPromptSubmit hook в Windows Git Bash? | номер issue и описание |
| 193 | NEG forbidden (ПО ХОДУ) | What are the official policy checks added to Claude on Nov 12 that affect rule enforcement? | list of new checks |
| 194 | NEG break (ПО ХОДУ) | Как реализовать Mem0 хранение правил без использования внешних библиотек? | инструкции по реализации |
| 195 | OSS workaround (ПО ХОДУ) | Mem0 local mode without API key github issue | Локальный запуск Mem0 без внешних API и ключей |
| 196 | OSS workaround (ПО ХОДУ) | LangGraph checkpointer sqlite local file persistence no server | Хранение состояния в SQLite для локального агента |
| 197 | OSS forbidden (ПО ХОДУ) | Arena Agent Mode external memory integration forbidden | Запреты на внешние модули памяти в Arena |
| 198 | OSS others (ПО ХОДУ) | issue: agent context loss after compaction github | Реальные кейсы потери контекста после сжатия |
| 199 | OSS workaround (ПО ХОДУ) | как подключить mem0 локально python без облака | Инструкции по локальному разворачиванию Mem0 на Python |
| 200 | OSS others (ПО ХОДУ) | LangMem vs Mem0 local storage comparison github | Сравнение локальных возможностей LangMem и Mem0 |
| 201 | OSS workaround (ПО ХОДУ) | claude code hook read file before response github | Примеры хуков для чтения файлов памяти |
