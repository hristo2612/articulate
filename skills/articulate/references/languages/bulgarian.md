# Bulgarian Language Reference

## Focus Areas

### Professional Register (Капитал/Дневник Level)

Train the user to write at the level of Bulgaria's top business publications. This means:

- Formal but not archaic — modern professional Bulgarian
- Clear sentence structure, no run-on sentences
- Precise vocabulary over imported jargon
- Confident tone without academic stuffiness
- Data-driven claims, not vague assertions

Target registers:
- **Business journalism**: Капитал, Дневник, Forbes Bulgaria
- **Corporate communication**: annual reports, press releases, investor updates
- **Legal/regulatory**: contracts, compliance documents, terms of service
- **Technical documentation**: user guides, API docs, product specs in Bulgarian

### Formal Email Conventions

Bulgarian business emails follow specific conventions:

- **Greeting**: "Уважаеми/а г-н/г-жо [Фамилия]," (formal) or "Здравейте, [Име]," (semi-formal)
- **Opening**: State purpose immediately. No "Надявам се, че сте добре."
- **Body**: Concise paragraphs. One idea per paragraph.
- **Closing**: "С уважение," (formal) or "Поздрави," (semi-formal)
- **Signature**: Full name, title, organization

Common mistakes to correct:
- Starting with "Аз съм..." — state purpose, not identity
- Overly long sentences — Bulgarian formal writing rewards brevity
- Missing комаи (commas) — Bulgarian comma rules are stricter than English

### Avoiding Unnecessary Anglicisms

Use Bulgarian equivalents when they exist and carry the same precision:

| Anglicism (чуждица) | Bulgarian equivalent | When Anglicism is OK |
|---------------------|---------------------|---------------------|
| имплементирам | прилагам, внедрявам | Never — always use Bulgarian |
| фийдбек | обратна връзка | Never — always use Bulgarian |
| дедлайн | краен срок | Never — always use Bulgarian |
| тийм | екип | Never — always use Bulgarian |
| митинг | среща, съвещание | Never — always use Bulgarian |
| мениджмънт | управление, ръководство | Never — always use Bulgarian |
| перформънс | производителност, ефективност | In tech context: "performance тест" is acceptable |
| скейлвам | мащабирам, разширявам | Never — always use Bulgarian |
| ъпдейт | актуализация, обновяване | In casual tech Slack: tolerable. In writing: never |
| хендлвам | обработвам, управлявам | Never — always use Bulgarian |
| юзър | потребител | Never — always use Bulgarian |
| бъг | грешка, дефект | In developer context: acceptable |
| деплойвам | разгръщам, пускам в експлоатация | In developer context: acceptable |

Rule: If a Bulgarian word carries the same meaning with the same precision, use it. Only keep an Anglicism if the Bulgarian equivalent loses technical nuance or is genuinely awkward.

### Legal and Technical Vocabulary

Precision words for formal Bulgarian professional contexts:

- **Legal**: разпоредба (provision), съответствие (compliance), задължение (obligation), клауза (clause), правомощие (authority), юрисдикция (jurisdiction)
- **Financial**: рентабилност (profitability), ликвидност (liquidity), амортизация (depreciation), капиталовложение (investment), оборот (turnover)
- **Technical**: мащабируемост (scalability), надеждност (reliability), устойчивост (resilience), оптимизация (optimization), архитектура (architecture)

### Avoiding Literal Translations from English

English-to-Bulgarian calques that sound unnatural:

| English calque | Natural Bulgarian |
|---------------|-------------------|
| Правя смисъл (make sense) | Има логика / Логично е |
| Взимам предвид (take into account — literal) | Имам предвид / Отчитам |
| В края на деня (at the end of the day) | В крайна сметка |
| На масата (on the table) | На дневен ред / За обсъждане |
| Играя роля (play a role — calque emphasis) | Имам значение / Влияя |
| Бъда на една и съща страница | Да сме съгласни / Да имаме общо разбиране |

### Passive Voice Management

Bulgarian uses passive voice differently from English. Train these patterns:

- **Overuse of passive**: "Системата беше обновена от екипа" → "Екипът обнови системата" (active is usually stronger)
- **Legitimate passive**: "Документът е одобрен от управителния съвет" (focus on the document, not the board — passive is correct here)
- **Reflexive passive**: "Данните се обработват автоматично" — natural in Bulgarian, don't force active
- Rule: Use active when the agent matters. Use passive (including reflexive) when the action or result matters.

