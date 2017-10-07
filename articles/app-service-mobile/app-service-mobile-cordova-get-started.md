---
title: "Azure 앱 서비스 모바일 앱에 Cordova 앱 aaaCreate | Microsoft Docs"
description: "Apache Cordova 개발을 위한 Azure 모바일 앱 백 엔드를 사용 하 여 시작 자습서 tooget이를 수행 합니다."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: "cordova,javascript,모바일,클라이언트"
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a>Apache Cordova 앱 만들기
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>개요
이 자습서는 Azure 모바일 앱 백 엔드를 사용 하 여 클라우드 기반 백 엔드 tooadd tooan Apache Cordova 모바일 앱 서비스 하는 방법을 보여 줍니다.  새 모바일 앱 백 엔드와 앱 데이터를 Azure에 저장하는 간단한 *할 일 목록* Apache Cordova 앱을 만듭니다.

Azure 앱 서비스의 hello 모바일 앱 기능을 사용 하는 방법에 대 한 다른 모든 Apache Cordova 자습서에 대 한 필수 구성 요소는이 자습서를 완료 합니다.

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 필수 구성 요소는 hello 필요:

* [Visual Studio Community 2017] 이상이 설치된 PC
* [Visual Studio Tools for Apache Cordova]
* [활성 Azure 계정](https://azure.microsoft.com/pricing/free-trial/)

또한 Visual Studio를 무시 하 고 hello Apache Cordova 명령줄 직접 사용할 수 있습니다.  Hello 명령줄을 사용 하는 Mac 컴퓨터에 대 한 hello 자습서를 완료 하는 경우 유용 합니다.  Hello 명령줄을 사용 하는 Apache Cordova 클라이언트 응용 프로그램 컴파일을이 자습서에서 다루지 않습니다.

## <a name="create-an-azure-mobile-app-backend"></a>Azure 모바일 앱 백 엔드 만들기
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[유사한 단계를 보여 주는 비디오 보기](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a>Hello 서버 프로젝트를 구성 합니다.
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a>다운로드 하 고 hello Apache Cordova 앱 실행
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a>다음 단계
이 빠른 시작 자습서를 완료 했으므로 tooone의 자습서를 따라 hello에 이동 합니다.

* [오프 라인 데이터 추가](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova 앱.
* [인증 추가](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova 앱.
* [푸시 알림 추가](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova 앱.

Azure 앱 서비스의 주요 개념에 대해 자세히 알아봅니다.

* [오프라인 데이터]
* [인증]
* [푸시 알림]

Toouse Sdk hello 하는 방법에 대해 알아봅니다.

* [Apache Cordova SDK]
* [ASP.NET 서버 SDK]
* [Node.js 서버 SDK]

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[오프라인 데이터]: app-service-mobile-offline-data-sync.md
[인증]: app-service-mobile-auth.md
[푸시 알림]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET 서버 SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js 서버 SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
