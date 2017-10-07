---
title: "데이터 과학 aaaThe 5-초보자를 위한 데이터 과학-Azure 기계 학습의 질문 | Microsoft Docs"
description: "데이터 과학 초보자는에서는 5 짧은 비디오의 기본 개념 hello 5 질문 데이터 과학 대답으로 시작 합니다. Azure Machine Learning"
keywords: "데이터 과학 수행,데이터 과학 초급자,초급자를 위한 데이터 과학, 데이터 과학 기본 사항,데이터 과학 질문,데이터 과학 비디오, 데이터 과학 소개"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a01f93ee-01eb-4afe-abbd-cfa035c119b0
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 6de0ca22556771a3044520d9ccc6771c3de78771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-for-beginners-video-1-hello-5-questions-data-science-answers"></a>데이터 과학 초보자를 위한 비디오 1: hello 5 데이터 과학 답변의 질문
간략 한 소개 toodata 과학 가져오기 *초보자를 위한 데이터 과학* 최상위 데이터 과학자에서 5 개의 짧은 비디오에서 합니다. 이러한 비디오는 기초적이지만 데이터 과학에 관심이 있든 데이터 과학자와 함께 일하든 상관없이 유용한 정보를 제공합니다.

이 첫 번째 비디오는 hello 종류의 데이터 과학 응답할 수 있는 질문에 대 한 선택 됩니다. hello 시리즈를 최대한 활용 tooget hello 모두 보기 [비디오 이동 toohello 목록](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/8/player]
>
>

## <a name="other-videos-in-this-series"></a>이 시리즈의 다른 비디오
*초보자를 위한 데이터 과학* 25 분 총 라인으로 전환 하는 간략 한 소개 toodata 과학 됩니다. 5개의 비디오를 모두 확인해 보세요.

* 비디오 1: hello 5 데이터 과학 답변의 질문
* 비디오 2: [데이터 과학에 사용할 수 있게 데이터가 준비되었나요?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4분 56초)*
* 비디오 3: [데이터로 대답할 수 있는 질문하기](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4분 17초)*
* 비디오 4: [단순 모델을 사용하여 답변 예측](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7분 42초)*
* 비디오 5: [타인의 작업 toodo 데이터 과학 복사](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 분 18 초)*

## <a name="transcript-hello-5-questions-data-science-answers"></a>대화 내용: hello 5 데이터 과학 답변의 질문
안녕하세요. Toohello 비디오 시리즈 시작 *초보자를 위한 데이터 과학*합니다.

데이터 과학 아주 수 있으므로 hello 기본 사항 여기 수식 또는 특수 용어를 프로그래밍 하는 컴퓨터 없이 소개 하겠습니다.

"Hello 5 개의 질문 데이터 과학 답변입니다." 방법에 대해 알아보겠습니다이 첫 번째 비디오

데이터 과학 번호를 사용 하 여 및 이름 (라고도: 범주 또는 레이블) toopredict tooquestions에 응답 합니다.

뜻밖일 수도 있지만 *데이터 과학으로 답변되는 질문은 다음 5개뿐입니다*.

* 이것은 A인가요 B인가요?
* 이것은 이상한가요?
* 양 또는 개수는 얼마인가요?
* 어떻게 구성되어 있나요?
* 다음에는 어떻게 해야 하나요?

이러한 각 질문은 알고리즘이라고 하는 별도의 기계 학습 방법군에 따라 답변됩니다.

레시피도 알고리즘 및 hello 구성 요소와 데이터에 대 한 유용한 toothink 것합니다. 알고리즘 어떻게 toocombine 및 혼합 hello 데이터 순서 tooget에 대 한 답변을 지시 합니다. 컴퓨터는 믹서기와 같습니다. 대부분 hello 알고리즘의 hello 복잡 한 작업의 수와 상당히 빠르게 수행 합니다.

## <a name="question-1-is-this-a-or-b-uses-classification-algorithms"></a>질문 1: 이것은 A인가요 B인가요?에서는 분류 알고리즘을 사용합니다.
Hello 질문부터 시작 하겠습니다:이 A 또는 B가?

![분류 알고리즘: 이것은 A인가요 B인가요?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/classification-algorithms.png)

이 알고리즘군을 2클래스 분류라고 합니다.

두 가지 가능한 답변이 있는 질문에 유용합니다.

예:

* 이 tire 못합니다 hello에 다음 1, 000 마일: Yes 또는 no?
* 어떤 방식이 더 많은 고객을 이끌까요? 5달러 쿠폰 또는 25% 할인?

이 질문에는 두 가지 옵션이 둘 이상의 문제나 tooinclude 될 수도 있습니다:이 A 또는 B 또는 C 또는 D, 등입니다?  이것을 다중 클래스 분류라고 하며 이 분류 방식은 몇 개 또는 몇천 개의 가능한 답변이 있을 때 유용합니다. 다중 클래스 분류 hello 가능성이 가장 높은 하나를 선택합니다.

