---
title: "에너지의 수요 예측에 대 한 Intelligence 솔루션 템플릿을 플레이 북 aaaCortana | Microsoft Docs"
description: "에너지 공익 사업체에서 수요를 예측할 수 있도록 하는 Microsoft Cortana Intelligence 솔루션 템플릿입니다."
services: cortana-analytics
documentationcenter: 
author: ilanr9
manager: ilanr9
editor: yijichen
ms.assetid: 8855dbb9-8543-45b9-b4c6-aa743a04d547
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2016
ms.author: ilanr9;yijichen;garye
ms.openlocfilehash: 32fc6ece7e24ced34282baf107548039694a38b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-demand-forecasting-of-energy"></a>에너지 수요 예측을 위한 Cortana Intelligence 솔루션 템플릿 플레이 북
## <a name="executive-summary"></a>요약
지난 몇 년 동안 인터넷 IoT (사물), hello에서 대체 에너지 원본과 빅 데이터 hello 유틸리티 및 에너지 도메인 toocreate vast 기회 병합 했습니다. Hello에서 동일한 시간, hello 유틸리티 및 hello 전체 에너지 섹터 더 나은 방법으로 toocontrol 요구 되는 소비자와 함께 해당 메일의 에너지 사용 평면화 소비를 살펴보았습니다. 따라서 유틸리티 및 스마트 그리드 회사 훌륭한 필요 tooinnovate에 있으며 자체 갱신 hello 합니다. 또한 많은 전원 및 유틸리티 표 오래 되 고 비용이 많이 들 toomaintain 강조 되 고 관리 합니다. Hello 작년 동안 hello 팀의 다양 한 고객 참여를 통해 hello 에너지 도메인 내에 근무 합니다. 이러한 고객 참여를이 통해 하는 동안 대부분의 경우에는 hello 유틸리티 또는 Isv (Independent Software Vendor) 입고 되었습니다 이후 에너지 수요의 예측에 발생 했습니다. 이러한 예측 현재와 미래의 비즈니스에 중요 한 역할 및 다양 한 사용 사례에 대 한 hello foundation 하 게 합니다. 여기에는 단기 및 장기 전원 부하 예측, 거래, 부하 분산 및 그리드 최적화 등이 포함됩니다. 빅 데이터 및 컴퓨터 학습 (ML)와 같은 고급 분석 AA () 메서드 정확 하 고 신뢰할 수 있는 예측을 생성 하기 위한 hello 핵심 요소는입니다.  

이 플레이 북에 넣을까요 함께 hello 비즈니스 및 성공적인 개발에 필요한 분석 지침 및 에너지 수요의 배포 솔루션을 예측 합니다. 이러한 제안된 지침은 공익 사업자, 데이터 과학자 및 데이터 엔지니어가 완전히 조작 가능한 클라우드 기반, 수요 예측 솔루션을 구축하는 데 도움이 될 수 있습니다. 해당 빅 데이터 및 고급 분석 작업 시작 하는 회사를 이러한 솔루션은 장기적인 스마트 그리드 전략에서 초기 시드 hello을 나타낼 수 있습니다.

> [!TIP]
> 이 서식 파일의 한 아키텍처 개요를 제공 하는 다이어그램 toodownload 참조 [에너지의 수요 예측에 대 한 Cortana Intelligence 솔루션 템플릿을 아키텍처](cortana-analytics-architecture-demand-forecasting-energy.md)합니다.  
> 
> 

## <a name="overview"></a>개요
이 문서에서는 hello 비즈니스, 데이터 및 Cortana Intelligence를 사용 하 여 및에서 특정 Azure 컴퓨터 학습 (AML) hello 구현 및 에너지 예측 솔루션의 배포에 대 한 기술적인 측면에 설명 합니다. hello 문서 세 부분으로 구성 됩니다.  

1. 비즈니스 이해  
2. 데이터 이해  
3. 기술 구현

hello **비즈니스 이해** 부분 윤곽선 비즈니스 측면 하나 요구 toounderstand hello 및 이전 toomaking 투자를 결정 하는 것이 좋습니다. Tooqualify 예측 분석 및 기계 학습은 실제로 효과적이 고 적용 가능한 손 tooensure에서 비즈니스 문제를 hello 하는 방법을 설명 합니다. hello 문서 기계 학습 및 사용 되는 tooaddress 에너지 예측 문제는 방법의 hello 기본 사항을 설명 합니다. Hello 필수 구성 요소 및 hello 자격 조건 사용 사례에 간략하게 설명 합니다. 일부 샘플 사용 사례와 비즈니스 사례 시나리오도 제공됩니다.

데이터는 hello 주요 요소는 기계 학습 솔루션입니다. hello **데이터 이해** 이 설명서의 hello 데이터의 몇 가지 중요 한 측면에 설명 합니다. Hello 에너지 예측, 데이터 품질 요구 사항 및 데이터 소스는 일반적으로 존재 하는 데 필요한 데이터 종류를 설명 합니다. 또한 hello 원시 데이터의 사용 되는 tooprepare 데이터 기능 실제로 일부 모델링 hello를 구동 하는 방법을 설명 합니다.

hello 문서의 hello 세 번째 부분에서는 hello **기술 구현** 는 솔루션의 측면입니다. 기능 엔지니어링 및 모델링 hello 데이터 과학 프로세스의 핵심 hello 같고 좀 더 자세히 설명 되 고 따라서 합니다. 웹 서비스를 예측 분석 솔루션의 클라우드 배포에 대 한 중요 한 자동차의 hello 개념을 설명 합니다. 종단 간 조작 가능한 솔루션의 일반적인 아키텍처도 간략하게 설명합니다.

또한 hello 문서 toogain 상세하게 hello 도메인 및 기술 이해를 사용할 수 있는 참조 자료를 포함 합니다.

