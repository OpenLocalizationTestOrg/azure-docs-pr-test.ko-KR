---
title: "aaaAzure Mobile Engagement 설명서와 모범 사례"
description: "Azure Mobile Engagement 시작 가이드 및 온보딩 모범 사례"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: dfce1183-6398-466e-aa7e-ed702fb52818
ms.service: mobile-engagement
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: d3f81c34fe74f741a60ca511caa55c312af73b1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---getting-started-guide-with-best-practices"></a>Azure Mobile Engagement - 모범 사례 시작 가이드
## <a name="overview"></a>개요
**hello 모바일 화면 공간이 매우 복잡 합니다:** 2013에서 연구 발견 hello 평균 모바일 장치 27 응용 프로그램을 설치 했습니다. 일반적으로 사용자는 월간 30시간을 이러한 앱에서 보냅니다. 이 시간의 대부분은 소셜 네트워킹과 게임에 소비됩니다(약 20시간). 2014 년으로 hello Android 시장에서 toochoose 사용자에 대 한 약 1.5 백만 응용 프로그램에 있습니다. hello Apple 스토어 약 1.2 백만 앱을 포함 합니다. 모바일 앱 사용은 개발자들이 이 성장 시장에서 경쟁하고 있으므로 여전히 증가하고 있습니다. 

hello 평균 모바일 사용자가 설치 하 고 자주 발생 하는 관심 분야 변경에 따라 사용 하 여 앱을 제거 하 고 앱에서 발생 합니다. 응용 프로그램의 순서 toodetermine hello 성공에 중요 한 tooknow 되기 보다 얼마나 많은 사용자가 응용 프로그램을 설치 합니다. 중요 한 tooknow 해당 사용률 추세를 변경 하는 경우 및 앱이 얼마나 유용한 경우 hello 다음 질문에 중요 해 집니다.

* 사용자가 시작 하는 toofind 필요 하지 않은 또는 사용 되지 않는 앱? 
* 얼마나 많은 사용자가 앱 사용을 완전히 중지했습니까? 
* 앱 내 구매 추세가 증가합니까 아니면 감소합니까?
* 사용자가 실패 하는 작업 흐름 toocomplete hello 앱 또는 관심 부족의 문제로 인해? 
* 수 유지 앱 유용 성과 관련 된 새로운 콘텐츠 tooyour 사용자 기본 푸시하여? 
* 이 새로운 콘텐츠 것은 모든 사용자에 대해 동일 하거나 응용 프로그램에서 동작에 따라 사용자 세그먼트에 초점을 맞추고 hello 무엇입니까? 

대답 tooquestions 비슷한 toothese 앱에서 hello 수명 및 수익을 확장할 수 있습니다. 또한 사용자 기반을 정의하고 유지하는 데에도 도움이 될 수 있습니다. 

미디어 관련 앱 경향이 toohave hello 가장 높은 보존 사용자 들의 일부입니다. 한 이유는 최신 콘텐츠 toousers 지속적으로 제공 합니다. Tooa 사용자 세그먼트 경향이 toohave 보존 응용 프로그램에 중대 한 영향을 전송 하는 유용한, 푸시 알림의 조기 채택 했습니다. 

hello Azure Mobile Engagement 프로그램은 설계 된 toohelp 메서드 toogather 제공 하 여 hello 수명 및 응용 프로그램의 보존을 확장 하 고 응용 프로그램의 hello 사용에 대 한 자세한 정보를 분석 합니다. Toobehavior에 따라 사용자 기반 분류 하 고 tooidentified 사용자 세그먼트 푸시 알림 및 앱에서 메시지를 제공 하기 위한 집중 된 캠페인을 만드는 데 도움이 됩니다. 핵심 성과 지표(KPI)는 사용자가 앱의 서로 다른 측면에 대해 얼마나 활발한지 측정합니다. Hello 메서드를 제공 하는 azure Mobile Engagement toodetermine이이 Kpi를 해야 합니다. Hello 반환 증가 하는 데 도움이 프로그램 ROI (투자) hello 인프라를 제공 하 여 모바일 앱과 함께 tooincrease engagement 필요 합니다. 

Azure Mobile Engagement을 최대한 활용 순서 tooget hello, toostart 잘 디자인 된 서비스 계획을 사용 해야합니다. 계획은 해야 toobe 수 toosegment 사용자 기본 hello 세분화 된 데이터를 식별 하는 데 도움이 됩니다. 행동과 앱 내 경험을 기반으로 이러한 데이터를 식별할 수 있습니다. 성공 하면 계획 toobe 위해에서 모범 사례 tooclearly hello는 응용 프로그램의 hello 목표를 측정 하는 KPI 정의입니다. 정의 된 일반 성능 표시기를와 쉽게에 포함할 수 있습니다 hello 필수 논리가 하면 앱 toocollect 세밀 하 게 세분화 된 데이터를 수행 합니다 tooanalyze를 사용 하 고 여 Kpi를 평가 합니다. 이 항목은 모범 사례 가이드 engagement 계획에 사용할 hello Kpi를 정의 합니다. 

