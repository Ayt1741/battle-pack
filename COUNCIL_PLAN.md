# plan.md — план запросов (протокол заказчика, этап 0)

| № | гипотеза | текст запроса | что хочу узнать |
|---|---|---|---|
| 1 | H1 inside | Anthropic Claude context compression documentation | how Claude compresses context internally |
| 2 | H1 break | GitHub issue 42 Claude context truncation loses system messages | exact error or bug where rules disappear after compression |
| 3 | H1 inside | Как работает механизм сжатия контекста в Claude и какие сообщения отбрасываются | детали алгоритма сжатия и приоритетов сообщений |
| 4 | H1 workaround | Workaround to preserve system prompt after Claude context compression using Mem0 | method to store and re‑inject rules after compression |
| 5 | H1 others | Open‑source project that keeps persistent LLM rules with LangGraph | example of external rule storage for LLM agents |
| 6 | H1 forbidden | Запрет на отключение сжатия контекста в Claude API | official statement that disabling compression is not allowed |
| 7 | H1 inside | PreCompact flag Anthropic API | whether a flag exists to control pre‑compression behavior |
| 8 | H1 break | GitHub issue anthonyc/claude-sdk #128 "system prompt lost after summarization" | specific issue showing rule loss after summarization |
| 9 | H1 workaround | Как обойти потерю правил в Claude при длительном диалоге без внешних хуков | technique to re‑assert rules inside same session |
| 10 | H1 others | Other LLM platforms (e.g., OpenAI, Cohere) handling of context compression for system messages | comparative approaches to preserve system prompts |
| 11 | H1 forbidden | Officially unsupported method to disable Claude content compression | any mention that turning off compression is prohibited |
| 12 | H1 inside | UserPromptSubmit token handling in Anthropic API | how user prompt submission interacts with compression |
| 13 | H1 break | Как правило 60‑65 влияют на приоритет сообщений при сжатии контекста | whether specific rule numbers are dropped by compression |
| 14 | H2 inside | Claude API documentation context compression rules enforcement | how Claude handles system messages during context compression |
| 15 | H2 inside | LangChain memory management file vs message priority documentation | official description of channel weighting in LangChain |
| 16 | H2 inside | Документация LangChain о приоритете файлового канала над пользовательским сообщением | где описано, какой канал считается более важным |
| 17 | H2 break | GitHub issue Anthropic Claude context truncation loses system messages #1234 | exact error or symptom when system prompts disappear |
| 18 | H2 break | LangGraph issue context compression drops earlier messages 2024-03 | specific issue showing loss of early rules |
| 19 | H2 break | GitHub issue #5678 LangChain потеря правил из файла при сжатии контекста | цитата ошибки и номер issue о пропаже правил |
| 20 | H2 workaround | How to persist system prompt across Claude sessions using Mem0 library | code example that stores rules outside the main context |
| 21 | H2 workaround | LangChain workaround for preserving user rules in file channel | step‑by‑step guide to keep file rules from being trimmed |
| 22 | H2 workaround | Как обойти ограничение контекста Claude, сохраняя правила в отдельном файле | практический пример обхода ограничения |
| 23 | H2 others | Open‑source agent framework that guarantees rule compliance across turns | projects with built‑in rule priority handling |
| 24 | H2 others | GitHub project 'agentic' implements rule priority file vs message | repository that shows explicit rule ordering logic |
| 25 | H2 forbidden | Anthropic policy forbids modifying system prompt after request | official statement that changing system prompt is prohibited |
| 26 | H2 forbidden | OpenAI usage policy prohibits storing user rules in external files for compliance | policy clause that bans external rule storage |
| 27 | H2 forbidden | Запрещено ли в политике Anthropic хранить правила в пользовательском файле | официальный запрет на хранение правил в файлах |
| 28 | H3 inside | Claude documentation rule processing precedence system_prompt token allocation | understand internal rule precedence handling |
| 29 | H3 inside | Как в AGENTS.md описан порядок применения конфликтующих правил | узнать порядок применения правил в AGENTS.md |
| 30 | H3 break | OpenAI ChatGPT issue #12345 rule conflict causing omission after context compression | find bug report about rule loss |
| 31 | H3 break | Ошибка PreCompact: "Rule truncation exceeded token limit" issue #987 on GitHub | получить точную цитату ошибки PreCompact |
| 32 | H3 workaround | LangChain memory buffer workaround to preserve system instructions across compressions | method to keep rules in memory |
| 33 | H3 workaround | Как в Mem0 реализован fallback‑prompt для сохранения всех правил | узнать способ резервного сохранения правил |
| 34 | H3 others | Letta open‑source project handling instruction overload with token budgeting | see how Letta manages many rules |
| 35 | H3 others | Пример проекта на GitHub, где используют CLAUDE.md для управления конфликтующими инструкциями | найти открытый код с разрешением конфликтов |
| 36 | H3 forbidden | OpenAI policy officially forbids deterministic enforcement of user‑provided rule sets | official statement on rule enforcement limits |
| 37 | H3 forbidden | Запрещено использовать внешние хуки для проверки соблюдения инструкций согласно OpenAI Usage Policy | получить официальное ограничение на внешние проверки |
| 38 | H3 inside | UserPromptSubmit flag documentation token budget allocation for system rules | details on UserPromptSubmit token budgeting |
| 39 | H3 break | GitHub issue #4567 "instruction conflict resolution" in LangGraph repository | find concrete failure example |
| 40 | H3 others | How other LLM platforms (e.g., Anthropic Claude) handle contradictory system prompts in long sessions | compare conflict handling across platforms |
| 41 | H5 inside | github LangGraph deterministic validation step agent loop | Как встроить детерминированный шаг проверки в LangGraph |
| 42 | H5 inside | Claude Code PreCompact hook external validation script | Официальные хуки Claude Code для внешней проверки |
| 43 | H5 break | LLM agent self-verification failure rate github issue | Точные примеры сбоев самопроверки в open-source проектах |
| 44 | H5 inside | arxiv LLM agent external verifier deterministic check | Научные работы о внешних верификаторах для LLM |
| 45 | H5 others | Mem0 Letta agent memory external state validation | Как Mem0/Letta хранят состояние для проверки |
| 46 | H5 break | github issue agent claims done but failed test | Баг-репорты о ложных утверждениях завершения |
| 47 | H5 workaround | обход проблемы забывания правил ИИ агент внешний скрипт проверка | Русскоязычные обсуждения обхода через внешние скрипты |
| 48 | H5 workaround | как проверить что ИИ выполнил задачу детерминированно | Практические методы детерминированной проверки выполнения |
| 49 | H5 others | github repo agent receipt proof of work pattern | Проекты с паттерном «квитанций» для агентов |
| 50 | H5 forbidden | forbidden: LLM self-correction without external feedback | Официальные предупреждения о ненадёжности самокоррекции |
| 51 | H5 forbidden | запрет на доверие самопроверке ИИ в production | Рекомендации по запрету доверия самопроверке |
| 52 | H5 workaround | python standard library json schema validation agent output | Как валидировать вывод агента стандартной библиотекой |
| 53 | H5 break | github issue context compression loses system prompt rules | Проблемы потери правил при сжатии контекста |
| 54 | H5 workaround | внешняя проверка ИИ агента через bash скрипт | Примеры bash-скриптов для внешней проверки агента |
| 55 | H6 inside | Как в документации Anthropic API описана обработка конфликтующих системных инструкций? | структуру приоритета правил |
| 56 | H6 inside | What does the Claude 3 system prompt specification (Claude.md) say about rule hierarchy? | rule precedence details |
| 57 | H6 inside | GitHub issue for LangChain memory handling: how are system messages stored and trimmed? | memory trimming algorithm |
| 58 | H6 break | OpenAI API error 'ContentPolicyViolation' exact message when user repeats 'finish the result' | error text and code |
| 59 | H6 break | Ошибка SafetyViolationError в Anthropic API при повторных запросах «доведи результат» | номер issue и пример |
| 60 | H6 break | GitHub issue #1234 in AutoGPT repo about policy override after multiple 'complete the task' prompts | issue details |
| 61 | H6 workaround | How to implement a verification step using Mem0 to enforce rule compliance after each agent action? | code example |
| 62 | H6 workaround | Обход ограничения политики в Claude через повторную проверку с помощью Letta | пример кода |
| 63 | H6 workaround | Using LangGraph's guard nodes to reject outputs that violate predefined constraints | implementation guide |
| 64 | H6 others | How does the open-source project 'Agentic' on GitHub enforce static policy rules across long dialogues? | design description |
| 65 | H6 others | Как в проекте LlamaIndex реализовано постоянное соблюдение пользовательских правил? | architectural overview |
| 66 | H6 others | What mechanisms do OpenAI's function calling agents use to ensure policy compliance? | technical description |
| 67 | H6 forbidden | What does OpenAI policy explicitly forbid: ignoring safety filters when user says 'just finish'? | policy excerpt |
| 68 | H6 forbidden | Какие правила Anthropic запрещают отключать проверку правил по запросу пользователя? | official statement |
| 69 | H7 inside | How does Claude handle context limits and rule truncation in long conversations? | Understand context truncation behavior. |
| 70 | H7 inside | What is the maximum token limit for Claude 3.5 Sonnet? | Token limit details. |
| 71 | H7 inside | Does Claude store user rules in a persistent memory module like Mem0? | Check persistent memory usage. |
| 72 | H7 break | Is there a known issue where Claude forgets user-defined rules after 50 turns? | Exact error or issue number. |
| 73 | H7 break | What is the GitHub issue #12345 about Claude forgetting rules? | Specific issue reference. |
| 74 | H7 workaround | Is there a workaround using a handoff file to preserve rules across sessions? | Handoff strategy. |
| 75 | H7 others | How do other agents like LangGraph maintain rule compliance? | Open source approach. |
| 76 | H7 forbidden | Does the official Claude documentation forbid using custom rule files? | Check policy. |
| 77 | H7 inside | Как правило обрабатывается в Claude при длительном диалоге? | Механизм обработки правил. |
| 78 | H7 break | Есть ли известный баг, когда Claude забывает правила после 30 сообщений? | Точная цитата ошибки. |
| 79 | H7 workaround | Какой workaround используют другие проекты для сохранения правил? | Примеры обхода. |
| 80 | H7 forbidden | Какие ограничения на использование пользовательских правил в официальной документации? | Официальные запреты. |
| 81 | H7 others | Есть ли пример кода на Python, который сохраняет правила в файл и загружает их в начале диалога? | Python example. |
| 82 | H8 inside | Arena Agent Mode context compression limits github issue | Официальные лимиты контекста и поведение при сжатии |
| 83 | H8 workaround | Claude Code PreCompact hook alternative file based memory | Обход сжатия контекста через файлы в Claude Code |
| 84 | H8 break | LangGraph checkpointer persistence state loss issue | Как LangGraph теряет состояние при сбоях |
| 85 | H8 others | LLM agent self-correction bash script verification pattern | Паттерны самопроверки агента через bash |
| 86 | H8 break | AGENTS.md CLAUDE.md instruction following failure rate | Статистика игнорирования инструкций в файлах |
| 87 | H8 others | Mem0 Letta long term memory agent context window | Как внешние памяти интегрируются с агентами |
| 88 | H8 forbidden | Arena AI agent mode bash execution restrictions | Что запрещено в bash-среде Arena |
| 89 | H8 inside | LLM context window truncation detection method | Методы детектирования обрезки контекста |
| 90 | H8 workaround | агент ИИ забывание правил bash скрипт проверка | Русскоязычные решения по проверке правил |
| 91 | H8 break | сжатие контекста LLM потеря инструкций github | Примеры потери инструкций при сжатии |
| 92 | H8 others | open source agent memory file system based | Open-source проекты с файловой памятью |
| 93 | H8 inside | Claude Code model switch context reset behavior | Поведение контекста при смене модели |
| 94 | H8 workaround | детерминированная проверка ИИ агента без внешних API | Методы детерминированной проверки без API |
| 95 | H8 others | LLM agent state machine file persistence github | Реализации конечных автоматов в файлах |
| 96 | NEG inside | What is the official documentation for the Claude Code rule enforcement API and its limitations? | details on rule enforcement API and known limits |
| 97 | NEG break | Is there a GitHub issue where Claude AI fails to apply rules from AGENTS.md during long dialogs? | specific issue number and error snippet |
| 98 | NEG workaround | How can a LangGraph agent be configured to persist rule definitions across turns? | LangGraph config for rule persistence |
| 99 | NEG others | What open-source projects implement a rule-based compliance layer for Claude agents? | list of projects and their GitHub repos |
| 100 | NEG forbidden | Which rules are officially marked as forbidden or unsupported in the Claude policy set? | list of prohibited rules and their IDs |
| 101 | NEG inside | Какова внутренняя реализация хранения правил в Mem0? | описание хранения правил в Mem0 |
| 102 | NEG break | Есть ли известные баги, связанные с игнорированием правил в PreCompact? | названия багов и номера issue |
| 103 | NEG workaround | Какие workarounds используют сообщества для обеспечения соблюдения правил в LangGraph? | пошаговый обход |
| 104 | NEG others | Какие проекты с открытым кодом используют Letta для контроля за соблюдением правил? | список проектов и их репозитории |
| 105 | NEG forbidden | Какие правила официально запрещены в Claude и почему? | список запрещенных правил и причины |
| 106 | NEG inside | Does the Claude policy document specify that rule enforcement is not guaranteed during context compression? | policy statement about compression |
| 107 | NEG break | What is the GitHub issue number for the bug where UserPromptSubmit ignores rules after 100 messages? | issue number and description |
| 108 | OSS inside | How do open source agents implement persistent rule enforcement using a local JSON file and checksum verification? | details of file format and checksum process |
| 109 | OSS inside | What GitHub projects provide a middleware that intercepts LLM output to enforce rule compliance? | list of repos and key modules |
| 110 | OSS inside | Which open source agents use an LRU cache to re‑inject truncated rules in truncated context? | examples and cache size settings |
| 111 | OSS break | What exact error messages appear when Claude 3.5 fails to load AGENTS.md due to context truncation? | точные цитаты ошибок |
| 112 | OSS break | Issue #1234 in LangChain repo shows rule‑violation detection failing after model switch – what is the root cause? | issue number and description |
| 113 | OSS workaround | How can a local rule‑checker be implemented in pure Python to flag prohibited phrases before output? | step‑by‑step guide |
| 114 | OSS others | What open source project demonstrates a client‑side rule validator that rejects outputs containing forbidden content? | project name and key file |
| 115 | OSS forbidden | Does the Claude API provide a flag to enforce rule compliance server‑side? | availability of such flag |
| 116 | OSS workaround | Как реализовать проверку правил в локальном агенте, используя только стандартную библиотеку Python? | пошаговый алгоритм |
| 117 | OSS inside | Какие флаги в AGENTS.md запрещают генерацию чисел, и как они проверяются? | список флагов и их описание |
| 118 | OSS others | What arXiv paper discusses deterministic rule enforcement in LLM agents? | paper title and DOI |
| 119 | OSS inside | How does Mem0 handle rule persistence across model switches? | mechanism description |
| 120 | H1 break (ПО ХОДУ) | GitHub issue NodeNestor/claude-rolling-context #7 "rolling context" flag | details on the rolling‑context flag and its impact on rule loss |
| 121 | H1 break (ПО ХОДУ) | Claude Opus 4.8 memory persistence bug "system prompt" | описание бага потери системных правил в Opus 4.8 |
| 122 | H1 inside (ПО ХОДУ) | autocompact flag disable Claude API documentation | official docs on turning off autocompact in Claude API |
| 123 | H1 inside (ПО ХОДУ) | PreCompact parameter Claude API v2.3 usage example | пример применения PreCompact при работе с Claude |
| 124 | H1 break (ПО ХОДУ) | GitHub issue anthonyc/claude-sdk #215 "system prompt lost after rolling summary" | report of system prompt loss after rolling‑summary compression |
| 125 | H1 others (ПО ХОДУ) | Claude Platform Docs "Context editing" best practices | рекомендации по редактированию контекста без потери правил |
| 126 | H2 break (ПО ХОДУ) | GitHub issue #13579 "RulePriorityError" file channel overrides user message Claude | Find details of RulePriorityError causing rule loss |
| 127 | H2 break (ПО ХОДУ) | LangChain issue #8421 "file_channel_priority" fails under context compression | Investigate file channel priority bug in LangChain |
| 128 | H2 inside (ПО ХОДУ) | Anthropic flag ANTH-CTX-2024-07 context compression rule weight | Understand new Anthropic flag affecting rule weight in compression |
| 129 | H2 others (ПО ХОДУ) | Mem0 library v2.2 release notes persistent system prompt across Claude sessions | Check if Mem0 v2.2 adds system prompt persistence |
| 130 | H2 workaround (ПО ХОДУ) | GitHub project "agentic" issue #210 "system_prompt_file_priority" | Find workaround for system prompt file priority issue |
| 131 | H2 forbidden (ПО ХОДУ) | Политика Anthropic запрещает хранить правила в файле после 2024‑08 | Уточнить ограничения политики Anthropic по файлам правил |
| 132 | H3 break (ПО ХОДУ) | GitHub issue #3362 langgraph_supervisor incompatibility with langgraph>=1.0.0 | Identify root cause and fix for dependency conflict |
| 133 | H3 inside (ПО ХОДУ) | openclaw issue #25620 context compaction fails token limit exceeded | Details on compaction failure and suggested workarounds |
| 134 | H3 others (ПО ХОДУ) | Zenity runtime protection flag for OpenAI AgentKit agents | Explain purpose and configuration of Zenity protection flag |
| 135 | H3 workaround (ПО ХОДУ) | Prompt budgeting token cap flag usage in Letta projects | Как применить флаг ограничения токенов в проектах Letta |
| 136 | H3 inside (ПО ХОДУ) | LangMem memory persistence flag in LangChain long‑term agents | Specification of memory persistence flag for LangMem |
| 137 | H3 break (ПО ХОДУ) | UserPromptSubmit flag token allocation conflict with system rules | Как конфликтует флаг UserPromptSubmit с системными инструкциями |
| 138 | H4 inside (ПО ХОДУ) | site:github.com issue "negative constraint" "context compression" LLM | Issue с жалобой на потерю запретов при сжатии контекста |
| 139 | H4 break (ПО ХОДУ) | "rolling context" "procedural memory" vs "inhibitory control" LLM | Сравнение устойчивости процедурных инструкций и запретов в скользящем окне |
| 140 | H4 inside (ПО ХОДУ) | github.com/NodeNestor/claude-rolling-context issues "rule" "forgotten" | Баги в конкретном репозитории, связанные с забыванием правил |
| 141 | H4 workaround (ПО ХОДУ) | LLM agent "do not" vs "always do" retention rate benchmark | Бенчмарки или тесты на долговременное удержание негативных и позитивных указаний |
| 142 | H4 others (ПО ХОДУ) | site:reddit.com/r/LocalLLaMA "context window" "negative prompt" lost | Практические кейсы пользователей о потере негативных промптов в длинных чатах |
| 143 | H4 inside (ПО ХОДУ) | "hash-chained" "agent-receipts" "instruction adherence" decay | Данные из проекта inchwormz о деградации следования инструкциям |
| 144 | H4 others (ПО ХОДУ) | RU: "контекст" "запрет" "процедура" "модель" "забывает" | Русскоязычные обсуждения различий в памяти моделей для запретов и действий |
| 145 | H5 inside (ПО ХОДУ) | inchwormz/agent-receipts hash‑chained receipt verification github issue | implementation details of hash‑chained receipts for AI agents |
| 146 | H5 break (ПО ХОДУ) | LangGraph deterministic validation step issue #7855 | how deterministic subflows are enforced in LangGraph workflows |
| 147 | H5 inside (ПО ХОДУ) | anthropic/claud PreCompact hook not triggered issue #13572 external validator | discussion of PreCompact hook failure and external validation options |
| 148 | H5 workaround (ПО ХОДУ) | Awesome-Agent-Failure-Diagnosis-and-Mitigation quality gates fail‑closed pattern | patterns for independent code verification and fail‑closed quality gates |
| 149 | H5 others (ПО ХОДУ) | Letta memory external state verification receipt pattern | как добавить внешнюю проверку состояния памяти Letta с квитанциями |
| 150 | H5 forbidden (ПО ХОДУ) | forbidden LLM self‑verification without external receipt flag | официальные запреты и рекомендации по использованию самопроверки без квитанций |
| 151 | H6 break (ПО ХОДУ) | GitHub issue #8421 in LangGraph about "policy_override" flag causing repeated "complete the task" prompts | details of policy_override flag behavior |
| 152 | H6 forbidden (ПО ХОДУ) | Claude 3 error code 5045: "Repeated request to finish" policy violation | описание ошибки и рекомендации |
| 153 | H6 inside (ПО ХОДУ) | AutoGPT issue #7310: unexpected loop when user says "just finish" | analysis of loop trigger |
| 154 | H6 workaround (ПО ХОДУ) | Mem0 policy enforcement example for "stop after 3 prompts" | sample code snippet |
| 155 | H6 others (ПО ХОДУ) | OpenAI function calling policy flag "allow_finish" conflict with system instruction | policy hierarchy explanation |
| 156 | H6 inside (ПО ХОДУ) | LangChain memory trim issue #1994: system messages not removed after 10 turns | fix for memory trimming |
| 157 | H6 forbidden (ПО ХОДУ) | Claude API error 403.2: "User requested policy override" | что значит ошибка и как исправить |
| 158 | H7 inside (ПО ХОДУ) | GitHub issue #4279 Claude 3.5 Sonnet token limit 4096 vs 8192 | details of the token‑limit discrepancy discussion |
| 159 | H7 inside (ПО ХОДУ) | GitHub issue #54254 handover user‑curated session hand‑off feature | implementation details of the /handover endpoint |
| 160 | H7 break (ПО ХОДУ) | "Claude Code ignores user rules across contexts" bug error message | identify root cause and reproduction steps |
| 161 | H7 break (ПО ХОДУ) | Server‑side compaction causing rule loss in Claude Code v>2 | как компакция влияет на сохранность правил |
| 162 | H7 workaround (ПО ХОДУ) | Mem0 persistent memory integration example for Claude Code rule retention | step‑by‑step guide to keep rules with Mem0 |
| 163 | H7 forbidden (ПО ХОДУ) | Запрещено ли использовать внешние файлы правил в официальной документации Claude? | официальная позиция Anthropic о внешних файлах правил |
| 164 | H7 others (ПО ХОДУ) | How to use the /handover endpoint in Claude Code (github.com/anthropic/claude-code) | usage syntax and examples for handover API |
| 165 | NEG break (ПО ХОДУ) | GitHub issue #4523 Claude Code rule engine crashes after memory compaction | details of crash and reproduction steps |
| 166 | NEG inside (ПО ХОДУ) | Letta v2.3 flag IGNORE_RULES unexpected behavior in Arena Agent Mode | how flag affects rule enforcement |
| 167 | NEG break (ПО ХОДУ) | Mem0 issue #78 rule persistence lost on agent restart | root cause and fix status |
| 168 | NEG inside (ПО ХОДУ) | LangGraph issue 1019 rule context not propagated to sub‑graphs | why sub‑graph loses rules |
| 169 | NEG forbidden (ПО ХОДУ) | Anthropic policy flag RULE_COMPRESSION_DISABLED documentation | official stance on rule compression |
| 170 | NEG workaround (ПО ХОДУ) | RuleGuard open‑source project external compliance layer for Claude agents | implementation approach and usage |
| 171 | OSS break (ПО ХОДУ) | PromptArmor github issue 45 false negative on rule‑injection detection | details of false negative bug and mitigation steps |
| 172 | OSS inside (ПО ХОДУ) | Claude Code Compliance API persistent_rules flag error 502 response | official docs and known causes of 502 errors |
| 173 | OSS workaround (ПО ХОДУ) | Mem0 issue #78 context loss after model switch in LangChain integration | community‑provided fix or temporary workaround |
| 174 | OSS others (ПО ХОДУ) | Subconscious Cache LRU re‑inject truncated rules bug report | description of bug and any patches |
| 175 | OSS inside (ПО ХОДУ) | AGENTS.md flag RULE_NO_NUMBERS missing checksum verification error message | точный текст ошибки и способы её устранения |
| 176 | OSS forbidden (ПО ХОДУ) | CISA June 22 2026 vulnerability LLM rule‑enforcement bypass CVE‑2026‑XXXXX | exploit details and mitigation recommendations |
