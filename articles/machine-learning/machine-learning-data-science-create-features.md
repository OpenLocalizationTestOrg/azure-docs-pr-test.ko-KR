---
title: "데이터 과학에서 엔지니어링 팀에 aaaFeature | Microsoft Docs"
description: "기능 엔지니어링의 hello 목적을 설명 하 고 기계 학습의 hello 데이터 향상 프로세스에서 해당 역할의 예제를 제공 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3fde69e8-5e7b-49ad-b3fb-ab8ef6503a4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: af40ea9cc9395bc87fe695eeaef26aa71e0ec9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-in-data-science"></a>데이터 과학의 기능 엔지니어링
이 항목 기능 엔지니어링의 hello 목적을 설명 하 고 기계 학습의 hello 데이터 향상 프로세스에서 해당 역할의 예제를 제공 합니다. hello 예제 tooillustrate Azure 기계 학습 스튜디오에서 가져온 것이 프로세스를 사용 합니다. 

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

이 **메뉴** tootopics toocreate 다양 한 환경에서 데이터에 대 한 기능 하는 방법을 설명 하는 링크입니다. 이 작업은 hello 단계 [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)합니다.

엔지니어링 시도 tooincrease hello 예측 력이 hello 설정 프로세스를 용이 하 게 하는 데 도움이 되는 원시 데이터에서 기능을 만들어 학습 알고리즘의 기능입니다. 기능 선택은 TDSP hello에 설명 된 hello의 한 부분 및 엔지니어링 hello [hello 팀 데이터 과학 프로세스 수명 주기는 무엇입니까?](data-science-process-overview.md) 기능 엔지니어링 및 선택 hello의 일부는 **기능 개발** hello TDSP의 단계입니다. 

* **엔지니어링 기능**:이 프로세스에서는 hello hello 데이터의 기존 원시 기능에서 toocreate 추가 관련 기능 및 tooincrease hello hello 학습 알고리즘의 예측 력이 합니다.
* **기능 선택**:이 프로세스 hello 학습 문제의 시도 tooreduce hello 차원에서 원래 데이터 기능의 hello 키 하위 집합을 선택 합니다.

일반적으로 **엔지니어링 기능** 적용 된 첫 번째 toogenerate 추가 기능을 고 hello **기능 선택** 단계는 수행된 된 tooeliminate 관련이 없는, 중복 또는 밀접 기능입니다.

기계 학습에서 사용 되는 hello 학습 데이터 수집 된 hello 원시 데이터에서 기능 추출 종종 향상 시킬 수 있습니다. 필기 문자의 tooclassify hello 이미지 약간 hello 원시 비트 배포 데이터에서 생성 하는 밀도 맵 만드는 방법은 학습의 hello 컨텍스트에서 엔지니어링 기능의 예입니다. 이 맵은 hello 문자의 hello 가장자리를 단순히 직접 사용 하 여 hello 원시 배포 보다 더 효율적으로 찾을 수 있습니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="creating-features-from-your-data---feature-engineering"></a>데이터에서 기능 만들기 - 기능 엔지니어링
hello 학습 데이터 행렬 (레코드 또는 행에 저장 된 관측 치를) 예제는 구성 하며 각각의 기능 (변수 또는 열에 저장 된 필드) 집합으로 이루어져 있습니다. hello hello 실험적 디자인에 지정 된 기능은 hello 데이터의 예상된 toocharacterize hello 패턴입니다. 선택한 기능 사용 되는 집합 tootrain 모델을 hello 다양 한 hello 원시 데이터 필드에 직접 포함 될 수 있지만 종종 hello (공학적된) 추가 기능 향상된 된 hello 원시 데이터 toogenerate의 hello 기능에서 생성 된 toobe 필요 학습 데이터 집합입니다.

모델을 학습 하는 경우 어떤 유형의 기능 tooenhance hello 데이터 집합을 생성 해야? Hello 교육을 향상 시키는 엔지니어링된 기능 hello 데이터의 hello 패턴을 더 잘 구분할 수 있는 정보를 제공 합니다. Hello 새 기능 tooprovide 추가 정보를 명확 하 게 캡처된 또는에서 명백 hello 원본 또는 기존 기능 집합 라고 생각 됩니다. 그러나 이 프로세스는 정교한 작업입니다. 안정되고 생산성이 있는 결정을 내리려면 도메인에 대한 전문 지식이 필요한 경우가 많습니다.

Azure 기계 학습을 시작할 때 hello Studio에에서 제공 된 샘플을 사용 하 여 구체적으로이 프로세스는 가장 쉬운 toograsp 됩니다. 다음은 제공되는 두 가지 예입니다.