## <a name="step-1-define-your-kpis-toofit-hello-bet-model"></a>1 단계: Kpi toofit hello 선택 모델 정의
Kpi 정의 올바르게 어려운 작업 toocomplete 될 수 있습니다. 서로 다른 산업을 위해 설계된 앱은 고유의 특이한 사항과 목적을 가지고 있습니다. 이는 tooconfuse 접근 방식을 경향이 수 있습니다. toohelp이 문제를 방지, 목표 및 Kpi 세 개의 주요 범주로 분류 해야 할: **비즈니스**, **Engagement**, 및 **기술**합니다. 이 hello 주기 **선택 모델**합니다.

좋은 계획은 각각 hello hello 선택 모델의 범주를 다음의 hello 성공을 측정 하는 hello Kpi와 함께 목표 일반적으로 갖습니다.

#### <a name="business-kpis"></a>비즈니스 KPI
비즈니스 Kpi hello 쉬운 부분 toobuild 이어야 합니다. 아마도 모바일 앱을 계획할 때 모종의 형태로 이를 이미 정의했을 것입니다. 이 KPI는 일반적으로 앱의 수익과 ROI를 측정하는 데 도움이 됩니다. hello 다음 목록에서는 몇 가지 예 성과 지표를 정의 하는 동안 안내 하는 데 도움이 되는 비즈니스 Kpi.

* 미디어 비즈니스 KPI
  * 클릭한 광고 수
  * 사용자당 페이지 방문 횟수
  * 현재 구독 수
* 게임 비즈니스 KPI 
  * 앱 내 구입 수
  * 사용자당 평균 수익(ARPU)
  * 세션당 소요된 시간
  * 게임 수준에서 재생한 횟수 및 현재 일수
* 전자 상거래 비즈니스 KPI
  * 앱을 사용한 일수
  * 사용자당 평균 수익(ARPU)
  * 체크아웃하는 동안 장바구니의 평균 금액
  * 대부분의 뷰 및 구입에 대한 제품 범주
* 은행 및 보험 비즈니스 KPI
  * 계정 수
  * 활성화된 기능
  * 방문한 페이지 수 제공
  * 클릭 또는 활성화된 경고 수       

#### <a name="engagement-kpis"></a>고객 관리 KPI
서비스 KPI의 사용자는 성능 표시기 toomeasure hello engagement입니다. 이 영역에는 추세 응용 프로그램의 hello 보존 결정할 수 있습니다. 다음은 이 유형의 KPI에 대한 몇 가지 예제 성과 지표입니다.

* Hello 지난 7 일 이내에에서 활성 사용자
* 지난 7 일 동안 hello에 대 한 비활성 사용자 수
* 30 일 이내에 hello 앱을 사용 하지 않은 사용자의 수  

명백한 일부 외부 요인이 이 영역의 지표에 영향을 줄 수 있습니다. 예를 들어 언제 든 사용자가 모바일 장치 toobe를 고려할 수 있습니다. 이는 사실일 수도 있고 그렇지 않을 수도 있습니다. 게임 앱 때 게이머는 재생 학교 안팎 작업 해제 하는 동안 자세한 공휴일 주위 toohave 사용량이 간격과 될 수 있습니다.   

잘 정의 되어이 범주에서 Kpi는 데 도움이 되도록 응용 프로그램 개발자와 고객이 간의 hello 관계를 측정 합니다.

#### <a name="technical-kpis"></a>기술 KPI
이 범주에 속하는 성과 지표는 앱이 올바르게 작동하는지, 작동 중지했는지 또는 충돌하고 있는지 여부를 결정하는 데 도움이 됩니다. 이 지표는 응용 프로그램의 hello 상태를 측정 하 고 hello 앱을 사용 하 여 사용자가 방해할 수 있는 유용성 문제를 확인할 수 있습니다. 또한이 범주에 대해 수집 된 정보는 관련 toomarketing 팀 것 성능 정보를 포함 합니다. hello 데이터에서 문제 해결에 유용한 경우도 IT 지원 팀 toohelp 보고 되지 않은 버그를 식별 합니다. 

다음은 기술 KPI의 몇 가지 예입니다.

