# Labb 9 - blogg med databas

## CRUD

![](../.gitbook/assets/image%20%2875%29.png)



**Skapa först tabellen i databasen**

* Skapa en ny tabell **blogg** i phpmyadmin:

```sql
CREATE TABLE IF NOT EXISTS blogg (
  id int(8) NOT NULL AUTO_INCREMENT PRIMARY KEY,
  title varchar(255) NOT NULL,
  post text NOT NULL
);
```

## **Skapa en mapp för resurser**

### Skydda från internet

* Skapa en mapp som heter **resurser**
* Och lägg in följande fil **.htaccess**:

{% tabs %}
{% tab title=".htaccess" %}
```text
Deny from All
```
{% endtab %}
{% endtabs %}

### Skapa anslutningen

* Skapa anslutningsfilen **conn.php**:

{% tabs %}
{% tab title="conn.php" %}
```php
<?php
$host = "localhost";
$databas = "...";
$användare = "...";
$lösenord = "...";

// 1. Logga in på mysql-servern och välj databas
$conn = new mysqli($host, $användare, $lösenord, $databas);

// Gick det ansluta?
if ($conn->connect_error) {
    die("Kunde inte ansluta till databasen: " . $conn->connect_error);
} else {
    echo "<p>Yipee! Gick bra att ansluta.</p>";
}
```
{% endtab %}
{% endtabs %}

## Mata in i tabellen

### Formuläret

* Skapa ett formulär för att mata in blogginläggets text:
  * Rubrik
  * Text
* Se [ett säkrare formulär](https://app.gitbook.com/@karye/s/webbserverpgm-1/~/drafts/-MNOHmuBB97EXQCkbQ9P/kapitel-3/skicka-data-fran-formulaer#en-saekrare-loesning)

### Registrera i tabellen

{% tabs %}
{% tab title="skriva.php" %}
```php
<div class="kontainer">
    <h1>Bloggen</h1>
    <main>
        <form action="#" method="post">
...
        </form>
        <?php
        // Ta emot text från formuläret och spara ned i en textfil.
        $rubrik = filter_input(INPUT_POST, 'rubrik', FILTER_SANITIZE_STRING);
        $inlagg = filter_input(INPUT_POST, 'inlagg', FILTER_SANITIZE_STRING);

        if ($rubrik && $inlagg) {

            // 2. Registrera inlägget i tabellen
            $sql = "INSERT INTO blog (rubrik, inlagg) VALUES ('$rubrik', '$inlagg')";
            $result = $conn->query($sql);

            // Gick det bra?
            if (!$result) {
                die("Något blev fel med SQL-satsen.");
            } else {
                echo "<p class=\"alert alert-success\">Inläggets har registrerats.</p>";
            }
        }
        ?>
    </main>
</div>
```
{% endtab %}
{% endtabs %}

### Meny

* Med en meny kan man navigera mellan sidorna

```php
<nav>
    <ul class="nav nav-tabs">
        <li class="nav-item"><a class="nav-link" href="./lasa.php">Läsa</a></li>
        <li class="nav-item"><a class="nav-link active" href="./skriva.php">Skriva</a></li>
        <li class="nav-item"><a class="nav-link" href="./lista.php">Admin</a></li>
    </ul>
</nav>
```

