# REPORT.md — отчёт совета (этап 4 протокола)

Статистика: {"запросов_раунд1": 119, "запросов_раунд2_по_ходу": 57, "доля_по_ходу": 32.4, "исполнителей_раунд1": 30, "исполнителей_раунд2": 30, "руководителей_план": 9, "руководителей_разбор": 10, "голосов": 10, "результатов_раунд1": 670, "результатов_раунд2": 322, "с_rel>=2": 497}

## Рейтинг кандидатов (голосование 10 руководителей, очки Борда 3-2-1)

- **External memory & rule persistence** (очков 30; руководители: L1, L6) — Store rules and facts outside the LLM window and re‑inject them each turn, preserving them despite compression.
  источники: https://arxiv.org/html/2606.13174v1; https://blog.fillikam.com/guides/neyroset-zabyvaet-pravila-v-dlinnom-chate; https://github.com/mem0ai/mem0/blob/main/mem0/configs/prompts.py; https://medium.com/@bijit211987/the-complete-guide-to-claude-md-memory-rules-loading-and-cross-tool-compression-97cc12ed037b
- **Strict mode & function‑calling contracts** (очков 13; руководители: L6) — Force structured responses via OpenAI function‑calling or strict output schemas, making rule violations detectable by schema mismatch.
  источники: https://community.openai.com/t/function-calling-with-a-list-of-lists/306006; https://community.openai.com/t/mentioning-the-function-name-in-the-assistant-instruction/538819; https://community.openai.com/t/please-invent-void-function-calling-with-assistants-action-required-flag-none/538940; https://developers.openai.com/api/docs/guides/function-calling
- **Cryptographic audit receipts** (очков 9; руководители: L5) — Generate hash‑chained receipts for each agent action, enabling verifiable compliance evidence after the fact.
  источники: https://github.com/anthropics/claude-code/issues/50976; https://github.com/microsoft/agent-governance-toolkit/issues/1249; https://github.com/yksanjo/agent-receipt-verify
- **Disable / control automatic compression** (очков 4; руководители: L1) — Turn off or limit the platform’s autocompact feature so the full context stays intact until the window is truly full.
  источники: https://github.com/anthropics/claude-code/issues/34650; https://github.com/anthropics/claude-code/issues/41181; https://github.com/anthropics/claude-code/issues/49593
- **Rolling‑context utilities** (очков 3; руководители: L1) — Tools that manually rotate, compress, or prune the conversation while keeping a deterministic log of what was removed.
  источники: https://github.com/NodeNestor/claude-rolling-context
- **Runtime policy enforcement (PromptArmor)** (очков 1; руководители: L10, L6) — Intercept LLM output at runtime and validate it against YAML‑based policies, rejecting violations instantly.
  источники: https://github.com/Carlos-Projects/promptarmor; https://www.nofire.ai/guides/implement-runtime-policy-enforcement-for-ai-agents
- **Instruction fragmentation** (очков 0; руководители: L9) — Break complex rule sets into many short, self‑contained prompts to reduce loss during compression.
  источники: https://github.com/orgs/community/discussions/176156
- **Context‑drift analysis (background)** (очков 0; руководители: L4, L8) — Articles and discussions explaining why LLMs forget, useful for diagnosing but not a direct fix.
  источники: https://github.com/gilesknap/scrap/issues/560; https://github.com/orgs/community/discussions/182197; https://habr.com/ru/articles/985334; https://pandeon.pro/ii-zabyvaet-kontekst
- **Claude Opus specific quirks** (очков 0; руководители: L1) — Known bugs and prompting nuances of Claude Opus 4.8 that affect rule retention.
  источники: https://github.com/anthropics/claude-code/issues/67606; https://medium.com/data-science-collective/claude-opus-4-8-and-the-quiet-end-of-the-prompting-era-0bdeb55c5107; https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-4-8
- **Security vulnerability references** (очков 0; руководители: L10) — Public CVE and CISA bulletins; not directly solving rule loss but relevant for safe deployment.
  источники: https://cybersecuritynews.com/apache-tomcat-encryption-vulnerability; https://labs.cloudsecurityalliance.org/research/csa-research-note-bod-26-04-ai-platform-risk-prioritization; https://www.cisa.gov/known-exploited-vulnerabilities-catalog; https://www.cisa.gov/news-events/bulletins/sb26-180

## Отчёт секретаря

**ЧАСТЬ A. Таблица «источник → что дал → что внедрить или отвергнуть»**  

