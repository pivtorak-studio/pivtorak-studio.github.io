---
id: seo-tricks-003-when-google-search-console-says-missing-object-member-name
language: pt
translation_of: seo-tricks-003-when-google-search-console-says-missing-object-member-name
title: 003 Quando o Google Search Console Diz — Falta } Ou o Nome de Um Membro do Objeto
description: "Um caso real do Google Search Console: investigação e correção de um erro de análise de dados estruturados causado pela forma como o JSON-LD estava colocado depois do YAML front matter nos ficheiros Markdown do Hugo."
summary: O Google Search Console comunicou que os dados estruturados não podiam ser analisados devido à ausência de } ou do nome de um membro do objeto. A investigação identificou o problema na separação entre o YAML front matter e o JSON-LD, afetando 565 ficheiros Markdown.
event_date: 2026-09-22T18:00:00
publication_date: 2026-09-22T18:00:00
slug: when-google-search-console-says-missing-object-member-name
tags:
  - Google Search Console
  - dados estruturados
  - JSON-LD
  - Hugo
  - debugging SEO
keywords:
  - Google Search Console dados estruturados
  - falta do nome de um membro do objeto
  - erro de análise JSON-LD
  - erro de análise de dados estruturados
  - Hugo JSON-LD
categories:
  - SEO
  - SEO técnico
series: SEOTricks
series_index: 3
research_origin: Pivtorak.Studio
status: published
featured: true
image: /images/seo-tricks-003-when-google-search-console-says-missing-object-member-name.webp
alt: Google Search Console confirma que um problema de análise de dados estruturados foi resolvido
related:
  - /pt/docs/seo-tricks/
  - /pt/docs/timeline/
authors:
  - Anna Pivtorak
draft: false
canonical: https://pivtorak.studio/pt/docs/seo-tricks/when-google-search-console-says-missing-object-member-name/
toc: true
weight: 3
completion: 100
seo: true
distribution: true
search: indexed
search_intent: resolver erros de análise de dados estruturados no Google Search Console
article_type: caso prático de troubleshooting SEO
primary_topic: análise de dados estruturados no Google Search Console
verification_model: Source → Build → Live
research_status: confirmed
technical_status: verified
lastmod: 2026-09-22T18:00:00
---

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "003 Quando o Google Search Console Diz — Falta } Ou o Nome de Um Membro do Objeto",
  "description": "Um caso real do Google Search Console: investigação e correção de um erro de análise de dados estruturados causado pela forma como o JSON-LD estava colocado depois do YAML front matter nos ficheiros Markdown do Hugo.",
  "inLanguage": "pt-PT",
  "datePublished": "2026-09-22T18:00:00+01:00",
  "dateModified": "2026-09-22T18:00:00+01:00",
  "author": {
    "@type": "Person",
    "name": "Anna Pivtorak",
    "url": "https://pivtorak.studio/pt/"
  },
  "publisher": {
    "@type": "Person",
    "name": "Anna Pivtorak"
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://pivtorak.studio/pt/docs/seo-tricks/when-google-search-console-says-missing-object-member-name/"
  },
  "url": "https://pivtorak.studio/pt/docs/seo-tricks/when-google-search-console-says-missing-object-member-name/",
  "image": "https://pivtorak.studio/images/seo-tricks-003-when-google-search-console-says-missing-object-member-name.webp",
  "articleSection": "Truques de SEO",
  "keywords": [
    "Google Search Console dados estruturados",
    "falta do nome de um membro do objeto",
    "erro de análise JSON-LD",
    "erro de análise de dados estruturados",
    "Hugo JSON-LD"
  ],
  "about": {
    "@type": "Thing",
    "name": "Análise de dados estruturados no Google Search Console"
  },
  "isPartOf": {
    "@type": "CreativeWorkSeries",
    "name": "Truques de SEO",
    "url": "https://pivtorak.studio/pt/docs/seo-tricks/"
  }
}
</script>


![_Truques de SEO. Quando o Google Search Console Diz: Falta `}` ou o Nome de Um Membro do Objeto. AP | Pivtorak.Studio. 22.09.2026_ © Anna Pivtorak (Kostyuk)](/images/seo-tricks-003-when-google-search-console-says-missing-object-member-name.webp)

# Quando o Google Search Console Diz: Falta `}` Ou o Nome de Um Membro do Objeto | Truques de SEO

_Um único carácter em falta pode tornar dados estruturados aparentemente válidos invisíveis para o analisador._

## Quick Summary Box

> **O Google Search Console comunicou:**  
> **Problema:** Não é possível analisar os dados estruturados  
> **Erro específico:** Falta `}` ou o nome de um membro do objeto

O problema foi causado pela forma como o JSON-LD estava colocado imediatamente após o front matter YAML nos ficheiros Markdown. A ausência de uma linha em branco fazia com que o conteúdo gerado fosse analisado incorretamente.

