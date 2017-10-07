---
title: "aaaAzure Mobile Engagement 문제 해결 가이드"
description: "Azure Mobile Engagement용 문제 해결 가이드"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 31134a29-a513-4e5e-b626-f6cf6fe04769
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: dd69bfd7019907c3e1da8df590db3b5f61606173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---troubleshooting-guide"></a>Azure Mobile Engagement - 문제 해결 가이드
## <a name="introduction"></a>소개
문제 해결 가이드 hello 일부 일반적으로 나타나는 문제 및 됩니다의 근본 원인을 직접 tootroubleshoot 사용을 이해 하는 데 도움이 됩니다. 

## <a name="general"></a>일반
일반적으로 hello 다음은 항상 확인 해야 합니다.

1. 에 설명 된 대로 통합에 필요한 모든 hello 단계를 수행한 확인 우리의 [자습서 시작](mobile-engagement-windows-store-dotnet-get-started.md)
2. Hello hello 플랫폼 Sdk의 최신 버전을 사용 하는 합니다. 
3. 몇 가지 문제는 특정 tooemulator만 때문에 실제 장치와 에뮬레이터에서 테스트 합니다. 
4. [여기](../azure-subscription-service-limits.md)
5. 수 없는 경우 tooconnect toohello Mobile Engagement 서비스 백 엔드 또는 데이터가 지속적으로 로드 되 고 있지 다음이 확인 하 여 현재 진행 중인 서비스 보안 문제가 있는지 확인 하는 [여기](https://azure.microsoft.com/status/)

## <a name="monitor-issues"></a>'모니터' 문제
### <a name="i-am-not-seeing-my-device-showing-up-on-hello-monitor-tab"></a>Hello 모니터 탭에서 표시 장치가 표시 되지 않는
모니터 탭 hello 장치 연결 된 tooyour Mobile Engagement 플랫폼을 실시간으로 표시 됩니다. 에뮬레이터 및 장치에서 디버깅하는 경우 여기에 하나 이상의 세션이 표시되어야 합니다. Hello 앱 배포 된 hello 계기에는 실시간으로 플랫폼에 연결 된 toohello 있는 hello 장치를 반영 하는 활성 세션 표시 됩니다. 

장치 hello 모니터 탭이 표시 되지 않는 경우 가능성이 높습니다 SDK 통합 문제입니다. 몇 가지 일반적인 단계 tootake tootroubleshoot은 다음과 같습니다.

1. Hello 모바일 앱에서 hello 올바른 연결 문자열을 사용 하는 hello SDK 키 섹션 및 API 키 섹션 하지 hello 인지 확인 합니다. hello 연결 문자열 연결 모바일 앱 toohello 인스턴스의 hello Mobile Engagement 응용 프로그램에 있는 장치 hello 모니터 탭에서 볼 수 있습니다. 
2. Windows 플랫폼-hello를 재정의 하는 페이지에 경우에 대 한 `OnNavigatedTo` 메서드를 확인 하는지 toocall `base.OnNavigatedTo(e)`합니다.
3. Mobile Engagement 기존 모바일 앱에 통합 하는 경우 통합 단계 고급 hello 확인 하 여 모든 단계를 누락 되지 않았는지를 확인할 수도 있습니다 [여기](mobile-engagement-windows-store-integrate-engagement.md)
4. 확인 작업이 하나 이상 화면 hello에 설명 된 대로 작업 하는 hello 플랫폼에 따라 EngagementActivity 있는 hello 페이지를 재정의 하 여 보내는 [시작 자습서](mobile-engagement-windows-store-dotnet-get-started.md)합니다.

### <a name="i-am-seeing-hello-monitor-tab-showing-a-session-even-when-i-have-disconnected-or-closed-my-app-emulator"></a>세션을 보여 주는 hello 모니터 탭 못한도 경우 I disconnected 했거나 내 앱을 닫을 / 에뮬레이터입니다.
이 시점에서 하나의 연결 된 toohello 플랫폼 hello 사용 중인 에뮬레이터 tooopen hello 응용 프로그램을 사용 하는 경우 이것이 가능성이 tooemulator quirks 때문입니다. 일반적으로 다시 돌아오는 toohello 홈 화면 앱 세션 toodisconnect hello에 대 한 hello 에뮬레이터에서 성공적으로 tooensure를 해야 합니다. 또한 Windows 플랫폼에서 Visual Studio를 사용 하 여 디버깅 하는 동안 해야 Visual Studio에서 toohello 이동 tooensure **수명 주기 이벤트** 를 클릭 하 고 메뉴 모음 **Suspend** tooreally 닫기 hello 세션입니다. 자세한 내용은 [Windows 자습서](mobile-engagement-windows-store-dotnet-get-started.md) 를 참조하세요. 

## <a name="analytics-issues"></a>'분석' 문제
### <a name="i-am-not-seeing-any-data-refreshed-data-on-analytics-tab"></a>분석 탭에 데이터/새로 고친 데이터가 나타나지 않습니다.
분석 데이터는 정기적으로 다시 계산되고 이 새로 고침에 대해 최대 24시간까지 걸릴 수 있습니다. 이 데이터는 실시간이 아니며 24시간 기간 내에서 새로 고침이 표시됩니다.
하지만 하십시오 확인 된 재정의 중 하나 이상 한 페이지씩 적어도 한 화면 또는 활동 toohello 플랫폼 백 엔드 보내고는 `EngagementActivity` 호출 또는 `SendActivity` explcitly 합니다. 

### <a name="i-am-seeing-incorrectly-captured-datetime-for-a-device-on-hello-analytics-tab"></a>장치에 대해 캡처되지 날짜/시간 hello 분석 탭 표시
hello 분석에 대 한 시간 동안은 날짜에 따라 hello hello 사용자의 장치 설정에서 합니다. 해당 hello 있도록 장치에 hello 날짜가 올바르게 설정 합니다. 

## <a name="segment-issues"></a>'세그먼트' 문제
### <a name="i-created-a-segment-and-it-is-showing-up-as-greyed-out-or-not-showing-any-data"></a>세그먼트를 만들었는데 회색으로 표시되거나 데이터가 표시되지 않습니다.
세그먼트 만들기 hello 순간에 실시간 하지 않습니다. 동일한 hello 분석 데이터 집계 및 최대 24 시간이 걸릴 수도 있으므로 시간 hello에 계산 됩니다. 하면 해야 나중에 다시 확인 하지만 한편도 확인 해야 모바일 앱 hello 세그먼트를 형성 되는 hello 기준 hello 데이터를 보내는 실제로 됩니다. 예: = foo hello 기준으로 이벤트 말 'foo' 되지 모든 모바일 장치에서 전송 되는 다음 EventName를 사용 하 여 만든 세그먼트에 대 한 세그먼트 데이터 수 없게 하는 경우. SDK 통합 tooensure 확인 해야 모바일 앱 hello 데이터를 올바르게 전송 됩니다. 

## <a name="reach-or-push-notifications-issues"></a>'도달률' 또는 푸시 알림 문제
### <a name="my-push-messages-are-not-being-delivered"></a>푸시 메시지 전달되지 않습니다.
1. 모든 hello 구성 요소-모바일 앱, SDK 및 hello 서비스 되는지 수 있고 올바르게 연결 되어 있으며 toodeliver 푸시 알림을 알림 tooa 테스트 장치 첫 번째 tooensure를 보내 보십시오. 
2. 예약 되지 않았으면는 캠페인을 통해 항상 hello 가장 간단한 '응용 프로그램의 알림'을 보내기 및 나 지정 된 모든 대상 그룹 조건을 포함 합니다. 알림 연결이 올바르게 작동 하는지 tooprove 역시입니다. 
3. 발생 하는 경우 좋은 또한 앱에서 알림 배달의 문제 먼저 응용 프로그램의 알림 보내기 tootry 1 단계. 
4. 모바일 앱에 대해 올바르게 구성 되어 ' 네이티브 푸시 ' 해당 hello를 확인 합니다. Hello 플랫폼에 따라 키 (Android, Windows) 또는 인증서 (iOS) 하거나 포함 됩니다 것입니다. 자세한 내용은 [사용자 인터페이스 - 설정](mobile-engagement-user-interface-settings.md)
5. 알림을 hello에 의해 차단 될 수도 앱 외 hello 모바일 운영 체제 있도록이 통해 사용자 hello 경우 되지 않습니다. 
6. Hello를 설정 하지 않으면는 확인 *대상 그룹 무시, 푸시가 전송 되지 hello API 통해 toousers* hello에 대 한 옵션 **캠페인** 의 도달 범위는 섹션에는 이렇게 하면 해당 푸시 캠페인 알림 Api를 통해 보낼 수만 있습니다. 
7. 모두 연결 된 장치와 WIFI 및 전화 연산자 네트워크 tooeliminate hello 네트워크 연결을 통해 문제의 가능한 원인으로 푸시 캠페인을 테스트 하 고 확인 하십시오.
8. 해당 hello 시스템 모든 동기화 장치 hello 푸시 알림 서비스의 기능 toodeliver 알림을 방해할도 때문에 장치/에뮬레이터에서 날짜/시간 올바른지 합니다. 

더 많은 플랫폼 관련 문제 해결 지침:

1. **iOS** 
   
   * Hello 인증서가 유효 하 고 푸시 알림을 iOS에 대 한 만료 되지 않은 지 확인 합니다. 
   * 모바일 고객 관리 앱에서 *프로덕션* 인증서를 올바르게 구성되었는지 확인합니다. 
   * *실제, 물리적 장치*에서 테스트하고 있는지 확인합니다. hello iOS 시뮬레이터는 푸시 메시지를 처리할 수 없습니다.
   * 해당 hello 번들 식별자 hello 모바일 앱에 올바르게 구성 되어 있는지 확인 합니다. Hello 지침을 참조 [여기](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)
   * 테스트할 때 모바일 프로비저닝 프로필에서 "임시" 배포를 사용합니다. "Debug"를 사용 하 여 응용 프로그램은 컴파일된 경우 수 tooreceive 알림 수 없습니다.
2. **Android**
   
   * \N 문자로 이어지는 모바일 앱의 AndroidManifest.xml 파일에 hello 올바른 프로젝트 수를 지정 했는지 확인 합니다. 
     
           <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
   * 누락 된 하거나 hello Android 매니페스트 파일에서 모든 권한을 잘못 구성 확인 
   * Hello hello GCM 서버 키 정답 같은 계정에서 tooyour 클라이언트 응용 프로그램을 추가 하는 hello 프로젝트 번호 인지 확인 합니다. 두 개의 hello 간의 불일치 나 가지 프로그램 푸시 수 없게 됩니다. 
   * 시스템 발생 하는 경우 알림을 하지만 하지 앱에서 다음 hello를 검토 [알림 섹션에 대 한 아이콘을 지정](mobile-engagement-android-get-started.md) 것으로 지정 하지 않는 경우 hello 올바른 아이콘 hello Android 매니페스트 파일에 있습니다. 
   * 외부 이미지 서버가 다음 toobe 수 toosupport HTTP 필요한 경우 다음 BigPicture 알림을 보내는 경우 "GET" 및 "HEAD"입니다.
3. **Windows**
   
   * 유효한 Windows 스토어 앱과 hello 앱에 연결 했는지 확인 합니다. Visual Studio-에서 tooright hello 프로젝트를 클릭 하 고 "스토어와 앱 연결" 옵션 및 hello Windows 스토어에서에서 만든 선택 hello 앱을 선택 해야 합니다. 이 Windows 스토어 앱에는 hello 네이티브 푸시 자격 증명 tooconfigure hello Mobile engagement 연결 포털에서 가져온 위치에서 같은 hello 이어야 합니다.
   * `EngagementOverlay` 통합으로 앱 내 알림이 아닌 앱 푸시 알림을 수신하는 경우 페이지에 루트 grid 요소가 있는지 확인합니다. EngagementOverlay 페이지 xaml 파일 tooadd 두 웹 보기에서 찾은 hello 첫 번째 "그리드" 요소를 사용 합니다. 하지만 웹 보기를 설정할 toolocate 원하는 tooensure 해야 "EngagementGrid" 다음과 같은 명명 된 표를 정의할 수 있습니다는 충분 한 높이 및 너비 hello에 대 한 후속 웹 hello 알림이 표시 되며 다음 hello를 뷰 앱에서 알림으로 알림입니다.
     
           <Grid x:Name="EngagementGrid"></Grid>

### <a name="i-created-a-push-notificationannouncement-campaign-and-even-after-it-sent-me-hello-notification-it-is-showing-as-active-what-does-it-mean"></a>푸시 알림/알림 만든/캠페인 및 'Active'로 표시 되어이 나에 게 hello 알림, 후에 있습니다. 무엇을 의미하나요?
hello **캠페인** 호출 Mobile Engagement에서 만든 새 장치 연결 tooyour 모바일 참여 플랫폼으로 장기 실행 푸시 알림 의미 이기 때문에 자동으로 전송 됩니다 hello 알림 되므로 여기에서 hello 캠페인에서 설정한 hello 조건을 만족 하으로 구성할 수 있습니다. 일회성 단일 알림 설정이 아닙니다. Hello 클릭 toomanually 가지게 **마침** tooterminate hello 캠페인 단추를 추가로 보낼 알림 하지 않습니다. 

### <a name="i-created-a-push-campaign-and-i-am-receiving-notifications-successfully-however-whenever-i-open-up-hello-app-i-get-hello-same-notification-even-when-i-had-actioned-it-before"></a>그러나 푸시 캠페인 만들고를 받고 알림 했습니다. hello 앱을 열 때마다 습 hello 조치를 취한 해야 했던 경우에 같은 알림 전에?
테스트 중 가능성이 toohappen와 에뮬레이터 또는 TestFlight와 같은 일부 테스트 프레임 워크를 사용 하는 경우입니다. 다음 인스턴스를 실행 하는 모든 앱에는 새 DeviceID를 획득 하 hello Mobile Engagement 플랫폼 tootreat를 유발 하는 백 엔드 tooour 보내는 일어나는 새 장치 및 hello 알림을 보내는 것입니다. 

## <a name="getting-support"></a>지원 받기
직접 없습니다 tooresolve hello 문제는 경우 다음을 수행할 수 있습니다.

1. StackOverflow 포럼에 기존 스레드가 hello에서 문제에 대 한 검색 및 [MSDN 포럼](https://social.msdn.microsoft.com/Forums/windows/en-US/home?forum=azuremobileengagement) 질문을 요청 하지 하는 경우에 한 합니다. 
2. 에 없기 때문에 다음 추가/투표 hello 요청에 대 한 기능을 찾을 경우 우리의 [UserVoice 포럼](https://feedback.azure.com/forums/285737-mobile-engagement/)
3. 있는 경우 Microsoft 지원 Open 지원 인시던트 hello 다음 세부 정보를 제공 하 여: 
   * Azure 구독 ID
   * 플랫폼(예:: iOS, Android 등)
   * 앱 ID
   * 캠페인 ID(푸시 알림 문제의 경우)
   * 장치 ID
   * 모바일 고객 관리 SDK 버전(예: Android SDK v2.1.0)
   * 정확한 오류 메시지 및 시나리오가 있는 오류 세부 정보

