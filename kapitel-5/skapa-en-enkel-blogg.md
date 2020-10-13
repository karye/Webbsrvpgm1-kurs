---
description: Skapa en webbapp med lagring i textfil
---

# Labb 4: blogg

## **Resultat**

![](../.gitbook/assets/dump-labb-4-1.png)

## **Syfte**

* Träna på att läsa in filer 
* Träna på att array och loopar
* Träna på felhantering

## **Startkod**

{% tabs %}
{% tab title="blogg.php" %}
```markup
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Min enkla blogg</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootswatch/4.3.1/minty/bootstrap.min.css">
    <link rel="stylesheet" href="./style.css">
</head>
<body>
    <div class="kontainer">
        <header>
            <h1>Bloggen</h1>
            <nav class="navbar navbar-expand-lg navbar-light">
                <ul class="nav nav-tabs">
                    <li class="nav-item"><a class="nav-link" href="blogg.php">Alla inlägg</a></li>
                    <li class="nav-item"><a class="active nav-link" href="spara.php">Skriva inlägg</a></li>
                </ul>
            </nav>
        </header>
        <main>
            <p class="card text-white bg-warning mb-3">Välkommen till min första webbapp!</p>
        </main>
        <footer>
            2019
        </footer>
    </div>
</body>
</html>
```
{% endtab %}

{% tab title="style.css" %}
```css
@import url('https://fonts.googleapis.com/css?family=Fredoka+One&display=swap');

body {
    background: rgb(255, 255, 255) url("../bilder/bg.jpg");
    background-size: cover;
}

.kontainer {
    background: #FFF;
    width: 800px;
    margin: 50px auto;
    padding: 40px;
    border-radius: 10px;
    box-shadow: 2px 2px 5px;
}
header {
    margin-bottom: 40px;
}
h1 {
    font-family: 'Fredoka One', cursive;
}
nav {
    margin: 10px 0;
}
main p {
    background: #ffffff;
    padding: 20px;
    border-radius: 5px;
    margin: 20px;
}
main form {
    margin: 20px;
}
main button {
    margin: 10px 0;
}

```
{% endtab %}
{% endtabs %}

## **Skriva inlägg**

### **Skriva inlägget : spara.php**

* Ett formulär behövs för att skriva in ett inlägg

```markup
...
<main>
    <form action="#" method="post">
        <textarea class="form-control" name="inlagg" id="inlagg" cols="30" rows="10"></textarea>
        <button class="btn btn-primary">Spara inlägg</button>
    </form>
</main>
...
```

### **Skriva till en textfil - spara.php**

* PHP-skriptet i **spara.php** tar emot data och skall lagra inlägget i en textfil
* Ersätt '...' med rätt PHP-syntax
* Studera
  * Funktionen [isset\(\)](https://devdocs.io/php/function.isset) - se om variabeln finns
  * Funktionen [fopen\(\)](https://devdocs.io/php/function.fopen) - öppna en fil
  * Funktionen [fwrite\(\)](https://devdocs.io/php/function.fwrite) - skriva till en fil

```php
...
<?php
/* Ta emot text från formuläret och spara ned i en textfil. */
if (...($_POST['inlagg'])) {
    $filnamn = "blogg.txt";
    $texten = $_POST["inlagg"];
    $tidpunkt = date('l j F Y h:i:s');

    // Öppna asnslutningen till textfilen
    $handtag = ...($filnamn, "a");

    // Ersätter /n med <br>
    $texten = ...($_POST['inlagg'], false);

    // Skriv text i textfilen
    ...($handtag, "<p>$tidpunkt<br>$texten</p>\n");

    // Stäng anslutningen till textfilen
    ...($handtag);

    echo "<p>Inlägget registrerat!</p>";
} else {
    echo "<p>Inlägg saknas!</p>";
}
?>
...
```

### **Kontrollera att filen är skrivbar**

* För att webbappen inte skall krascha behöver vi kontrollera en del saker
* Studera koden nedan
* Studera också 
  * Funktionen [is\_writable\(\)](https://devdocs.io/php/function.is-writable) - se om filen är skrivbar
* Ersätt '...' med rätt text
* Infoga kontrollerna \(if-satser\) i **spara.php**

```php
<?php
$filnamn = "test.txt";
$texten = "Text som skall sparas ned!\n";

// Är filens skrivbar?
if (is_writable($filnamn )) {

    // Kan vi öppna filen?
    if (!$handle = fopen($filnamn , 'a')) {
         echo "... $filnamn";
         exit;
    }

    // Skriv något i textfilen
    if (fwrite($handle, $texten ) === FALSE) {
        echo "... $filnamn";
        exit;
    } else {
        echo "... ($texten) ... ($filnamn)";
    }
    fclose($handle);

} else {
    echo "...";
}
?>
```

## **Läsa inläggen**

### **Läsa från en textfil - blogg.php**

* Här läses alla inlägg in från textfilen
* Ersätt '...' med rätt PHP-syntax
* Studera:
  * Funktionen [file](https://devdocs.io/php/function.file) - läsa in hela filen

```php
    ...
    <?php
    $filnamn = "blogg.txt";

    // Öppna asnslutningen till textfilen
    $innehall = ...(...);

    // Läs rad för rad i textfilen
    ... ($innehall as $rad) {
        echo "$rad";
    }

    // Stäng anslutningen till textfilen
    ...(...);
    ?>
    ...
```

### **Visa senaste inläggen överst**

* De inlästa inläggen måste visas i omvänd ordning
* Studera:
  * Funktionen [array\_reverse](https://devdocs.io/php/function.array-reverse)