Verificámos os ficheiros-fonte afetados, corrigimos a formatação, confirmámos que qualquer dano acidental na codificação introduzido durante a correção tinha sido totalmente restaurado, reconstruímos o site com sucesso e publicámos a correção. Posteriormente, o Google Search Console confirmou que o problema tinha sido resolvido.

## A Questão

O que levou o Google Search Console a informar que os dados estruturados do site não podiam ser analisados?

O erro específico era:

> **Falta `}` ou o nome de um membro do objeto**

Era necessário determinar se o problema estava no próprio JSON-LD, nos templates Hugo que o geravam ou na forma como o JSON-LD estava colocado nos ficheiros Markdown de origem.

## Porque É Importante

Os dados estruturados ajudam os motores de pesquisa a compreender o significado e a estrutura de uma página. Se o JSON-LD não puder ser analisado, esses dados estruturados não poderão ser processados de forma fiável.

Isto **não significa automaticamente** que a página não possa ser rastreada ou indexada, nem que o seu posicionamento será afetado. O problema aqui é mais específico: **os próprios dados estruturados podem não estar disponíveis para os motores de pesquisa da forma pretendida.**

Por isso, um erro de análise merece ser corrigido, especialmente quando o mesmo padrão nos ficheiros de origem afeta muitas páginas do site.

## A Verificação

Começámos por verificar os próprios ficheiros de origem, em vez de assumir que o JSON-LD estava malformado.

A investigação abrangeu quatro níveis:

1. **O relatório do Google Search Console** — para identificar o problema e a mensagem de erro exatos.  
2. **Os templates Hugo** — para verificar onde os dados estruturados eram gerados e se a sintaxe JSON-LD estava a ser alterada durante a geração das páginas.  
3. **Os ficheiros Markdown de origem** — para verificar como os blocos `<script>` de JSON-LD estavam colocados em relação ao YAML front matter.  
4. **O HTML gerado** — para comparar a estrutura dos ficheiros de origem com o resultado efetivamente produzido pelo Hugo.  

Uma pesquisa nos conteúdos do site revelou **565 ficheiros Markdown** nos quais o delimitador de fecho do YAML front matter era imediatamente seguido pelo bloco `<script>` de JSON-LD, sem uma linha em branco:

```text
---
<script type="application/ld+json">
```

Em seguida, testámos a mesma estrutura depois de inserir uma linha em branco:

```text
---

<script type="application/ld+json">
```

O HTML gerado foi verificado quanto à presença do script de dados estruturados e de caracteres JSON escapados, como `&quot;`.

A verificação mostrou que a alteração de formatação era suficiente para manter o front matter e o JSON-LD corretamente separados no HTML gerado.

## O Que Descobrimos

A investigação revelou que o próprio JSON-LD não era o problema.

### O que esperávamos

Cada ficheiro Markdown tinha um bloco normal de YAML front matter seguido de um bloco `<script>` com JSON-LD. Depois de processado pelo Hugo, os dados estruturados deveriam aparecer como um script separado no HTML gerado.

### O que observámos

Em **565 ficheiros Markdown**, o delimitador de fecho do YAML front matter era imediatamente seguido pelo bloco JSON-LD:

```text
---
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  ...
}
</script>
```

Não existia uma linha em branco entre o fim do front matter e o elemento HTML `<script>`.

Este padrão repetia-se nos ficheiros afetados, pelo que o problema não era um objeto JSON malformado isolado.

### O que as evidências mostraram

Testámos o mesmo conteúdo depois de adicionar uma única linha em branco:

```text
---

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  ...
}
</script>
```

Depois de reconstruir o site com o Hugo, o HTML gerado continha o JSON-LD como um script separado de `application/ld+json`.

Na página de teste, a verificação dos dados estruturados apresentou:

```text
application/ld+json: 1 of 1
&quot;: No results
```

Isto foi significativo porque mostrou que o JSON-LD estava a chegar ao HTML gerado no formato esperado, em vez de ser incorretamente combinado com o front matter anterior.

### O que causou o problema

A causa **não era, portanto, a ausência de `}` dentro do objeto JSON-LD**.

O problema subjacente era a **falta de separação entre o YAML front matter e o bloco `<script>` JSON-LD seguinte nos ficheiros Markdown de origem**.

Como o mesmo padrão estava presente em 565 ficheiros, o problema poderia afetar os dados estruturados numa parte significativa do site.

A investigação revelou também uma lição prática importante: quando um motor de pesquisa comunica um erro de análise JSON, a mensagem apresentada nem sempre identifica a verdadeira origem do problema. Neste caso, a referência à ausência de `}` apontava para o objeto JSON, mas as evidências mostraram que o problema estava na **fronteira entre o front matter Markdown e o bloco JSON-LD**.

## A Correção

A correção foi deliberadamente simples: **adicionar uma linha em branco entre o delimitador de fecho do YAML front matter e o bloco `<script>` JSON-LD em cada ficheiro Markdown afetado.**

