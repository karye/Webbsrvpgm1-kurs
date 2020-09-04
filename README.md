---
description: Hur man skapar en dynamisk webbsida med PHP
---

# Dynamiska webbsidor

## **Grundstrukturen för en webbsida**

Webbsidor består av kod i språket HTML - Hypertext Markup Language. En minimal webbsida kan se ut enligt följande. PHP-skript skrivs inuti sk PHP-taggar, här testar vi funktionen phpinfo\(\):

```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title></title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <?php
    phpinfo();
    ?>
</body>
</html>
```

