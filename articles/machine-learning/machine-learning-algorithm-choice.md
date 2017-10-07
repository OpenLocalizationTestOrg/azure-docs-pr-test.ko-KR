---
title: "aaaHow toochoose 기계 학습 알고리즘 | Microsoft Docs"
description: "어떻게 클러스터링 감독 및 자율 학습을 위한 Azure 기계 학습 알고리즘 toochoose, 분류 또는 회귀 실험 합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a3b23d7f-f083-49c4-b6b1-3911cd69f1b4
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/25/2017
ms.author: garye
ms.openlocfilehash: 367b2278acc2435f27f9d24ead8199db58aca283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-algorithms-for-microsoft-azure-machine-learning"></a>어떻게 toochoose Microsoft Azure 기계 학습 알고리즘
hello toohello 란 질문의 대답 "어떤 기계 학습 알고리즘을 사용 해야 합니까?" 항상 "상황마다 다릅니다."입니다. Hello 크기, 품질 및 hello 데이터의 특성에 따라 다릅니다. 대상에 따라 달라 집니다 toodo hello 답으로 합니다. Hello 수학 hello 알고리즘의 사용 중인 hello 컴퓨터에 대 한 지침으로 변환 되었으면 방식에 따라 다릅니다. 시간이 얼마나 있는지에 따라 다릅니다. 알고리즘을 시도 하기 전에 최적의 성능을 발휘 합니다 가장 발생 하는 hello 데이터 과학자도 알 수 없습니다.

## <a name="hello-machine-learning-algorithm-cheat-sheet"></a>hello 컴퓨터 학습 알고리즘 치트 시트
hello **Microsoft Azure 컴퓨터 학습 알고리즘 치트 시트** hello 오른쪽 선택 기계 학습 알고리즘 hello Microsoft Azure 기계 학습 라이브러리 알고리즘에서 예측 분석 솔루션에 대 한 합니다.
이 문서는 방법을 단계별로 설명 toouse 것입니다.

> [!NOTE]
> toodownload hello 치트 시트를 서버와이 문서와 하면서 진행 너무 라인[알고리즘 치트 시트를 Microsoft Azure 기계 학습 스튜디오에 대 한 학습 컴퓨터](machine-learning-algorithm-cheat-sheet.md)합니다.
> 
> 

이 치트 시트를 염두에 대 한 매우 특정 대상을: 시작 부분 데이터 과학자와 undergraduate 수준 기계 학습 toochoose Azure 기계 학습 스튜디오에서 사용 된 알고리즘 toostart 시도 합니다. 따라서 일반화되고 지나치게 단순화되었을 수 있으나 안전한 방향으로 사용자를 안내합니다. 여기에 나와 있는 것 외에도 수많은 알고리즘이 있습니다. Azure 기계 학습에 사용할 수 있는 방법의 전체 집합이 tooencompass 증가 추가 합니다.

이러한 권장 사항은 많은 데이터 과학자 및 기계 학습 전문가로부터 수집한 피드백 및 팁입니다. 모든 항목에 동의 하지 않은 것 이지만 시도 tooharmonize 서로의 의견 대략적인 합의를 합니다. 대부분의 반대 의견이의 hello 문 "종속..."로 시작

### <a name="how-toouse-hello-cheat-sheet"></a>어떻게 toouse hello 치트 시트
로 hello 차트에 대 한 hello 경로 및 알고리즘 레이블이 읽기 "에 대 한  *&lt;경로 레이블&gt;*를 사용 하 여  *&lt;알고리즘&gt;*." 예를 들어, "*속도*의 경우 *두 개의 클래스 로지스틱 회귀*를 사용하세요."와 같습니다. 경우에 따라 두 개 이상의 분기가 적용됩니다.
완벽하게 맞는 것이 없는 경우도 있습니다. 의도 한 toobe 경험의 권장 하는, 따라서 정확한 것에 대 한 걱정 하지 마십시오.
여러 데이터 과학자와 알아보았습니다.만 있는지 hello 최상의 알고리즘은 tootry 찾을를 해당 hello 라고 모두 합니다.

