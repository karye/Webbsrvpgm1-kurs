---
description: 'Hämta dagens horoskop från https://astro.elle.se'
---

# Webscraping

## Studera webbsidan

### HTML-koden

* Genom att studera HTML-koden ser man vart horoskop-texten ligger

![HTML-koden som inneh&#xE5;ller horoskoptexten](../.gitbook/assets/image%20%2834%29.png)

### Identifiera start

* Nu gäller det att identifiera var börjar horoskopet i HTML-koden:

```markup
<div class="c-post_content__wrapper">
```

* Varje månad ligger sedan inuti:

```markup
<div class="o-indenter">
```

## Strategi för webscrapping

### Sökstrategi

* Man börjar med att söka efter **c-post\_content\_\_wrapper**

### Och var den slutar

* Horoskopen när denna klass dyker upp **c-post\_tag**

## Testa strategin

{% tabs %}
{% tab title="astro.php" %}
```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Dagens horoskop</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="kontainer">
        <?php
        echo "<h1>Dagens horoskop</h1>";

        // Hämta sidan
        $sidan = file_get_contents("https://astro.elle.se");

        // Sök början på texten
        $start = strpos($sidan, "c-post_content__wrapper") ;
        if ($start !== false) {
            echo "<p>Horoskopet började på position $start</p>";
        } else {
            echo "<p>Hittade inte horoskopets början!</p>";
        }
        
        // Hitta var horoskopet slutar
        $slut = strpos(...);
        
        // Plocka ut ungefär delen med horoskoptexten
        $horoskopText = substr(...);
        
        ?>
    </div>
</body>
</html>
```
{% endtab %}

{% tab title="style.css" %}
```css
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
    font-family: 'Open Sans', sans-serif;
    border: 1px solid #ddd;
    box-shadow: 0 0 12px #f0e9d1;
    color: #4e4e4e;
}
.kol2 {
    margin: 1em 0;
    display: grid;
    grid-template-columns: 1fr 2fr;
    grid-gap: 1em;
}
.kol3 {
    margin: 1em 0;
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    grid-gap: 1em;
}
form {
    margin: 1em 0;
    color: #4e4e4e;
}
label {
    text-align: right;
    align-self: center;
    font-size: 0.9em;
}
input, textarea {
    padding: 0.7em;
    border-radius: 0.3em;
    border: 1px solid #ccc;
    font-weight: bold;
    box-shadow: inset 0 2px 2px rgba(0, 0, 0, 0.1);
}
textarea {
    height: 5em;
    width: 100%;
}
button {
    margin: 1em 0;
    padding: 0.7em;
    border-radius: 0.3em;
    border: none;
    font-weight: bold;
    color: #FFF;
    background-color: #55a5d2;
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
```
{% endtab %}
{% endtabs %}

## Horoskopet

### Vädurens horoskop

* Första div-boxen börjar med **&lt;div class="o-indenter"&gt;**
* och slutar med **&lt;/div&gt;**
* Så här plockar man ut rubriken **Väduren**

```php
// första delen före annonsen
$start = strpos($horoskopText, ...);
$slut = strpos($horoskopText, ...);
$del1 = substr($horoskopText, ...);
echo "$del1</div>\n";
```

* Upprepa en gång till för att plocka ut Vädurens horoskop
* Upprepa så många gånger det behövs att få ut all horoskop text

