---
description: Läsa från textfil och "parsa" data som är csv-formaterat.
---

# Labb 3: läsa in csv-fil

## Resultatet

![](../.gitbook/assets/image%20%2810%29.png)

## **Syfte**

* Träna på att läsa filer 
* Träna på att array och loopar
* Träna på felhantering

## Läs in csv-filen

* Webbapplikationen skall läsa in innehållet i filen **restauranger.csv**
* Och skriva ut alla rader
* Referens till funktioner som används:
  * Funktionen [file\(\)](https://devdocs.io/php/function.file)
  * Funktionen[ ](https://devdocs.io/php/function.array)[foreach](https://devdocs.io/php/control-structures.foreach)

{% tabs %}
{% tab title="lista.php" %}
```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Skriv ut csv-fil</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="kontainer">
        <h1>Alla restauranger</h1>
        <?php
        $filnamn = # kod...;

        // Läs in hela filen i en sträng: file()
        $rader = # kod...;

        // Loopa igenom alla rader
        # kod..

            // Skriv ut raden
            echo $rad;
        
        ?>
    </div>
</body>
</html>
```
{% endtab %}

{% tab title="style.css" %}
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
table {
    font-size: 0.8em;
}
table th {
    background: #305A85;
    color: #FFF;
}
```
{% endtab %}

{% tab title="restauranger.csv" %}
```text
Bagel Street Cafe, Kungsgatan 42, 11156, Stockholm
Café Cups, Fleminggatan 18, 11226, Stockholm
Dagobert restaurang, Roslagsgatan 7, 113 55, Stockholm
Falafel Kungen, Sveavägen 71, 11350, Stockholm
G&E Pizzeria / Vasa La grande, Dalagatan 32, 11324, Stockholm
Göran Terrassen, Sankt Göransplan 1, 11219, Stockholm
Il Piccio Ristorante, Fridhemsgatan 3, 11240, Stockholm
Kebab Kungen, Odengatan 54, 11322, Stockholm
Mam Restaurang, Hagagatan 44, 11347, Stockholm
Nybergs Konditori, Upplandsgatan 26, 11326, Stockholm
O´Mamma Mia, Kungstensgatan 60, 11329, Stockholm
Restaurang Aroti, Wallingatan 40, 11124, Stockholm
Sterix, Polhemsgatan 50, 11230, Stockholm
Subway Hötorget, Subway Hötorget T-bana, 11156, Stockholm
Subway Karlbergsvägen, Karlbergsvägen 16, 11327, Stockholm
Subway Sankt Eriksplan, Sankt Eriksplan 17, 11320, Stockholm
Subway Sveavägen/Olofsgatan, Sveavägen 33, 11134, Stockholm
Subway, Odengatan 49, 11351, Stockholm
Sushirullen Odenplan, Norrtullsgatan 10, 11327, Stockholm
Taco Bar Sveavägen, Sveavägen 108, 11350, Stockholm
TacoBar, Sankt Eriksplan 5, 11320, Stockholm
Valkyria, Crafoordsv 12, 11324, Stockholm
```
{% endtab %}
{% endtabs %}

## Skriv ut i tabellform

* Skriv nu ut alla rader i tabellform istället
* Använd [Bootstrap](https://getbootstrap.com/docs/4.5/content/tables/) för att göra varannan tabellrad med olika bakgrundsfärg

{% tabs %}
{% tab title="lista.php" %}
```php
<?php
echo "<table>";
echo "<tr><th>Restaurang</th></tr>";

// Loopa igenom alla rader
# kod...

echo "</table>";
?>
```
{% endtab %}
{% endtabs %}

## Kontrollera att filen finns och är läsbar

* Skapa ett felmeddande om filen ej går att hitta eller läsa
* Använd [Bootstrap alerts](https://getbootstrap.com/docs/4.5/components/alerts/) för att styla felmeddelandet
* Referens till funktioner som används:
  * Funktionen [is\_readable\(\)](https://devdocs.io/php/function.is-readable)

{% tabs %}
{% tab title="lista.php" %}
```php
<?php
$filnamn = # kod...;

// Om filen läsbar skriv ut alla tabellrader
# kod...

// Annars skriv ut felmeddelande 
# kod...
?>
```
{% endtab %}
{% endtabs %}

## Mer detaljerad tabell

* Dela upp raderna i dess delar: Namn, Gata, Postnr, Postort
* Referens till funktioner som används:
  * Funktionen [explode\(\)](https://devdocs.io/php/function.explode)

```php
echo "<tr><th>Namn</th><th>Gata</th><th>Postnr</th><th>Postort</th></tr>";
# kod...
    // Dela upp raden
    $delar = # kod...;

    // Skriv ut tabellrad
    echo "<tr><td>$delar[0]</td><td>$delar[1]</td><td>$delar[2]</td><td>$delar[3]</td></tr>";
# kod...
```

