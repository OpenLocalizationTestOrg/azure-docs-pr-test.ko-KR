---
title: "데이터 과학을 위한 데이터 준비 aaaIs? 데이터 평가 - Azure Machine Learning | Microsoft Docs"
description: "데이터 toobe 데이터 과학을 위한 준비에 대 한 4 hello 기준에 알아봅니다. 데이터 과학 초보자를 위한 비디오 2에 대 한 기본 데이터 평가 된 구체적인 예 toohelp에 있습니다."
keywords: "관련 데이터,데이터 평가,데이터 준비,데이터 기준,데이터 준비"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: ef6bb680ace771537157dbdd50a4ccce0a3eb7ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="is-your-data-ready-for-data-science"></a>데이터 과학에 사용할 수 있게 데이터가 준비되었나요?
## <a name="video-2-data-science-for-beginners-series"></a>비디오 2: 초급자를 위한 데이터 과학 시리즈
자세한 방법을 tooevaluate 사용자 데이터 toomake 기본 조건은 toobe 데이터 과학을 위한 준비를 충족 하는지 확인 합니다.

hello 시리즈를 최대한 활용 tooget hello 모두 보기 [비디오 이동 toohello 목록](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a>이 시리즈의 다른 비디오
*초보자를 위한 데이터 과학* 는 5 개의 짧은 비디오의 간략 한 소개 toodata 과학 합니다.

* 비디오 1: [hello 5 데이터 과학 답변의 질문](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 분 14 초)*
* 비디오 2: 데이터 과학에 사용할 수 있게 데이터가 준비되었나요?
* 비디오 3: [데이터로 대답할 수 있는 질문하기](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4분 17초)*
* 비디오 4: [단순 모델을 사용하여 답변 예측](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7분 42초)*
* 비디오 5: [타인의 작업 toodo 데이터 과학 복사](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 분 18 초)*

## <a name="transcript-is-your-data-ready-for-data-science"></a>비디오 내용: 데이터 과학에 사용할 수 있게 데이터가 준비되었나요?
시작 너무 "는 데이터 데이터 과학을 위한 준비"? hello 시리즈에서 두 번째 비디오 hello *초보자를 위한 데이터 과학*합니다.  

데이터 과학 제공할 수 원하는 대답 hello, toogive 있는 것으로 고품질 원자재 toowork 일부입니다. 피자를 만드는 것과 같습니다 hello 더 나은 hello 구성 요소로 시작 하 여 hello 더 잘 hello 최종 제품입니다. 

## <a name="criteria-for-data"></a>데이터 기준
따라서 데이터 과학자의 경우 hello는 toopull 함께 필요한 몇 가지 구성 요소가 있습니다.

다음과 같은 데이터가 필요합니다.

* 관련성
* 연결됨
* 정확함
* 충분 한 toowork와

## <a name="is-your-data-relevant"></a>여러분의 데이터는 관련성이 있나요?
따라서 첫 번째 요소 hello-관련 데이터를 필요 합니다.

![관련 데이터 및 관련이 없는 데이터 - 데이터 평가](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

Hello 왼쪽에서 hello 테이블을 보고 합니다. म 보스턴 막대에 속하지 않은 7 개인 충족, 해당 피 주류 수준, hello Red Sox 타율의 마지막 게임에서 및 hello 가격 편리 하 게 저장소에 가장 가까운 hello에 우유를 측정 합니다.

이 모든 것은 완벽하게 합법적인 데이터입니다. 유일한 결함은 서로 관련성이 없다는 것입니다. 이러한 수치 간에는 명확한 관계가 없습니다. 내가 준 우유 및 hello Red Sox 타율의 현재 가격 hello 면 없으므로 내 피 주류 콘텐츠를 볼 수 있습니다.

이제 hello 오른쪽에 hello 테이블 살펴보겠습니다. 이 시간 가졌던 한 음료 수가 본문 대용량 및 계산 hello 각 사람의 측정 했습니다.  각 행에 hello 숫자 다른 tooeach 관련 됩니다. 내가 준 됐 Margaritas 내 본문 mass 및 hello 수, 하는 경우 만들 수 피 내에서 추측 주류 콘텐츠.

## <a name="do-you-have-connected-data"></a>연결된 데이터가 있습니까?
hello 다음 요소는 연결 된 데이터입니다.

![연결된 데이터 및 연결되지 않은 데이터 - 데이터 기준, 데이터 준비](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

다음은 hamburgers의 hello 품질에 관련 된 일부 데이터: 온도, patty 가중치 및 잡지 hello 로컬 음식 등급 grill 합니다. 하지만 hello 왼쪽에 hello 테이블에서의 hello 차이 확인 합니다.

대부분의 데이터 집합에서 일부 값이 누락되어 있습니다. 다음과 같은 일반적인 toohave 구멍 되며 주위 toowork 방법으로. 하지만 데이터 시작 있어서 같은 toolook가 없습니다. 너무 많은 경우.

누락 된 데이터 크기 것 이므로 모든 종류의 관계를 하드 toocome는 hello 왼쪽에 hello 표를 보면 grill 온도 patty 두께입니다. 연결되지 않은 데이터의 예입니다.

그러나 hello 오른쪽에 테이블을 hello, 꽉 차서 완료-연결 된 데이터의 예입니다.

## <a name="is-your-data-accurate"></a>데이터가 정확한가요?
hello 필요한 다음 요소는 정확성입니다. 화살표가 있는 toohit 싶습니다 대상을 5는 다음과 같습니다.

![정확한 데이터 및 부정확한 데이터 - 데이터 기준](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

Hello 오른쪽 위에 있는 hello 대상 확인 합니다. Hello bullseye 동안만 긴밀 하 게 그룹화를 설명 했습니다. 물론 정확한 편입니다. 이상 하 게 데이터 과학자의 hello 언어로 실적 hello 대상 오른쪽 아래에 또한 간주 정확 하 게 합니다.

이 화살표의 hello 센터 toomap 인 경우 매우 가까운 toohello bullseye 임을 표시 됩니다. 가운데에 오도록 hello bullseye 주위 있으므로 하는 것으로 간주 정확 하지만 이러한 정확 하지 않은 간주 하는 hello 화살표 hello 대상 주위의 모든 분산 됩니다.

이제 왼쪽 위 대상 hello 살펴보겠습니다. 화살끼리 매우 가깝게 모여 있습니다. Precise, 하지만 달라도 정확 하 게 hello 센터는 hello bullseye 해제 방법 이기 때문입니다. 및 물론, hello 왼쪽 아래 대상의 hello 화살표는 부정확 하 고 정확 하지 않은 합니다. 이 궁수는 좀 더 연습이 필요합니다.

## <a name="do-you-have-enough-data-toowork-with"></a>와 충분 한 데이터 toowork 있습니까?
마지막으로, 요소 #4-toohave 충분 한 데이터가 필요 합니다.

![분석을 위한 충분한 데이터가 있나요? 데이터 평가](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

표의 각 데이터 요소를 그림의 붓 자국을 생각해보세요. 그 중 일부만 있는, hello 그리기 상당히 유사 항목 일 수 있습니다-하드 tootell는 어떤 경우입니다.

더 많은 몇 개의 브러시 스트로크를 추가 하는 경우 페인트 tooget는 약간 더 선명 하 게 시작 합니다.

충분 한 거의 스트로크를 사용 하는 경우 몇 가지 광범위 한 결정에 충분 한 toomake만 볼 수 있습니다. Toovisit 원하는 수 위치는 무엇입니까? 밝고 깨끗한 물처럼 보입니다. 맞습니다. 제가 휴가를 보내고 싶은 곳입니다.

더 많은 데이터를 추가 하면 hello 그림 더 명확 하 게 되며 보다 세부적인된 결정을 내릴 수 있습니다. 이제 I 확인 hello hello 왼쪽된 은행에 3 개의 호텔 됩니다. 아시다시피 정말 마음에 hello 포그라운드로 hello 하나의 hello 아키텍처 기능이 있습니다. 하겠습니다 곳에서 나, 세 번째 층 hello에 있습니다.

관련, 연결 된 정확한 데이터와 충분 한, 일부 고품질 데이터 과학 toodo 해야 하는 모든 hello 구성 요소는 및입니다.

다른 4 개의 비디오 hello 아웃 있는지 toocheck 수 *초보자를 위한 데이터 과학* Microsoft Azure 기계 학습에서 합니다.

## <a name="next-steps"></a>다음 단계
* [Machine Learning Studio로 첫 번째 데이터 과학 실험 시도](machine-learning-create-experiment.md)
* [가져오기 소개 tooMachine Microsoft Azure에서 학습](machine-learning-what-is-machine-learning.md)