* 처리되지 않은 또는 처리된 예외 정보 및 개수 
* 마지막 충돌에 대한 타임 스탬프
* 마지막 클릭한 버튼 또는 마지막 방문한 페이지
* Hello 앱의 메모리 사용량
* 앱 프레임 속도
* 실행 중인 앱 hello OS 버전
* 앱 버전

이러한 Kpi toohelp 측정값 앱 성능을 정의 버그가 생길 정확 하 게 합니다. 이 지표는 고객을 위해 toodeliver 문제를 해결 해야 하는 hello 시간을 단축 하는 데 도움이 됩니다. 또한 특정 문제를 발견한 사용자 계층을 정의하는 데 도움이 될 수 있습니다. 사용 가능한 수정 사항 및 잠재적인 프로 모션 toohelp에 관한 사용자 조각화 toocreate 캠페인 toodeliver 알림 고객 만족도 복구를 사용할 수 있습니다. 

#### <a name="playbook-exercise-1-create-your-kpi-dashboard"></a>플레이 북 연습 1: KPI 대시보드 만들기
마케팅 전략을 정의할 때 KPI는 각각의 주 목표에 대한 뷰를 제공해야 합니다. Toocollect 중요 한 정보 toomonitor hello 최종 사용자의 사용자 앱과 hello 동작 수 있는 명확 하 게 정의 된 데이터 요소 수 있어야 합니다.

Hello 아래 정보를 포함 하는 KPI 대시보드 만들기

1. Hello 앱에 대 한 Kpi hello 이란?
2. 어떤 데이터 요소는 각 KPI toorepresent 사용 합니까?
3. 내 응용 프로그램에 대한 이 데이터(즉, 화면, 설정, 시스템...)를 어디서 찾습니까?
4. 이 KPI에 대한 고객 관리 순서를 실행할 수 있습니까?

Hello를 사용할 수 있습니다 **KPI 작성기** 워크시트에 우리의 [미디어 플레이 북 템플릿] [ Media Playbook link] 예제 및 설명서입니다.

## <a name="step-2-your-engagement-program"></a>2 단계: 고객 관리 프로그램
우수한 모바일 고객 관리 프로그램을 앱의 핵심 구성 요소로 생각해야 합니다. 이 첫 번째 요일 인 앱 사용 hello 하는 동안 사용자에 대해 실행 하는 좋은 시작 프로그램 반드시 있어야 합니다. 이 계약 및 응용 프로그램의 보존에 매우 긍정적인 영향 toohave를 경향이 있습니다. 연구를 해당 hello 대부분의 사용자가 중지 설치 후 처음 몇 일 동안 앱 hello를 사용 하 여 보여 줍니다. Toostrive toomeet 하거나 hello 사용자 응용 프로그램에 계속 포커스가 있는 동안 초기 고객의 기대 구동 관심을 초과 합니다. 표시할 hello 키 값과 응용 프로그램의 이점 tooyour 고객 있는지 확인 합니다. 

![](./media/mobile-engagement-getting-started-best-practices/unsegmented-push-notifications.png)

푸시 알림은 hello 가장 좋은 방법은 tooearly 프로그램에 참여 모바일 장치 사용자가 있습니다. 그러나 푸시 알림에 대한 사용자를 구분할 때 각별히 주의해야 합니다. 사용자가 스팸 또는 흥미가 없는 알림을 받는 것 같이 느끼면 심각한 영향을 미칠 수 있기 때문입니다. 몇 번의 클릭에서 사용자 응용 프로그램을 삭제할 수 있습니다 tooreturn 하지 않습니다. hello 사용자 제네릭 스팸 대신 항상 개인 설정 된 응용 프로그램에 값을 표시 됩니다.

사용자가, 수행 되 면 다음 engagement 프로그램 데 도움이 됩니다 hello 앱의 다른 측면 드라이브.

예를 들어, 앱 활성 사용자 toorate를 요청 하는 캠페인을 설정할 수 있습니다. 이 사용자 세그먼트는 가장 활동적인 hello hello 대부분 경험이 하면 응용 프로그램에 있으므로 예상 대로 toogive hello 가장 정확한 등급입니다. 높은 앱 등급을 만든 후에 새 고객 취득 비용을 감소도 응용 프로그램의 hello 유기적 다운로드를 드라이브를 유용 합니다.

#### <a name="engagement-sequence"></a>고객 관리 시퀀스
글로벌 고객 관리 프로그램은 서로 다른 고객 관리 순서를 포함하고 있습니다. 각 시퀀스 tooreach 몇 가지 목표를 목표로 합니다.

