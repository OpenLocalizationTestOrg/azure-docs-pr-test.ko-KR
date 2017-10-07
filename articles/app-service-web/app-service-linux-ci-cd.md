---
title: "Linux에서 Azure 웹 앱과 함께 배포 aaaContinuous | Microsoft Docs"
description: "어떻게 toosetup Linux에서 Azure 웹 앱에서 연속 배포 합니다."
keywords: azure app service, linux, oss, acr
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a>Linux에서 Azure Web App을 사용한 연속 배포

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

이 자습서에서는 관리되는 [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) 리포지토리 또는 [Docker 허브](https://hub.docker.com)에서 사용자 지정 컨테이너 이미지에 대한 연속 배포를 구성합니다.

## <a name="step-1---sign-in-tooazure"></a>1 단계-tooAzure 로그인

Azure 포털에서 http://portal.azure.com toohello에 로그인

## <a name="step-2---enable-container-continuous-deployment-feature"></a>2단계 - 컨테이너 연속 배포 기능 사용

사용 하 여 hello 연속 배포 기능을 활성화할 수 있습니다 [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) hello 다음 명령을 실행 하 고

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

Hello에  **[Azure 포털](https://portal.azure.com/)**, hello 클릭 **앱 서비스** hello 창의 hello 왼쪽의 옵션입니다.

Tooconfigure Docker 허브에 대 한 연속 배포 하려는 앱의 hello 이름을 클릭 합니다.

Hello에 **앱 설정**, 라고 앱 추가 `DOCKER_ENABLE_CI` hello 값을 가진 `true`합니다.

![앱 설정 이미지 삽입](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a>3단계 - 웹후크 URL 준비

사용 하 여 hello Webhook URL을 가져올 수 있습니다 [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) hello 다음 명령을 실행 하 고

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

다음 끝점 toohave hello hello Webhook URL에 대 한 필요한: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`합니다.

가져올 수 있습니다 프로그램 `publishingusername` 및 `publishingpwd` hello 웹 앱을 다운로드 하 여 hello Azure 포털을 사용 하 여 프로필을 게시 합니다.

![웹후크 추가 이미지 2 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a>4단계: 웹후크 추가

### <a name="azure-container-registry"></a>Azure Container Registry

레지스트리 포털 블레이드에서 **웹후크**를 클릭하고 **추가**를 클릭하여 새 웹후크를 만듭니다. Hello에 **webhook 만들기** 블레이드에서 프로그램 webhook에 이름을 지정 합니다. 가져온 tooprovide hello URL hello Webhook URI에 대 한 필요한 **3 단계**

컨테이너 이미지를 포함 하는 리포지토리의 hello으로 hello 범위를 정의 하는 있는지 확인 합니다.

![웹후크 이미지 삽입](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

Hello 이미지를 업데이트 하는 경우 hello 새 이미지로 hello 웹 응용 프로그램 자동으로 업데이트 합니다.

### <a name="docker-hub"></a>Docker 허브

Docker 허브 페이지에서 **웹후크**를 클릭한 후 **웹후크 만들기**를 클릭합니다.

![웹후크 추가 이미지 1 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

가져온 tooprovide hello URL hello Webhook URL에 대 한 필요한 **3 단계**

![웹후크 추가 이미지 2 삽입](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

Hello 이미지를 업데이트 하는 경우 hello 새 이미지로 hello 웹 응용 프로그램 자동으로 업데이트 합니다.

## <a name="next-steps"></a>다음 단계
* [Linux에서 Azure Web App이란?](./app-service-linux-intro.md)
* [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/)
* [Linux의 Azure Web App에서 Node.js용 PM2 구성 사용](app-service-linux-using-nodejs-pm2.md)
* [Linux의 Azure Web App에서 .NET Core 사용](app-service-linux-using-dotnetcore.md)
* [Linux의 Azure Web App에서 Ruby 사용](app-service-linux-ruby-get-started.md)
* [Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker toouse 이미지 방법](./app-service-linux-using-custom-docker-image.md)
* [Linux의 Azure App Service Web App에 대한 FAQ](./app-service-linux-faq.md) 
* [Azure CLI 2.0을 사용하여 Linux에서 웹앱 관리](./app-service-linux-cli.md)



