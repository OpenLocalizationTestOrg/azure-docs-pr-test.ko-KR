---
title: "기계 학습을 사용 하 여 고객 변동 aaaAnalyzing | Microsoft Docs"
description: "고객 이탈을 분석하고 채점하는 통합 모델 개발에 대한 사례 연구"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: 1333ffe2-59b8-4f40-9be7-3bf1173fc38d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 070e6a2ebe4f2fe439a42ffe1a3fa9d6d3788d62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a>Azure 기계 학습을 사용하여 고객 이탈 분석
## <a name="overview"></a>개요
이 문서에서는 Azure Machine Learning을 사용하여 빌드된 고객 이탈 분석 프로젝트의 참조 구현을 제공합니다. 이 문서에서는 전체적는 산업 고객 변동 hello 문제를 해결 하는 데 관련 된 일반 모델에 설명 합니다. 또한 기계 학습을 사용 하 여 작성 된 모델을의 hello 정확도 측정 및 평가 이후 개발 하는 방법을 설명 합니다.  

### <a name="acknowledgements"></a>감사의 말
이 실험은 Microsoft의 수석 데이터 과학자인 Serge Berger와 이전 Microsoft Azure 기계 학습 제품 관리자인 Roger Barga가 개발하고 테스트했습니다. hello Azure 설명서 팀 감사 히 전문 지식을 바탕으로 인해 및에이 문서를 공유 해 주셔서 감사 합니다.

> [!NOTE]
> 이 실험에 사용 되는 hello 데이터에 공개적으로 사용할 수 없는 경우 변동 분석에 대 한 toobuild 기계 학습 모델 하는 방법의 예제를 보려면: [소매 변동 모델 템플릿](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) 에 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com/)
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-problem-of-customer-churn"></a>고객 변동 hello 문제
모든 enterprise 섹터 및 hello 소비자 시장에서 기업에는 변동와 toodeal이 되어 있습니다. 때때로 이탈이 지나치고 정책 의사 결정에 영향을 미칠 수도 있습니다. hello 전통적인 솔루션 toopredict 높은 경향은 churners 이며 캠페인, 마케팅 호텔 서비스를 통해 또는 특수 dispensations 적용 하 여 해당 요구를 해결 합니다. 이러한 접근 방식은 업계 tooindustry 뿐 한 업계 (예를 들어 telecommunications) 내에서 특정 소비자 클러스터 tooanother 에서도 달라질 수 있습니다.

hello 공통적으로 적용 기업 필요로 이러한 특별 한 고객 유지 노력 toominimize 한다는입니다. 따라서 자연 방법론 변동 hello 확률 모든 고객 tooscore 되 고 hello 상위 n 개 항목을 해결 합니다. hello 우수 고객 이윤이 가장 높은 것; hello 될 수 있습니다. 예를 들어 더 복잡 한 시나리오는 수익 함수 특수 분배 후보 hello 선택 하는 동안 사용 됩니다. 그러나 이러한 고려 사항은 변동 처리 하기 위한 hello 전체적인 전략의 일부입니다. 기업에는 또한 계정 위험 (및 관련 된 위험 허용 범위)에 tootake 사항이 hello 수준과 hello 개입 및 적당히 고객 조각화의 비용입니다.  

## <a name="industry-outlook-and-approaches"></a>업계 전망 및 접근법
정교한 이탈 처리는 성숙한 산업의 표시입니다. hello 전형적인 예로 hello telecommunications 업계 구독자가 공급자 tooanother에서 알려진된 toofrequently 스위치. 이 자발적인 이탈이 주된 관심사입니다. 또한 공급자 누적 많은 기술 자료에 대 한 *드라이버 변동*되는 hello 요소 드라이브 고객 tooswitch 해당 합니다.

