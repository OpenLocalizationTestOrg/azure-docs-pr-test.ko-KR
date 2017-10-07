---
title: "웹 응용 프로그램에 액세스 Azure CLI 2.0을 사용 하 여 Linux aaaManage | Microsoft Docs"
description: "Azure CLI를 사용하여 Linux에서 웹앱 관리"
keywords: "azure app service, 웹앱, cli, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>Azure CLI를 사용하여 Linux에서 웹앱 관리

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Hello 명령을 사용 하 여이 문서에서 수 toocreate 됩니다 하 고 Azure CLI 2.0을 사용 하 여 Linux에서 웹 앱을 관리 합니다.
Hello 새 버전의 두 가지 방법으로 hello CLI 사용 하 여 시작할 수 있습니다.

* 컴퓨터에 [Azure CLI 2.0 설치](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure Cloud Shell(미리 보기)](../cloud-shell/overview.md) 사용


## <a name="create-a-linux-app-service-plan"></a>Linux App Service 계획 만들기

Linux 앱 서비스 계획 toocreate, hello 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>사용자 지정 Docker 컨테이너 웹앱 만들기

toocreate 웹 응용 프로그램 및 사용자 지정 Docker 컨테이너 toorun 구성 hello 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a>Hello Docker 컨테이너 로깅을 활성화합니다

tooactivate Docker 컨테이너 로깅 hello, hello 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Linux 응용 프로그램에서 기존 웹 앱에 대 한 사용자 지정 Docker 컨테이너 hello 변경

hello 현재 Docker 이미지 tooa 새 이미지에서 이전에 만든된 응용 프로그램 toochange hello 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>개인 레지스트리의 Docker 이미지 사용

앱 toouse 이미지 전용 레지스트리를 구성할 수 있습니다. 레지스트리, 사용자 이름 및 암호 tooprovide hello url 필요합니다. 다음 명령을 hello를 사용 하 여 수행할 수 있습니다.

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>사용자 지정 Docker 이미지에 대한 연속 배포 사용

다음 명령을 hello로 hello CD 기능을 고 hello webhook url을 가져올 수 있습니다. 이 url 사용된 tooconfigure 있습니다 DockerHub 또는 Azure 컨테이너 레지스트리 리포지토리 될 수 있습니다.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>기본 제공된 런타임 프레임워크 중 하나를 사용하여 Linux 앱에서 웹앱 만들기

toocreate hello 다음 명령을 사용할 수 있는, Linux 응용 프로그램에서 PHP 5.6 웹 앱입니다.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Linux 앱에서 기존 웹앱에 대한 프레임워크 버전 변경

hello 현재 프레임 워크 버전 tooNode.js 6.11에서 이전에 만든된 응용 프로그램 toochange hello 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>웹앱에 대한 Git 배포 설정

응용 프로그램에 대 한 Git 배포를 tooset, hello 다음 명령을 사용할 수 있습니다.

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>다음 단계
* [Linux에서 Azure Web App이란?](app-service-linux-intro.md)
* [Azure CLI 2.0 설치](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure Cloud Shell(미리 보기)](../cloud-shell/overview.md)
* [Azure App Service에서 스테이징 환경 설정](./web-sites-staged-publishing.md)
* [Linux에서 Azure 웹앱을 사용한 연속 배포](./app-service-linux-ci-cd.md)