### Antes

```text
---
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  ...
}
</script>
```

### Depois

```text
---

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  ...
}
</script>
```

Os ficheiros afetados encontravam-se nos diretórios de conteúdo do site. No total, **565 ficheiros Markdown** continham este padrão específico.

Em vez de editar os ficheiros individualmente, aplicámos a correção de forma sistemática a todos os ficheiros afetados.

### Uma complicação importante

Durante a primeira operação de edição em massa, o tratamento da codificação pelo Windows PowerShell introduziu **mojibake de UTF-8** nos ficheiros afetados. Caracteres como:

```text
â€”
â€™
Â©
ðŸ...
```

apareceram no lugar dos caracteres Unicode originais.

Interrompemos o processo, identificámos o problema de codificação e restaurámos os ficheiros afetados utilizando a transformação inversa CP1252/UTF-8. Uma verificação posterior confirmou:

```text
Ficheiros com mojibake restantes: 0
```

Em seguida, verificámos o `git diff` para garantir que o conteúdo original não tinha sido alterado. O diff final mostrou que a alteração pretendida consistia na adição de **uma linha em branco por ficheiro afetado**.

### Resultado final

A correção produziu:

```text
565 files changed, 565 insertions(+)
```

O Hugo foi então executado e o site foi compilado com sucesso.

Depois de verificarmos os ficheiros de origem, a alteração foi submetida e publicada no GitHub:

```text
915f05fa Add spacing between front matter and JSON-LD
```

O ponto essencial da correção não foi alterar os objetos JSON-LD, mas sim **separar o YAML front matter do bloco JSON-LD seguinte nos ficheiros Markdown de origem**.

## Verificação

A verificação seguiu a sequência completa:

**Source → Build → Live**

### Source

Depois da correção, verificámos os ficheiros Markdown afetados e o `git diff`.

O diff final confirmou que a alteração pretendida se limitava à adição de **uma linha em branco** entre o YAML front matter e o bloco JSON-LD em cada ficheiro afetado.

Os 565 ficheiros afetados foram submetidos no commit:

```text
915f05fa Add spacing between front matter and JSON-LD
```

### Build

Depois da correção, o site foi reconstruído com o Hugo.

A compilação foi concluída com sucesso. Os avisos de depreciação do Hugo já existentes permaneceram, mas não estavam relacionados com o problema dos dados estruturados e não impediram a compilação.

Também verificámos que não permanecia nenhum caso de mojibake após a recuperação da codificação:

```text
Ficheiros com mojibake restantes: 0
```

O conteúdo corrigido foi então enviado para o GitHub:

```text
bde59e67..915f05fa  main -> main
```

### Live

A verificação final e mais importante veio do próprio **Google Search Console**.

Posteriormente, o Google enviou uma confirmação de que o problema tinha sido resolvido:

> **Confirmámos que corrigiu os problemas: Structured data cannot be parsed.**

O erro específico anteriormente comunicado pelo Google era:

> **Falta `}` ou o nome de um membro do objeto**

O Google confirmou a correção na página que voltou a verificar.

Este é o nível mais elevado de verificação disponível neste caso: a origem foi corrigida, o site foi compilado com sucesso, a versão corrigida foi publicada e **o Google Search Console confirmou independentemente que o problema de análise dos dados estruturados tinha sido resolvido no site publicado.**

### Resultado

**Source → corrigido**  
**Build → concluído com sucesso**  
**Live → verificado pelo Google Search Console** ✅

A distinção importante é que as duas primeiras verificações demonstraram que a correção funcionava tecnicamente; a confirmação final do Google demonstrou que **o motor de pesquisa aceitou os dados estruturados corrigidos no site publicado**.

## Conclusão Final

A principal lição é simples: **quando o Google comunica um erro de análise dos dados estruturados, não devemos assumir que o próprio objeto JSON-LD está malformado. É necessário verificar todo o percurso, desde o Markdown de origem até ao HTML gerado.**

Neste caso, uma única linha em branco em falta entre o YAML front matter e um bloco `<script>` JSON-LD foi suficiente para provocar um problema de análise em **565 ficheiros**. A correção foi pequena, mas encontrar a verdadeira causa exigiu verificar os ficheiros de origem, a compilação do Hugo, o HTML gerado e, finalmente, o site publicado através do Google Search Console.

_Por vezes, o erro aponta para o JSON. O verdadeiro problema pode estar imediatamente antes dele._

`Google Search Console` · `dados estruturados` · `JSON-LD` · `Hugo` · `debugging SEO`

**Alt-text:**  
Google Search Console confirma que o problema de análise dos dados estruturados foi resolvido no site publicado.

_Truques de SEO. Quando o Google Search Console Diz: Falta `}` ou o Nome de Um Membro do Objeto. AP | Pivtorak.Studio. 22.09.2026_  
© Anna Pivtorak (Kostyuk)

