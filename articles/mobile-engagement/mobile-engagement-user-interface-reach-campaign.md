---
title: "Mobile Engagement 사용자 인터페이스-aaaAzure 캠페인에 도달"
description: "Laern 어떻게 toocreate 및 푸시 알림 캠페인 Azure Mobile Engagement를 사용 하 여 관리"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a>어떻게 toocreate 및 푸시 알림 캠페인 관리
푸시 알림을 toosend 필요한 모든 hello 정보를 제공 하 여 복잡 한 수식을 사용 하 여 hello hello UI toocreate 새 푸시 캠페인의 도달 범위 섹션을 사용할 수 있습니다. hello 푸시 캠페인의 옵션에 따라 약간 다 4 hello 캠페인 종류: 공지, 여론 조사, 데이터 푸시 및 타일 (Windows Phone만 해당).

### <a name="option-applies-to"></a>옵션 적용 대상
* 언어: 모두(알림, 설문 조사, 데이터 푸시, 타일)
* 캠페인: 모두(알림, 설문 조사, 데이터 푸시, 타일)
* 알림: 알림, 설문 조사
* 콘텐츠: 각 캠페인 유형에서 고유함
* 대상: 모두(알림, 설문 조사, 데이터 푸시, 타일)
* 시간 프레임: 알림, 설문 조사, 타일
* 테스트: 모두(알림, 설문 조사, 데이터 푸시, 타일)

![도달률 캠페인1][20]

## <a name="languages"></a>언어
Hello 언어 드롭 다운 메뉴 toosend toouse 다른 언어로 설정 된 푸시 toodevices 프로그램의 다른 버전을 사용할 수 있습니다. 기본적으로 모든 장치 toouse 설정 된 언어에 관계 없이 동일한 푸시 hello를 표시 됩니다. 사용자가 자신의 장치 집합 tooa 다른 언어와 hello 기본 언어 버전의 hello 푸시를 받게 됩니다. Hello 푸시 캠페인 옵션의 대다수 사용 하면 toospecify 대체 콘텐츠 대 각 hello 추가 언어를 선택 합니다. 

![도달률 캠페인2][21]

### <a name="language-differences-apply-to"></a>다른 언어 적용 대상
* 언어: 고유한 언어 추가 toohello 기본 언어에서 선택할 수 있습니다.
* 캠페인: 모든 언어에 대해 동일합니다.
* 알림: 각 언어에 대 한 고유한 또한 toohello 기본 언어
* 내용: 각 언어에 대 한 고유한 또한 toohello 기본 언어
* 대상: 개별 언어 기준별로 필터링할 수 있습니다.
* 시간 프레임: 모든 언어에 대해 동일합니다.
* 테스트: 한 번에 tooeach 언어 전송 될 수 있습니다.

### <a name="supported-languages"></a>지원되는 언어
* 아랍어(ar) 
* 불가리아어(bg) 
* 카탈로니아어(ca) 
* 중국어(zh) 
* 크로아티아어(hr) 
* 체코어(cs) 
* 덴마크어(da) 
* 네덜란드어(nl) 
* 영어(en) 
* 핀란드어(fi) 
* 프랑스어(fr) 
* 독일어(de) 
* 그리스어(el) 
* 히브리어(he) 
* 힌디어(hi) 
* 헝가리어(hu) 
* 인도네시아어(id) 
* 이탈리아어(it) 
* 일본어(ja) 
* 한국어(ko) 
* 라트비아어(lv) 
* 리투아니아어(lt) 
* 말레이어(macrolanguage)(ms) 
* 노르웨이어 복말(nb) 
* 폴란드어(pl) 
* 포르투갈어(pt) 
* 루마니아어(ro) 
* 러시아어(ru) 
* 세르비아어(sr) 
* 슬로바키아어(sk) 
* 슬로베니아어(sl) 
* 스페인어(es) 
* 스웨덴어(sv) 
* 타갈로그어(tl) 
* 태국어(th) 
* 터키어(tr) 
* 우크라이나어(uk) 
* 베트남어(vi) 

## <a name="campaign"></a>캠페인
사용할 수 있습니다 hello 캠페인 섹션 tooset hello 이름 및 캠페인의 범주도 마치 푸시 캠페인의 tooignore hello 대상 섹션을 계획 하 고 hello Reach API를 통해이 캠페인 (및 hello 낮은 수준 푸시 API를 사용 하 여 일부 요소)를 대신 보냅니다. 범주는 미리 정의 된 설정에 따라 사용자 지정 알림 템플릿 toocontrol 앱 내 알림과 함께 사용할 수 있습니다. Hello Reach API를 통해 기존 "범주" 목록을 가져올 수 있습니다.

