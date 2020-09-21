---
description: Slumpa fram sex olika ordspråk från en lista av tio
---

# Slumpa fram ordspråk

## **Syfte**

* Referens till funktioner som används:
  * Funktionen [rand\(\)](https://devdocs.io/php/function.rand)
  * Funktionen [for-loopar](https://devdocs.io/php/control-structures.for)
  * Funktionen[ array\(\)](https://devdocs.io/php/function.array)

### **ordsprak.php**

* Välj ut 10 ordspråk från [Lista\_över\_svenska\_ordspråk](https://sv.wikipedia.org/wiki/Lista_%C3%B6ver_svenska_ordspr%C3%A5k)
* Slumpa fram 6 ordspråk

```php
<?php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Slumpa fram sex ordspråk</title>
</head>
<body>
<?php
    // Skapa en array med tio ordspråk
    $ordsprak[] = "Blyga pojkar får aldrig kyssa vackra flickor.";
    $ordsprak[] = "Borta bra men hemma bäst.";
    $ordsprak[] = "Bra karl reder sig själv.";
    $ordsprak[] = "Bränt barn skyr elden.";
    $ordsprak[] = "Bättre att förekomma än förekommas.";
    $ordsprak[] = "Bättre brödlös än rådlös.";
    $ordsprak[] = "Bättre en fågel i handen än tio i skogen.";
    $ordsprak[] = "Bättre ensam än i dåligt sällskap.";
    $ordsprak[] = "Bättre fly än illa fäkta.";
    $ordsprak[] = "Bättre föregå än föregås.";

    // for-loop som går 6 varv för att vi vill skriva ut 6 ordspråk
    for ($i = ..; $i < ..; $i++) {
        
        // Slumpa fram ett tal mellan 0 och 9 med funktionen rand()
        $index = ...;

        // Skriv ut ordspråket 
        echo "<p>$ordsprak[$index]</p>";
    }
?>
</body>
</html>
```

### Kontrollera att ordspråket inte redan valts ut

* Skapa en ny array för att lagra alla tagna ordspråk

```php
// En kontroll-array där vi lagrar vilka ordspråk vi skrivit ut
$tagna = [];
```

* Kontrollera att ordspråket inte redan tagits

```php
// Skriv ut om den inte finns i arrayen $tagna
// Kontrollera med funktionen in_array()
if (...) {
    
    // Skriv ut ordspråket 
    echo "<p>$ordsprak[$index]</p>";
    
    // Lagra positionen i arrayen $tagna
    ...;
} else {
    
    // Backa $i med 1
    ...;
}
```

