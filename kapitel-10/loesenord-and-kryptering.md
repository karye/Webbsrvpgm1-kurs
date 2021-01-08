# Lösenord & kryptering\(?\)

## Skapa tabell

![](../.gitbook/assets/register-tabell.png)

## Registrera användare

```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Inloggning</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="kontainer">
        <header>
            <h1>Inloggning</h1>
        </header>
        <main>
            <?php
            // Ta emot data
            $fnamn = filter_input(INPUT_POST, 'fnamn', FILTER_SANITIZE_STRING);
            $enamn = filter_input(INPUT_POST, 'enamn', FILTER_SANITIZE_STRING);
            $anamn = filter_input(INPUT_POST, 'anamn', FILTER_SANITIZE_STRING);
            $losen = filter_input(INPUT_POST, 'losen', FILTER_SANITIZE_STRING);

            // Kontrollera att POST-variablerna finns, dvs första gången.
            if ($fnamn && $enamn && $anamn && $losen) {

                // Skapa sql-frågan vi skall köra
                $sql = "INSERT INTO register (fnamn, enamn, anamn, hash) VALUES ('$fnamn', '$enamn','$anamn', '$hash')";
                $result = $conn->query($sql);

                // Gick det bra? Kunde SQL-satsen köras?
                if (!$result) {
                    die("Det blev fel med SQL-satsen.");
                } else {
                    echo "<p class=\"alert alert-success\">Användaren <strong>$anamn</strong> registrerad!</p>";
                }

                // Stänger ned anslutningen
                $conn->close();
            }
            ?>
            <form action="#" method="post">
                <label>Förnamn<input type="text" name="fnamn" required></label>
                <label>Efternamn<input type="text" name="enamn" required></label>
                <label>Användarnamn<input type="text" name="anamn" required></label>
                <label>Lösenord<input type="password" name="losen" required></label>
                <button class="btn btn-primary">Registrera</button>
            </form>
        </main>
    </div>
</body>
</html>
```

## Lista alla användare

```php
<main>
    <?php
    // Skapa SQL-frågan
    $sql = "SELECT * FROM register";
    $result = $conn->query($sql);

    // Gick det bra? Kunde SQL-satsen köras?
    if (!$result) {
        die("Något blev fel med SQL-satsen.");
    } else {
        // echo "<p>Användardata kunde hämtas!</p>";
    }

    echo "<table class=\"table table-striped\">";
    echo "<tr>
        <th>Förnamn</th>
        <th>Efternamn</th>
        <th>Användarnamn</th>
        </tr>";

    // Skriv resultatet rad för rad
    while ($rad = $result->fetch_assoc()) {
        echo "<tr>";
        
        // Skriv ut förnamnet inom en cell
        echo "<td>{$rad['fnamn']}</td>";
        // Skriv ut efternamnet inom en cell
        echo "<td>{$rad['enamn']}</td>";
        // Skriv ut användarnamnet inom en cell
        echo "<td>{$rad['anamn']}</td>";
        
        echo "</tr>";
    }
    echo "</table>";

    $conn->close();
    ?>
</main>
```

## Lösenord-hash

```php
// Skapa ett hash från lösenordet
$hash = password_hash($losen, PASSWORD_DEFAULT);
```

## Inloggning

```php
<main>
    <?php
    // Ta emot data
    $anamn = filter_input(INPUT_POST, 'anamn', FILTER_SANITIZE_STRING);
    $losen = filter_input(INPUT_POST, 'losen', FILTER_SANITIZE_STRING);

    // Kontrollera att POST-variablerna finns, dvs första gången.
    if ($anamn && $losen) {

        // Skapa sql-frågan vi skall köra
        $sql = "SELECT * FROM register WHERE anamn = '$anamn';";
        $result = $conn->query($sql);

        // Gick det bra? Kunde SQL-satsen köras?
        if (!$result) {
            die('Det blev fel med SQL-satsen.');
        } else {
            $rad = $result->fetch_assoc();
            if (password_verify($losen, $rad['hash'])) {
                $_SESSION['anamn'] = $anamn;
                echo "<p class=\"alert alert-success\">Du är inloggad!</p>";
            } else {
                echo "<p class=\"alert alert-dismissible alert-warning\">Felaktigt lösenord</p>";
            }
        }

        // Stänger ned anslutningen
        $conn->close();
    } ?>
    <form action="#" method="post">
        <label>Användarnamn
        <input type="text" name="anamn" required></label>
        <label>Lösenord
        <input type="password" name="losen" required></label>
        <button class="btn btn-primary">Logga in</button>
    </form>
</main>
```