예를 들어, 핸드셋 장치 원하는 hello 휴대폰 비즈니스의 변동의 잘 알려진 드라이버. 결과적으로, 인기 있는 정책에는 새 구독자 및 전체 가격 tooexisting 업그레이드에 대 한 고객 청구에 대 한 송수화기의 toosubsidize hello 가격입니다. 지금까지이 정책을 차례로 화면에 표시 공급자 toorefine 고 전략이 새 할인 하나의 공급자 tooanother tooget에서 도약 toocustomers가 되었습니다.

송수화기 제품의 높은 변동성은 현재 송수화기 모델을 기반으로 한 이탈 모델이 잘못되었음을 빠르게 입증하는 요소입니다. 또한 휴대폰만 통신 장치가 아닌; 값은 시간 문 (고려 hello iPhone)도 되며 이러한 소셜 예측자 일반 통신 데이터 집합의 외부 hello 범위.

hello 모델링 됩니다 변동에 대 한 알려진된 이유를 제거 하 여 사운드 정책 시도해 볼 수 없습니다. 실제로 의사 결정 트리와 같이 범주형 변수를 수량화하는 대표적인 모델을 비롯하여 연속 모델링 전략은 **필수**입니다.

조직에서는 큰 데이터 집합을 사용 하 여 고객에 게에, 효과적인 방법 toohello 문제로 (특히, 빅 데이터에 따라 변동 검색)의 빅 데이터 분석을 수행 하려고 합니다. hello ETL 섹션에 맞춰져 있으며 권장 사항에에서는 변동 hello 빅 데이터 접근 방식 toohello 문제에 대 한 자세한을 찾을 수 있습니다.  

## <a name="methodology-toomodel-customer-churn"></a>방법론 toomodel 고객 변동
일반적인 문제 해결 프로세스 toosolve 고객 변동은 그림 1-3에 표시 됩니다.  

1. 위험 모델 tooconsider을 사용 하면 작업 위험 및 확률에 미치는 영향입니다.
2. 개입 모델 tooconsider을 사용 하면 hello 수준의 개입 hello 확률 청크 및 hello 양이 고객 수명 가치 (CLV)의 영향을 줄 수는 방법입니다.
3. 이 분석은 에스컬레이션된 tooa 사전 마케팅 캠페인을 고객 세그먼트 toodeliver hello 최적의 제공 대상 tooa 정 성적 분석 인계 합니다.  

![][1]

이 과정 이라면 방법은 hello 가장 좋은 방법은 tootreat 변동을 있지만 복잡성 함께 제공: hello 모델 간의 다중 모델 아키타 및 추적 종속성 toodevelop 있는 합니다. hello 다음 다이어그램에에서 표시 된 대로 모델 간에 hello 상호 작용을 캡슐화 할 수 있습니다.  

![][2]

*그림 4: 통합 다중 모델 원형*  

Hello 모델 간의 상호 작용에는 키 toodeliver 전체적인 접근 방식 toocustomer 보존 하는 경우입니다. 각 모델; 시간에 따라 반드시 저하 따라서 hello 아키텍처는 암시적 루프 (유사한 toohello 아키타 hello CRISP-DM 데이터 마이닝 표준에 따라 설정 [***3***]).  

hello 마케팅-위험-의사 결정 분할/분해의 전체 주기는 여전히 적용 가능한 toomany 비즈니스 문제는 일반화 된 구조입니다. 변동을 분석 문제의이 그룹의 강력한 담당자 단순히 않으므로 간단한 예측 솔루션을 허용 하지 않는 복잡 한 비즈니스 문제의 모든 hello 특성을 나타냅니다. hello 소셜 hello 최신 접근 방식 toochurn의 측면 특히 hello 접근 방식에서 강조 표시 되지 않습니다 되지만 모델에서와 같이 hello 소셜 측면 hello 모델링 아키타에 캡슐화 됩니다.  

