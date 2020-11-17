---
description: Hur man laddar en fil till servern
---

# Ladda upp filer

## Youtube tutorial

{% embed url="https://youtu.be/JaRq73y5MJk" %}

## Formuläret

* Först behöver man ett formulär
* Formuläret har ett extra attribut **enctype**
* Och input skall vara av typ **file**

{% tabs %}
{% tab title="form.html" %}
```markup
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <title>Filuppladdning</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <form action="..." method="POST" enctype="...">
            <input type="...">
            <button ...>Ladda upp!</button>
        </form>
    </div>
</body>
</html>
```
{% endtab %}

{% tab title="style.css" %}
```
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');

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

form {
    margin: 1em 0;
    padding: 1em;
    font-size: 0.9em;
    color: #4e4e4e;
    background: #E6F2F8;
    border-radius: 0.3em;
}
form label {
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

table {
    width: 100%;
    border-collapse: collapse;
    margin: 2em 0;
}
table th, table td {
    padding: 0.5em;
    text-align: left;
}
table th {
    background: #305A85;
    color: #FFF;
}
table tr:nth-child(even) {
    background: #E6F2F8;
}
table tr:nth-child(odd) {
    background: #FFF;
}
table .fa {
    color: #55a5d2;
}
```
{% endtab %}
{% endtabs %}

## PHP-koden

{% tabs %}
{% tab title="upload.php" %}
```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <title>Enkel filuppladning</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <?php
            // Skickas filer?
            if (...($_POST['submit'])) {
                $file = $_FILES['file'];
    
                $fileName = ...
                $fileTmpName = ...;
                $fileSize = ...;
                $fileError = ...;
                $fileType = ...;
    
                $fileExt = ...('.', ...);
                $fileActualExt = ...(end($fileExt));
                $allowedExt = ['jpg', 'jpeg', 'png'];
    
                if (in_array(...)) {
                    if (...) {
                        if (...) {
                            ...
                        } else {
                            echo "<p>Filen är för stor!</p>";
                        }
                    } else {
                        echo "<p>Det blev ett fel: $fileError</p>";
                    }
                } else {
                    echo "<p>Du kan inte ladda filer av typen $fileActualExt</p>";
                }
            }
        ?>
    </div>
</body>
</html>
```
{% endtab %}
{% endtabs %}

