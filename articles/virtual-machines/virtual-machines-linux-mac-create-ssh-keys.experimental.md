---
title: In Azure een SSH-sleutelpaar maken voor virtuele Linux-machines | Microsoft Docs
description: "Maak op een veilige manier een sleutelpaar met een openbare en een privé-SSH-sleutel voor virtuele Azure Linux-machines."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
experiment_id: rasquill-ssh-20170308
translationtype: Human Translation
ms.sourcegitcommit: 97acd09d223e59fbf4109bc8a20a25a2ed8ea366
ms.openlocfilehash: 878b297c4c9e5ef4a7177e9bd5dc564a0c83680b
ms.lasthandoff: 03/10/2017



---

# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a>Een sleutelpaar met een openbare en een privé-SSH-sleutel maken voor virtuele Linux-machines

In dit artikel wordt beschreven hoe u een sleutelpaar met een openbare en een persoonlijke sleutel met SSH-protocol versie 2 RSA maakt voor gebruik met virtuele Linux-machines.  Met een SSH-sleutelpaar kunt u virtuele machines in Azure maken die voor verificatie standaard gebruikmaken van SSH-sleutels, waardoor aanmelding met een wachtwoord niet meer nodig is.  Wachtwoorden kunnen worden geraden en stellen uw virtuele machines bloot aan voortdurende aanvalspogingen om uw wachtwoord te raden. Virtuele machines die zijn gemaakt met de Azure-sjablonen of de `azure-cli`, kunnen uw openbare SSH-sleutel opnemen als onderdeel van de implementatie, waardoor configuratie na implementatie niet meer nodig is voor het uitschakelen van aanmelding met een wachtwoord voor SSH.

## <a name="quick-commands"></a>Snelle opdrachten

Voer de volgende opdrachten uit via een Bash-shell en vervang de voorbeelden door uw eigen gegevens.

Uw openbare SSH-sleutelbestand wordt standaard gemaakt in `~/.ssh/id_rsa.pub`. Maak met onderstaande opdracht een wachtwoordzin voor het beveiligen van uw persoonlijke sleutel als u hierom wordt gevraagd. (Een wachtwoordzin is een wachtwoord dat wordt gebruikt om uw persoonlijke sleutel te versleutelen.)

```bash
ssh-keygen -t rsa -b 2048 
```

Voeg de zojuist gemaakte sleutel toe aan `ssh-agent`:

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> De bovenstaande opdrachten werken op Linux-besturingssystemen van bijna alle distributies, maar niet per se in containers, omdat de omgeving aanzienlijk beperkt kan zijn. 

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht

