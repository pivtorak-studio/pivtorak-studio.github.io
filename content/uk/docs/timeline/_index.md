---
title: "⏳ Хронологія: Шлях та Еволюція"
description: "Історична реконструкція подій, що сформували ідентичність Anna Pivtorak. Від витоків до створення Pivtorak.Studio."
weight: 5
---

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "CreativeWorkSeries",
  "name": "Хронологія: Шлях та Еволюція — Anna Pivtorak",
  "description": "Динамічна реконструкція подій та етапів формування дослідницької ідентичності.",
  "author": {
    "@type": "Person",
    "name": "Anna Pivtorak"
  }
}
</script>

# ⏳ Хронологія: Шлях та Еволюція

Цей розділ є динамічною реконструкцією подій.    
Кожен запис має дві часові мітки:      
**Historical Date** (час, коли відбулася подія) та       
**Publication Date** (час, коли цей досвід був осмислений та зафіксований у цифрі).    

{{< details "Натисніть, щоб переглянути події за роками" >}}
<ul>
  {{ range (sort .Site.RegularPages "Params.event_date" "asc") }}
    {{ if .Params.event_date }}
      <li>
        <strong>{{ .Params.event_date }}</strong> — 
        <a href="{{ .RelPermalink }}">{{ .Title }}</a>
      </li>
    {{ end }}
  {{ end }}
</ul>
{{< /details >}}
