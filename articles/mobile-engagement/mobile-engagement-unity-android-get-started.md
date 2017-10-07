---
title: "Unity Android 배포에 대 한 Azure Mobile Engagement와 시작 됨 aaaGet"
description: "자세한 내용은 방법 tooiOS 장치를 배포 하는 Unity 앱에 대 한 분석 및 푸시 알림을 사용 하 여 Azure Mobile Engagement toouse 합니다."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a>Unity Android 배포용 Azure Mobile Engagement 시작
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

이 항목에서는 Azure Mobile Engagement toounderstand toouse 앱 사용량과 tooan Android 장치를 배포할 때 Unity 응용 프로그램의 알림을 toosegmented 사용자 밀어넣기 toosend 합니다.
이 자습서에서는 hello 클래식 Unity 롤 볼 자습서 hello 시작 지점으로 합니다. 이 hello 단계를 수행 해야 [자습서](mobile-engagement-unity-roll-a-ball.md) hello 자습서 아래 전시 우리는 Mobile Engagement 통합 hello 계속 하기 전에. 

이 자습서는 hello 다음을 사항이 필요합니다.

* [Unity 편집기](http://unity3d.com/get-unity)
* [Mobile Engagement Unity SDK](https://aka.ms/azmeunitysdk)
* Google Android SDK

> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started)을 참조하세요.
> 
> 

## <a id="setup-azme"></a>Android 앱용 Mobile Engagement 설정
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
1. Hello를 열고 **EngagementConfiguration** hello SDK 폴더 및 update hello에서 스크립트 파일 **ANDROID\_연결\_문자열** hello 연결 문자열에서 가져온 Azure 포털 안녕하세요 이전 버전에서.  
   
    ![][73]
2. Hello 파일 저장 
3. **파일 -> Engagement -> Android 매니페스트 생성**을 실행합니다. Mobile Engagement SDK hello로 추가 하는 hello 플러그 인이 고 클릭 하 여 프로젝트 설정을 자동으로 업데이트 됩니다. 
   
    ![][74]

> [!IMPORTANT]
> Hello는 업데이트할 때마다 있는지 tooexecute이 확인 **EngagementConfiguration** 파일 그렇지 않으면 hello 응용 프로그램에서 변경 내용을 반영 되지 것입니다. 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a>기본 추적에 대 한 hello 응용 프로그램 구성
1. Hello를 열고 **PlayerController** 스크립트가 편집을 위해 toohello 플레이어 개체를 연결 합니다. 
2. Hello 다음 추가 문을 사용 하 여:
   
        using Microsoft.Azure.Engagement.Unity;
3. Hello toohello 다음 추가 `Start()` 메서드
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>배포 하 고 hello 앱 실행
Android SDK가이 Unity 앱 tooyour 장치 toodeploy를 시도 하기 전에 컴퓨터에 설치 되어 있는지 확인 합니다. 

1. Android 장치 tooyour 컴퓨터를 연결 합니다. 
2. **파일 -> 빌드 설정**을 엽니다. 
   
    ![][40]
3. **Android**를 선택한 후 **플랫폼 전환**을 클릭합니다.
   
    ![][51]
   
    ![][52]
4. **플레이어 설정** 을 클릭하고 유효한 번들 식별자를 제공합니다. 
   
    ![][53]
5. 마지막으로 **빌드 및 실행**
   
    ![][54]
6. 수 tooprovide 폴더 이름 toostore hello Android 패키지를 요청 합니다. 
7. 모든 작업이 제대로 hello 패키지 되는 연결 된 배포 tooyour 경우가 경우 장치의 휴대폰에서 Unity 게임을 표시 됩니다! 

## <a id="monitor"></a>실시간 모니터링과 앱 연결
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a>Hello EngagementConfiguration 업데이트
1. Hello를 열고 **EngagementConfiguration** hello SDK 폴더 및 update hello에서 스크립트 파일 **ANDROID\_GOOGLE\_번호** hello로 **Google 프로젝트 번호** hello Google 클라우드 개발자 포털에서 이전에 얻은 합니다. 이 문자열 값 이므로 tooenclose 있는지 확인 해야 큰따옴표에서 합니다. 
   
    ![][75]
2. Hello 파일을 저장 합니다. 
3. **파일 -> Engagement -> Android 매니페스트 생성**을 실행합니다. Mobile Engagement SDK hello로 추가 하는 hello 플러그 인이 고 클릭 하 여 프로젝트 설정을 자동으로 업데이트 됩니다. 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a>Hello 앱 tooreceive 알림 구성
1. Hello를 열고 **PlayerController** 스크립트가 편집을 위해 toohello 플레이어 개체를 연결 합니다. 
2. Hello toohello 다음 추가 `Start()` 메서드
   
        EngagementReachAgent.Initialize();
3. Hello 응용 프로그램을 업데이트 했으므로 배포 하 고 장치 hello 지침 아래에 제공 된 기준에 hello 앱을 실행 합니다. 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
