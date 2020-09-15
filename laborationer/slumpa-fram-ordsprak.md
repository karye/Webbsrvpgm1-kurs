# Slumpa fram ordspråk

## **Syfte**

* Slumpa fram sex olika ordspråk från en lista av tio
* Referens till funktioner på [http://php.net](http://php.net/):
  * [http://php.net/manual/en/function.rand.php](http://php.net/manual/en/function.rand.php)
  * [http://php.net/manual/en/control-structures.for.php](http://php.net/manual/en/control-structures.for.php)
  * [http://php.net/manual/en/function.in-array.php](http://php.net/manual/en/function.in-array.php)

### **ordsprak.php**

* Ersätt '...' med rätt PHP-syntax

```php
<?php
/**
* Slumpar fram ordspråk
*
* PHP version 5
* @category   Enkel skriptsida
* @author     Karim Ryde <karye.webb@gmail.com>
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
    
    // En kontroll-array där vi lagrar vilka ordspråk vi skrivit ut
    $kontrol[] = array();

    // for-loop som går 5 varv för att vi vill skriva ut 6 ordspråk
    ... ($i = 1; $i < 6; $i++) {
        
        // Slumpa fram ett tal mellan 0 och 9 med funktionen rand()
        $index = ...;

        // Skriv ut om den inte finns i arrayen $kontroll, kontroll mha funktionen in_array()
        if (...) {
            
            // Skriv ut ordspråket 
            echo "<p>$ordsprak[$index]</p>";
            
            // Lagra positionen i arrayen $kontroll
            ...;
        } else {
            
            // Minska $i med ett
            ...;
        }
    }

?>
</body>
</html>
```
