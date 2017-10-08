---
title: "aaaAzure Mobile Engagement 사용자 인터페이스-설정"
description: "어떻게 toomanage hello Azure Mobile Engagement를 사용 하 여 응용 프로그램의 전역 설정에 알아봅니다"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 858f4cb4-14de-4bb5-826f-28cadbfc928b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02d4a36c591fc5e097410b7e931d1c9ce81d68d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-global-settings-of-your-application"></a>어떻게 toomanage hello 응용 프로그램의 전역 설정
hello **설정을** hello 응용 프로그램에 대 한 권한이 부여 되었습니다. hello 권한과 hello 응용 프로그램의 hello 플랫폼에 따라 프로그램 응용 프로그램 마다 다른에 사용할 수 있는 메뉴 옵션입니다. Hello 다음을 포함 하는 설정: 세부 정보, 프로젝트, 네이티브 푸시를 사용, 푸시 속도, 태그 (응용 프로그램 정보), 및가 상업적 압박이 합니다. (SDK hello를 사용 하 여) 응용 프로그램에서 프로그램 이나 백 엔드 (장치 API hello를 사용 하 여) hello hello 설정 섹션의 태그 (응용 프로그램 정보) 메뉴 옵션을 관리할 수 있습니다. 

> [!NOTE]
> 섹션의 hello **Mobile Engagement** 포털 UI hello 포함 **도움말 표시** 단추입니다. 이 단추 tooget 섹션에 대 한 자세한 컨텍스트 정보를 누릅니다.
> 
> 

## <a name="details"></a>세부 정보
응용 프로그램, 응용 프로그램 및 사용자 역할 권한에의 보기 hello 소유자의 toochange hello 이름 및 설명이 있습니다. 

분석 구성을 사용 하면 tooview 또는 변경 hello 일에 시작 주 및 hello 일의 보존 시간입니다.

  ![settings1][46]

## <a name="projects"></a>프로젝트
Tooselect 사용 하면 모든 프로젝트에 포함 하려는 응용 프로그램 tooappear 합니다. 

프로젝트 및 보기 hello 이름, 설명, 소유자에 대 한 검색할 수 있습니다 및 모든 프로젝트의 역할 권한을 응용 프로그램의 일부인 합니다.

자세한 내용은 [UI 설명서 - 홈][Link 13]을 참조하세요.

  ![settings3][48]

## <a name="native-push"></a>네이티브 푸시
새 인증서 또는 delete와에 대 한 기존 인증서를 사용 하 여 네이티브 푸시를 통한 tooregister가 있습니다. 네이티브 푸시에 언제 든 지 실행 중이지 않을 때에 Azure Mobile Engagement toopush tooyour 응용을 수 있습니다. 

하나 이상의 네이티브 푸시 서비스에 대 한 인증서 또는 자격 증명을 입력 한 후 "항상"를 선택할 수 있습니다 hello 푸시 API에서에서 Reach 캠페인을 사용 하 여 hello "알림" 매개 변수를 만들 때.

### <a name="apple-push-notification-service-apns"></a>APNS(Apple 푸시 알림 서비스)
tooenable를 사용 하 여 네이티브 푸시를 사용 하 여 hello Apple Push Notification Service 인증서 tooregister 해야 합니다. Toospecify hello 인증서 종류를 (DEV) 개발 또는 프로덕션 (PROD)로 필요 합니다. 그런 다음 인증서와 hello 암호를 업로드할 필요 합니다.

자세한 내용은 참조: [SDK 설명서-iOS-어떻게 tooPrepare Apple 푸시 알림에 대 한 응용 프로그램][Link 5]

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a>WPNS(Windows 푸시 알림 서비스)
Windows 알림 서비스를 사용 하 여 네이티브 푸시 tooenable, 응용 프로그램의 자격 증명을 제공 해야 합니다. 이렇게 하려면 패키지 SID(보안 식별자)와 비밀 키가 필요합니다.

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a>Google Cloud Messaging for Android(GCM)
Google에서 toofollow hello 지침이 필요한 네이티브 푸시 GCM을 사용 하 여에 tooenable 합니다. 그런 후에 IP 제한 없이 구성된 서버의 단순 API 키를 붙여 넣어야 합니다. Android v1.12.0 + 용 hello SDK로 통합이 필요 합니다.

자세한 내용은 다음을 참조하세요. 

* [GCM tooIntegrate SDK 설명서 Android 방법][Link 5]
* [Google 개발자 GCM 가이드](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a>Amazon Device Messaging for Android(ADM)
ADM 사용 tooenable 네이티브 푸시, Amazon 제공 해야 <OAuth credentials> 로 구성 된 클라이언트 ID와 클라이언트 암호 (Android v2.1.0 + 용 SDK와의 통합 필요).

자세한 내용은 다음을 참조하세요. 

* [ADM tooIntegrate SDK 설명서 Android 방법][Link 5]
* [Amazon 개발자 ADM 설명서](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a>푸시 속도
응용 프로그램의 hello 현재 푸시 속도 표시 하 고 응용 프로그램의 toodefine hello 푸시 속도 있습니다.

  ![settings7][52]

## <a name="tag-app-info"></a>태그(앱 정보)
![settings11][56]

## <a name="commercial-pressure"></a>상업적 압력
![settings12][57]

## <a name="see-also"></a>참고 항목
* [개념][Link 6]
* [문제 해결 가이드 서비스][Link 24]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

