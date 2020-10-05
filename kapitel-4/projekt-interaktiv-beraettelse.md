---
description: Skapa en interaktiv berättelse
---

# Projekt 1: interaktiv berättelse

## Interaktiv berättelse

Använd **if-else**-satser tillsammans med det du lärt dig tidigare för att konstruera en interaktiv berättelse med minst två beslut och tre olika slut.

## Flödesschema

Börja med att designa din berättelse. Använd ett enkelt beslutsträd, tex något av dessa:  


![Fl&#xF6;desschema](https://docs.google.com/drawings/u/0/d/sCVbah0fMe_4baeG0KFlTag/image?w=572&h=171&rev=1&ac=1&parent=14wTbpTkwo_McghrUHrnIT7yZQJ79HvoMWTnrXWkoWLM)

## Instruktioner

* Använd **if-else**-satser för att undersöka vilket val spelaren gjort
* Skriv kommentarer i koden om vad de olika koderna gör.
* Minst en klasskamrat ska ha testat din berättelse & ha tittat på koden.

{% tabs %}
{% tab title="berattelse.php" %}
```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Interaktiv berättelse</title>
    <link rel="stylesheet" href="https://cdn.rawgit.com/Chalarangelo/mini.css/v3.0.1/dist/mini-default.min.css">
    <link rel="stylesheet" href="berattelse.css">
</head>
<body>
    <div class="kontainer">
        <h1>Interaktiv berättelse</h1>
        <form action="#" method="POST">
            <label for="...">...</label>
            <input id="..." class="form-control" type="text" name="...">
            <button type="submit" class="btn btn-primary">Skicka</button>
        </form>

        <?php
        // Finns data?
        if (isset($_POST["..."])) {

            // Ta emot data från formuläret
            $... = $_POST["..."];

        }
    </div>
</body>
</html>
```
{% endtab %}

{% tab title="berattelse.css" %}
```
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

## Förbättringar

Om du har tid, fundera över förbättringar, t.ex:

* Lägg in snygga [Emojis](https://emoji-css.afeld.me/)
* Välj färger till texten och bakgrunden
* Prova använda switch

### Avancerat

* Gör så att det inte spelar någon roll vilka stora eller små bokstäver man skriver in mha [strtolower\(\)](https://devdocs.io/php/function.strtolower)
* Gör så att något val har tre alternativ istället för två
* Använd en loop för att se till så att användaren inte kan gå vidare förrän hen skrivit ett svar \(inga tomma svar tex\)

### Ännu mer avancerat

* Lägg in varje “rum” i en egen funktion, och anropa funktion från varandra \(t.ex. att metod2 anropas inuti metod1\)
* Lägg in frågandet i en funktion, som ställer frågan och inte avslutas innan spelaren skrivit in ett giltigt svar. Då returneras valet till koden där metoden anropades

