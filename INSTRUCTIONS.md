# 🛠 Інструкції з обслуговування сайту Pivtorak Studio

Цей файл містить технічні кроки для керування мовними версіями та SEO.

---
*Примітка: Після внесення змін перевірте локально через `hugo server`.*

# 🌍 Multilingual SEO System — Pivtorak.Studio

## 🧩 Загальна логіка

Сайт побудований на Hugo з підтримкою багатомовності:

* 🇺🇦 Ukrainian (default)
* 🇬🇧 English
* 🇵🇹 Portuguese (EU)
* 🇷🇺 Russian (тимчасово вимкнена)

SEO-система включає:

* hreflang (alternate links)
* canonical URLs
* OpenGraph + Twitter Cards
* multilingual sitemap

---

## ⚙️ Увімкнення / вимкнення RU-мови

### 🔴 Поточний стан:

RU-мова **вимкнена** і НЕ індексується Google.

---

## ✅ Щоб УВІМКНУТИ RU:

### 1. У файлі `hugo.toml`:

Розкоментувати:

```toml
[languages.ru]
  languageName = 'RU'
  contentDir = 'content/ru'
  weight = 4
```

---

### 2. У файлі `layouts/partials/seo.html`:

ВИДАЛИТИ блок:

```html
{{ if eq .Language.Lang "ru" }}
<meta name="robots" content="noindex, nofollow">
{{ end }}
```

---

### 3. Деплой сайту

Після цього:

* RU з’явиться в sitemap
* RU сторінки почнуть індексуватися

---

## ⛔ Щоб ВИМКНУТИ RU назад:

### 1. Закоментувати в `hugo.toml`:

```toml
# [languages.ru]
#   languageName = 'RU'
#   contentDir = 'content/ru'
#   weight = 4
```

---

### 2. (опціонально) Повернути noindex у `seo.html`

---

## 🧠 Важливо

* Всі переклади повинні мати однаковий:

  ```yaml
  translationKey: pivtorak-studio
  ```

* Це потрібно для:

  * hreflang
  * sitemap зв’язків
  * правильного SEO

---

## 🗺 Sitemap

Головний sitemap:

```
/sitemap.xml
```

Містить мовні sitemap:

* /uk/sitemap.xml
* /en/sitemap.xml
* /pt/sitemap.xml

---

## 🚀 Якщо щось “зламалось”

Перевірити:

* чи є `translationKey`
* чи існують всі мовні версії сторінки
* чи не вимкнена мова в `hugo.toml`

---

## 💡 Принцип

Система зроблена так, щоб:

✔ працювати автоматично
✔ не вимагати ручного редагування
✔ легко перемикати мови

---

## 🛡 Контроль

Навіть якщо RU-файли існують:

* поки мова вимкнена → Google їх НЕ бачить
* це безпечно для SEO

---
