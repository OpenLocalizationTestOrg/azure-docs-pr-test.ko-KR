---
title: "기계 학습에서 모델 성능을 aaaEvaluate | Microsoft Docs"
description: "Tooevaluate Azure 기계 학습에서 성능을 모델링 하는 방법에 대해 설명 합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 5dc5348a-4488-4536-99eb-ff105be9b160
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bradsev;garye
ms.openlocfilehash: 03477368758dbb13aa6f54c5d27fb215615d1f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooevaluate-model-performance-in-azure-machine-learning"></a>Tooevaluate는 Azure 기계 학습에서 성능을 모델링 하는 방법
이 문서는 방법을 보여 주는 tooevaluate Azure 기계 학습 스튜디오에서 모델의 성능을 hello이 작업에 대 한 hello 메트릭 사용할 수 있는 한 간략 한 설명을 제공 합니다. 다음 세 가지 일반적인 감독 학습 시나리오가 제공됩니다. 

* 회귀
* 이진 분류 
* 다중 클래스 분류

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

모델의 hello 성능 평가 hello 데이터 과학 프로세스에 hello 핵심 단계 중 하나입니다. (예측) 점수 매기기 얼마나 성공적인 hello 나타냅니다 dataset의 학습 된 모델에 의해 된 합니다. 

Azure Machine Learning에서는 해당 기본 Machine Learning 모듈 중 두 가지 모듈인 [모델 평가][evaluate-model] 및 [모델 교차 유효성 검사][cross-validate-model]를 통한 모델 평가를 지원합니다. 이러한 모듈을 사용 하면 toosee 어떻게 다양 한 기계 학습 및 통계에 자주 사용 되는 메트릭 기준으로 모델 작업을 수행 합니다.

## <a name="evaluation-vs-cross-validation"></a>평가 및 교차 유효성 검사
평가 및 교차 유효성 검사는 모델의 toomeasure hello 성능 표준 방법입니다. 둘 다 검사하거나 다른 모델과 비교할 수 있는 평가 메트릭을 생성합니다.

[모델 평가] [ evaluate-model] 점수가 매겨진된 데이터 집합에는 입력 (또는 2 한 경우에 2 다른 모델의 toocompare hello 성능을 원하는)로 필요 합니다. 즉, 있습니다 tootrain hello를 사용 하 여 모델 [모델 학습] [ train-model] hello를 사용 하 여 일부 데이터 집합에 대 한 예측 모듈과 확인 [모델 점수 매기기] [ score-model] 모듈, 전에 hello 결과 평가할 수 있습니다. hello 평가에 따라 레이블/hello true 레이블, hello에 의해 출력 되는 모두 함께 확률 점수가 매겨진 hello [모델 점수 매기기] [ score-model] 모듈입니다.

또는 여러 가지 학습 점수 평가 작업 (10 개의 접기가) 서로 다른 하위 집합에 대해 자동으로 hello 입력된 데이터의 교차 유효성 검사 tooperform를 사용할 수 있습니다. hello 입력된 데이터는 테스트를 위해 예약 되어 있으므로 하나 및 학습에 대 한 다른 9 hello 10 부분으로 나누어집니다. 이 프로세스를 10 번 반복 하 고 hello 평가 메트릭 평균을 계산 합니다. 이렇게 하면 모델 toonew 데이터 집합을 일반화가 얼마나 잘 결정 하는 데 있습니다. hello [모델 교차 유효성 검사] [ cross-validate-model] 모듈에서는 학습 되지 않은 모델에서 사용 하 고 일부 10 개의 접기가 레이블이 각각 hello의 hello 평가 결과 데이터 집합 및 출력, toohello 결과 평균 하는 또한 합니다.

다음 섹션 hello,에서는 간단한 회귀 및 분류 모델을 작성 하 고 두 hello를 사용 하 여 성능을 평가 [모델 평가] [ evaluate-model] 및 hello [교차 유효성 검사 모델] [ cross-validate-model] 모듈입니다.

