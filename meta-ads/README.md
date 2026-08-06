# Meta ads — audit, launch, weekly optimisation

Your ad account says a lead costs $18. Is that good?

Nobody can answer that from the dashboard. Not the account, not an agency, not you. The answer lives in three numbers the dashboard has never seen: what you keep from a deal, how many enquiries turn into money, and how much of that profit you are willing to spend to get one.

This skill starts there. It works out the most you can pay for a customer before advertising stops making you money, then judges every campaign against that number instead of against a benchmark somebody posted on LinkedIn.

> **You do not need to be a programmer to use this.** Installing takes about two minutes and works on every Claude plan, including the free one.

## Before you install: connect your ad account

This skill reads your live campaigns. Without a connection it will tell you so and stop — it will not invent numbers or show you an example.

1. In Claude, add the official Meta ads connector: `https://mcp.facebook.com/ads`
2. Sign in with the Business account that owns your ads
3. Grant access to the ad account you want to work on:
   - **read-only** is enough to analyse
   - **read and write** is needed to create campaigns or change budgets

## Install without a terminal

1. **Download:** [meta-ads.zip](https://github.com/vitalii-matvieiev/skills/releases/latest/download/meta-ads.zip)
2. In Claude, open **Customize → Skills**
3. Upload the file and switch the skill on
4. Start a normal chat and describe your situation in plain words

## Install with a terminal

```bash
npx skills add vitalii-matvieiev/skills --skill meta-ads
```

## What to say to it

No commands to learn. Write the way you would to a person:

- *"Look at my Facebook ads. I am spending €2,000 a month and I have no idea if it works."*
- *"A lead costs me $18. Is that expensive?"*
- *"Where is my ad budget actually going?"*
- *"I want to start advertising my service. Help me set up the first campaign."*
- *"Go through last week — what should I scale and what should I turn off?"*
- *"My cost per lead doubled and I do not know why."*

It will ask you questions before it touches anything. Answer honestly, including "I do not know" — it handles that.

## What you get back

Three findings with numbers, not a list of twenty observations. A table where every campaign has one verdict — scale, hold, fix, or stop — with the arithmetic behind it. A plan split into today, this week, and things not worth doing at all. And a written report you can keep.

If you asked it to change something, it shows you the exact list first and waits for your yes. New campaigns are always created **paused** — nothing starts spending your money on its own.

It will also tell you things you may not want to hear: that fewer than ten conversions is not enough to conclude anything, that your tracking may be counting conversions twice and flattering your results, and that without knowing your margin you can watch your advertising but you cannot manage it.

It looks at your actual ads, not just their numbers — it renders them as they appear in the feed, in Stories, in Reels, and sends you the links so you can see what your audience sees.

## Stuck on the connection?

Just say so — *"I cannot get the ads tools to work"* — and it will walk you through it one step at a time, then verify the result instead of assuming it worked. It cannot click through your browser or log into Meta for you; that part is yours.

## What it cannot do

It does not run in the background. Nothing is monitored or changed while you are away, and it does not remember your previous conversations. It does read your account's own change history, so it can still tell you what was changed last week and whether it helped.

The numbers come from Meta's attribution, not from your bookkeeping. A gap against your CRM is normal; a gap of several times means your tracking is broken, and it will say so.

Meta only. Not Google, not TikTok, not LinkedIn. Rouble-denominated ad accounts are out of scope.

---

# Реклама в Meta — розбір, запуск, тижнева оптимізація

Кабінет показує, що заявка коштує 18 доларів. Це добре?

З кабінету цього не скаже ніхто. Ні сам кабінет, ні агенція, ні ви. Відповідь лежить у трьох числах, яких кабінет ніколи не бачив: скільки залишається з угоди, скільки заявок стають грошима і яку частку цього прибутку ви готові віддати за одного клієнта.

Цей скіл починає саме звідти. Він рахує, скільки максимум можна платити за клієнта, поки реклама ще заробляє, — і далі судить кожну кампанію за цим числом, а не за бенчмарком із чужого допису.

> **Щоб цим користуватися, не треба бути програмістом.** Встановлення займе близько двох хвилин і працює на всіх тарифах Claude, включно з безкоштовним.

## Перед встановленням: підключіть рекламний кабінет

Скіл читає ваші живі кампанії. Без підключення він так і скаже й зупиниться — вигадувати цифри або показувати приклад він не буде.

1. У Claude додайте офіційний конектор реклами Meta: `https://mcp.facebook.com/ads`
2. Увійдіть через Business-акаунт, якому належить реклама
3. Видайте доступ до потрібного рекламного акаунта:
   - **тільки читання** — достатньо для аналізу
   - **читання і запис** — потрібно, щоб створювати кампанії й міняти бюджети

## Встановлення без терміналу

1. **Завантажте:** [meta-ads.zip](https://github.com/vitalii-matvieiev/skills/releases/latest/download/meta-ads.zip)
2. У Claude відкрийте **Customize → Skills**
3. Завантажте файл і увімкніть скіл
4. Почніть звичайний чат і опишіть свою ситуацію простими словами

## Встановлення через термінал

```bash
npx skills add vitalii-matvieiev/skills --skill meta-ads
```

## Що йому писати

Жодних команд вчити не треба. Пишіть так, як писали б людині:

- *«Подивись мою рекламу у фейсбуці. Витрачаю 2000 євро на місяць і не розумію, чи це працює».*
- *«Заявка коштує 18 доларів. Це дорого?»*
- *«Куди насправді йде мій рекламний бюджет?»*
- *«Хочу почати рекламувати свою послугу. Допоможи налаштувати першу кампанію».*
- *«Пройдись по минулому тижню — що масштабувати, що вимкнути?»*
- *«Заявка подорожчала вдвічі, і я не розумію чому».*

Він ставитиме питання, перш ніж щось зробити. Відповідайте чесно, зокрема «не знаю» — це він теж уміє обробити.

## Що ви отримаєте

Три знахідки з цифрами, а не список із двадцяти спостережень. Таблицю, де в кожної кампанії один вердикт — масштабувати, тримати, лікувати чи вимкнути — з арифметикою під ним. План, поділений на «сьогодні», «цього тижня» і «не робити взагалі». І письмовий звіт, який лишається у вас.

Якщо ви попросили щось змінити — спочатку він покаже точний список і дочекається вашого «так». Нові кампанії завжди створюються **на паузі**: ніщо не починає витрачати гроші самостійно.

Він також скаже те, що не хочеться чути: що менш ніж десять заявок — це замало для будь-яких висновків, що ваше відстеження може рахувати конверсії двічі й прикрашати результат, і що без знання власної маржі рекламу можна спостерігати, але не можна нею керувати.

Він дивиться на самі оголошення, а не тільки на їхні цифри — показує їх такими, якими вони виглядають у стрічці, в Stories, у Reels, і дає посилання, щоб ви побачили те саме, що бачить ваша аудиторія.

## Не виходить підключити?

Просто скажіть — *«не можу підключити рекламний кабінет»* — і він проведе вас по кроках, а потім перевірить результат, а не вдаватиме, що все спрацювало. Натиснути кнопки у вашому браузері чи зайти у ваш Meta-акаунт замість вас він не може — це ваша частина.

## Чого він не вміє

Він не працює у фоні. Поки вас немає, нічого не відстежується й не змінюється, і попередніх розмов він не пам'ятає. Але історію змін самого кабінету він читає — тож усе одно скаже, що змінювали минулого тижня і чи це допомогло.

Цифри беруться з моделі атрибуції Meta, а не з вашої бухгалтерії. Розбіжність із CRM — нормально; розбіжність у рази означає, що зламане відстеження, і він про це скаже.

Тільки Meta. Не Google, не TikTok, не LinkedIn. З рекламними кабінетами в російських рублях скіл не працює.
