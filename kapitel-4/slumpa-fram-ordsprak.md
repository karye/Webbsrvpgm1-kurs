---
description: Slumpa fram sex olika ordspråk från en lista av tio
---

# Labb 1: slumpa fram ordspråk

## **Resultatet**

![](../.gitbook/assets/image%20%288%29.png)

## **Syfte**

* Träna slumpa fram 6 ordspråk
* Träna på array och loopar

## **Startkod**

### Slumpa fram ett ordspråk

* Välj ut 10 ordspråk från [svenska\_ordspråk](https://sv.wikipedia.org/wiki/Lista_%C3%B6ver_svenska_ordspr%C3%A5k)
* Referens till funktioner som används:
  * Funktionen[ array\(\)](https://devdocs.io/php/function.array)
  * Funktionen [rand\(\)](https://devdocs.io/php/function.rand)

{% tabs %}
{% tab title="ordsprak.php" %}
```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Slumpa fram sex ordspråk</title>
    <link rel="stylesheet" href="https://cdn.rawgit.com/Chalarangelo/mini.css/v3.0.1/dist/mini-default.min.css">
    <link rel="stylesheet" href="ordsprak.css">
</head>
<body>
<?php
    // Skapa en array med tio ordspråk
    $ordsprak[] = "Blyga pojkar får aldrig kyssa vackra flickor.";
    ...

    // Slumpa fram ett tal mellan 0 och 9 med funktionen rand()
    $index = ...;

    // Skriv ut ordspråket 
    echo ...;
?>
</body>
</html>
```
{% endtab %}

{% tab title="ordsprak.css" %}
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

li {
    margin-bottom: 5px;
}

table {
    width: 100%;
    border-collapse: collapse;
    margin: 2em 0;
}
th, td {
    padding: 0.5em;
    text-align: left;
}
th {
    background: #305A85;
    color: #FFF;
}
tr:nth-child(even) {
    background: #E6F2F8;
}
tr:nth-child(odd) {
    background: #FFF;
}
table .fa {
    color: #55a5d2;
}
table img {
    width: 50px;
}

form img {
    width: 30px;
}
form label {
    display: flex;
    align-items:center;
}
form span {
    padding: 10px;
}
```
{% endtab %}
{% endtabs %}

## Steg 1

### Slumpa fram 6 ordspråk

* Skriv nu ut 6 ordspråk genom att upprepa koden 6 ggr
* Referens till funktioner som används:
  * Kontrollkommando [for-loop](https://devdocs.io/php/control-structures.for)

{% tabs %}
{% tab title="ordsprak.php" %}
```php
// for-loop som går 6 varv för att vi vill skriva ut 6 ordspråk
... {
    
    // Slumpa fram ett tal mellan 0 och 9 med funktionen rand()
    $index = ...;

    // Skriv ut ordspråket 
    echo ...;
}
```
{% endtab %}
{% endtabs %}

## Steg 2

### Skapa en numrerad lista

* Skriv ut ordspåken som en lista

```php
// <ol>
echo "<ol>";
..
echo "<li>...</li>";
..
echo "</ol>";
```

## Steg 3

### Se till att ordspråk inte skrivs ut igen

* Kontrollera att ordspråket inte redan skrivits ut

### Skapa en ny array för att lagra alla tagna ordspråk

```php
// En kontroll-array där vi lagrar vilka ordspråk vi skrivit ut
$tagna = [];
```

### Kontrollera att ordspråket inte redan tagits

* Referens till funktioner som används:
  * Funktionen [in-array](https://devdocs.io/php/function.in-array)

```php
// Skriv ut om den inte finns i arrayen $tagna
// Kontrollera med funktionen in_array()
if (...) {
    
    // Skriv ut ordspråket 
    echo "...";
    
    // Lagra positionen i arrayen $tagna
    ...;
} else {
    
    // Backa $i med 1
    ...;
}
```

