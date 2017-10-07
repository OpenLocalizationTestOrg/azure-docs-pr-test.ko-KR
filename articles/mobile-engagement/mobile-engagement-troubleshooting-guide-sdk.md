---
title: "aaaAzure Mobile Engagement 문제 해결 가이드-SDK"
description: "Azure Mobile Engagement에서 SDK 통합 문제 해결"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a>SDK 통합 문제에 대한 문제 해결 가이드
hello 다음은 Azure Mobile Engagement 응용 프로그램에 통합 하는 방법에 발생할 수 있는 관련 문제입니다.

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a>응용 프로그램의 다른 영역에서 발생한 오류를 통해 검색된 SDK 문제
### <a name="issue"></a>문제
* 분석, 모니터링, 구분 또는 대시보드의 UI 데이터 수집 오류
* 푸시 오류(푸시가 앱 내부 또는 외부나 두 위치에서 모두 작동하지 않음)
* 고급 기능 오류(추적, 지리적 위치 또는 플랫폼별 푸시 미작동)
* API 오류(API에서 자동 오류가 자주 발생하며 오류 메시지가 표시되지 않음)
* 서비스 오류(Azure Mobile Engagement 기능이 응용 프로그램에서 작동하지 않음)

### <a name="causes"></a>원인
* 오류 (예: 한 UI 데이터 컬렉션 오류, 푸시 오류, 고급 기능 실패, API 오류, 응용 프로그램 충돌 또는 명백한 서비스 응용 프로그램에 의해 검색 됩니다 toobe hello Azure Mobile Engagement SDK로 해결 해야 하는 대부분의 문제 작동 중단)입니다.  
* Azure Mobile Engagement의 특정 기능은 하기 전에 응용 프로그램에서 작동 하지 않았습니다, toocomplete hello 통합을 해야 합니다. 
* Azure Mobile Engagement의 특정 기능은 작동 중지 있다면 hello Azure Mobile Engagement SDK로 tooupgrade toohello 마지막 버전을 할 수 있습니다. 다른 버전의 Azure Mobile Engagement (Android, iOS, Windows 및 Windows Phone)에서 지 원하는 각 플랫폼에 대 한 Azure Mobile Engagement SDK hello 임을 기억 합니다.

#### <a name="sdk-integration"></a>SDK 통합
* Azure Mobile Engagement가 SDK에 올바르게 통합되지 않았습니다(분석).
* 도달률이 SDK에 올바르게 통합되지 않았습니다(앱 내 푸시/앱 외부 푸시).
* 인증서가 만료되었거나 프로덕션/개발 버전이 잘못되었습니다(iOS에만 해당).
* GCM 또는 ADM이 SDK에 올바르게 통합되지 않았습니다(Android에만 해당 - 서비스별 푸시).
* 추적이 SDK에 올바르게 통합되지 않았습니다(설치 스토어 추적).
* 지연 위치 또는 GPS 위치가 SDK에 올바르게 통합되지 않았습니다(지리적 위치 기준 대상 지정).

**참고 항목:**

* [SDK 설명서 - 통합 가이드][Link 5] 
* [문제 해결 가이드 - 푸시][Link 23]

#### <a name="sdk-upgrade"></a>SDK 업그레이드
* 이전 버전의 SDK (대개 관련된 toonewer 버전의 hello 장치 OS) hello로 tooupgrade SDK tooresolve 문제 필요 합니다.
* 장치에서 앱의 모든 이전 버전을 제거 하 고 hello 최신 버전의 응용 프로그램을 다시 설치, hello hello Azure Mobile Engagement UI tooconfirm 장치 응용 프로그램의 최신 버전 hello를 사용 하 고 있는지에서 장치 ID를 다시 등록 합니다.

**참고 항목:**