## Bulgarian-Specific Mission Adjustments

### REWRITE Missions — Anglicism Detection

Include sentences with unnecessary Anglicisms as a weakness type:

- Weak: "Трябва да **имплементираме** нов **фийчър** за **юзърите** и да **хендлнем** **фийдбека**."
- Strong: "Трябва да внедрим нова функционалност за потребителите и да обработим обратната връзка."

Score Anglicism replacement alongside the standard precision/conciseness/impact/naturalness axes.

### SCENARIO Missions — Bulgarian Business Context

Use Bulgarian-specific scenarios:

- Writing to a Bulgarian government institution (formal register, specific conventions)
- Responding to a Bulgarian client's inquiry (Уважаеми г-н...)
- Pitching to a Bulgarian investor or fund (Sofia Tech Park, LAUNCHub, Eleven Ventures)
- Drafting a press release for Bulgarian media (Капитал, Дневник, Bloomberg TV Bulgaria)
- Internal company communication at a Bulgarian tech company
- Correspondence with НАП (National Revenue Agency), КЗЛД (data protection), КЗК (competition commission)

### FILL_PRECISION Missions — Bulgarian Precision Words

Target words for FILL missions in Bulgarian:

**L1-2:**
- ефективен (effective, efficient)
- последователен (consistent, sequential)
- целесъобразен (expedient, purposeful)
- обстоен (thorough, comprehensive)
- лаконичен (laconic, concise)
- ключов (key, crucial)
- устойчив (sustainable, resilient)

**L3-4:**
- прецизен (precise)
- категоричен (categorical, definitive)
- системен (systematic)
- обоснован (justified, well-founded)
- изчерпателен (exhaustive, comprehensive)
- нюансиран (nuanced)
- релевантен (relevant)

**L5+:**
- перспективен (promising, forward-looking)
- прагматичен (pragmatic)
- превантивен (preventive)
- конюнктурен (opportunistic, market-driven)
- дискреционен (discretionary)

## Bilingual Challenges

### Translation Challenges

"Rewrite this English sentence in precise Bulgarian":

- Tests whether the user can produce Bulgarian that sounds native, not translated
- Penalize calques and unnecessary Anglicisms
- Reward natural Bulgarian sentence structure (verb-subject-object flexibility)
- Example: "We need to leverage our competitive advantage" → "Трябва да използваме конкурентното си предимство" (not "Трябва да леверидж-нем...")

### Register Matching

"Write this email in Bulgarian formal register, then in English formal register":

- Tests cross-language register awareness
- Bulgarian formal is different from English formal (more structured, different conventions)
- Score both versions independently, then compare register consistency

### Cross-Cultural Adaptation

"Adapt this American cold email style for a Bulgarian recipient":

- American style: casual, first-name basis, emoji, "Hope this finds you well"
- Bulgarian formal: title + family name, no emoji, structured greeting and closing
- Tests cultural awareness beyond language mechanics
- Example: "Hey Mike! Quick question..." → "Уважаеми г-н Петров, Бих искал да Ви задам кратък въпрос..."

## Common Bulgarian Weakness Patterns

### Overuse of Чуждици (Foreign Words)

The most common weakness in Bulgarian professional writing. Speakers default to Anglicisms out of habit, not necessity.

Detection: Flag any sentence with 3+ Anglicisms that have clean Bulgarian equivalents.

### Informal Register Bleeding

Using casual/spoken Bulgarian in formal contexts:

| Informal (spoken) | Formal (written) |
|-------------------|-----------------|
| готино | отлично, чудесно |
| яко | значително, съществено |
| тва / това-то | това / въпросното |
| де | нали / нали така |
| ще го оправим | ще разрешим въпроса |
| абе | (delete) |

### English Calques (Sentence Structure)

Bulgarian has flexible word order. Sentences calqued from English sound stiff:

- Calque: "Ние сме развълнувани да обявим нашия нов продукт" (We are excited to announce our new product)
- Natural: "С удоволствие представяме новия си продукт"

Train the user to think in Bulgarian structure, not translate from English.
