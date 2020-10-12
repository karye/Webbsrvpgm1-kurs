---
description: Enklare med bara formulär och PHP-skript på samma sida
---

# Skicka data från formulär

## Exempel på 

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

