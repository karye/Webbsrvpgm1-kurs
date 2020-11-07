---
description: Hur skickar man data till ett PHP-skript?
---

# Från formulär till PHP-skript

## Skicka data från formulär till PHP-skript

### Ett formulär 

```php
<div class="container">
    <h1>Två tal</h1>
    <form action="exempel-2.php" method="POST">
        <label for="tal1">Ange tal 1</label>
        <input id="tal1" class="form-control" type="text" name="talet1">
        <label for="tal2">Ange tal 2</label>
        <input id="tal2" class="form-control" type="text" name="talet2">
        <button type="submit" class="btn btn-primary">Skicka</button>
    </form>
</div>
```

### Mottagande skriptet

```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Resultat från formuläret</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <?php
    // läs av skickat tal1 från formuläret
    $tal1 = $_POST["talet1"];
    $tal2 = $_POST["talet2"];

    // Räkna ut summan
    $summa = $tal1 + $tal2;

    // Skriv ut resultatet
    // Summan av 3 + 5 är 8
    echo "<p>Summan av $tal1 + $tal2 är $summa</p>";
    ?>
</body>
</html>
```

## Allt på en-sida: formulär och PHP-skript

* Formuläret skickar tillbaka till sig själv med **action="\#"**
* Men då måste man kontrollera om något kommer in med **if \(isset\(...\)\)**

{% tabs %}
{% tab title="PHP" %}
```php
<div class="container">
    <h1>Spara ditt namn</h1>
    <form action="#" method="POST">
        <label>Ange namn <input type="text" name="namn"></label>
        <button>Spara</button>
    </form>
    <?php
    // Finns data?
    if (isset($_POST["namn"])) {

        // Läs in texten från formuläret
        $namn = $_POST["namn"];

        // Nu gör vi det vi ska
        
    }
    ?>
</div>
```
{% endtab %}

{% tab title="CSS" %}
```
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');

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

h1, h2, h3 {
    color: #9c813d;
}
h1, h2, h3, p {
    margin: 0.5em 0;
}
h3 {
    margin-top: 2em;
}

form {
    margin: 1em 0;
    padding: 1em;
    font-size: 0.9em;
    color: #4e4e4e;
    background: #E6F2F8;
    border-radius: 0.3em;
}
form label {
    display: grid;
    grid-template-columns: 1fr 2fr;
    margin: 10px 0;
    padding: 0;
}
form input, form textarea {
    padding: 0.5em;
    margin-top: -0.4em;
    font-style: italic;
    border-radius: 0.3em;
    border: 2px solid #55a5d2;
    box-shadow: inset 0 2px 2px rgba(0, 0, 0, 0.1);
}
form textarea {
    height: 10em;
}
form button {
    margin: 1em 0;
    padding: 0.7em;
    border-radius: 0.3em;
    border: none;
    font-weight: bold;
    color: #FFF;
    background-color: #55a5d2;
}

table {
    width: 100%;
    border-collapse: collapse;
    margin: 2em 0;
}
table th, table td {
    padding: 0.5em;
    text-align: left;
}
table th {
    background: #305A85;
    color: #FFF;
}
table tr:nth-child(even) {
    background: #E6F2F8;
}
table tr:nth-child(odd) {
    background: #FFF;
}
table .fa {
    color: #55a5d2;
}
```
{% endtab %}
{% endtabs %}

## En säkrare lösning

* Man skyddar mot skadlig kod med [filter-input](https://devdocs.io/php/function.filter-input)

{% tabs %}
{% tab title="PHP" %}
```php
<div class="container">
    <h1>Spara ditt namn</h1>
    <form action="#" method="POST">
        <label>Ange namn <input type="text" name="namn"></label>
        <button>Spara</button>
    </form>
    <?php
    // Ta emot det som skickas
    $namn = filter_input(INPUT_POST, 'namn', FILTER_SANITIZE_STRING);
    
    // Om data finns..
    if ($namn) {
        // Programmets kod
        ...
    }
    ?>
</div>
```
{% endtab %}

{% tab title="CSS" %}
```
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');

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

h1, h2, h3 {
    color: #9c813d;
}
h1, h2, h3, p {
    margin: 0.5em 0;
}
h3 {
    margin-top: 2em;
}

form {
    margin: 1em 0;
    padding: 1em;
    font-size: 0.9em;
    color: #4e4e4e;
    background: #E6F2F8;
    border-radius: 0.3em;
}
form label {
    display: grid;
    grid-template-columns: 1fr 2fr;
    margin: 10px 0;
    padding: 0;
}
form input, form textarea {
    padding: 0.5em;
    margin-top: -0.4em;
    font-style: italic;
    border-radius: 0.3em;
    border: 2px solid #55a5d2;
    box-shadow: inset 0 2px 2px rgba(0, 0, 0, 0.1);
}
form textarea {
    height: 10em;
}
form button {
    margin: 1em 0;
    padding: 0.7em;
    border-radius: 0.3em;
    border: none;
    font-weight: bold;
    color: #FFF;
    background-color: #55a5d2;
}

table {
    width: 100%;
    border-collapse: collapse;
    margin: 2em 0;
}
table th, table td {
    padding: 0.5em;
    text-align: left;
}
table th {
    background: #305A85;
    color: #FFF;
}
table tr:nth-child(even) {
    background: #E6F2F8;
}
table tr:nth-child(odd) {
    background: #FFF;
}
table .fa {
    color: #55a5d2;
}
```
{% endtab %}
{% endtabs %}

