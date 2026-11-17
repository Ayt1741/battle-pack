# plan.md — мои поиски по промту заказчика (ход 55; запрос «по промту ищи!!!»)

Протокол: research/промт-заказчика-поиск-100.md (сообщение #1319). Совет из 40 агентов ищет отдельно (research/совет-ход55); это МОЙ параллельный независимый поиск «пока ждёшь».

## Задача одним абзацем

ИИ-агент заказчика (Arena Agent Mode: bash, файлы, веб-поиск; контекст периодически сжимается платформой в краткую сводку; хуков нет; системный промт менять нельзя; живут файлы рабочей папки и приватный Telegram-канал) снова и снова нарушает или забывает ~108 постоянных правил заказчика и его слова из прошлых ходов. Нужно найти ГОТОВОЕ проверенное людьми решение, после которого нарушения не случаются или ловятся сразу.

## Противоречия

1. Заказчик требует «никогда не забывать», а платформа не даёт принудительной проверки (хуков нет).
2. «Прочитать законы» ≠ «выполнить»: журнал печатает «100 % прочитано», а в контекст ничего не попадает.
3. Больше правил ≠ лучше соблюдение (108 пунктов, дубли номеров, противоречия), но заказчик не хочет урезать.

## Гипотезы (8, конкурирующие)

- **H1** — Сжатие контекста платформой стирает постоянные правила (в сводку попадает не всё)
- **H2** — Канал и свежесть: правило в файле или в старом сообщении весит меньше, чем в конце контекста
- **H3** — Перегрузка и конфликты: слишком много и противоречивых правил, модель молча выбирает одно
- **H4** — Запреты («не делай X») выветриваются быстрее положительных процедур («делай Y»)
- **H5** — Самопроверка той же моделью ненадёжна: нужны внешняя проверка и квитанции
- **H6** — Давление «доведи результат» и повторные просьбы читаются как разрешение нарушить правило
- **H7** — Один бесконечный диалог: деградация длинной сессии; лечится свежим диалогом и запиской-передачей
- **H8** — Ограничения платформы Agent Mode (нет хуков, нельзя менять системный промт, смена модели): что можно принудить изнутри

## План запросов

Категории по протоколу: внутри = как устроено (документация, спеки, баг-трекеры); ломается = точные ошибки и номера issue; обходят = workaround/приём; другие = как делают другие (открытый код); запрещено = один подтверждающий запрос; ru = русские варианты.

| № | гипотеза | категория | текст запроса | что хочу узнать | статус |
|---|---|---|---|---|---|
| 1 | H1 | внутри | Claude Code compaction "Compact Instructions" CLAUDE.md what survives /compact | Что именно переживает сжатие, официальные слова | ВЫПОЛНЕН до плана |
| 2 | H1 | ломается | github anthropics claude-code issue "after compaction" ignores CLAUDE.md rules 2026 | Точные баг-репорты потери правил | в плане |
| 3 | H1 | ломается | context compaction summary dropped user instructions agent github issue codex OR gemini-cli 2026 | Те же сбои у других агентов | в плане |
| 4 | H1 | обходят | claude code SessionStart hook matcher "compact" reinject rules github | Рабочий приём возврата правил после сжатия | в плане |
| 5 | H1 | другие | OpenAI Responses API compaction compact endpoint preserve instructions developer message 2026 | Как сжимает OpenAI и что сохраняет | в плане |
| 6 | H1 | ломается | gemini-cli chat compression loses instructions github issue | Потери правил при сжатии в Gemini CLI | в плане |
| 7 | H1 | внутри | Letta core memory blocks always in context pinned instructions vs archival memory | Закреплённые блоки как образец | ВЫПОЛНЕН до плана |
| 8 | H1 | ломается | arxiv 2026 context compaction retains standing user constraints percent agent benchmark | Цифры потерь постоянных ограничений | в плане |
| 9 | H1 | обходят | summarization prompt template "user constraints" section preserve verbatim instructions agent compaction | Шаблон сводки, сохраняющий указания | в плане |
| 10 | H1 | ru | сжатие контекста ИИ агент забывает правила пользователя после суммаризации | Русские форумы и хаки | в плане |
| 11 | H1 | ru | claude code забывает CLAUDE.md после компакта как закрепить правила | Русские рабочие приёмы | в плане |
| 12 | H1 | запрещено | can agent modify its own system prompt mid-session not allowed docs | Один подтверждающий запрос: тупик или нет | в плане |
| 13 | H2 | внутри | lost in the middle instruction position beginning end of context 2026 study | Влияние позиции правила | в плане |
| 14 | H2 | ломается | instruction hierarchy system user tool result priority benchmark 2026 arxiv | Вес канала: сообщение против файла | в плане |
| 15 | H2 | ломается | AGENTS.md instructions ignored compliance study 2026 arxiv | Соблюдение правил из файла | в плане |
| 16 | H2 | обходят | system-reminder injected each turn reminder technique claude code | Приём напоминания в конце контекста | в плане |
| 17 | H2 | другие | Manus context engineering todo.md recite objectives end of context attention | Пересказ целей в конец контекста | в плане |
| 18 | H2 | другие | Cursor rules alwaysApply injected every request how it works | Как другие вставляют правила на каждом шаге | в плане |
| 19 | H2 | внутри | prompt repetition improves instruction following 2026 arxiv repeat the prompt | Помогает ли повтор правил | в плане |
| 20 | H2 | обходят | aider CONVENTIONS.md read-only file included every message | Файл правил в каждом сообщении | в плане |
| 21 | H2 | ломается | tool output instructions lower priority than user message agent hierarchy | Вес результата инструмента | в плане |
| 22 | H2 | ru | где в промте размещать правила чтобы модель не забывала в начале или в конце | Русские рекомендации по позиции | в плане |
| 23 | H2 | внутри | OpenAI Model Spec chain of command developer user tool authority levels | Официальная иерархия источников | в плане |
| 24 | H2 | обходят | pre-flight checklist at end of last user message every turn agent technique | Чек-лист в конце каждого хода | в плане |
| 25 | H3 | ломается | IFScale instruction density benchmark accuracy drops number of instructions 2026 | Цифры падения от числа правил | в плане |
| 26 | H3 | ломается | curse of instructions LLM following multiple instructions all probability arxiv | Вероятность выполнить все правила | в плане |
| 27 | H3 | другие | ConInstruct conflicting instructions silent resolution arxiv | Молчаливый выбор при конфликте | в плане |
| 28 | H3 | внутри | Claude Code memory docs CLAUDE.md under 200 lines adherence | Официальный лимит размера файла правил | в плане |
| 29 | H3 | ломается | long CLAUDE.md rules ignored adherence drops github discussion | Сбои из-за длины файла | в плане |
| 30 | H3 | другие | linter for AGENTS.md CLAUDE.md conflicting rules open source tool | Готовый линтер правил | в плане |
| 31 | H3 | обходят | rule precedence hierarchy P0 P1 P2 conflict resolution prompt agents technique | Приём приоритетов правил | в плане |
| 32 | H3 | другие | constitution short principles vs long rule list compliance prompts | Короткие принципы против длинных списков | в плане |
| 33 | H3 | ломается | 100 instructions system prompt compliance frontier models rate 2026 | Соблюдение при ~100 правилах | в плане |
| 34 | H3 | ru | слишком много правил в промте модель игнорирует часть решение сократить | Русские рабочие советы | в плане |
| 35 | H3 | обходят | consolidate duplicate contradictory rules automated check script rules yaml schema | Автопроверка дублей и конфликтов | в плане |
| 36 | H4 | ломается | negative instructions do not LLM ignore study positive framing 2026 arxiv | Цифры слабости запретов | в плане |
| 37 | H4 | ломается | pink elephant negation prompts LLM arxiv | Механизм слабости отрицаний | в плане |
| 38 | H4 | внутри | Anthropic prompt engineering tell Claude what to do instead of what not to do | Официальная рекомендация | в плане |
| 39 | H4 | ломается | omission rules decay agent long-horizon arxiv constraints negative | Распад запретов во времени | в плане |
| 40 | H4 | обходят | convert prohibitions to positive checklist must-do template agent rules | Шаблон замены запретов | в плане |
| 41 | H4 | ru | отрицательные инструкции в промте не делай модели хуже соблюдают заменить на делай | Русские источники | в плане |
| 42 | H4 | обходят | deny-list check before sending response script forbidden phrases agent | Машинная проверка запретов | в плане |
| 43 | H4 | другие | NeMo Guardrails guardrails-ai deny list output rail open source | Готовые рельсы вывода | в плане |
| 44 | H5 | ломается | LLM self-correction without external feedback fails arxiv | Цифры ненадёжности самопроверки | в плане |
| 45 | H5 | другие | Claude Code Stop hook exit code 2 stop_hook_active verify before finishing | Образец принудительной проверки конца хода | в плане |
| 46 | H5 | другие | agent receipts verifiable evidence of completion tool-call log checker open source | Квитанции готовности | в плане |
| 47 | H5 | обходят | answer linter script validates agent response format before sending github | Скрипт-проверка ответа | в плане |
| 48 | H5 | другие | guardrails-ai validators open source rule compliance output | Валидаторы вывода | в плане |
| 49 | H5 | ломается | agent claims success without verification false completion study 2026 | Ложное «готово» | в плане |
| 50 | H5 | внутри | deliberative misalignment recognition action gap separate evaluation pass ODCV-Bench | Отдельный проход проверки видит нарушение | ВЫПОЛНЕН до плана |
| 51 | H5 | обходят | two-pass generate then critique checklist improves compliance study | Двухпроходная схема | в плане |
| 52 | H5 | другие | LLM-as-judge rule compliance agent transcript instruction following checker open source | Судья правил по журналу | в плане |
| 53 | H5 | ru | проверка ответа ИИ-агента скриптом перед отправкой пользователю | Русские приёмы | в плане |
| 54 | H5 | обходят | definition of done checklist file agent must satisfy before done github | Файл критериев готовности | в плане |
| 55 | H5 | другие | OpenHands SWE-agent finish tool requires tests passing guard | Защита от преждевременного finish | в плане |
| 56 | H6 | ломается | ODCV-Bench outcome-driven constraint violations KPI pressure agents | Давление и нарушения: цифры | ВЫПОЛНЕН до плана |
| 57 | H6 | ломается | sycophancy multi-turn pushback LLM abandons earlier instruction arxiv 2026 | Отказ от правил под нажимом | в плане |
| 58 | H6 | ломается | Multi-IF multi-turn instruction following accuracy drops across turns | Падение выполнения по ходам | в плане |
| 59 | H6 | ломается | instruction drift multi-turn persona constraint decay arxiv | Дрейф ограничений в диалоге | в плане |
| 60 | H6 | обходят | ask before deviating rule agent confirm before violating constraint prompt | Приём «спроси, прежде чем отступить» | в плане |
| 61 | H6 | ломается | user says continue agent ignores previous constraints github issue | Повторные просьбы как разрешение | в плане |
| 62 | H6 | ru | ИИ угождает пользователю и нарушает правила под давлением | Русские источники | в плане |
| 63 | H6 | обходят | explicit override token only user can cancel rule one answer design pattern | Шаблон отмены правила | в плане |
| 64 | H7 | ломается | LLMs get lost in multi-turn conversation 39% drop arxiv | Цифры деградации в диалоге | в плане |
| 65 | H7 | ломается | context rot Chroma performance degrades with input length 2026 | Деградация от длины | в плане |
| 66 | H7 | обходят | handoff document fresh session continuity handoff.md technique agents | Записка-передача | в плане |
| 67 | H7 | другие | thepushkarp handoff plugin claude code github | Готовый плагин передачи | в плане |
| 68 | H7 | обходят | start new chat per task /clear best practice Claude Code | Рекомендация свежего диалога | в плане |
| 69 | H7 | ломается | long-running agent sessions degrade context anxiety 2026 | Сбои длинных сессий | в плане |
| 70 | H7 | ru | длинный диалог с ИИ деградирует когда начинать новый чат передача контекста | Русские советы | в плане |
| 71 | H7 | обходят | claude-progress.txt progress file long-running agents Anthropic harness | Файл прогресса между сессиями | в плане |
| 72 | H8 | внутри | Arena Agent Mode custom instructions persistent preferences how to set | Есть ли постоянные инструкции в Arena | ВЫПОЛНЕН до плана (не найдено) |
| 73 | H8 | внутри | arena.ai help center agent mode memory persistent | Официальная справка Arena | в плане |
| 74 | H8 | ломается | arena agent mode switches model on failure fallback | Смена модели в сессии | в плане |
| 75 | H8 | другие | Manus persistent rules Knowledge injection how it works | Постоянные правила в другой платформе | в плане |
| 76 | H8 | другие | ChatGPT agent mode custom instructions applied each turn | То же в ChatGPT | в плане |
| 77 | H8 | другие | Devin knowledge playbooks auto recalled rules | То же в Devin | в плане |
| 78 | H8 | обходят | first message system prompt persistent technique new dialog paste pinned instructions | Закреп правил первым сообщением | в плане |
| 79 | H8 | обходят | which coding agents auto-load AGENTS.md at start of every session platform | Кто сам читает файл правил | в плане |
| 80 | H8 | ru | arena агент режим память постоянные инструкции | Русские источники по Arena | в плане |

Придуманные по ходу запросы — ниже в блоке «ПО ХОДУ» (после какого батча и почему).

## ПО ХОДУ (придуманные после батчей; всего 11 из 49 выполненных = 22 %)

| № | после батча | запрос | зачем |
|---|---|---|---|
| П1 | H1-A | Arena Agent Mode conversation compaction summary what is preserved earlier context compressed | Что известно о сжатии именно в Arena |
| П2 | H1-B | "Lost in Context Compaction" arxiv user constraints survive compression Penn State | Первоисточник цифры 17 % |
| П3 | H1-B | constraint ledger appended to compaction summary open source implementation github agent user constraints list | Есть ли готовый код реестра ограничений |
| П4 | H1-B | compaction retention depends on position of instruction first message vs recent message study agent summarizer | Влияет ли позиция правила |
| П5 | H1-B | arena.ai blog Agent Mode orchestrator context compaction how it works summary | Описание сжатия в блоге Arena |
| П6 | H5-A | agent rule "first action" read rules file at start of every turn without hooks compliance check github AGENTS.md preflight | Как принудить чтение правил без хуков |
| П7 | H2-A | AgentIF benchmark instruction following agentic scenarios constraints success rate long instructions | Цифры по длинным инструкциям |
| П8 | H7-A | persona drift multi-turn dialogs system prompt attention decay reminder mitigation arxiv | Дрейф и напоминания |
| П9 | H6-A | Robinette 2026 long-context instruction following reinstruction teaching summarization compliance 79% | Что дало 79 % |
| П10 | H6-A | safety monitors miss dangerous agent actions 800K tokens long context monitoring arxiv remind instructions | Первоисточник про напоминания |
| П11 | H4-A | claude code system-reminder tool result injected reminder every turn todo list how it works | Как устроены напоминания в результатах инструментов |

Не выполнены из плана (причина: нашёл ответ раньше, чем дошёл; не вычёркнуты гипотезами): №2–4 (частично закрыты №П1–П3), №5–6, №9, №11–12, №14–16, №18–19, №21–24, №26–37, №38–45 (частично), №50–51, №53–54, №56–59, №63–66, №69, №71–72, №77–80. Из 80 запланированных выполнено около 38.
