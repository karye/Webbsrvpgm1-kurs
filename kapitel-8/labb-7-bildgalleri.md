---
description: Hur man enkelt skapar ett bildgalleri oavsett antal bilder
---

# Labb 7 - bildgalleri

## Resultat

![Bildgalleri med karusell](../.gitbook/assets/image%20%2865%29.png)

## Startkod

* Skapa en katalog bilder och spara ned ett antal bilder där
* Skanna katalogen "bilder"

{% tabs %}
{% tab title="PHP" %}
```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Bildgalleri</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="kontainer">
        <?php
        // Ange katalogen
        $katalog = ...;

        echo "<h1>Bildgalleri</h1>";

        // Hämta katalogens innehåll
        $filer = ...;
        
        // Loopa igenom alla funna filer
        foreach ($filer as $fil) {

            // Visa inte ”." och ”.."
            if (...) {
                ...;
            }

            // Visa bara bilden om filformat ”jpg”
            $info = ...;
            if (...) {
                echo "...";
            }
        }
        ?>
    </div>
</body>
</html>
```
{% endtab %}

{% tab title="CSS" %}
```css
@import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro&display=swap');

/* Enkel CSS-reset */
html {
    box-sizing: border-box;
}
*, *:before, *:after {
    box-sizing: inherit;
}
body, h1, h2, h3, h4, h5, h6, p, ul {
    margin: 0;
    padding: 0;
}

body {
    background: #F9F6EB;
}
.kontainer {
    width: 600px;
    padding: 2em;
    margin: 3em auto;
    background: #fff;
    border-radius: 5px;
    font-family: 'Source Sans Pro', sans-serif;
    border: 1px solid #ddd;
    box-shadow: 0 0 12px #f0e9d1;
    color: #4e4e4e;
}

h1, h2, h3 {
    color: #9c813d;
}
h1, h2, h3, p {
    margin: 0.5em 0;
}
h3 {
    margin-top: 2em;
}
img {
    width: 100%;
    box-shadow: 1px 1px 2px #999;
}
```
{% endtab %}
{% endtabs %}

![](../.gitbook/assets/image%20%2866%29.png)

### Skapa rutnät

* Använd CSS grid för att snygga till bildgalleriet

![](../.gitbook/assets/image%20%2864%29.png)

## Bildkarusell från Bootstrap

* Använd [carousel](https://getbootstrap.com/docs/4.5/components/carousel/) för att kunna bläddra mellan bilderna

![](../.gitbook/assets/image%20%2867%29.png)

## Förbättringar

* Visa bildens fotografens namn under bilden
* Slumpa fram 9 bilder ur samlingen

