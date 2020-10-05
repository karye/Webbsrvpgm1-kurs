---
description: Omvandla text till morsekod
---

# Labb 2: omvandla till morse

## **Resultatet**

![](../.gitbook/assets/image%20%2812%29.png)

## **Syfte**

* Träna på associativ array
* Träna på foreach-loop

## **Startkod**

* Först grundkoden för formuläretet 
* .. och ta emot det som formuläret skickar

{% tabs %}
{% tab title="ordsprak.php" %}
```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Text till morsekod</title>
    <link rel="stylesheet" href="https://cdn.rawgit.com/Chalarangelo/mini.css/v3.0.1/dist/mini-default.min.css">
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="kontainer">
        <h1>Omvandla text till morsekod</h1>
        <form action="#" method="POST">
            <textarea name="texten" cols="30" rows="10"></textarea>
            <button type="submit" class="btn btn-primary">Skicka</button>
        </form>
        <?php
        // Finns data?
        if (isset($_POST["..."])) {

            // Ta emot data från formuläret
            # kod... = $_POST["..."];

        }
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
    height: 10em;
    width: 100%;
}
button {
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

{% tab title="morse.js" %}
```javascript
var AudioContext = window.AudioContext || window.webkitAudioContext;
var ctx = new AudioContext();
var dot = 1.2 / 15;

document.getElementById("demo").onsubmit = function() {
    var t = ctx.currentTime;

    var oscillator = ctx.createOscillator();
    oscillator.type = "sine";
    oscillator.frequency.value = 600;

    var gainNode = ctx.createGain();
    gainNode.gain.setValueAtTime(0, t);

    this.code.value.split("").forEach(function(letter) {
        switch (letter) {
            case ".":
                gainNode.gain.setValueAtTime(1, t);
                t += dot;
                gainNode.gain.setValueAtTime(0, t);
                t += dot;
                break;
            case "-":
                gainNode.gain.setValueAtTime(1, t);
                t += 3 * dot;
                gainNode.gain.setValueAtTime(0, t);
                t += dot;
                break;
            case " ":
                t += 7 * dot;
                break;
        }
    });

    oscillator.connect(gainNode);
    gainNode.connect(ctx.destination);

    oscillator.start();

    return false;
}
```
{% endtab %}
{% endtabs %}

## Steg 1

* Omvandla texten till versaler
* Plocka isär texten i bokstäver

{% tabs %}
{% tab title="ordsprak.php" %}
```php
<?php
{
    // Ta emot data från formuläret
    # kod... = $_POST["..."];

    // Omvandla texten till versaler strtoupper()
    # $texten = kod...
    
    // Dela upp texten i dess bokstäver str_split()
    # $bokstäver = kod...
    
}
?>
```
{% endtab %}
{% endtabs %}

## Steg 2

{% tabs %}
{% tab title="ordsprak.php" %}
```php
<?php
{
    // Ta emot data från formuläret
    # kod... = $_POST["..."];

    // Omvandla texten till versaler strtoupper()
    # $texten = kod...
    
    // Dela upp texten i dess bokstäver str_split()
    # $bokstäver = kod...
    
    // Loopa igenom texten bokstav-för-bokstav
    # kod... {

        // Skriv ut bokstaven
        # kod...
    }
}
?>
```
{% endtab %}
{% endtabs %}

## Steg 3

* Infoga [morsealfabetet](https://morsealfabetet.se/)

{% tabs %}
{% tab title="ordsprak.php" %}
```php
<?php
{
    // Ta emot data från formuläret
    # kod... = $_POST["..."];

    // Morsealfabetet A-Z och mellanslag
    $morse['A'] = '.-';
    # kod...

    // Omvandla texten till versaler strtoupper()
    # $texten = kod...
    
    // Dela upp texten i dess bokstäver str_split()
    # $bokstäver = kod...
    
    // Loopa igenom texten
    # kod... {

        // Skriv ut bokstavens morsekod
        # kod...
    }
}
?>
```
{% endtab %}
{% endtabs %}

## Steg 4

* Koppla in ett js-skript för att spela up morse-koden

{% tabs %}
{% tab title="ordsprak.php" %}
```php
        <?php
        {
            // Ta emot data från formuläret
            # kod... = $_POST["..."];
            # kod...
            
            
            // Loopa igenom texten
            echo "<form id=\"demo\"><label>$texten</label><input type=\"text\" pattern=\"[.\- ]+\" name=\"code\" value=\"";
            # kod...
            # kod...
            # kod...
            echo "\"><button>Spela upp</button></form>";
        }
        ?>
    </div>
    <script src="morse.js"></script>
</body>
</html>
```
{% endtab %}
{% endtabs %}

## Förbättringar

### Hantera åäö

* Använd följande funktion, dvs **m\_str\_split\($texten\)** istället **str\_split\($texten\)**

```php
    // För att hantera texten med svenska tecken
    function mb_str_split($str, $l = 1) {
        if ($l > 0) {
            $ret = array();
            $len = mb_strlen($str, "UTF-8");
            for ($i = 0; $i < $len; $i += $l) {
                $ret[] = mb_substr($str, $i, $l, "UTF-8");
            }
            return $ret;
        }
        return preg_split("//u", $str, -1, PREG_SPLIT_NO_EMPTY);
    }
```

