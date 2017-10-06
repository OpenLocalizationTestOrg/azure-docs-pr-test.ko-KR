---
title: "Mobile Engagement 사용자 인터페이스-aaaAzure 조건에 도달"
description: "Toouse 대상 조건 toosend 푸시 캠페인 tooa Azure Mobile Engagement를 사용 하 여 사용자의 하위 집합을 선택 하는 방법에 대해 알아봅니다"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a>Toouse 대상 조건 toosend 푸시 캠페인 tooa 사용자의 하위 집합을 선택 하는 방법
Hello "새 기준" 단추와 특정 기준으로 대상 그룹을 대상으로 hello 가장 강력한 개념에 대해 Azure Mobile Engagement는 사용 하면 보내는 관련 대 한 푸시 알림 hello 고객 tooinstead 스팸 모든 사용자의 응답 하는 중 하나입니다. 표준 기준에 따라 대상 그룹을 제한 하 고 푸시 toodetermine 시뮬레이션 얼마나 많은 사람들이 hello 알림을 받게 됩니다.

**참고 항목:**

* [UI 설명서 - 도달률 - 새 푸시 캠페인][Link 27]

## <a name="audience-criteria-can-include"></a>대상 기준에는 다음 항목이 포함될 수 있습니다.
* * * Technicals: * *에 따라 hello 대상 같은 기술 정보 hello 분석 및 모니터링 섹션에서 볼 수 있습니다. **참고 항목** [UI 설명서 - 분석][Link 15],  [UI 설명서 - 모니터][Link 16]
* **위치:** "실시간 위치 보고"을 사용 하 여 지 오 펜싱을 사용 하는 응용 프로그램 기준 tootarget hello GPS 위치에서에서 대상 그룹으로 지리적 위치를 사용할 수 있습니다. "지연 영역 위치 보고" 호출 또한 사용된 tootarget hello 휴대 전화 위치에서 대상 그룹을 수 ("실시간 위치 보고" 및 "지연 된 영역 위치 보고" 해야 활성화 hello SDK에서에서). **참고 항목:** [SDK 설명서 - iOS - 통합][Link 5], [SDK 설명서 - Android - 통합][Link 5]
* **도달률 피드백:** 알림, 설문 조사 및 데이터 푸시의 도달률 피드백을 통해 이전 도달률 알림의 피드백에 따라 대상을 지정할 수 있습니다. 이렇게 하면 toobetter 대상 두세 도달 보다 캠페인 청중 처음으로 hello 수 있습니다. 사용할 수도 있습니다 toofilter 캠페인 tooNOT를 설정 하 여 유사 콘텐츠 관련 된 알림을 이미 받은 사용자가 특정 이전 캠페인을 이미 받은 toousers를 보낼 수 있습니다. 여전히 활성 상태인 특정 캠페인에 포함된 사용자가 새 푸시를 받지 않도록 제외할 수도 있습니다. **참고 항목:** [UI 설명서 - 도달률 - 푸시 콘텐츠][Link 29]
* **설치 추적:** 사용자가 앱을 설치한 위치를 기준으로 정보를 추적할 수 있습니다. **참고 항목:** [UI 설명서 - 설정][Link 20]
* **사용자 프로필:** 표준 사용자 정보에 따라 대상 수 하 고 사용자가 만든 hello 사용자 지정 앱 정보를 기준으로 대상 수 있습니다. 사용자가 현재 로그인에 고 tooset 방금 어떻게가 응답 tooprevious 캠페인 대신 자체 hello 응용 프로그램에서 요청 했습니다 특정 질문에 답변 한 사용자가 포함 됩니다. 앱에 대해 정의한 모든 앱 정보가 이 목록에 표시됩니다.
* 세그먼트: 여러 기준을 포함하는 특정 사용자 동작을 기준으로 작성한 세그먼트에 따라 대상을 지정할 수도 있습니다. 앱에 대해 정의한 모든 세그먼트가 이 목록에 표시됩니다. **참고 항목:** [UI 설명서 - 세그먼트][Link 18]
* **응용 프로그램 정보:** "설정" tootrack 사용자 동작에서 사용자 지정 응용 프로그램 정보 태그를 만들 수 있습니다. **참고 항목:** [UI 설명서 - 설정][Link 20]

