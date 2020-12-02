---
description: Hur man skapar en blogg som har sina inlägg i en tabell
---

# Labb 9 - blogg med databas

## Funktioner i en webbapplikation

### CRUD

* I en webbapplikation pratar om sk CRUD.
* Det betyder hur man hanterar informationen som lagras i webbappen
* Man skall kunna göra följande operationer:
  * Spara information, tex användare, inlägg osv
  * Läsa/söka efter det som lagrats i databasen
  * Kunna redigera det som lagrats
  * Kunna ta bort från databasen det man inte vill behålla

![](../.gitbook/assets/image%20%2875%29.png)



### **Steg 1 - skapa först tabellen i databasen**

* Skapa en ny tabell **blogg** i phpmyadmin:

```sql
CREATE TABLE IF NOT EXISTS blogg (
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  rubrik VARCHAR(255) NOT NULL,
  inlagg TEXT NOT NULL,
  datum TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);
```

### **Steg 2 - skapa en mapp för resurser**

* Skapa en mapp som heter **resurser**
* Skapa anslutningsfilen **conn.php**:

{% tabs %}
{% tab title="conn.php" %}
```php
<?php
$host = "localhost";
$databas = "...";
$användare = "...";
$lösenord = "...";

// 1. Logga in på mysql-servern och välj databas
$conn = new mysqli($host, $användare, $lösenord, $databas);

// Gick det ansluta?
if ($conn->connect_error) {
    die("Kunde inte ansluta till databasen: " . $conn->connect_error);
} else {
    echo "<p>Yipee! Gick bra att ansluta.</p>";
}
```
{% endtab %}
{% endtabs %}

* Och för att skydda mot intrång lägg in följande fil **.htaccess**:

{% tabs %}
{% tab title=".htaccess" %}
```text
Deny from All
```
{% endtab %}
{% endtabs %}

### Steg 3 - skapa en mallsida

* Här inkluderas anslutningsfilen **conn.php**
* [Bootstrap ](https://getbootstrap.com/docs/4.5/getting-started/introduction/)används för att styla sidorna

```php
<?php
include_once "./resurser/conn.php";
?>
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>bloggen</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="kontainer">
        <nav>
            <ul class="nav nav-tabs">
                <li class="nav-item"><a class="nav-link" href="./lasa.php">Läsa</a></li>
                <li class="nav-item"><a class="nav-link active" href="./skriva.php">Skriva</a></li>
                <li class="nav-item"><a class="nav-link" href="./lista.php">Admin</a></li>
            </ul>
        </nav>
    
    </div>
</body>
</html>
```

## Skapa skriptsidorna

### Steg 4 - spara inlägget i databasen

* Spara information motsvarar C:et i **CRUD**
* Skapa en sida **skriva.php** utifrån mallen
* Skapa ett formulär för att mata in blogginläggets text:
  * En inmatningsruta för inläggets rubrik: rubrik
  * En textarea för inläggets text: inlägg
* Se [ett säkrare formulär](https://app.gitbook.com/@karye/s/webbserverpgm-1/~/drafts/-MNOHmuBB97EXQCkbQ9P/kapitel-3/skicka-data-fran-formulaer#en-saekrare-loesning)

{% tabs %}
{% tab title="skriva.php" %}
```php
<form action="#" method="post">
...
</form>
<?php
// Ta emot text från formuläret och spara ned i en textfil.
$rubrik = filter_input(INPUT_POST, 'rubrik', FILTER_SANITIZE_STRING);
$inlagg= filter_input(INPUT_POST, 'inlagg', FILTER_SANITIZE_STRING);

// Finns det data?
if ($rubrik && $inlagg) {

    // 2. Registrera inlägget i tabellen
    $sql = "INSERT INTO blog (rubrik, inlagg) VALUES ('$rubrik', '$inlagg')";
    $result = $conn->query($sql);

    // Gick det bra?
    if (!$result) {
        die("Något blev fel med SQL-satsen.");
    } else {
        echo "<p class=\"alert alert-success\">Inläggets har registrerats.</p>";
    }
}
?>
```
{% endtab %}
{% endtabs %}

### Steg 5 - hämta inläggen från databasen

* Hämta inläggen motsvarar R:et i **CRUD**
* Skapa en sida **lista.php** utifrån mallen
* Hämta alla inlägg från tabellen, se koden nedan
* Presentera inläggen på ett snyggt sätt

```php
<?php
// 2. Ställ en SQL-fråga
$sql = "SELECT * FROM blog";
$result = $conn->query($sql);

// Gick det bra?
if (!$result) {
    die("Något blev fel med SQL-satsen.");
} else {
    echo "<p>Lista på bilar kunde hämtas.</p>";
}

// Presentera resultatet
while ($rad = $result->fetch_assoc()) {
    echo "<p>$rad[rubrik] $rad[inlagg]</p>";
}
?>
```

### Steg 6 - söka efter ett inlägg 

* Hämta inläggen motsvarar R:et i **CRUD**
* Skapa en sida **hitta.php**
  * Den här sidan är en kombination av **skriva.php**
  * .. och **lista.php**
* Skapa ett formulär för att mata in en sökterm
* Hämta alla inlägg från tabellen med utgångspunkt på söktermen
* Presentera inläggen som matchar söktermen på ett snyggt sätt

