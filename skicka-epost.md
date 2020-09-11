---
description: Det svåra konsten att skicka epost
---

# Skicka epost

## **SMTP-protokollet skickar epost**

**SMTP** står för Simple Mail Transfer Protocol och är protokollet som används varje gång man skickar iväg ett epost-meddelande. Det finns flera serverprogramvaror som är gjorda för att hantera ivägskickandet av epost. **sendmail**, **postfix** och **exim** hör till de vanligaste **SMTP**-servrarna. För att php ska kunna epost till **SMTP**-servern behöver vi tala om sökvägen till servern i **php.ini**:

```bash
sendmail_path = /usr/bin/sendmail
```

Använder du **Windows** följer oftast inte någon **SMTP**-server med. Då behöver du ställa in den separata **SMTP**-server som php ska ta kontakt med - enklast är att använda din internetleverantörs **SMTP**-server. Vilken adress det är varierar, exempelvis är adressen smtprelay1.telia.com till Telias **SMTP**-server.

```bash
SMTP = smtprelay1.telia.com;
sendmail_from = 'dinmailadress@telia.com>'
```

Eposten förs över helt som text, detta för att bibehålla kompabilitet med gamla system. Före själva meddelandet kommer meddelanderubrikerna. Av dessa är tre stycken obligatoriska:

| **From** | Talar om vem som skickade eposten: ex: &lt;thomas@snt.se&gt; |
| :--- | :--- |
| **To** | Talar om till vem meddelandet ska |
| **Date** | Talar om när epost-meddelandet skickades |
| **Subject** | Vad epost-meddelandet handlar om \(används nästan alltid men är inte obligatorisk\) |

Förutom dessa rubriker finns ett antal andra meddelanderubriker som brukar förekomma i epost.

### **Funktionen mail**

PHP har en enkel funktion för att skicka epost, som fyndigt nog heter **mail\(\)**. se [http://php.net/manual/en/function.mail.php](http://php.net/manual/en/function.mail.php) . Den används på detta sätt:

```php
$amne = "Viktigt meddelande";
$mottagare = "test@test.se";
$avsandare = "From: thomas@snt.se\n";
$meddelandetext = "Testar att skicka e-post\n med PHP";
mail($mottagare, $amne, $meddelandetext, $avsandare);
```

### **PHPMailer**

För alla utom de allra enklaste fallen är det bättre att använda sig av ett tilläggsbibliotek som heter **PHPMailer**. Det finns att ladda ned på adressen [https://github.com/PHPMailer/PHPMailer](https://github.com/PHPMailer/PHPMailer) där det också finns utförliga exempel på användandet.

```php
<?php
require 'libphp-phpmailer/class.phpmailer.php';

$mail = new PHPMailer;

$mail->SMTPDebug = 3;                               // Enable verbose debug output

$mail->isSMTP();                                      // Set mailer to use SMTP
$mail->Host = 'smtp.gmail.com';                       // Specify main and backup SMTP servers
$mail->SMTPAuth = true;                               // Enable SMTP authentication
$mail->Username = '...';                     // SMTP username
$mail->Password = '...';                              // SMTP password
$mail->SMTPSecure = 'tls';                            // Enable TLS encryption, `ssl` also accepted
$mail->Port = 587;                                    // TCP port to connect to

$mail->setFrom('twiggy@cybergymnasiet.se', 'Mailer');
$mail->addAddress('anders.andersson@cybergymnasiet.se', 'Anders Andersson');     // Add a recipient
//$mail->addAddress('ellen@example.com');               // Name is optional
//$mail->addReplyTo('info@example.com', 'Information');
//$mail->addCC('cc@example.com');
//$mail->addBCC('bcc@example.com');

//$mail->addAttachment('/var/tmp/file.tar.gz');         // Add attachments
//$mail->addAttachment('/tmp/image.jpg', 'new.jpg');    // Optional name
//$mail->isHTML(true);                                  // Set email format to HTML

$mail->Subject = 'PHPMailer GMail SMTP test';
$mail->Body    = 'This is the HTML message body <b>in bold!</b>';
$mail->AltBody = 'This is the body in plain text for non-HTML mail clients';

if(!$mail->send()) {
    echo 'Message could not be sent.';
    echo 'Mailer Error: ' . $mail->ErrorInfo;
} else {
    echo 'Message has been sent';
}
?>
```

## Uppgifter - skicka epost

### **Uppgift 8.1**

Gör ett formulär med fält för avsändaradress, adressen e-posten ska skickas till, själva meddelandet och ärende. Skriv sedan ett PHP-program som tar hand om formuläret och skickar eposten.

### **Uppgift 8.2**

Utveckla programmet i övning 1 så att man kan skriva in flera adresser separerade med kommatecken. Programmet ska sedan skicka epost-meddelandet till alla adresserna. Tips: använd funktionen **split\(\)**.

