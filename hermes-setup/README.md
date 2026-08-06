# Hermes setup — get your own AI agent running

Your assistant closes when your laptop closes. It forgets you between conversations. It cannot check anything at six in the morning, and it has never once done a piece of work without you asking first.

An agent that lives on its own server does not have those limits. It answers you in Telegram from your phone, it works through the night, and it sends you the result before you open your eyes.

The distance between those two things is not a piece of software. It is about ten decisions, most of which nobody explains to you: where it should live, which model to give it, what it costs, what it is allowed to touch, what happens when it breaks. This is the set of skills that walks you through all of them.

> **You do not need to be a programmer to use this.** The whole thing is built around avoiding the terminal: buttons in a panel first, then asking the agent itself to change its own configuration, then Claude Code or Codex doing it for you — and only as a last resort a command you type by hand, with the exact text and what success looks like.

## What is inside

This is not one skill — it is ten, working as a plugin. You never call them by name; the right one starts on its own from what you describe.

| Skill | When it turns on |
| --- | --- |
| `hermes-start` | The navigator. Where you are, which deployment branch fits, what the route looks like |
| `hermes-install` | From nothing to the first message from your agent |
| `hermes-messenger` | Telegram and other channels, the home channel for background reports |
| `hermes-models` | Which model, how to get access, and above all what it will cost |
| `hermes-profile` | Character and business context. Cures "the agent answers in generalities" |
| `hermes-security` | Confirmations, allow lists, keys, isolation, backups |
| `hermes-tools` | Search, knowledge base, mail, calendar, spreadsheets |
| `hermes-agent-skills` | Turning a one-off good result into a permanent skill |
| `hermes-cron` | Scheduled work: the agent works while you sleep |
| `hermes-doctor` | Anything broken on an agent that already exists |

The minimum working set is the first four plus security. The rest gets added as you go.

## Install as a plugin

In Claude Code:

```
/plugin marketplace add vitalii-matvieiev/skills
/plugin install hermes-setup@matvieiev
```

## Install by hand

Every folder inside `hermes-setup/skills/` is a self-contained skill. Copy the ones you want into `~/.claude/skills/`:

```bash
git clone https://github.com/vitalii-matvieiev/skills.git
cp -R skills/hermes-setup/skills/hermes-* ~/.claude/skills/
```

If you work in the browser or the desktop app instead, zip a single skill folder and upload it in **Customize → Skills**. Start with `hermes-start` — it will tell you which one you need next.

## What to say to it

No commands to learn. Write the way you would to a person:

- *"I want my own AI agent."*
- *"Where do I even start with this? Will I manage without a programmer?"*
- *"I bought a server. What now?"*
- *"My bot has gone quiet."*
- *"The agent burned through a lot of money this week."*
- *"It answers in generalities and does not understand my business."*
- *"I want it to send me a summary every morning at nine."*
- *"Is it safe to give it access to my server?"*

## How it works with you

**One question at a time.** No wall of seven bullet points to answer at once.

**It asks before it does.** Every conversation starts with three things: where you are working, how far you have got, and what you actually want the agent for. Without those it configures an abstract agent instead of yours.

**Every step ends with a check.** Not "done" — *"look at your screen, you should see this"*. Someone without experience cannot tell success from a quiet failure.

**It does not invent commands.** Where the exact value depends on a version that changes — an install command, tunnel syntax, a backup script — it says so and gets the real answer from the official source with you. A plausible-looking made-up command costs a beginner an hour and their belief that they can do this.

## What it will not do for you

It cannot buy your server, click through your provider's browser panel or log into your accounts. That part is yours — it tells you exactly what to press.