> [!WARNING]
> Toosend 해야는 hello "대상 그룹 무시, 푸시가 전송 되지 hello API 통해 toousers" 옵션 사용 Reach 캠페인의 hello "는 캠페인" 섹션에 hello 캠페인은 자동으로 보내지 않습니다 hello Reach API를 통해 수동으로 합니다.

![도달률 캠페인3][22]

### <a name="option-applies-to"></a>옵션 적용 대상
* 이름: 모두
* 범주: 알림, 설문 조사
* 대상 그룹 무시, 푸시가 toousers hello API 통해 전송 되지: 모든

## <a name="notification"></a>알림
포함 하 여 푸시에 대 한 hello 알림 섹션 tooset 기본 설정을 사용할 수 있습니다: hello hello 푸시 hello 메시지, 앱에서 이미지의 제목 또는 해제 가능한 경우. 다양 한 알림 설정을 장치의 플랫폼 특정 toohello 사용 됩니다. 푸시를 전송할 위치로 "앱 내" 또는 "앱 외부" 중 하나를 선택하거나 둘 다를 선택할 수 있습니다. (사용자가 "옵트인" 또는 "옵트아웃"을 "부족 app"에 푸시합니다 hello 운영 체제 수준 장치에서 입력 해야 하며 Azure Mobile Engagement는 금지 됩니다 수 toooverride이이 설정 되어야 합니다. 또한 hello Reach API 처리 "app" 및 "out 응용 프로그램의" 푸시 해야 합니다. hello 푸시 API 사용 가능 너무 푸시 "응용 프로그램의 초과" 사용된 toohandle.) 푸시 그림 또는 사용자 응용 프로그램 또는 tooanother 위치 (Android SDK 2.1.0 또는 필요한 이상 의도 범주) 응용 프로그램에서 외부 연결을 위한 딥 링크 등의 HTML 콘텐츠를 사용자 지정할 수 있습니다. Hello 아이콘 또는 iOS 배지를 변경할 수 있으며 텍스트 또는 웹 콘텐츠 (html 콘텐츠, URL 링크 tooanother 위치 내부 또는 외부 hello 앱의 팝업)를 보냅니다. Android 장치 링을 만들거나 hello 푸시를 진동 수도 있습니다. (있는지 있습니다 됩니다 필요 hello에서 Android SDK 사용 권한 파일 tooring 매니페스트 또는 장치를 진동 올바른 기억 합니다.) 모든 장치에서 화면 크기가 다르므로 현재 Android의 "큰 사진" 크기에 대한 업계 표준은 없지만 거의 모든 화면 크기에서는 400x100 크기의 사진을 사용하면 됩니다.

### <a name="delivery-types"></a>배달 유형
* 앱 외부만: hello 사용자 hello 응용 프로그램을 사용 하지 않는 경우 hello 알림이 배달 됩니다.
* 앱만 알림 부족 hello Apple 또는 Google (GCM 또는 APNS 인증서)에서 발급 한 인증서가 필요합니다.
* 앱에서만: hello 알림이 hello 응용 프로그램을 실행 하는 경우에 나타납니다.
* hello 알림 hello Capptain 전달 시스템 tooreach hello 사용자를 사용합니다. Hello 레이아웃/의 시각적 표시 빌드되고 푸시 완전히 사용자 지정할 수 있습니다.
* 언제 든 지:이 옵션 중 하나가 hello 응용 프로그램의 실행 알림을 보내는 보장 합니다.

![도달률 캠페인4][23]

### <a name="option-applies-to"></a>옵션 적용 대상
* 알림: 알림, 설문 조사

## <a name="content"></a>Content
공지, 여론 조사, 데이터 푸시 및 타일 (Windows Phone만 해당)의 hello 콘텐츠 섹션 toomodify hello 콘텐츠를 사용할 수 있습니다. 푸시 캠페인의 hello 콘텐츠 설정에는 캠페인의 특정 toohello 형식입니다. 

### <a name="see-also"></a>참고 항목
* [UI 설명서 - 도달률 - 푸시 콘텐츠][Link 29]

![도달률 캠페인5][24]

## <a name="audience"></a>대상
Hello Audience 섹션 toodefine 표준 목록이 항목 toolimit 캠페인 또는 사용자 지정 된 기준에 따라 캠페인 제한에 사용할 수 있습니다. hello 표준 집합이 옵션 tooLimit 청중이 있습니다 toopush tooeither 기존 또는 새 사용자 또는 네이티브 푸시 사용자만. 또한 사용자 받는 hello 푸시 할당량 toolimit hello 수를 설정할 수 있습니다. 캠페인 필터링 된 tooinclude 방법에 대 한 hello 식을 수동으로 편집할 수 있습니다 하나 이상의 조건 tootarget 사용자입니다. 대상 식은 수동으로 입력할 수 있습니다. 이러한 식은 조건 간의 hello 관계를 명시적으로 정의 해야 합니다. 기준을 설명하는 식별자는 대문자로 시작해야 하며 공백은 포함할 수 없습니다. 사용 하 여 hello hello 조건 사이 관계를 설명할 수 있습니다 'and', 'or', 'not' 연산자와 '(',')'입니다. 예: "Criterion1 or (Criterion1 and not Criterion2)".