여기서 또 다른 흥미로운 요소는 빅데이터 분석입니다. 오늘날의 통신 및 소매 비즈니스 고객에 게에 대 한 철저 한 데이터를 수집 하 고 해당 hello 필요한 연결 다중 모델은 일반적인 추세를 제공 추세와 같은 새로운 될 것에 대 한 hello 사물 인터넷 쉽게 수 것으로 예상 하 고 유비쿼터스 된 장치에 여러 계층에서 비즈니스 tooemploy 스마트 솔루션을 허용 합니다.  

 

## <a name="implementing-hello-modeling-archetype-in-machine-learning-studio"></a>기계 학습 스튜디오에서 아키타 모델링 hello 구현
방금 설명한 hello 문제가 들어 이란 hello 가장 좋은 방법은 tooimplement 통합된 모델링 및 점수 매기기 방법 이 섹션에서는 Azure 기계 학습 스튜디오를 사용하여 이 작업을 하는 방법을 보여 줍니다.  

hello 다중 모델 방법은 필수인 변동에 대 한 전역 아키타를 디자인 하는 경우입니다. Hello 방식의 (예측) 부분 점수 매기기에 hello 다중 모델 이어야 합니다.  

hello 다음 그림에 hello 프로토타입 기계 학습 스튜디오 toopredict 변동의 점수 매기기 알고리즘 4 개를 사용 하는 만들었습니다. hello 다중 모델 접근 방식을 사용 하는 앙상블 분류자 tooincrease 정확도 toocreate 뿐만 아니라 tooprotect 과잉 맞춤이 및 tooimprove 규범적인 기능 선택에 대 한 합니다.  

![][3]

*그림 5: 일탈 모델링 접근법의 프로토타입*  

hello 다음 섹션에서는 기계 학습 스튜디오를 사용 하 여 구현한 모델 점수 매기기 hello 프로토타입에 대 한 자세한 정보.  

### <a name="data-selection-and-preparation"></a>데이터 선택 및 준비
hello 데이터 toobuild hello 모델을 사용 하 고 hello 난독 처리 하는 데이터 tooprotect 고객 개인 정보 점수 고객 CRM 세로 솔루션에서 얻을 합니다. hello 데이터 포함 hello 미국의 8, 000 구독에 대 한 정보 되 고 결합 하 여 세 개의 소스: 데이터 (구독 메타 데이터), 활동 데이터 (hello 시스템 사용) 및 고객 지원 데이터를 프로 비전 합니다. hello 데이터에는 모든 비즈니스 관련 hello 고객;에 대 한 정보 예를 들어 충성도 메타 데이터 / 신용 점수는 포함 되지 않습니다.  

간단히 말해 데이터 준비가 이미 다른 곳에서 완료되었다고 가정하므로 ETL 및 데이터 정리 프로세스는 범위를 벗어납니다.   

모델링에 대해 기능 선택을 기반으로 한 예측자를 hello 임의 포리스트 모듈을 사용 하는 hello 프로세스에 포함 된 hello 집합의 점수 매기기 예비 의미 합니다. 기계 학습 스튜디오에서 hello 구현에 대 한 hello 평균값, 중앙값, 및 대표 기능에 대 한 범위를 계산 했습니다. 예를 들어, 사용자 활동에 대 한 최소 및 최대 값과 같은 hello 질적 데이터에 대 한 집계를 추가 했습니다.    

또한 가장 최근 6 개월 hello에 대 한 임시 정보를 캡처 했습니다. 1 년 동안 데이터를 분석 했습니다 하 고는 통계적으로 중요 한 추세 인 경우에 변동에 hello 영향이 크게 감소 6 개월 후를 설정 했습니다.  

hello 가장 중요 한 점은 해당 hello 전체 포함 하는 프로세스 ETL, 기능 선택 하 고 모델링 기계 학습 스튜디오에서는 Microsoft Azure에서 데이터 원본을 사용 하 여 구현 되었습니다.   

hello 다음 다이어그램에서는 사용 된 hello 데이터입니다.  

![][4]

*그림 6: 데이터 원본 발췌(난독 처리됨)*  

![][5]

*그림 7: 데이터 원본에서 추출된 기능*
 

