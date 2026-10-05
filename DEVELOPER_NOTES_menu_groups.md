# 🧭 Pivtorak.Studio — Menu Groups

Цей файл описує технічну логіку групування верхньорівневих розділів у лівому меню Pivtorak.Studio.

Документ потрібен для того, щоб:

- розуміти, як формуються групи;
- не шукати логіку в окремих Markdown-файлах;
- правильно додавати нові серії;
- не створювати нову групу там, де достатньо додати slug до вже існуючої;
- зберігати однакову структуру меню для всіх мовних версій.

---

## 1. Де знаходиться логіка меню

Групування реалізоване в локальному partial:

```
layouts/partials/docs/menu.html
```

Це **не Hugo taxonomy** і не окремий YAML-файл.

Групування визначається безпосередньо в шаблоні меню через списки slug'ів.

---

# 2. Основний принцип

Hugo бачить верхньорівневі сторінки та секції.

Для кожної секції використовується її slug:

```
$slug := path.Base $page.File.Dir
```

Потім slug перевіряється на належність до однієї з груп.

Наприклад:

```
$seriesProjectsSlugs := slice
  "core-recalibration"
  "peaceful-life"
  "the-majestic-discipline"
  "shield-of-nation"
  "living-topography"
  "esmée-the-dragon-of-balance"
  "political-design"
  "extra-credit-problem"
```

Якщо slug секції входить до цього списку, вона належить до групи **Series & Projects**. Вставлений текст markdown

---

# 3. Поточні групи

Зараз меню використовує шість спеціальних груп:

|Group|Technical list|Rank|
|---|---|---|
|Identity|$identitySlugs|`0`|
|Research|$researchSlugs|`1`|
|Series & Projects|$seriesProjectsSlugs|`2`|
|Studio|$studioSlugs|`3`|
|Tools|$toolsSlugs|`7`|
|Archive|$archiveSlugs|`8`|

Усе, що не потрапляє до цих списків, отримує rank `9`. Вставлений текст markdown

Це означає, що **наявність `_index.md` сама по собі не визначає групу**.

Групу визначає список slug'ів у menu template.

---

# 4. Identity

Технічний список:

```
$identitySlugs := slice
  "pivtorak-studio"
  "anna-pivtorak-kostyuk-identity-and-evolution"
  "independent-researcher-manifesto"
```

До Identity також спеціально прирівняна сторінка:

```
about.md
```

Отже, Identity може містити не тільки секції, а й окрему сторінку `about.md`. Вставлений текст markdown

### Коли додавати сюди новий матеріал

Якщо новий верхньорівневий розділ описує:

- авторку;
- особисту ідентичність;
- еволюцію авторки;
- базову ідентичність студії;
- маніфест незалежного дослідника,

його slug може бути доданий до $identitySlugs.

---

# 5. Research

Технічний список:

```
$researchSlugs := slice
  "architecture-of-value"
  "expertise"
  "knowledge-base"
  "knowledge-graph"
  "Academic-Publications"
```

Це група для дослідницьких напрямів та інфраструктури знань. Вставлений текст markdown

### Важливо

Не слід автоматично поміщати сюди **кожну статтю, яка є дослідженням**.

Групуються саме **верхньорівневі секції**, а не окремі Markdown-статті.

---

# 6. Series & Projects

Це головна група для послідовних авторських серій та окремих великих проєктів.

Поточний список:

```
$seriesProjectsSlugs := slice
  "core-recalibration"
  "peaceful-life"
  "the-majestic-discipline"
  "shield-of-nation"
  "living-topography"
  "esmée-the-dragon-of-balance"
  "political-design"
  "extra-credit-problem"
```

Вставлений текст markdown

---

## 6.1. Як нова серія потрапляє до цієї групи

**Не потрібно створювати окремий HTML-код для нової серії.**

Потрібно лише:

### 1. Створити звичайну верхньорівневу секцію

Наприклад:

```
content/uk/docs/new-series/
```

і відповідні мовні версії:

```
content/en/docs/new-series/
content/pt/docs/new-series/
```

Якщо потрібна RU-версія:

```
content/ru/docs/new-series/
```

---

### 2. Визначити slug

У нашому випадку це:

```
new-series
```

Саме цей slug буде отриманий через:

```
path.Base $page.File.Dir
```

---

### 3. Додати slug до $seriesProjectsSlugs

Наприклад:

```
$seriesProjectsSlugs := slice
  "core-recalibration"
  "peaceful-life"
  "the-majestic-discipline"
  "shield-of-nation"
  "living-topography"
  "esmée-the-dragon-of-balance"
  "political-design"
  "extra-credit-problem"
  "new-series"
```

Після цього Hugo автоматично включить нову секцію до групи **Series & Projects**. Вставлений текст markdown

---

# 7. Studio

Поточний список:

```
$studioSlugs := slice
  "001-Pivtorak-Studio-Standard"
  "process-diary"
```

Studio використовується для матеріалів, безпосередньо пов'язаних із функціонуванням та розвитком Pivtorak.Studio.

