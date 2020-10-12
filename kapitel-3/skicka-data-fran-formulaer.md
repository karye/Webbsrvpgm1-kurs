---
description: Hur skickar man data till PHP?
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
* Men då måste vi kontrollera om något kommer in med **if \(isset\(...\)\)**

```php
<div class="container">
    <h1>Spara ditt namn</h1>
    <form action="#" method="POST">
        <label>Ange namn</label>
        <input type="text" name="namn">
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

