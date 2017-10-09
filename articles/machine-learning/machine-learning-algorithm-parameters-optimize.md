---
title: "aaaOptimize Azure 기계 학습에서 알고리즘 | Microsoft Docs"
description: "Azure 기계 학습에서 알고리즘에 대 한 toochoose hello 최적의 매개 변수 설정 하는 방법에 대해 설명 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a>Azure 기계 학습에서 매개 변수 toooptimize 알고리즘을 선택 합니다.
이 항목에서는 Azure 기계 학습에서 알고리즘에 대 한 toochoose hello 오른쪽 hyperparameter 설정 하는 방법을 설명 합니다. 대부분 기계 학습 알고리즘 매개 변수 tooset이 있어야 합니다. 모델을 학습 하는 경우 해당 매개 변수에 대 한 tooprovide 값이 있어야 합니다. hello 학습 된 모델의 hello 효율성 hello 모델 매개 변수를 선택 하면에 따라 달라 집니다. hello hello 최적의 매개 변수 집합을 찾는 작업 이라고 *선택 모델*합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

다양 한 방법으로 toodo 모델 선택이 있습니다. 기계 학습에서 교차 유효성 검사는 모델 선택에 대 한 hello 가장 널리 사용 되는 메서드 중 하나 이므로 Azure 기계 학습에서 hello 기본 모델 선택 메커니즘. Azure Machine Learning에서는 R과 Python을 둘 다 지원하므로 언제든지 R 또는 Python을 사용하여 고유한 모델 선택 메커니즘을 구현할 수 있습니다.

Hello hello 최상의 매개 변수 집합을 찾는 과정에서 네 단계는

1. **Hello 매개 변수 공간 정의**: hello 알고리즘에 대 한 hello 정확한 매개 변수 값을 원하는 tooconsider 먼저 결정 합니다.
2. **Hello 교차 유효성 검사 설정을 정의 합니다.**: toochoose 교차 유효성 검사 hello 데이터 집합에 대 한 정리 하는 방법을 결정 합니다.
3. **Hello 메트릭을 정의**: hello 최상의 집합이 정확도 등의 매개 변수를 확인 하기 위한 어떤 메트릭 toouse 결정, 오류, 정밀도, 회수, 또는 f-점수 제곱 평균입니다.
4. **학습, 평가 및 비교**: hello 매개 변수 값의 각 고유 조합에 대 한 교차 유효성 검사에 의해 수행 이며 hello 오류 메트릭을 정의한 기반 합니다. 평가 후 비교, hello 최고 성능의 모델을 선택할 수 있습니다.

다음 이미지는 hello Azure 기계 학습에서 수행할 수 있습니다 어떻게 표시를 보여 줍니다.