###### <a name="life-push-sequence"></a>수명 푸시 순서
수명 푸시 시퀀스에 대 한 hello 목표 hello 사용자의 커뮤니케이션: hello 앱의 hello 수명 주기에 따라 달라 집니다. 특정 사용자는 새 사용자, 소극적 또는 매우 적극적인 사용자일 수 있습니다. Engagement 수명 주기의 다른 단계에서 사용자는 hello 형태의 toodocumentation 팁 또는 링크에서 새 콘텐츠에서 활용할 수 있습니다. 

예를 들어 새 사용자를 지향된 tooan 응용 프로그램을 시작 하는 데 도움이 필요 또는 새 사용자 보상 비슷한 toohello hello hello 앱을 시작 하는 처음으로 다음에서 이점을 얻을 수 있습니다...

*"주셔서 감사 드립니다 toohave 도와! Toologin tooget 기억 하면 첫 번째 월 무료! "*

###### <a name="behavioral-push-sequence"></a>동작 푸시 순서
hello 푸시 동작 시퀀스는 hello 앱에 대 한 수집 하는 사용자 동작에 따라 tooincrease 사용을 방식 합니다.  

예를 들어 판타지 football 응용 프로그램의 활성 사용자 푸시 알림을 수행 하는 hello로 수행 되 고에서 이점을 얻을 수 중...

*"John 님은 열렬한 축구 팬입니다! Tooour NFL 섹션에 로그인 및 사용 가능한 액세스 toohello 슈퍼볼 win! "*

###### <a name="alerting-push-sequence"></a>수명 푸시 알림
사용자는 자신의 관심에 초점을 맞춘 관련 뉴스를 높이 평가합니다. 알림 푸시 순서는 사용자가 명확히 나타낸 관심을 기반으로 알림을 보내서 참여를 강화합니다. 사용자가 자신의 관심사 hello 응용 프로그램에서 명시적 액세스할 수 있습니다. 이 수를 결정할 수도 hello 앱과 사용자 상호 작용 하는 동안 수집 된 데이터에 따라 암시적으로.

예를 들어 전자 상거래 응용 프로그램의 hello 사용자 커피 비즈니스 KPI 사용 하 여 캡처할가 있는 특정 브랜드를 구입 정기적으로 될 수 있습니다. hello 다음과 같은 경고가 향상 시킬 수 hello 앱이이 사용자의이 협력 합니다.

*"Hi Wes, 커피 머 내역 프로그램 중 하나가 됩니다 25 %hello 할인 판매에 2015 년 9 월의 첫 번째 주입니다. 고객으로 서 있습니다 드립니다 및 toomake 있는지 려 한다고 인식 합니다. "*

###### <a name="rentention-push-sequence"></a>보존 푸시 순서
반복적인 푸시 알림 캠페인 toohelp를 사용 하 여이 시퀀스 aims tooretain 사용자 드라이브는 일반 습관이 hello 앱에 연락 합니다. 이 hello로 이용할 수 hello 상호 작용 하는 경우 앱 보존을 늘릴 수 있습니다. 

예를 들어 스포츠 관련된 응용 프로그램의 hello 사용자 hello 푸시 알림을 hello 사용자의 즐겨 찾는 팀에 따라 매주 다음 나타날 수 있습니다.

*"기회 toowin 200 포인트에 대 한 이동 투표 여부 hello New York Yankees 게임 이번 주에 대해 토론토 Blue 제비 승리 합니다!"*

#### <a name="hello-3w-approach"></a>hello 3W 접근 방식
Hello 개의 푸시 시퀀스를 마스터 최종 사용자에 게 문의 하는 데 도움이 됩니다. 그러나 보내야 toouse hello 3W 접근 방식을 개인 알림을 위한 합니다. hello 3W 접근 방식을 해결 해야 Who, 있으며 각 알림에 대해 합니다. 이러한 3 개의 질문을 명확하게 충족하면 알림이 참여를 위해 올바르게 집중되어야 합니다.

![](./media/mobile-engagement-getting-started-best-practices/who-what-when.png)

###### <a name="who-hello-user-segment-that-will-receive-messages"></a>메시지를 받을 사용자 세그먼트는: hello
푸시 알림 tooyour 사용자가 매우 중요 한 통신 채널을 고려 되어야 합니다. Hello toosend tooa 사용자 세그먼트를 목표로 알림은 해당 사용자 세그먼트의 범위가 지정 된 잘 toohello 관심 사항이 있는지 확인 합니다. 잘못 라우팅된 알림 가능성이 매우 toohave 사용자에는 음수 효과입니다. 스팸 tooyour 응용 프로그램을 제거 하 고 선행 고려 될 수 있습니다. 

알림을 받을 사용자 계층을 정의할 때 특정 기술 및 동작 기준의 조합을 사용합니다. 사용자 세그먼트를 정의 하는 간단한 예제 문 다음 비슷한 toohello 수 있습니다.