* 회귀 예제 [자전거 여 hello 수의 예측](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4) hello 대상 값은 알려진 하는 감독 된 실험에서
* [기능 해싱](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)

## <a name="example-1-adding-temporal-features-for-regression-model"></a>예 1: 회귀 모델을 위해 시간 기능 추가
사용 hello 실험 "수요 예측 자전거의" Azure 기계 학습 스튜디오 toodemonstrate tooengineer 기능이 하는 방법에 회귀 작업에 대 한 합니다. hello이이 실험은 hello 자전거, 자전거 여는 특정 월/일/시간 내에서 hello 수,에 대 한 toopredict hello 요구 합니다. 데이터 집합을 hello "자전거 임대 UCI 데이터 집합" hello 원시 입력 데이터로 사용 됩니다. 이 데이터 집합은 hello hello 미국에에서 워싱턴 DC에서 자전거 임대 네트워크를 유지 하는 대문자 자전거 공유 회사에서에서 실제 데이터를 기반으로 합니다. hello dataset hello 년 2011 및 2012 년에에서 하루 중 특정 시간 내에서 자전거 여 hello 수를 나타내며 17379 행과 17 열을 포함 합니다. 날씨 조건 (온도/습도/풍속) 및 hello 날짜 (휴일/요일) hello 종류 hello 원시 기능 집합에 포함 되어 있습니다. hello 필드 toopredict "cnt", 특정 시간 내에서 hello 자전거 대 여를 나타내는 하며 범위는 1 too977에서 범위는 수입니다.

Hello를 사용 하 여 4 개의 회귀 모델을 생성 하는 hello 학습 데이터의 효과적인 기능 생성의 hello 목표와 동일한 알고리즘 하지만 네 개의 서로 다른 학습 데이터 집합입니다. 4 hello 데이터 집합을 나타내는 원시 입력된 데이터를 동일한 hello 되지만 기능의 증가 함에 설정은 합니다. 이러한 기능은 다음 네 가지 범주로 그룹화됩니다.

1. A = 날씨 + 휴일 + 평일 + hello 예측 된 날에 대 한 주말 기능
2. B = 12 시간 동안 이전 각 hello 임대 된 자전거 수
3. C = 된 임대 각 hello hello에 12 일 이전 동일 자전거 수 시간
4. D = 된 임대 각 hello hello에 12 일로, 이전 동일 자전거 수 시간 및 hello 같은 날

기능 집합 A hello 원래 원시 데이터에 이미 존재 하는 것 외에도 hello 다른 세 가지 기능을 만듭니다 hello 기능 엔지니어링 프로세스. 기능 B 캡처 hello 자전거에 대 한 최근 요청을 설정합니다. 기능 C 캡처 자전거에 대 한 hello 요구 한 특정 시간에 설정합니다. 특정 시간 및 특정 요일 hello 자전거에 대 한 캡처 수요가 D를 설정 하는 기능. hello 4 개의 학습 데이터 집합 각 기능 집합 A "," A + B "," A + B + C "및" A + B + C + D, 각각 포함 합니다.

Hello Azure 기계 학습 실험에서에서 hello 미리 처리 된 입력된 데이터 집합에서 4 개의 분기를 통해 이러한 4 개의 학습 데이터 집합을 구성 합니다. 이러한 분기 중 각각 포함 된 hello 왼쪽 대부분 분기를 제외 하 고는 [R 스크립트 실행](https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/) (기능 B, C 및 D 설정) 하는 파생된 기능 집합이 각각 구성 되 고 추가 된 toohello 가져온 데이터 집합 있는 모듈입니다. hello 다음 그림 hello 두 번째 왼쪽된 분기 toocreate 기능 집합 B hello R 스크립트를 사용 하는 방법을 보여 줍니다.

![기능 만들기](./media/machine-learning-data-science-create-features/addFeature-Rscripts.png)

다음 표에 hello에 hello 비교 hello 4 개의 모델의 hello 성능 결과 요약 되어 있습니다. 최상의 결과 얻으려면 hello A + B + C 기능으로 표시 됩니다. 추가 기능 집합 hello 학습 데이터에 포함 되 면 오류 속도 감소 hello 유의 합니다. 이 가정 hello 기능 집합 B, C 제공 hello 회귀 작업에 대 한 추가 관련 정보를 확인 합니다. 하지만 D hello 기능을 추가 하지 않는 것 tooprovide hello 오류율 추가 감소 합니다.

![결과 비교](./media/machine-learning-data-science-create-features/result1.png)