> Note는이 데이터는 전용 포트 이며 따라서 hello 모델 및 데이터를 공유할 수 없습니다.
> 그러나 공개적으로 사용할 수 있는 데이터를 사용 하 여 비슷한 모델을이 샘플 실험을 hello 참조 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com/): [Telco 고객 변동](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383)합니다.
> 
> Cortana 인텔리전스 Suite를 사용 하 여 변동을 분석 모델을 구현 하는 방법에 대 한 자세한 toolearn, 것도 좋습니다 [이 비디오](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) 수석 프로그램 관리자 Wee Hyong Tok 여 합니다. 
> 
> 

### <a name="algorithms-used-in-hello-prototype"></a>Hello 프로토타입에 사용 되는 알고리즘
다음 4 개의 기계 학습 알고리즘 hello 사용 toobuild hello 프로토타입 (사용자 지정):  

1. LR(로지스틱 회귀)
2. BT(향상된 의사 결정 트리)
3. AP(Averaged Perceptron)
4. SVM(Support Vector Machine)  

hello 다음 다이어그램에서는 일부는 hello 모델 생성 된 hello 순서를 나타내는 hello 실험 디자인 화면에서를 수행 합니다.  

![][6]  

*그림 8: 기계 학습 스튜디오에서 모델 만들기*  

### <a name="scoring-methods"></a>점수 매기기 방법
레이블이 지정 된 학습 데이터 집합을 사용 하 여 4 hello 모델 점수가 했습니다.  

또한 hello SAS Enterprise 마이너 12의 데스크톱 버전을 사용 하 여 작성 된 데이터 집합 tooa 비교 가능한 모델 점수 매기기 hello을 제출 했습니다. Hello SAS 모델 및 모든 4 개의 기계 학습 스튜디오 모델의 hello 정확도 측정 했습니다.  

## <a name="results"></a>결과
이 섹션에서는 데이터 집합 점수 매기기 hello를 기반으로 hello 모델의 정확도 hello에 대 한 우리의 연구 결과 소개 합니다.  

### <a name="accuracy-and-precision-of-scoring"></a>점수 매기기의 정확도 및 정밀도
일반적으로 Azure 기계 학습에서 hello 구현이 SAS 뒤의 약 10-15% (곡선 아래의 영역 또는 AUC) 정확도 되었습니다.  

그러나 변동의 hello 가장 중요 한 메트릭을 hello 오 분류 속도: 즉, 상위 n 개 churners hello 분류자에서 예측으로 hello의 있는 실제로 수행한 **하지** , 변경 및 특별 한 처리를 아직 받지? hello 다음 다이어그램에서는 모든 hello 모델에 대 한이 오 분류 비율을 비교합니다.  

![][7]

*그림 9: Passau 프로토타입 AUC(Area Under Curve)*

### <a name="using-auc-toocompare-results"></a>AUC toocompare 결과 사용 하 여
영역에서 곡선 (AUC)은 전역 측정 한 값을 나타내는 메트릭입니다 *separability* 양수 및 음수 모집단에 대 한 점수의 hello 배포판 사이입니다. 비슷한 toohello 기존 수신기 연산자 특성 (ROC) 그래프에서 하지만 중요 한 차이점 해당 hello AUC 메트릭이 않습니다 toochoose 임계값 필요 하지 않습니다. 대신, 통해 hello 결과 요약 하기 **모든** 가능한 선택 항목입니다. 반면, hello 기존의 ROC 그래프 hello 세로 축 및 hello false 양의 속도 hello 가로 축에에 hello 양의 속도 표시 하 고 hello 분류 임계값 달라 집니다.   

일반적으로 AUC는 모델 toobe AUC 값을 사용 하 여 비교할 수 있기 때문에 서로 다른 알고리즘 (또는 다른 시스템)에 대 한 주요 측정값으로 사용 됩니다. 이는 기상학 및 생물공학과 같은 산업에서 일반적인 접근법입니다. 따라서 AUC는 분류자 성능을 평가하는 데 널리 사용되는 대표적인 도구입니다.  