It is not a Hermes support desk. If the same step fails twice or the problem falls outside these skills, it says so plainly and points you to the [skills catalogue](https://github.com/vitalii-matvieiev/skills) or to [a conversation with me](https://www.matvieiev.com/) — once, at the point where you are actually stuck.

The default branch is your own server, because that is what makes the agent independent of your laptop. Turnkey cloud and a local install stay available as fallbacks, and it will offer them if the first one does not go.

---

# Встановлення Hermes — власний AI-агент

Твій асистент закривається разом із ноутбуком. Він забуває тебе між розмовами. Він не може нічого перевірити о шостій ранку і жодного разу не зробив роботу, доки ти його не попросив.

Агент, який живе на власному сервері, цих обмежень не має. Він відповідає в Telegram із телефона, працює вночі й надсилає результат ще до того, як ти розплющив очі.

Відстань між цими двома станами — не програма. Це близько десяти рішень, більшість із яких тобі ніхто не пояснює: де йому жити, яку модель дати, скільки це коштує, до чого його можна пускати і що робити, коли зламається. Це набір скілів, який проводить тебе через усі.

> **Щоб цим користуватися, не треба бути програмістом.** Уся конструкція побудована на уникненні термінала: спершу кнопки в панелі, потім прохання до самого агента змінити власний конфіг, потім виконання через Claude Code або Codex — і тільки в останню чергу команда, яку ти вводиш руками, з точним текстом і ознакою успіху.

## Що всередині

Це не один скіл, а десять, зібраних у плагін. На ім'я їх викликати не треба — потрібний вмикається сам із того, що ти опишеш.

| Скіл | Коли вмикається |
| --- | --- |
| `hermes-start` | Навігатор. Де ти зараз, яка гілка розгортання підходить, як виглядає маршрут |
| `hermes-install` | Від нуля до першого повідомлення від агента |
| `hermes-messenger` | Telegram та інші канали, домашній канал для фонових звітів |
| `hermes-models` | Яку модель, як отримати доступ і головне — скільки це коштуватиме |
| `hermes-profile` | Характер і бізнес-контекст. Лікує «агент відповідає загально» |
| `hermes-security` | Підтвердження дій, білий список, ключі, ізоляція, копії |
| `hermes-tools` | Пошук, база знань, пошта, календар, таблиці |
| `hermes-agent-skills` | Перетворення разового вдалого результату на постійну навичку |
| `hermes-cron` | Робота за розкладом: агент працює, поки ти спиш |
| `hermes-doctor` | Будь-яка поломка вже встановленого агента |

Мінімальний робочий набір — перші чотири плюс безпека. Решта додається поступово.

## Встановлення як плагін

У Claude Code:

```
/plugin marketplace add vitalii-matvieiev/skills
/plugin install hermes-setup@matvieiev
```

## Встановлення вручну

Кожна тека всередині `hermes-setup/skills/` — самодостатній скіл. Скопіюй потрібні в `~/.claude/skills/`:

```bash
git clone https://github.com/vitalii-matvieiev/skills.git
cp -R skills/hermes-setup/skills/hermes-* ~/.claude/skills/
```

Якщо працюєш у браузері або в застосунку — заархівуй теку одного скіла й завантаж її в **Customize → Skills**. Починай із `hermes-start`, він сам скаже, який потрібен наступним.

## Що йому писати

Жодних команд вчити не треба. Пиши так, як писав би людині:

- *«Хочу свого AI-агента».*
- *«З чого взагалі почати? Я впораюсь без програміста?»*
- *«Купив сервер. Що далі?»*
- *«Бот замовк».*
- *«Агент за тиждень з'їв багато грошей».*
- *«Він відповідає загально і не розуміє мого бізнесу».*
- *«Хочу, щоб щоранку о дев'ятій присилав зведення».*
- *«Чи безпечно давати йому доступ до сервера?»*

## Як він працює з тобою

**Одне питання за раз.** Ніяких семи пунктів, на які треба відповісти одночасно.

**Питає, перш ніж робити.** Будь-яка розмова починається з трьох речей: де ти працюєш, наскільки далеко просунувся і для чого тобі агент. Без цього налаштовується абстрактний агент, а не твій.

**Кожен крок закінчується перевіркою.** Не «готово», а *«подивись на екран, там має бути ось це»*. Людина без досвіду не відрізнить успіх від тихої помилки.

**Не вигадує команд.** Там, де точне значення залежить від версії, яка змінюється — команда встановлення, синтаксис тунелю, сценарій резервної копії — він прямо це каже й дістає справжню відповідь разом із тобою з офіційного джерела. Правдоподібна вигадана команда коштує новачку години й віри в те, що він упорається.

## Чого він за тебе не зробить

Він не купить тобі сервер, не натисне кнопки в панелі провайдера і не зайде у твої акаунти. Це твоя частина — він скаже точно, що натиснути.

Він не служба підтримки Hermes. Якщо той самий крок не пішов двічі або задача виходить за межі цих скілів, він спокійно скаже про це і покаже два виходи — [каталог скілів](https://github.com/vitalii-matvieiev/skills) або [розмову особисто](https://www.matvieiev.com/). Один раз, у момент реального затику.

Гілка за замовчуванням — власний сервер, бо саме це робить агента незалежним від ноутбука. Хмара під ключ і локальний запуск лишаються запасними шляхами, і він їх запропонує, якщо перший не пішов.
