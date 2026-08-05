# skills

Agent skills for founders, entrepreneurs and creative people who run their work on AI.

> **You do not need to be a programmer to use these.**
> If you use Claude in your browser or the desktop app, installing one takes about two minutes. No terminal, no GitHub account, no code.

## What a skill is

A skill is a set of instructions an AI agent installs once and then follows on its own. You do not read it, run it, or learn any commands. You describe your situation in plain words, and the agent recognises which skill applies and works through it with you — asking what it needs, in the right order, without you having to know the method.

Think of it as handing your agent a specialist's checklist instead of hoping it improvises well.

## How to install

Every skill lives in its own folder in this repository. Open the one you need from the list below — each has its own page with a download link and instructions.

**Without a terminal.** Download the skill's `.zip` from its page, then in Claude open **Customize → Skills**, upload the file and switch it on. Works on every Claude plan, including the free one.

**With a terminal.** For Claude Code, Codex, Cursor, OpenCode and 70+ other agents:

```bash
# everything in this repository
npx skills add vitalii-matvieiev/skills

# one specific skill
npx skills add vitalii-matvieiev/skills --skill <skill-name>

# see what is inside before installing
npx skills add vitalii-matvieiev/skills --list
```

## How to use one

You never call a skill by name. You write to your agent the way you would write to a person — describe the situation, the problem, the decision you are stuck on. The agent picks the right skill itself and starts asking you questions.

Each skill's page has real examples of what to write.

## Skills

| Skill | What it does |
|---|---|
| **[slicing-pie](slicing-pie/)** | Splits startup equity between co-founders by actual contribution instead of a handshake 50/50. Calculates the split, sets the moment it freezes, covers what happens when someone leaves. |

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
> Якщо ви користуєтесь Claude у браузері або в застосунку, встановлення займе близько двох хвилин. Без терміналу, без акаунта на GitHub, без коду.

## Що таке скіл

Скіл — це набір інструкцій, які AI-агент встановлює один раз і далі виконує сам. Його не треба читати, запускати чи вчити якісь команди. Ви описуєте свою ситуацію звичайними словами, а агент розпізнає, який скіл підходить, і проводить вас через нього — питає те, що йому потрібно, у правильному порядку, і вам не треба знати саму методику.

Простіше кажучи: ви даєте агенту чек-лист фахівця замість того, щоб сподіватися, що він вдало зімпровізує.

## Як встановити

Кожен скіл лежить в окремій папці цього репозиторію. Відкрийте потрібний зі списку нижче — у кожного своя сторінка з посиланням на завантаження та інструкцією.

**Без терміналу.** Завантажте `.zip` скіла з його сторінки, потім у Claude відкрийте **Customize → Skills**, завантажте файл і увімкніть. Працює на всіх тарифах Claude, включно з безкоштовним.

**Через термінал.** Для Claude Code, Codex, Cursor, OpenCode і ще 70+ агентів:

```bash
# усе, що є в репозиторії
npx skills add vitalii-matvieiev/skills

# один конкретний скіл
npx skills add vitalii-matvieiev/skills --skill <назва-скіла>

# подивитися, що всередині, перед встановленням
npx skills add vitalii-matvieiev/skills --list
```

## Як цим користуватися

Скіл ніколи не викликають на ім'я. Ви пишете агенту так, як писали б людині — описуєте ситуацію, проблему, рішення, на якому застрягли. Агент сам обирає потрібний скіл і починає ставити вам питання.

На сторінці кожного скіла є живі приклади того, що писати.

## Скіли

| Скіл | Що робить |
|---|---|
| **[slicing-pie](slicing-pie/)** | Ділить частки в стартапі між співзасновниками за реальним внеском, а не за домовленістю «50 на 50 по руках». Рахує розподіл, визначає момент його заморозки, описує, що робити, коли хтось виходить. |

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