> [!NOTE]
> 캠페인에 포함 하는 대규모 고객을 사용 하 여 hello 서버 쪽 검색을 대상으로 속도가 느려질 수 있음, 여러 캠페인에 동일한 hello toostart 사용 하려는 경우에 특히 시간입니다.

* 가능하면 캠페인을 한 번에 하나만 시작합니다.
* hello 최대 4 개의 캠페인 한 번에만 시작 합니다.
* 푸시 tooyour 활성 사용자만 ("네이티브 푸시를 사용 하 여 도달할 수 있는 사용자만 참여" checkbox "활성 사용자만 참여" 및) 여전히 hello 앱이 설치를 사용 하는 사용자만 toobe 검색 할 수 있도록 합니다.
  대상 그룹에서 정의 되 면 hello를 사용할 수 있습니다 하는 사용자 수를이 푸시 받습니다 아웃 단추 toofind 시뮬레이션 합니다. 이 옵션은 잠재적으로 대상 (이 사용자의 무작위 샘플을 기준으로 추정)이 대상이 그룹으로 알려진된 사용자의 hello 수를 계산 합니다. 알아 두어야 하 hello 응용 프로그램을 제거한 사용자도이 대상 그룹에 속하지만 연결할 수 없습니다.

### <a name="see-also"></a>참고 항목
* [UI 설명서 - 도달률 - 새 푸시 기준][Link 28]

![도달률 캠페인6][25]

### <a name="edit-expression"></a>식 편집
![도달률 캠페인7][26]

### <a name="limit-your-audience-option-applies-to"></a>대상 제한 옵션 적용 대상
* 사용자 하위 집합만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)
* 이전 사용자만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)
* 새 사용자만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)
* 유휴 사용자만 참여: 알림, 설문 조사, 타일
* 활성 사용자만 참여: 모두(알림, 설문 조사, 데이터 푸시, 타일)
* 네이티브 푸시를 사용하여 연결할 수 있는 사용자만 참여: 알림, 설문 조사

## <a name="time-frame"></a>시간 프레임
Hello 기간 섹션 tooset hello 푸시가 전송 되지 있고 즉시 hello 시간 프레임 빈 toostart hello 캠페인을 그대로 둘 수도 때 사용할 수 있습니다. hello 최종 사용자 표준 시간대를 사용 하 여 시작할 수 있습니다 hello 캠페인 푸시 캠페인에 대 한 hello world 일치 hello 시간 내에 모든 표준 시간대 설정 될 때까지 한 번에 작은 일괄 처리 보내고 아시아의 최종 사용자에 대 한 보다 일찍 하루 기억 합니다. Hello 최종 사용자 표준 시간대를 사용 하 여도 지연이 발생할 수 있습니다 캠페인에 hello 푸시를 시작 하기 전에 hello 전화에서 toorequest hello 시간에 있기 때문입니다.

> [!NOTE]
> 종료 날짜가 없는 캠페인은 푸시를 로컬로 캐시할 수 있으므로 캠페인을 수동으로 종료한 후에도 푸시가 표시될 수 있습니다. tooavoid이 동작을 특정 캠페인에 대 한 종료 시간입니다.

### <a name="see-also"></a>참고 항목
* [도달률 - 방법 - 예약][Link 3] 

![도달률 캠페인8][27]

### <a name="settings-apply-to"></a>설정 적용 대상
* 시간 프레임: 알림, 설문 조사, 타일

## <a name="test"></a>테스트
Hello 캠페인을 저장 하기 전에 hello 테스트 섹션 toosend이 푸시 tooyour 자체 테스트 장치를 사용할 수 있습니다. 이 캠페인에 대 한 모든 사용자 지정 언어를 구성한 경우에 각 언어의 hello 푸시를 테스트할 수 있습니다. 테스트 장치는 "내 계정"에서 설정할 수 있습니다.

> [!NOTE]
> 푸시 hello 단추를 사용 하는 경우 데이터는 기록 되지 서버 쪽 너무 "test", 실제 푸시 캠페인에 대 한 데이터는 기록만 합니다.

### <a name="see-also"></a>참고 항목
* [UI 설명서 - 내 계정][Link 14]

![도달률 캠페인9][28]

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

