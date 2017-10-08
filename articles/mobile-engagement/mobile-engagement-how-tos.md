---
title: "Mobile Engagement 사용자 인터페이스-도달 How To aaaAzure"
description: "Azure Mobile Engagement의 사용자 인터페이스 개요"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4b6dafd09d894214d4c386f5c6f157a77671606f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-using-and-managing-pushes-tooreach-out-tooyour-end-users"></a>사용 및 관리를 시작 하는 tooget tooyour 최종 사용자에 게 아웃 tooreach를 푸시하는 방법
일단 hello SDK에 통합 되어 앱을 시작할 수 있습니다 hello UI tooPush 알림 toohello 사용자 응용 프로그램의 hello hello Reach 섹션을 사용 하 여 합니다.  

## <a name="do-your-first-push-notification-campaign"></a>첫 번째 푸시 알림 캠페인 수행
* 범위 hello SDK 사용 하 여 앱에 통합 되어 있는지 확인 합니다. 
* 응용 프로그램을 선택합니다.

![First1][1]

* "범위" 섹션을 클릭 하 고 "새 알림" toohello 이동

![First2][2]

* 새 캠페인을 만들고 이름을 지정합니다.
  
![First3][3]

* 어떻게 hello 알림 배달, 앱에서만로 선택 합니다.

![First4][4]

* 원하는 toopush hello 메시지 만들기

![First5][5]

* (선택 사항) hello 알림 제목을 작성할 수 있습니다.
* 푸시 메시지 내용을 작성합니다.
* 이미지를 업로드할 수 있습니다. 주의 hello 파일의 hello 크기 32, 768 바이트를 초과할 수 없습니다.
* 또한 옵션을 추가 하는 hello 기능 tooselect 했지만이 자습서의 포커스가 hello에 대 한 살펴보겠습니다는 나중에.
* 만 알림으로 hello 콘텐츠 형식 선택

![First6][6]

* 푸시 캠페인을 만듭니다. 그러면 해당 캠페인이 캠페인 목록에 표시됩니다.

![First7][7]

## <a name="test-your-push-notification-campaign"></a>푸시 알림 캠페인 테스트
![Test1][8]

* 장치를 등록합니다.
* 클릭 toopush 원하는 hello hello 장치의 확인란을 선택 합니다.
* "Test" 단추 toosend hello 푸시 toohello 장치 hello 클릭 합니다.

![Test2][9]

* Hello 캠페인을 활성화 합니다.

![Test3][10]

* 캠페인을 만든 하기만 하면 tooactivate tooyour 사용자를 푸시 알림 toobe hello에 대 한 것입니다.

## <a name="send-personalized-pushes"></a>개인 설정 푸시 보내기
* 이 예제에는 푸시 hello 푸시 알림을에 사용자 지정 리베이트 코드를 입력 하는 위치를 만듭니다.

![Personalize1][11]

따라서 응용 프로그램 정보 태그에서 여 마커를 대체 하 여 개인 설정 작동 toomake hello 사용자가 hello 적절 한 응용 프로그램 정보 정의 먼저 있는지 해야 합니다. 이 예제에서는 hello 대상된 사용자는 응용 프로그램 정보 태그 rebate_code 정의 해야 합니다.
위에 나와 있는 것 처럼 hello 푸시 알림 콘텐츠에 hello 응용 프로그램 정보 태그의 실제 콘텐츠 hello로 대체 toobe 임을 나타내는 hello 표식 ${rebate_code}를 포함 합니다.

> [!WARNING]
> Hello 앱 정보 태그 hello 사용자에 대해 정의 되어 있지 않으면, hello 사용자 hello 푸시를 받지 못합니다.

* 결과

![Personalize2][12]

### <a name="you-can-further-personalize-hello-text-your-notification"></a>추가로 개인 설정할 수 있습니다 hello 텍스트 사용자 알림
![Personalize3][13]

* Hello 알림의 hello 제목을 포함 하 여
* Hello의 내용과 hello 메시지입니다.
* Hello 알림의 유형입니다 (텍스트 보기 또는 웹 보기)를 선택 합니다.

![Personalize4][14]

### <a name="hello-body-of-an-announcement-may-also-be-personalized-with"></a>공지의 hello 본문와도 개인 설정할 수 있습니다.
* hello 작업 URL 해야 원하는 방문 페이지 toocustomize hello
* hello 제목
* hello 메시지의 hello 본문입니다.

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a>푸시 알림 차별화(앱 내부 또는 외부에서)
* Push, 응용 프로그램을 선택, toohello "범위" 섹션을 이동, 선택 또는 푸시 캠페인 만들고 toohello "알림" 섹션을 이동 알림의 hello 종류를 선택 합니다.
* 클릭 하 여 원하는 hello "배달 모드" 합니다.
* 특정 활동 (화면)에서 "제한 활동" 확인란 hello 알림을 표시할 때 발생 하는 hello를 클릭 합니다.

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a>"앱 외부에서만" 배달 모드
![Differentiate2][16]