## <a name="example2"></a> 예 2: 텍스트 마이닝에 기능 만들기
기능 엔지니어링 마이닝, 문서 분류 및 감성 분석 등 작업 관련된 tootext에서 광범위 하 게 적용 됩니다. 예를 들어 여러 범주로 tooclassify 문서 원하는 때 일반적인 가정은 hello 단어/구를 하나의 문서 범주에 포함 된 않는다는 다른 문서 범주에 가능성이 더 낮아집니다 toooccur입니다. 다른 단어 hello 단어/구를 분포의 hello 주파수는 수 toocharacterize 다른 문서 범주입니다. 텍스트 마이닝 응용 프로그램에서 개별 텍스트 콘텐츠 정보가 hello 입력 데이터로 일반적으로 사용 되므로 hello 엔지니어링 프로세스 기능은 필요한 toocreate hello 기능 단어/구 주파수를 포함 합니다.

tooachieve이 작업을 호출 하는 기술을 **기능 해시** 가 적용 된 tooefficiently 인덱스에 임의의 텍스트 형식 기능을 설정 합니다. 대신 각 텍스트 기능 (단어/구) tooa 특정 인덱스, 해시 함수 toohello 기능을 적용 하 고 해당 해시 값으로 인덱스를 직접 사용 하 여이 메서드 함수를 연결 합니다.

Azure 기계 학습에는 이러한 단어/문구 기능을 편리하게 생성하는 [기능 해싱](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) 모듈이 있습니다. 다음 그림에서는 이 모듈을 사용하는 예를 보여줍니다. 두 개의 열을 포함 하는 hello 입력된 데이터 집합: 1 too5에서 범위의 책 등급 hello 및 실제 검토 콘텐츠 hello 합니다. 이 hello 목표 [기능 해시](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) 모듈의 해당 단어 hello hello 발생 빈도 표시 하는 새로운 기능의 bunch tooretrieve / phrase(s) hello 특정 책 검토 내에서. toouse이이 모듈에서는 toocomplete hello 단계를 수행 해야 합니다.

* 먼저 hello 입력된 텍스트를 포함 하는 hello 열 선택 (이 예에서 "Col2").
* 둘째, 즉, 2 "해시 비트 크기" too8 hello 설정 ^8 = 256 기능 생성 됩니다. hello 단어/단계 모든 hello 텍스트에 해시 된 too256 인덱스 됩니다. hello 매개 변수 "해시 비트 크기" 1 too31에서 범위. 단어 hello / phrase(s) 가능성이 더 낮아집니다 toobe toobe 더 큰 숫자를 설정 하는 경우 동일 인덱스 hello로 해시 됩니다.
* 셋째, hello 매개 변수 "N 그램" too2를 설정 합니다. 이 hello 입력된 텍스트에서 그램이 (모든 단일 단어에 대 한 기능) 유 니 그램과 바이 (인접 한 단어의 모든 쌍에 대 한 기능)의 발생 빈도를 hello를 가져옵니다. hello 매개 변수 "N 그램" 범위는 hello toobe 순차적 단어의 최대 수를 나타내는 0 too10에서 기능에 포함 합니다.  

!["기능 해싱"모듈](./media/machine-learning-data-science-create-features/feature-Hashing1.png)

hello 다음 그림은 어떤 hello 이러한 새 기능은 표시 합니다.

!["기능 해싱" 예](./media/machine-learning-data-science-create-features/feature-Hashing2.png)

## <a name="conclusion"></a>결론
엔지니어링 및 선택한 기능 hello 데이터에 포함 된 tooextract hello 키 정보를 시도 하는 hello 학습 프로세스의 hello 효율성을 향상 합니다. 이러한 모델 tooclassify hello 입력된 데이터의 hello 거듭제곱을 정확 하 게 향상 시킬 및 toopredict 결과 관심 더 강력 하 게 합니다. 기능 엔지니어링 및 선택 toomake hello 학습 더 계산 tractable 결합할 수도 있습니다. 이 작업을 수행 하 여 향상 하 고 toocalibrate 또는 모델을 학습 필요 hello 기능 수를 줄이면 합니다. Hello 기능 선택한 tootrain hello 모델에 최소한의 hello 데이터의 hello 패턴을 설명 하 고 다음 결과 성공적으로 예측 하는 독립 변수 집합은 수학적으로 말하자면, 있습니다.

Note 아닌지 항상 반드시 tooperform 기능 엔지니어링 이나 기능 선택 합니다. 또는 필요한 지 여부 또는 수집 hello 알고리즘을 선택 했으며 hello 실험의 hello hello 데이터에 따라 달라 집니다.