"를 시작한 모든 사용자가 모바일 응용 프로그램 hello에 대 한 처음으로 3 일 전에 hello 및 실제로 로그인을 완료 하지 않고 두 번 hello 로그인 페이지를 방문한"입니다.

해당 문에 hello 데이터 해야 toocollect toosupport 특정 시나리오를 식별 하는 데 도움이 됩니다.

###### <a name="what-hello-message-that-you-will-send"></a>내용: hello 메시지를 보낼
**발신음**

계층으로 구분한 사용자별로 적절한 발신음을 고객 관리에 사용합니다. 이 최종 사용자와 좋은 방법 tooconnect 보다 분명 하 고 응용 프로그램에 대 한 사용자의 관심을 승격 합니다. 

**리디렉션**

푸시 알림은 이상 hello 응용 프로그램을 열기 위해 사용할 수 있습니다. Hello 알림 메시지 제공 브로드캐스트 뉴스와 같은 컨텍스트 또는 제품 프로 모션,이 알림 년 5 월 딥 링크 toohello hello 응용 프로그램 내에서 콘텐츠를 마우스 오른쪽 단추로 직접 합니다. toosupport이 URL을 만들어야 합니다 구성표 toolet hello 응용 프로그램 hello 리디렉션을 관리 합니다. 고객 관리 순서에서 작업할 때 이는 잊지 말아야 할 중요한 단계입니다.

다른 시스템에 대한 리디렉션을 관리할 수도 있습니다. 예를 들어, 작업 URL 것이 가능한 tooredirect 최종 사용자에 게 toomany hello 다음을 비롯 한 다른 시스템:

* 웹 사이트
* 이미 설정된 이메일이 있는 사서함
* SMS 상자
* 다이얼 서비스
* 직접 toohello 앱 스토어의 hello 응용 프로그램 등급을 평가 합니다. 

이 tooengage 최종 사용자에 게 많은 기회를 제공 하 고 tooimprove 공연 자동 규칙을 만듭니다.

**형식/콘텐츠**

다양한 유형 및 푸시 알림 형식:

1. **공지** : 여러 순간 toosend 광고 메시지 toousers 사용 하면 (앱, 응용 프로그램에서 외부 또는 아무 때나).
2. **폴링** : 질문을 하 여 최종 사용자의 toogather 정보를 사용 합니다. 답변이 조건 tootarget 최종 사용자가 만들 때 사용할 수 있습니다.
3. **데이터 푸시** : toosend는 이진 또는 base64 데이터 파일 tooupdate hello 앱 수 있도록 합니다. 데이터 푸시에 포함 된 hello 정보는 응용 프로그램에서 tooyour 응용 프로그램 toopersonalize hello 사용자 환경을 전송 됩니다. 응용 프로그램 데이터 푸시의 설계 toobe toosupport hello 데이터에 필요 합니다.
4. **타일 (Windows Phone만 해당)** : toouse hello Microsoft 푸시 알림 서비스 (MPNS) toosend (SDK 버전 0.9.0 이후 지원 됨 XML 데이터를 포함 하는 기본 푸시 알림을 사용할 수. 타일에 대 한 마지막 페이로드 hello 수 없습니다 32kb를 초과 합니다.). hello 메시지 보드의 타일에 직접 나타납니다.
5. **웹 뷰** : 웹 뷰는 웹 콘텐츠가 포함된 팝업입니다. 이 팝업이 나타나며이 hello 푸시 알림을 hello 최종 사용자가 클릭 합니다. 웹 보기 있습니다 toohave hello 최종 사용자와 더 많은 상호 작용 합니다.

> [!NOTE]
> 으로 푸시 알림을 보내는 hello 콘텐츠를 준수 하는지 hello 각 플랫폼 (iOS, Android, Windows) 응용 프로그램을 개발 하 고 푸시 알림을 보내는 대 한 지침이 있는지 확인 합니다.
> 
> 

###### <a name="when-hello-timing-of-your-campaign"></a>캠페인의 타이밍 hello 경우:
캠페인 푸시 알림을 트리거하지 hello 최상의 시간 tooactivate 인가요? 수동이어야 합니까 아니면 자동이어야 합니까? 되풀이되어야 합니까? 결정 hello 적절 한 시기 또는 주파수 hello 최상의 결과를 필수 tooengage 사용자입니다. 각 engagement 시퀀스 및 시나리오에 대해 지정 해야 경우 푸시 알림을 hello 최상의 시간 toosend 됩니다. 몇 가지 가능한 예는 다음과 같습니다.

![](./media/mobile-engagement-getting-started-best-practices/campaign-timing-examples.png)