## <a name="evaluating-a-regression-model"></a>회귀 모델 평가
차원, 성능, 엔진 사양 등과 같은 일부 기능을 사용 하 여 자동차의 가격이 toopredict 원하는 가정 합니다. 이것은 일반 회귀 문제, 여기서는 대상 변수가 hello (*가격*) 연속 숫자 값입니다. Hello 기능 지정한 특정 자동차의 값을 예측할 수 있습니다는 자동차의 hello 가격 단순 선형 회귀 모델을 충족할 수 있습니다. 이 회귀 모델을 사용할 수 있습니다 tooscore hello 동일한 데이터 집합에서 학습 하는 것입니다. 모든 hello 자동차에 대 한 예측된 가격 hello 있는 것, 일단 얼마나 hello 예측 사양과 hello 실제 가격에서 평균 확인 하 여 hello 모델의 hello 성능을 평가 수 있습니다. tooillustrate이 hello 사용 하 여 *자동차 가격 데이터 (Raw) 데이터 집합* hello에서 사용할 수 있는 **저장 된 데이터 집합** Azure 기계 학습 스튜디오의 섹션입니다.

### <a name="creating-hello-experiment"></a>Hello 실험 만들기
Azure 기계 학습 스튜디오의 모듈 tooyour 작업 영역을 다음 hello를 추가 합니다.

* 자동차 가격 데이터(원시)
* [선형 회귀][linear-regression]
* [모델 학습][train-model]
* [모델 점수 매기기][score-model]
* [모델 평가][evaluate-model]

그림 1과의 hello hello 레이블 열 집합에 다음과 같이 hello 포트 연결 [모델 학습] [ train-model] 모듈 너무*가격*합니다.

![회귀 모델 평가](media/machine-learning-evaluate-model-performance/1.png)

그림 1. 회귀 모델 평가

### <a name="inspecting-hello-evaluation-results"></a>Hello 평가 결과 검사합니다.
Hello의 hello 출력 포트를 클릭할 수 실행 중인 hello 실험 한 후 [모델 평가] [ evaluate-model] 모듈과 선택 *시각화* toosee hello 평가 결과입니다. 회귀 모델에 대 한 평가 메트릭을 사용할 수 있는 hello: *평균 절대 오차*, *루트 평균 절대 오차*, *상대 절대 오차*,  *상대 제곱 오차*, 및 hello *결정 계수*합니다.

"error" 여기 hello 차이 나타내는 hello 용어 hello hello true 값과 예측 된 값입니다. hello 절대 값 또는 이러한 차이의 제곱 hello 일반적으로 계산된 toocapture hello hello 차이 hello로 모든 인스턴스에서 오류의 크기를 예측 하 고 true 값 일부 경우에는 음수 수 총 간주 됩니다. hello 오차 메트릭 hello hello true 값에서 해당 예측의 평균 편차 hello 관점에서 회귀 모델의 예측 성능을 측정합니다. 오류 값이 낮을수록 hello 모델은 보다 정확한 예측을 만드는 것을 의미 합니다. 전체 오류 메트릭 모델 hello 0 이면 hello 데이터를 완벽 하 게 적합 합니다.

R 라고도 하는 결정 hello 계수 제곱, hello 모델이 얼마나 잘 hello 데이터에 적합할 측정 하는 표준 방법 이기도 합니다. Hello 모델에 의해 설명 변형의 hello 비율로 해석 될 수 있습니다. 이 경우 비율이 높을수록 좋으며, 1은 완벽한 적합을 나타냅니다.

![선형 회귀 평가 메트릭](media/machine-learning-evaluate-model-performance/2.png)

그림 2. 선형 회귀 평가 메트릭

### <a name="using-cross-validation"></a>교차 유효성 검사 사용
앞서 언급 했 듯이 반복된 학습을 수행할 수 있습니다, 점수 매기기 및 평가 자동으로 사용 하 여 hello [모델 교차 유효성 검사] [ cross-validate-model] 모듈입니다. 이 경우에는 데이터 집합, 학습되지 않은 모델 및 [모델 교차 유효성 검사][cross-validate-model] 모듈만 있으면 됩니다(아래 그림 참조). 참고 tooset hello 레이블 열을 너무 필요한*가격* hello에 [모델 교차 유효성 검사] [ cross-validate-model] 모듈의 속성입니다.

