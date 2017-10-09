---
title: "aaaFeature 엔지니어링 및 Azure 기계 학습에서 선택 | Microsoft Docs"
description: "기능 선택 및 기능 엔지니어링의 hello 목적에 설명 하 고 기계 학습의 hello 데이터 향상 프로세스에서 해당 역할의 예를 제공 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ceb524d-842e-4f77-9eae-a18e599442d6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: zhangya;bradsev
ROBOTS: NOINDEX
redirect_url: machine-learning-data-science-create-features
redirect_document_id: True
ms.openlocfilehash: e3e59329bf46f334396f5975b4e656137362d7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Azure 기계 학습의 기능 엔지니어링 및 선택
이 기능 엔지니어링 및 기계 학습의 hello 데이터 개선 프로세스의 기능 선택의 hello 목적으로 설명합니다. Azure Machine Learning 스튜디오에서 제공하는 예제를 사용하여 이러한 프로세스와 관련된 내용을 설명합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

기계 학습에서 사용 되는 hello 학습 데이터 hello 선택 영역이 나 hello 수집 되는 원시 데이터에서 기능 추출 종종 향상 될 수 있습니다. Hello 원시 비트 배포 데이터에서 필기 문자의 tooclassify hello 이미지는 방법을 학습의 hello 컨텍스트에서 엔지니어링 기능의 예로 비트 밀도 지도 구성 됩니다. 이 맵은 hello 문자의 hello 가장자리 hello 원시 배포 보다 더 효율적으로 찾을 수 있습니다.

엔지니어링 및 선택한 기능 hello 데이터에 포함 된 tooextract hello 키 정보를 시도 하는 hello 학습 프로세스의 hello 효율성을 향상 합니다. 이러한 모델 tooclassify hello 입력된 데이터의 hello 거듭제곱을 정확 하 게 향상 시킬 및 toopredict 결과 관심 더 강력 하 게 합니다. 기능 엔지니어링 및 선택 toomake hello 학습 더 계산 tractable 결합할 수도 있습니다. 이 작업을 수행 하 여 향상 하 고 toocalibrate 또는 모델을 학습 필요 hello 기능 수를 줄이면 합니다. Hello 기능 선택한 tootrain hello 모델에 최소한의 hello 데이터의 hello 패턴을 설명 하 고 다음 결과 성공적으로 예측 하는 독립 변수 집합은 수학적으로 말하자면, 있습니다.

hello 엔지니어링 및 기능 선택은 일반적으로 네 단계로 구성 되는 대규모 프로세스의 한 부분.

* 데이터 수집
* 데이터 향상
* 모델 생성
* 후처리

엔지니어링 및 선택 기계 학습의 hello 데이터 개선 단계를 구성 합니다. 이 프로세스의 세 가지 요소는 목적에 따라 다음과 같이 구별할 수 있습니다.

* **데이터 사전 처리**:이 프로세스 수집 된 데이터를 hello 시도 tooensure 명확 하 고 일관 됩니다. 여러 데이터 집합 통합, 누락된 데이터 처리, 일관되지 않은 데이터 처리 및 데이터 유형 변환과 같은 작업이 포함됩니다.
* **엔지니어링 기능**:이 프로세스가 hello hello 데이터와 tooincrease 예측 력이 toohello 학습 알고리즘의에서 기존 원시 기능에서 toocreate 추가 관련 기능을 시도 합니다.
* **기능 선택**:이 프로세스에서는 hello 학습 문제의 원래 데이터 기능 tooreduce hello 차원 hello 키 일부를 선택 합니다.

이 항목에서는 hello 데이터 향상 프로세스의 hello 기능 엔지니어링 및 기능 선택 측면에 대해서만 다룹니다. Hello 데이터 전처리 단계에 대 한 자세한 내용은 참조 하십시오. [Azure 기계 학습 스튜디오에서 데이터를 전처리](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/)합니다.

## <a name="creating-features-from-your-data--feature-engineering"></a>데이터에서 기능 만들기--기능 엔지니어링
hello 학습 데이터 행렬 (레코드 또는 행에 저장 된 관측 치를) 예제는 구성 하며 각각의 기능 (변수 또는 열에 저장 된 필드) 집합으로 이루어져 있습니다. hello hello 실험적 디자인에 지정 된 기능은 hello 데이터의 예상된 toocharacterize hello 패턴입니다. 선택한 기능 사용 되는 집합 tootrain 모델을 hello 다양 한 hello 원시 데이터 필드에 직접 포함 될 수 있지만 추가 엔지니어링된 기능 toobe hello 원시 데이터 toogenerate 향상 된 학습 데이터 집합의에서 hello 기능에서 생성 된 필요한 경우가 많습니다.

