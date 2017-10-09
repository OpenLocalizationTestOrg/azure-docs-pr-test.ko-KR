---
title: "hello 팀 데이터 과학 프로세스의에서 aaaFeature 선택 | Microsoft Docs"
description: "기능 선택의 hello 용도 설명 하 고 기계 학습의 hello 데이터 향상 프로세스에서 해당 역할의 예를 제공 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 878541f5-1df8-4368-889a-ced6852aba47
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: 54af93c83e4cc6a3670b3ad62490e0f74082b4ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-selection-in-hello-team-data-science-process-tdsp"></a>Hello 팀 데이터 과학 프로세스 (TDSP)의 기능 선택
이 문서는 기능 선택의 hello 목적에 설명 하 고 기계 학습의 hello 데이터 향상 프로세스에서 해당 역할의 예제를 제공 합니다. 이들 예는 Azure 기계 학습 스튜디오에서 가져온 것입니다. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

기능 선택은 hello 팀 데이터 과학 프로세스 (TDSP)이 설명에 한 부분 및 엔지니어링 hello [hello 팀 데이터 과학 프로세스는 무엇입니까?](data-science-process-overview.md)합니다. 기능 엔지니어링 및 선택 hello의 일부는 **기능 개발** hello TDSP의 단계입니다.

* **엔지니어링 기능**:이 프로세스에서 hello 데이터 및 tooincrease 예측 력이 toohello 학습 알고리즘의 기존 원시 기능 hello toocreate 추가 관련 기능을 시도 합니다.
* **기능 선택**:이 프로세스 hello 학습 문제의 시도 tooreduce hello 차원에서 원래 데이터 기능의 hello 키 하위 집합을 선택 합니다.

일반적으로 **엔지니어링 기능** 적용 된 첫 번째 toogenerate 추가 기능을 고 hello **기능 선택** 단계는 수행된 된 tooeliminate 관련이 없는, 중복 또는 밀접 기능입니다.

## <a name="filtering-features-from-your-data---feature-selection"></a>데이터에서 기능 필터링 - 기능 선택
기능 선택은 일반적으로 분류 또는 회귀 작업 같은 예측 모델링 태스크에 대 한 학습 데이터 집합의 hello 구축을 위한 적용 되는 프로세스입니다. hello 목표 tooselect hello 데이터에서 기능 toorepresent hello 분산의 최대 크기의 최소 집합을 사용 하 여 크기를 축소 하는 hello 원래 데이터 집합에서 hello 기능 하위 집합입니다. 이 기능의 하위이 집합은 다음 hello 유일한 기능 toobe tootrain hello 모델을 포함 합니다. 기능 선택은 두 가지 기본 용도로 사용됩니다.

* 첫째 기능 선택을 수행하면 관련이 없는 중복된 기능이나 고도로 상관된 기능을 제거하여 분류 정확도를 높입니다.
* 둘째, 모델 학습 프로세스를 보다 효율적으로 수 있는 기능의 hello 수를 줄입니다. 지원 벡터 컴퓨터 같은 비용이 많이 드는 tootrain 않은 학습자에 특히 유용 합니다.

기능 선택 hello 사용 된 데이터 집합 tootrain hello 모델의 기능 tooreduce hello 수 찾기지 않습니다 이지만 하지 일반적으로 hello 용어 "차원 감소" tooby 참조 합니다. 기능 선택 방법을 변경 하지 않은 hello 데이터의 원래 기능 하위 집합을 추출 합니다.  차원성 감소 방법을 hello 초기 기능을 변환 하 고 있으므로 수정할 수 있는 엔지니어링된 기능을 사용 합니다. 차원 수 감소 메서드의 예로는 주성분 분석, 표준 상관 분석 및 특이값 분해가 있습니다.

그중에서도 감독된 컨텍스트에서 가장 널리 적용되는 기능 선택 메서드 범주는 “필터 기반 기능 선택"이라고 합니다. 각 기능 및 hello 대상 특성 간의 hello 상관 관계를 평가 하 여 이러한 메서드는 통계 측정값 tooassign 점수 tooeach 기능을 적용 합니다. hello 기능에서는 다음 유지 하거나 특정 기능 제거에 대 한 사용된 toohelp 집합 hello 임계값 수 있는 hello 점수에 의해 순위를 지정 합니다. 이러한 방법에 사용 된 hello 통계 측정값의 예로 사용자 상관 관계, 상호 정보 및 카이 제곱된 테스트 hello 들 수 있습니다.