매일 많은 알림을 전송하는 경우 사용자가 전달 내용을 스팸으로 여길 수 있다는 것을 심각하게 고려해야 합니다. 

Azure Mobile Engagement toohelp 스팸 인정 되 통신을 방지 하는 두 가지 방법을 제공 합니다. 먼저, 사용 세부적인 조각화 tooensure 대상 hello 하지 동일한 사용자가 수행 합니다. 또한 Azure 모바일 서비스 계약 "할당량" 기능을 제공합니다. 이 기능으로 캠페인을 위해 전송되는 알림을 제한할 수 있습니다. 예를 들어 주당 기본 할당량 too5 설정 됩니다 되도록 hello 캠페인 사용자 세그먼트의 일부 해당 주간에 5 개 이하의 알림을 수신 하는 대로 포함 하는 사용자.

#### <a name="playbook-exercise-2-create-your-engagement-program"></a>플레이 북 연습 2: 고객 관리 프로그램 만들기
이러한 보안 설정을 요약 하는 일정 시간을 할애 하 고 tooplay 특정 순서를 사용 하 되 hello 캠페인을 정의 합니다. Hello 3W 접근 방식을 toohello 알림을 캠페인에 적용 해야 합니다. 

사용 하 여 hello **Engagement 프로그램** hello에서 워크시트 [미디어 플레이 북 템플릿] [ Media Playbook link] 예제 및 설명서입니다.

## <a name="step-3-app-integration"></a>3 단계: 앱 통합
#### <a name="create-a-tag-plan"></a>태그 계획 만들기
toointegrate Azure Mobile Engagement 응용 프로그램에 toocreate 태그 계획 해야 합니다. hello 태그 계획은 hello 프로젝트의 hello 토대입니다. Hello hello 응용 프로그램의 작업 흐름 hello 마케팅 사양 및 hello 앱 toomeasure Kpi에서에서 수집 된 hello 실제 태그 데이터 관계를 정의합니다. 어떤 분석 수 없게 됩니다. 나타냅니다 toosee hello 포털에서입니다. 또한 사용자 세그먼트를 정의 하 고 집중 된 푸시 알림 tooengage 최종 사용자에 게 보낼 수도 있습니다. Hello 태그 계획 정의 만든 후 hello 코드 toointegrate 추가 응용 프로그램에 간단 hello Azure Mobile Engagement SDK를 사용 하 여 합니다.

태그 계획은 응용 프로그램의 모든 내용에 태그를 지정하지 않아야 합니다. 모바일 고객 관리 전략의 일부인 태그 데이터만 포함해야 합니다. 이는 응용 프로그램 간에 따라 달라질 수 있습니다. hello [미디어 플레이 북 템플릿] [ Media Playbook link] Azure Mobile Engagement 사용 하 여 지정된 된 메서드에에서 태그 계획 구축한 제공 합니다. 사용 하 여 hello **태그 계획** 워크시트 가이드 toobuilding으로 태그를 계획 합니다.

태그 섹션에 hello 워크시트에 정의할 때 매우 구체적 이어야 합니다. 이 매우 중요 한 tooavoid 혼동입니다. 각 태그를 전송하는 각 예상 시나리오를 상세하게 정의합니다. 각 태그를 포함 하는 위치 hello 활동의 hello 이름을 포함 합니다. 이 모든에 포함할지 hello **Informative** hello 워크시트의 일부입니다. hello 태그 계획 워크시트 hello 테스트 확인에 대 한 기본 참조 해야 합니다. 

Hello에 **데이터 toocollect** 섹션, 개발 팀은 찾기 hello 형식, 이름, 값 및 각에 필요한 추가 정보 키/값 쌍에는 태그에 포함 됩니다 hello 응용 프로그램입니다.

Hello 프로젝트와 관련 된 모든 팀과 함께 hello 태그 계획을 검토 하는 것이 좋습니다. 필요한 수정을 하고 모든 내용이 마케팅 및 개발 팀에 대해 명확한지 확인합니다.

hello **작업 보고서** 워크시트에 사용 되는 toohelp 가이드 hello 프로젝트에 관여 하는 모든 사용자 일 수 있습니다.

#### <a name="data-types"></a>데이터 형식
이는 Azure Mobile Engagement에 의한 데이터 지원의 일반적인 형식입니다.

###### <a name="devices-and-users"></a>장치 및 사용자
Azure Mobile Engagement는 각 장치에 대해 고유한 식별자를 생성하여 사용자를 식별합니다. 이 식별자는 hello 장치 식별자 (또는 deviceid) 라고 합니다. 동일한 공유 장치에서 실행 중인 모든 응용 프로그램에 동일한 장치 식별자 hello 하는 방식으로 생성 됩니다.

