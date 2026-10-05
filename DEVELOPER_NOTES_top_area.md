# DEVELOPER_NOTES_top_area.md

# Pivtorak.Studio — Верхня частина сайту
## Developer Notes / Design & Maintenance Reference

Цей документ фіксує поточну архітектуру та принципи верхньої частини
Pivtorak.Studio, щоб у майбутньому можна було безпечно повернутися до
цього коду без повторного дослідження всієї історії змін.

> **Статус:** завершений дизайн-етап.
> Верхня частина вважається стабільною. Будь-які подальші зміни —
> окремий дизайн-етап із власним build → visual check → commit → push.

---

## 1. Що входить до верхньої частини

На desktop верхня зона складається з:

1. **Upper Navigation**
2. **Research on Request**
3. **Information Strip**
4. **Main content area** з Sidebar / Article / TOC

Це одна композиційна зона над основним контентом.

На mobile верхня навігація та Information Strip не використовуються
як desktop-елементи; Research on Request має окреме компактне mobile
оформлення.

---

## 2. Верхня навігація

### Порядок

**Research → Series & Projects → Studio → Tools → Archive → Pivtorak.Studio**

`Pivtorak.Studio` є домашнім посиланням і стоїть останнім.

Окремого пункту `Home` немає.

Language switcher і search залишаються у Sidebar.

### Landing pages

Upper Navigation веде на кореневі landing pages:

- Research: `/en/research/`, `/uk/research/`, `/pt/research/`
- Series & Projects: `/en/series-and-projects/`, `/uk/series-and-projects/`, `/pt/series-and-projects/`
- Studio: `/en/studio/`, `/uk/studio/`, `/pt/studio/`
- Tools: `/en/tools/`, `/uk/tools/`, `/pt/tools/`
- Archive: `/en/archive/`, `/uk/archive/`, `/pt/archive/`

RU існує в content, але мова зараз вимкнена.

### Реалізація

```text
layouts/partials/docs/upper-navigation.html
```

Підключення:

```text
layouts/partials/docs/inject/content-before.html
```

### Принцип дизайну

Upper Navigation має бути стриманою, не декоративною:
приблизно 16px, невисока, прозорий фон, тонкий divider, без жирного
накреслення.

Не перетворювати її на mega-menu без окремого рішення.

---

## 3. Research on Request

Поточний текст:

**⌕ Research on Request:** Market Research · Competitive Intelligence ·
Consumer Insights · Cultural Analysis · Feasibility Studies · Business
Plans · Investment Analysis · research@pivtorak.studio

Функція:

> одразу повідомити зовнішньому відвідувачу, що Pivtorak.Studio може
> виконувати дослідницьку роботу на замовлення.

### Реалізація

```text
layouts/partials/docs/research-banner.html
layouts/baseof.html
```

Banner викликається перед:

```html
<main class="container flex">
```

Тому він може займати всю ширину над Sidebar + Article + TOC.

### i18n

```text
i18n/en.yaml
i18n/uk.yaml
i18n/pt.yaml
i18n/ru.yaml
```

RU може мати переклад, але сама мова залишається вимкненою.

### Desktop

- inline layout;
- приблизно 15px;
- прозорий/нейтральний фон;
- тонка рамка;
- без shadow/card;
- послуги та email залишаються в одному інформаційному рядку,
  наскільки це дозволяє ширина.

### Mobile

- рамка;
- внутрішній padding;
- центрований текст;
- природне перенесення рядків;
- той самий зміст.

Mobile не повинен автоматично успадковувати desktop geometry.

### Важливе правило

Не додавати поруч другий рекламний banner, grant banner, «For Grant
Evaluators» banner або другий Information Strip.

---

## 4. Information Strip

Information Strip — постійний ідентифікаційний рядок над основним
контентом.

### EN

`Pivtorak.Studio · Contemporary conceptual practice`

`Anna Pivtorak · Independent Researcher`

`Governance systems · Cultural capital · Visual analytics · Structuring meanings`

### UA

`Pivtorak.Studio · Сучасна концептуальна практика`

`Анна Півторак · Незалежний дослідник`

`Системи врядування · Культурний капітал · Візуальна аналітика · Структурація смислів`

### PT

`Pivtorak.Studio · Prática conceptual contemporânea`

`Anna Pivtorak · Investigadora Independente`

`Sistemas de governação · Capital cultural · Análise visual · Estruturação de significados`

### Реалізація

```text
layouts/partials/docs/inject/content-before.html
assets/_custom.scss
i18n/*.yaml
```

### Дизайн

- прозорий фон;
- без card/shadow;
- тонкий divider;
- невеликий вертикальний інтервал між рядками;
- приблизно 48px від divider до H1;
- desktop-only.

Information Strip — **ідентифікація, а не реклама**.

---

## 5. Загальна композиційна модель

```text
Header / site chrome
        ↓
Upper Navigation
        ↓
Information Strip
        ↓
Research on Request
        ↓
Main container
    ├── Sidebar
    ├── Article
    └── TOC
```