"App" 부족 hello 응용 프로그램이 닫힐 때 배달 모드에 푸시 알림을 제공 합니다. 이 hello 표준 푸시 알림입니다.
"App" 부족을 선택 하면 이미을 제공 해야에서는 (APNS 또는 GCM)에서 응용 프로그램을 구축 하는 hello 플랫폼에서 hello 인증서입니다.

### <a name="see-also"></a>참고 항목
* [Apple 푸시 알림 서비스 - 인증서](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging - 인증서](http://developer.android.com/google/gcm/index.html) 

### <a name="in-app-only-delivery-mode"></a>"앱 내에서만" 배달 모드
![Differentiate3][17]

"앱만" 배달 모드 hello 응용 프로그램을 실행 하는 경우 푸시 알림을 제공 합니다.
이 알림에 대 한 불필요 toogo 통해 hello APNS 및 GCM 시스템입니다.
최종 사용자에 게 응용 프로그램에 전달 시스템 tooreach hello를 사용할 수 있습니다.
완벽 하 게 hello 알림을 사용자 지정할 수 있으며 결정 있는 활동 (화면) hello 알림이 표시 됩니다.

### <a name="anytime-delivery-mode"></a>"항상" 배달 모드
"언제 든 지" 배달 모드를 선택할 수, 최종 사용자 여부 hello tooreach 사용 하면 응용 프로그램의 실행 합니다.
"언제 든 지"를 선택 하면 이미을 제공 해야 응용 프로그램 (APNS 이나 GCM)에 따라 구성 하는 hello 플랫폼에서 hello 인증서입니다. 

## <a name="schedule-a-push-campaign"></a>푸시 캠페인 예약
### <a name="plan-toostart-a-campaign"></a>캠페인 tooStart 계획
![Shedule1][18]

Hello 3 월의 21st 되며 알림 toomake 있고 자정에 3 월의 22nd을 hello에 대 한 planed 있습니다. Hello 인터페이스 toodo 푸시를 앞에 toostay가 필요가 없습니다! 사전에 hello 정확한 분 알림을 보내지 것입니다 계획할 수 있습니다.

* 선택을 취소 hello "None" 확인란을 선택 하 고 시작 시간을 선택 합니다. 
* 원하는 toostart hello 푸시 캠페인 hello 시간과 hello 날짜를 선택 합니다.

### <a name="plan-tooend-a-campaign"></a>캠페인 tooend 계획
![Shedule2][19]

원하는 프로그램 캠페인 toostop hello에서 3 월의 1 오후 3시에 몰라도 toodo 있을 수 없습니다 것입니다.
Hello 인터페이스 toopush 앞에 toostay가 필요가 없습니다! 사전에 hello 정확한 분 캠페인은 중지를 계획할 수 있습니다.

* "None" hello에서 클릭 확인란을 선택 하거나 종료 시간을 선택 합니다.
* 원하는 toofinish hello 푸시 캠페인 hello 시간과 hello 날짜를 선택 합니다.

### <a name="end-a-campaign-manually"></a>캠페인 수동 종료
![Shedule3][20]

기본적으로 hello "None"-확인란이 선택 되어 있습니다.
Hello 캠페인 hello에서 활성화 되는 즉시 시작 됩니다이 즉 섹션에 도달 하 고 hello에서 중지 됩니다 하면 끝 섹션에 도달 합니다.

> [!NOTE]
> 종료 날짜 없이 만든 캠페인 hello 장치에서 hello 푸시를 로컬로 저장 하 고 hello 앱 hello 캠페인 수동으로 종료 될 경우에 열릴 때 hello 표시 합니다.

## <a name="enhance-a-push-notification-with-a-text-view"></a>텍스트 뷰로 푸시 알림 개선
### <a name="what-is-a-text-view"></a>텍스트 뷰란 무엇인가요?
![TextView1][21]

텍스트 뷰는 텍스트 내용이 있는 팝업입니다. 이 팝업 hello 푸시 알림을 hello 최종 사용자가 클릭 한 후에 나타납니다.
텍스트 보기 있습니다 toopresent tooyour 최종 사용자 콘텐츠입니다. 이 hello 기회 toopresent tooa 페이지 리디렉션 tooa 저장소를 웹 페이지를 열고 등 지리적으로 지역화 된 검색 시작 전자 메일을 보내는 응용 프로그램의 점프 같은 호출 tooaction도 중...

### <a name="example-text-view"></a>예: 텍스트 뷰
* Hello에 "도달" 섹션에서 푸시 알림 캠페인을 만들고 캠페인에 이름을 지정합니다

![TextView2][22]

* Hello 알림을에 표시 되는 hello 메시지를 씁니다.
* Hello "텍스트"의 콘텐츠 형식을 알림 선택

![TextView3][23]

> [!NOTE]
> 텍스트 뷰를 푸시할 경우 항상 알림이 먼저 제공됩니다. 

* (선택한 다음 hello 텍스트 알림 콘텐츠 hello 하위 섹션, 나타날 toodefine hello 텍스트 toobe 표시를 사용할 수 있도록 합니다.) hello 텍스트를 정의 합니다.

![TextView4][24]

* Hello 위쪽 hello 메시지에 나타나는 hello 제목을 작성 합니다.
* Hello 텍스트 보기의 hello 주 콘텐츠를 작성 합니다.
* (작업 단추는 hello 응용 프로그램 toomake tooan 앱 스토어 또는 모든 종류의 소스를 제공할 수 있습니다 리디렉션 hello 응용 프로그램의 페이지를 여는 등 특정 작업을 사용 하는 데 사용) hello 실행 단추에 표시 되는 hello 콘텐츠를 작성 합니다.
* Hello 끝내기 단추에 표시 되는 쓰기 hello 콘텐츠 (hello 끝내기 단추를 클릭 하 여 hello 텍스트 보기는 사라집니다.)
* 푸시 알림 캠페인 만들기 및 hello 캠페인 목록에 표시 됩니다.

![TextView5][25]

* 푸시 알림 캠페인 toosend hello 텍스트 보기 tooyour 사용자를 활성화 합니다.

![TextView6][26]

* 결과

![TextView7][27]

* hello 사용자를 클릭 하 고 hello 알림을 받게 됩니다.
* hello 텍스트 보기 된 팝업 허용 hello 사용자 toointeract으로 나타납니다.

## <a name="enhance-a-push-notification-with-a-web-view"></a>웹 뷰로 푸시 알림 개선
### <a name="what-is-a-web-view"></a>웹 뷰란 무엇인가요?
![WebView1][28]

웹 뷰는 웹 콘텐츠가 있는 팝업입니다. 이 팝업이 나타나며이 hello 푸시 알림을 hello 최종 사용자가 클릭 합니다.
웹 보기 있습니다 toohave hello 최종 사용자와 더 많은 상호 작용 합니다.
이 hello 기회 toopresent 리디렉션 tooApp 저장소와 같은 웹 페이지를 열고 시작 등 검색 지리적으로 지역화 된 전자 메일 보내기 호출 tooaction도 중...

### <a name="example-web-view"></a>예: 웹 뷰
* Hello에 "도달" 섹션의 푸시 캠페인을 만들고 캠페인에 이름을 지정 합니다.

![WebView2][29]

* Hello 알림을에 표시 되는 hello 메시지를 씁니다.
* "Web"으로 hello 알림 콘텐츠 형식 선택

![WebView3][30]

### <a name="about-announcement-types"></a>알림 유형 정보:
* 알림 전용: 단순한 표준 알림입니다. 사용자가 클릭, 추가 보기 없음 나타나지만 hello 작업만 연결 된 경우 tooit 발생 하는지 의미 합니다.
* 텍스트 알림: hello 사용자 toohave 텍스트 보기를 살펴보면 맞물릴 때 알리는 것입니다.
* 웹 공지: hello 사용자 toohave 웹 보기를 살펴보면 맞물릴 때 알리는 것입니다.
  Hello "웹 공지" 콘텐츠를 선택 합니다.

> [!NOTE]
> 웹 뷰를 푸시할 경우 항상 알림이 먼저 제공됩니다.

* (선택한 다음 hello 웹 알림 콘텐츠 hello 하위 섹션, 나타날 toodefine hello 웹 보기 콘텐츠 toobe 표시를 사용할 수 있도록 합니다.) hello 웹 콘텐츠를 정의 합니다.

![WebView4][31]

* (선택 사항) hello 메시지 hello 위쪽에 표시 되는 hello 제목을 작성 합니다.
* 여기에 HTML 코드를 작성합니다.
* 편집 모드 단추 tooswitch edition hello 소스 클릭 하 고 같은 어떻게 나타나는지 확인 합니다.
* (작업 단추는 hello 응용 프로그램 toomake tooa 저장소 또는 모든 종류의 소스를 제공할 수 있습니다 리디렉션 hello 응용 프로그램의 페이지를 여는 등 특정 작업을 사용 하는 데 사용) hello 실행 단추에 표시 되는 hello 콘텐츠를 작성 합니다.
* Hello 끝내기 단추에 표시 되는 쓰기 hello 콘텐츠 (hello 끝내기 단추를 클릭 하 여 hello 웹 보기 사라집니다).
* 결과

![WebView5][32]

* hello 사용자 hello 알림의 받을 항목을 클릭 합니다.
* hello 텍스트 보기 된 팝업 허용 hello 사용자 toointeract으로 나타납니다.

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

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

