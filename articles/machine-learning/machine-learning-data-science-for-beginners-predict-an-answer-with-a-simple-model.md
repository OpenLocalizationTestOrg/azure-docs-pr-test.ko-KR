---
title: "간단한 회귀 모델-Azure 기계 학습에 대 한 답변 aaaPredict | Microsoft Docs"
description: "어떻게 toocreate 간단한 회귀 비디오 4 초보자를 위한 데이터 과학에서 가격 toopredict를 모델링 합니다. 대상 데이터와 함께 선형 회귀가 포함됩니다."
keywords: "모델 만들기,단순 모델,가격 예측,단순 회귀 모델"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a>단순 모델을 사용하여 답변 예측
## <a name="video-4-data-science-for-beginners-series"></a>비디오 4: 초급자를 위한 데이터 과학 시리즈
간단한 회귀 모델 toopredict toocreate 비디오 4 초보자를 위한 데이터 과학에 다이아몬드의 가격 hello 하는 방법에 대해 알아봅니다. 대상 데이터를 사용하여 회귀 모델을 그려볼 것입니다.

hello 시리즈를 최대한 활용 tooget hello 모두 보기 [비디오 이동 toohello 목록](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a>이 시리즈의 다른 비디오
*초보자를 위한 데이터 과학* 는 5 개의 짧은 비디오의 간략 한 소개 toodata 과학 합니다.

* 비디오 1: [hello 5 데이터 과학 답변의 질문](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 분 14 초)*
* 비디오 2: [데이터 과학에 사용할 수 있게 데이터가 준비되었나요?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4분 56초)*
* 비디오 3: [데이터로 대답할 수 있는 질문하기](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4분 17초)*
* 비디오 4: 단순 모델을 사용하여 답변 예측
* 비디오 5: [타인의 작업 toodo 데이터 과학 복사](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 분 18 초)*

## <a name="transcript-predict-an-answer-with-a-simple-model"></a>비디오 내용: 단순 모델을 사용하여 답변 예측
Toohello hello "데이터 과학에 대 한 초보자를 위한" 시리즈의에서 네 번째 동영상을 시작 합니다. 여기서는 간단한 모델을 빌드하고 예측을 진행할 것입니다.

*모델* 은 데이터에 대한 간소화된 이야기입니다. 무슨 의미인지 보여드리겠습니다.

## <a name="collect-relevant-accurate-connected-enough-data"></a>관련성 있고, 정확하고, 연결된 충분한 데이터 수집
다이아몬드의 tooshop을 한다고 가정 하겠습니다. 에 속한 1.35 캐럿 다이아몬드에 대 한 설정 사용 하 여 toomy 할머니 링 있고 tooget 가격은 어느 정도 이해 합니다. Hello 보석 저장소로 메모장 및 펜 걸릴 및 내가 모든 hello 대/소문자 및 carats 어느 정도 입니까은 hello 다이아몬드의 hello 가격 기록 합니다. Hello 첫 번째 다이아몬드-1.01 carats 및 $7,366로 시작합니다.

이제 하 고이 작업을 수행 모든 hello에 대 한 hello 저장소에서 다른 다이아몬드입니다.

![다이아몬드 데이터 열](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

목록에는 두 개의 열이 있습니다. 각 열은 캐럿 무게와 가격의 두 가지 다른 특성을 포함하며 각 행은 1개의 다이아몬드를 나타내는 단일 데이터 요소를 포함합니다.

실제로 여기에 작은 데이터 집합인 표를 만들었습니다. 이 표가 우리의 품질 기준을 충족한다는 것을 알 수 있습니다.

* hello 데이터는 **관련** -가중치는 확실 하 게 관련된 tooprice
* 있기 **정확한** -म म 적어 hello 가격을 다시 확인
* **연결되어 있음** - 이러한 열에는 공백이 없습니다.
* 볼 수 있겠지만, 및가 **충분 한** 데이터 tooanswer 우리의 질문

## <a name="ask-a-sharp-question"></a>정확하게 질문하기
이제 날카로운 방식으로 우리의 질문을 야기 합니다 했습니다: "는 비용 비용 toobuy 1.35 캐럿 다이아몬드?"

이 목록은 없는 1.35 캐럿 다이아몬드, toouse hello 나머지 우리의 데이터 tooget 응답 toohello 질문 해야 합니다.

## <a name="plot-hello-existing-data"></a>Hello 기존 데이터 표시
hello 먼저 하겠습니다 점은 긋습니다 번호, 축, toochart hello 가중치를 호출 합니다. hello 범위의 hello 가중치 0 too2 이므로 범위 및 각 절반 캐럿에 대 한 틱 put을 검사 하는 줄을 내릴 합니다.

그런 다음 세로 축 toorecord hello 가격을 그릴 알아보고 toohello 가중치 가로 축 연결 하겠습니다. 단위는 달러가 됩니다. 이제 좌표축이 설정되었습니다.

![무게 및 가격 축](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

현재 진행 중인 tootake이이 데이터 이제로 설정 된 *산 점도*합니다. 이것이 좋은 방법 toovisualize 숫자 데이터 집합입니다.

첫 번째 데이터 요소 hello에 대 한 1.01 carats에서 세로 선을 파악 했습니다. 그런 다음 $7,366에 해당하는 수평선을 확인합니다. 만나는 위치에 점을 그립니다. 이것은 첫 번째 다이아몬드를 나타냅니다.

이제이 목록에 각 다이아몬드를 통해 이동 하 고 동일한 작업을 hello 수행 합니다. 다 끝나면 각 다이아몬드에 하나씩 여러 개의 점이 그려집니다.

![산점도](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a>Hello 데이터 요소를 통해 그리기 hello 모델
이제 hello 점과 squint 보면 hello 컬렉션 fat, 유사 항목 줄 같이 표시 합니다. 마커를 사용해서 그 사이로 직선을 그릴 수 있습니다.

선을 그려서 *모델*을 만들었습니다. Hello 현실 세계 차지 하 고 그 단순한 만화 버전으로 생각 됩니다. 이제 hello 만화 잘못 되었습니다.-hello 줄 모든 hello 데이터 요소를 통해 이동 하지 않습니다. 하지만 유용한 단순화 기법입니다.

![선형 회귀 선](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

hello 점으로 거치지 않습니다 정확 하 게 hello 줄 hello 팩트는 정상입니다. 데이터 과학자 hello-된 모델을 hello 선-임을 한다는 것으로이 설명 하 고 각 점의 대 한 일부 *노이즈* 또는 *분산* 연관 됩니다. 완벽 한 관계를 원본으로 사용 하는 hello 않으며 노이즈와 불확실 한 정보를 추가 하는 hello 해보겠습니다, 실제 세계 않으면입니다.

Tooanswer hello 질문 त ु म 때문에 *얼마나 됩니까?* 라고는 *회귀*합니다. 또한 직선을 사용하므로 *선형 회귀*에 해당합니다.

## <a name="use-hello-model-toofind-hello-answer"></a>Hello 모델 toofind hello 답변을 사용 하 여
이제 우리에게는 모델이 있고 “1.35 캐럿의 다이아몬드 가격은 얼마나 될까요?”라는 질문을 해보겠습니다.

tooanswer 우리의 질문 1.35 carats 파악 하 고 세로 선을 그립니다. Hello 모델 선과 교차, 여기서 가로줄 toohello 달러 축을 파악 했습니다. 정확히 10,000에 닿네요. 와우 그렇다면 이게 정답입니다. Hello 대답은: 1.35 캐럿 다이아몬드 약 10, 000 달러 비용이 듭니다.

![Hello 모델에 hello 답변 찾기](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a>신뢰 구간 만들기
것이 자연 toowonder 어떻게이 예측은 정확 합니다. Hello 1.35 캐럿 다이아몬드 너무 매우 가까운 됩니다 유용 tooknow가 $ 10, 000, 또는 위 또는 아래로 많은 합니다. toofigure이 out, 봉투 (envelope)의 hello 점 대부분을 포함 하는 hello 회귀선 주위를 그릴 보겠습니다. 이 봉투 (envelope이) 라고 우리의 *신뢰 구간*: We're 때문에이 봉투 속하는 가격 확신 상당히 지난 hello에서 그 중 대부분 합니다. 해당 봉투의 hello 위아래 hello hello 1.35 캐럿 줄이 교차 하는 곳에서 두 개 가로 줄 내릴 수 있습니다.

![예측](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

이제 우리 수 예를 신뢰 구간 우리의: 수 말할 자신 있게 1.35 캐럿 다이아몬드의 hello 가격 약 $10000-하지만 $8000 낮은 것 이며 함을 $ 12, 000으로 높을 수 있습니다.

## <a name="were-done-with-no-math-or-computers"></a>수학이나 컴퓨터 없이도 해냈습니다.
어떤 데이터 과학자 toodo, 지급에 수행한 및 그리기 만으로 했던:

* 데이터로 답변할 수 있는 질문을 했습니다.
* *선형 회귀*를 사용하여 *모델*을 작성했습니다.
* *신뢰 구간*을 토대로 *예측*을 했습니다.

Toodo 수학 또는 컴퓨터를 사용 하지 않았습니다 고 것입니다.

우리에게 더 많은 정보가 있었다면, 예를 들어

* hello는 hello 다이아몬드의 잘라내기
* 색상 변경 (얼마나 비슷한지를 hello 다이아몬드는 toobeing 흰색)
* hello 수가 hello 다이아몬드에 포함

그러면 더 많은 열이 형성될 것입니다. 이 경우에는 수학이 도움이 됩니다. 을 두 개 이상의 열이 있는 경우 용지에 하드 toodraw 점입니다. hello 수학을 사용 하면 해당 줄 또는 해당 평면 tooyour 데이터를 매우 잘 맞습니다.

또한 다이아몬드 몇 개가 아니라 2,000개 또는 2백만 개가 있다면 컴퓨터로 훨씬 더 빠르게 이러한 작업을 처리할 수 있습니다.

오늘 toodo 선형 회귀 되 고, 설정 하는 방법 데이터를 사용 하 여 예측에 대 한 콘텐츠입니다.

Hello 아웃 있는지 toocheck "데이터 과학에 대 한 초보자를 위한"에서 Microsoft Azure 기계 학습에서 비디오를 다른 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [Machine Learning Studio로 첫 번째 데이터 과학 실험 시도](machine-learning-create-experiment.md)
* [가져오기 소개 tooMachine Microsoft Azure에서 학습](machine-learning-what-is-machine-learning.md)