* [SDK 설명서 - 릴리스 정보](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [SDK 설명서 - 업그레이드 가이드](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a>기타 SDK 관련 문제
* Azure Mobile Engagement 하면이 응용 프로그램 매니페스트 "AndroidManifest.xml"에 오류 toowork (Android에만 해당) 되지 않습니다.
* SDK 통합 및 API 사용 된 일반적인 문제는 tooconfuse hello SDK 키 및 hello API 키입니다.

**참고 항목:**

* [개념 - 용어집][Link 6]

## <a name="advanced-coding-issues"></a>고급 코딩 문제
### <a name="issue"></a>문제
* 플랫폼별 코드 직접 관련 되지 않은 tooAzure Mobile Engagement iOS, Android 및 Windows Phone 문제를 일으킬 수 있습니다.

### <a name="causes"></a>원인
* Azure Mobile Engagement와 관련 된 코딩 문제를 고급 대부분의 일반적인 원인은 잘못 작성 된 플랫폼에 따라 특정 코드 직접 관련 되지 않은 tooAzure Mobile Engagement 합니다. Tooconsult 설명서 특정 toohello 플랫폼을 개발 하는 대 한 또한 tooAzure Mobile Engagement 설명서 (Android, iOS, 웹, Windows 및 Windows Phone) 필요 합니다.
* 또한 "categories"를 잘못 구성 내부 또는 외부 hello 앱 (Android에만 해당)의 알림 tooanother 위치에서 연결 하는 것을 금지 합니다. 
* 설정 하지 않으면 "UIKit.framework" iOS 코드를 보여 주는 "기호를 찾을 수 없음 오류"에서 "optional" 너무 오래 된 iOS 장치 (iOS에만 해당)에서 충돌 및/또는 합니다.
* 만료 된 인증서 또는 hello 개발자 또는 Prod 버전의 hello 인증서를 사용 하 여 올바르게 하지, 원인 밀어넣기 (iOS에만 해당)을 발급 합니다.
* Azure Mobile Engagement 없습니다 (예: Android 및 iOS에서 푸시 hello system center의 작동 원리에 대 한 앱 외부)을 제어 하는 몇 가지 제한 사항 내재 된 tooa 플랫폼이 있습니다.
* Azure Mobile Engagement 참조에 대 한 iOS 및 Android 용 Azure Mobile Engagement에서 사용 되는 hello 내부 패키지의 전체 목록을 게시 합니다. Azure Mobile Engagement의 기능 중 일부는 특정 toohello 플랫폼 (Android, iOS, 웹, Windows 및 Windows Phone) 염두에 둬야 합니다.

### <a name="see-also"></a>참고 항목
* [문제 해결 가이드 - 푸시][Link 23] 
* [SDK 설명서 - 릴리스 정보][Link 5]
* [SDK 설명서 - 업그레이드 가이드][Link 5]

## <a name="application-crashes"></a>응용 프로그램 작동 중단
### <a name="issue"></a>문제
* Hello 최종 사용자의 장치에 응용 프로그램 작동이 중단 됩니다.

### <a name="causes"></a>원인
* Hello에서 크래시 정보를 볼 수 있습니다 *분석 UI* 또는 hello *분석 API*
* Hello 오래 걸리고 hello 테스트 장치의 장치 ID를 찾을 수 있습니다는 최종 사용자 toohelp 프로그램 응용 프로그램 toocrash 발생 시킨 작업을 동일한 프로그램 충돌의 hello 원인을 식별 합니다.
* Toohello hello SDK의 최신 버전을 업그레이드 하 여 응용 프로그램 toocrash 시키는 hello Azure Mobile Engagement SDK가 있는 알려진된 문제를 해결 한 경우에 따라 합니다. 충돌을 조사할 때 플랫폼에 대 한 있는지 toocheck hello 릴리스 정보를 확인 합니다.

### <a name="see-also"></a>참고 항목
* [SDK 설명서 - 릴리스 정보][Link 5]
* [SDK 설명서 - 업그레이드 가이드][Link 5]

## <a name="app-store-upload-failures"></a>앱 스토어 업로드 오류
### <a name="issue"></a>문제
* 오류 관련 toouploading hello 앱 tooApple, Google 또는 hello Windows 앱 스토어의 최신 버전입니다.

### <a name="causes"></a>원인
* 앱 저장 경우에 따라 앱이 차단을 사용 하는 특정 기능 (예: hello Apple 스토어 hello 스토어의 앱에서 IDFV hello 사용 되지 않으며 hello GooglePlay 저장소 hello 앱 간에 응용 프로그램 정보를 공유할 수 없습니다). 
* 앱 toohello 스토어에 업로드 하는 데 문제가 있는 경우 해당 플랫폼 및 hello SDK의 현재 버전에 대 한 hello 릴리스 정보를 확인 하 고 있는지 확인 합니다.

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