## <a name="question-2-is-this-weird-uses-anomaly-detection-algorithms"></a>질문 2: 이것은 이상한가요?는 변칙 감지 알고리즘을 사용합니다.
데이터 과학 대답할 수 있는 hello 다음 질문은:이 생소할은? 이 질문은 변칙 감지라고 하는 알고리즘군을 통해 답변됩니다.

![변칙 감지 알고리즘: 이것은 이상한가요?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/anomaly-detection-algorithms.png)

신용 카드가 있는 경우 이미 변칙 감지를 통한 혜택을 보고 있는 것입니다. 신용 카드 회사 toopossible 사기 행위 경고 있습니다 수 있도록 구매 패턴을 분석 합니다. "이상하게" 요금이 청구되었다면 평소에 물건을 구매하지 않던 매장에서 구매하거나 굉장히 비싼 가격의 상품을 구매해서일 수 있습니다.

이 질문은 다양한 측면에서 유용할 수 있습니다. 예:

* 압력 계기를 사용 하는 자동차를 설정한 경우 tooknow 할 수 있습니다: 일반 읽기이 압력 계기는?
* 모니터링 하는 경우 인터넷 hello, tooknow 원하는: hello에서이 메시지는 일반적인 인터넷?

변칙 감지는 예기치 않거나 비정상적인 이벤트 또는 동작에 플래그를 지정합니다. 단서를 제공 여기서 toolook 문제에 대 한 합니다.

## <a name="question-3-how-much-or-how-many-uses-regression-algorithms"></a>질문 3: 양 또는 개수는 얼마인가요?에서는 회귀 알고리즘을 사용합니다.
기계 학습을 예측할 수도 hello 응답 tooHow 훨씬? 방식이 나 많은? 이 질문에 응답 하는 hello 알고리즘 패밀리 회귀를 라고 합니다.

![회귀 알고리즘: 양 또는 개수는 얼마인가요?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/regression-algorithms.png)

회귀 알고리즘은 다음과 같은 수치 예측을 수행합니다.

* 다음 화요일 수 온도 hello는 무엇입니까?  
* 4사분기 매출은 얼마나 될까요?

수치를 요구하는 질문에 답변하는 데 도움이 됩니다.

## <a name="question-4-how-is-this-organized-uses-clustering-algorithms"></a>질문 4: 어떻게 구성되어 있나요?에서는 클러스터링 알고리즘을 사용합니다.
이제 hello 마지막 두 개의 질문은 더 높은 수준의 비트입니다.

데이터 집합의 toounderstand hello 구조를 원하는 경우에 따라이 구성 되어? 이 질문의 경우 여러분이 결과를 이미 알고 있는 예제는 없을 것입니다.

데이터의 hello 구조 아웃 방식으로 tootease 많이 가지가 있습니다. 한 가지 방법은 클러스터링입니다. 이 방식은 보다 쉬운 해석을 위해 데이터를 적절한 "그룹"으로 분리합니다. 클러스터링을 사용하면 한 가지 정답은 없습니다.

![클러스터링 알고리즘: 어떻게 구성되어 있나요?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/clustering-algorithms.png)

질문을 클러스터링하는 일반적인 예제는 다음과 같습니다.

* 어떤 뷰어 동일 hello와 같은 유형의 영화?
* 어떤 프린터 모델 hello 실패 같은 방식으로?

데이터가 구성된 방식을 이해하면 동작 및 이벤트를 더 잘 이해하고 예측할 수 있게 됩니다.  

## <a name="question-5-what-should-i-do-now-uses-reinforcement-learning-algorithms"></a>질문 5: 이제 어떻게 해야 하나요?에서는 강화 학습 알고리즘을 사용합니다.
hello 마지막 질문 – 어떻게 해야 합니까? 강화 학습이라는 알고리즘군을 사용합니다.

보충 학습 rat 및 인간이 hello 브레인 toopunishment 및 보상의 대처 방법을에서 영감을 얻은 되었습니다. 이러한 알고리즘에서 결과 알아보고 hello 다음 동작을 결정 합니다.

일반적으로 지원용 학습은 toomake 많은 휴먼 도움 없이 작은 결정의 자동화 된 시스템에 적합 합니다.

![강화 학습 알고리즘: 다음에는 어떻게 해야 하나요?](./media/machine-learning-data-science-for-beginners-the-5-questions-data-science-answers/reinforcement-learning-algorithms.png)

답변되는 질문은 일반적으로 기계나 로봇에 의해 진행되는 작업에 대한 것입니다. 예:

* 저는 집을 온도 제어 시스템: hello 온도 조정 하거나 경우 그대로?  
* 내가 자동 주행 자동차라면 노란색 신호등에서 브레이크를 밟을까요? 아니면 가속 패달을 밟을까요?  
* 로봇 항목이 대 한: 밍, 유지 또는 스테이션 충전 toohello 돌아가서?

강화 학습 알고리즘은 진행하면서 데이터를 수집하고 시행 착오를 통해 학습합니다.

설정 작업이 완료-하므로 hello 5 질문 데이터 과학 응답할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [Machine Learning Studio로 첫 번째 데이터 과학 실험 시도](machine-learning-create-experiment.md)
* [가져오기 소개 tooMachine Microsoft Azure에서 학습](machine-learning-what-is-machine-learning.md)
