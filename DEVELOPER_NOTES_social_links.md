# DEVELOPER_NOTES_social_links.md

# Pivtorak.Studio — Social Media Links

## Developer Notes / Integration & Maintenance Reference

Цей документ фіксує принципи інтеграції зовнішніх соціальних платформ у Pivtorak.Studio.

Його мета — забезпечити повторюваний, легкий і безпечний спосіб додавання соціальних іконок без повторного дослідження архітектури сайту.

> **Поточний статус:** Instagram успішно інтегровано в Desktop Upper Navigation.
> 
> Подальші соціальні інтеграції виконувати за цим документом, перевіряючи актуальну структуру коду перед кожною зміною.

---

## 1. Принцип інтеграції

Соціальні мережі є зовнішніми каналами комунікації Pivtorak.Studio.

Вони доповнюють сайт, але не замінюють його як основне середовище досліджень, публікацій і документації.

Основні принципи:

- мінімальна кількість UI-елементів;
    
- впізнавані оригінальні символи платформ;
    
- SVG замість растрових зображень;
    
- відсутність зовнішніх JavaScript-залежностей;
    
- відкриття зовнішніх посилань у новій вкладці;
    
- збереження наявної геометрії навігації;
    
- локальні перевизначення Hugo замість редагування теми.
    

---

## 2. Поточна реалізація: Instagram

**Platform:** Instagram  
**Account:** Pivtorak.Studio  
**Profile:** [https://www.instagram.com/pivtorak.studio/](https://www.instagram.com/pivtorak.studio/)

### Розташування

Desktop Upper Navigation:

- основні розділи залишаються ліворуч;
    
- Pivtorak.Studio залишається домашнім посиланням;
    
- Instagram розташовується праворуч від назви бренду.
    

Instagram не створює окремого пункту основної навігації.

### Відображення

- компактна SVG-іконка;
    
- монохромний вигляд;
    
- колір успадковується через `currentColor`;
    
- hover/focus використовує `var(--color-link)`;
    
- розмір SVG: 21 × 21 px;
    
- розмір інтерактивної області: 24 × 24 px.
    

### HTML

Реалізація розташована в:

`layouts/_partials/docs/upper-navigation.html`

Instagram використовує:

- `target="_blank"` — відкриття в новій вкладці;
    
- `rel="noopener noreferrer"` — безпечне відкриття;
    
- `aria-label` — доступна назва посилання;
    
- `title` — підказка;
    
- `aria-hidden="true"` для декоративного SVG;
    
- `focusable="false"` для SVG.
    

### CSS / SCSS

Реалізація розташована в:

`assets/_custom.scss`

Використовуються класи:

```
.upper-navigation-brand-group
.upper-navigation-instagram
```

Група бренду та соціальної іконки використовує Flexbox.

Hover і keyboard focus:

```
.upper-navigation-instagram:hover,
.upper-navigation-instagram:focus-visible {
  color: var(--color-link);
}
```

---

## 3. Адаптивність

Поточна верхня навігація має такі правила:

```
.upper-navigation {
  display: none;
}
```

Desktop:

```
@media screen and (min-width: 57rem)
```

Тому Instagram наразі є елементом Desktop Upper Navigation.

Мобільна інтеграція не реалізована.

Не змінювати mobile layout автоматично під час додавання нових соціальних платформ. Це має бути окреме дизайнерське рішення.

---

## 4. Додавання наступної соціальної іконки

Перед інтеграцією нової платформи:

1. Перевірити актуальний `upper-navigation.html`.
    
2. Перевірити актуальні стилі в `_custom.scss`.
    
3. Визначити офіційну адресу профілю.
    
4. Підготувати SVG відповідної платформи.
    
5. Додати посилання з унікальним CSS-класом.
    
6. Зберегти наявні атрибути доступності та безпеки.
    
7. За потреби додати мінімальні стилі.
    
8. Перевірити геометрію навігації.
    

Не створювати окремі компоненти або JavaScript, якщо звичайного HTML і SCSS достатньо.

Не дублювати стилі без необхідності.

---

## 5. Обмеження та правила

- Не редагувати `themes/hugo-book/`.
    
- Не змінювати порядок основних пунктів навігації.
    
- Не змінювати висоту Upper Navigation без окремого рішення.
    
- Не додавати текстові назви соціальних мереж без дизайнерської потреби.
    
- Не завантажувати зовнішні віджети та стрічки автоматично.
    
- Не створювати паралельну систему соціальних посилань.
    
- Не додавати іконки платформ, профілі яких ще не підтверджені.
    

Усі зміни виконувати через власні шаблони та стилі сайту.

---

## 6. Перевірка після інтеграції

### Build

```
hugo
```

### Visual inspection

Перевірити:

- Desktop Upper Navigation;
    
- розташування назви бренду;
    
- розташування соціальних іконок;
    
- збереження всіх основних пунктів;
    
- відсутність горизонтального переповнення;
    
- hover та keyboard focus;
    
- відкриття зовнішнього посилання;
    
- EN, UK, PT.
    

Mobile перевіряти окремо, якщо змінюється його архітектура.

### Git

```
git status
git diff
```

Перевірити, що змінені лише заплановані файли.

Після успішної перевірки:

```
git add <змінені файли>
git commit -m "Add Instagram social link to upper navigation"
git push
```

Після Push перевірити опубліковану версію.

---

## 7. Related Developer Notes

```
DEVELOPER_NOTES.md
DEVELOPER_NOTES_top_area.md
DEVELOPER_NOTES_logo_favicon.md
DEVELOPER_NOTES_menu_groups.md
```

Цей документ доповнює документацію верхньої частини сайту та визначає правила інтеграції зовнішніх соціальних платформ.

---

# Final principle

**Social platforms are gateways to Pivtorak.Studio, not substitutes for its knowledge architecture.**

Keep the integration recognizable, lightweight, accessible, and independent from external widgets.

One icon → one verified link → one controlled implementation.

---
### Production Verification

- Instagram icon successfully rendered on the live website.
- External link to https://www.instagram.com/pivtorak.studio/ verified.
- Navigation appearance and existing menu functionality preserved after deployment.