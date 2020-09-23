---
description: 'Installera alla verktyg, konfigurera alla inställningar, skapar alla mappar'
---

# Introduktion

## Installera webbeditorn VS Code & tillägg

* Installera [VS Code](https://code.visualstudio.com/)
* Installera tillägg
* Installera [git-scm](https://git-scm.com/)

![](.gitbook/assets/image.png)

## Installera PHP och konfigurera VS Code

* [ ] Ladda ned [PHP 7.4 x64 Thread Safe 2](https://windows.php.net/download)
* [ ] Packa upp till c:/php
* [ ] Öppna VS Code
* [ ] Fyll i rätt sökväg se [https://code.visualstudio.com/docs/languages/php](https://code.visualstudio.com/docs/languages/php)

## Skapa en utvecklingsmiljö

* [ ] Skapa ett konto på github
* [ ] Skapa en repository EE18-ar3
* [ ] Skapa en mapp c:/github
* [ ] Klona EE18-ar3 i VS Code inuti c:/github

![](.gitbook/assets/image%20%281%29.png)

## Installera Docker Desktop och LAMP-server

###  LAMP = Linux Apache Mysql PHP 

1. [ ] Installera Docker Desktop
2. [ ] Gå in i BIOS och slå på virtualisering
3. [ ] I Docker Settings aktivera Shared Folders
4. [ ] I VS Code installera tillägget Docker
5. [ ] Öppna terminalen i VS Code och kör kommandot 
6. [ ] Om du använder powershell: 

```bash
docker run -d --restart unless-stopped -p 8080:80 -p 10000:10000 -v "c:\github:/var/www" --name lamp karye/lampw 
```

* [ ] Om du använder bash: 

```bash
docker run -d --restart unless-stopped -p 8080:80 -p 10000:10000 -v /host_mnt/c/github:/var/www --name lamp karye/lampw
```

1. [ ] Instruktioner till hur du använder LAMPW finns på [https://hub.docker.com/r/karye/lampw](https://hub.docker.com/r/karye/lampw)

## Bra webblänkar

