---
description: Skapa en webbapp med lagring i textfil
---

# Skapa en enkel blogg

## **Syfte**

* Skriva enkla blogginlägg
* Lagra dessa i en textfil
* Läsa hela bloggen

## **Skapa hemsidan: blogg.html**

```markup
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Min enkla blogg</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootswatch/4.3.1/flatly/bootstrap.min.css">
    <link rel="stylesheet" href="./css/style.css">
</head>
<body>
    <div class="kontainer">
        <header>
            <h1>Bloggen</h1>
            <nav>
                <ul class="nav nav-pills">
                    <li class="nav-item"><a class="nav-link active" href="blogg.html">Hemsida</a></li>
                    <li class="nav-item"><a class="nav-link" href="skriva.html">Skriva inlägg</a></li>
                    <li class="nav-item"><a class="nav-link" href="lasa.php">Läsa inlägg</a></li>
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

## **Skriva in inlägg**

### **Skriva inlägget : skriva.html**

```markup
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Mina enkla blogg</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootswatch/4.3.1/flatly/bootstrap.min.css">
    <link rel="stylesheet" href="./css/style.css">
</head>
<body>
    <div class="kontainer">
        <header>
            <h1>Bloggen</h1>
            <nav>
                <ul class="nav nav-pills">
                    <li class="nav-item"><a class="nav-link" href="blogg.html">Hemsida</a></li>
                    <li class="nav-item"><a class="nav-link active" href="skriva.html">Skriva inlägg</a></li>
                    <li class="nav-item"><a class="nav-link" href="lasa.php">Läsa inlägg</a></li>
                </ul>
            </nav>
        </header>
        <main>
            <form action="spara.php" method="post">
                <textarea class="form-control" name="inlagg" id="inlagg" cols="30" rows="10"></textarea>
                <button class="btn btn-primary">Spara inlägg</button>
            </form>
        </main>
        <footer>
            2020
        </footer>
    </div>
</body>
</html>
```

### **Skriva till en textfil - spara.php**

* Ersätt '...' med rätt PHP-syntax
* Studera
  * Funktionen [isset\(\)](https://devdocs.io/php/function.isset)
  * Funktionen [fopen\(\)](https://devdocs.io/php/function.fopen)
  * Funktionen [fwrite\(\)](https://devdocs.io/php/function.fwrite)

```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Skriva inlägg</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootswatch/4.3.1/flatly/bootstrap.min.css">
    <link rel="stylesheet" href="./css/style.css">
</head>
<body>
    <div class="kontainer">
        <header>
            <h1>Bloggen</h1>
            <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item"><a class="nav-link" href="blogg.html">Hemsida</a></li>
                    <li class="nav-item"><a class="nav-link" href="skriva.html">Skriva inlägg</a></li>
                    <li class="nav-item active"><a class="nav-link" href="lasa.php">Läsa inlägg</a></li>
                </ul>
            </nav>
        </header>
        <main>
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
        </main>
        <footer>
            2019
        </footer>
    </div>
</body>
</html>
```

### **Kontrollera att filen är skrivbar**

* Studera koden nedan och infoga **if**-satserna
* Ersätt '...' med rätt text

```php
<?php
$filnamn = "test.txt";
$texten = "Add this to the file\n";

// Är filens skrivbar?
if (is_writable($filnamn )) {

    // Kan vi öppna filen?
    if (!$handle = fopen($filnamn , 'a')) {
         echo "... ($filename)";
         exit;
    }

    // Skriv något i textfilen
    if (fwrite($handle, $texten ) === FALSE) {
        echo "... ($filnamn)";
        exit;
    } else {
        echo ".. ($texten) .. ($filnamn)";
    }
    fclose($handle);

} else {
    echo "..";
}
?>
```

## **5 Läsa från en textfil - hamta.php**

* Ersätt '...' med rätt PHP-syntax
* Studera:
  * [http://php.net/manual/en/function.file.php](http://php.net/manual/en/function.file.php)
  * [http://php.net/manual/en/function.array-reverse.php](http://php.net/manual/en/function.array-reverse.php)

```php
<!doctype html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <title>Läsa en fil</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Min blogg</h1>
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
</body>
</html>
```

### **6 Visa senaste inläggen överst**

* De inlästa inläggen måste visas i omvänd ordning
* Studera:
  * [http://php.net/manual/en/function.array-reverse.php](http://php.net/manual/en/function.array-reverse.php)

### **7 Skapa en menysida - index.html**

```markup
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8" />
    <title>Enkel blogg</title>
    <link rel="stylesheet" href="">
</head>
<body>
    <h1>Blogg admin</h1>
    <ul>
        <li>Skapa nytt blogginlägg</li>
        <li>Läsa bloggen</li>
        <li>Radera bloggen</li>
    </ul>
</body>
</html>
```

