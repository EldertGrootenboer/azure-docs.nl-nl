---
title: "Privé-Docker-register maken - Azure Portal | Microsoft Docs"
description: "Aan de slag met het maken en beheren van privé-Docker-containerregisters met Azure Portal"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
translationtype: Human Translation
ms.sourcegitcommit: 356de369ec5409e8e6e51a286a20af70a9420193
ms.openlocfilehash: e74c5428f0e31d9d3cf06b85aa8cefde868e9d67
ms.lasthandoff: 03/27/2017

---

# <a name="create-a-private-docker-container-registry-using-the-azure-portal"></a>Een privé-Docker-containerregister maken met Azure Portal
Gebruik Azure Portal om een containerregister te maken en de instellingen ervan te beheren. U kunt ook containerregisters maken en beheren met de [Azure CLI 2.0-opdrachten](container-registry-get-started-azure-cli.md) of programmatisch met de [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376) voor Container Registry.

Zie [het overzicht](container-registry-intro.md) voor meer achtergrondinformatie en concepten.



## <a name="create-a-container-registry"></a>Een containerregister maken
1. Klik in [Azure Portal](https://portal.azure.com) op **+ Nieuw**.
2. Zoek in Marketplace naar **Azure Container Registry**.
3. Selecteer **Azure Container Registry** met als uitgever **Microsoft**.
    ![Container Registry-service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)
4. Klik op **Create**. De blade **Azure Container Registry** wordt weergegeven.

    ![Container Registry-instellingen](./media/container-registry-get-started-portal/container-registry-settings.png)
5. Voer de volgende gegevens in op de blade **Azure Container Registry**. Klik op **Maken** wanneer u klaar bent.

    a. **Registernaam**: een unieke domeinnaam op het hoogste niveau voor uw specifieke register. De registernaam in dit voorbeeld is *myRegistry01*, maar u hoort deze door uw eigen unieke naam te vervangen. De naam mag alleen uit letters en cijfers bestaan.

    b. **Resourcegroep**: selecteer een bestaande [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) of typ de gewenste naam voor een nieuwe resourcegroep.

    c. **Locatie**: selecteer een Azure Datacenter-locatie waar de service [beschikbaar](https://azure.microsoft.com/regions/services/) is, zoals **Zuid-centraal VS**.

    d. **Beheerder**: schakel eventueel toegang tot het register in voor een beheerder. U kunt deze instelling wijzigen nadat u het register hebt gemaakt.

      > [!IMPORTANT]
      > Naast toegang via een beheeraccount ondersteunen containerregisters verificatie met behulp van service-principals van Azure Active Directory. Bekijk voor meer informatie [Verifiëren met het containerregister](container-registry-authentication.md).
      >

    e. **Opslagaccount**: maak een [opslagaccount](../storage/storage-introduction.md) met de standaardinstelling of selecteer een bestaand opslagaccount op dezelfde locatie. Premium-opslag wordt momenteel niet ondersteund.

## <a name="manage-registry-settings"></a>Registerinstellingen beheren
Nadat u het register hebt gemaakt, kunt u de registerinstellingen openen via de blade **Container Registry** in de portal. U hebt de instellingen mogelijk nodig om u aan te melden bij uw register of om de beheerder in of uit te schakelen.

1. Klik op de blade **Container Registry** op de naam van uw register.

    ![Blade Container Registry](./media/container-registry-get-started-portal/container-registry-blade.png)
2. Klik op **Toegangssleutel** om de toegangsinstellingen te beheren.

    ![Toegang tot Container Registry](./media/container-registry-get-started-portal/container-registry-access.png)
3. De volgende instellingen zijn van belang:

   * **Aanmeldserver**: de door u opgegeven naam die aan alle vereisten voldoet voor het aanmelden bij het register. In dit voorbeeld is het `myregistry01.azurecr.io`.
   * **Beheerder**: schakel het beheeraccount van het register in of uit.
   * **Gebruikersnaam** en **Wachtwoord**: de aanmeldgegevens van het beheeraccount (indien ingeschakeld) waarmee u zich kunt aanmelden bij het register. U kunt indien nodig de wachtwoorden opnieuw genereren. Er worden twee wachtwoorden gemaakt, zodat u met één wachtwoord verbonden kunt blijven met het register terwijl u het andere wachtwoord opnieuw genereert. Zie [Verifiëren met een persoonlijk Docker-containerregister](container-registry-authentication.md) om in plaats daarvan te verifiëren met een service-principal.

## <a name="next-steps"></a>Volgende stappen
* [Uw eerste installatiekopie pushen met de Docker-CLI](container-registry-get-started-docker-cli.md)