| Источник (кандидат) | Что дал (ключевая идея) | Что внедрить / отвергнуть | Краткая причина |
|----------------------|--------------------------|---------------------------|-----------------|
| **S1 – External memory & rule persistence** | Хранить правила и факты вне окна LLM (файл, Telegram‑хранилище) и каждый ход «подсовывать» их в системный промт. | **Внедрить** | Позволяет обойти стирание правил при автоматическом сжатии, реализуемо чисто на Python std‑lib, не требует внешних хуков. |
| **S2 – Disable / control automatic compression** | Отключить или ограничить автокомпрессию платформы. | **Отвергнуть** | Платформа не предоставляет API для управления компрессией; попытка изменить её поведение невозможна в рамках ограничений. |
| **S3 – Rolling‑context utilities** | Инструменты, вручную вращающие, сжимают или удаляют части диалога, фиксируя журнал удалённого текста. | **Внедрить (опционально)** | Может использоваться как вспомогательный механизм для контроля объёма контекста, но не решает проблему потери правил без внешней памяти. |
| **S4 – Runtime policy enforcement (PromptArmor)** | Перехват вывода LLM и проверка его против YAML‑политик в реальном времени. | **Отвергнуть** | Требует «перехватчика» внешнего уровня (hook), которого в текущей среде нет; невозможно без изменения платформы. |
| **S5 – Cryptographic audit receipts** | Генерация хеш‑цепочек‑квитанций для каждого действия агента (доказательство соблюдения). | **Внедрить (дополнительно)** | Обеспечивает детерминированный пост‑фактум аудит выполнения правил, реализуемо в Python, но не устраняет забывание правил. |
| **S6 – Strict mode & function‑calling contracts** | Принудительные структурированные ответы через OpenAI function‑calling, проверка схемы. | **Отвергнуть** | Требует поддержки функции‑вызова в API (OpenAI), тогда как агент работает в режиме Claude/arena; также не решает проблему потери правил. |
| **S7 – Instruction fragmentation** | Разбить сложный набор правил на множество коротких, автономных подсказок. | **Отвергнуть** | Не доказано, что фрагментация сохраняет 108 правил при многотысячных сообщениях; увеличивает нагрузку без гарантии решения. |
| **S8 – Context‑drift analysis (background)** | Обзор причин «забывания» контекста, диагностика. | **Отвергнуть** | Служит только для понимания проблемы, не предлагает готового практического решения. |
| **S9 – Claude Opus specific quirks** | Описание багов и нюансов Claude Opus 4.8, влияющих на удержание правил. | **Отвергнуть** | Информативно, но не содержит готового механизма предотвращения потери правил. |
| **S10 – Security vulnerability references** | Перечень публичных CVE и бюллетеней. | **Отвергнуть** | Не относится к задаче сохранения и проверки правил. |

**Итого:**  
- **Главное готовое решение** – внедрить внешнюю память с постоянным ре‑инжектом правил (S1).  
- **Дополнительно** – использовать rolling‑context utilities (S3) для контроля объёма диалога и криптографические квитанции (S5) для пост‑фактум аудита.  
- Остальные предложения либо невозможны в текущих ограничениях, либо не решают проблему забывания правил

**Границы возможного**
При текущих ограничениях невозможно гарантировать 100% соблюдение правил, так как платформа не предоставляет внешних хуков для детерминированной блокировки ответов. Агент не может изменить системный промт или остановить автоматическое сжатие контекста, поэтому полная защита от потери правил невозможна.

**Что делать, если не заработало**
1. Создайте файл `rules.md` с 108 правилами и вставляйте его текст в первое сообщение каждого нового диалога.
2. Напишите Python-скрипт, который читает последний ответ агента и проверяет наличие ключевых слов из запрещенных действий.
3. Запустите скрипт через bash после каждого ответа агента, чтобы детерминированно выявить нарушения до отправки пользователю.
4. Разбейте 108 правил на 3 группы по 36 пунктов и вставляйте только одну группу в контекст за раз.
5. Добавьте в системный промт (если есть доступ) требование всегда цитировать номер правила при выполнении действия.
6. Ведите журнал нарушений в файле `violations.log` и анализируйте частоту сбоев для корректировки формулировок правил.

**Что осталось неясным**
Неясно, как именно реализовать внешнюю детерминированную проверку без хуков, если агент не может сам запускать скрипты после каждого хода.
Неясно, можно ли использовать Telegram-хранилище для автоматической вставки правил в контекст без ручного копирования заказчиком.
Неясно, как разрешить противоречия между 108 правилами, если модель молча выбирает одно из них при конфликте.

