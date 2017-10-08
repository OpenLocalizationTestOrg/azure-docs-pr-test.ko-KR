---
title: "Windows 범용 앱 Azure Mobile Engagement aaaGet 시작"
description: "자세한 내용은 방법 toouse Azure Mobile Engagement Windows 유니버설 앱에 대 한 분석 및 푸시 알림입니다."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a>Windows 유니버설 앱용 Azure Mobile Engagement 시작
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

이 항목에서는 Azure Mobile Engagement toounderstand toouse 응용 프로그램 사용 및 송신 푸시 Windows 유니버설 응용 프로그램의 알림을 toosegmented 사용자입니다.
이 자습서에는 hello 간단한 브로드캐스트 시나리오를 Mobile Engagement를 사용 하 여 보여 줍니다. WNS(Windows 알림 서비스)를 사용하여 푸시 알림을 받고 기본적인 앱 사용 데이터를 수집하는 빈 Windows 유니버설 앱을 만듭니다.

> [!NOTE]
> hello Azure Mobile Engagement 서비스 년 3 월 2018 사용 중지 될 했으며 현재 사용 가능한 tooexisting 고객만 합니다. 자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.

## <a name="prerequisites"></a>필수 조건
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a>Windows 유니버설 앱용 Mobile Engagement 설정
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결
이 자습서는 기본적인 "통합", 최소한의 hello 필요한 toocollect 데이터 설정 되 고 푸시 알림을 보내는 표시 합니다. hello에 hello 완벽 한 통합 설명서를 확인할 수 있습니다 [Mobile Engagement Windows 유니버설 SDK 통합](mobile-engagement-windows-store-sdk-overview.md)합니다.

Visual Studio toodemonstrate hello 통합 된 기본 응용 프로그램을 만듭니다.

### <a name="create-a-windows-universal-app-project"></a>Windows 유니버설 앱 프로젝트 만들기
hello 다음 단계에서는 가정 hello를 사용 하 여 Visual Studio 2015의 hello 단계는 이전 버전의 Visual Studio에서 유사 합니다.

1. Visual Studio를 시작 및 hello **홈** 화면에서 **새 프로젝트**합니다.
2. Hello 팝업에 선택 **Windows** -> **유니버설** -> **비어 있는 앱 (유니버설 Windows)**합니다. Hello 앱 입력 **이름** 및 **솔루션 이름**, 클릭 하 고 **확인**합니다.

    ![][1]

이제는 다음 hello Azure Mobile Engagement SDK가 통합 Windows 유니버설 앱 프로젝트를 작성 했습니다.

### <a name="connect-your-app-toomobile-engagement-backend"></a>응용 프로그램 tooMobile Engagement 백 엔드 연결
1. Hello 설치 [MicrosoftAzure.MobileEngagement] 프로젝트에서 Nuget 패키지 합니다. Windows 및 Windows Phone 플랫폼을 대상으로 하는 경우 필요한 toodo이 두 프로젝트에 대 한 합니다. Windows 8.x 및 Windows Phone 8.1 hello 같은 Nuget 패키지 위치 hello 올바른 플랫폼별 바이너리 각 프로젝트에 있습니다.
2. 열기 **Package.appxmanifest** 기능에 따라 해당 hello 있습니다 추가 되어 있는지 확인 하 고 있습니다.

        Internet (Client)

    ![][2]
3. 이제 Mobile Engagement 응용 프로그램에 대 한 앞에서 복사한 hello 연결 문자열을 복사 하 고 hello에 붙여 `Resources\EngagementConfiguration.xml` hello 간의 파일 `<connectionString>` 및 `</connectionString>` 태그:

    ![][3]

    > [!TIP]
    > 앱이 Windows와 Windows Phone 플랫폼을 모두 대상으로 하는 경우 여전히 지원하는 각 플랫폼에 하나씩 두 개의 Mobile Engagement 응용 프로그램을 만들어야 합니다. Hello 대상 그룹의 올바른 분할을 만들 수는 각 플랫폼에 대 한 대상된 적절 하 게 알림을 보낼 수를 두 응용 프로그램이 있으면이 보장 합니다.

    > [!IMPORTANT]
    > NuGet 자동으로 복사할 수 없습니다 hello SDK 리소스 Windows 10 UWP 응용 프로그램에서. 설정한 toodo hello Nuget 패키지가 설치 된 경우 (readme.txt)을 표시 하는 hello 단계를 수동으로 수행 합니다.  

1. Hello에 `App.xaml.cs` 파일:

    a. Hello 추가 `using` 문:

            using Microsoft.Azure.Engagement;

    b. Hello Engagement 초기화 하는 메서드를 추가 합니다.

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    c. Hello에 SDK hello 초기화 **OnLaunched** 메서드:

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    c. Hello에 hello 다음 삽입 **OnActivated** 메서드 하 고 이미 존재 하지 않는 경우 hello 메서드를 추가 합니다.

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <a id="monitor"></a>실시간 모니터링 사용
데이터를 전송 하는 toostart 및는 hello 사용자가 활성화 되도록 하나 이상 화면 (활동) toohello Mobile Engagement 백 엔드를 전송 해야 합니다.