###### <a name="sessions-and-activities"></a>세션 및 작업
세션은 사용자가 실행 되 고 hello 응용 프로그램의 한 인스턴스입니다. hello 사용자가 중단할 때까지 hello 앱을 시작 하는 hello 시간부터 hello 세션에 걸쳐 있습니다.

활동은 논리적 그룹화 집합의 작업 세션 중 hello 앱 수행할 수 있습니다. Hello 앱에는 특정 화면은 일반적으로 하지만 아무것도 hello 논리 hello 응용 프로그램에 의해 정의 될 수 있습니다. 적어도 앱에 대한 각 화면 또는 작업에 대한 태그를 지정해야 합니다. 따라서 있습니다 toounderstand hello 사용자-경로 수 있습니다.

###### <a name="events"></a>이벤트
이벤트는 hello 앱과 함께 사용 되는 tooreport 사용자 상호 작용 합니다. 이는 콘텐츠 공유 또는 비디오 시작 같은 순간적인 작업일 수 있습니다. 이벤트 태그 지정을 사용자 hello 앱와 상호 작용 하는 방법을 보여 주는 데이터 컬렉션을 제공 합니다. 

###### <a name="jobs"></a>작업
작업은 기간 영향을 주는 tooreport 사용 되는 작업입니다. 몇 가지 예:

* API 호출의 실행
* 광고의 표시 시간
* 백그라운드 작업 기간 
* 구매 프로세스 기간
* 비디오 시청

###### <a name="errors"></a>오류
오류는 hello 앱에서 감지한 tooreport 사용 되는 문제입니다. 예: 잘못된 사용자 작업 또는 API 호출 실패.

###### <a name="application-information"></a>응용 프로그램 정보
응용 프로그램 정보 (App-info)를 사용 tootag 데이터 관련 응용 프로그램으로 tooa 사용자의 경험 합니다. 사용자의 상호 작용 hello 응용 프로그램에 의해 생성 됩니다. 

지정 된 앱 정보 키에 대 한 Azure Mobile Engagement만은 hello 최신 값 기록이 없습니다. 응용 프로그램 정보에서 응용 프로그램 또는 최종 사용자의 hello 상태를 보여 줍니다. 예를 들어 hello 로그인 상태 또는 사용자가 즐겨 찾는 제품 그룹입니다.

###### <a name="crash-data"></a>충돌 데이터
Hello 응용 프로그램에서 처리 되지 않은 hello Mobile Engagement SDK 보고서 응용 프로그램 오류에 의해 자동으로 수집 된 데이터 충돌. 예: 발생한 처리되지 않은 예외.

###### <a name="extra-data"></a>추가 데이터
매개 변수를 사용하여 이벤트, 오류 및 작업을 향상시킬 수 있습니다. 이 추가 정보는 개발자 hello 응용 프로그램의 특정 데이터를 제공할 수 있습니다. 이는 세분화된 구분을 정의하는 데 중요합니다. 

예를 들어 "문서" 태그 hello 값 하면 해당 특정 문서를 볼 사용자에 따라 toosegment 최종 사용자가 있습니다. 그러나 이것만으로 충분하지 않을 수 있습니다. 같은 “article” 태그가 작업 내에 “news_category” 같은 추가 태그도 포함하고 있으면 더 좋을 수 있습니다. 이 방법이 유용 toodetermine hello 사용자에 대 한 즐겨찾기 범주를 동적으로 hello 합니다. 

추가 정보는 키/값 쌍으로 보고됩니다. 이 미디어 응용 프로그램에 대 한 hello 예제에서는 "news_category"에 대 한 hello 추가 정보는 해당 범주에 대 한 hello 값 것입니다. 예: "스포츠", "경제" 또는 "정치".

#### <a name="tag-and-sdk-integration"></a>태그 및 SDK 통합
통합 하기 위한 단계별 지침은 앱에 Azure Mobile Engagement SDK hello에 대 한 따라 hello [Engagement SDK 통합](mobile-engagement-windows-store-integrate-engagement.md) Azure 웹 사이트에 대 한 설명서입니다. 해당 페이지의 hello 위쪽 hello 링크에서 대상 플랫폼을 선택 합니다.

Azure Mobile Engagement의 위쪽에 만들어진 앱 두 개에 대한 프로젝트를 만드는 것이 좋습니다. 개발 및 테스트 준비 및 프로덕션 준비에 대 한 다른 hello에 대 한 하나입니다. IT 팀이 성공적으로 hello 사용자 수용 테스트 tooproduction를 준비 하는 테스트에서 다음 승격할 수 있습니다.

