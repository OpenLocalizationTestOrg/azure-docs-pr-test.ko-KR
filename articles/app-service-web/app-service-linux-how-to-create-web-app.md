---
title: "aaaCreate Azure 웹 앱 Linux에서 실행 중인 | Microsoft Docs"
description: "Linux의 Azure Web App용 웹앱 만들기 워크플로"
keywords: "azure app service, 웹앱, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Linux에서 실행되는 Azure Web App 만들기

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a>Azure 포털 toocreate hello 웹 응용 프로그램 사용
Hello에서 Linux에서 웹 앱을 만들기 시작할 수 있습니다 [Azure 포털](https://portal.azure.com) hello 다음 이미지와 같이:

![Hello Azure 포털에서 웹 앱을 만들기 시작][1]

다음으로 hello **만들기 블레이드** hello 다음 이미지와 같이 열립니다.

![hello 만들기 블레이드][2]

1. 웹앱에 이름을 지정합니다.
2. 기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만듭니다. (사용 가능한 지역이 hello에 [제한 사항 섹션](app-service-linux-intro.md).)
3. 기존 Azure App Service 계획을 선택하거나 새 App Service 계획을 만듭니다. (Hello에 앱 서비스 계획을 참조 하십시오 [제한 사항 섹션](app-service-linux-intro.md).)
4. Hello 응용 프로그램을 선택 하려는 toouse 스택 합니다. 여러 버전의 Node.js, PHP, .Net Core, Ruby 중에 선택할 수 있습니다.

Hello 응용 프로그램 스택 hello 다음 이미지와 같이 hello 응용 프로그램을 만든 후 hello 응용 프로그램 설정에서 변경할 수 있습니다.

![응용 프로그램 설정][3]

## <a name="deploy-your-web-app"></a>웹앱 배포
선택 **배포 옵션** hello 관리 포털에서는에서 있습니다 hello 옵션 toouse 로컬 Git 또는 GitHub 리포지토리 toodeploy 응용 프로그램입니다. hello 지침 hello 나머지는 Linux 비 웹 앱에 대 한 유사한 toothose 합니다. Hello 지침에 따르면 [로컬 Git 배포](app-service-deploy-local-git.md) 또는 [연속 배포](app-service-continuous-deployment.md) toodeploy 앱.

또한 응용 프로그램 tooyour 사이트 FTP tooupload를 사용할 수 있습니다. 에서 가져올 수 있습니다 hello FTP 끝점 웹 앱에 대 한 hello 진단 로그 섹션 hello 다음 이미지와 같이:

![진단 로그][4]

## <a name="next-steps"></a>다음 단계
* [Linux에서 Azure Web App이란?](app-service-linux-intro.md)
* [Linux의 Azure Web App에서 Node.js용 PM2 구성 사용](app-service-linux-using-nodejs-pm2.md)
* [Linux의 Azure App Service Web App에서 Ruby 사용](app-service-linux-ruby-get-started.md)
* [Linux의 Azure App Service Web App에 대한 FAQ](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
