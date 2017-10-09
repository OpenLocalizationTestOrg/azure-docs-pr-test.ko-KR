---
title: "웹 앱에 대 한 Azure Mobile Engagement 시작 aaaGet | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure Mobile Engagement 웹 앱에 대 한 분석 및 푸시 알림입니다."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a>Web Apps용 Azure Mobile Engagement 시작
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

이 항목에서는 Azure Mobile Engagement toounderstand toouse 웹 응용 프로그램 사용 합니다.

> [!NOTE]
> hello Azure Mobile Engagement 서비스 년 3 월 2018 사용 중지 될 했으며 현재 사용 가능한 tooexisting 고객만 합니다. 자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.

이 자습서는 hello 다음을 사항이 필요합니다.

* Visual Studio 2015 또는 원하는 다른 편집기
* [웹 SDK](http://aka.ms/P7b453)

이 웹 SDK의 미리 보기에만 hello 순간에 분석 지원 및 브라우저 또는 앱에서 푸시 알림을 보내는 아직 지원 하지 않습니다. 

> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started)을 참조하세요.
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a>웹앱용 Mobile Engagement 설정
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결
이 자습서는 basic 통합"," hello 필요한 최소 집합 toocollect 데이터를 표시 합니다.

또한 Visual Studio 외부에서 만든 모든 웹 응용 프로그램과 hello 단계를 수행 하는 경우 기본 웹 응용 프로그램을 Visual Studio toodemonstrate hello 통합으로 만듭니다. 

### <a name="create-a-new-web-app"></a>새 웹앱 만들기
hello 다음 단계에서는 가정 hello를 사용 하 여 Visual Studio 2015의 hello 단계는 이전 버전의 Visual Studio에서 유사 합니다. 

1. Visual Studio를 시작 및 hello **홈** 화면에서 **새 프로젝트**합니다.
2. Hello 팝업에 선택 **웹** -> **ASP.Net 웹 응용 프로그램**합니다. Hello 앱 입력 **이름**, **위치** 및 **솔루션 이름**, 클릭 하 고 **확인**합니다.
3. Hello에 **´ ï ´** 선택 팝업에서 **빈** 아래 **ASP.Net 4.5 템플릿** 클릭 **확인**합니다. 

이제는 Azure Mobile Engagement 웹 SDK hello 통합할 새 빈 웹 응용 프로그램 프로젝트를 작성 했습니다.

### <a name="connect-your-app-toomobile-engagement-backend"></a>응용 프로그램 tooMobile Engagement 백 엔드 연결
1. 라는 새 폴더를 만들어 **javascript** 솔루션에 hello 웹 SDK JS 파일을 추가 하 고 **azure engagement.js** 넣습니다. 
2. 라는 새 파일 추가 **main.js** 이 hello 코드 다음 javascript 폴더에 있습니다. 있는지 tooupdate hello 연결 문자열을 확인 합니다. 이 `azureEngagement` 개체를 사용 하는 tooaccess 웹 SDK 메서드 됩니다. 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![js 파일이 포함된 Visual Studio입니다.][1]

## <a name="enable-real-time-monitoring"></a>실시간 모니터링 사용
순서 toostart 데이터를 보내고는 hello 사용자가 활성화 되도록 하나 이상의 활동 toohello Mobile Engagement 백 엔드를 보내야 합니다. 웹 응용 프로그램의 hello 컨텍스트에서 활동은 웹 페이지. 

1. 호출 하는 새 페이지를 만들고 **home.html** 솔루션 및 웹 앱에 대 한 페이지 hello 시작으로 설정 합니다. 
2. Hello body 태그 내 hello 다음을 추가 하 여 이전에이 페이지에에서 추가 하는 hello 두 javascript를 포함 합니다. 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. Hello body 태그 toocall EngagementAgent 업데이트 `startActivity` 메서드
   
        <body onload="engagement.agent.startActivity('Home')">
4. **home.html**은 다음과 같이 표시됩니다.
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a>실시간 모니터링과 앱 연결
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a>분석 확장
다음은 현재 분석에 사용할 수 있는 웹 SDK와 함께 사용할 수 있는 모든 hello 메서드:

1. 작업/웹 페이지:
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. 이벤트
   
        engagement.agent.sendEvent(name, extras);
3. 오류
   
        engagement.agent.sendError(name, extras);
4. 작업
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

