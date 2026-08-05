# skills

Agent skills for founders, entrepreneurs and creative people who run their work on AI.

> **You do not need to be a programmer to use these.**
> If you use Claude in your browser or the desktop app, installing one takes about two minutes. No terminal, no GitHub account, no code. Instructions right below.

## Install without a terminal

Works on every Claude plan, including the free one.

1. **Download the skill:** [slicing-pie.zip](https://github.com/vitalii-matvieiev/skills/releases/latest/download/slicing-pie.zip)
2. In Claude, open **Customize → Skills**
3. Upload the file and switch the skill on
4. Start a normal chat and describe your situation in plain words

That is it. You never open the file, never read it, never edit anything. Claude does that part.

## Install with a terminal

For Claude Code, Codex, Cursor, OpenCode and 70+ other agents:

```bash
npx skills add vitalii-matvieiev/skills
```

One skill instead of all of them:

```bash
npx skills add vitalii-matvieiev/skills --skill slicing-pie
```

See what is inside before installing:

```bash
npx skills add vitalii-matvieiev/skills --list
```

## What to say once it is installed

You do not call the skill by name and you do not learn any commands. You write the way you would to a person, and Claude picks the right skill itself. For `slicing-pie`, any of these works:

- *"We are three co-founders and I want to recalculate our shares fairly."*
- *"My partner put in $12,000, I work full-time with no salary. What split is fair?"*
- *"We agreed on 50/50 a year ago and it no longer feels right. Help me redo it."*
- *"One of our co-founders is leaving. What happens to their share?"*

Claude will ask what it needs — market salary rates, hours, money spent — and give you a table with percentages, a spreadsheet to keep updating, and the questions your team has not answered yet.

## Skills

| Skill | What it does |
|---|---|
| [slicing-pie](slicing-pie/) | Splits startup equity between co-founders by actual contribution instead of a handshake 50/50. Calculates the split, sets the moment it freezes, and covers what happens when someone walks away. |

More coming: offers, funnels, hiring, agent operations.

## Why these are different

Most skills you can install are a framework somebody read about last week, reformatted into Markdown. These are not that.

Everything here comes out of work I actually did. My own companies — the ones that worked and the ones that did not. The mentors I paid for and argued with. The courses I finished, and the ones I dropped halfway because they were hollow. The books I read, applied, and watched collide with reality until only the usable part was left.

A method becomes a skill in this repository only after it has survived that: run on a real business, with real money and real consequences. Everything that did not survive is not here. That is the entire filter.

So you are not getting a summary of a book. You are getting what was left of it after it went through practice.

— Vitalii Matvieiev · [matvieiev.com](https://www.matvieiev.com) · [LinkedIn](https://www.linkedin.com/in/matvieiev-vitalii/)

## Paid skills

The deeper, more opinionated ones — built from client work and sold separately.

→ [matvieiev.com/matvieiev-store](https://www.matvieiev.com/matvieiev-store)

## Feedback

Used a skill and it handled your case badly? [Open an issue](https://github.com/vitalii-matvieiev/skills/issues) with the prompt you gave it and what you expected instead. That is how these get better.

## License

MIT — use them, fork them, ship them. See [LICENSE](LICENSE).

---

# skills — українською

Скіли для агентів, призначені фаундерам, підприємцям і креативним людям, які будують свою роботу на AI.

> **Щоб цим користуватися, не треба бути програмістом.**
> Якщо ви користуєтесь Claude у браузері або в застосунку, встановлення займе близько двох хвилин. Без терміналу, без акаунта на GitHub, без коду. Інструкція одразу нижче.

## Встановлення без терміналу

Працює на всіх тарифах Claude, включно з безкоштовним.

1. **Завантажте скіл:** [slicing-pie.zip](https://github.com/vitalii-matvieiev/skills/releases/latest/download/slicing-pie.zip)
2. У Claude відкрийте **Customize → Skills**
3. Завантажте файл і увімкніть скіл
4. Почніть звичайний чат і опишіть свою ситуацію простими словами

Це все. Файл не треба відкривати, читати чи редагувати — цим займається Claude.

## Встановлення через термінал

Для Claude Code, Codex, Cursor, OpenCode і ще 70+ агентів:

```bash
npx skills add vitalii-matvieiev/skills
```

Один скіл замість усіх:

```bash
npx skills add vitalii-matvieiev/skills --skill slicing-pie
```

Подивитися, що всередині, перед встановленням:

```bash
npx skills add vitalii-matvieiev/skills --list
```

## Що писати після встановлення

Скіл не треба викликати на ім'я, і жодних команд вчити не потрібно. Ви пишете так, як писали б людині, а Claude сам обирає потрібний скіл. Для `slicing-pie` підійде будь-що з такого:

- *«Нас троє співзасновників, хочу справедливо перерахувати частки»*
- *«Партнер вклав $12 000, я працюю фултайм без зарплати. Як ділити?»*
- *«Рік тому домовились 50 на 50, зараз це виглядає нечесно. Допоможи перерахувати»*
- *«Один зі співзасновників виходить із проєкту. Що робити з його часткою?»*

Claude сам запитає те, що йому потрібно — ринкові ставки, години, вкладені гроші — і видасть таблицю з відсотками, файл для щотижневого обліку та питання, на які ваша команда ще не відповіла.

## Скіли

| Скіл | Що робить |
|---|---|
| [slicing-pie](slicing-pie/) | Ділить частки в стартапі між співзасновниками за реальним внеском, а не за домовленістю «50 на 50 по руках». Рахує розподіл, визначає момент його заморозки й описує, що робити, коли хтось виходить із проєкту. |

Далі будуть: офери, воронки, найм, операційка на агентах.

## Чому вони інші

Більшість скілів, які можна встановити, — це фреймворк, про який хтось прочитав минулого тижня й переклав у Markdown. Тут не так.

Усе, що є в цьому репозиторії, виросло з роботи, яку я справді робив. З моїх власних компаній — і тих, що спрацювали, і тих, що ні. З менторів, яким я платив і з якими сперечався. З курсів, які я закінчив, і тих, які кинув на середині, бо вони виявилися порожніми. З книжок, які я читав, застосовував і дивився, як вони розбиваються об реальність, доки не лишалося те, що дійсно працює.

Метод стає скілом у цьому репозиторії лише після того, як пройшов через це: був застосований у живому бізнесі, з реальними грошима й реальними наслідками. Того, що не витримало перевірки, тут немає. У цьому весь відбір.

Тобто ти отримуєш не переказ книжки. Ти отримуєш те, що від неї лишилося після практики.

— Віталій Матвєєв · [matvieiev.com](https://www.matvieiev.com) · [LinkedIn](https://www.linkedin.com/in/matvieiev-vitalii/)

## Платні скіли

Глибші й гостріші — зроблені з клієнтської роботи, продаються окремо.

→ [matvieiev.com/matvieiev-store](https://www.matvieiev.com/matvieiev-store)

## Зворотний зв'язок

Скористався скілом, і він погано впорався з твоїм випадком? [Створи issue](https://github.com/vitalii-matvieiev/skills/issues) — напиши свій запит і те, чого ти очікував натомість. Саме так вони стають кращими.

## Ліцензія

MIT — користуйся, форкай, впроваджуй. Див. [LICENSE](LICENSE).
