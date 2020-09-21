# Slumpa fram ordspråk

## **Syfte**

* Slumpa fram sex olika ordspråk från en lista av tio
* Referens till funktioner:
  * Funktionen [rand\(\)](http://php.net/manual/en/function.rand.php)
  * Funktionen [for-loopar](http://php.net/manual/en/control-structures.for.php)
  * Funktionen [array\(\)](http://php.net/manual/en/function.in-array.php)

### **ordsprak.php**

* Slumpa fram 6 ordspråk

```php
<?php
/**
* Slumpar fram ordspråk
*
* PHP version 5
* @category   Enkel skriptsida
* @author     ...
* @license    PHP CC
* @link
*/
?>
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
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

### Kontrollera att ordspråket 

* Skapa en ny array för att lagra alla tagna  ordspråk

```php
    // En kontroll-array där vi lagrar vilka ordspråk vi skrivit ut
    $tagna= array();
```

* Kontrollera att ordspråket inte redan plockats

```php
        // Skriv ut om den inte finns i arrayen $tagna
        // Kontroll mha funktionen in_array()
        if (...) {
            
            // Skriv ut ordspråket 
            echo "<p>$ordsprak[$index]</p>";
            
            // Lagra positionen i arrayen $tagna
            ...;
        } else {
            
            // Minska $i med 1
            ...;
        }
```



