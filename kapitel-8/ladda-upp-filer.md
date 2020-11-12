# Ladda upp filer\(?\)

## Formuläret

```markup
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <title>Filuppladdning</title>
    <link rel="stylesheet" href="">
</head>
<body>
    <form action="..." method="post" enctype="...">
        <input ...>
        <button ...>Ladda upp!</button>
    </form>
</body>
</html>
```

## PHP-koden

```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <title>Enkel filuppladning</title>
</head>
<body>
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
</body>
</html>
```