Azure 기계 학습 스튜디오에서는 기능 선택에 제공되는 모듈이 있습니다. 이러한 모듈에는 hello 다음 그림에에서 나와 있는 것 처럼 [필터 기반 기능 선택] [ filter-based-feature-selection] 및 [피셔 선형 판별 분석] [ fisher-linear-discriminant-analysis].

![기능 선택 예](./media/machine-learning-data-science-select-features/feature-Selection.png)

예를 들어, hello hello 사용 [필터 기반 기능 선택] [ filter-based-feature-selection] 모듈입니다. Hello 편의 위해 위에서 설명한 toouse hello 텍스트 마이닝 예제를 계속 실행 합니다. 회귀 모델 256 기능 집합을 이후 hello 통해 만드는 toobuild 한다고 가정 [기능 해시] [ feature-hashing] 모듈 및 해당 hello 응답 변수는 "Col1" hello 및 책을 나타냅니다. 1 too5에서 사이인 등급을 검토 합니다. "기능 점수 매기기 방법" toobe "피어슨 상관 관계"를 설정 하 여 "대상 열" toobe "Col1" 및 "원하는 기능의 수" too50 hello hello 합니다. 다음 hello 모듈 [필터 기반 기능 선택] [ filter-based-feature-selection] hello 대상 특성 "Col1"와 함께 50 기능을 포함 하는 데이터 집합을 생성 합니다. hello 다음이 실험에서는 hello 흐름 알아보고 hello 지금까지 언급 된 입력된 매개 변수.

![기능 선택 예](./media/machine-learning-data-science-select-features/feature-Selection1.png)

hello 다음 그림은 hello 결과 데이터 집합. 각 기능은 점수를 기준으로 hello 자체 간의 피어슨 상관 관계에 있으며 대상 특성 "Col1" hello 합니다. 최고 점수와 hello 기능이 유지 됩니다.

![기능 선택 예](./media/machine-learning-data-science-select-features/feature-Selection2.png)

선택한 hello 기능의 hello 해당 점수는 hello 다음 그림에에서 표시 됩니다.

![기능 선택 예](./media/machine-learning-data-science-select-features/feature-Selection3.png)

이 적용 하 여 [필터 기반 기능 선택] [ filter-based-feature-selection] 모듈을 50의 256 hello 대상 변수로 "Col1" 상관 관계가 지정 된 기능에 가장를 hello 있어야 하기 때문에 기능을 선택한 hello 점수 매기기에 따라 "피어슨 상관 관계" 메서드입니다.

## <a name="conclusion"></a>결론
기능 엔지니어링 및 기능 선택은 일반적으로 엔지니어링 및 선택한 기능 hello 데이터에 포함 된 tooextract hello 키 정보를 시도 하는 프로세스를 학습 하는 hello의 hello 효율성을 높입니다. 이러한 모델 tooclassify hello 입력된 데이터의 hello 거듭제곱을 정확 하 게 향상 시킬 및 toopredict 결과 관심 더 강력 하 게 합니다. 기능 엔지니어링 및 선택 toomake hello 학습 더 계산 tractable 결합할 수도 있습니다. 이 작업을 수행 하 여 향상 하 고 toocalibrate 또는 모델을 학습 필요 hello 기능 수를 줄이면 합니다. Hello 기능 선택한 tootrain hello 모델에 최소한의 hello 데이터의 hello 패턴을 설명 하 고 다음 결과 성공적으로 예측 하는 독립 변수 집합은 수학적으로 말하자면, 있습니다.

Note 아닌지 항상 반드시 tooperform 기능 엔지니어링 이나 기능 선택 합니다. 또는 필요한 지 여부 또는 수집 hello 알고리즘을 선택 했으며 hello 실험의 hello hello 데이터에 따라 달라 집니다.

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

