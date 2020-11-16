---
description: Bra och användbart att veta.
---

# Obs! svenskt språkstöd

## Datum på svenska

### Inbyggda datum-funktionen

[date\(\)](https://devdocs.io/php/function.date) ger oss ett svar på engelska:

```php
<?php
$datum = date("l y F");
echo "<p>$datum</p>";
?>
```

### Växla språkstöd

För att få svar på svenska måste vi ange svenska **locale** med funktionen [setlocale\(\)](https://devdocs.io/php/function.setlocale). Sen formaterar vi datumet mha [strftime\(\)](https://devdocs.io/php/function.strftime):

```php
<?php
setlocale(LC_ALL, "sv_SE.utf8");
$dagensDatum = strftime("%A %y %B");
echo "<p>På svenska blir det: $dagensDatum</p>";
echo "<p>Man kan ju börja med stor bokstav: " . ucwords($dagensDatum) . "</p>";
?>
```



