---
title: "Unity iOS 배포에 대 한 Azure Mobile Engagement와 시작 됨 aaaGet"
description: "자세한 내용은 방법 tooiOS 장치를 배포 하는 Unity 앱에 대 한 분석 및 푸시 알림을 사용 하 여 Azure Mobile Engagement toouse 합니다."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a>Unity iOS 배포용 Azure Mobile Engagement 시작
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

이 항목에서는 Azure Mobile Engagement toounderstand toouse 앱 사용량과 tooan iOS 장치를 배포할 때 Unity 응용 프로그램의 알림을 toosegmented 사용자 밀어넣기 toosend 합니다.
이 자습서에서는 hello 클래식 Unity 롤 볼 자습서 hello 시작 지점으로 합니다. 이 hello 단계를 수행 해야 [자습서](mobile-engagement-unity-roll-a-ball.md) hello 자습서 아래 전시 우리는 Mobile Engagement 통합 hello 계속 하기 전에. 

이 자습서는 hello 다음을 사항이 필요합니다.

* [Unity 편집기](http://unity3d.com/get-unity)
* [Mobile Engagement Unity SDK](https://aka.ms/azmeunitysdk)
* XCode 편집기

> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started)을 참조하세요.
> 
> 

## <a id="setup-azme"></a>iOS 앱용 Mobile Engagement 설정
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결
### <a name="import-hello-unity-package"></a>Hello Unity 패키지 가져오기
1. Hello 다운로드 [Mobile Engagement Unity 패키지](https://aka.ms/azmeunitysdk) 고 tooyour 로컬 컴퓨터를 저장 합니다. 
2. 너무 이동**자산 패키지 가져오기-> 사용자 지정 패키지->** 및 선택 hello 패키지 단계 위에 hello을 다운로드 합니다. 
   
    ![][70] 
3. 모든 파일을 선택했는지 확인하고 **가져오기** 단추를 클릭합니다. 
   
    ![][71] 
4. 가져오기에 성공 하려면 프로젝트의 가져온 hello SDK 파일 표시 됩니다.  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a>Hello EngagementConfiguration 업데이트
1. Hello를 열고 **EngagementConfiguration** hello SDK 폴더 및 update hello에서 스크립트 파일 **IOS\_연결\_문자열** hello 연결 문자열에서 이전에 얻은 Azure 포털 안녕하세요에서.  
   
    ![][73]
2. Hello 파일을 저장 합니다. 

### <a name="configure-hello-app-for-basic-tracking"></a>기본 추적에 대 한 hello 응용 프로그램 구성
1. Hello를 열고 **PlayerController** 스크립트가 편집을 위해 toohello 플레이어 개체를 연결 합니다. 
2. Hello 다음 추가 문을 사용 하 여:
   
        using Microsoft.Azure.Engagement.Unity;
3. Hello toohello 다음 추가 `Start()` 메서드
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>배포 하 고 hello 앱 실행
1. IOS 장치 tooyour 컴퓨터를 연결 합니다. 
2. **파일 -> 빌드 설정**을 엽니다. 
   
    ![][40]
3. **iOS**를 선택한 후 **플랫폼 전환**을 클릭합니다.
   
    ![][41]
   
    ![][42]
4. **플레이어 설정** 을 클릭하고 유효한 번들 식별자를 제공합니다. 
   
    ![][53]
5. 마지막으로 **빌드 및 실행**
   
    ![][54]
6. 수 tooprovide 폴더 이름 toostore hello iOS 패키지를 요청 합니다. 
   
    ![][43]
7. 모든 세밀 하 게 되 면 hello 프로젝트를 컴파일해야 합니다 및 XCode 응용 프로그램에서 열 해야 하는 것입니다. 
8. 해당 hello 있는지 확인 **번들 식별자** hello 프로젝트에서 잘못 됩니다.  
   
    ![][75]
9. 이제 hello 패키지는 연결 된 장치에 배포 된 tooyour 하 고 휴대폰에서 Unity 게임을 표시 되어야 있도록 XCode에서 hello 앱 실행! 

## <a id="monitor"></a>실시간 모니터링과 앱 연결
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용
Mobile Engagement 사용 하면 사용자와 toointeract 및 도달 범위 푸시 알림과 앱 내 메시징을 캠페인의 hello 컨텍스트에서 사용 합니다. 이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.
Toodo의 추가 구성을 앱 tooreceive 알림에서 및에 대 한 설치 프로그램은 이미 있습니다.

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
