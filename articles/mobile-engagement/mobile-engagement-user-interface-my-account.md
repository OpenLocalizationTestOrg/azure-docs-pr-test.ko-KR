---
title: "aaaAzure Mobile Engagement 사용자 인터페이스-내 계정"
description: "자세한 내용은 방법 toomanage Azure Mobile Engagement를 사용 하 여 사용자 계정 프로필과 테스트 장치"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 22832678-3959-4b8c-9fb2-f2ff5974e5d1
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1d85f0e87c43605f59f6536ae42a7fb6a99ee36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-your-account-profile-and-test-devices"></a>어떻게 toomanage 계정 프로필 및 테스트 장치
이 문서에서는 hello 설명 **홈** hello 페이지 **Mobile Engagement** 포털입니다. Hello를 사용 하 여 **Mobile Engagement** 포털 toomonitor 모바일 앱을 관리 하 고 있습니다. 

tooget toohello **내 계정** 페이지 hello hello 페이지 위쪽에서 사용자의 계정을 클릭 합니다.

UI가 보고 하 고 프로필 설정을 포함 하 여 사용자 계정과 연결 된 hello 설정을 변경 하 고 수 있는 장치 Id를 테스트 하는 hello 내 계정 섹션 번호입니다. 이러한 설정은 hello Device API를 통해 액세스할 수 있는 항목을 포함 합니다.

![MyAccount1][7]  

## <a name="profile"></a>프로필
계정 설정을 확인하거나 변경할 수 있습니다. 제공할 수도 다른 사용자 권한 toouse hello에서 전자 메일 주소에 따라 응용 프로그램 [홈](mobile-engagement-user-interface-home.md)합니다.

![MyAccount2][8]  

## <a name="devices"></a>장치
보기, 추가 또는 제거 tootest를 사용할 수 있는 hello 테스트 장치의 장치 ID를 테스트 프로그램 **도달** 또는 **푸시** 캠페인입니다. Toofind 각 플랫폼에 대 한 장치의 장치 ID를 hello 하는 방법에 대 한 상황에 맞는 지침 (iOS, Android, Windows Phone 등) "새 장치"를 클릭 하면 표시 됩니다. 

![MyAccount3][9]  

toouse 푸시 API 또는 Device API tooknow 사용자의 고유한 장치 식별자 (deviceid 매개 변수 hello)를 해야 합니다. 여러 가지 방법으로 tooretrieve 하기:

1. 프로그램 백 엔드에서 hello 장치 API tooget hello 식별자의 전체 목록 장치의 hello "Get" 기능을 사용할 수 있습니다.
2. 응용 프로그램에서 SDK tooget hello를 사용할 수 있습니다 것입니다. (Android에서는 및의 에이전트 클래스 hello hello getDeviceID() 함수 호출 ios에서의 에이전트 클래스 hello hello deviceid 속성을 읽을.)
3. 도달률 공지의에서 hello 알림이와 관련 된 hello 작업 URL hello {deviceid} 패턴을 포함 하는 경우 자동으로 바뀝니다 트리거 hello 동작 hello 장치의 hello 식별자로.
   http://<example>.com/registeruser?deviceid={deviceid}&otherparam=myparamdata는 http://<example>.com/registeruser?deviceid=XXXXXXXXXXXXXXXX&otherparam=myparamdata로 바꿉니다. 
4. Reach 웹 공지에서 hello hello 알림이의 HTML 코드 {deviceid} hello 패턴을 포함 하는 경우 자동으로 바뀝니다 hello 웹 공지를 표시 하는 hello 장치의 hello 식별자로.
   예를 들어 {deviceid} 장치 식별자는 다음과 같이 바뀝니다. XXXXXXXXXXXXXXXX
5. 장치에서 응용 프로그램을 열고 태그가 지정된 앱에서 이벤트를 수행합니다.
   "--모니터-응용 프로그램 이벤트-UI, 세부 정보에서" hello를 hello 목록에서 사용자가 수행 하는 이벤트를 찾습니다.
   Hello 모니터에서에서 toothis 이벤트를 클릭 합니다.
   이 이벤트를 수행 했는지 hello 장치 hello 목록에서 장치 ID를 찾아야 합니다.
   그런 다음이 장치 ID를 복사한 "새 장치--내 계정-UI 장치 장치 플랫폼을 선택 하는 데 사용"을 hello 등록 수 있습니다.
   >(를 변경할 수 IDFA iOS에 대 한 비활성화 되 면 hello 장치 ID 수 hello 시간에 따라 제거 하 고 응용 프로그램을 다시 설치 하는 경우.)

## <a name="troubleshooting-guide"></a>문제 해결 가이드
* [문제 해결 가이드 - 서비스][Link 24]

## <a name="see-also"></a>참고 항목
* [UI 설명서 - 홈][Link 13]

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




