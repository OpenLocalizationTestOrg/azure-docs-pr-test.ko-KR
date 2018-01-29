---
title: "Web App for Containers로 Docker 컨테이너 레지스트리에서 연속 배포 - Azure | Microsoft Docs"
description: "Web App for Containers의 Docker 컨테이너 레지스트리에서 연속 배포를 설정하는 방법."
keywords: Azure App Service, Linux, OSS
services: app-service
documentationcenter: 
author: ahmedelnably
manager: cfowler
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: cccbd4952c66d3d8140e2a03e3b76afaa5ba3fbf
ms.sourcegitcommit: b979d446ccbe0224109f71b3948d6235eb04a967
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2017
---
# <a name="continuous-deployment-with-web-app-for-containers"></a>Web App for Containers를 사용한 연속 배포

이 자습서에서는 관리되는 [Azure Container Registry](https://azure.microsoft.com/services/container-registry/) 리포지토리 또는 [Docker 허브](https://hub.docker.com)에서 사용자 지정 컨테이너 이미지에 대한 연속 배포를 구성합니다.

## <a name="sign-in-to-azure"></a>Azure에 로그인

[Azure 포털](https://portal.azure.com)

## <a name="enable-container-continuous-deployment-feature"></a>컨테이너 연속 배포 기능 사용

[Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)를 사용하고 다음 명령을 실행하여 연속 배포 기능을 사용하도록 설정할 수 있습니다.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
```

**[Azure Portal](https://portal.azure.com/)**에서 페이지 왼쪽의 **App Service** 옵션을 클릭합니다.

Docker 허브 연속 배포를 구성하려는 앱의 이름을 클릭합니다.

**앱 설정**에서 `true` 값을 갖는 `DOCKER_ENABLE_CI`라는 앱을 추가합니다.

![앱 설정 이미지 삽입](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="prepare-webhook-url"></a>Webhook URL 준비

[Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)를 사용하고 다음 명령을 실행하여 웹후크 URL을 가져올 수 있습니다.

```azurecli-interactive
az webapp deployment container show-cd-url -n sname1 -g rgname
```

웹후크 URL에는 끝점 `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`가 필요합니다.

Azure Portal에서 웹앱 게시 프로필을 다운로드하여 `publishingusername` 및 `publishingpwd`를 구할 수 있습니다.

![웹후크 추가 이미지 2 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="add-a-web-hook"></a>Webhook 추가

### <a name="azure-container-registry"></a>Azure Container Registry

레지스트리 포털 블레이드에서 **웹후크**를 클릭하고 **추가**를 클릭하여 새 웹후크를 만듭니다. **웹후크 만들기** 블레이드에서 웹후크에 이름을 지정합니다. 웹후크 URI에 **3단계**에서 가져온 URL을 제공해야 합니다.

범위를 컨테이너 이미지를 포함하는 리포지토리로 정의해야 합니다.

![웹후크 이미지 삽입](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

이미지를 업데이트할 때 자동으로 웹앱이 새 이미지로 업데이트됩니다.

### <a name="docker-hub"></a>Docker 허브

Docker 허브 페이지에서 **웹후크**를 클릭한 후 **웹후크 만들기**를 클릭합니다.

![웹후크 추가 이미지 1 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

웹후크 URL에 **3단계**에서 가져온 URL을 제공해야 합니다.

![웹후크 추가 이미지 2 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

이미지를 업데이트할 때 자동으로 웹앱이 새 이미지로 업데이트됩니다.

## <a name="next-steps"></a>다음 단계

* [Linux의 Azure App Service란?](./app-service-linux-intro.md)
* [Azure Container Registry](https://azure.microsoft.com/services/container-registry/)
* [Linux의 Azure App Service에서 .NET Core 사용](quickstart-dotnetcore.md)
* [Linux의 Azure App Service에서 Ruby 사용](quickstart-ruby.md)
* [Web App for Containers에 사용자 지정 Docker 이미지를 사용하는 방법](quickstart-custom-docker-image.md)
* [Containers용 Azure App Service Web App 관련 FAQ](./app-service-linux-faq.md)
* [Azure CLI 2.0을 사용하여 Web App for Containers 관리](./app-service-linux-cli.md)