![회귀 모델 교차 유효성 검사](media/machine-learning-evaluate-model-performance/3.png)

그림 3. 회귀 모델 교차 유효성 검사

실행 중인 hello 실험 한 후 hello의 hello 오른쪽 출력 포트를 클릭 하 여 hello 평가 결과 검사할 수 [모델 교차 유효성 검사] [ cross-validate-model] 모듈입니다. 각 반복 (접기)에 대 한 hello 메트릭에 대 한 자세히 보기를 제공할 것이 하 이며 hello 각각 hello 메트릭 (그림 4)의 결과 평균.

![회귀 모델의 교차 유효성 검사 결과](media/machine-learning-evaluate-model-performance/4.png)

그림 4. 회귀 모델의 교차 유효성 검사 결과

## <a name="evaluating-a-binary-classification-model"></a>이진 분류 모델 평가
이진 분류 시나리오에서는 hello 대상 변수에 단 두 가지 결과 예: {0, 1} 또는 {false, true}, {음수, 양의}. 일부와 성인 직원의 데이터 집합을 지정 하는 것으로 가정 인구 통계 및 고용 변수와 toopredict hello 수입 수준, hello 값이 포함 된 이진 변수를 묻는 {"< = 50k", "> 50k"을 (를). Hello 음수 클래스 보다 작거나 같은지를 확인 하는 hello 직원 나타냅니다. 즉, 연도 및 클래스는 다른 모든 직원 나타냅니다. 양수 hello 당 too50K 합니다. Hello 회귀 시나리오에서와 같이 모델을 학습 일부 데이터 점수와 hello 결과 평가 했습니다. hello 주요 차이점 여기에 Azure 기계 학습을 계산 하는 메트릭 및 출력의 hello 선택입니다. tooillustrate hello 소득 수준 예측 시나리오에서 사용 하 여 hello [성인](http://archive.ics.uci.edu/ml/datasets/Adult) dataset toocreate Azure 기계 학습 실험 및 2 클래스 로지스틱 회귀 모델에서는 자주 사용 되는 이진 파일의 hello 성능을 평가 합니다. 분류자입니다.

### <a name="creating-hello-experiment"></a>Hello 실험 만들기
Azure 기계 학습 스튜디오의 모듈 tooyour 작업 영역을 다음 hello를 추가 합니다.

* 성인 인구 조사 소득 이진 분류 데이터 집합
* [2클래스 로지스틱 회귀 분석][two-class-logistic-regression]
* [모델 학습][train-model]
* [모델 점수 매기기][score-model]
* [모델 평가][evaluate-model]

그림 5 및 hello hello 레이블 열 집합에 다음과 같이 hello 포트 연결 [모델 학습] [ train-model] 모듈 너무*소득*합니다.

![이진 분류 모델 평가](media/machine-learning-evaluate-model-performance/5.png)

그림 5. 이진 분류 모델 평가

### <a name="inspecting-hello-evaluation-results"></a>Hello 평가 결과 검사합니다.
Hello의 hello 출력 포트를 클릭할 수 실행 중인 hello 실험 한 후 [모델 평가] [ evaluate-model] 모듈과 선택 *시각화* toosee hello 평가 결과 (그림 7). 이진 분류 모델에 대 한 평가 메트릭을 사용할 수 있는 hello: *정확도*, *정밀도*, *회수*, *F1 점수*, 및 *AUC*합니다. 또한 hello 모듈 표시 참 긍정, 거짓 부정, 거짓 긍정 및 참 부정 hello 많이 혼동 행렬의 출력으로 *ROC*, *정밀도/회수*, 및 *리프트* 곡선으로 분할 합니다.

정확도 단순히 hello 비율을 제대로 분류 된 인스턴스. 이 일반적으로 보면 분류자를 평가할 때 hello 첫 번째 메트릭. 그러나 때 hello 테스트 데이터는 짝이 맞지 않습니다 (대부분의 hello 인스턴스 속해 있는 hello 클래스 tooone), 또는 더 관심이 정확도 hello 클래스 중 하나에서 hello 성능에서 분류자의 hello 효과 캡처하지 실제로 않습니다. Hello 소득 수준 분류 시나리오에서는 위치 hello 인스턴스 중 99% 나타내며 사용자에 게 폭이 보다 작거나 같은 일부 데이터에 대해 테스트 하는 가정 too50K 1 년입니다. Hello 클래스를 예측 하 여 가능한 tooachieve 0.99 정확도은 "< = 50k" 모든 인스턴스에 대 한 합니다. 이 경우 hello 분류자 toobe 전반적으로 성공한 작업을 수행 하 보이지만 실제로 실패 tooclassify hello high-income 개인 (hello 1%)의 모든 올바르게 있습니다.

따라서 hello 평가의 보다 구체적인 측면을 캡처하는 것이 도움이 toocompute 추가 메트릭을. 이러한 메트릭의 hello 세부 정보를 살펴보기 전에 이진 분류에 대 한 평가의 중요 한 toounderstand hello 혼동 행렬 것 합니다. hello 학습 집합의 레이블 어떤에서는 일반적으로 2 가능한 값에 대해 수행할 수는 hello 클래스 tooas 양수 또는 음수를 참조 하십시오. 분류자를 올바르게 예측 하는 hello 양수 및 음수 인스턴스 참 긍정 (TP) 및 참 부정 (TN) 각각 이라고 합니다. 마찬가지로, 오 분류 hello 인스턴스는 (FP) 거짓 긍정 및 거짓 부 정의 (FN) 라고 합니다. hello 혼동 행렬 되는 테이블 hello에 속하는 각 4 범주의 인스턴스 수를 표시 합니다. Azure 기계 학습에서는 hello hello 데이터 집합의 두 클래스 중 hello 양의 클래스를 자동으로 결정 합니다. Hello 클래스 레이블을 부울 또는 정수, 다음 hello 'true' 또는 '1' 레이블이 지정 된 인스턴스는 hello 양의 클래스를 할당 됩니다. Hello 레이블을 인 문자열 hello hello 소득 데이터 집합의 경우와 같이 hello 레이블을 사전순으로 정렬 됩니다 하 고 hello 두 번째 수준 hello 양의 클래스는 hello 첫 번째 수준이 toobe hello 음수 클래스를 선택 합니다.

![이진 분류 혼동 행렬](media/machine-learning-evaluate-model-performance/6a.png)

그림 6. 이진 분류 혼동 행렬

Toohello 소득 분류 문제를 다시 살펴보자면, tooask 여러 평가 질문 하는 데 도움이 사용 하는 hello 분류자의 hello 성능을 파악 원하는 것입니다. 매우 일반적인 질문은: ' hello 누구 hello 개인 부족 예측된 toobe 획득 모델 > 개수 분류 된 올바르게 50k (TP + FP) (TP)?' Hello 확인 하 여이 질문에 대답 하기 **정밀도** hello 모델을 올바르게 분류 되는 긍정의 hello 비율의: TP/(TP+FP) 합니다. 또 다른 일반적인 질문은 "hello 높은 earning 가진 모든 직원으로 소득 부족 > 개수 않은 분류자를 hello 50k (TP + FN) 올바르게 분류 (TP)"입니다. 이 실제로 hello **회수**, 또는 hello true 양의 속도: hello 분류자의 TP/(TP+FN) 합니다. 정확도와 재현율 사이에는 명확한 반비례 관계가 있는 것을 볼 수 있습니다. 예를 들어, 상대적으로 균형 잡힌된 데이터 집합에 지정 된 경우 양의 인스턴스 대부분을 예측 하는 분류자 가질 높은 회수 있지만 많은 hello 음수 인스턴스 대신 낮은 정밀도 수 마이닝에서 잘못 분류 되 다 수의 거짓 긍정 결과입니다. 이러한 두 메트릭을 달라의 그림 toosee 클릭할 수 있습니다 hello 평가 결과 출력 페이지에서 hello ' 정밀도/회수 ' 곡선 (그림 7의 왼쪽 위).

![이진 분류 평가 결과](media/machine-learning-evaluate-model-performance/7.png)

그림 7. 이진 분류 평가 결과

흔히 사용 되는 메트릭에 hello 관련 된 다른 **F1 점수**, 전체 자릿수와 회수 고려를 따르세요. 이러한 2 메트릭의 hello 조화 평균 이며 따라서 계산: F1 = 2 (전체 자릿수 x 회수) / (정밀도 + 회수). hello F1 점수는 단일 숫자는 좋은 방법 toosummarize hello 평가 하지만 전체 자릿수와 회수 함께 toobetter 분류자 동작 하는 방법을 이해 하는 것이 좋습니다 toolook 항상 쉽습니다.

또한 hello false 양의 속도 hello 및 hello true 양의 속도 검사할 수 하나 **수신기 운영 특징 (ROC)** 곡선 및 해당 hello **영역 아래의 hello 곡선 (AUC)** 값입니다. hello 가깝게이 곡선 toohello 상단 왼쪽 모서리 이면 hello 더 나은 hello 분류자의 성능은 (즉 최대화 hello true 양의 속도 hello false 양의 비율을 최소화 하면서). 닫기 toohello 대각선 있는 곡선 그리기 hello, 결과 toomake 예측 가능성이 높은 분류자에서 toorandom 추측을 닫습니다.

### <a name="using-cross-validation"></a>교차 유효성 검사 사용
Hello 회귀 예제와 같이 toorepeatedly 학습 교차 유효성 검사를 수행 점수와 hello 데이터의 여러 하위 집합을 자동으로 평가할 수 했습니다. 마찬가지로, 우리 צ ְ ײ hello [모델 교차 유효성 검사] [ cross-validate-model] 모듈과 학습 되지 않은 로지스틱 회귀 모델을 데이터 집합입니다. hello 레이블 열을 너무 설정 되어야 합니다.*소득* hello에 [모델 교차 유효성 검사] [ cross-validate-model] 모듈의 속성입니다. Hello 실험을 실행 하 고 hello 오른쪽 클릭 하면 출력의 hello 포트 후 [모델 교차 유효성 검사] [ cross-validate-model] 볼 수 있습니다 모듈 hello 이진 분류 메트릭 값이 각 접기에 대해 또한 toohello 평균 및 각각의 표준 편차를 제공 합니다. 

![이진 분류 모델 교차 유효성 검사](media/machine-learning-evaluate-model-performance/8.png)

그림 8. 이진 분류 모델 교차 유효성 검사

![이진 분류자의 교차 유효성 검사 결과](media/machine-learning-evaluate-model-performance/9.png)

그림 9. 이진 분류자의 교차 유효성 검사 결과

## <a name="evaluating-a-multiclass-classification-model"></a>다중 클래스 분류 모델 평가
이 실험 인기 있는 hello 사용 [Iris](http://archive.ics.uci.edu/ml/datasets/Iris "Iris") hello iris 공장의 3 다른 유형 (클래스)의 인스턴스가 포함 된 데이터 집합입니다. 각 인스턴스에 대해 4개의 기능 값(꽃받침 길이/너비 및 꽃잎 길이/너비)이 있습니다. 학습 म hello 이전 실험 하 고 사용 하 여 테스트 된 hello 모델 hello 동일한 데이터 집합. 여기에서 사용 하 여 hello [분할 데이터] [ split] hello 데이터 모듈 2 toocreate 하위 집합 hello에 먼저, 및 점수를 매깁니다. 학습과 평가 hello에 두 번째입니다. hello Iris 데이터 집합은 hello에서 공개적으로 사용할 [UCI 기계 학습 리포지토리](http://archive.ics.uci.edu/ml/index.html)를 사용 하 여 다운로드할 수 있습니다는 [데이터 가져오기] [ import-data] 모듈입니다.

### <a name="creating-hello-experiment"></a>Hello 실험 만들기
Azure 기계 학습 스튜디오의 모듈 tooyour 작업 영역을 다음 hello를 추가 합니다.

* [데이터 가져오기][import-data]
* [다중 클래스 의사 결정 포리스트][multiclass-decision-forest]
* [데이터 분할][split]
* [모델 학습][train-model]
* [모델 점수 매기기][score-model]
* [모델 평가][evaluate-model]

그림 10에 다음과 같이 hello 포트를 연결 합니다.

Hello 레이블 열 인덱스의 hello 설정 [모델 학습] [ train-model] 모듈 too5 합니다. hello 데이터 집합에 머리글 행이 없는 않지만 해당 hello 클래스 레이블을 hello 다섯 번째 열에 표시 됩니다.

Hello 클릭 [데이터 가져오기] [ import-data] 모듈 및 집합 hello *데이터 소스* 속성 너무*HTTP 통해 웹 URL*, 및 hello *URL*  toohttp://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data 합니다.

Hello에 대 한 학습에 사용 되는 인스턴스 toobe의 집합 hello 비율 [분할 데이터] [ split] 모듈 (예: 0.7).

![다중 클래스 분류자 평가](media/machine-learning-evaluate-model-performance/10.png)

그림 10. 다중 클래스 분류자 평가

### <a name="inspecting-hello-evaluation-results"></a>Hello 평가 결과 검사합니다.
Hello 실험을 실행 하 고 hello 출력 포트의 클릭 [모델 평가][evaluate-model]합니다. 이 경우 hello 평가 결과 hello 형태의 혼동 행렬이 표시 됩니다. hello 매트릭스 3 가지 모든 클래스에 대 한 예측 된 인스턴스 및 실제 hello를 보여 줍니다.

![다중 클래스 분류 평가 결과](media/machine-learning-evaluate-model-performance/11.png)

그림 11. 다중 클래스 분류 평가 결과

### <a name="using-cross-validation"></a>교차 유효성 검사 사용
앞서 언급 했 듯이 반복된 학습을 수행할 수 있습니다, 점수 매기기 및 평가 자동으로 사용 하 여 hello [모델 교차 유효성 검사] [ cross-validate-model] 모듈입니다. 데이터 집합, 학습되지 않은 모델 및 [모델 교차 유효성 검사][cross-validate-model] 모듈이 필요합니다(아래 그림 참조). hello tooset hello 레이블 열이 필요 하면 다시 [모델 교차 유효성 검사] [ cross-validate-model] 모듈 (열 인덱스 5이 경우에서). Hello 실험을 실행할 hello 오른쪽을 클릭 하 고 출력의 hello 포트 후 [모델 교차 유효성 검사][cross-validate-model], 각 접기으로 평균 및 표준 편차 hello에 대 한 hello 메트릭 값을 검사할 수 있습니다. hello 여기에 표시 된 메트릭은 hello 비슷한 toohello hello 이진 분류 사례에서 설명 하는 것입니다. 그러나 다중 클래스 분류에서를 그대로 전반적인 양수 또는 음수 클래스가 없습니다. 클래스 별로 계산 하 여 수행 됩니다 컴퓨팅 hello 참 긍정/부정 및 거짓 긍정/부정. 예를 들어 때 컴퓨팅 hello 정밀도, 회수 hello ' Iris setosa' 클래스의 가정 hello 양의 클래스 및 다른 모든 음수으로 이것이.

![다중 클래스 분류 모델 교차 유효성 검사](media/machine-learning-evaluate-model-performance/12.png)

그림 12. 다중 클래스 분류 모델 교차 유효성 검사

![다중 클래스 분류 모델의 교차 유효성 검사 결과](media/machine-learning-evaluate-model-performance/13.png)

그림 13. 다중 클래스 분류 모델의 교차 유효성 검사 결과

<!-- Module References -->
[cross-validate-model]: https://msdn.microsoft.com/library/azure/75fb875d-6b86-4d46-8bcc-74261ade5826/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[multiclass-decision-forest]: https://msdn.microsoft.com/library/azure/5e70108d-2e44-45d9-86e8-94f37c68fe86/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-logistic-regression]: https://msdn.microsoft.com/library/azure/b0fd7660-eeed-43c5-9487-20d9cc79ed5d/

