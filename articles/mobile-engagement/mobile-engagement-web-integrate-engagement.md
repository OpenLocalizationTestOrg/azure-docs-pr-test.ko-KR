---
title: "Mobile Engagement 웹 SDK 통합 aaaAzure | Microsoft Docs"
description: "최신 업데이트 및 hello Azure Mobile Engagement 웹 SDK에 대 한 절차 hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a>웹 응용 프로그램에 Azure Mobile Engagement 통합
> [!div class="op_single_selector"]
> * [Windows 범용](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

hello 가장 간단한 방법은 tooactivate hello 분석 워크 로드와 웹 응용 프로그램에서 Azure Mobile Engagement의 함수 모니터링이 문서의 hello 절차에 설명 합니다.

Hello 단계 tooactivate hello 로그 있는 보고서를 필요한 toocompute 사용자, 세션, 활동, 충돌 및 technicals 하는 방법에 대 한 모든 통계를 따릅니다. 이벤트, 오류, 작업 및 등의 응용 프로그램에 따라 통계에 대 한 hello Azure Mobile Engagement API를 사용 하 여 로그 보고서를 수동으로 활성화 해야 있습니다. 자세한 내용은 [어떻게 toouse hello 고급 Mobile Engagement 웹 응용 프로그램에서 API 태깅](mobile-engagement-web-use-engagement-api.md)합니다.

## <a name="introduction"></a>소개
[Hello Azure Mobile Engagement 웹 SDK 다운로드](http://aka.ms/P7b453)합니다.
hello 모바일 Engagement 웹 SDK는 단일 JavaScript 파일 요소로 제공 되며, azure engagement.js 있는 사이트 또는 웹 응용 프로그램의 각 페이지에서 tooinclude 합니다.

> [!IMPORTANT]
> 이 스크립트를 실행 하기 전에 스크립트를 실행 하거나 코드 조각 tooconfigure Mobile Engagement 응용 프로그램에 대해 작성 해야 합니다.
> 
> 

## <a name="browser-compatibility"></a>브라우저 호환성
Mobile Engagement 웹 SDK hello 네이티브 JSON 인코딩 및 디코딩, 또한: toocross 도메인 AJAX 요청 (hello W3C CORS 사양에 의존)를 사용 합니다. 브라우저를 수행 하는 hello와 호환 되는지:

* Microsoft Edge 12+
* Internet Explorer 10+
* Firefox 3.5+
* Chrome 4+
* Safari 6+
* Opera 12+

## <a name="configure-mobile-engagement"></a>Mobile Engagement 구성
전역 만드는 스크립트를 작성 `azureEngagement` hello 다음 예제와 같이 JavaScript 개체입니다. 사이트에 여러 개의 페이지가 있을 수 있으므로 이 예제에서는 이 스크립트가 모든 페이지에 포함되어 있다고 가정합니다. 이 예제에서는 hello JavaScript 개체 이름은 `azure-engagement-conf.js`합니다.

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

hello `connectionString` hello Azure 포털을 응용 프로그램에 표시 됩니다에 대 한 값입니다.

> [!NOTE]
> `appVersionName` 및 `appVersionCode`는 선택 사항입니다. 그러나 분석할 때 프로세스 버전 정보가 처리될 수 있도록 구성하는 것이 좋습니다.
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a>페이지에 Mobile Engagement 스크립트 포함
Mobile Engagement 스크립트 tooyour 페이지 hello 같은 방법으로 다음 중 하나에 추가 합니다.

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

또는 다음을 사용하세요.

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a>Alias
Hello 만듭니다 hello Mobile Engagement 웹 SDK 스크립트를 로드 한 다음 **engagement** 별칭 tooaccess hello SDK Api입니다. 이 별칭 toodefine hello SDK 구성을 사용할 수 없습니다. 이 별칭은 이 설명서에서 참조로 사용됩니다.

Note는 hello 기본 별칭 충돌 페이지에서 다른 전역 변수를 재정의할 수 hello 구성에서 다음과 같이 hello Mobile Engagement 웹 SDK를 로드 하기 전에:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a>기본 보고
Mobile Engagement의 기본 보고 기능에는 사용자, 세션, 활동 및 작동 중단에 대한 통계와 같은 세션 수준 통계가 포함됩니다.

### <a name="session-tracking"></a>세션 추적
Mobile Engagement 세션은 일련의 활동으로 나뉘며 각각이 이름으로 식별됩니다.

기존 웹 사이트는 사이트의 각 페이지에서 서로 다른 활동을 선언하는 것이 좋습니다. 웹 사이트 또는 웹 응용 프로그램의 어떤 hello에서 현재 페이지는 바뀌지 경우 hello 페이지 내에서 같은 소규모, tootrack hello 활동을 할 수 있습니다.

하거나, toostart 또는 변경 hello 현재 사용자 작업을 호출 hello `engagement.agent.startActivity` 함수입니다. 예:

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

Mobile Engagement 서버 hello hello 응용 프로그램 페이지를 닫은 후 3 분 이내 세션이 열린를 자동으로 종료 됩니다.

또는 `engagement.agent.endActivity`를 호출하여 세션을 수동으로 종료할 수 있습니다. 이 옵션은 현재 사용자 활동 too'Idle hello 설정 합니다.'  hello 세션 하지 않는 한 10 초 후 종료 됩니다 새 호출을 통해서도`engagement.agent.startActivity` hello 세션을 다시 시작 합니다.

Hello 글로벌 engagement 개체에 hello 10 초 지연 시간을 다음과 같이 구성할 수 있습니다.

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> 사용할 수 없는 `engagement.agent.endActivity` hello에 `onunload` 콜백이이 단계에서 AJAX 호출을 변경할 수 없습니다.
> 
> 

## <a name="advanced-reporting"></a>고급 보고
필요에 따라 tooreport 응용 프로그램별 이벤트, 오류 및 작업을 하려는 경우에 toouse hello Mobile Engagement API 필요 합니다. Hello를 통해 Mobile Engagement API hello 액세스 `engagement.agent` 개체입니다.

모든 hello 고급 hello Mobile Engagement API에서에서 Mobile Engagement의 기능에 액세스할 수 있습니다. hello API hello 문서에 자세히 설명 되어 [어떻게 toouse hello 고급 Mobile Engagement 웹 응용 프로그램에서 API 태깅](mobile-engagement-web-use-engagement-api.md)합니다.

## <a name="customize-hello-urls-used-for-ajax-calls"></a>AJAX 호출에 사용 되는 hello Url을 사용자 지정
Mobile Engagement 웹 SDK를 사용 하 여 해당 hello Url을 사용자 지정할 수 있습니다. 예를 들어 tooredefine hello 로그 URL (hello SDK 끝점 로깅에 대 한), hello 구성을 재정의할 수 있습니다 다음과 같이 합니다.

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

URL 함수로 시작 하는 문자열을 반환 하는 경우 `/`, `//`, `http://`, 또는 `https://`, hello 기본 스키마가 사용 되지 않습니다. 기본적으로 hello `https://` 구성표 해당 Url에 사용 됩니다. Toocustomize hello 기본 체계를 사용 하도록 하려는 경우 다음과 같이 hello 구성을 재정의 합니다.

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