## <a name="example"></a>예제:
Toopush 원하는 알림만 toohello 하위 집합에서-app를 수행한 사용자의 동작을 구입 합니다.

1. 응용 프로그램 설정 페이지 tooyour hello "앱 정보" 메뉴를 선택한 "새 응용 프로그램 정보"를 선택 합니다.
2. "inAppPurchase"라는 새 부울 앱을 등록합니다.
3. Hello 사용자 앱에서 바로 구매를 성공적으로 수행 하는 경우이 응용 프로그램 정보를 설정 하는 응용 프로그램을 "true" 너무 확인 (hello sendAppInfo ("inAppPurchase",...)를 사용 하 여 함수)
4. 않으려면 toodo이 응용 프로그램에서 hello 장치 API를 사용 하 여 백 엔드에서 수행할 수 있습니다)
5. 그런 다음 프로그램 알림 "inAppPurchase" 필요 청중 toousers 프로그램 제한 조건으로 설정 "true" 너무 toocreate만 필요)

> [!NOTE]
> 응용 프로그램 정보 태그 이외의 기준에 따라 대상 컴퓨터가 있어야 사용자의 장치에서 Azure Mobile Engagement toogather 정보 hello 푸시 전송 되 고 지연 않을 수 있습니다. 배지 업데이트 등의 복합 푸시 구성 옵션을 사용하는 경우에도 푸시가 지연될 수 있습니다. Hello 푸시 API에서에서 "단일 쇼트" 캠페인을 사용 하는 hello 절대 가장 빠른 푸시 방법 Azure Mobile Engagement 에서입니다. Reach 캠페인 (에서 나 hello Reach API hello UI)에 대 한 푸시 기준으로 앱 정보 태그만 사용 하는 것이 응용 프로그램 정보 태그 hello 서버 쪽에서 저장 되므로 hello 다음 가장 빠른 방법입니다. 푸시 캠페인에 대 한 다른 대상 기준을 사용 하는 hello 가장 유연한 이자 가장 느린 푸시 방법은 Azure Mobile Engagement 순서 toosend hello 캠페인의 tooquery hello 장치에 있기 때문입니다.

![도달률 기준1][29] 

## <a name="criterion-options-apply-to"></a>기준 옵션 적용 대상:
* **기술 정보**     
* 펌웨어 이름: 펌웨어 이름
* 펌웨어 버전: 펌웨어 버전
* 장치 모델: 장치 모델
* 장치 제조업체: 장치 제조업체
* 응용 프로그램 버전: 응용 프로그램 버전
* 통신 회사 이름: 통신 회사 이름, 정의되지 않음
* 통신 회사 국가: 통신 회사 국가, 정의되지 않음
* 네트워크 유형: 네트워크 유형
* 로캘: 로캘
* 화면 크기: 화면 크기
* **위치**      
* 마지막으로 확인된 지역: 국가, 지역, 구/군/시
* 실시간 지리적 펜스: 지점(이름/작업), 원형 지점(이름, 위도, 경도, 미터 단위 반경)
* **도달률 피드백**     
* 알림 피드백: 알림, 피드백
* 설문 조사 피드백: 설문 조사, 피드백
* 설문 조사 응답 피드백: 설문 조사 응답 피드백, 질문, 선택 항목
* 데이터 푸시 피드백: 데이터 푸시, 피드백
* **설치 추적**     
* 스토어: 스토어, 정의되지 않음
* 원본: 원본, 정의되지 않음
* **사용자 프로필**     
* 성별: 남성 또는 여성, 정의되지 않음
* 생년월일: 연산자, 날짜, 정의되지 않음
* 옵트인(opt in): true 또는 false, 정의되지 않음
* **앱 정보**      
* 문자열: 문자열, 정의되지 않음
* 날짜: 연산자, 날짜, 정의되지 않음
* 정수: 연산자, 숫자, 정의되지 않음
* 부울: true 또는 false, 정의되지 않음
* **세그먼트**    
* 드롭다운 목록의 세그먼트 이름, 제외 항목(이 세그먼트에 포함되지 않은 대상 사용자)

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