Це опис композиційної моделі. Перед змінами фактичний порядок викликів
у шаблонах потрібно перевіряти в коді.

---

## 6. Desktop geometry

Основні параметри:

- desktop breakpoint: **57rem / 912px**;
- container max-width: **100rem / 1600px**;
- Sidebar: **15rem / 240px**;
- TOC: **15rem / 240px**;
- column gap: **2rem / 32px**;
- main content — flexible;
- markdown base size: **17px**.

Поточний top spacing:

```scss
main.container {
  margin-top: 1rem;
}
```

Раніше використовувався більший shell top offset (2–3rem), але він
створював зайве повітря і був прибраний.

---

## 7. Sticky behavior

На desktop Sidebar і TOC використовують локально налаштовану sticky
поведінку замість початкового fixed-підходу Hugo Book.

Мета: Sidebar, центральна колонка і TOC повинні починати композицію на
одній вертикальній лінії.

Не повертати fixed-поведінку theme без перевірки всієї desktop geometry.

Mobile behavior не змінювати разом із desktop змінами.

---

## 8. Theme source

Звичайні дизайн-зміни робити через site-local overrides:

```text
assets/_custom.scss
layouts/
layouts/partials/
i18n/
```

Не редагувати:

```text
themes/hugo-book/
```

Локальна копія `layouts/baseof.html` уже використовується для
архітектурної вставки banner. Якщо theme колись оновлюватиметься,
порівняти локальний `baseof.html` з актуальним upstream.

---

## 9. Основний CSS-файл

```text
assets/_custom.scss
```

Особливо уважно перевіряти:

```scss
@media screen and (min-width: 57rem)
```

Не змінювати одночасно container width, Sidebar, TOC, gap, top spacing,
banner spacing і typography.

**Один параметр → build → visual check → рішення.**

---

## 10. Якщо колись захочемо «допиляти» верхню частину

Спочатку сформулювати проблему.

### Навігація

```text
layouts/partials/docs/upper-navigation.html
```

### Research on Request

```text
layouts/partials/docs/research-banner.html
i18n/*.yaml
```

### Information Strip

```text
layouts/partials/docs/inject/content-before.html
assets/_custom.scss
i18n/*.yaml
```

### Вертикальне положення всієї верхньої зони

Перевіряти:

```text
layouts/baseof.html
assets/_custom.scss
main.container
.book-page
.book-menu
.book-toc
```

Не починати з випадкового збільшення `margin` або `padding`.

---

## 11. Чого не додавати автоматично

Не додавати без окремого дизайнерського рішення:

- ще один banner;
- ще один верхній information block;
- декоративний hero;
- grant block;
- «For Grant Evaluators» page лише заради grant positioning;
- дубль назви Pivtorak.Studio без функціональної причини;
- окремий Home;
- language switcher у верхній навігації;
- search у верхній навігації.

Сайт має залишатися **дослідницьким середовищем**, а не презентаційним
landing page з великою кількістю promotional UI.

---

## 12. Landing pages

Landing pages існують насамперед для структурної навігації.

Вони не повинні автоматично перетворюватися на рекламні сторінки,
sales funnels чи grant applications.

Якщо розділ отримає достатньо реального змісту, його landing page можна
розвивати на основі цього змісту.

---

## 13. Перевірка після майбутньої зміни

### 1. Одна зміна

Не змішувати дизайн, структуру і контент в одному експерименті.

### 2. Build

```powershell
hugo
```

За потреби clean build:

```powershell
Remove-Item -Recurse -Force .\public\
hugo
```

### 3. Visual inspection

Перевірити:

- desktop;
- вузький desktop;
- mobile;
- EN;
- UK;
- PT.

RU не потрібно вмикати лише для visual test.

### 4. Git

```powershell
git status
git diff
git add <змінені файли>
git commit -m "<короткий опис>"
git push
```

### 5. Final check

```powershell
git status
```

Очікувано:

```text
nothing to commit, working tree clean
```

---

## 14. Поточна точка відліку

Основний checkpoint завершення Research on Request + desktop layout:

```text
f72fe9b0
design: finalize research banner and desktop layout
```

Подальший branding/favicon checkpoint:

```text
9279b45b
Update P.S. branding and favicon
```

Цей документ не змінює код сайту. Він лише фіксує поточну архітектуру
та правила майбутнього обслуговування.

---

# Final principle

> **Верхня частина Pivtorak.Studio вже виконує свою роботу.**
>
> Вона повинна швидко відповісти:
>
> **де я → що це за середовище → що тут можна досліджувати або замовити.**
>
> Подальше професійне посилення сайту має відбуватися передусім через
> **реальний зміст, дослідження, публікації, проєкти та результати**, а
> не через збільшення кількості UI-елементів у верхній частині.

---

## End of maintenance note

**Do not optimize what is already clear.  
Add evidence before adding decoration.**
