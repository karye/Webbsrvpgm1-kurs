---
description: Inloggning med modal och ajax-anrop
---

# Login modal

## Resultat

![En modal-ruta kompatibel med Bootstrap](../.gitbook/assets/image%20%2880%29.png)

## Native JavaScript for Bootstrap V4 Github

* [https://thednp.github.io/bootstrap.native/v5.html](https://thednp.github.io/bootstrap.native/v5.html)
* [https://thednp.github.io/bootstrap.native/v5.html\#componentModal](https://thednp.github.io/bootstrap.native/v5.html#componentModal)
* [https://github.com/thednp/bootstrap.native/blob/master/dist/bootstrap-native-v5.min.js](https://github.com/thednp/bootstrap.native/blob/master/dist/bootstrap-native-v5.min.js)

## Webbsidan

{% tabs %}
{% tab title="index.php" %}
```javascript
<?php
/**
 * PHP version 7
 * @category   Ajax för inloggning
 * @author     ...
 * @license    PHP CC
 */
?>
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Inloggning</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="kontainer">
        <h1>Inloggning</h1>
        <button class="btn btn-primary" id="login">Logga in</button>
    </div>

    <div id="modal" class="modal fade" tabindex="-1" role="dialog" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="myModalLabel">Inloggning</h5>
                    <button type="button" class="close" data-bs-dismiss="modal" aria-label="Close">×</button>
                </div>
                <div class="modal-body">
                    <form>
                        <label>Användarnamn <input type="text" name="anamn" required></label>
                        <label>Lösenord <input type="password" name="lösen" required></label>
                        <div class="grid">
                            <button type="submit" class="btn btn-primary">Logga in</button>
                            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Avbryt</button>
                            <div class="result"></div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
```
{% endtab %}

{% tab title="style.css" %}
```css
@import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro|Damion|Roboto+Slab&display=swap');

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
    background: url("./bilder/tim-arterbury-8Jccz5IN7ZM-unsplash.jpg") top center no-repeat;
}
.kontainer {
    width: 700px;
    padding: 2em;
    margin: 1em auto;
    min-height: 89vh;
    background: #c7c7c7c7;
    border-radius: 5px;
    font-family: 'Roboto Slab', serif;
    border: 1px solid #a0a0a0;
    box-shadow: 1px 1px 4px #686868;
}
nav {
    padding: 1em 0;
}
main {
    padding: 1em;
    font-size: 0.9em;
    color: #7b7b7b;
}

nav .anamn {
    margin-left: auto;
    padding: 10px;
    font-weight: bold;
}

form {
    background: #ffffffa3;
    border: 1px solid #a0a0a0;
    padding: 2em;
    border-radius: 5px;
}
form label {
    color: #555555;
    font-weight: bold;
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
form img {
    width: 30px;
}
form .grid {
    display: grid;
    grid-template-columns: 1fr 1fr 2fr;
    gap: 1em;
}
form .result {
    text-align: right;
    color: #cc2a2a;
    font-style: italic;
    align-self: center;
}


h1, h2, h3, h4, h5, h6 {
    font-size: 1em;
    font-weight: bold;
}
h1, h2, h3, p {
    margin: 0.8em 0;
}
h1 {
    color: #ffffff;
    font-size: 3em;
    margin: 0;
    text-shadow: 1px 1px 1px #5c5c5c;
}

table {
    width: 100%;
    border-collapse: collapse;
    border: 1px solid #b89e44;
    background: #ffffffa3;
    padding: 2em;
    border-radius: 5px;
}
th, td {
    padding: 0.5em;
    text-align: left;
}
th {
    background: #FFF;
    padding: 1em 0.5em;
}
tr:nth-child(even) {
    background: #f1f1f1;
}
/* tr:nth-child(odd) {
    background: #FFF;
} */
table .fa {
    color: #55a5d2;
}
table img {
    width: 50px;
}

.inlagg {
    background: #ffffffa3;
    border: 1px solid #b89e44;
    padding: 2em;
    margin-bottom: 2em;
    border-radius: 5px;
}

.modal-body {
    background: burlywood;
}
```
{% endtab %}
{% endtabs %}

### Modal

* Länka in Bootstrap CSS 
* Ladda ned och länka in [Native JavaScript for Bootstrap V4 Github](https://thednp.github.io/bootstrap.native/v5.html)

```markup
<script src="./bootstrap-native-v5.min.js"></script>
```

* Infoga modal-rutans HTML-kod på sidan

```markup
<!-- blank modal template -->
<div id="modal" class="modal fade" tabindex="-1" role="dialog" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="myModalLabel">Inloggning</h5>
                <button type="button" class="close" data-bs-dismiss="modal" aria-label="Close">×</button>
            </div>
            <div class="modal-body">
                <!-- Content goes here -->
            </div>
        </div>
    </div>
</div>
```

### login.js

```javascript
const eModal = document.querySelector("#modal");
const eForm = document.querySelector("form");
const eLogin = document.querySelector("#login");
const eResult = document.querySelector(".result");

// Initialisera modal-fönstret
var myModal = new BSN.Modal(
    '#modal', // target selector
    { // options object
        //content: '<div class="modal-body">Some content to be set on init</div>', // sets modal content
        backdrop: 'static', // we don't want to dismiss Modal when Modal or backdrop is the click event target
        keyboard: false // we don't want to dismiss Modal on pressing Esc key
    }
);

// Öppna modal-fönstret
eLogin.addEventListener("click", function () {
    myModal.show();
});
```

## Formuläret

```markup
<form>
    <label>Användarnamn <input type="text" name="anamn" required></label>
    <label>Lösenord <input type="password" name="lösen" required></label>
    <div class="grid">
        <button type="submit" class="btn btn-primary">Logga in</button>
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Avbryt</button>
        <div class="result"></div>
    </div>
</form>
```

### Test

* Nu skall modal-rutan öppna när man klickar på en knapp med \#login

## Ajax-anrop till servern

* Med ajax kan man kommunicera direkt med ett skript på webbservern istället för att skicka data från ett formulär

### Anropet i från Javascript

* Js-skriptet läser av formuläret och skickar till PHP-skriptet på webbservern
* Js-skriptet presenterar inloggningsvaret för användaren

```javascript
// Hantera inloggning
eForm.addEventListener("submit", function (e) {
    // Hindra form byta sida
    e.preventDefault();

    // Läs in formuläret
    const postData = new FormData(eForm);

    // Anropa backend
    fetch("./ajax/check-user.php", {
        method: "POST",
        body: postData
    })
        //.then(res => res.text())
        //.then(text => console.log(text))
        .then(response => response.json())
        .then(data => {
            switch (data.status) {
                case "ok":
                    console.log(data.meddelande);
                    myModal.hide();
                    eLogin.disabled = true;
                    break;
                case "ej":
                    eResult.innerHTML = data.meddelande;
                    console.log(data.meddelande);
                    break;
                case "fel":
                    console.log(data.meddelande);
                    break;
            }
        })
        .catch(error => {
            console.error("Error:", error);
        })
})
```

### Backend check-user.php

* Skriptet som kollar om användaren finns i databasen

```php
<?php
include_once "../resurser/konfig-db.php";
session_start();

// Ta emot data
$anamn = filter_input(INPUT_POST, 'anamn', FILTER_SANITIZE_STRING);
$lösen = filter_input(INPUT_POST, 'lösen', FILTER_SANITIZE_STRING);

// Kontrollera att POST-variablerna finns, dvs första gången.
if ($anamn && $lösen) {

    // Skapa sql-frågan
    $sql = "SELECT * FROM register WHERE anamn = '$anamn';";
    $result = $conn->query($sql);

    // Gick det bra?
    if (!$result) {
        echo json_encode([
            'status' => 'fel',
            'meddelande' => "Något gick fel"
        ]);
    } elseif ($result->num_rows == 0) {
        echo json_encode([
            'status' => 'ej',
            'meddelande' => "Användaren finns inte"
        ]);
    } else {
        // Hämta användarens data
        $rad = $result->fetch_assoc();

        // Kontrollera att lösenordet motsvarar hash i databasen
        if (password_verify($lösen, $rad['hash'])) {
            echo json_encode([
                'status' => 'ok',
                'meddelande' => "Kunde logga in"
            ]);
        } else {
            echo json_encode([
                'status' => 'ej',
                'meddelande' => "Kunde inte logga in"
            ]);
        }
    }

    // Stänger ned anslutningen
    $conn->close();
}
```

### Rensa formuläret 

```javascript
// Rensa formuläret när modal-fönstret stängs
eModal.addEventListener('hide.bs.modal', function (e) {
    eResult.textContent = '';
    eForm.reset();
}, false);
```

