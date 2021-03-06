---
title: Een statische HTML-web-app in vijf minuten maken in Azure | Microsoft Docs
description: Hier ontdekt u door een voorbeeld-app te implementeren hoe eenvoudig het is om web-apps in App Service uit te voeren.
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: cephalin
translationtype: Human Translation
ms.sourcegitcommit: be3ac7755934bca00190db6e21b6527c91a77ec2
ms.openlocfilehash: ba9b9b780da74c44f6314fa289f1d6b8c231dd30
ms.lasthandoff: 05/03/2017


---
# <a name="create-a-static-html-web-app-in-azure-in-five-minutes"></a>Een statische HTML-web-app in vijf minuten maken in Azure
[!INCLUDE [app-service-web-selector-get-started](../../includes/app-service-web-selector-get-started.md)] 

Met deze Quickstart leert u in een paar minuten hoe u een eenvoudige HTML+CSS-site implementeert in [Azure App Service](../app-service/app-service-value-prop-what-is.md).

Voordat u begint, moet u controleren of de Azure-CLI is geïnstalleerd. Zie voor meer informatie de [Installatiehandleiding van de Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="log-in-to-azure"></a>Meld u aan bij Azure.
Meld u aan bij Azure door `az login` uit te voeren en de aanwijzingen op het scherm te volgen.
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a>Een resourcegroep maken   
Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md). Hier verzamelt u alle Azure-resources die u samen wilt beheren, zoals de web-app en de bijbehorende SQL Database-back-end.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

Gebruik de Azure CLI-opdracht `az appservice list-locations` om te zien welke waarden u kunt gebruiken voor `--location`.


## <a name="create-an-app-service-plan"></a>Een App Service-plan maken
Maak een 'GRATIS' [App Service-plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

## <a name="create-a-web-app"></a>Een webtoepassing maken
Maak een web-app met een unieke naam in `<app_name>`.

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan my-free-appservice-plan
```

## <a name="deploy-sample-application"></a>Voorbeeldtoepassing implementeren
Implementeer een voorbeeld van een HTML-site vanuit GitHub.

```azurecli
az appservice web source-control config --name <app_name> --resource-group myResourceGroup \
--repo-url "https://github.com/Azure-Samples/app-service-web-html-get-started.git" --branch master --manual-integration 
```

## <a name="browse-to-web-app"></a>Naar de web-app bladeren
Voer deze opdracht uit om uw app live in werking te zien in Azure.

```azurecli
az appservice web browse --name <app_name> --resource-group myResourceGroup
```

Gefeliciteerd, uw eerste statische HTML-site wordt live uitgevoerd in Azure App Service.

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Volgende stappen

Bekijk vooraf gemaakte [CLI-scripts voor web-apps](app-service-cli-samples.md).