![Hello 최상의 매개 변수 집합 찾기](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a>Hello 매개 변수 공간 정의
Hello 모델 초기화 단계에서 설정 하는 hello 매개 변수를 정의할 수 있습니다. hello 모든 기계 학습 알고리즘의 매개 변수 창에 두 가지 트레이너 모드: *단일 매개 변수* 및 *매개 변수 범위*합니다. 매개 변수 범위 모드를 선택합니다. 매개 변수 범위 모드에서는 각 매개 변수에 대한 여러 값을 입력할 수 있습니다. Hello 텍스트 상자에 쉼표로 구분 된 값을 입력할 수 있습니다.

![2클래스 향상된 의사 결정 트리, 단일 매개 변수](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 Hello 최대 및 최소 포인트 hello 그리드 및 hello 포인트 toobe로 생성 된 총 수를 정의할 수 있습니다 또는 **범위 작성기를 사용 하 여**합니다. 기본적으로 hello 매개 변수 값은 선형 눈금에 생성 됩니다. 그러나 **로그 눈금 간격이** 을 선택 하면 hello 값 hello 로그 눈금에 생성 됩니다 (즉, hello의 hello 포인트가입니다 개의 대신 상수). 정수 매개 변수의 경우 하이픈을 사용하여 범위를 정의할 수 있습니다. 예를 들어, "1-10"은 1과 10 사이의 모든 정수 hello 매개 변수 집합을 이루는 (둘 다 포함). 혼합 모드도 지원됩니다. 예를 들어, 매개 변수 집합을 hello "1-10, 20, 50" 정수 1-10, 20, 포함 및 50 합니다.

![2클래스 향상된 의사 결정 트리, 매개 변수 범위](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a>교차 유효성 검사 접기 정의
hello [분할 및 샘플링] [ partition-and-sample] 모듈에 사용 되는 toorandomly 할당 접기 toohello 데이터 일 수 있습니다. 같은 hello 모듈에 대 한 샘플 구성이 hello,에서는 5 개의 접기를 정의 하 고 접기 번호 toohello 샘플 인스턴스를 임의로 할당 합니다.

![파티션 및 샘플](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a>Hello 메트릭 정의
hello [모델 하이퍼 튜닝] [ tune-model-hyperparameters] 모듈 실험적으로 hello 최상의 매개 변수 집합을 지정 된 알고리즘 및 데이터 집합에 대 한 선택에 대 한 지원을 제공 합니다. 또한 학습 hello에 대 한 tooother 정보 모델을 hello **속성** 이 모듈의 창 hello 측정 하는 hello 최상의 매개 변수 집합을 포함 합니다. 분류 및 회귀 알고리즘 각각에 대한 두 개의 드롭다운 목록 상자가 있습니다. 회귀 메트릭 hello 분류 알고리즘 고려 대상인 hello 알고리즘을 사용 하는 경우 무시 됩니다 하며 그 반대 과정도 수행 합니다. 이 특정 예제 hello 메트릭을 **정확도**합니다.   

![매개 변수 비우기](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a>학습, 평가 및 비교
동일한 hello [모델 하이퍼 튜닝] [ tune-model-hyperparameters] 다양 한 메트릭을 평가 다음 hello hello를 기반으로 가장 학습 된 모델을 만듭니다 toohello 매개 변수 집합을 해당 하는 모든 hello 모델을 학습 하는 모듈 선택한 메트릭입니다. 이 모듈에는 다음 두 개의 필수 입력이 있습니다.

* 학습 되지 않은 학습자 hello
* hello 데이터 집합

hello 모듈에는 선택적 입력 데이터 집합을 있습니다. 접기 정보 toohello 필수 데이터 집합 입력으로 hello 데이터 집합을 연결 합니다. Hello 데이터 집합에 모든 접기 정보 할당 되지 않은 경우 기본적으로는 10 배로 교차 유효성 검사 실행 자동으로 됩니다. Hello 접기 할당에 작업이 수행 되지 않습니다 및 유효성 검사 데이터 집합 hello 선택적 데이터 집합 포트에서 제공 되며, 다음 학습 테스트 모드 선택 되 고 hello 첫 번째 데이터 집합은 각 매개 변수 조합에 대해 사용 되는 tootrain hello 모델입니다.

![향상된 의사 결정 트리 분류자](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

hello 모델 hello 유효성 검사 데이터 집합에 대해 평가 됩니다. hello 매개 변수 값의 함수로 hello 모듈의 출력 포트 가지 다른 메트릭으로 남아 있습니다. hello toohello 최고 성능의 모델 toohello 메트릭 선택에 따라 해당 하는 hello 학습 된 모델을 제공 하는 출력 포트 오른쪽 (**정확도** 이 경우).  

![유효성 검사 데이터 집합](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

Hello 오른쪽 출력 포트를 시각화가 선택한 hello 정확한 매개 변수를 볼 수 있습니다. 이 모델은 테스트 집합을 채점하거나 학습된 모델로 저장한 후 조작 가능한 웹 서비스를 제공하는 데 사용될 수 있습니다.

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
