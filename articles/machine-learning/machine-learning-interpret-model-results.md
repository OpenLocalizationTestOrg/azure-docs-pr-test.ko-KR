---
title: "기계 학습에서 모델 결과 aaaInterpret | Microsoft Docs"
description: "어떻게 toochoose hello 최적의 매개 변수를 사용 하 여 및 점수 모델 출력을 시각화 하는 알고리즘에 대 한 설정 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52161b1aa5ff3e7a63fc4b1bfb7c5e354eabcc50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a>Machine Learning에서 모델 결과 해석
이 항목에서는 설명 어떻게 toovisualize Azure 기계 학습 스튜디오에서 예측 결과 해석 합니다. 모델을 학습 하 고 ("hello 모델 점수") 그 위에 예측 수행 후 toounderstand 필요 하 고 hello 예측 결과 해석 합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Azure 기계 학습에는 다음과 같이 네 가지 주된 유형의 기계 학습 모델이 있습니다.

* 분류
* 클러스터링
* 회귀
* 추천 시스템

이 모델 위에 예측에 사용 하는 hello 모듈은:

* 분류 및 회귀를 위한 [모델 점수 매기기][score-model] 모듈
* [TooClusters 할당] [ assign-to-clusters] 클러스터링에 대 한 모듈
* 추천 시스템을 위한 [매치박스 추천 점수 매기기][score-matchbox-recommender]

이 문서에서는 이러한 각 모듈에 대 한 toointerpret 예측 결과 하는 방법을 설명 합니다. 이러한 모듈의 개요를 참조 하십시오. [어떻게 toochoose 매개 변수 toooptimize Azure 기계 학습에서 알고리즘](machine-learning-algorithm-parameters-optimize.md)합니다.

이 항목에서는 예측 해석에 대해 다루지만 모델 평가는 다루지 않습니다. 방법에 대 한 자세한 내용은 tooevaluate 모델 참조 [tooevaluate Azure 기계 학습에서 성능을 모델링 하는 방법을](machine-learning-evaluate-model-performance.md)합니다.

새 tooAzure 기계 학습 하 고 시작 하는 간단한 실험 tooget 만들기 도움말을 참조 하십시오. 필요한 경우 [Azure 기계 학습 스튜디오에서 간단한 실험 만들기](machine-learning-create-experiment.md) Azure 기계 학습 스튜디오에서.

## <a name="classification"></a>분류
분류 문제의 하위 범주는 다음 두 가지가 있습니다.

* 2클래스에만 문제가 있음(2클래스 또는 이진 분류)
* 세 개 이상의 클래스에 문제가 있음(다중 클래스 분류)

Azure 기계 학습 분류를 이러한 유형에 각각의 서로 다른 모듈 toodeal 갖지만 예측 결과 해석 하기 위한 hello 메서드는 유사 합니다.

### <a name="two-class-classification"></a>2클래스 분류
**예제 실험**