중요 한 toonote는 म 숨기지 않으려면 toocover이 문서 hello 깊은 데이터 과학 프로세스에서는 수치 및 기술 요소 이며 이러한 세부 정보는 [Azure 기계 학습 설명서](http://azure.microsoft.com/services/machine-learning/) 및 [블로그](http://blogs.microsoft.com/blog/tag/azure-machine-learning/)에서 확인할 수 있습니다.

### <a name="target-audience"></a>대상 사용자
이 문서에 대 한 hello 대상 사용자는 비즈니스 및 기술 담당자가 toogain 기술 및 솔루션 및 hello 에너지 예측 도메인 내에서 사용 되 고 방법 이해 기계 학습의 기반으로 합니다.

이 문서 toogain hello 높은 수준의 프로세스 드라이브 hello 에너지 예측 솔루션의 배포를 보다 잘 이해 읽을 데이터 과학자를 활용할 수 있습니다. 이 컨텍스트에서 사용 되는 tooestablish를 정하는 기준 및 더에 대 한 시작 지점 자세히 설명 하 고 자료 고급 일 수도 있습니다.

### <a name="industry-trends"></a>산업 동향
지난 몇 년 동안 hello에서 IoT, 대체 에너지 소스 및 빅 데이터 hello 유틸리티 및 에너지 공간에서 toocreate vast 기회를 병합 했습니다. Hello에 동시, hello 유틸리티 및 hello 전체 에너지 섹터에 더 나은 방법으로 toocontrol 요구 되는 소비자와 함께 해당 메일의 에너지 사용 평면화 소비를 살펴보았습니다.

가 hello 선구적인 된 많은 유틸리티 및 스마트 에너지 회사 [스마트 그리드](https://en.wikipedia.org/wiki/Smart_grid) hello 표에 의해 생성 된 hello 데이터의 사용 하는 경우 다양 한 사용을 배포 하 여 합니다. 전기 프로덕션의 기본적인 특성 hello 중심으로 많은 사용 사례: 누적 하거나 재고로 따로 저장 될 수는 없습니다. 따라서 생성되는 전기를 사용해야 합니다. Toobecome 보다 효율적인 원하는 유틸리티 tooforecast 전력 소비를 단순히 필요 하는 알려 능력 너무 때문에**공급 및 수요를 분산**, 에너지 wastage 하지 못하도록 차단 **greenhouse 줄이기 내보내기 작업 가스**, 고 비용을 제어 합니다.

비용에 관해 이야기할 때 가격이라는 다른 중요한 측면이 있습니다. 새 기능 tootrade 전원 유틸리티 간의 가져온 훌륭한 필요 너무**향후 수요를 예측 하는 전기 이후 가격**합니다. 그러면 회사는 발전량을 결정할 수 있습니다.

'스마트' hello 단어를 사용할 때 다음 예측을 확인 하 고 내릴 수 있는 tooa 표 실제로 이라고 합니다. 소비량의 계절별 변동을 예상할 수 있으며 **임시 오버로드 상황을 예견하고 자동으로 조정**할 수 있습니다. (사용 하 여 hello 이러한 스마트 미터) 소비를 원격으로 규제 하 여 지역화 된 오버 로드 상황을 처리할 수 있습니다. **먼저 예측 하 고 다음 작업을 수행 하 여**, hello 눈금은 더 효율적인 시간이 지남에 따라 합니다.

특정 제품군의 미래를 예측 하는 포함 하는 사용 사례에 대해 살펴볼 것이 문서의 나머지 부분 hello에 대 한, 단기 및 장기 에너지 요구 합니다. 몇 개월 동안 이러한 영역에서 작업 하 고 일부 지식과 tooproduce 업계 등급의 결과 수 있는 기술 얻었습니다. 다른 사용 사례는 가까운 미래 hello에 hello 문서에도 설명 합니다.

## <a name="business-understanding"></a>비즈니스 이해
### <a name="business-goals"></a>비즈니스 목표
hello **에너지 데모** toodemonstrate 일반적인 예측 분석 및 기계 학습 매우 짧은 시간 내에 배포할 수 있는 솔루션 ´ ֲ 합니다. 특히 현재 초점은 에너지 수요 예측 솔루션을 사용하여 비즈니스 가치를 신속하게 실현하고 활용할 수 있도록 하는 것입니다. 이 플레이 북의 hello 정보 hello 고객 목표를 수행 하는 hello를 수행 하는 데 도움이 됩니다.

* 기계 학습의 짧은 시간 toovalue 기반 솔루션
* 기능 tooexpand 파일럿 사용 사례 tooother 사용 사례 또는 tooa 보다 넓은 범위의 해당 비즈니스 요구에 따라
* Cortana Intelligence Suite 제품 지식을 신속하게 획득

이러한 목표를가지고 있는이 플레이 북 hello 비즈니스 및 기술 지식 이러한 목표를 달성 하는 데 도움이 되는 전달 하고자 합니다.

### <a name="power-load-and-demand-forecasting"></a>전원 부하 및 수요 예측
Hello 에너지 섹터 내에서 여러 가지 방법으로 수요에서 예측 수 문제 해결할 수 있도록 중요 한 비즈니스 있을 수 있습니다. 사실, 수요 예측 간주할 수 hello 업계의 핵심 사용 사례에 대 한 hello foundation 있습니다. 일반적으로 단기 및 장기라는 두 가지 유형의 에너지 수요 예측을 고려합니다. 각각 서로 다른 목적이 있으며 서로 다른 방법을 활용할 수 있습니다. 두 hello 간의 주요 차이점 hello는 hello hello 시간의 범위 이후 hello에 म 예측 것을 의미 하는 수평을 예측 합니다.

#### <a name="short-term-load-forecasting"></a>단기 부하 예측
Hello 에너지 요청의 컨텍스트 내에서 짧은 단어 로드 예측 (STLF)는 가까운 미래 hello 표 (또는 전체적으로 hello 그리드)의 여러 부분에는 hello에 예상한 hello 집계 된 부하로 정의 됩니다. 이 컨텍스트에서 단기는 1 시간 too24 시간 hello 범위 내에서 정의 된 toobe 시간 마감일을는 합니다. 일부 경우에 48시간 범위도 가능합니다. 따라서 STLF이 hello 눈금의 한 운영 사용 사례에 매우 일반적입니다. STLF 기반 사용 사례의 몇 가지 예는 다음과 같습니다.

* 공급과 수요 균형 조정
* 전원 거래 지원
* 시장 조성(전력 가격 설정)
* 그리드 운영 최적화
* [수요 대응](https://en.wikipedia.org/wiki/Demand_response)
* 최고 수요 예측
* 수요 관리
* 부하 분산 및 오버로드 방지
* 장기 부하 예측
* 장애 및 이상 감지
* 최고 단축/평준화 

STLF 모델 hello 기반 대부분 (마지막 일 또는 주)을 지 나 근처 소비 데이터와 사용으로 중요 한 예측자 온도 예상 합니다. 정확 하 게 온도 too24 시간 이상 hello 다음 시간에 대 한 예측을 얻기 해지고 이하로 challenge 지금 일 수 있습니다. 이러한 모델은 비교적 중요 하지 않은 tooseasonal 패턴 또는 장기 소비 추세입니다.

SLTF 솔루션은 또한 가능성이 toogenerate 대량 예측 호출이 (서비스 요청 수)는 시간 단위로 및 일부 경우에도 높은 빈도로 호출 되 고 있으므로 합니다. 여기서 각 개별 변전소 또는 변환기는 독립 실행형 모델으로 표시 하 고 따라서 hello 요청 볼륨을 예측은 더 높은 매우 일반적인 toosee implantation 이기도 합니다.

#### <a name="long-term-load-forecasting"></a>장기 부하 예측
hello 목표의 긴 단어 부하 예측 (LTLF)에 1 주일 toomultiple 개월에서 (및 경우에 따라 여러 해 동안) 사이의 시간 마감일을 사용 하 여 tooforecast 전원 요청입니다. 이 시간 범위는 주로 계획 중이고 투자 사용 사례에 적용 가능합니다.

장기 시나리오에는 여러 연도 (최소 3 년)의 범위를 검사 하는 중요 toohave 고품질 데이터입니다. 이러한 모델은 일반적으로 hello 기록 데이터의 계절성 패턴을 추출를 외부 predicators 등 사용 하려는 계절 및 기후 패턴으로 합니다.

것이 중요 마감일을 예측 하는 긴 hello hello tooclarify, hello 정확한 hello 예측 덜 수 있습니다. 따라서 중요 한 tooproduce 실제 hello와 함께 신뢰도 간격 일부 예측 인간이를 계획 과정 toofactor hello 가능한 변형을 허용 하는 버전이 있습니다.

LTLF에 대 한 hello 소비 시나리오에서 주로 계획 하 고 있으므로 기대할 수 있는 많은 낮은 예측 볼륨 (으로 비교 된 tooSTLF). 이러한 예측을 Excel 또는 PowerBI와 같은 시각화 도구에 포함 된 표시 되는 일반적으로 것 하 고 hello 사용자가 수동으로 호출할 수 있습니다.

### <a name="short-term-vs-long-term-prediction"></a>단기 및 장기 예측 비교
다음 표에서 hello 존중 toohello 가장 중요 한 특성에서 STLF LTLF을 비교 합니다.

| 특성 | 단기 부하 예측 | 장기 부하 예측 |
| --- | --- | --- |
| 예측 기간 |1 시간 too48 시간부터 |이상인 too6 1 개월 |
| 데이터 세분성 |매시간 |매시간 또는 매일 |
| 일반적인 사용 사례 |<ul><li>공급과 수요의 균형</li><li>최대 시간 예측</li><li>수요 대응</li></ul> |<ul><li>장기 계획</li><li>그리드 자산 계획</li><li>리소스 계획</li></ul> |
| 일반적인 예측 변수 |<ul><li>일 또는 주</li><li>하루 중 시간</li><li>시간별 온도</li></ul> |<ul><li>연간 월</li><li>날짜</li><li>장기 온도 및 기후</li></ul> |
| 과거 데이터 범위 |두 개의 toothree 년치 데이터 |5 개의 too10 년치 데이터 |
| 일반적인 정확도 |5% 이하의 MAPE* |25% 이하의 MAPE* |
| 예측 빈도 |1시간 또는 24시간마다 생성됨 |월별, 분기별 또는 매년 한 번 생성됨 |

\*[MAPE](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error) – 평균 백분율 오차(Mean Average Percent Error)

이 테이블에서 볼 수 때 매우 중요할 toodistinguish hello 짧은 사이의 hello 장기적으로 다양 한 비즈니스 요구를 나타내고 다른 배포 및 사용량 패턴 있을 수 있습니다 이러한 시나리오를 예측 합니다.

### <a name="example-use-case-1-esmart-systems--overload-optimization"></a>사용 사례 예 1: eSmart 시스템 - 오버로드 최적화
중요 한 역할을 [스마트 그리드](https://en.wikipedia.org/wiki/Smart_grid) toodynamically의 지속적으로 최적화 및 사용량 패턴을 변경 하는 hello에 대 한 조정 합니다. 전력 소비량은 주로 온도 변화로 인한 장기 변동의 영향을 받을 수 있습니다(*예:*냉방 또는 난방에 많은 전력이 사용됨). At hello 동일한 시간, 전원 소비 장기적 추세의 영향도 받습니다. 여기에는 계절성 효과, 국경일, 장기 소비량 증가 및 소비자 지수, 유가 및 GDP와 같은 경제적 요인도 포함될 수 있습니다.

이 사용 사례에 [eSmart](http://www.esmartsystems.com/) hello 눈금의 지정 된 모든 변전소에 오버 로드 상황 예측 hello 경향은 수 있게 하는 클라우드 기반 toodeploy 솔루션 려 합니다. 특히, eSmart 되므로 가능성이 toooverload hello 내에서 다음 시간 즉각적인 조치 tooavoid 될 수 있으며 또는 해당 상황이 해결 tooidentify substations 필요 합니다.

정확하고 신속한 예측 수행을 위해서는 세 가지 예측 모델을 구현해야 합니다.

* 사용 하도록 설정 하는 동안 각 변전소의 전력 소비량 예측 하는 hello 다음 몇 주 또는 월 긴 용어 모델
* 단기 모델로 hello 다음 시간 동안 특정된 변전소에 오버 로드 상황의 예측을 사용 하 여
* 여러 시나리오에 대해 향후 온도 예측을 제공하는 온도 모델

hello hello 장기 모델의 목적은 (전원 전송 용량 제공)의 경향은 toooverload 여 toorank hello substations hello 다음 주 또는 월 중입니다. 따라서 hello hello 단기 예측에 대 한 입력으로 부합할 substations의 짧은 목록을 만들을 수 있습니다. 필요 tooconstantly 생성 다중 시나리오 온도 예측 및 toohello 장기 모델에 대 한 입력으로 해당 피드는 온도 hello 장기 모델에 대 한 중요 한 예측자는 그대로 있습니다. 그런 다음 호출 hello 단기 예측 toopredict 어떤 변전소 가능성이 toooverload hello를 통해 다음 시간입니다.

hello 단기 및 장기 모델은 각 변전소 당 개별적으로 배포 됩니다. 따라서 이러한 모델의 실제 실행 hello 광범위 한 오케스트레이션이 필요합니다. hello 단기적으로는 더 세분화 된 모델에 더 높은 예측 정확도 toogain hello 각 시간에 대 한 전용입니다. 이러한 모든 모델 1 시간 마다 실행 되는 몇 분 tooallow 충분 한 시간 toorespond 내에 실행 완료 필요한 경우 예방 조치를 수행 합니다. 모델의이 컬렉션 정기 간행물 재교육 hello 가장 최근 데이터를 사용 하 여 최신 상태로 유지 됩니다.

이 사용 사례에 대한 자세한 내용은 [여기](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18945)에 있습니다.

#### <a name="use-case-qualification-criteria--prerequisites"></a>사용 사례 자격 조건 - 필수 구성 요소
hello 주 Cortana Intelligence의 강도가 강력한 능력 toodeploy 및 배율 컴퓨터 학습 중심 솔루션입니다. 동시에 실행 되는 예측 toosupport 수천 디자인 된 경우 Toomeet 변경 사용 패턴을 자동으로 축소할 수 있는 합니다. 따라서 솔루션의 초점은 정확도와 컴퓨팅 성능에 있습니다. 예를 들어 유틸리티 회사는 정확한 에너지 요청 hello 각 시간 및 hello 다음 시간에 대 한 예측을 생성 합니다. 다른 손 hello, 이유 hello 사용량이 예측된 toobe 이므로의 hello 질문 답변을 얻는 데 필요한 덜 (hello 모델 자체에서 자동으로 처리 하는).

따라서 모든 사용 사례 및 비즈니스 문제 효과적으로 해결할 수 기계 학습을 사용 하 여 중요 한 toorealize 버전이 있습니다.

Cortana 인텔리전스 및 기계 학습 hello 다음 조건을 충족 하는 경우 특정된 비즈니스 문제를 해결 하는 데 매우 유용 수 있습니다.

* hello 손에 비즈니스 문제는 **예측** 본질적으로 합니다. 예측 사용 사례 예제는 hello 다음 시간 동안 특정된 변전소에 toopredict 전원 로드 하는 유틸리티. Hello 반면에, 분석 하 고 기록 사용량이 드라이버 순위 것 **설명** 본질적으로 및 덜 적용할 수 있습니다.
* 확실 **작업 경로의** hello 예측 한 번 수행 toobe를 사용할 수 있습니다. 예를 들어 hello 다음 시간 동안에 변전소 오버 로드를 예측 해당 변전소와 연결 된 부하를 줄이고 잠재적으로 오버 로드를 방지의 자동 관리 작업을 트리거할 수 있습니다.
* hello 사용 사례를 나타냅니다는 **문제의 일반적인 유형을** 되도록 해결 면 hello 방식으로 toosolving 유사한 다른 사용 사례 pave 수 있습니다.
* hello 고객을 설정할 수 **양적 예측과 질적 목표** toodemonstrate 성공적인 솔루션 구현 합니다. 예를 들어 에너지 수요 예측에 대 한 적절 한 정량 목표 hello 필요한 정확도 임계값 것 (*예:*, too5를 %에 구문 오류가 ï ´ ù) 변전소 오버 로드 후 hello 정밀도 (참 긍정 속도)을 예측 하는 경우 또는 및 회수 (참 긍정 익스텐트) 지정된 된 임계값 이상 이어야 합니다. 이러한 목표 hello 고객의 비즈니스 목표에서 파생 되어야 합니다.
* 확실 **통합 시나리오** hello 회사의 비즈니스 워크플로 사용 합니다. 예를 들어 hello 변전소 부하 예측 hello 그리드 컨트롤 센터 tooallow 오버 로드 방지 활동에 통합할 수 있습니다.
* hello 고객에 게 준비 toouse **충분 한 품질을 사용 하 여 데이터** toosupport hello 사용 사례 (hello 다음 섹션에서 더 많은 **데이터 품질**,이 플레이 북의).
* 고객 포옹 클라우드 중심이 데이터 아키텍처 hello 또는 **클라우드 기반 기계 학습**, Azure 기계 학습 및 기타 Cortana Intelligence 제품군 구성 요소를 포함 합니다.
* hello 고객은 감수할 tooestablish **끝 tooend 데이터 흐름** 시설 hello를 지속적으로 hello 클라우드로 데이터를 전달 하 고이 너무**운영 화** hello 솔루션입니다.
* hello 고객이 너무**전용 리소스** toohello 고객 성공 시 전송 되는 수 고 hello 초기 파일럿 구현 하는 동안 지식과 hello 솔루션의 소유권 될 수 있도록 완료 합니다.
* hello 고객 리소스가 있어야는 **숙련 된 데이터 전문가**가급적, 데이터 과학자입니다.

크게 hello 위의 조건에 따라 사용 사례의 자격 사용 사례의 hello 성공률 개선 하 고 나중에 사용할 사례의 hello 구현에 대 한 좋은 beachhead 연결할 수 있습니다.

### <a name="cloud-based-solutions"></a>클라우드 기반 솔루션
Azure에서 Cortana 인텔리전스 Suite는 hello 클라우드에 상주 하는 통합된 환경입니다. 클라우드 환경에서 고급 분석 솔루션의 hello 배포 비즈니스에 대 한 상당한 도움을 보유 하 고 hello에 동시 의미할 수 있습니다. 회사에 대 한 중요 한 변화를 계속 사용 하 여 온-프레미스 IT 솔루션. Hello 에너지 섹터 내 hello 클라우드로 작업 하는 점진적 마이그레이션의 명확한 추세가 있습니다. 이 추세 밀접 하 hello 스마트 눈금의 hello 개발 함께, 위에서 설명한 것 처럼 **산업 동향**합니다. 이 플레이 북 hello 에너지 도메인에는 클라우드 기반 솔루션에 초점 때 중요 한 tooexplain hello 이점 및 기타 고려 사항 클라우드 기반 솔루션을 배포 합니다.

Hello는 클라우드 기반 솔루션의 가장 큰 장점은 가장 hello 비용입니다. 솔루션은 클라우드 배포 구성 요소를 활용하므로 이와 관련된 사전 투자 비용 또는 매출원가(COGS) 구성 요소 비용이 없습니다. 즉, 하드웨어, 소프트웨어 및 IT 유지 관리에 필요한 tooinvest 없습니다는 비즈니스 위험은 크게 감소 이므로 합니다.

또 다른 중요 한 이점은 클라우드 기반 솔루션의 hello 종 량 제 비용 구조입니다. 계산 또는 저장소용 클라우드 기반 서버는 필요에 따라 배포 및 확장할 수 있습니다. 클라우드 기반 솔루션의 비용 효율성 이점은 hello를 나타냅니다.

마지막으로,이 모든가 hello 클라우드 기반 제품은의 일부가 IT 유지 관리 또는 인프라 이후 개발에 투자에 대 한 않아도가 됩니다. toothat 범위 내에서 Cortana Intelligence Suite hello 가장 및에 포함 됩니다 클래스 서비스는도 지도 진화 유지 합니다. 새로운 기능, 구성 요소 및 기능이 지속적으로 도입되고 개발되고 있습니다.

Hello 클라우드 전환을 시작 되는 회사를 권장 하는 매우 tootake 단계적 접근 방식을 클라우드 마이그레이션도로 지도 구현 하 여 합니다. 유틸리티 및 hello 에너지 도메인에 있는 회사에 대 한이 플레이 북에 설명 된 hello 사용 사례 나타낼 수 있는 기회가 hello 클라우드에서 예측 분석 솔루션 파일럿에 대 한 것으로 생각 합니다.

#### <a name="business-case-justification-considerations"></a>비즈니스 사례 근거 고려 사항
대부분의 경우에서 hello 고객 클라우드 기반 솔루션 및 기계 학습은 중요 한 구성 요소는 지정 된 사용 사례에 대 한 사유를 만들 때의 관심을 가질 수 있습니다. 온-프레미스 솔루션은 클라우드 기반 솔루션의 hello 경우에서와 달리 hello 선불 비용이 발생 하지 구성 요소는 무시할 수 있으며 hello 비용 요소 대부분이 실제 사용와 연결 합니다. Cortana 인텔리전스 Suite에는 솔루션을 예측 하는 에너지 toodeploying 있어 여러 서비스는 단일 공용 비용 구조와 통합할 수 있습니다. 예를 들어 데이터베이스 (*예:*, SQL Azure) 사용된 toostore hello 원시 데이터 수 있으며 다음 Azure 기계 학습을 예측 하는 실제 hello에 대 한이 사용 되는 toohost hello 예측 서비스입니다. 이 예제에서는 저장소 및 트랜잭션 구성 요소 비용 구조 hello 포함 됩니다.

Hello에 다른 손 하나 있어야 (단어 짧거나 깁니다)을 예측 한 에너지 요청 운영 hello 비즈니스 가치를 잘 알게 합니다. 사실, 각 예측된 작업의 중요 한 toorealize hello 비즈니스 값입니다. 예를 들어 정확 하 게 hello에 대 한 전원 부하 다음 24 시간을 예측 수 overproduction hello 그리드에서 오버 로드를 방지할 수 있습니다 및 매일 재무 절감 측면에서 한정 될이 있습니다.

솔루션은 수 사용량이 hello 재무 혜택을 계산 하기 위한 기본 수식은 예측: ![hello 재무 혜택 요구를 계산 하기 위한 기본 식은 예측 솔루션](media/cortana-analytics-playbook-demand-forecasting-energy/financial-benefit-formula.png)

종 량 제 가격 모델을 제공 하는 Cortana Intelligence Suite 이므로 고정된 비용 구성 요소 toothis 수식을 헤드 필요가 없습니다. 이 수식은 매일, 매월 또는 매년 단위로 계산할 수 있습니다.

현재 Cortana Intelligence Suite 및 Azure 기계 학습 가격 계획은 [여기](http://azure.microsoft.com/pricing/details/machine-learning/)에서 확인할 수 있습니다.

### <a name="solution-development-process"></a>솔루션 개발 프로세스
클라우드 기반 기술을 사용 하 여 hello 개발 주기의 예측 솔루션은 일반적으로 하기에 모두 4 단계를 포함 한 에너지 요청 및 내 서비스 hello Cortana 인텔리전스 Suite 합니다.

Hello 다이어그램을 다음에 설명 되어 있습니다.

![스마트 그리드 주기](media/cortana-analytics-playbook-demand-forecasting-energy/smart-grid-cycle.png)

다음 단락 뒤에 hello이 4 단계 프로세스를 설명 합니다.

1. **데이터 수집** – 모든 고급 분석 기반 솔루션은 데이터에 의존합니다(**데이터 이해** 참조). 특히, toopredictive 분석 및 예측를 때는 데이터의 지속적이 고 동적 흐름에 의존 합니다. 에너지 수요 예측의 hello 경우가이 데이터 스마트 미터에서 직접 기반 할 수 있습니다 또는 온-프레미스 데이터베이스에 이미 집계할 수 있습니다. 또한 날씨 및 온도와 같은 기타 외부 데이터 원본도 활용합니다. 이 지속적인 데이터 흐름은 오케스트레이션, 예약 및 저장되어야 합니다. [Azure 데이터 팩터리](http://azure.microsoft.com/services/data-factory/) (ADF)는 이 작업을 완수하기 위한 주요 수단입니다.
2. **모델링** – 에너지를 정확 하 고 신뢰할 수 있는 예측에 대 한 하나 해야 개발 (학습) 하는 좋은 모델 hello 기록 데이터의 사용 및 추출 hello를 의미 있는 유지 관리 하 고 예측 패턴에서 hello 데이터입니다. hello 영역 컴퓨터 학습 (ML)의 고급 알고리즘을 정기적으로 개발 되 고 사용 하 여 신속 하 게 증가 했습니다. Azure 기계 학습 스튜디오에는 hello 가장 고급 작업을 완료 흐름 내에서 기계 학습 알고리즘을 활용 하는 데 도움이 되는 뛰어난 사용자 환경을 제공 합니다. 해당 워크플로의 직관적인 흐름 다이어그램에서 설명 하 고 hello 데이터 준비, 기능 추출, 모델링 및 모델 평가 포함 합니다. hello 사용자는이 환경에 포함 된 다양 한 모델의 수가 수백 개에 가져올 수 있습니다. 이 단계의 hello 끝으로 데이터 과학자는 완벽 하 게 평가 및 배포에 대 한 준비 작업 모델을 적용 됩니다.
   
   hello 다음 다이어그램은 일반적인 워크플로 보여 줍니다.
   
   ![모델링 워크플로](media/cortana-analytics-playbook-demand-forecasting-energy/modeling-workflow.png)
3. **배포** – 작업 모델을 사용 하 여 손에 hello 다음 단계는 배포 합니다. 여기에서 다양 한 소비 클라이언트 hello 인터넷을 통해 동시에 호출할 수 있는 RESTful API를 노출 하는 웹 서비스 hello 모델 변환 됩니다. Azure ML 단추를 클릭 한 번으로 hello Azure 기계 학습 스튜디오에서 직접 모델을 배포 하는 간단한 방법을 제공 합니다. hello 전체 배포 프로세스 hello 내부적 수행합니다. 이 솔루션에 필요한 hello 소비 toomeet 확장할 자동으로 수 있습니다.
4. **소비** –이 단계에서는 실제로 하도록 tooproduce 예측 모델을 예측 하는 hello를 사용 합니다. hello 소비 사용자 응용 프로그램에서 구동 될 수 있습니다 (*예:*, 대시보드) 하거나 직접와 같은 운영 시스템에서 요청/분산 시스템 또는 그리드 최적화 솔루션입니다. 여러 사용 사례가 단일 모델에서 구동될 수 있습니다.

## <a name="data-understanding"></a>데이터 이해
Hello 비즈니스 고려 사항을 다루는 후 (참조 **비즈니스 이해**) 준비 toodiscuss hello 데이터 파트 이제는 솔루션을 예측 한 에너지 요청입니다. 모든 예측 분석 솔루션은 신뢰할 수 있는 데이터에 의존합니다. 에너지 수요 예측을 위해 다양한 수준의 세분성을 지닌 과거 소비량 데이터에 의존합니다. 해당 기록 데이터는 hello 원자재도 사용 됩니다. 분석이 수행 됩니다는 신중 하 게는 hello 데이터 과학자 결국를 생성 하는 데 필요한 hello 예측 모델에 적용할 수 있는 예측자 (기능 참조 tooas도 함)를 식별 합니다.

이 섹션의 나머지에서는 hello을 설명 합니다 다양 한 단계 및 고려 사항은 hello 데이터를 이해 하는 데 hello와 방법을 toobring 것 tooa 사용 하기 쉬운 형식입니다.

### <a name="hello-model-development-cycle"></a>hello 모델 개발 주기
적절한 예측 모델을 생성하려면 몇 가지 세심한 준비와 계획이 필요합니다. 여러 단계로 프로세스를 모델링 하 고 한 번에 한 단계에 중점을 두기 hello 세분화 hello 전체 프로세스의 hello 결과 크게 향상 시킬 수 없습니다.

hello 다음 다이어그램에서는 방법을 모델링 프로세스 hello 세분화 될 수는 여러 단계로 수행 합니다.

![모델 개발 주기](media/cortana-analytics-playbook-demand-forecasting-energy/model-development-cycle.png)

마찬가지로 hello 주기는 6 개의 단계로 구성 됩니다. 알 수 있습니다.

* 문제 공식화
* 데이터 수집 및 데이터 탐색
* 데이터 준비 및 기능 엔지니어링
* 모델링
* 모델 평가
* 개발

이 섹션의 나머지 부분 hello hello 개별 단계와 항목이 tooconsider 각 단계에서 설명 합니다.

### <a name="problem-formulation"></a>문제 공식화
Hello 가장 중요 한 단계 1 요구 사항에 맞춰 tootake 이전 tooimplementing 모든 예측 분석 솔루션 hello 문제 공식화를 고려할 수 있습니다. 변환 여기는 비즈니스 문제를 hello 및 모델링 기법 및 데이터를 사용 하 여 해결할 수는 요소는 toospecific 분해 합니다. 좋습니다 tooformulate hello 문제 tooanswer 일련의 질문으로 싶습니다. 다음은 에너지 수요 예측의 hello 범위 내에서 적용할 수 있는 몇 가지 가능한 질문입니다.

* 개별 변전소 다음 시간 또는 일 hello에 대 한 예상 hello 부하 이란?
* Hello 일 어떤 시간에 내 눈금에 직면할 최대 수요?
* 내 눈금 toosustain hello 예상 최대 부하는 될 가능성이?
* Hello 전원 스테이션에서 hello 각 시간 동안 전력이 얼마나 생성 되어야 하나요?

이러한 질문을 작성 하는 작업 toofocus를 hello 적절 한 데이터를 가져오고 당면한 비즈니스 문제 hello에 완벽 하 게 정렬 되는 솔루션 구현에 있습니다. 또한 hello 모델의 tooevaluate hello 성능을 수 있는 몇 가지 주요 메트릭을 설정할 수 있습니다. 예를 들어 정확도 해야 hello 예측 수 및 hello 다양 한 오류 여전히 hello 비즈니스에서 허용 되는 무엇입니까?

### <a name="data-sources"></a>데이터 원본
최신 스마트 그리드 hello 다양 한 부분 및 hello 눈금의 구성 요소에서 데이터를 수집합니다. 이 데이터는 hello 작업의 다양 한 측면 및 hello 전원 눈금의 hello 사용률을 나타냅니다. Hello 에너지 수요 예측의 hello 범위 내에서 hello 토론 hello 실제 수요 소비를 반영 하는 데이터 원본에 대해을 제한 됩니다. 한 가지 중요한 에너지 소비량 원본은 스마트 측정기입니다. Hello 전 세계 유틸리티 소비자에 대 한 스마트 미터 신속 하 게 배포 합니다. 스마트 미터 hello 실제 전원 소비를 기록 하 고 지속적으로이 데이터 백 toohello 유틸리티 회사를 릴레이 합니다. 데이터 수집 되 고 매 5 분 too1 시간에서 사이의 고정된 된 간격에 다시 전송 합니다. 더 많은 고급 스마트 미터를 원격으로 프로그래밍할 수와 비율을 toocontrol hello 가계 내에서 실제로 사용 합니다. 스마트 측정기 데이터는 비교적 신뢰할 수 있으며 타임스탬프를 포함합니다. 따라서 수요 예측에 중요한 요소입니다. Hello 그리드 토폴로지 내에서 다양 한 수준에서 데이터를 측정기 (합계) 집계할 수: transformer, 변전소, 지역, *등*합니다. 그런 다음 선택할 수 hello 필요한 집계 수준 toobuild 예측 모델에 대 한 합니다. 예를 들어 로드 하는 경우 hello 유틸리티 회사는 향후 tooforecast와 같은 각 해당 그리드 substations 다음 모든 미터 데이터 수 각 개별 변전소에 대해 집계 됨 있고 모델을 예측 하는 hello에 대 한 입력으로 사용 합니다. 내부 데이터 원본으로 toosmart 미터 이라고합니다.

신뢰할 수 있는 에너지 수요 예측은 다른 외부 데이터 원본에 따라서도 좌우됩니다. 전력 소비에 영향을 주는 가지 중요 한 요소에 hello 날씨 인지 hello 온도 보다 정확 하 게 합니다. 과거 데이터는 외부 온도와 전력 소비량 간의 강력한 상관 관계를 보여 줍니다. 소비자에 게 확인 핫 여름 기간 동안 해당 에어컨의 및 hello 겨울 전원을 시스템이 열 켜는 동안의 사용 합니다. Hello 눈금 위치에 기록 temperatures 신뢰할 수 있는 소스는 따라서 키. 또한 전력 소비량의 예측 변수로 온도의 정확한 예측을 사용합니다.

다른 외부 데이터 원본도 에너지 수요 예측 모델을 구축하는 데 도움이 될 수 있습니다. 여기에는 장기 기후 변동, 경제 지수(*예:*GDP) 등이 포함될 수 있습니다. 이 문서에서는 이러한 다른 데이터 원본은 포함하지 않습니다.

### <a name="data-structure"></a>데이터 구조
한 후 데이터 원본 필수 hello 식별, 우리는 tooensure hello 수집 된 원시 데이터에 포함 되어 있는지와 같은 수정할 데이터 기능. 모델을 예측 하는 신뢰할 수 있는 요청 toobuild는 수집 된 데이터를 hello tooensure hello 향후 수요를 예측 하는 데 도움이 되는 데이터 요소를 포함 합니다. 다음은 hello hello 원시 데이터의 데이터 구조 (스키마)와 관련 된 몇 가지 기본 요구 사항입니다.

hello 원시 데이터 행과 열으로 이루어져 있습니다. 각 측정은 데이터의 단일 행으로 표시됩니다. 데이터의 각 행에 여러 개의 열 (참조 tooas 기능도 또는 필드)에 포함 됩니다.

1. **타임 스탬프** – hello 타임 스탬프 필드 hello 실제 시간 hello 측정 된 기록 하는 시간을 나타냅니다. Hello 일반 날짜/시간 형식 중 하나가 지정 된 것을 따라야 합니다. 날짜와 시간 부분 모두 포함해야 합니다. 대부분의 경우에서 필요는 없습니다 hello 시간 toobe까지 기록에 대 한 두 번째 수준의 세분성 hello 합니다. 사용 하는 중요 한 toospecify hello 시간 영역 hello 데이터가 기록 됩니다.
2. **ID 미터링** -이 필드는 hello 미터 또는 hello 측정 장치 식별. 범주 변수이며 문자와 숫자 조합을 사용할 수 있습니다.
3. **소비 값** – 지정된 된 날짜/시간에 실제로 사용 hello입니다. hello 소비량을 kwh (와트) 측정할 수 있습니다 또는 다른 기본 단위입니다. hello 데이터의 모든 측정 단위에서 일관 된 측정 단위 hello toonote 유지 해야 합니다. 경우에 따라 소비량은 3개의 전원 단계를 통해 공급될 수 있습니다. 이 경우이 필요 합니다 toocollect 모든 hello 독립 소비 단계입니다.
4. **온도** – hello 온도 독립적인 소스에서 일반적으로 수집 합니다. 그러나 hello 소비 데이터와 호환 되어야 합니다. 타임 스탬프 위에 설명 된 대로 수행할 수 있게 하는 다음을 포함 해야 toobe hello 실제 소비 데이터와 동기화 합니다. hello 온도 값도 표시할지 화씨 지정할 수 있지만 모든 측정 단위에서 일관 된 상태를 유지 해야 합니다.
5. **위치 –** hello 위치 필드는 일반적으로 hello 온도 데이터를 수집한 hello 위치와 연결 합니다. 우편 번호 또는 위도/경도(lat/long) 형식으로 나타낼 수 있습니다.

다음 표에서 hello 적합 한 소비와 온도 데이터 형식 예를 보여 줍니다.

| **Date** | **Time** | **측정기 ID** | **1단계** | **2단계** | **3단계** |
| --- | --- | --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |ABC1234 |7.0 |2.1 |5.3 |
| 7/1/2015 |10:00:01 |ABC1234 |7.1 |2.2 |4.3. |
| 7/1/2015 |10:00:02 |ABC1234 |6.0 |2.1 |4.0 |

| **Date** | **Time** | **위치** | **온도** |
| --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |11242 |24.4 |
| 7/1/2015 |10:00:01 |11242 |24.4 |
| 7/1/2015 |10:00:02 |11242 |24.5 |

위에서 볼 수 있듯이 이 예에서는 3개의 전원 단계와 관련된 소비량에 대해 3개의 다른 값을 포함합니다. 그러나 또한 결합 하려면 하나의 열으로 hello 날짜 및 시간 필드 구분 됩니다 note 또한 합니다. 이 경우 hello 위치 열은 5 자리 우편 번호 형식 및도 섭씨 형식에서 hello 온도에 표시 됩니다.

### <a name="data-format"></a>데이터 형식
Cortana 인텔리전스 Suite hello CSV, TSV, JSON와 같은 가장 일반적인 데이터 형식을 지원할 수 있습니다 *등*합니다. hello 프로젝트의 전체 수명 주기 hello에 대 한 해당 hello 데이터 형식을 일관성 있게 유지 합니다.

### <a name="data-ingestion"></a>데이터 수집
에너지 수요 예측을 지속적으로 및 자주 예측할 이후 hello 원시 데이터 단색 하 고 안정적인 데이터 수집 프로세스를 통해 전달 되는지 확인 해야 합니다. hello 수집 프로세스 hello 원시 데이터를 예측 프로세스 hello 필요 시 hello에 대 한 사용할 수 있는지를 보장 해야 합니다. 의미 hello 데이터 수집 빈도 hello 예측 빈도 보다 커야 합니다.

예를 들어: 솔루션은 매일 오전 8 시에 새 예측을 생성 한 후 해야 하는 동안 수집 된 모든 hello 데이터 마지막 hello tooensure 예측 우리의 필요 시 24 시간에 되었습니다 완벽 하 게 수집 된 해당 지점까지 및 tooeven hello를 포함 합니다. 데이터의 마지막 시간입니다.

이 tooaccomplish 주문에서 Cortana 인텔리전스 Suite는 신뢰할 수 있는 데이터 수집 프로세스를 다양 한 방법으로 toosupport을 제공 합니다. 이 수에 대해 자세히 설명 hello **배포** 이 문서의 섹션.

### <a name="data-quality"></a>데이터 품질
안정적이 고 정확한 수요 예측을 수행 하는 데 필요한 hello 원시 데이터 원본에는 몇 가지 기본 데이터 품질 기준 충족 해야 합니다. 고급 통계 방법을 사용 하는 toocompensate 몇 가지 가능한 데이터 품질 문제에 대 한를 사용할 수 있지만 새 데이터를 수집 하는 경우 몇 가지 기본 데이터 품질 임계값을 교차는 म tooensure 여전히 필요 합니다. 원시 데이터 품질에 관한 몇 가지 고려 사항은 다음과 같습니다.

* **누락 값** – 이것은 toohello 상황 때의 특정 값을 수집 되지 않았습니다. hello을 기본 요구 사항은 여기 해당 hello 누락 값 비율 안 10% 보다 큰 모든 주어진된 시간 간격에 대 한 합니다. 단일 값이 누락된 경우 '0'이 아닌, 유효한 측정값일 수 있는 미리 정의된 값(예: '9999')을 사용하여 표시해야 합니다.
* **정확도 측정** – 소비 또는 온도의 hello 실제 값을 정확 하 게 기록해 야 합니다. 정확하지 않은 측정값은 정확하지 않은 예측을 생성합니다. 일반적으로 hello 측정 오류는 %1 상대 toohello true 값 보다 작아야 합니다.
* **측정 시간** – 필요한 hello 데이터 수집의 해당 hello 실제 타임 스탬프 hello 실제 측정 상대 toohello 실제로 시간 10 초 보다 더 사양과 되지 것입니다.
* **동기화** - 여러 데이터 원본을 사용하는 경우(*예:*소비량 및 온도) 이들 간에 시간 동기화 문제가 없는지 확인해야 합니다. 따라서 해당 hello 시간 차이 두 개의 독립적인 데이터 원본에서 수집 하는 hello 타임 스탬프 10 초 이상 초과 하지 않아야 합니다.
* **대기 시간** - 위에서 설명한 것처럼 **데이터 수집**에서 신뢰할 수 있는 데이터 흐름 및 수집 프로세스에 의존합니다. toocontrol는 hello 데이터 대기 시간을 제어 म 확인 해야 합니다. 이 hello 실제 측정 하는 hello 시간과는 hello Cortana Intelligence Suite 저장소에 로드 되 고 사용할 준비가 되었는지 hello 시간 사이의 시간 차이 hello로 지정 됩니다. 단기 부하에 대 한 예측 hello 총 대기 시간 해야 30 분 보다 클 수 없습니다. 장기 부하에 대 한 예측 hello 총 대기 시간 해야 1 일 보다 클 수 없습니다.

### <a name="data-preparation-and-feature-engineering"></a>데이터 준비 및 기능 엔지니어링
Hello 원시 데이터에 되어 수집 된 후 (참조 **데이터 수집**) 안전 하 게 되었습니다 준비 toobe 처리는 저장 합니다. hello 데이터 정리는 기본적으로 hello 원시 데이터를 가져와 및 변환 (변환, 모양 변경) hello 모델링 단계에 대 한 폼에 넣습니다. 와 같은 해당 실제 측정 된 값, 표준화 된 값, 보다 복잡 한 작업은 hello 원시 데이터 열을 사용 하 여와 같은 간단한 작업에 포함 될 수 있습니다는 [지연 시간](https://en.wikipedia.org/wiki/Lag_operator), 등입니다. 새로 만든 hello 데이터 열 참조 tooas 데이터 기능 및 이러한 생성 hello 과정은 참조 tooas 기능 엔지니어링 합니다. Hello 끝날 때이 프로세스에서는 것이 hello 원시 데이터에서 파생 된 및 모델링에 사용할 수 있는 새 데이터 집합입니다. 또한 hello 데이터 준비 단계의 필요한 누락 값 care of tootake (참조 **데이터 품질**)을 느리게 합니다. 일부 경우에도 모든 값에 나타나는 toonormalize hello 데이터 tooensure이 필요 합니다 hello 같은 눈금.

요구 사항을 보여 hello 에너지에 포함 된 hello 일반 데이터 기능 중 일부는이 섹션에서는 모델을 예측 합니다.

**시간 기반 기능과:** 이러한 기능은 hello 날짜/타임 스탬프 데이터에서 파생 됩니다. 이러한 기능은 추출되어 다음과 같은 범주 기능으로 변환됩니다.

* 시간 일-이 값을 0 too23 가져오고 있는 hello 날의 hello 시간
* 일의 주 –이 hello 요일 hello 나타내며 값 1 (일요일) too7 (토요일)을에서 가져오고
* 날짜의 월 – hello 실제 날짜를 나타내는이 및이 값 1 too31에서 사용할 수 있습니다
* 월 연도의 –이 hello 월 나타내며 값 1 (1 월) too12 (12 월)을에서 가져오고
* 주말 –이 주말에 대 한 평일 또는 1에 대 한 hello 값 0을 사용 하는 이진 값 기능
* 휴일-이 공휴일에 대 한 일반 하루 또는 1에 대 한 hello 값 0을 사용 하는 이진 값 기능
* 푸리에 용어 – 용어는 hello 타임 스탬프에서 파생 된 가중치 푸리에 hello 및 hello 데이터에 사용 되는 toocapture hello 계절성 (주기) 됩니다. 데이터에 여러 계절이 포함될 수 있으므로 푸리에 항을 곱해야 할 수 있습니다. 예를 들어 수요 값에는 3 푸리에 항이 발생하는 연간, 주별 및 일별 계절/주기가 포함될 수 있습니다.

**독립 측정 기능:** hello 독립 기능을 같은 toouse 예측자도 부문의 모든 hello 데이터 요소를 포함 합니다. 여기서는 hello 종속 기능을 제외 toopredict 합니다.

* Lag 기능 –이 시간을 향해 이동 hello 실제 수요의 값입니다. 예를 들어 지연 1 기능 hello (시간별 데이터 가정) 이전 시간 상대 toohello 현재 타임 스탬프에 hello 요청 값을 저장 합니다. 마찬가지로, 우리에 추가할 수 지연 2 3, 지연 *등*. hello 모델 결과 평가 하 여 hello 모델링 단계 과정에서 사용 되는 지연 기능의 hello 실제 조합을 결정 됩니다.
* 장기간 추세 –이 기능은 수요 년 간의 선형 증가 hello를 나타냅니다.

**종속 기능:** hello 종속 기능은 같은 hello 데이터 열이 모델 toopredict 합니다. 와 [기계 학습 감독](https://en.wikipedia.org/wiki/Supervised_learning), 먼저 모델을 학습 hello hello 종속 기능을 사용 하 여 (이 또한 참조 tooas 레이블) 해야 합니다. 이렇게 하면 종속 기능 hello와 관련 된 hello 데이터 hello 모델 toolearn hello 패턴이 있습니다. 에너지 수요 예측 일반적으로 toopredict hello 실제 수요 고 따라서 여기서 사용 하는 hello 종속 기능으로 합니다.

**누락 값 처리:** hello 데이터 준비 단계 toodetermine hello 가장 좋은 전략 toohandle 누락 값이 필요 합니다. 이 주로 수행를 사용 하 여 hello 다양 한 통계 [데이터 귀속 방식을](https://en.wikipedia.org/wiki/Imputation_\(statistics\))합니다. 에너지 수요 예측의 경우 hello에서는 일반적으로 돌립니다 누락 값을 이전 사용할 수 있는 데이터 요소에서 이동 평균을 사용 하 여 합니다.

**데이터 정규화:** 데이터 정규화에 사용 되는 toobring 유사한 규모를 예측 하는 요청 등의 모든 숫자 데이터는 변환의 형식이 있습니다. 일반적으로 모델 정확도 hello 및 정밀도 개선 이로써 있습니다. 일반적으로 할 경우 hello 실제 값 hello hello 데이터 범위를 나누어 합니다.
크기 조정 hello 원래 값-1과 1 사이의 일반적으로 더 작은 범위에 있습니다.

## <a name="modeling"></a>모델링
hello 모델링 단계를 모델로 hello 데이터의 hello 변환이 이루어지는입니다. Hello에 있는이 프로세스의 핵심 고급 hello 기록 데이터 (학습 데이터)를 검색 패턴을 추출 하 고, 모델을 작성 하는 알고리즘입니다. 해당 모델 나중에 사용 되는 toobuild hello 모델 되지 않은 새 데이터에 사용 되는 toopredict 될 수 있습니다.

신뢰할 수 있는 작동 하는 상태 모델 tooscore 새 데이터는 구조화 된 tooinclude hello를 사용한 다음 수 필수 기능 (X). hello 지속형된 모델 (hello 교육 단계에서 사용 하는 개체)을 사용 하 고 hello 대상 변수 Ŷ로 표시 되는 예측 평가 프로세스 hello 하면 있습니다.

### <a name="demand-forecasting-modeling-techniques"></a>수요 예측 모델링 기법
Hello 경우 요청 하도록 예측의 시간으로 정렬 되는 기록 데이터를 사용 합니다. 일반적으로 hello 시간 차원으로 포함 된 toodata 이라고 [시계열](https://en.wikipedia.org/wiki/Time_series)합니다. 시계열 모델링과 toofind 시간 관련 시간에서 hello 목표 추세, 계절성, 자동-상관 관계 (시간별) 및 이러한 모델을 작성 합니다.

최근 몇 년 동안 고급 알고리즘으로 개발 된 tooaccommodate 시계열 예측 및 예측 정확도 tooimprove 했습니다. 여기에서 몇 가지 알고리즘을 간단히 다루겠습니다.

> [!NOTE]
> 이 섹션은 의도 한 toobe 수요 예측에 대 한 일반적으로 사용 되는 기술을 모델링의 간략 한 설문 조사 대신 학습 및 예측 개요 컴퓨터 아니라 없습니다. 자세한 내용과 시계열 예측에 대 한 교육 자료 좋습니다 hello 책 [Forecasting: 원칙 및 사례](https://www.otexts.org/book/fpp)합니다.
> 
> 

#### <a name="ma-moving-averagehttpswwwotextsorgfpp62"></a>[**MA(이동 평균)**](https://www.otexts.org/fpp/6/2)
이동 평균 하나 hello 첫 번째 분석 하는 방법 시계열 예측에 사용 된 이며 오늘 가장 일반적으로 사용 하는 hello 기술 중 하나는 여전히 합니다. 이기도 hello foundation에 대 한 고급 기법을 예측 합니다. 이동 평균이 있는 K의 이동 평균 hello hello 순서를 표시 하는 여기서 hello K 가장 최근의 지점 통한 평균을 구하여 hello 다음 데이터 요소를 예측는 했습니다.

hello 이동 평균 기술을 hello 영향을 예측 하는 hello 다듬기 않으며 hello 데이터의 잘 큰 변동성을 처리 하지 않을 수 있습니다.

#### <a name="ets-exponential-smoothinghttpswwwotextsorgfpp75"></a>[**ETS(지수 평활법)**](https://www.otexts.org/fpp/7/5)
지 수 다듬기 ETS ()는 제품군의 다양 한 메서드는 값은 작업의 최근 데이터 요소 순서 toopredict hello 다음 데이터 요소에 사용 합니다. hello 아이디어 tooassign 보다 높은 가중치 toomore 최근 값 이며 점진적으로 이전 측정 된 값에 대 한이 무게를 줄입니다. 다양 한 방법이 제품군의 여러 가지, 그 중 일부만 포함 hello 데이터의 계절성 처리와 같은 [Holt Winters 계절별 메서드](https://www.otexts.org/fpp/7/5)합니다.

이러한 메서드의 일부 hello 데이터의 계절성 hello에에서도 계산 합니다.

#### <a name="arima-auto-regression-integrated-moving-averagehttpswwwotextsorgfpp8"></a>[**ARIMA(자동 회귀 통합 이동 평균)**](https://www.otexts.org/fpp/8)
ARIMA(자동 회귀 통합 이동 평균)는 시계열 예측에 일반적으로 사용되는 메서드의 또 다른 제품군입니다. 실질적으로 자동 회귀 메서드를 이동 평균과 결합합니다. 자동 회귀 방법은 이전 시계열 값 순서 toocompute hello 다음 날짜 지점 작성 하 여 회귀 모델을 사용 합니다. ARIMA 방식 등이 포함 된 데이터 요소 간의 hello 차이 계산 하는 hello 원래 측정 된 값 대신 사용 하 여 차이점 보관용 메서드를도 적용 됩니다. 마지막으로, ARIMA도 활용 hello 위에서 설명한 평균 기법을 이동 합니다. 다양 한 방법으로 이러한 메서드의 모든의 hello 조합이 있는 구조체 hello ARIMA 메서드의 제품군입니다.

오늘날, ETS 및 ARIMA는 에너지 수요 예측 및 다른 많은 예측 문제에 널리 사용되고 있습니다. 대부분의 경우에서 이러한 위해 결합 toodeliver 매우 정확한 결과입니다.

**일반 다중 회귀** 회귀 모델에는 hello 가장 중요 한 기계 학습 및 통계 hello 도메인 내에서 모델링 접근 방식을 수 있습니다. 시계열의 hello 컨텍스트에서 회귀 toopredict hello 미래 값을 사용 (*예:*, 수요의). 회귀에서는 hello 예측자의 선형 조합을 사용할 하 고 hello 학습 프로세스 중 한 이러한 예측자 hello 가중치 (또한 참조 tooas 계수)에 대해 알아봅니다. hello 목표는 예측된 값을 예측 한 회귀선 tooproduce입니다. 회귀 메서드는 hello 대상 변수 숫자를 하 고 따라서 시계열 예측도 맞는 경우에 적합 합니다. [선형 회귀](https://en.wikipedia.org/wiki/Linear_regression)처럼 매우 단순한 회귀 모델부터 의사 결정 트리, [임의 포리스트](https://en.wikipedia.org/wiki/Random_forest), [신경망](https://en.wikipedia.org/wiki/Artificial_neural_network), 향상된 의사 결정 트리처럼 보다 고급 모델까지 광범위한 회귀 메서드가 있습니다.

에너지 요청 회귀 문제도 예측을 생성할 목록 hello 실제 수요 시계열 데이터를 온도 등의 외부 요소에 결합할 수 있는 데이터 기능을 선택 하는 유연성을 많이 있습니다. Hello 선택한 기능에 대 한 자세한 내용은 hello 엔지니어링 기능에에서 대해서는 설명 (참조 **데이터 준비 및 기능 엔지니어링**)이 플레이이 북의 섹션입니다.

구현 하 고 에너지 수요 예측 파일럿 배포에 대 한 경험을 발견 했습니다 hello Azure 기계 학습에서 사용할 수 있는 고급 회귀 모델은 tooproduce hello에 대 한 최상의 결과 만들 것을 사용 합니다.

## <a name="model-evaluation"></a>모델 평가
모델 평가 hello 내에서 중요 한 역할을 **모델 개발 주기**합니다. 이 단계에서 의견에 귀으로 hello 모델 및 실제 데이터와 함께 성능 유효성을 검사 합니다. Hello 단계를 모델링 하는 동안 hello 모델 학습에 대 한 hello 사용할 수 있는 데이터의 일부로 사용 합니다. Hello 평가 단계 hello 데이터 tootest hello 모델의 나머지 부분에서는 hello를 수행 합니다. 실질적으로 재구성 되었습니다 하 hello hello 학습 데이터 집합으로 동일한 기능을 포함 하는 hello 모델 새 데이터를 제공 하는 것은 의미 합니다. 그러나 hello 유효성 검사 과정에서는 hello 모델 toopredict hello 대상 변수를 사용 하 여 대신 hello 사용할 수 있는 대상 변수를 제공 합니다. 종종 모델 점수 매기기와 프로세스를 통해 toothis 이라고합니다. 다음는 hello true 대상 값과 비교는 스토리를 예측 hello를 사용 하 여 사용 합니다. hello 목적은 toomeasure 이며 hello 차이 hello 예측 및 hello true 값을 의미 hello 예측 오류를 최소화 합니다. Hello 오류 측정 정량화는 키 toofine 조정 hello 모델 같은 고 hello 오류 실제로 감소 하는지 여부를 확인 합니다. 미세 조정 hello 모델 hello 설정 프로세스를 제어 하는 모델 매개 변수를 수정 하거나 추가 하거나 데이터 기능을 제거 하 여 수행할 수 있습니다 (tooas 참조 [매개 변수 스윕](https://channel9.msdn.com/Blogs/Azure/Data-Science-Series-Building-an-Optimal-Model-With-Parameter-Sweep)). 실제로 모델링, hello 기능 엔지니어링 팀 간의 tooiterate 필요 하 고 수 tooreduce hello 오류 toohello 필요한 수준을 하는 때까지 여러 번 평가 단계 모델 수 있습니다는 것입니다.

Hello 예측 오류 0 만큼 안 됩니다 tooemphasis 모든 결과 완벽 하 게 예측할 수 있는 모델은 유용 합니다. 그러나 특정 크기의 오류는 hello 비즈니스 받아들일 수 있습니다. Hello 유효성 검사 프로세스 중 우리의 모델 예측 오류 hello는 수준 또는 수준 hello 비즈니스 허용 오차 보다 더 나은 tooensure를 하겠습니다. 따라서 것이 중요 tooset hello 수준의 hello hello 시작 시 hello 견딜 오류 hello 하는 동안 순환 **문제 공식화** 단계입니다.

### <a name="typical-evaluation-techniques"></a>일반적인 평가 기법
다양한 방법으로 예측 오차를 측정하고 정량화할 수 있습니다. 이 섹션에서는 살펴볼 것 hello 토론 평가 기술 관련 tootime 시리즈 및 관련 된 예측 에너지 요청입니다.

#### <a name="mapehttpsenwikipediaorgwikimeanabsolutepercentageerror"></a>[**MAPE**](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
MAPE는 절대 평균 백분율 오차(Mean Absolute Percentage Error)를 나타냅니다. MAPE와 각 예측된 지점 및 해당 포인트의 hello 실제 값 간의 hello 차이 계산는 것입니다. 에서는 다음 hello 차이 상대 toohello 실제 값의 hello 비율을 계산 하 여 hello 오류 요소당을 수량화 합니다. 마지막 단계에서는 이러한 값의 평균을 구합니다. hello 수학 MAPE에 사용 되는 공식은 hello 다음 다음과 같습니다.

![MAPE 수식](media/cortana-analytics-playbook-demand-forecasting-energy/mape-formula.png)
*여기서 A<sub>t</sub> hello 실제 값, F<sub>t</sub> 는 예측된 값 hello n은 hello 마감일을 예측 합니다.*

## <a name="deployment"></a>배포
Hello 모델링 단계를 파악 했으며 hello 모델 성능을 유효성이 검사 되 면 준비 toogo hello 배포 단계에 있습니다. 이 컨텍스트에서 배포 hello 고객 활성화 tooconsume hello 모델을 의미 큰 규모로를 실제 예측을 실행 하 여 합니다. 배포의 hello 개념은 Azure 기계 학습에서 키 주요 목표는 tooconstantly hello 데이터에서 hello 통찰력을 얻는 것과 반대로 toojust으로 예측을 호출 합니다. hello 배포 단계는 hello 일부 대규모에 소비 hello 모델 toobe 설정 위치입니다.

Hello 예측 에너지 요청의 컨텍스트 내에서 목표를 두고 새로운 데이터는 hello 모델에 사용할 수 있는 하 고 해당 hello 예상한 데이터 백 toohello 사용 중인 클라이언트에 전송 됩니다 tooinvoke 연속적이 고 정기적으로 예측을입니다.

### <a name="web-services-deployment"></a>웹 서비스 배포
hello 주 배포 가능한 문서 블록 Azure 기계 학습에서는 hello 웹 서비스입니다. 이 hello 클라우드에서 예측 모델의 hello 가장 효과적인 방법은 tooenable 소비 합니다. hello 웹 서비스는 hello 모델을 캡슐화 하 고 있는 마치 겠습니다는 [RESTful](http://www.restapitutorial.com/) API (응용 프로그래밍 인터페이스). hello API hello 다이어그램 아래에 설명 된 대로 클라이언트 코드의 일부로 사용할 수 있습니다.

![배포 및 소비 서비스](media/cortana-analytics-playbook-demand-forecasting-energy/web-service-deployment-and-consumption.png)

볼 수 있듯이 hello 웹 서비스 Cortana Intelligence Suite 클라우드 hello에 배포 되 고 해당 노출 된 REST API 끝점을 통해 호출할 수 있습니다. 다른 종류의 다양 한 도메인 간 클라이언트 hello 웹 API를 통해 hello 서비스를 동시에 호출할 수 있습니다. hello 웹 서비스 지원 수천 개의 동시 호출 또한 확장할 수 있습니다.

### <a name="a-typical-solution-architecture"></a>일반적인 솔루션 아키텍처
솔루션을 예측 한 에너지 요청을 배포할 때는 되 면 hello 예측 웹 서비스 및 hello 전체 데이터 흐름을 용이 하 게 하는 최종 tooend 솔루션 배포 연습 합니다. 시 hello 새 예측 호출한 toomake 있는지 hello 모델은 최신 데이터 기능을 통해 제공 됩니다.이 필요 합니다. 의미 해당 hello 새로 수집 된 원시 데이터는 지속적으로 수집 된 처리 되 고 어떤 hello 모델 작성에 설정 하는 hello 필요한 기능으로 변환 합니다. At hello 동일 time, 우리 있게 toomake hello 예상한 hello에 사용할 수 있는 데이터는 사용 중인 클라이언트를 종료 하려고 합니다. 아래 hello 다이어그램에는 예제 데이터 흐름 주기 (또는 데이터 파이프라인) 보여 줍니다.

![에너지 수요 예측 끝 tooEnd 데이터 흐름](media/cortana-analytics-playbook-demand-forecasting-energy/energy-demand-forecase-end-data-flow.png)

다음은 hello 에너지 수요 예측된 사이클의 일부로 발생 하는 hello 단계입니다.

1. 수백만 개의 배포된 데이터 측정기가 실시간으로 전력 소비량 데이터를 계속 생성합니다.
2. 이 데이터는 수집되어 클라우드 리포지토리(*예:*Azure Blob)에 업로드됩니다.
3. 처리 되기 전에 hello 원시 데이터는 집계 된 tooa 변전소 또는 hello 비즈니스에 정의 된 대로 국가별 수준입니다.
4. hello 기능 처리 (참조 **데이터 준비 및 처리 하는 기능**) 한 다음 작업 수행 및에 필요한 생성 hello 데이터 모델 학습 또는 점수 매기기 – hello 기능 집합 데이터는 데이터베이스에 저장 됩니다 (*예를 들어*, SQL Azure).
5. 다시 학습 하는 서비스는 hello 호출 toore 학습 hello 예측 모델 – hello 모델의 버전을 업데이트 하는 웹 서비스를 평가 하는 hello에서 사용할 수 있도록 유지 됩니다.
6. 웹 서비스를 평가 하는 hello 필요한 hello 예측된 주파수 적합 한 일정으로에서 호출 됩니다.
7. hello 예상한 데이터 hello 끝 소비 클라이언트에서 액세스할 수 있는 데이터베이스에 저장 됩니다.
8. hello 소비 클라이언트 hello 예측을 검색 하 고 hello 눈금에 다시 적용 한 필요한 hello 사용 사례에 따라 사용 합니다.

이 전체 주기는 완전 자동화 및 실행 하는 일정에 따라 중요 한 toonote 것 합니다. 이 데이터 주기의 hello 전체 오케스트레이션과 같은 도구를 사용 하 여 수행할 수 있습니다 [Azure Data Factory](http://azure.microsoft.com/services/data-factory/)합니다.

### <a name="end-tooend-deployment-architecture"></a>종료 tooEnd 배포 아키텍처
순서 toopractically에서 Cortana 인텔리전스에 대 한 에너지 수요 예측된 솔루션을 배포, tooensure hello 필수 구성 요소 설정 되며 올바르게 구성 해야 합니다.

hello 다음 다이어그램에서는 구현 하 고 위에서 설명한 hello 데이터 흐름 주기를 조정 하는 일반적인 Cortana Intelligence 기반 아키텍처 수행 합니다.

![종료 tooEnd 배포 아키텍처](media/cortana-analytics-playbook-demand-forecasting-energy/architecture.png)

Hello 구성 요소 및 hello 전체 아키텍처에 대 한 자세한 내용은 toohello 에너지 솔루션 템플릿을 참조 하십시오.