---

# 8. Tools

Поточний список:

```
$toolsSlugs := slice
  "calculators"
  "converters"
  "templates"
  "seo-tricks"
```

Це практичні та технічні ресурси сайту.

Нова сторінка потрапляє сюди за тим самим принципом: її slug додається до $toolsSlugs.

---

# 9. Archive

Поточний список:

```
$archiveSlugs := slice
  "the-movement-matrix"
```

Це спеціальна архівна група.

Не слід автоматично відносити сюди всі сторінки зі словом `archive` у назві. Належність визначається явно через $archiveSlugs.

---

# 10. Порядок груп

Порядок визначається не порядком Markdown-файлів і не алфавітом.

Для кожної сторінки створюється значення:

```
(rank, original-index)
```

у форматі:

```
printf "%02d-%05d"
```

Потім весь список сортується за цим значенням. Вставлений текст markdown

Поточна схема:

```
0 — Identity
1 — Research
2 — Series & Projects
3 — Studio
4–6 — currently unused
7 — Tools
8 — Archive
9 — everything else
```

Таким чином, якщо додати нову серію до $seriesProjectsSlugs, **їй не потрібно задавати окремий weight для розташування групи**.

Вона автоматично отримає rank `2`.

---

# 11. Як додати нову серію — коротка інструкція

Якщо з'являється нова серія:

### Крок 1

Створити її звичайну Hugo section:

```
content/uk/docs/my-new-series/
```

### Крок 2

Створити `_index.md`.

### Крок 3

Створити мовні версії:

```
content/en/docs/my-new-series/
content/pt/docs/my-new-series/
```

за потреби — RU.

### Крок 4

Перевірити slug:

```
my-new-series
```

### Крок 5

Додати **тільки цей slug** до:

```
$seriesProjectsSlugs
```

### Крок 6

Зробити Hugo build:

```
hugo
```

### Крок 7

Перевірити меню.

**Інший код групування змінювати не потрібно.**

---

# 12. Якщо нова серія не повинна бути в Series & Projects

Не потрібно додавати її до $seriesProjectsSlugs.

Спочатку визначається її роль:

```
Identity
Research
Series & Projects
Studio
Tools
Archive
```

і slug додається до відповідного списку.

Якщо секція не належить до жодної спеціальної групи, вона залишиться у звичайному меню з rank `9`.

---

# 13. Одна секція — одна група

Для верхнього рівня не слід додавати один і той самий slug до кількох груп без спеціальної причини.

Умови перевіряються послідовно:

```
Identity
→ Research
→ Series & Projects
→ Studio
→ Tools
→ Archive
```

Тому при перетині списків спрацює **перша відповідна умова**. Вставлений текст markdown

Практичне правило:

> **Один верхньорівневий розділ повинен мати одну основну позицію в глобальному меню.**

---

# 14. Що НЕ потрібно робити

При створенні нової серії не потрібно:

- створювати новий partial;
- створювати окремий HTML-блок;
- копіювати код групи;
- змінювати rank;
- додавати спеціальний CSS;
- змінювати тему Hugo Book;
- створювати окремий пункт у `hugo.toml`;
- вручну додавати кожну статтю серії до меню.

Меню вже вміє рекурсивно показувати дочірні сторінки секції через:

```
book-section-children
```

а сам пункт секції створюється через:

```
book-page-link
```

Вставлений текст markdown

---

# 15. Що важливо для нової серії

Нова серія повинна мати нормальну Hugo-структуру:

```
new-series/
├── _index.md
├── 001-first-item.md
├── 002-second-item.md
└── ...
```

Для багатомовного сайту структура повинна бути паралельною:

```
content/
├── uk/docs/new-series/
├── en/docs/new-series/
└── pt/docs/new-series/
```

Мовні зв'язки та `translationKey` належать до окремої multilingual-системи сайту і не визначають групу меню. У поточній документації multilingual SEO саме `translationKey` використовується для зв'язування перекладів. DEVELOPER_NOTES

---

# 16. Головний принцип

Система побудована так:

```
Hugo section
      ↓
section slug
      ↓
перевірка slug у списках
      ↓
визначення групи
      ↓
rank групи
      ↓
сортування
      ↓
відображення в Sidebar
```

Тобто **група — це властивість навігаційної логіки, а не властивість самої статті**.

---

## 17. Найважливіше правило для майбутнього

> **Нова серія не «реєструється» в меню окремим пунктом.**
> 
> Вона створюється як звичайна Hugo section, після чого її slug додається до відповідного списку групи.

Для типової нової авторської серії:

```
$seriesProjectsSlugs
```

це єдина зміна в логіці групування.

---

### Примітка

Поточна реалізація має **явні списки slug'ів**, а не автоматичне визначення «що є серією» за front matter `series`. Це важливо: поле `series` на окремій сторінці використовується також для `series-navigation`, але саме воно **не додає верхньорівневу секцію до групи Series & Projects**. `series-navigation.html` показує карту серії, коли сторінка має `series`. Вставлено файл розмітки (4)