### <a name="comparing-misclassification-rates"></a>오분류 비율 비교
약 8, 000 구독 hello CRM 데이터를 사용 하 여 hello 오 분류 속도 hello 데이터 집합을 비교 했습니다.  

* hello SAS 오 분류 속도 10-15%입니다.
* hello 기계 학습 스튜디오 오 분류 속도 상위 200-300 churners hello에 대 한 15-20%입니다.  

Hello telecommunications 업계에서 있는 고객 호텔 서비스 또는 다른 특별 한 처리를 제공 하 여 가장 높은 위험 toochurn hello만 중요 한 tooaddress입니다. 이러한 측면에서는 hello 기계 학습 스튜디오 구현 hello SAS 모델 수준의 맞춤형는 결과를 얻습니다.  

Hello 하 여 동일한 토큰을 정확도 전체 자릿수 보다 더 중요 한 잠재적인 churners 잘못 분류에 주로 관심이 있으므로 합니다.  

Wikipedia에서 다이어그램을 다음 hello 역동적인, 이해 하기 쉬운 그래픽에서 hello 관계를 보여 줍니다.  

![][8]

*그림 10: 정확도와 정밀도 간의 균형 유지*

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a>향상된 의사 결정 트리 모델의 정확도 및 정밀도 결과
다음 차트 표시 hello 원시 hello toobe hello hello 4 개의 모델 간에 가장 정확 하 게 발생 하는 hello 승격 된 의사 결정 트리 모델에 대 한 hello 기계 학습 프로토타입을 사용 하 여 점수 매기기에서 발생 합니다.  

![][9]

*그림 11: 향상된 의사 결정 트리 모델 특성*

## <a name="performance-comparison"></a>성능 비교
데이터 hello 기계 학습 스튜디오 모델과 비교 가능한 SAS Enterprise 마이너 12.1 hello 데스크톱 버전을 사용 하 여 만든 모델을 사용 하 여을 획득 된 hello 속도 비교 했습니다.  

다음 표에 hello hello 알고리즘의 hello 성능을 요약 되어 있습니다.  

*표 1. Hello 알고리즘의 일반적인 성능 (정확도)*

| LR | BT | AP | SVM |
| --- | --- | --- | --- |
| 평균 모델 |hello 최상의 모델 |성능 미만 |평균 모델 |

par 크게 달라 실적이 우수 했습니다 SAS를 실행 하지만 정확도의 속도 대 한 15 25%가 기계 학습 스튜디오에서 호스트 되는 hello 모델입니다.  

## <a name="discussion-and-recommendations"></a>설명 및 권장 사항
Hello telecommunications 업계의 몇 가지 사례 tooanalyze 늘어났습니다 변동를 포함 하 여:  

* 네 가지 기본 범주에 대한 메트릭을 도출합니다.
  * **엔터티(예: 구독)**. Hello 구독 및/또는 변동의 hello 주제는 고객에 대 한 기본 정보를 프로 비전 합니다.
  * **활동**. 예를 들어 hello 수가 로그인 관련된 toohello 엔터티에 있는 모든 가능한 사용 정보를 가져옵니다.
  * **고객 지원**. Hello 구독 있어 문제점 또는 고객와의 상호 작용을 지원 하는지 여부를 고객 지원 로그 tooindicate에서 정보를 수집 합니다.
  * **경쟁 및 비즈니스 데이터**. Hello 고객에 대 한 가능한 모든 정보 (예를 들어 가능 사용 불가능 하거나 하드 tootrack).
* 중요도 toodrive 기능 선택을 사용 합니다. 이 hello 승격 된 의사 결정 트리 모델은 항상 성공할 가능성이 접근 방식을 의미 합니다.  