Het gebruik van openbare en persoonlijke SSH-sleutels is de eenvoudigste manier om u aan te melden bij uw Linux-servers. [Cryptografie met openbare sleutels](https://en.wikipedia.org/wiki/Public-key_cryptography) biedt een veel veiligere manier van aanmelding bij uw virtuele Linux- of BSD-machines in Azure dan wachtwoorden, die aanzienlijk eenvoudiger met een brute force-aanval kunnen worden aangevallen.

> [!IMPORTANT]
> Uw openbare sleutel kan worden gedeeld met iedereen, maar alleen u (of uw lokale beveiligingsinfrastructuur) beschikt over uw persoonlijke sleutel.  De privé-SSH-sleutel moet ter beveiliging een [zeer veilig wachtwoord](https://www.xkcd.com/936/) hebben (bron:[xkcd.com](https://xkcd.com)).  Dit wachtwoord dient alleen voor toegang tot de persoonlijke SSH-sleutel en **is niet** het wachtwoord voor het gebruikersaccount.  Wanneer u een wachtwoord aan de SSH-sleutel toevoegt, wordt de privésleutel versleuteld met behulp van 128-bits AES, zodat deze niet kan worden gebruikt zonder het wachtwoord om de privésleutel te ontsleutelen.  Als een aanvaller uw persoonlijke sleutel zou stelen en deze geen wachtwoord zou hebben, zou de aanvaller in staat zijn om de persoonlijke sleutel te gebruiken voor aanmelding bij de servers waarop de bijbehorende openbare sleutel is geïnstalleerd.  Als een persoonlijke sleutel is beveiligd met een wachtwoord, kan deze niet worden gebruikt door de aanvaller. Zo beschikt u over een extra beveiligingslaag voor uw infrastructuur in Azure.

In dit artikel worden openbare en persoonlijke sleutelbestanden met SSH-protocol versie 2 RSA gemaakt, die worden aanbevolen voor implementaties in Resource Manager.  *ssh-rsa*-sleutels zijn vereist in de [portal](https://portal.azure.com) voor zowel de klassieke implementatie als de implementatie voor resourcebeheer.

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a>SSH-wachtwoorden uitschakelen met SSH-sleutels

Azure vereist openbare en persoonlijke sleutels van ten minste 2048 bits in ssh-rsa-indeling. Voor het maken van de sleutels gebruiken we `ssh-keygen`, die een reeks vragen stelt en vervolgens een persoonlijke sleutel en een overeenkomende openbare sleutel schrijft. Wanneer een virtuele Azure-machine wordt gemaakt, wordt de openbare sleutel gekopieerd naar `~/.ssh/authorized_keys`.  SSH-sleutels in `~/.ssh/authorized_keys` worden gebruikt om de client te vragen de bijbehorende persoonlijke sleutel te verstrekken bij verbinding via een SSH-aanmelding.  Wanneer er in Azure een virtuele Linux-machine wordt gemaakt met SSH-sleutels voor verificatie, configureert Azure de SSHD-server zodanig dat aanmelding met een wachtwoord niet wordt toegestaan en alleen SSH-sleutels worden toegestaan.  Daarom kunt u helpen de VM-implementatie te beveiligen door virtuele Azure Linux-machines met SSH-sleutels te maken. Ook kunt u uzelf de typische configuratiestap besparen die moet worden uitgevoerd na de implementatie: wachtwoorden uitschakelen in het configuratiebestand sshd_config.

## <a name="using-ssh-keygen"></a>ssh-keygen gebruiken

Met deze opdracht wordt een met een wachtwoord beveiligd (versleuteld) SSH-sleutelpaar gemaakt met 2048-bits RSA waaraan opmerkingen worden toegevoegd om het gemakkelijk te kunnen identificeren.  

SSH-sleutels worden standaard opgeslagen in de `~/.ssh`-directory.  Als u niet beschikt over de map `~/.ssh`, wordt deze door de opdracht `ssh-keygen` voor u gemaakt met de juiste machtigingen.

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

*Uitleg van de opdracht*

`ssh-keygen` = het programma dat wordt gebruikt voor het maken van de sleutels

`-t rsa` = type sleutel dat moet worden gemaakt, namelijk de RSA-indeling [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)

`-b 2048` = aantal bits van de sleutel


## <a name="classic-portal-and-x509-certs"></a>Klassieke portal en X.509-certificaten

Als u de [klassieke portal](https://manage.windowsazure.com/) van Azure gebruikt, zijn X.509-certificaten vereist voor de SSH-sleutels.  Er zijn geen andere typen openbare SSH-sleutels toegestaan. Het *moeten* X.509-certificaten zijn.

Een X.509-certificaat maken met een bestaande privé-SSH-RSA-sleutel:

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a>Klassieke implementatie met behulp van`asm`

Als u gebruikmaakt van het klassieke implementatiemodel (Azure CLI voor servicebeheer `asm`), kunt u een openbare SSH-RSA-sleutel of een RFC4716-sleutel gebruiken in een **PEM**-container.  De openbare SSH-RSA-sleutel is de sleutel die eerder in dit artikel is gemaakt met behulp van `ssh-keygen`.

Een RFC4716-sleutel maken van een bestaande openbare SSH-sleutel:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Voorbeeld van ssh-keygen

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
The keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

Opgeslagen sleutelbestanden:

`Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

De naam van het sleutelpaar voor dit artikel.  De naam **id_rsa** is de standaardwaarde voor een sleutelpaar. Sommige programma’s verwachten mogelijk **id_rsa** als naam voor het persoonlijke sleutelbestand, dus is het een goed idee als u er een hebt. De map `~/.ssh/` is de standaardlocatie voor SSH-sleutelparen en het SSH-configuratiebestand.  Als `ssh-keygen` niet wordt opgegeven met een volledig pad, worden de sleutels in de huidige werkmap gemaakt in plaats van in de standaardmap `~/.ssh`.

Een vermelding van de `~/.ssh`-map

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

Sleutelwachtwoord:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen` verwijst naar een wachtwoord voor het versleutelen van de privésleutel (een zogenaamde 'wachtwoordzin').  Het wordt *sterk* aanbevolen een wachtwoordzin toe te voegen aan uw sleutelparen. Zonder een wachtwoordzin die de persoonlijke sleutel beveiligt, kan iedereen met een exemplaar van het sleutelbestand zich aanmelden bij elke server die beschikt over de bijbehorende openbare sleutel. Het toevoegen van een wachtwoordzin biedt veel meer bescherming in het geval iemand in staat is toegang te krijgen tot uw persoonlijke sleutelbestand. In de extra tijd die dit oplevert, kunt u de sleutels wijzigen waarmee u wordt geverifieerd.

## <a name="using-ssh-agent-to-store-your-private-key-password"></a>ssh-agent gebruiken voor het opslaan van het wachtwoord van uw persoonlijke sleutel

Teneinde te voorkomen dat u de wachtwoordzin van uw persoonlijke sleutelbestand bij elke SSH-aanmelding moet opgeven, kunt u `ssh-agent` gebruiken om het wachtwoord van uw persoonlijke sleutelbestand in de cache te plaatsen. Als u een Mac gebruikt, worden de wachtwoorden van uw persoonlijke sleutels veilig opgeslagen door Sleutelhangertoegang van OSX wanneer u `ssh-agent` aanroept.

Controleer en gebruik `ssh-agent` en `ssh-add` om het SSH-systeem te informeren over de sleutelbestanden, zodat de wachtwoordzin niet interactief hoeft te worden gebruikt.

```bash
eval "$(ssh-agent -s)"
```

Voeg nu de persoonlijke sleutel toe aan `ssh-agent` met de opdracht `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

Het wachtwoord voor persoonlijke sleutel wordt nu opgeslagen in `ssh-agent`.

## <a name="using-ssh-copy-id-to-install-the-new-key"></a>De nieuwe sleutel installeren met behulp van `ssh-copy-id`
Als u al een virtuele machine hebt gemaakt, kunt u de nieuwe openbare SSH-sleutel voor uw virtuele Linux-machine installeren met de volgende opdracht. Hiermee worden de gebruikersnaam van de virtuele machine en het serveradres vervangen door uw eigen waarden:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Een SSH-configuratiebestand maken en configureren

Het wordt aanbevolen een `~/.ssh/config`-bestand te maken en te configureren om aanmeldingen te versnellen en het gedrag van uw SSH-clientgedrag te optimaliseren.

In het volgende voorbeeld wordt een standaardconfiguratie getoond.

### <a name="create-the-file"></a>Het bestand maken

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a>Bewerk het bestand om de nieuwe SSH-configuratie toe te voegen:

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>Voorbeeld van `~/.ssh/config`-bestand:

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

Deze SSH-configuratie bevat afzonderlijke secties voor elke server, zodat elke server kan beschikken over een eigen toegewezen sleutelpaar. De standaardinstellingen (`Host *`) zijn voor alle hosts die niet overeenkomen met een van de specifieke hosts die hoger in het configuratiebestand staan.

### <a name="config-file-explained"></a>Uitleg van configuratiebestand

`Host` = de naam van de host die wordt aangeroepen op de terminal.  `ssh fedora22` vertelt `SSH` dat de waarden moeten worden gebruikt in het instellingenblok met het label `Host fedora22` OPMERKING: de host kan elk label zijn dat logisch is voor uw gebruik. Het label vertegenwoordigt niet de werkelijke hostnaam van een server.

`Hostname 102.160.203.241` = het IP-adres of de DNS-naam van de server die wordt benaderd.

`User ahmet` = het account van de externe gebruiker dat moet worden gebruikt bij het aanmelden bij de server.

`PubKeyAuthentication yes` = vertelt SSH dat u gebruik wilt maken van een SSH-sleutel voor aanmelding.

`IdentityFile /home/ahmet/.ssh/id_id_rsa` = de persoonlijke SSH-sleutel en de bijbehorende openbare sleutel te gebruiken voor verificatie.

## <a name="ssh-into-linux-without-a-password"></a>SSH in Linux zonder een wachtwoord

Nu u een SSH-sleutelpaar en een geconfigureerd SSH-configuratiebestand hebt, kunt u zich snel en veilig aanmelden bij uw virtuele Linux-machine. De eerste keer dat u zich met een SSH-sleutel bij een server aanmeldt, wordt u gevraagd naar de wachtwoordzin voor dat sleutelbestand.

```bash
ssh fedora22
```

### <a name="command-explained"></a>Uitleg van de opdracht

Wanneer `ssh fedora22` wordt uitgevoerd, zoekt en laadt SSH eerst instellingen uit het `Host fedora22`-blok en laadt het vervolgens alle overige instellingen uit het laatste blok, `Host *`.

## <a name="next-steps"></a>Volgende stappen

De volgende stap bestaat uit het maken van virtuele Linux-machines in Azure met de nieuwe openbare SSH-sleutel.  Virtuele Azure-machines die zijn gemaakt met een openbare SSH-sleutel voor aanmelding, zijn beter beveiligd dan virtuele machines die zijn gemaakt met een wachtwoord als standaardaanmeldingsmethode.  Virtuele Azure-machines die zijn gemaakt met behulp van SSH-sleutels zijn standaard geconfigureerd met wachtwoorden uitgeschakeld, waarmee brute force-aanvallen om wachtwoorden te raden worden voorkomen. Als u meer hulp nodig hebt bij het maken van het SSH-sleutelpaar of meer certificaten nodig hebt, bijvoorbeeld voor gebruik met de klassieke portal, raadpleegt u [Gedetailleerde stappen voor het maken van SSH-sleutelparen en certificaten](virtual-machines-linux-create-ssh-keys-detailed.md).

* [Een beveiligde virtuele Linux-machine maken met een Azure-sjabloon](virtual-machines-linux-create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Een beveiligde virtuele Linux-machine maken met Azure Portal](virtual-machines-linux-quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Een beveiligde virtuele Linux-machine maken met de Azure CLI](virtual-machines-linux-quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