다음은 예제 hello에서 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com/) 동일한 데이터와 비교 하 여 hello 결과 hello에 대 한 여러 가지 알고리즘을 실험의: [다중 클래스 분류자 비교: 문자 인식 ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

> [!TIP]
> 기계 학습 스튜디오의 hello 기능의 개요 다이어그램 참조 toodownload 및 인쇄 [Azure 기계 학습 스튜디오 기능의 개요 다이어그램](machine-learning-studio-overview-diagram.md)합니다.
> 
> 

## <a name="flavors-of-machine-learning"></a>기계 학습의 다양한 특징
### <a name="supervised"></a>감독
감독 학습 알고리즘은 예제 집합을 토대로 예측합니다. 예를 들어, 기록 주가 향후 가격에 사용한 toohazard 추측 될 수 있습니다. 학습에 사용 되는 각 예제는 hello 값으로 표시 되어-이 경우 주가 hello 합니다. 감독 학습 알고리즘은 이러한 값 레이블에서 패턴을 찾습니다. 관련 될 수 있는 모든 정보를 사용할 수 있습니다-hello 요일을 hello 주, hello 시즌, hello 회사의 재무 데이터, 업계의 hello 유형으로, 지정 학적 사건과 같은 중단의 hello 존재 여부 — 고 각 알고리즘 다양 한 유형의 패턴을 찾습니다. Hello 알고리즘 hello 가장 효율적인 패턴 수를 찾으면 사용 하 여 테스트 데이터에 대 한 패턴 toomake 예측에 레이블 없음는-내일의 가격입니다.

감독 학습은 널리 사용되고 유용한 기계 학습 유형입니다. 단, Azure 기계 학습에서 모든 hello 모듈 학습 알고리즘 감독 합니다. Azure 기계 학습 내에서는 분류, 회귀 및 이상 감지의 여러 특정 유형의 감독 학습이 표시됩니다.

* **분류**. Hello 데이터에 사용 되는 toopredict 범주 되는, 분류 지도 학습 호출 됩니다. 이 경우 hello 'cat' 또는 'dog'의 그림으로 이미지를 할당할 때 합니다. 선택 항목이 두 가지뿐인 경우 **2클래스** 또는 **이항 분류**라고 합니다. 이 문제는으로 알려져 있는 경우 더 많은 범주도 hello NCAA 년 3 월 목표 토너먼트의 hello 승자 예측 하는 경우, **다중 클래스 분류**합니다.
* **회귀** 주가와 같은 값을 예측하는 경우 감독 학습을 회귀라고 합니다.
* **이상 감지**. 경우에 따라 hello 목표는 단순히 일반적이 지 않습니다 tooidentify 데이터 요소입니다. 예를 들어 이상 금융 거래 감지에서 매우 비정상적인 신용 카드 지출 패턴이 의심 대상입니다. hello 가능한 변형을 하므로 다양 한 되며 hello 학습 예제가 거의 없으므로, 인지 가능 하지 않은 toolearn 사기성 어떤 활동이 같습니다. 이상 탐지 사용 방법은 toosimply 어떤 정상적인 작업 (기록 비 사기성 트랜잭션을 사용 하 여) 처럼 보이는 자세히 알아보고와 비슷한 되는 모든 항목을 식별 합니다.

### <a name="unsupervised"></a>자율
자율 학습에서는 데이터 요소에 연결된 레이블이 없습니다. 대신, hello 목표는 감독 되지 않은 알고리즘 몇 가지 방식으로 또는 toodescribe hello 데이터 구조를 구성 하는 알 수 있습니다. 이는 클러스터로 그룹화하거나 복잡한 데이터가 보다 단순하게 또는 조직화되어 표시되도록 데이터를 바라보는 다양한 방법을 찾는 것을 의미할 수 있습니다.

### <a name="reinforcement-learning"></a>보충 학습
보충 학습 hello 알고리즘이 가져옵니다 toochoose 작업을 응답 tooeach 데이터 요소에. hello 학습 알고리즘 짧은 시간 나중 얼마나 양호한 hello 의사 결정을 나타내는 보상 신호를 받습니다.
이에 따라 hello 알고리즘 순서 tooachieve hello에 대 한 가장 높은 보상에서 해당 전략을 수정 합니다. 현재 Azure 기계 학습에는 보충 학습 알고리즘 모듈이 없습니다. 보충 학습 로봇, 여기서 hello 시간에 한 지점 센서 판독값의 집합은 데이터 요소 고 hello 알고리즘 hello 로봇 다음 작업을 선택 해야에서 일반적입니다. 사물 인터넷의 응용 프로그램에 적합한 학습이기도 합니다.

## <a name="considerations-when-choosing-an-algorithm"></a>알고리즘 선택 시 고려 사항
### <a name="accuracy"></a>정확도
항상 가능한 hello 가장 정확 하 게 응답을 가져오는 필요가 없습니다.
용도에 따라 근사치가 적절한 경우도 있습니다. 않은 hello 경우 수 toocut 것일 수 있습니다 더 많은 대략적인 방법으로 생각해 여 크게 처리 시간입니다. 보다 근접한 방법의 다른 이점은 기본적으로 [과잉 맞춤](https://youtu.be/DQWI1kvmwRg)경향을 피할 수 있다는 것입니다.

### <a name="training-time"></a>학습 시간
안녕 수가 분 단위 또는 시간 필요한 tootrain 모델 알고리즘 간에 크게 다릅니다. 학습 시간이 종종 밀접 한 관련이 정확도-다른 hello 하나 일반적으로 포함 합니다. 또한 일부 알고리즘은 데이터 요소 다른 항목 보다 더 중요 한 toohello 수입니다.
시간이 제한 되는 경우에 특히 hello 데이터 집합이 큰 경우 hello 선택한 알고리즘 운영할 수 있습니다.

### <a name="linearity"></a>선형성
많은 기계 학습 알고리즘에서 선형성을 활용합니다. 선형 분류 알고리즘은 클래스를 직선(또는 고차원의 아날로그)으로 구분할 수 있다고 가정합니다. 여기에는 로지스틱 회귀 및 지원 벡터 컴퓨터가 포함됩니다(Azure 기계 학습에 구현됨).
선형 회귀 알고리즘은 데이터가 직선을 따르는 경향이 있다고 가정합니다. 이러한 가정은 일부 문제에 대해서는 그다지 나쁘지 않지만 어떤 면에서는 정확도가 떨어질 수 있습니다.

![비선형 클래스 경계][1]

***비선형 클래스 경계*** *- 선형 분류 알고리즘에 의존하며 결과의 정확도가 떨어짐*

![비선형 추세 반영 데이터][2]

***비선형 추세 반영 데이터*** *- 선형 회귀 방법을 사용하면 필요한 것보다 훨씬 많은 오류가 생성됨*

위험성에도 불구하고, 선형 알고리즘은 공격에 대한 최전선으로 매우 널리 사용됩니다. 이들은 toobe 알고리즘 방식으로 간단 하 고 학습에 빠르게는 경향이 있습니다.

### <a name="number-of-parameters"></a>매개 변수 수
매개 변수는 hello 손잡이가 하는 데이터 과학자는 알고리즘을 설정할 때 tooturn를 가져옵니다. 숫자 허용 오차 또는, 반복 또는 hello 알고리즘의 동작 방식을 변형의 여러 옵션의 수와 같은 hello 알고리즘의 동작에 영향을 주는 합니다. hello 학습 시간 및 hello 알고리즘의 정확도 매우 중요 한 toogetting 정당한 hello 올바른 설정을 경우가 있습니다. 일반적으로 많은 수의 매개 변수를 사용 하는 알고리즘 가장 평가판 hello 및 오류 toofind 좋은 조합이 필요합니다.

또는 Azure 기계 학습에는 [매개 변수 스위핑](machine-learning-algorithm-parameters-optimize.md) 모듈 블록이 있어 선택한 세분성에서 모든 매개 변수 조합을 자동으로 시도합니다. 이 좋은 방법 toomake 있는지 hello 매개 변수 공간의 스팬 했습니다, 그리고 hello 필요한 시간 tootrain 모델 급격 하 게 증가 hello 수의 매개 변수를 사용 합니다.

hello 거꾸로는 일반적으로 많은 매개 변수가 있는 의미는 알고리즘에는 유연 하 게 합니다. 또한 정확도도 매우 뛰어날 수 있습니다. 제공 hello 잘 조합 매개 변수 설정 찾을 수 있습니다.

### <a name="number-of-features"></a>기능 수
특정 유형의 데이터에 대 한 hello 다양 한 기능에는 데이터 요소의 매우 큰 비교 toohello 숫자일 수 있습니다. 이 경우 종종 hello와 genetics 또는 텍스트 데이터입니다. hello 많은 수의 기능 일부 학습 알고리즘을 학습 unfeasibly 긴 시간을 만드는 성능이 저하 수 있습니다. 지원 벡터 컴퓨터는 특히 적합된 toothis 대/소문자 (아래 참조).

### <a name="special-cases"></a>특수 사례
일부 학습 알고리즘 hello 데이터 또는 원하는 hello 결과의 hello 구조에 대 한 특정 가정을 확인합니다. 사용자 요구에 적합한 것을 찾을 수 있는 경우 보다 유용한 결과, 보다 정확한 예측 또는 단축된 교육 시간을 제공할 수 있습니다.

| **알고리즘** | **정확도** | **학습 시간** | **선형성** | **매개 변수** | **참고 사항** |
| --- |:---:|:---:|:---:|:---:| --- |
| **2클래스 분류** | | | | | |
| [로지스틱 회귀](https://msdn.microsoft.com/library/azure/dn905994.aspx) | |● |● |5 | |
| [의사 결정 포리스트](https://msdn.microsoft.com/library/azure/dn906008.aspx) |● |○ | |6 | |
| [의사 결정 정글](https://msdn.microsoft.com/library/azure/dn905976.aspx) |● |○ | |6 |적은 메모리 공간 |
| [향상된 의사 결정 트리](https://msdn.microsoft.com/library/azure/dn906025.aspx) |● |○ | |6 |큰 메모리 공간 |
| [신경망](https://msdn.microsoft.com/library/azure/dn905947.aspx) |● | | |9 |[추가 사용자 지정 가능](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [평균 퍼셉트론](https://msdn.microsoft.com/library/azure/dn906036.aspx) |○ |○ |● |4 | |
| [지원 벡터 컴퓨터](https://msdn.microsoft.com/library/azure/dn905835.aspx) | |○ |● |5 |큰 기능 집합의 적합 |
| [로컬 심층 지원 벡터 컴퓨터](https://msdn.microsoft.com/library/azure/dn913070.aspx) |○ | | |8 |큰 기능 집합의 적합 |
| [Bayes 지점 컴퓨터](https://msdn.microsoft.com/library/azure/dn905930.aspx) | |○ |● |3 | |
| **다중 클래스 분류** | | | | | |
| [로지스틱 회귀](https://msdn.microsoft.com/library/azure/dn905853.aspx) | |● |● |5 | |
| [의사 결정 포리스트](https://msdn.microsoft.com/library/azure/dn906015.aspx) |● |○ | |6 | |
| [의사 결정 정글 ](https://msdn.microsoft.com/library/azure/dn905963.aspx) |● |○ | |6 |적은 메모리 공간 |
| [신경망](https://msdn.microsoft.com/library/azure/dn906030.aspx) |● | | |9 |[추가 사용자 지정 가능](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [one-v-all](https://msdn.microsoft.com/library/azure/dn905887.aspx) |- |- |- |- |속성을 선택 하는 hello 2 클래스 메서드를 참조 하십시오. |
| **회귀** | | | | | |
| [선형](https://msdn.microsoft.com/library/azure/dn905978.aspx) | |● |● |4 | |
| [베이지언 선형](https://msdn.microsoft.com/library/azure/dn906022.aspx) | |○ |● |2 | |
| [의사 결정 포리스트](https://msdn.microsoft.com/library/azure/dn905862.aspx) |● |○ | |6 | |
| [향상된 의사 결정 트리](https://msdn.microsoft.com/library/azure/dn905801.aspx) |● |○ | |5 |큰 메모리 공간 |
| [빠른 포리스트 분위수](https://msdn.microsoft.com/library/azure/dn913093.aspx) |● |○ | |9 |지점 예측이 아닌 배포 |
| [신경망](https://msdn.microsoft.com/library/azure/dn905924.aspx) |● | | |9 |[추가 사용자 지정 가능](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [포아송 ](https://msdn.microsoft.com/library/azure/dn905988.aspx) | | |● |5 |기술적으로 로그 선형입니다. 개수를 예측하는 경우 |
| [서수](https://msdn.microsoft.com/library/azure/dn906029.aspx) | | | |0 |순위 순서를 예측하는 경우 |
| **이상 감지** | | | | | |
| [지원 벡터 컴퓨터](https://msdn.microsoft.com/library/azure/dn913103.aspx) |○ |○ | |2 |특히 큰 기능 집합의 적합 |
| [PCA 기반 이상 감지](https://msdn.microsoft.com/library/azure/dn913102.aspx) | |○ |● |3 | |
| [K-means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/) | |○ |● |4 |클러스터링 알고리즘 |

**알고리즘 속성:**

**●** -정확성, 빠른 학습 시간 및 선형성 hello 사용을 보여 줍니다.

**○** - 양호한 정확도 및 보통의 교육 시간 나타냄

## <a name="algorithm-notes"></a>알고리즘 참고 사항
### <a name="linear-regression"></a>선형 회귀
앞에서 설명한 대로 [선형 회귀](https://msdn.microsoft.com/library/azure/dn905978.aspx) 선 (또는 평면 또는 평면이) toohello 데이터 집합에 적합 합니다. 자주 사용되고 간단하며 빠르지만 일부 문제에 대해서는 지나치게 단순화될 수 있습니다.
[선형 회귀 자습서](machine-learning-linear-regression-in-azure.md)는 여기를 확인하세요.

![선형 추세 반영 데이터][3]

***선형 추세 반영 데이터***

### <a name="logistic-regression"></a>로지스틱 회귀
로지스틱 회귀는 위한 강력한 도구로 실제로 사용 '회귀' hello 이름에 포함 되어, 있지만 [2 클래스](https://msdn.microsoft.com/library/azure/dn905994.aspx) 및 [다중 클래스](https://msdn.microsoft.com/library/azure/dn905853.aspx) 분류 합니다. 빠르고 단순합니다. 사용 하 여 팩트 hello는 '-직선 대신 모양의 곡선 하면 적합 한 데이터를 그룹으로 분할 합니다. 로지스틱 회귀는 선형 클래스 경계를 제공하므로 이를 사용할 때는 선형 근사값이 수락할 수 있는 것인지 확인해야 합니다.

![한 기능을 사용 하 여 로지스틱 회귀 tootwo 클래스 데이터][4]

***한 기능을 사용 하 여 로지스틱 회귀 tootwo 클래스 데이터*** *-클래스 경계는 hello 항목이 요소를 어떤 hello 로지스틱 곡선 방금 가까운 tooboth 클래스*

### <a name="trees-forests-and-jungles"></a>트리, 포리스트 및 정글
의사 결정 포리스트([회귀](https://msdn.microsoft.com/library/azure/dn905862.aspx), [2클래스](https://msdn.microsoft.com/library/azure/dn906008.aspx) 및 [다중 클래스](https://msdn.microsoft.com/library/azure/dn906015.aspx)), 의사 결정 정글([2클래스](https://msdn.microsoft.com/library/azure/dn905976.aspx) 및 [다중 클래스](https://msdn.microsoft.com/library/azure/dn905963.aspx)) 및 향상된 의사 결정 트리([회귀](https://msdn.microsoft.com/library/azure/dn905801.aspx) 및 [2클래스](https://msdn.microsoft.com/library/azure/dn906025.aspx))는 모두 의사 결정 트리, 기본적인 Machine Learning 개념을 기반으로 합니다. 에 의사 결정 트리의 여러 변형이 모두 동일한 작업을 수행 하지만-hello 기능 공간 대부분 hello 있는 영역으로 세분화 동일한 레이블. 분류 또는 회귀를 수행 중인지 여부에 따라 일관된 범주 또는 상수 값의 하위 지역일 수 있습니다.

![의사 결정 트리가 기능 공간 세분화][5]

***의사 결정 트리는 기능 공간을 대략적으로 균일한 값의 하위 지역으로 세분화함***

기능 공간을 임의로 작은 영역으로 분할할 수 있습니다, 되므로 쉽게 tooimagine 정밀 하 게 충분 한 toohave 단일 데이터 요소 / 지역당 분할 합니다. 이는 극단적인 과잉 맞춤의 예입니다. 순서 tooavoid에이 다양 한 트리 생성 됩니다 수행 하는 특별 한 수학 주의 하 여 hello 트리는 상호 관련 되지 않습니다. 이 "의사 결정 포리스트"의 평균을 hello는 과잉 맞춤을 방지 하는 트리입니다. 의사 결정 포리스트는 많은 양의 메모리를 사용할 수 있습니다. 의사 결정 정글은 학습 시간이 약간 초과의 hello 부담 적은 메모리를 사용 하는 variant입니다.

향상된 의사 결정 트리는 세분화할 수 있는 횟수 및 각 하위 지역에 허용되는 데이터 요소 수를 제한하여 과잉 맞춤을 피합니다. 알고리즘 하기 전에 hello 트리 남긴 hello 오류에 대 한 보정을 위해 학습 있으며 각 트리의 시퀀스를 생성 합니다. hello 결과 toouse 메모리가 매우 많이 느껴질 수 있는 매우 정확 하 게 학습자입니다. Hello 전체 기술 설명에 대 한 체크 아웃 [Friedman의 원래 자료](http://www-stat.stanford.edu/~jhf/ftp/trebst.pdf)합니다.

[빠른 포리스트 변 위치 회귀](https://msdn.microsoft.com/library/azure/dn913093.aspx) 은 뿐만 아니라 hello 일반적인 ()의 중앙값 hello 데이터 영역, 뿐만 아니라 hello 형태의 변 위치에서 해당 배포 내에서 알아야 하는 hello 특별 한 경우에 대 한 의사 결정 트리의 변형입니다.

### <a name="neural-networks-and-perceptrons"></a>신경망 및 퍼셉트론
신경망은 [다중 클래스](https://msdn.microsoft.com/library/azure/dn906030.aspx), [2클래스](https://msdn.microsoft.com/library/azure/dn905947.aspx) 및 [회귀](https://msdn.microsoft.com/library/azure/dn905924.aspx)를 반영한 두뇌 영감 학습 알고리즘입니다. 무한 한에서 나올 있지만 hello 신경망 내 Azure 기계 학습에서 사용 약관은 모두 hello 형태의 방향이 있는 비순환 그래프. 따라서 입력 기능은 출력으로 전환되기 전에 계층 시퀀스를 통해 앞으로(뒤로는 불가능) 전달됩니다. 각 계층의 입력에 가중치를 적용을 다양 한 조합 한 hello 다음 계층에 전달 합니다. 기능 toolearn에서 간단한 계산 결과 이러한 조합은 클래스 경계 및 데이터 추세 매직 여 겉보기 정교한 있습니다. 이러한 종류의 네트워크 다 계층화 된 많은 양의 기술 보고 뒷받침하는 "심층 학습" hello 및 과학 소설 수행 합니다.

하지만 이러한 높은 성능을 위해서는 대가가 따릅니다. 신경망은 기능이 많이 포함 된 큰 데이터 집합에 대 한 특히는 오랜 시간이 tootrain을 걸릴 수 있습니다. 즉, 매개 변수 비우기를 수행 hello 학습 시간이 크게 확장 대부분 알고리즘 보다 더 많은 매개 변수 갖습니다.
및 너무 누구나 해당 overachievers[자신의 네트워크 구조를 지정](http://go.microsoft.com/fwlink/?LinkId=402867),이 속성은 exhaustible 되지 않습니다.

![신경망을 통해 경계가 학습][6]
***복잡 하 고 불규칙 한 신경망을 통해 학습 하는 hello 경계 수***

hello [2 클래스 평균 퍼셉트론](https://msdn.microsoft.com/library/azure/dn906036.aspx) 신경망의 응답 tooskyrocketing 학습 시간이 됩니다. 2클래스 평균 퍼셉트론은 선형 클래스 경계를 제공하는 네트워크 구조를 사용합니다. 오늘날의 기준으로 기본 거의 있지만 강력 하 게 작업은 오랜 전통을 개이고 만큼 작지 않아서 toolearn를 신속 하 게 됩니다.

### <a name="svms"></a>SVM
지원 벡터 컴퓨터 Svm ()는 최대한 광범위 한 여백으로 여 클래스를 구분 하는 hello 경계를 찾습니다. Hello 두 개의 클래스를 명확 하 게 분리 될 수 없으며 hello 알고리즘 hello 최상의 경계를 수 있습니다. Azure 기계 학습에서 작성 된 대로 hello [2 클래스 SVM](https://msdn.microsoft.com/library/azure/dn905835.aspx) 직선만으로이 작업을 수행 합니다. (SVM-speak에서 선형 커널을 사용합니다.) 이 선형 근사값을 사용 하면 되므로 수 toorun 매우 신속 하 게 합니다. 텍스트 또는 유전자처럼 기능 중심의 데이터에서 특히 유용합니다. 이러한 경우 Svm는 덜 과잉 맞춤이 대부분의 다른 알고리즘 보다 또한 toorequiring 많지 메모리으로 보다 신속 하 게 수 tooseparate 클래스입니다.

![지원 벡터 컴퓨터 클래스 경계][7]

***일반적인 지원 벡터 컴퓨터 클래스 경계는 두 개의 클래스를 구분 하는 hello 여백 최대화***

다른 제품 Microsoft Research의 hello [2 클래스 로컬 심층 SVM](https://msdn.microsoft.com/library/azure/dn913070.aspx) 비선형 SVM 대부분의 hello 선형 버전의 hello 속도 메모리 효율성을 유지 하면서의 변형입니다. Hello 선형 접근 방식을 충분히 정확한 답을 제공 하지 않습니다 사례에 대 한 이상적입니다. hello 개발자 하 게 hello 문제 많은 작은 선형 SVM 문제를 구분 하 여 빠른 유지 합니다. 읽기 hello [설명 전체](http://research.microsoft.com/um/people/manik/pubs/Jose13.pdf) hello에 대 한 내용은이 트릭 어떻게 삽입 있습니다.

Hello 비선형 Svm의 효과적인 확장을 사용 하 여, [1 클래스 SVM](https://msdn.microsoft.com/library/azure/dn913103.aspx) 밀접 하 게 hello 전체 데이터 집합에 간략하게 설명 하는 경계를 그립니다. 이것은 이상 감지에 유용합니다. 모든 새 데이터까지 해당 경계에 해당 하지 않는 요소가 주목할 만한 충분 한 비정상적인 toobe 합니다.

### <a name="bayesian-methods"></a>Bayesian 메서드
Bayesian 메서드는 과잉 맞춤을 방지하는 매우 뛰어난 품질을 자랑합니다. Hello 대답의 hello 가능성이 분포에 대 한 미리 몇 가지 사항을 가정 하 여이 수행 합니다. 이 방법에 대한 다른 부산물은 매우 적은 매개 변수입니다. Azure Machine Learning은 분류([2클래스 Bayes 지점 컴퓨터](https://msdn.microsoft.com/library/azure/dn905930.aspx)) 및 회귀([베이지언 선형 회귀](https://msdn.microsoft.com/library/azure/dn906022.aspx)) 모두에 대해 두 베이지언 알고리즘을 포함합니다.
Hello 데이터를 분할 하거나 직선에 맞게 수는 이러한 가정 하는 참고 합니다.

역사를 거슬러 보면, Bayes 지점 컴퓨터는 Microsoft Research에서 개발되었습니다. 그 이면에는 매우 뛰어난 이론적인 작업을 포함하고 있습니다. hello 관심된 학생은 방향이 지정 된 toohello [JMLR의 문서를 원래](http://jmlr.org/papers/volume1/herbrich01a/herbrich01a.pdf) 및 [Chris bishop이 작성 하 여 통찰력 블로그](http://blogs.technet.com/b/machinelearning/archive/2014/10/30/embracing-uncertainty-probabilistic-inference.aspx)합니다.

### <a name="specialized-algorithms"></a>특수화된 알고리즘
매우 구체적인 목표가 있다면 운이 좋을 수 있습니다. Hello Azure 기계 학습 컬렉션 내에서 특수화 하는 알고리즘 있습니다.

- 순위 예측([서수 회귀](https://msdn.microsoft.com/library/azure/dn906029.aspx)),
- 수 예측([포아송 회귀](https://msdn.microsoft.com/library/azure/dn905988.aspx)),
- 변칙 검색([주요 구성 요소 분석](https://msdn.microsoft.com/library/azure/dn913102.aspx) 기준 및 [지원 벡터 컴퓨터](https://msdn.microsoft.com/library/azure/dn913103.aspx) 기준)
- 클러스터링([K-means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/))

![PCA 기반 이상 감지][8]

***PCA 기반 비정상 검색*** *-hello 포함 된 대부분의 hello 데이터 stereotypical 배포에 해당 되며 다음 해당 배포에서 크게 벗어난 포인트 주의 대상*

![K-means를 사용하여 그룹화된 데이터 집합][9]

***K-means를 사용하여 데이터 집합을 5개 클러스터로 그룹화합니다.***

앙상블 이기도 [중 하나-v-모든 다중 클래스 분류자](https://msdn.microsoft.com/library/azure/dn905887.aspx), 나누기 hello N 클래스 분류 문제가 N-1 2 클래스 분류 문제가 발생 합니다. hello 정확도, 교육 시간 및 선형성 속성 hello 2 클래스 분류자를 사용 하 여 결정 됩니다.

![2 클래스 분류자 tooform 세 클래스 분류자 결합][10]

***2 클래스 분류자의 쌍 tooform 세 클래스 분류자 결합***

액세스 tooa 강력한 기계 학습 프레임 워크의 hello 제목 아래에 포함 되어 azure 기계 학습 [Vowpal Wabbit](https://msdn.microsoft.com/library/azure/8383eb49-c0a3-45db-95c8-eb56a1fef5bf)합니다.
VW는 분류 및 회귀를 모두 학습할 수 있으며 부분적으로 레이블이 지정되지 않은 데이터에서도 학습이 가능하므로 여기에서 분류를 거부합니다. 다양 한 알고리즘, 손실 함수 및 최적화 알고리즘을 학습 중 하나는 toouse를 구성할 수 있습니다. 효율적이 고, 매우 빠른 toobe를 접지 hello에서 설계 되었습니다. 적은 작업으로 엄청나게 큰 기능 집합을 처리합니다.
Microsoft Research의 John Langford가 시작하여 진행한 VW는 스톡 카 알고리즘 분야에서 포뮬러 원(Formula One) 엔트리입니다. 모든 문제 VW, 맞지만 던 수도 없습니다 tooclimb 인터페이스에 대해 학습 합니다. 또한 여러 언어로 된 [독립 실행형 오픈 소스 코드](https://github.com/JohnLangford/vowpal_wabbit) 도 제공됩니다.

## <a name="more-help-with-algorithms"></a>알고리즘에 대한 자세한 도움말
* 알고리즘을 설명하고 예제를 제공하는 다운로드 가능한 인포그래픽은 [다운로드 가능한 인포그래픽: 알고리즘 예제를 포함한 Machine Learning 기본 사항](machine-learning-basics-infographic-with-algorithm-examples.md)을 참조하세요.
* Azure 기계 학습 스튜디오에서 사용할 수 있는 모든 hello 기계 학습 알고리즘의 범주별 목록을 보려면 참조 [모델 초기화] [ initialize-model] hello Studio 기계 학습 알고리즘 및 모듈 도움말입니다.
* Azure Machine Learning Studio의 전체 알고리즘 및 모듈에 대한 알파벳 순서 목록은 Machine Learning Studio 알고리즘 및 모듈 도움말에서 [Machine Learning Studio 모듈의 A-Z 목록][a-z-list]을 참조하세요.
* Azure 기계 학습 스튜디오의 hello 기능의 개요 다이어그램 참조 toodownload 및 인쇄 [Azure 기계 학습 스튜디오 기능의 개요 다이어그램](machine-learning-studio-overview-diagram.md)합니다.


<!-- Reference links -->
[initialize-model]: https://msdn.microsoft.com/library/azure/dn905812.aspx
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx

<!-- Media -->

[1]: ./media/machine-learning-algorithm-choice/image1.png
[2]: ./media/machine-learning-algorithm-choice/image2.png
[3]: ./media/machine-learning-algorithm-choice/image3.png
[4]: ./media/machine-learning-algorithm-choice/image4.png
[5]: ./media/machine-learning-algorithm-choice/image5.png
[6]: ./media/machine-learning-algorithm-choice/image6.png
[7]: ./media/machine-learning-algorithm-choice/image7.png
[8]: ./media/machine-learning-algorithm-choice/image8.png
[9]: ./media/machine-learning-algorithm-choice/image9.png
[10]: ./media/machine-learning-algorithm-choice/image10.png