1. Hello에 **MainPage.xaml.cs**, hello 다음 추가 `using` 문:

    Microsoft.Azure.Engagement.Overlay; 사용
2. 기본 클래스 hello 변경 **MainPage** 에서 **페이지** 너무**EngagementPageOverlay**:

        class MainPage : EngagementPageOverlay
3. Hello에 `MainPage.xaml` 파일:

    a. Tooyour 네임 스페이스 선언을 추가 합니다.

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    b. Hello 대체 **페이지** hello XML 태그 이름에 **engagement: EngagementPageOverlay**

> [!IMPORTANT]
> 페이지 hello를 재정의 하는 경우 `OnNavigatedTo` 메서드 수 있는지 toocall `base.OnNavigatedTo(e)`합니다. 그렇지 않으면 hello 활동 보고 되지 않습니다 `EngagementPage` 호출 `StartActivity` 내 해당 `OnNavigatedTo` 메서드). 이 Windows Phone 프로젝트에서 특히 중요 hello 기본 서식 파일에 있는 한 `OnNavigatedTo` 메서드.
>
> 에 대 한 **Windows 10 유니버설 앱**, hello에서 권장 하는 hello 메서드를 사용 하 여 "권장 되는 방법: 페이지 클래스 오버 로드" 섹션의 [고급 hello Windows 유니버설 앱 Engagement SDK로 보고](mobile-engagement-windows-store-advanced-reporting.md) 위에서 설명한 하나는 hello 대신 합니다.

## <a id="monitor"></a>실시간 모니터링과 앱 연결
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용
Mobile Engagement toointeract 있으며 푸시 알림과 앱 내 메시징을 캠페인의 hello 컨텍스트에서 사용자에 게 도달 합니다. 이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.
hello 다음 섹션에서는 앱 tooreceive를 속성을 설정.

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a>사용자 응용 프로그램 tooreceive WNS 푸시 알림을 사용 하도록 설정
1. Hello에 `Package.appxmanifest` 파일 hello에 **응용 프로그램** 탭의 **알림**설정, **알림 가능:** 너무**예**

    ![][5]

### <a name="initialize-hello-reach-sdk"></a>REACH SDK hello를 초기화 합니다.
`App.xaml.cs`, 호출 **EngagementReach.Instance.Init(e);** hello에 **InitEngagement** hello 에이전트 초기화 직후 함수:

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

준비 toosend 알림을 것입니다. 그런 다음 이 기본 통합을 제대로 수행했는지 확인합니다.

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a>권한 부여 액세스 tooMobile Engagement toosend 알림
1. 웹 브라우저에서 [Windows 스토어 개발자 센터]를 열어 로그인하고 필요한 경우 계정을 만드십시오.
2. 클릭 **대시보드** hello 오른쪽 위 코너 한 다음 클릭 **새 앱 만들기** hello 왼쪽된 패널 메뉴에서 합니다.

    ![][9]
3. 해당 이름을 예약하여 앱을 만듭니다.

    ![][10]
4. Hello 응용 프로그램을 만든 후 너무 이동**서비스에 푸시 알림을->** hello 왼쪽된 메뉴에서 합니다.

    ![][11]
5. Hello에 푸시 알림 섹션을 hello 클릭 **Live 서비스 사이트** 링크 합니다.

    ![][12]
6. Toohello 푸시 자격 증명 섹션을 이동 하는 경우. Hello에 있는지 확인 **앱 설정** 섹션 및 다음 복사 프로그램 **패키지 SID** 및 **클라이언트 암호**

    ![][13]
7. Toohello 이동 **설정** Mobile Engagement 포털의 hello를 클릭 하 고 **하 여 네이티브 푸시** hello 왼쪽에는 섹션입니다. 클릭 hello **편집** 단추 tooenter 프로그램 **패키지 보안 식별자 (SID)** 하였고 **비밀 키** 표시 된 것 처럼:

    ![][6]
8. 마지막으로 hello 앱 스토어에서이 작성된 된 앱과 Visual Studio 응용 프로그램에 연결 했는지 확인 합니다. Visual Studio의 **스토어에 앱 연결**을 클릭합니다.

    ![][7]

## <a id="send"></a>보낼 알림 tooyour 앱
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Hello 앱이 실행 중인 앱 내 알림이 표시 됩니다. 그렇지 않으면 hello 앱 닫혀 있는 경우에 알림 메시지 표시 합니다.
경우에 앱에서 알림을 하지만 하지 알림 메시지를 표시 하 고 hello 앱 Visual Studio에서 디버그 모드에서 실행 하는 **수명 주기 이벤트 Suspend->** hello 도구 모음 tooensure hello 이러한 앱이 중지 됩니다. Visual Studio에서 hello 응용 프로그램을 디버깅 하는 동안 hello 홈 단추를 클릭 한 경우 다음 해당 하지 않는 항상 일시 중단 하 고 알림 메시지로 표시 되지 hello 알림이 앱에 표시 하는 동안.  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Windows 스토어 개발자 센터]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
