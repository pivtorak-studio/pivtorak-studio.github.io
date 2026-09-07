## `robots.txt` — виправлення

1. Перевірили `robots.txt` → замість директив роботів Hugo генерував 34 KB список сторінок сайту.
2. Перевірили `layouts`, `theme`, `content`, `static` і конфігурацію → окремого `robots.txt` не було.
3. Виявили, що Hugo має вбудований output format `robots` (`text/plain`).
4. У `hugo-book` існує catch-all template `layouts/all.txt`, який через template lookup використовувався для цього output.
5. Створили власний `layouts/robots.txt`, щоб явно визначити правильний шаблон.
6. Виконали чистий Hugo build і перевірили результат.
7. Commit `8c98ac0a` + push у `main`.
8. GitHub Actions успішно задеплоїв сайт.
9. Live `/robots.txt` перевірено — **працює коректно**.

**Результат:**

User-agent: *
Allow: /

Sitemap: https://pivtorak.studio/sitemap.xml

**Виправлено:** Hugo `robots` output перехоплювався catch-all template `hugo-book/layouts/all.txt`, через що `/robots.txt` містив список сторінок. Додано явний `layouts/robots.txt`; після clean build і deployment live `/robots.txt` працює коректно.

---
## Короткий чек-лист перевірки `robots.txt`

ROBOTS.TXT CHECK

1. Source:
   layouts/robots.txt / static/robots.txt / Hugo config

2. Build:
   hugo

3. Local:
   Get-Content .\public\robots.txt

4. Live:
   https://pivtorak.studio/robots.txt

5. Verify:
   - HTTP 200, not 404
   - plain text
   - User-agent directive
   - correct Allow/Disallow rules
   - correct Sitemap URL
   - referenced sitemap exists

6. If wrong:
   inspect Hugo template lookup, especially all.txt.

---
### правило

> **Перевіряємо не тільки наявність `robots.txt`, а три рівні:**
> 
> **source → generated build → live URL.**

---
## Алгоритм перевірки `robots.txt`

### 1. Перевірити, чи існує source-механізм

У корені Hugo-проєкту:

```
Get-ChildItem -Path . -Filter robots.txt -File -Recurse | Select-Object FullName, Length
```

Перевірити, чи немає:

```
layouts/robots.txt
static/robots.txt
```

а також перевірити конфігурацію:

```
hugo config | Select-String -Pattern 'enableRobotsTXT|robots|output'
```

Для нашого сайту очікуємо:

```
enableRobotsTXT = true
```

---

### 2. Зробити Hugo build

```
hugo
```

Якщо build завершився без `ERROR`, перевірити:

```
Get-Content .\public\robots.txt
```

Очікуваний результат:

```
User-agent: *
Allow: /

Sitemap: https://pivtorak.studio/sitemap.xml
```

---

### 3. Перевірити саме live-сайт

Відкрити:

```
https://pivtorak.studio/robots.txt
```

Перевірити:

- файл відкривається, **не 404**;
- це plain-text robots.txt, а не HTML;
- присутній `User-agent: *`;
- правила `Allow` / `Disallow` відповідають задуму сайту;
- присутній правильний `Sitemap`;
- Sitemap веде на існуючий sitemap.

---

### 4. Якщо результат неправильний

Якщо замість robots directives бачимо, наприклад:

```
Pivtorak.Studio
- Назва сторінки: URL
- Назва сторінки: URL
...
```

**не виправляти `public/robots.txt` вручну.**

Перевірити template lookup:

```
layouts/robots.txt
themes/<theme>/layouts/robots.txt
layouts/all.txt
```

Особливо звернути увагу на catch-all `all.txt`, оскільки plain-text output може бути ним перехоплений.

---

### 5. Після виправлення

Зробити clean build:

```
Remove-Item -Recurse -Force .\public\
hugo
```

Перевірити:

```
Get-Content .\public\robots.txt
```

Після deployment знову перевірити:

```
https://pivtorak.studio/robots.txt
```