2 클래스 분류 문제의 경우의 예는 iris 꽃의 hello 분류 됩니다. hello 작업은 tooclassify iris 꽃 해당 기능을 기반으로 합니다. hello Azure 기계 학습에서 제공 된 Iris 데이터 집합의 하위 집합인 인기 있는 hello [Iris 데이터 집합](http://en.wikipedia.org/wiki/Iris_flower_data_set) 지정 (클래스 0과 1) 화 단 두 개의 전용의 인스턴스를 포함 합니다. 각 꽃에는 네 가지 특징이 있습니다(꽃받침 길이, 꽃받침 너비, 꽃잎 길이 및 꽃잎 너비).

![붓꽃 실험의 스크린샷](./media/machine-learning-interpret-model-results/1.png)

그림 1. 붓꽃 2클래스 분류 문제 실험

실험 되었습니다 수행된 toosolve이이 문제를 그림 1에 나와 있는 것 처럼 합니다. 2클래스의 향상된 의사 결정 트리 모델이 학습되어 점수가 지정되었습니다. Hello에서 hello 예측 결과 시각화할 수 이제 [모델 점수 매기기] [ score-model] hello의 hello 출력 포트를 클릭 하 여 모듈 [모델 점수 매기기] [ score-model]모듈을 클릭 한 다음 **시각화**합니다.

![모델 점수 매기기 모듈](./media/machine-learning-interpret-model-results/1_1.png)

그림 2에 나와 있는 것 처럼 결과 점수 매기기 hello가 표시 됩니다.

![붓꽃 2클래스 분류 문제 실험의 결과](./media/machine-learning-interpret-model-results/2.png)

그림 2. 2클래스 분류의 모델 점수 매기기 결과 시각화

**결과 해석**

Hello 결과 테이블에 열이 6 개 있습니다. hello 왼쪽된 열 4 개는 hello 4 개의 기능입니다. hello 오른쪽으로 두 열, 점수가 매겨진 레이블 및 점수가 매겨진 확률은 hello 예측 결과입니다. hello 점수가 매겨진 확률 열 표시 hello 속할 확률을 꽃 toohello 양의 클래스 (클래스 1). 예를 들어 hello hello 열 (0.028571) 이면 첫 번째 꽃 hello 0.028571 확률 속한 tooClass 1에서에서 첫 번째 숫자입니다. 점수가 매겨진 레이블 열 표시 hello hello 각 꽃에 대 한 클래스를 예측합니다. 이 설정은 hello 점수가 매겨진 확률 열에 기반 합니다. Hello 꽃의 확률 점수가 매겨진 0.5 보다 큰 경우 클래스 1로 예측 합니다. 그렇지 않으면 클래스 0으로 예측됩니다.

**웹 서비스 게시**

Hello 예측 결과 이해 하 고 사운드 판단 한 후 hello 실험 게시할 수 있습니다를 웹 서비스로 다양 한 응용 프로그램에 배포 하 고 모든 새 iris 꽃에서 tooobtain 클래스 예측을 호출할 수 있도록 합니다. toolearn toochange 학습 점수 매기기 실험으로 실험 및 웹 서비스로 게시 하는 방법 참조 [hello Azure 기계 학습 웹 서비스 게시](machine-learning-walkthrough-5-publish-web-service.md)합니다. 이 절차에 따르면 그림 3에 표시된 대로 점수 매기기 실험이 제공됩니다.

![점수 매기기 실험의 스크린샷](./media/machine-learning-interpret-model-results/3.png)

그림 3. 점수 매기기 hello iris 2 클래스 분류 문제 실험

이제 해야 tooset hello 입력 및 출력 hello 웹 서비스에 대 한 합니다. hello 입력이 hello 오른쪽 입력된 포트의 [모델 점수 매기기][score-model], Iris 꽃 기능 입력 hello은입니다. hello hello 출력에 따라 선택 여부 관심이 hello에 predicted 클래스 (점수가 매겨진된 레이블), 확률 또는 둘 다 hello 점수가 매겨진 합니다. 이 예에서는 둘 다에 관심이 있다고 가정합니다. tooselect hello 출력 열을 사용 하 여 원하는 [데이터 집합에서 열 선택] [ select-columns] 모듈입니다. [데이터 집합의 열 선택][select-columns] 모듈을 클릭하고, **열 선택기 시작**을 클릭한 다음 **점수가 매겨진 레이블** 및 **점수가 매겨진 확률**을 선택합니다. hello 출력 포트를 설정한 후 [데이터 집합에서 열 선택] [ select-columns] 다시 실행 수 있어야 준비 toopublish hello 점수 매기기 실험을 웹 서비스로 클릭 하 여 **웹 게시 서비스**합니다. hello 최종 실험 그림 4와 유사합니다.

![hello iris 2 클래스 분류 실험](./media/machine-learning-interpret-model-results/4.png)

그림 4. 붓꽃 2클래스 분류 문제의 마지막 점수 매기기 실험

Hello 웹 서비스를 실행 하 고 테스트 인스턴스에의 한 기능 값을 입력 한 후 hello 결과 두 개의 숫자를 반환 합니다. hello 첫 번째 숫자는 레이블, 점수가 매겨진 hello 및 hello 확률 점수가 매겨진 hello를 두 번째는 합니다. 이 꽃은 확률이 0.9655인 클래스 1로 예측됩니다.

![모델 점수 매기기 테스트 해석](./media/machine-learning-interpret-model-results/4_1.png)

![점수 매기기 테스트 결과](./media/machine-learning-interpret-model-results/5.png)

그림 5. 붓꽃 2클래스 분류의 웹 서비스 결과

### <a name="multi-class-classification"></a>다중 클래스 분류
**예제 실험**

이 실험에서는 다중 클래스 분류의 예로 문자 인식 작업을 수행합니다. hello 분류자 시도 toopredict 특정 이미지를 직접 작성 하는 hello에서 추출 된 일부 직접 작성 된 특성 값을 기반으로 하는 문자 (클래스).

![문자 인식 예제](./media/machine-learning-interpret-model-results/5_1.png)

Hello 학습 데이터에서 직접 작성 된 문자 이미지에서 추출 된 16 기능이 있습니다. 문자는 26 hello 26 클래스를 형성합니다. 그림 6 표시는 다중 클래스 분류를 학습 하는 실험 문자 인식에 대 한 모델 되며 hello에서 동일한 예측 기능 집합에 테스트 데이터 집합.

![문자 인식 다중 클래스 분류 실험](./media/machine-learning-interpret-model-results/6.png)

그림 6. 문자 인식 다중 클래스 분류 문제 실험

Hello 결과 hello에서 시각화 [모델 점수 매기기] [ score-model] 의 hello 출력 포트를 클릭 하 여 모듈 [모델 점수 매기기] [ score-model] 모듈 한 다음 클릭 하면 **시각화**, 그림 7에 표시 된 것 처럼 콘텐츠가 표시 됩니다.

![모델 점수 매기기 결과](./media/machine-learning-interpret-model-results/7.png)

그림 7. 다중 클래스 분류에서 모델 점수 매기기 결과 시각화

**결과 해석**

16 개의 열을 왼쪽된 hello hello 테스트 집합의 hello 기능 값을 나타냅니다. hello 2 클래스의 경우에서 "XX" 클래스에 대 한 점수가 매겨진 확률은 hello 점수가 매겨진 확률 열 동일와 같은 이름의 hello 열입니다. 특정 클래스에 해당 하는 항목이 hello hello 확률 해당를 보여 줍니다. 예를 들어 hello 첫 번째 항목에 대 한 확률이 0.003571는 "A" 0.000451 일 가능성이 있는 "B", 및 등 인지 합니다. hello 마지막 열 (점수가 매겨진 레이블) hello 2 클래스 경우에서 점수가 매겨진 레이블 동일 hello 됩니다. 가장 큰 hello hello 해당 항목의 클래스를 예측된 하는 대로 확률 점수가 매겨진 hello 사용 하 여 hello 클래스 템플릿을 선택 합니다. 예를 들어 hello 첫 번째 항목에 대 한 hello 레이블 점수는 "F" hello 가장 큰 확률 toobe는 "F" (0.916995)에 있기 때문입니다.

**웹 서비스 게시**

또한 각 진입 지점과 hello 가능성 레이블 점수가 매겨진 hello에 대 한 레이블 점수가 매겨진 hello를 얻을 수 있습니다. hello 기본 논리는 확률 점수가 매겨진 모든 hello 간에 toofind hello 최대 확률입니다. toodo이 toouse hello 해야 [R 스크립트 실행] [ execute-r-script] 모듈입니다. 그림 8에 R 코드 hello 보여지고 hello 결과 hello 실험은 그림 9에 표시 됩니다.

![R 코드 예제](./media/machine-learning-interpret-model-results/8.png)

그림 8. 점수가 매겨진 레이블와 hello 추출에 대 한 R 코드 hello 레이블의 확률에 연결

![실험 결과](./media/machine-learning-interpret-model-results/9.png)

그림 9. Hello 문자 인식 다중 클래스 분류 문제의 최종 점수 매기기 실험

게시 고 hello 웹 서비스를 실행 한 입력된 기능 값을 입력 한 후 hello 결과 아래 그림 10을 반환 합니다. 이 직접 작성 된 문자의 압축을 푼 16 기능 0.9715 확률이 예측된 toobe "T"입니다.

![점수 매기기 모듈 테스트 해석](./media/machine-learning-interpret-model-results/9_1.png)

![테스트 결과](./media/machine-learning-interpret-model-results/10.png)

그림 10. 다중 클래스 분류의 웹 서비스 결과

## <a name="regression"></a>회귀
회귀 문제는 분류 문제와 다릅니다. 분류 문제의 경우 toopredict 불연속 클래스, iris 꽃 속한 클래스 등을 시도 하는 합니다. 하지만 다음 예에서는 회귀 문제의 hello에 보시 toopredict 자동차의 hello 가격 같은 연속 변수를 시도 하는 합니다.

**예제 실험**

회귀 예제로 자동차 가격 예측을 사용합니다. 만들기, 연료 유형, 본문 유형 및 드라이브 휠을 포함 하 여 해당 기능을 기반으로 하는 자동차의 toopredict hello 가격을 하려고 합니다. 그림 11에서 hello 실험 표시 됩니다.

![자동차 가격 회귀 실험](./media/machine-learning-interpret-model-results/11.png)

그림 11. 자동차 가격 회귀 문제 실험

형상화 hello [모델 점수 매기기] [ score-model] 모듈 그림 12 같은 목록이 hello 만들어집니다.

![자동차 가격 예측 문제의 점수 매기기 결과](./media/machine-learning-interpret-model-results/12.png)

그림 12. Hello 자동차 가격 예측 문제에 대 한 점수 매기기 결과

**결과 해석**

점수가 매겨진된 레이블은 hello 결과 열이 점수 매기기 결과에서입니다. hello 번호는 각 자동차에 대 한 hello 예측된 가격입니다.

**웹 서비스 게시**

Hello 회귀 실험을 웹 서비스로 게시 하 고 호출할 hello에서 자동차 가격 예측을 위해 hello 2 클래스 분류와 동일 하 게 대/소문자를 사용 합니다.

![자동차 가격 회귀 문제의 점수 매기기 실험](./media/machine-learning-interpret-model-results/13.png)

그림 13. 자동차 가격 회귀 문제의 점수 매기기 실험

Hello 웹 서비스를 실행 hello 반환 결과 그림 14 같습니다. 이 차량에 대 한 예측된 가격 hello $15,085.52입니다.

![점수 매기기 모듈 테스트 해석](./media/machine-learning-interpret-model-results/13_1.png)

![점수 매기기 모듈 결과](./media/machine-learning-interpret-model-results/14.png)

그림 14. 자동차 가격 회귀 문제의 웹 서비스 결과

## <a name="clustering"></a>클러스터링
**예제 실험**

사용 hello Iris 데이터 집합 다시 toobuild 클러스터링 실험 합니다. 여기만 기능이 고 클러스터링에 사용할 수 있도록 아웃 hello 클래스 레이블을 hello 데이터 집합의 필터링 할 수 있습니다. 이 iris에서 대/소문자를 사용 하 여, 클러스터 toobe 두 hello 꽃을 클러스터링 하는 두 개의 클래스로 hello 학습 프로세스 중 hello 수를 지정 합니다. hello 실험 그림 15에 표시 됩니다.

![붓꽃 클러스터링 문제 실험](./media/machine-learning-interpret-model-results/15.png)

그림 15. 붓꽃 클러스터링 문제 실험

클러스터링 분류 점에서 다릅니다 hello 학습 데이터 집합에 단독으로 지상 검증 레이블이 없는 합니다. 클러스터링 그룹 hello 고유 클러스터인에 학습 데이터 집합 인스턴스. Hello 모델 레이블의 hello 학습 프로세스 중 해당 기능 간의 hello 차이점에 배웁니다 항목 hello 합니다. 그 후 hello 학습 된 모델을 사용할 있습니다 toofurther 이후 항목을 분류 합니다. 두 가지 방법으로 클러스터링 문제 내에서 필요한 hello 결과의 수입니다. hello 첫 번째 부분에는 hello 학습 데이터 집합, 레이블 지정은 및 hello 두 번째는 분류 hello 학습 된 모델에 새 데이터 집합입니다.

hello hello 결과의 첫 번째 부분 시각화할 수 hello 왼쪽의 출력 포트를 클릭 하 여 [클러스터링 모델 학습] [ train-clustering-model] 클릭 한 다음 **시각화**합니다. hello 시각화는 그림 16에 표시 됩니다.

![클러스터링 결과](./media/machine-learning-interpret-model-results/16.png)

그림 16. Hello 학습 데이터 집합에 대 한 결과 클러스터링 시각화

hello 학습 된 클러스터링 모델을 가진 새 항목이 클러스터링 hello 두 번째 파트의 hello 결과 17 그림에에서 표시 됩니다.

![클러스터링 결과 시각화](./media/machine-learning-interpret-model-results/17.png)

그림 17. 새 데이터 집합에 대한 클러스터링 결과 시각화

**결과 해석**

모양이 hello 두 부분의 hello 결과 서로 다른 실험 단계에서 형태소 분석, 있지만 동일 hello 및 hello에서 해석 되는 동일한 방식으로 합니다. hello 처음 네 개의 열은 기능입니다. 할당, hello 마지막 열은 hello 예측 결과입니다. 예측 된 고객 수가 hello 할당 된 항목 hello toobe hello 즉, 동일한 클러스터의 유사성 (hello 기본 유 클 리 디안 거리 메트릭을 사용 하 여이 실험) 어떤 방식으로든에서 공유 합니다. 클러스터 toobe 2의 hello 번호를 지정 하기 때문에 0 또는 1 할당의 hello 항목으로 표시 됩니다.

**웹 서비스 게시**

웹 서비스 실험 클러스터링 hello를 게시할 수 있으며 같은 방식으로 hello 2 클래스 분류에서 대/소문자를 사용 하 여 클러스터링 예측 hello에 대 한 호출 수 있습니다.

![붓꽃 클러스터링 문제 점수 매기기 실험](./media/machine-learning-interpret-model-results/18.png)

그림 18. 붓꽃 클러스터링 문제 점수 매기기 실험

Hello 웹 서비스를 실행 한 후 hello 그림 19 같이 결과 반환 합니다. 이 꽃 클러스터 0의에서 예측된 toobe입니다.

![점수 매기기 모듈 테스트 해석](./media/machine-learning-interpret-model-results/18_1.png)

![점수 매기기 모듈 결과](./media/machine-learning-interpret-model-results/19.png)

그림 19. 붓꽃 2클래스 분류의 웹 서비스 결과

## <a name="recommender-system"></a>추천 시스템
**예제 실험**

추천 시스템에 대 한 예를 들어 hello 식당 권장 사항 문제를 사용할 수 있습니다: 해당 등급 기록을 기반으로 하는 고객을 위한 식당을 권장할 수 있습니다. hello 입력된 데이터의 세 부분으로 구성 됩니다.

* 고객이 평가한 음식점 등급
* 고객 특징 데이터
* 음식점 기능 데이터

몇 가지 방법으로 hello로 해 [Matchbox 추천 학습] [ train-matchbox-recommender] Azure 기계 학습의 모듈:

* 지정된 사용자와 항목의 등급 예측
* 사용자 지정 항목 tooa 권장
* 사용자 지정 하는 사용자가 관련된 tooa 찾기
* 항목 관련된 tooa 항목 찾기

수행할 toodo hello에 4 hello 옵션 중에서 선택 하 여 선택할 수 있습니다 **추천 예측 종류** 메뉴. 여기서 네 개 시나리오를 모두 진행할 수 있습니다.

![매치박스 추천](./media/machine-learning-interpret-model-results/19_1.png)

추천 시스템의 일반적인 Azure Machine Learning 실험은 그림 20과 비슷합니다. 어떻게 toouse 해당 추천 시스템 모듈 참조에 대 한 내용은 [matchbox 추천 학습] [ train-matchbox-recommender] 및 [matchbox 추천 점수 매기기] [ score-matchbox-recommender].

![추천 시스템 실험](./media/machine-learning-interpret-model-results/20.png)

그림 20. 추천 시스템 실험

**결과 해석**

**지정된 사용자와 항목의 등급 예측**

선택 하 여 **등급 예측** 아래 **추천 예측 종류**, 지정 된 사용자와 항목에 대 한 등급 시스템 toopredict hello hello 추천이 요청 됩니다. 시각화의 hello hello [Matchbox 추천 점수 매기기] [ score-matchbox-recommender] 출력 그림 21은 같습니다.

![Hello 추천 시스템-등급 예측의 결과 점수를 매깁니다.](./media/machine-learning-interpret-model-results/21.png)

그림 21. 등급 예측 hello 추천 시스템의 hello 점수 결과 시각화

hello 처음 두 열은 hello 입력된 데이터에서 제공 하는 hello 사용자-항목 쌍입니다. hello 세 번째 열에 특정 항목에 대 한 사용자의 예측된 등급을 hello 됩니다. 예를 들어 hello 첫 번째 행 U1048가 고객 2로 toorate 식당 135026 예측 합니다.

**사용자 지정 항목 tooa 권장**

선택 하 여 **항목 추천** 아래 **추천 예측 종류**, 사용자 것을 요청 hello 추천 시스템 toorecommend 항목 tooa 사용자를 지정 합니다. 이 시나리오에서 마지막 매개 변수 toochoose hello는 *항목 선택 권장*합니다. 옵션 hello **(모델 평가 경우)에 대 한 항목에서 등급을 지정 하는 방법** 주로 hello 학습 프로세스 중 모델 평가 위한 것입니다. 이 예측 단계에서는 **모든 항목에서**를 선택합니다. 시각화의 hello hello [Matchbox 추천 점수 매기기] [ score-matchbox-recommender] 출력 그림 22 같습니다.

![추천 시스템 - 항목 추천의 점수 매기기 결과](./media/machine-learning-interpret-model-results/22.png)

그림 22. 항목 추천 hello 추천 시스템의 점수가 결과 시각화

hello 입력된 데이터에서 제공한 사용자 Id toorecommend 항목을 제공 하는 hello 6 열 나타냅니다 hello 중 첫 번째를 hello 합니다. hello 다른 5 개의 열 항목을 나타낼 hello toohello 사용자 관련성 내림차순에서 것이 좋습니다. 예를 들어 hello 첫 번째 행에 hello 가장 권장 U1048 고객에 대 한 식당은 차례로 135018, 134975, 135021, 132862 134986 합니다.

**사용자 지정 하는 사용자가 관련된 tooa 찾기**

선택 하 여 **관련 사용자** 아래 **추천 예측 종류**, 사용자 것을 요청 hello 추천 시스템 toofind 관련된 사용자 지정 tooa 사용자입니다. 관련된 사용자는 hello 사용자 기본 설정이 비슷한가 있습니다. 이 시나리오에서 마지막 매개 변수 toochoose hello는 *관련 사용자 선택*합니다. 옵션 hello **에서 사용자가 항목 등급을 지정한 (모델 평가 위해)** 주로 hello 학습 프로세스 중 모델 평가 위한 것입니다. 이 예측 단계에서는 **모든 사용자로부터**를 선택합니다. 시각화의 hello hello [Matchbox 추천 점수 매기기] [ score-matchbox-recommender] 출력 그림 23 같습니다.

![추천 시스템 - 관련 사용자의 점수 매기기 결과](./media/machine-learning-interpret-model-results/23.png)

그림 23. 관련된 사용자 hello 추천 시스템의 점수 결과 시각화

먼저 hello의 사용자 Id 필요한 toofind 제공 hello 6 열 표시 hello와 관련 된 사용자 입력된 데이터에서 제공 합니다. hello 다른 5 개의 열 저장소 hello 관련성 내림차순에서 hello 사용자의 관련된 사용자 예측된 합니다. 예를 들어 hello 첫 번째 행에 U1048 고객에 대 한 hello 관련성이 가장 높은 고객은 차례로 U1066, U1044, U1017, U1072 U1051 합니다.

**항목 관련된 tooa 항목 찾기**

선택 하 여 **관련 항목** 아래 **추천 예측 종류**, hello 추천 시스템 toofind 관련된 항목 제공 tooa 항목이 요청 됩니다. 관련 항목은 동일 하 여 hello hello 항목 가능성이 가장 높은 toobe 빴 사용자입니다. 이 시나리오에서 마지막 매개 변수 toochoose hello는 *항목 선택 관련*합니다. 옵션 hello **(모델 평가 경우)에 대 한 항목에서 등급을 지정 하는 방법** 주로 hello 학습 프로세스 중 모델 평가 위한 것입니다. 이 예측 단계에서는 **모든 항목에서** 를 선택합니다. 시각화의 hello hello [Matchbox 추천 점수 매기기] [ score-matchbox-recommender] 출력 그림 24 같습니다.

![추천 시스템 - 관련 항목의 점수 매기기 결과](./media/machine-learning-interpret-model-results/24.png)

그림 24. 관련된 항목 hello 추천 시스템의 점수 결과 시각화

필요한 항목 Id를 지정 하는 hello 6 열 나타냅니다 hello 중 첫 번째 hello toofind 관련 항목을 hello 입력된 데이터에서 제공 합니다. hello 다른 5 개의 열 저장소 hello 관련성 기준으로 내림차순으로 hello 항목의 관련된 항목을 예측된 합니다. 예를 들어 hello 첫 번째 행 135026 항목에 대 한 hello 관련성이 가장 높은 항목 차례로 135035, 132875, 135055, 134992 135074은 됩니다.

**웹 서비스 게시**

다음이 실험을 웹 서비스 tooget 예측으로 게시 하는 hello 프로세스는 각각 hello 네 가지 시나리오에 대해 비슷합니다. 여기 예를 들어 hello 두 번째 시나리오 (권장 되는 항목 tooa 사용자 지정)를 수행 합니다. 참고할 수 세 개의 다른 hello와 동일한 절차를 hello 합니다.

저장 하는 hello 추천 시스템 학습된 된 모델을 학습 하 고 hello 입력된 데이터 tooa 필터링 단일 사용자 ID 열으로 요청을 그림 25에서와 같이 hello 실험을 연결 하 고 웹 서비스로 게시할 수 있습니다.

![Hello 식당 권장 문제의 실험 점수 매기기](./media/machine-learning-interpret-model-results/25.png)

그림 25. Hello 식당 권장 문제의 실험 점수 매기기

Hello 웹 서비스를 실행 hello 반환 결과 그림 26 같습니다. U1048 사용자에 대 한 hello 5 개 권장된 레스토랑은 134986 "," 135018 "," 134975 "," 135021, "및" 132862 합니다.

![추천 시스템 서비스의 샘플](./media/machine-learning-interpret-model-results/25_1.png)

![샘플 실험 결과](./media/machine-learning-interpret-model-results/26.png)

그림 26. 음식점 추천 문제의 웹 서비스 결과

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