#### <a name="user-acceptance-testing-uat"></a>사용자 수용 테스트(UAT)
사용자 수용 테스트(UAT)에는 모든 것이 설계한 대로 작동한다고 확인하는 과정이 포함됩니다. 워크플로를 완료하고 태그 계획에 따라 모든 필요한 데이터를 수집할 수 있습니다.

* Toodocumented AZME 개념에 따라 준비 해야 정보 태그 지정
* 필요한 모든 정보가 수집됨추가 정보 값, 앱 정보 값 포함)
* 용어 체계 태그 계획에 따라 tooyout 일치
* 전송된 중복 태그 없음

모든 hello 유형의 응용 프로그램에 삽입 한 알림 동작을 철저히 테스트

* 앱에서 그리고 앱 내의 알림, 설문 조사, 데이터 푸시
* 텍스트/웹 뷰
* 배지 업데이트, 범주

#### <a name="setup"></a>설정
Azure Mobile Engagement 설정은 매우 간단합니다. 모든 hello 설명서 toohello 사용자 인터페이스는 hello Azure Mobile Engagement 웹 사이트에서 사용할 수 있는 관련 [어떻게 toonavigate hello 사용자 인터페이스](mobile-engagement-user-interface-home.md)합니다.

Hello 적절 한 역할 및 프로젝트의 hello 사용자에 대 한 역할 멤버 자격을 설정 하 여 시작 하는 것이 좋습니다. 이렇게 하면 모든 사용자에 대해 적절 한 액세스 toohello 플랫폼을 관리할 수 있습니다. 역할은 다음을 포함할 수 있습니다.

* 관리자
* 개발자
* 뷰어 

나중에:

* 자신의 장치에서 프로그램 deviceID tootest를 등록 합니다.
* 사용자의 계정 toohello 설정 이동 하 고 hello 시간대 toohave 차트 및 시간대에 대해 설정 된 알림 배달 시간을 설정 합니다.
* 응용 프로그램의 toohello 설정 이동 하 고 hello "앱-info" tootarget 최종 사용자 나감에 필요를 등록 합니다.

어떻게 toorun 첫 번째 푸시 대 한 자세한 내용은 알림 캠페인, 검토 [tooget 처음 사용 하는 방법과 tooreach tooyour 최종 사용자가 푸시 관리](mobile-engagement-how-tos.md)합니다.

## <a name="conclusion"></a>결론
고객 관리 프로그램은 반복적이며 앱에 가장 적합한 내용을 실험하면서 지속적으로 자신의 앱을 개선해야 합니다. 

경험을 개발 하는 동안 처음에 engagement 전략 toobuild 전체 전역 engagement 전략 시도 하지 않습니다. 식별 하 여 Kpi 단계별 접근 방법과 tooleverage 해당 합니다. 고객 관리 전략은 각 앱마다 고유합니다.

경험을 개발한 다음 tooyour engagement 프로그램 hello 추가 고려할 수 있습니다.

* 추적: 사용자를 획득하고 아마도 데이터 컬렉션 소스를 정의합니다. Azure mobile Engagement는 연결 된 toodata 컬렉션 원본 될 수 있습니다. 각 소스의 toomonitor 성능이 있습니다. 이 정보 획득 투자 흥미로운 toomaximize 됩니다. 
* A / B 테스트: 고객 관리 프로그램의 필수 부분입니다. 각 앱마다 자체의 구체적 사항이 있습니다. A/B 테스트를 사용하면 고객 관리 프로그램을 개선할 수 있습니다.
* 지리적 위치: 브랜드에 대해 아주 좋은 기회입니다. 감사 toothis 기능 hello 올바른 위치와 시간에 도달할 수 있습니다. Toouse 지리적 위치를 시작 하기 전에 충분 한 최종 사용자 동작 데이터를 수집 했는지 확인 하는 것이 좋습니다.
* 데이터 푸시: 데이터 푸시는 보이지 않는 푸시입니다. 데이터 푸시를 사용하여 최종 사용자 동작을 기반으로 응용 프로그램을 사용자 지정할 수 있습니다. 예를 들어, 사용자 세그먼트 첨단 기술 제품을 자주 참조, hello 응용 프로그램 소유자 첨단 기술 콘텐츠를 사용한 홈 페이지의 내용을 사용자 정의할 수 있는 데이터 푸시를 보낼 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [Azure Mobile Engagement 계정을 만듭니다](mobile-engagement-create.md).
* 방문 [Mobile Engagement 전략 정의](mobile-engagement-define-your-mobile-engagement-strategy.md) toolearn Mobile Engagement 전략 정의 하는 방법에 대 한 자세한 합니다.

<!--Image references-->


<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
