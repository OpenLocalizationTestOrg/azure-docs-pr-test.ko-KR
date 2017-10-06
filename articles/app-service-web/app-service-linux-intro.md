---
title: "웹 응용 프로그램에 액세스 Linux aaaIntroduction tooAzure | Microsoft Docs"
description: "Linux의 Azure Web App에 대해 자세히 알아봅니다."
keywords: azure app service, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a>소개 tooAzure Linux에서 웹 응용 프로그램

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>개요
고객 스택 되는 응용 프로그램에 대 한 기본적으로 Linux에서 Linux toohost 웹 앱에 웹 앱을 사용할 수 있습니다. hello 다음 섹션에는 현재 지원 되는 hello 응용 프로그램 스택 합니다. 

## <a name="features"></a>기능
현재 웹 응용 프로그램에 액세스 Linux 응용 프로그램 스택 다음 hello를 지원 합니다.

* Node.js
    * 4.4.
    * 4.5.
    * 6.2
    * 6.6
    * 6.9
    * 6.10
    * 6.11
    * 8.0
    * 8.1
* PHP
    * 5.6
    * 7.0
* .NET Core
    * 1.0
    * 1.1
* 루비
    * 2.3

고객은 다음을 사용하여 해당 응용 프로그램을 배포할 수 있습니다.

* FTP
* 로컬 Git
* GitHub
* Bitbucket

응용 프로그램 크기 조정:

* 고객 웹 앱 및 축소 하 여 확장할 수 해당 앱 서비스 계획의 hello 계층을 변경
* 고객 응용 프로그램을 확장 하 고 자신의 SKU의 hello 범위 내에서 여러 응용 프로그램 인스턴스를 실행할 수 있습니다.

에 대 한 Kudu hello 기본 기능 중 일부:

* 환경
* 배포
* 기본 콘솔
* SSH

devops:

* 스테이징 환경
* ACR 및 DockerHub CI/CD

## <a name="limitations"></a>제한 사항
hello Azure 포털 현재 Linux에서 웹 앱에 대 한 작동 하는 유일한 기능을 표시 하거나 숨깁니다 hello rest 합니다. 더 많은 기능을 사용 하도록 설정 하는 대로 hello 포털에 표시 됩니다.

가상 네트워크 통합, Azure Active Directory/타사 인증 또는 Kudu 사이트 확장 등의 일부 기능은 아직 사용할 수 없습니다. 이러한 기능을 사용할 수 되 면이 문서 및 블로그 hello 변경에 대 한 업데이트 됩니다.

이 공개 미리 보기가 현재 hello 다음 영역에서에서 사용할 수만 있습니다.

* 미국 서부
* 미국 동부
* 서유럽
* 북유럽
* 미국 중남부
* 미국 중북부
* 동남아시아
* 동아시아
* 오스트레일리아 동부
* 일본 동부
* 브라질 남부
* 인도 남부

웹 앱 linux hello 전용된 앱 서비스 계획에서만 지원 됩니다 및 무료 또는 공유 계층에는 없습니다. 또한 일반 및 Linux 웹앱에 대한 App Service 계획은 상호 배타적이므로 비 Linux App Service 계획에서 Linux 웹앱을 만들 수 없습니다.

웹 앱이 Linux hello에서 비 Linux 웹 앱을 포함 하지 않는 리소스 그룹에 만들어야 동일한 지역입니다.

## <a name="troubleshooting"></a>문제 해결 ##

응용 프로그램 toostart 못하거나 toocheck hello 로깅 응용 프로그램에서 원하는 Docker가 hello LogFiles 디렉터리에 로그인 하는 hello를 확인 합니다. SCM 사이트 또는 FTP를 통해 이 디렉터리에 액세스할 수 있습니다.
toolog hello `stdout` 및 `stderr` tooenable 사용자 컨테이너에서 필요한 **Docker 컨테이너 로깅** 아래 **진단 로그**합니다.

![로깅 사용][2]

![Kudu tooview Docker 로그를 사용 하 여][1]

hello SCM 사이트에 액세스할 수 있습니다 **고급 도구** hello에 **개발 도구** 메뉴.

## <a name="next-steps"></a>다음 단계
다음 링크 tooget linux 응용 프로그램 서비스를 시작 하는 hello를 참조 하십시오. [당사 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview)에 질문 및 문제를 게시할 수 있습니다.

* [Linux에서 Azure 웹 앱에 대 한 사용자 지정 Docker toouse 이미지 방법](app-service-linux-using-custom-docker-image.md)
* [Linux의 Azure Web App에서 Node.js용 PM2 구성 사용](app-service-linux-using-nodejs-pm2.md)
* [Linux의 Azure App Service Web App에서 .NET Core 사용](app-service-linux-using-dotnetcore.md)
* [Linux의 Azure App Service Web App에서 Ruby 사용](app-service-linux-ruby-get-started.md)
* [Linux의 Azure App Service Web App에 대한 FAQ](app-service-linux-faq.md)
* [Linux의 Azure Web App에 대한 SSH 지원](./app-service-linux-ssh-support.md)
* [Azure App Service에서 스테이징 환경 설정](./web-sites-staged-publishing.md)
* [Linux에서 Azure Web App을 사용한 Docker 허브 연속 배포](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png