모델을 학습 하는 경우 어떤 유형의 기능 tooenhance hello 데이터 집합을 생성 해야? Hello 교육을 향상 시키는 엔지니어링된 기능 hello 데이터의 hello 패턴을 더 잘 구분할 수 있는 정보를 제공 합니다. Hello 새 기능 tooprovide 추가 정보를 기대 명확 하 게 캡처된 또는 원래 hello에 명백 하지 않은 또는 기존 기능 설정 했지만이 프로세스는 아트 만들어집니다. 안정되고 생산성이 있는 결정을 내리려면 도메인에 대한 전문 지식이 필요한 경우가 많습니다.

Azure 기계 학습을 시작할 때 기계 학습 스튜디오에 제공 된 샘플을 사용 하 여 구체적으로이 프로세스는 가장 쉬운 toograsp 됩니다. 다음은 제공되는 두 가지 예입니다.

* 회귀 예제 ([자전거 여 hello 수의 예측](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) hello 대상 값은 알려진 하는 감독 된 실험에서
* [기능 해싱][feature-hashing]을 사용하는 텍스트 마이닝 분류 예제

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>예 1: 회귀 모델을 위해 시간 기능 추가
toodemonstrate는 tooengineer 회귀 작업에 대 한 기능을 어떻게 사용 hello 실험 "수요 예측 자전거의" Azure 기계 학습 스튜디오에서 합니다. hello이이 실험은 hello 자전거, 자전거 여 내 특정 월, 일 또는 시간인 hello 수,에 대 한 toopredict hello 요구 합니다. 데이터 집합 hello **자전거 임대 UCI 데이터 집합** hello 원시 입력 데이터로 사용 됩니다.

이 데이터 집합 hello hello 미국에에서 워싱턴 DC에서 자전거 임대 네트워크를 유지 하는 대문자 자전거 공유 회사에서에서 실제 데이터를 기반으로 합니다. hello 데이터 집합 자전거 여 hello 수는 하루 중 특정 시간 내에서 2011 too2012 나타내며 17379 행과 17 열을 포함 합니다. 날씨 조건 (온도, 습도, 풍속) 및 (공휴일 또는 평일) hello 날짜 hello 종류 hello 원시 기능 집합에 포함 되어 있습니다. hello 필드 toopredict은 **cnt**, 개수는 특정 시간 내에서 hello 자전거 대 여 나타내며 1 too977에서 사이의 정수입니다.

tooconstruct hello 학습 데이터의 효과적인 기능을 4 개의 회귀 모델이 hello를 사용 하 여 생성 된 동일한 알고리즘을 이지만 네 개의 서로 다른 학습 데이터 집합입니다. 4 hello 데이터 집합을 나타내는 원시 입력된 데이터를 동일한 hello 되지만 기능의 증가 함에 설정은. 이러한 기능은 다음 네 가지 범주로 그룹화됩니다.

1. A = 날씨 + 휴일 + 평일 + hello 예측 된 날에 대 한 주말 기능
2. B = 12 시간 동안 이전 각 hello 임대 된 자전거 수
3. C = 된 임대 각 hello hello에 12 일 이전 동일 자전거 수 시간
4. D = 된 임대 각 hello hello에 12 일로, 이전 동일 자전거 수 시간 및 hello 같은 날

Hello 원래 원시 데이터에 이미 존재, 기능 집합 A 외에도 hello 다른 세 가지 기능을 만듭니다 hello 기능 엔지니어링 프로세스. 기능 B 캡처 hello hello 자전거에 대 한 최근 요청을 설정합니다. 기능 C 캡처 자전거에 대 한 hello 요구 한 특정 시간에 설정합니다. 특정 시간 및 특정 요일 hello 자전거에 대 한 캡처 수요가 D를 설정 하는 기능. 각각 4 hello 학습 데이터 집합의 포함 기능 집합 A "," A + B "," A + B + C "및" A + B + C + D, 각각.

Azure 기계 학습 실험 hello에 hello 미리 처리 된 입력된 데이터 집합에서 4 개의 분기를 통해 이러한 4 개의 학습 데이터 집합을 구성 합니다. 이러한 분기 중 각각가 포함 된 hello 맨 왼쪽 분기를 제외 하 고는 [R 스크립트 실행] [ execute-r-script] 집합이 있는 (기능 B, C 및 D 설정) 하는 기능을 파생 모듈 각각 구현 되 고 추가 toohello는 데이터 집합을 가져옵니다. hello 다음 그림 hello 두 번째 왼쪽된 분기 toocreate 기능 집합 B hello R 스크립트를 사용 하는 방법을 보여 줍니다.

![기능 집합 만들기](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

hello 다음 표에 요약 되어 hello 4 개의 모델의 hello 성능 결과의 hello 비교 합니다. 최상의 결과 얻으려면 hello A + B + C 기능으로 표시 됩니다. 추가 기능 집합 hello 학습 데이터에 포함 되 면 해당 hello 오류율 감소 note 합니다. 이 확인 B와 C hello 회귀 작업에 대 한 추가 관련 정보를 제공 하는 기능 집합을 hello 우리의 가정 합니다. Hello D 기능 집합을 추가 하지 않는 것 tooprovide hello 오류율 추가 감소 합니다.

![성능 결과 비교](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a> 예 2: 텍스트 마이닝에 기능 만들기
기능 엔지니어링 마이닝, 문서 분류 및 감성 분석 등 작업 관련된 tootext에서 광범위 하 게 적용 됩니다. 예를 들어 여러 범주로 tooclassify 문서를 사용할 때 일반적인 가정은 hello 단어 또는 구를 하나의 문서 범주에 포함 된 않는다는 다른 문서 범주에 가능성이 더 낮아집니다 toooccur입니다. 즉, hello hello 단어 또는 구를 분포의 빈도가 수 toocharacterize 다른 문서 범주입니다. 텍스트 마이닝 응용 프로그램에서는 hello 엔지니어링 프로세스 기능은 개별 항목의 텍스트 내용을 일반적으로 역할을 하므로 입력된 데이터 hello 때문에 단어 또는 구를 주파수와 관련 된 필요한 toocreate hello 기능 합니다.

tooachieve이 작업을 호출 하는 기술을 *기능 해시* 가 적용 된 tooefficiently 인덱스에 임의의 텍스트 형식 기능을 설정 합니다. 대신 각 텍스트 기능 (단어 또는 구를) tooa 특정 인덱스, 해시 함수 toohello 기능을 적용 하 여 및 직접 인덱스로 해당 해시 값을 사용 하 여이 메서드 함수를 연결 합니다.

Azure Machine Learning에는 이러한 단어 또는 문구 기능을 편리하게 생성하는 [기능 해싱][feature-hashing] 모듈이 있습니다. hello 다음 그림은이 모듈을 사용 하는 예제. 두 개의 열을 포함 하는 hello 입력된 데이터 집합: hello 책 등급 1 too5 및 hello 실제 검토 콘텐츠에서 사이의 값입니다. 이 hello 목표 [기능 해시] [ feature-hashing] 모듈은 tooretrieve hello 특정 우수에서 hello 해당 단어 또는 구를의 hello 발생 빈도 표시 하는 새로운 기능입니다. toouse toocomplete hello 단계를 수행 해야이 모듈:

1. Hello 입력된 텍스트가 포함 된 select hello 열 (**Col2** 이 예에서).
2. 설정 *해시 비트 크기* too8 즉, 2 ^8 = 256 기능 만들어집니다. hello hello 텍스트에서 단어 또는 구를 다음 too256 인덱스 해시 됩니다. 매개 변수를 hello *해시 비트 크기* 범위는 1 too31에서 합니다. Hello 매개 변수 설정 tooa 더 큰 숫자를 hello 단어 또는 구를 가능성이 낮습니다 toobe 해시 hello에 동일한 인덱스입니다.
3. Hello 매개 변수를 설정 *N 그램* too2 합니다. Hello 입력된 텍스트에서 그램이 (모든 단일 단어에 대 한 기능) 유 니 그램과 바이 (인접 한 단어의 모든 쌍에 대 한 기능)의 발생 빈도 hello를 검색 합니다. 매개 변수를 hello *N 그램* hello 순차적 단어 toobe 기능에 포함 된 최대 수를 나타내는 0 too10 범위입니다.  

![기능 해싱 모듈](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

hello 다음 그림은 이러한 새 기능은 표시 되는 같습니다.

![기능 해싱 예제](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>데이터에서 기능 필터링--기능 선택
*기능 선택* 일반적으로 된 프로세스를 적용할 분류 또는 회귀 작업 같은 예측 모델링 태스크에 대 한 학습 데이터 집합의 toohello 생성입니다. hello 목표 tooselect hello 데이터에서 기능 toorepresent hello 분산의 최대 크기의 최소 집합을 사용 하 여 크기를 줄여 주는 hello 원래 데이터 집합에서 hello 기능의 하위 집합입니다. 이 하위 집합의 기능 hello 전용 기능 포함 toobe tootrain hello 모델을 포함합니다. 기능 선택은 두 가지 기본 용도로 사용됩니다.

* 기능 선택을 수행하면 관련이 없는 중복된 기능이나 고도로 상관된 기능을 제거하여 분류 정확도를 높입니다.
* 기능 선택은 감소 hello 여러 가지 기능을 하면 hello 모델 학습 프로세스를 보다 효율적입니다. 지원 벡터 컴퓨터 같은 비용이 많이 드는 tootrain 않은 학습자에 특히 유용 합니다.

기능 선택 tooreduce hello hello 사용 되는 데이터 집합 tootrain hello 모델의 기능 수를 검색 하지만 일반적으로 tooby hello 용어를 참조 *차원 감소 합니다.* 기능 선택 방법을 변경 하지 않은 hello 데이터의 원래 기능 하위 집합을 추출 합니다.  차원성 감소 방법을 hello 초기 기능을 변환 하 고 있으므로 수정할 수 있는 엔지니어링된 기능을 사용 합니다. 차원 수 감소 메서드의 예로는 주성분 분석, 표준 상관 분석 및 특이값 분해가 있습니다.

감독된 컨텍스트에서 가장 널리 적용되는 기능 선택 메서드 범주는 필터 기반 기능 선택입니다. 각 기능 및 hello 대상 특성 간의 hello 상관 관계를 평가 하 여 이러한 메서드는 통계 측정값 tooassign 점수 tooeach 기능을 적용 합니다. hello 기능은 다음을 기준으로 사용할 수 있는 hello 점수 tooset hello 임계값을 유지 하거나 특정 기능을 제거 합니다. 이러한 방법에 사용 된 hello 통계 측정값의 예로 피어슨 상관 관계, 상호 정보 및 카이 제곱 검정 hello 들 수 있습니다.

Azure Machine Learning 스튜디오에서는 기능 선택의 모듈을 제공합니다. 이러한 모듈에는 hello 다음 그림에에서 나와 있는 것 처럼 [필터 기반 기능 선택] [ filter-based-feature-selection] 및 [피셔 선형 판별 분석] [ fisher-linear-discriminant-analysis].

![기능 선택 예](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

예를 들어 hello를 사용 하 여 [필터 기반 기능 선택] [ filter-based-feature-selection] 앞부분에 설명 된 hello 텍스트 마이닝 예제를 사용 하 여 모듈입니다. 한다고 가정 toobuild 회귀 모델은 256 기능 집합이 hello를 통해 만들어진 후 [기능 해시] [ feature-hashing] 모듈 및 해당 hello 응답 변수는 **Col1**책을 나타내는 등급 1 too5에서 범위의 검토 합니다. 설정 **기능 점수 매기기 방법** 너무**피어슨 상관 관계**, **대상 열** 너무**Col1**, 및 **수가 필요한 기능** 너무**50**합니다. hello 모듈 [필터 기반 기능 선택] [ filter-based-feature-selection] hello 대상 특성와 함께 50 기능을 포함 하는 데이터 집합을 생성 한 다음 **Col1**합니다. hello 다음이 실험에서는 hello 흐름 알아보고 hello 입력된 매개 변수.

![기능 선택 예](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

hello 다음 그림은 hello 결과 데이터 집합. 각 기능 hello 자신과 hello 사이의 피어슨 상관 관계를 기반으로 점수는 대상 특성 **Col1**합니다. 최고 점수와 hello 기능이 유지 됩니다.

![필터 기반 기능 선택 데이터 집합](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

다음 그림에서는 hello hello 해당 점수 hello 선택 기능입니다.

![선택한 기능 점수](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

이 적용 하 여 [필터 기반 기능 선택] [ filter-based-feature-selection] 모듈을 50의 256 기능을 대부분의 기능은 hello 대상 변수 상호 연관 hello 했기 때문에 선택한 **Col1** hello 점수 매기기 방법에 따라 **피어슨 상관 관계**합니다.

## <a name="conclusion"></a>결론
기능 엔지니어링 및 기능 선택 기계 학습 모델을 작성할 때 다음 두 단계로 tooprepare hello 학습 데이터에서 일반적 수행 됩니다. 일반적으로 기능 엔지니어링이 적용 된 첫 번째 toogenerate 추가 기능을 한 다음 hello 기능 선택 단계 수행된 tooeliminate 관련이 없는, 중복 또는 밀접된 기능.

필요는 없습니다 항상 tooperform 기능 엔지니어링 이나 기능 선택 합니다. 필요한 지 여부 또는 hello 알고리즘을 선택 하면를 수집 했으며 hello 실험의 hello hello 데이터에 따라 달라 집니다.

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
