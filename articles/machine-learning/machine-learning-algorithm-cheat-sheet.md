---
title: "학습 알고리즘 치트 시트 aaaMachine | Microsoft Docs"
description: "인쇄 가능한 기계 학습 알고리즘 치트 시트를 사용 하면 Azure 기계 학습 스튜디오에서 예측 모델에 hello 적합 한 알고리즘을 선택 합니다."
keywords: "알고리즘 치트 시트, 치트 시트, 기계 학습 알고리즘"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e1dc31ec-1acb-463f-ba77-de565d4ddf4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: garye
ms.openlocfilehash: 2bedd77bfc65128a90c6128743016415dd8609d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-algorithm-cheat-sheet-for-microsoft-azure-machine-learning-studio"></a>Microsoft Azure 기계 학습 스튜디오용 기계 학습 알고리즘 치트 시트
hello **Microsoft Azure 컴퓨터 학습 알고리즘 치트 시트** hello 예측 분석 모델에 대 한 올바른 알고리즘을 선택 하는 데 도움이 됩니다.

[Azure 기계 학습 스튜디오](https://studio.azureml.net/) hello에서 알고리즘의 대규모 라이브러리에 ***회귀***, ***분류***, ***클러스터링***, 및 ***이상 탐지*** 제품군입니다. 각 디자인 된 tooaddress 기계 학습 문제의 다른 형식입니다.

## <a name="download-machine-learning-algorithm-cheat-sheet"></a>다운로드: 기계 학습 알고리즘 치트 시트
**여기에 hello 치트 시트를 다운로드: [컴퓨터 학습 알고리즘 치트 시트 (11 x 17 인치)](http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet-v6.pdf)**

![컴퓨터 학습 알고리즘 치트 시트: 자세한 방법을 toochoose 기계 학습 알고리즘입니다.][cheat-sheet]

[cheat-sheet]: ./media/machine-learning-algorithm-cheat-sheet/machine-learning-algorithm-cheat-sheet-small_v_0_6-01.png

다운로드 하 여 도움이 및 g h e l 알고리즘 선택 tabloid 크기 tookeep에 hello 컴퓨터 학습 알고리즘 치트 시트를 인쇄 합니다.

> [!NOTE]
> Hello 문서 참조 [어떻게 toochoose Microsoft Azure 기계 학습 알고리즘](machine-learning-algorithm-choice.md) 자세히 살펴보도록 toousing에 대 한이 치트 시트입니다.
> 
> 

## <a name="more-help-with-algorithms"></a>알고리즘에 대한 자세한 도움말
* 이 치트 시트를 사용 하 여 hello 올바른 알고리즘 및 hello 다양 한 유형의 기계 학습 알고리즘을 사용 하는 방법에 대해 자세히 설명 선택에 대 한 도움말을 참조 하십시오. [방법을 Microsoft Azure 기계 학습은toochoose알고리즘](machine-learning-algorithm-choice.md).
* 알고리즘을 설명하고 예제를 제공하는 다운로드 가능한 인포그래픽은 [다운로드 가능한 인포그래픽: 알고리즘 예제를 포함한 Machine Learning 기본 사항](machine-learning-basics-infographic-with-algorithm-examples.md)을 참조하세요.
* 모든 hello 기계 학습 알고리즘 기계 학습 스튜디오에서 사용할 수 있는의 범주별 목록을 참조 하십시오. [모델 초기화] [ initialize-model] hello Studio 기계 학습 알고리즘 및 모듈 도움말입니다.
* 기계 학습 스튜디오의 전체 알고리즘 및 모듈에 대한 알파벳 순서 목록은 기계 학습 스튜디오 알고리즘 및 모듈 도움말에서 [기계 학습 스튜디오 모듈의 A-Z 목록][a-z-list]을 참조하세요.
* 기계 학습 스튜디오의 hello 기능의 개요 다이어그램 참조 toodownload 및 인쇄 [Azure 기계 학습 스튜디오 기능의 개요 다이어그램](machine-learning-studio-overview-diagram.md)합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="notes-and-terminology-definitions-for-hello-machine-learning-algorithm-cheat-sheet"></a>참고 및 hello 기계 학습 알고리즘에 대 한 용어 정의 치트 시트

* 규칙-thumb의 대략적인이이 알고리즘 치트 시트에서 제공 하는 hello 제안 됩니다. 제안을 변형하거나 명백하게 위반할 수 있습니다. 이 의도 한 toosuggest 시작 지점입니다. 두려워 toorun 데이터에 대해 여러 가지 알고리즘 간의 한 일 경쟁 하지 마십시오. 각 알고리즘의 hello 원칙을 이해 하 고 데이터를 생성 한 hello 시스템 이해에 대 한 조치 단순히는 없습니다.

* 모든 Machine Learning 알고리즘에는 자체 스타일이나 *귀납적 바이어스*가 있습니다. 특정 문제의 경우 여러 알고리즘이 적절할 수 있으며, 한 알고리즘이 다른 알고리즘보다 더 적합할 수 있습니다. 하지만 항상 가능한 tooknow 미리는 hello 가장 적합 한 것은 아닙니다. 이러한 경우 여러 가지 알고리즘 hello 치트 시트에 모두 나열 됩니다. 적합 한 전략 tootry 하나의 알고리즘 고 hello 결과 아직 만족 스러운 경우 다른 hello 시도 됩니다. 다음은 예제 hello에서 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com/) 동일한 데이터와 비교 하 여 hello 결과 hello에 대 한 여러 가지 알고리즘을 실험의: [다중 클래스 분류자 비교: 문자 인식 ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

* Machine Learning의 세 가지 주요 범주는 **감독 학습**, **자율 학습** 및 **보충 학습**입니다.

  * **감독 학습**에서 각 데이터 요소는 관심 범주 또는 값과 연결되거나 해당 레이블이 지정됩니다.  범주 레이블의 예는 이미지를 'cat' 또는 'dog'로 할당하는 것입니다.  값 레이블 예에 사용 되는 자동차와 관련 된 hello 판매 가격입니다. hello 지도 학습의 목적은 toostudy 많은 레이블이 지정 된 이러한 경우 예제와 다음 toobe 이후 데이터 요소에 대 한 수 toomake 예측 합니다. 예를 들어 동물 또는 정확 하 게 판매 가격 tooother 할당 자동차를 사용 하 고 올바른 hello로 새 사진을 식별 합니다. 이는 널리 사용되고 유용한 기계 학습 유형입니다. 학습 알고리즘을 제외 하 고 감독 모든 Azure 기계 학습 모듈 hello [K-means 클러스터링][k-means-clustering]합니다.

  * **자율 학습**에서 데이터 요소에는 연결된 레이블이 없습니다. 대신, 자율된 학습 알고리즘의 목표를 hello 몇 가지 방식으로 또는 toodescribe tooorganize hello 데이터 구조입니다. 이는 K-Means처럼 클러스터로 그룹화하거나 더 간단하게 표시되도록 복잡한 데이터를 보는 다양한 방법을 찾는 것을 의미할 수 있습니다.

  * **강화한 학습**, hello 알고리즘 가져옵니다 toochoose 작업 응답 tooeach 데이터 요소에 있습니다. 것 일반적인 접근 방식은에서 로봇, 여기서 hello 시간에 한 지점 센서 판독값의 집합은 데이터 요소 고 hello 알고리즘 hello 로봇 다음 작업을 선택 해야 합니다. 사물 인터넷의 응용 프로그램에 적합한 학습이기도 합니다. hello 학습 알고리즘 짧은 시간 나중 얼마나 양호한 hello 의사 결정을 나타내는 보상 신호를 받습니다. 이에 따라 hello 알고리즘 순서 tooachieve hello에 대 한 가장 높은 보상에서 해당 전략을 수정 합니다. 현재 Azure 기계 학습에는 보충 학습 알고리즘 모듈이 없습니다.

* **Bayes 방법** 통계적으로 독립적인 데이터 요소의 hello 가정 합니다. 이 즉, 하나의 데이터 요소만 모델링 되지 않은 다양 hello가 아닙니다. 다른 사용자와 상호 관련 된, 즉 예측할 수 없습니다. 예를 들어 hello 데이터가 기록 되 고 hello 시간 (분) 떨어져 있는 하루를 측정 하는 두 개의 측정값 hello 다음 지하철 학습 도착할 때까지 경우은 통계적으로 독립적입니다. 그러나 두 측정 일 분 떨어져 있는 통계적으로 독립적-hello 값이 매우 다른 hello hello 값의 예측 합니다.

* **승격된 의사 결정 트리 회귀 모델**은 기능 겹침 또는 기능 간의 상호 작용을 활용합니다. 의미를 지정 된 모든 데이터를 하나의 기능의 값 hello는 약간 다른 hello 값의 예측입니다. 예를 들어 일일 온도 높은/낮은 데이터 hello 날에 대 한 hello 낮은 온도 알고 있으면 있습니다 toomake를 합리적인 추측 높은 hello에서. hello 두 기능에 포함 된 hello 정보 다소 중복 됩니다.

* 본질적으로 다중 클래스 분류자를 사용하거나 두 클래스 분류자 집합을 하나의 **앙상블**로 결합하면 데이터를 세 개 이상의 범주로 분류할 수 있습니다. Hello 앙상블 방법에서은 각 클래스에 대 한 별도 2 클래스 분류자-hello 데이터 두 가지 범주로 구분 하는 각: ""이이 클래스"이 클래스를 제외한이 있습니다." 그런 다음 이러한 분류자 hello 올바르게 지정 hello 데이터 요소에 대해 투표 합니다. 이 hello operational 원칙 [-One-vs-all 다중 클래스][one-vs-all-multiclass]합니다.

* 로지스틱 회귀 및 hello Bayes 지점 컴퓨터를 포함 하는 여러 가지 방법을 가정 **선형 클래스 경계**합니다. 즉, 해당 hello 가정 클래스 간의 경계가 약 직선 (또는에 hyperplanes hello 보다 일반적인 경우). 대 개의 경우이 특성의 hello 데이터, 하지만 tooseparate을 시도한 후까지 모르는 리 있는 일반적으로 미리 시각화 하 여 피어에서 확인 될 수 있습니다. Hello 클래스 경계 매우 비정상적인 것, 계속 들어 의사 결정 트리, 의사 결정 정글, 지원 벡터 컴퓨터, 신경망입니다.

* 신경망 사용 하 여 범주 변수를 만들어 한 **더미 변수가** 각 범주에 대 한 설정 too1 hello 범주 적용 되는 경우, 0 위치 하지 않습니다.


<!-- This is how you can embed a link in an image in HTML. Don't know how toodo this in markdown.
<a href="http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet.pdf">
<img src="C:\Users\garye\azure-docs-pr\articles\media\machine-learning-algorithm-cheat-sheet\cheat-sheet-small.png">
</a>
-->

<!-- Module References -->
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx
[initialize-model]: https://msdn.microsoft.com/library/azure/0c67013c-bfbc-428b-87f3-f552d8dd41f6/
[k-means-clustering]: https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/
[one-vs-all-multiclass]: https://msdn.microsoft.com/library/azure/7191efae-b4b1-4d03-a6f8-7205f87be664/
