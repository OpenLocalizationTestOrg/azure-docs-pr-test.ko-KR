---
title: "Mobile Engagement 사용자 인터페이스-aaaAzure 모니터"
description: "자세한 내용은 방법 toomonitor Azure Mobile Engagement 응용 프로그램에 대 한 실시간 데이터"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: b91ad89a-b89d-4377-abb0-cc2d16a2836d
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3a581e4166bc88e6ee7aa784d4047c94533685b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-real-time-data-about-your-application"></a>어떻게 toomonitor 응용 프로그램에 대 한 실시간 데이터
이 문서에서는 hello 설명 **모니터** hello 탭 **Mobile Engagement** 포털입니다. Hello를 사용 하 여 **Mobile Engagement** 포털 toomonitor 모바일 앱을 관리 하 고 있습니다. 먼저 toocreate hello 포털을 사용 하 여 해당 toostart 참고는 **Azure Mobile Engagement** 계정. 

hello hello UI의 모니터 섹션 실시간 분석 정보를 제공 하 고 있습니다 tooset 경고 임계값에 도달 하면 대부분의 hello에 대 한 동일한 hello에서 지금까지 사용할 수 있는 정보 [분석](mobile-engagement-user-interface-analytics.md) 의 섹션 UI 번호입니다. Hello 참조 **용어집** hello 섹션인 [개념](http://go.microsoft.com/fwlink/?LinkId=525555) 용어 및 약어를 분석 및 모니터링에 대 한 정의 항목 (hello 다음과 같은: 활성 사용자, 새 사용자를 유지 하는 사용자, 세션, 사용자 경로 그래프, 사용자가 지도, 추적 Url, 추세, 활동, 이벤트, 작업, 오류, 추가 정보, 충돌, 및 app-info).

> [!NOTE]
> 섹션의 hello **Mobile Engagement** 포털 UI hello 포함 **도움말 표시** 단추입니다. 이 단추 tooget 섹션에 대 한 자세한 컨텍스트 정보를 누릅니다.
> 
> 

## <a name="monitor---sessions-jobs-events-errors-and-crashes"></a>모니터 - 세션, 작업, 이벤트, 오류 및 작동 중단
현재 세션 및 특정 화면을 사용 중인 사용자나 특정 작업을 수행 중인 사용자의 수를 확인할 수 있습니다. 세션, 작업, 이벤트, 오류 및 작동 중단을 기준으로 구분된 사용자 활동을 확인할 수 있습니다. Hello 현재 정보를 참조할 수 있으며 지난 시간, 일 또는 주 hello에서 hello 정보를 표시 합니다. Hello 정보 각 범주에 모두 표시 하거나 세션, 작업, 이벤트, 오류 및 크래시 특정 hello를 정렬할 수 있습니다.  라이브 모니터링 유용한 toouse 푸시 캠페인 toosee 등의 이벤트 동안가 있는 경우는 한 상승 동작에서 오른쪽 푸시 알림을 보낸 후 합니다.

![Monitor1][14]  

## <a name="troubleshooting-with-monitor---events---details"></a>모니터를 통해 문제 해결 - 이벤트 - 세부 정보
Hello 장치 모니터링, 분석의 Azure Mobile Engagement의 통합을 지 테스트 장치와 tooconfirm에 대 한 ID는 가장 쉬운 방법으로 toofind의 테스트 장치에서 응용 프로그램에서 이벤트를 생성 및 모니터-이벤트-세부 정보에서 찾아은 및 세그먼트 응용 프로그램에서 작동 합니다. Hello 테스트 장치의 장치 ID를 만든 후 tooyour 테스트 장치를 "내 계정-장치"에 추가할 수 있습니다. 이벤트를 생성할 수 없는 경우 Azure Mobile Engagement SDK hello 사용 하 여 Android/iOS/웹/Windows/Windows Phone 앱에 올바르게 통합 되어 있는지 확인 합니다.

자세한 내용은 [SDK 설명서][Link 5]를 참조하세요.

![Monitor2][15]  

## <a name="troubleshooting-with-monitor---crashes---details"></a>모니터를 통해 문제 해결 - 작동 중단 - 세부 정보
Toohelp 앱이 충돌 하는 이유를 확인 하는 모니터-충돌-세부 정보에서 응용 프로그램에 대 한 충돌 정보를 검토할 수 있습니다. 또한 각 버전의 각 버전의 hello Android/iOS/웹/Windows/Windows Phone 용 SDK에 대 한 hello 릴리스 정보에 hello SDK의 알려진된 문제를 찾아야 합니다.

자세한 내용은 [SDK 설명서 - 릴리스 정보][Link 5]를 참조하세요.

![Monitor3][16]

## <a name="monitor---alerts"></a>모니터 - 경고
또한 tooyou 전자 메일 또는 인스턴트 메시지를 통해 자동으로 전송 될 경고에 대 한 조건을 지정할 수 있습니다. Google의 GTalk, Apple의 iChat 등 XMPP 호환 서비스가 지원됩니다. 경고는 초/분/시간당 특정 세션, 작업, 이벤트, 오류 또는 작동 중단 수보다 크거나(>) 작은(<) 미리 정의된 검색 임계값을 기준으로 합니다. 경고는 지정된 유형의 모든 활동을 모니터링할 수도 있고 특정 작업, 이벤트 또는 오류 활동만 모니터링할 수도 있습니다. 

Hello 시간 (분)를 지정 된 간격 마다 1 알림 계시다 hello toomake 받게 있는지, 결제 경고가 트리거될 때는 동일한 경고에 대 한 두 알림을 구분할 최소 크기는 최소 검색 속도 지정할 수 있습니다.

![Monitor4][17]

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
