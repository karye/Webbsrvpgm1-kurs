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

* Skapa anslutningsfilen conn.php:

{% tabs %}
{% tab title="conn.php" %}
```sql
<?php
$host = "localhost";
$databas = "...";
$användare = "...";
$lösenord = "...";

/* 1. Logga in på mysql-servern och välj databas */
$conn = new mysqli($host, $användare, $lösenord, $databas);

/* Gick det ansluta? */
if ($conn->connect_error) {
    die("Kunde inte ansluta till databasen: " . $conn->connect_error);
} else {
    //echo "<p>Yipee! Gick bra att ansluta.</p>";
}
```
{% endtab %}
{% endtabs %}

