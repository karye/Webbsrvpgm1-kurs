---
description: Välj steg-för-steg komponenterna till din dator
---

# Labb 8 - bygg-din-pc

## Resultat

![](../.gitbook/assets/image%20%2844%29.png)

## Första sidan

### Startkoden

* Första sidan läser bilderna i katalogen för cpu:er
* Bilderna filnamn följer formatet **vara\_pris.jpg/png**

{% tabs %}
{% tab title="steg1.php" %}
```php
<?php
include_once "./funktioner.inc.php";
?>
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Webbshop - steg 1 - cpu</title>
    <link rel="stylesheet" href="shop.css">
</head>
<body>
    <div class="kontainer">
        <h1>Bygg din PC - steg 1</h1>
        <h2>Välj CPU</h2>
        <form action="./steg2.php" method="post">
        <?php
        // Lista alla produkter i katalogen
        $katalog = "...";

        // Hämta katalogens innehåll
        $filer = scandir($katalog);
        
        // Loopa igenom alla filer
        ... {
        
            // Hämta info om filen
            $info = pathinfo(...);
            
            // Är filen av typ 'jpg' eller 'png' visa bilden i en listan
            if (...) {
            
                // Skapa en radioknapp med tillhörande miniatyrbild 
                echo "<label>";
                echo "<input type=\"radio\" name=\"vara\" value=\"$fil\" required>";
                echo "<img src=\"$katalog/$fil\">";
                $vara = vara($fil);
                $pris = pris($fil);
                echo "$vara $pris:-";
                echo "</label>";
            }
        }
        ?>
        <button>Gå till steg 2</button>
        </form>
    </div>
</body>
</html>
```
{% endtab %}
{% endtabs %}

### Include-filen med funktioner

* För att göra koden mer läsbar flyttas två funktioner till en separat fil

{% tabs %}
{% tab title="funktioner.inc.php" %}
```php
<?php
function vara($bilden) {

    /* Plocka ut del före punkten */
    $delar1 = explode('.', $bilden);

    /* Dela upp efter _ */
    $delar2 = explode('_', $delar1[0]);

    /* Plocka ut sista delen = priset */
    array_pop($delar2);

    /* Slå ihop övriga delar till varans namn */
    $vara = implode(' ', $delar2);

    return $vara;
}
function pris($bilden) {

    /* Plocka ut del före punkten */
    $delar1 = explode('.', $bilden);

    /* Dela upp efter _ */
    $delar2 = explode('_', $delar1[0]);

    /* Plocka ut sista delen = priset */
    $pris = array_pop($delar2);

    return $pris;
}
?>
```
{% endtab %}
{% endtabs %}

## Andra sidan

### steg2.php

```php
<?php
include_once "./funktioner.inc.php";
?>
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Webbshop - steg 1 - cpu</title>
    <link rel="stylesheet" href="shop.css">
</head>
<body>
    <div class="kontainer">
        <h1>Bygg din PC - steg 2</h1>
        <h2>Välj kylare</h2>
        <form action="./steg3.php" method="post">
            <?php
            // Lista alla produkter i katalogen
            $katalog = "...";
    
            // Hämta katalogens innehåll
            $filer = scandir($katalog);
            
            // Loopa igenom alla filer
            ... {
            
                // Hämta info om filen
                $info = pathinfo(...);
                
                // Är filen av typ 'jpg' eller 'png' visa bilden i en listan
                if (...) {
                
                    // Skapa en radioknapp med tillhörande miniatyrbild 
                    echo "<label>";
                    echo "<input type=\"radio\" name=\"vara\" value=\"$fil\" required>";
                    echo "<img src=\"$katalog/$fil\">";
                    $vara = vara($fil);
                    $pris = pris($fil);
                    echo "$vara $pris:-";
                    echo "</label>";
                }
            }
            ?>
            <button>Gå till steg 3</button>
        </form>
        <h2>Varukorg</h2>
        <?php
        // Visa innehållet på varukorgen = varukorg.txt
        $varukorg = "...";

        // Ta emot data som skickas
        $vara = filter_input(INPUT_POST, 'vara', FILTER_SANITIZE_STRING);
        if ($vara) {
        
            // Spara ned i varukorg.txt
            $handtag = fopen($varukorg, 'w');
            fwrite($handtag, "$vara\n");
            fclose($handtag);
        }

        // Är filens läsbar
        if (is_readable($varukorg)) {
            
            // Läs in textfilen varukorg.txt i en array
            $rader = file($varukorg);
            $total = 0;

            // Skriv ut som tabell
            echo "<table>";
            echo "<thead>";
            echo "<tr><th>Vara</th><th>Pris</th></tr>";
            echo "</thead>";
            echo "<tbody>";
            foreach ($rader as $rad) {
                $vara = vara($rad);
                $pris = pris($rad);
                $total = $total + $pris;
                echo "<tr><td>$vara</td><td>$pris:-</td></tr>";
            }
            echo "</tbody>";
            echo "<tfoot>";
            echo "<tr><td>Total</td><td>$total:-</td></tr>";
            echo "</tfoot>";
            echo "</table>";
        } else {
            echo "<p>Varukorgen saknas!</p>";
        }
        ?>
        <a class="knapp" href="steg1.php">Börja om!</a>
    </div>
</body>
</html>
```