hello 사용 하 여 이러한 네 가지 범주의 hello 감 하는 만드는 간단한 *결정적* 범주별 적절 한 요소에 구성 하는 인덱스에 따라 접근 방식을 tooidentify 고객 변동에 대 한 위험에는 충분 합니다. 불행히도 이 생각은 타당한 것처럼 보이지만 잘못된 이해입니다. hello 이유는 변동은 임시 효과 toochurn hello 요인은 일반적으로 임시 상태입니다. 고객 tooconsider 두면 오늘 하면 다를 수 있습니다 내일 고 확실히 됩니다 다른 6 개월 지금부터 합니다. 따라서 *확률적* 모델이 필요합니다.  

일반적으로 비즈니스 인텔리전스 지향 접근 방식 tooanalytics이 선호 하는 비즈니스에 중요 한 관찰이 종종 간과 되, 이기 때문에 대부분는 판매 쉽고 간단 하 게 자동화 입 합니다.  

그러나 기계 학습 스튜디오를 사용 하 여 셀프 서비스 분석에 대 한 hello 약속 부문 또는 부서, 그레이드할 정보의 hello 네 가지 범주는 하다는 것 변동에 대 한 기계 학습에 중요 한 원본입니다.  

Azure 기계 학습에 방문 하 고 다른 흥미로운 기능은 hello 기능 tooadd 이미 사용할 수 있는 미리 정의 된 모듈의 사용자 지정 모듈 toohello 저장소 기능입니다. 이 기능을 기본적으로, 기회 tooselect 라이브러리 만들고 수직적 시장에 사용할 템플릿을 작성 합니다. Azure 기계 학습의 hello 마켓플레이스를 구별 하는 중요 한 요소인 것합니다.  

이 항목을 hello 이후, 특히 관련 toobig 데이터 분석 toocontinue 바랍니다.
  

## <a name="conclusion"></a>결론
이 문서에서는 일반 프레임 워크를 사용 하 여 고객 변동의 합리적 tootackling hello 일반적인 문제를 설명 합니다. 점수 매기기 모델의 프로토타입을 고려하고 Azure 기계 학습을 사용하여 해당 프로토타입을 구현했습니다. 마지막으로, 큰지에 toocomparable 알고리즘에 따라 SAS 사용 하 여 hello 프로토타입 솔루션의 성능과 hello 정확도 평가 했습니다.  

**자세한 내용은 다음을 참조하세요.**  

이 문서가 도움이 되었나요? 사용자 의견을 보내주세요. 값 1 (나쁨) too5 (점 높음) 중 하나를 알려,이 문서를 평가해 주시기 및 이유 지정 했을 수 이러한 등급? 예:  

* 점수를 주 시겠습니까 기한 toohaving 좋은 예, 뛰어난 스크린 샷, 명료한 또는 다른 이유로 높은?
* 점수를 주 시겠습니까 기한 toopoor 예제, 유사 항목 스크린 샷 또는 명확 하지 않은 쓰기 낮은?  

이 피드백 hello 배포 하는 백서의 품질을 개선 하는 데는 데 도움이 됩니다.   

[사용자 의견 보내기](mailto:sqlfback@microsoft.com).
 

## <a name="references"></a>참조
[1] 예측 분석: McKnight, 정보 관리 년 7 월/년 8 월 2011 년 p.18-20 W. hello 예측을 초과 합니다.  

[2] Wikipedia 문서: [Accuracy and precision](http://en.wikipedia.org/wiki/Accuracy_and_precision)

[3] [CRISP-DM 1.0: Step-by-Step Data Mining Guide](http://www.the-modeling-agency.com/crisp-dm.pdf)   

[4] [Big Data Marketing: Engage Your Customers More Effectively and Drive Value](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)

[5] [Cortana Intelligence 갤러리](http://gallery.cortanaintelligence.com/)의 [Telco 이탈 모델 템플릿](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) 
 

## <a name="appendix"></a>부록
![][10]

*그림 12: 이탈 프로토타입에 대한 프레젠테이션 스냅숏*

[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png
[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
