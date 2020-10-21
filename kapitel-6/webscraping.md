---
description: 'Hämta dagens horoskop från https://astro.elle.se'
---

# Webscraping

## Studera webbsidan

### HTML-koden

* Genom att studera HTML-koden ser man vart horoskop-texten ligger

![HTML-koden som inneh&#xE5;ller horoskoptexten](../.gitbook/assets/image%20%2834%29.png)

### Identifiera start

* Nu gäller det att identifiera var börjar HTML-koden

```markup
<div class="c-post_content__wrapper">
```

* För varje månad ligger horoskoptexten i:

```markup
<div class="o-indenter">
```



