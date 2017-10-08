---
title: "기계 학습 스튜디오에서 간단한 실험 aaaA | Microsoft Docs"
description: "이 기계 학습 자습서에서는 쉬운 데이터 과학 실험을 안내합니다. 회귀 알고리즘을 사용 하는 자동차의 hello 가격을 예측할 합니다 했습니다."
keywords: "실험, 선형 회귀, 기계 학습 알고리즘, 기계 학습 자습서, 예측 모델링 기술, 데이터 과학 실험"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a>기계 학습 자습서: Azure 기계 학습 스튜디오에서 첫 번째 데이터 과학 실험 만들기

**Azure Machine Learning Studio**를 사용한 경험이 없는 경우 이 자습서는 도움이 됩니다.

이 자습서에서는 살펴봅니다 방법 toouse Studio hello에 대 한 첫 번째 toocreate 기계 학습 실험을 합니다. hello 실험 제조업체와 기술 사양 등 다른 변수를 기반으로 하는 자동차의 hello 가격을 예측 하는 분석 모델을 테스트 합니다.

> [!NOTE]
> 이 자습서에서는 사용 하 여 실험에 어떻게 toodrag 놓기 모듈의 기본 사항 hello 이들을 서로 연결 hello 실험을 실행 하 고 hello 결과를 확인 합니다. 하지 않겠습니다 toodiscuss hello 기계 학습의 일반 항목 또는 방법을 사용 하 여 tooselect 환영 100 + 기본 제공 알고리즘 및 데이터 조작 모듈 스튜디오에 포함 되어 있습니다.
>
>새 toomachine 학습 인 경우 hello 비디오 시리즈 [초보자를 위한 데이터 과학](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) 좋은 위치 toostart 될 수 있습니다. 이 비디오 시리즈 일상적인 언어 및 개념을 사용 하 여 충분히 소개 toomachine 학습입니다.
>
>기계 학습에 익숙한 경우, 기계 학습 스튜디오 및 hello 기계 학습 포함 된 알고리즘에 대 한 일반적인 내용은 원하는 좋은 몇 가지 리소스가 다음과 같습니다.
>
- [기계 학습 스튜디오란 무엇인가요?](machine-learning-what-is-ml-studio.md) - Studio의 차원 높은 개요입니다.
- [알고리즘 예제를 사용한 기본 사항 학습 컴퓨터](machine-learning-basics-infographic-with-algorithm-examples.md) -이 인포 그래픽은 toolearn hello 다양 한 유형의 기계 학습 스튜디오에 포함 된 기계 학습 알고리즘에 대 한 자세한를 원하는 경우에 유용 합니다.
- [기계 학습 설명서](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -이 가이드에서는 위의 hello 인포 그래픽 동일 하지만 대화형 형식으로 유사한 정보를 다룹니다.
- [시스템 학습 알고리즘 치트 시트](machine-learning-algorithm-cheat-sheet.md) 및 [어떻게 toochoose Microsoft Azure 기계 학습 알고리즘](machine-learning-algorithm-choice.md) -이 다운로드할 수 있는 포스터와 함께 제공 된 문서 심층에서 hello Studio 알고리즘에 설명 합니다.
- [기계 학습 스튜디오: 알고리즘 및 모듈 도움말](https://msdn.microsoft.com/library/azure/dn905974.aspx) -이 hello 기계 학습 알고리즘을 포함 하 여 모든 스튜디오 모듈에 대 한 전체 참조

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a>기계 학습 스튜디오는 도움이 되나요?

기계 학습 스튜디오 예측 모델링 기술로 미리 프로그래밍 끌어서 놓기 모듈을 사용 하 여 실험을 쉽게 tooset이 있습니다.

대화형 시각적 작업 영역을 사용하여 ***데이터 집합*** 및 분석 ***모듈***을 대화형 캔버스로 끌어서 놓습니다. 함께 tooform를 연결 된 ***실험*** 기계 학습 스튜디오에서 실행 하는 합니다.
하면 ***모델을 만들***, ***hello 모델을 학습***, 및 ***점수 및 테스트 모델 hello***합니다.

Hello 실험을 편집 하면 모델 디자인에 대해 반복할 수 및 원하는 결과 hello 제공 될 때까지 실행 합니다. 모델이 준비되면 ***웹 서비스***로 게시하여 다른 사람이 새 데이터를 전송하고 예측 결과를 얻을 수 있습니다.

## <a name="open-machine-learning-studio"></a>Machine Learning Studio 열기

Studio에서 시작 tooget 너무 이동[https://studio.azureml.net](https://studio.azureml.net)합니다. 이전에 Machine Learning Studio에 등록했다면 **로그인**을 클릭합니다. 그렇지 않은 경우 **여기서 등록**을 클릭하고 무료와 유료 옵션 중 하나를 선택합니다.

![TooMachine 학습 스튜디오에 로그인][sign-in-to-studio]
<br/>
***TooMachine 학습 스튜디오에 로그인***

## <a name="five-steps-toocreate-an-experiment"></a>5 단계 toocreate 실험

이 컴퓨터 학습 자습서의 다섯 가지 기본 단계 toobuild 기계 학습 스튜디오 toocreate, 학습의 실험을 수행 하 고 모델 점수를 매깁니다. 합니다.

- **모델 만들기**
    - [1단계: 데이터 가져오기]
    - [2 단계: hello 데이터 준비]
    - [3단계: 기능 정의]
- **Hello 모델 학습**
    - [4단계: 학습 알고리즘 선택 및 적용]
- **모델을 hello 점수 및 테스트**
    - [5단계: 새 자동차 가격 예측]

[1단계: 데이터 가져오기]: #step-1-get-data
[2 단계: hello 데이터 준비]: #step-2-prepare-the-data
[3단계: 기능 정의]: #step-3-define-features
[4단계: 학습 알고리즘 선택 및 적용]: #step-4-choose-and-apply-a-learning-algorithm
[5단계: 새 자동차 가격 예측]: #step-5-predict-new-automobile-prices

> [!TIP] 
> Hello의 작업 복사본을 찾을 수 있습니다 다음 hello에 실험 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com)합니다. 너무 이동**[여 첫 번째 데이터 과학 자동차 가격 예측 실험](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  클릭 **Studio에서 열기** toodownload hello 실험에 기계 학습의 복사본 스튜디오 작업 영역입니다.


## <a name="step-1-get-data"></a>1단계: 데이터 가져오기

hello 먼저 tooperform 기계 학습 데이터입니다.
Machine Learning Studio에는 사용할 수 있고 다양한 원본에서 데이터를 가져올 수 있는 여러 샘플 데이터 집합이 있습니다. 이 예제에서는 hello 샘플 데이터 집합 사용 **자동차 가격 데이터 (Raw)**, 작업 영역에 포함 된 합니다.
이 데이터 집합에는 제조업체, 모델, 기술 사양 및 가격과 같은 정보를 포함하여 여러 개별 자동차에 대한 항목이 포함되어 있습니다.

Tooget 실험으로 데이터 집합을 hello 하는 방법을 다음과 같습니다.

1. 클릭 하 여 새 실험 만들기 **+ 새로 만들기** hello 기계 학습 스튜디오 창의 hello 맨 아래에 선택 **실험**를 선택한 후 **빈 실험**합니다.

2. hello 실험에는 hello 캔버스의 hello 위쪽에 표시 될 수 있는 기본 이름이 지정 됩니다. 이 텍스트를 선택 하 고 이름을 바꾸거나 toosomething 의미 있는 예를 들어 **자동차 가격 예측**합니다. hello 이름 toobe 고유 필요 하지 않습니다.

    ![Hello 실험 이름 바꾸기][rename-experiment]

2. hello 실험 캔버스의 toohello 왼쪽 데이터 집합 및 모듈의 팔레트입니다. 형식 **automobile** 이 색상표 toofind hello 데이터 집합의 레이블이 지정 된 hello 상단 hello 검색 상자에 **자동차 가격 데이터 (Raw)**합니다. 이 데이터 집합 toohello 실험 캔버스를 끕니다.

    ![Hello 자동차 데이터 집합을 찾아서 hello 실험 캔버스로 끌어][type-automobile]
    <br/>
    ***Hello 자동차 데이터 집합을 찾아서 hello 실험 캔버스로 끌어***

toosee이이 데이터는 모양을 처럼 hello 자동차 데이터 집합의 hello 맨 아래에 hello 출력 포트를 클릭 한 다음 선택 **시각화**합니다.

![Hello 출력 포트를 클릭 하 고 "시각화"를 선택 합니다.][select-visualize]
<br/>
***Hello 출력 포트를 클릭 하 고 "시각화"를 선택 합니다.***

> [!TIP]
> 데이터 집합 및 모듈은 입력과 출력 포트 작은 원을 표시-hello 위쪽에, 입력된 포트를 나타내는 출력 hello 맨 아래에는 포트.
실험을 통해 데이터 흐름 toocreate 다른 tooan 입력된 포트의 단일 모듈의 출력 포트로 연결 합니다.
언제 든 지 어떤 hello 데이터가 표시 되는 해당 시점 hello 데이터 흐름에서 데이터 집합 또는 모듈 toosee의 출력 포트 hello 클릭 수 있습니다.

이 샘플 데이터 집합에 자동차의 각 인스턴스에 행으로 나타나고 각 자동차와 연결 된 hello 변수 열으로 나타납니다. 특정 자동차에 대 한 hello 변수를 제공 하겠습니다 tootry toopredict hello 가격 맨 오른쪽 열 (열의 26 "price").

![Hello 데이터 시각화 창에서 hello 자동차 데이터 보기][visualize-auto-data]
<br/>
***Hello 데이터 시각화 창에서 hello 자동차 데이터 보기***

Hello를 클릭 하 여 시각화 창 닫기 hello "**x**" hello 오른쪽 위 모퉁이에 있습니다.

## <a name="step-2-prepare-hello-data"></a>2 단계: hello 데이터 준비

데이터 집합은 일반적으로 전처리를 거쳐야 분석할 수 있습니다. 예를 들어 보았을 것 hello 누락 된 다양 한 행의 hello 열에 있는 값입니다. 이러한 누락 값 정리 hello 모델 hello 데이터를 정확 하 게 분석할 수 있도록 toobe가 필요 합니다. 지금은 누락된 값이 있는 행을 모두 제거하겠습니다. 또한 hello **정규화 손실** hello 모델에서 해당 열 모두 제외 하도록 열에 누락 값의 상당 합니다.

> [!TIP]
> 누락 된 값 입력된 데이터에서 청소 hello는 hello 모듈의 대부분을 사용 하기 위한 필수 구성 요소입니다.

먼저 hello를 제거 하는 모듈 추가 **정규화 손실** 열 완전히 누락 된 데이터가 모든 행을 제거 하는 다른 모듈을 추가 합니다.

1. 형식 **열 선택** hello 모듈 색상표 toofind hello hello 맨 hello 검색 상자에 [데이터 집합의 열 선택] [ select-columns] 모듈을 끌어와서 toohello 실험 캔버스 . 이 모듈에서는 tooinclude 하거나에서 제외할 데이터 열을 모델 hello tooselect 수 있습니다.

2. Hello의 hello 출력 포트를 연결 **자동차 가격 데이터 (Raw)** dataset toohello 입력 포트의 hello [데이터 집합의 열 선택] [ select-columns] 모듈입니다.

    ![Hello "Dataset에서 열 선택" 모듈 toohello 실험 캔버스에 추가 하 고 연결][type-select-columns]
    <br/>
    ***Hello "Dataset에서 열 선택" 모듈 toohello 실험 캔버스에 추가 하 고 연결***

3. Hello 클릭 [데이터 집합의 열 선택] [ select-columns] 모듈과 클릭 **열 선택기 시작** hello에 **속성** 창.

    - Hello 왼쪽에서 클릭 **규칙**
    - **다음으로 시작**에서 **모든 열**을 클릭합니다. 이렇게 하면 [데이터 집합의 열 선택] [ select-columns] (tooexclude에 대 한 하는 열)을 제외한 모든 hello 열을 통해 toopass 합니다.
    - Hello 드롭다운 목록에서 선택 **제외** 및 **열 이름을**, 다음 hello 텍스트 상자 안쪽을 클릭 합니다. 열 목록이 표시됩니다. 선택 **정규화 손실**, 및 추가 된 toohello 텍스트 상자입니다.
    - Hello (정상)이 확인 표시 단추 tooclose hello 열 선택 (오른쪽 hello)를 클릭 합니다.

    ![Hello 열 선택기 시작 하 고 "정규화 손실" hello 열 제외][launch-column-selector]
    <br/>
    ***Hello 열 선택기 시작 하 고 "정규화 손실" hello 열 제외***

    지금은 hello 속성 창에 대 한 **데이터 집합의 열 선택** 통과 하 게 할 모든 열을 통해 제외 하 고 hello 데이터 집합에서 나타냅니다 **정규화 손실**합니다.

    ![해당 "정규화 손실" hello 열은 제외 hello 속성 창 표시][showing-excluded-column]
    <br/>
    ***해당 "정규화 손실" hello 열은 제외 hello 속성 창 표시***

    > [!TIP]
    클릭 hello 모듈 및 텍스트를 입력할 주석 tooa 모듈을 추가할 수 있습니다. 한 눈에 볼 수 있습니다이 실험에서 hello 모듈을 수행 합니다. 이 경우 hello를 두 번 클릭 [데이터 집합의 열 선택] [ select-columns] 모듈 및 형식 hello 주석 "제외 정규화 손실."
    >
    >


    ![모듈 tooadd 주석을 두 번 클릭][add-comment]
    <br/>
    ***모듈 tooadd 주석을 두 번 클릭***

3. 끌어서 hello [누락 데이터 정리] [ clean-missing-data] 모듈 toohello 캔버스를 실험 하 고 toohello 연결 [데이터 집합의 열 선택] [ select-columns] 모듈입니다. Hello에 **속성** 창 선택 **전체 행 제거** 아래 **Cleaning 모드**합니다. 이렇게 하면 [누락 데이터 정리] [ clean-missing-data] tooclean hello 데이터 값이 누락 된 행을 제거 합니다. Hello 모듈을 두 번 클릭 하 고 "누락 된 값 행을 제거 합니다." hello 주석 입력

    ![Hello 청소 모드 설정 너무 "전체 행 제거" hello "누락 데이터 정리" 모듈에 대 한][set-remove-entire-row]
    <br/>
    ***Hello 청소 모드 설정 너무 "전체 행 제거" hello "누락 데이터 정리" 모듈에 대 한***

4. 클릭 하 여 hello 실험을 실행 **실행** hello hello 페이지 맨 아래에 있습니다.

    Hello 실험 실행이 완료 되었을 때 모든 hello 모듈 성공적으로 완료 되는 녹색 확인 표시가 tooindicate가 있습니다. 또한 hello 확인 **완료 된 실행** hello 오른쪽 위 모서리에서 상태입니다.

![를 실행 한 후 hello 실험은 다음과 같이 표시][early-experiment-run]
<br/>
***를 실행 한 후 hello 실험은 다음과 같이 표시***

> [!TIP]
> Hello 실험을 지금 실행 되었습니까 이유 म? 실행 중인 hello 실험 하 여 데이터에 대 한 열 정의 hello hello 통해 hello 데이터 집합에서 전달 [데이터 집합의 열 선택] [ select-columns] 모듈 및 hello를 통해 [누락 데이터를 정리] [ clean-missing-data] 모듈입니다. 즉, 너무 연결할 모듈[누락 데이터 정리] [ clean-missing-data] 이 정보를 갖게 됩니다.

Toothis 포인트 hello 실험에 했던 모든 정리 hello 데이터입니다. Tooview hello 정리할 데이터 집합 hello 남아 있는 hello의 출력 포트를 클릭 합니다 [누락 데이터 정리] [ clean-missing-data] 모듈과 선택 **시각화**합니다. 해당 hello 확인 **정규화 손실** 열 더 이상 포함 되어 있으며, 누락 값이 없습니다.

We're 준비 toospecify 기능에서는 이제 hello 데이터를 정리 했으므로 toouse hello 예측 모델에 맞추려고 합니다.

## <a name="step-3-define-features"></a>3단계: 기능 정의

기계 학습에서 *기능*은 관심 있는 부분에 대한 측정 가능한 개별 속성입니다. 여기서는 데이터 집합의 각 행이 하나의 자동차를 나타내고 각 열은 해당 자동차의 기능입니다.

Toosolve를 원하는 찾기 좋은 예측 모델을 만들기 위한 기능 집합 실험과 hello 문제에 대 한 지식이 필요 합니다. 일부 기능은 예측 hello 대상 다른 항목 보다 더 효과적일 수 있습니다. 또한 일부 기능은 다른 기능과 강력한 상관 관계가 있고 제거할 수 있습니다. 예를 들어 도시 mpg 및 고속도로 mpg 밀접 한 관련이 하므로 하나를 유지 하 고 크게 hello 예측 영향을 주지 않고 다른 hello를 제거할 수 있습니다.

이 데이터 집합의 hello 기능의 하위 집합을 사용 하는 모델을 제작 해 보겠습니다. 나중에 다시 시도 하 고 다른 기능 선택, hello 실험을 다시 실행 고 확인할 수 있습니다 더 나은 결과 얻을 경우. 하지만 toostart, 같은 기능 hello 해 보겠습니다.

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. 다른 [데이터 집합의 열 선택] [ select-columns] 모듈 toohello 실험 캔버스입니다. Hello의 출력 포트를 왼쪽 hello 연결 [누락 데이터 정리] [ clean-missing-data] hello의 모듈 toohello 입력 [데이터 집합의 열 선택] [ select-columns] 모듈입니다.

    ![Hello "Dataset에서 열 선택" 모듈 toohello "누락 데이터 정리" 모듈에 연결][connect-clean-to-select]
    <br/>
    ***Hello "Dataset에서 열 선택" 모듈 toohello "누락 데이터 정리" 모듈에 연결***

2. Hello 모듈을 두 번 클릭 하 고 "선택 기능, 예측에 대 한 합니다."를 입력 합니다.

2. 클릭 **열 선택기 시작** hello에 **속성** 창.

3. **규칙으로**를 클릭합니다.

4. **다음으로 시작**에서 **열 없음**을 클릭합니다. Hello 필터 행에서 선택 **Include** 및 **열 이름을** hello 텍스트 상자에서 열 이름의 목록 선택 합니다. 이 hello를 지정 하는 점을 제외 하 고 모든 열 (기능) 통과 모듈 toonot hello 전달 합니다.

5. Hello 확인 표시 (정상) 단추를 클릭 합니다.

    ![Hello 열 (기능) tooinclude hello 예측에서 선택][select-columns-to-include]
    <br/>
    ***Hello 열 (기능) tooinclude hello 예측에서 선택***

이 학습 알고리즘에서는 hello 다음 단계에서 toopass toohello 원하는 hello 기능이 포함 된 필터링된 된 데이터 집합을 생성 합니다. 나중에 돌아와서 다른 선택 기능을 사용하여 다시 시도할 수 있습니다.

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a>4단계: 학습 알고리즘 선택 및 적용

이제 hello 데이터 준비 되 면 예측 모델 생성 구성 되어 있다고 학습 및 테스트 합니다. 예제의 데이터 tootrain hello 모델에서는 한 hello 모델 toosee 테스트해 보겠습니다 다음 수 toopredict 가격은 근접도입니다.
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

*분류*와 *회귀*는 감독 기계 학습 알고리즘의 두 형식입니다. 분류는 색(빨강, 파랑 또는 녹색)과 같이 정의된 범주 집합에서 답변을 예측합니다. 회귀는 사용 되는 toopredict 숫자입니다.

에 사용 하기 위해 숫자인 경우 toopredict 가격 회귀 알고리즘을 사용 합니다. 이 예제에서는 간단한 *선형 회귀* 모델을 사용합니다.

> [!TIP]
> 다양 한 유형의 기계 학습 알고리즘에 대 한 자세한 toolearn 하 고 때 toouse 초보자를 위한 계열에 대 한 데이터 과학 hello에 hello 첫 번째 비디오를 볼 수 있습니다 이러한 [hello 5 데이터 과학 답변의 질문](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)합니다. Hello 인포 그래픽도 확인할 수 있습니다 [알고리즘 예제를 사용한 기본 사항 학습 컴퓨터](machine-learning-basics-infographic-with-algorithm-examples.md), 체크 아웃 hello 또는 [컴퓨터 학습 알고리즘 치트 시트](machine-learning-algorithm-cheat-sheet.md)합니다.

Hello 가격을 포함 하는 데이터 집합을 지정 하 여에 hello 모델을 학습 합니다. hello 모델 hello 데이터를 찾습니다는 자동차의 기능과 해당 가격 간의 상관 관계를 검색합니다. 그런 다음 hello 모델 테스트해 보겠습니다-म 된 자동차에 대 한 기능 집합을 지정 하 고 hello 모델 toopredicting hello 알려진된 가격을 제공 하는 얼마나 비슷한지를 참조 합니다.

Hello 모델을 학습 하 고 hello 데이터를 별도 학습 및 테스트 데이터 집합으로 분할 하 여 테스트에 대 한 데이터를 사용 합니다.

1. 선택 하 고 hello 끌어 [분할 데이터] [ split] 모듈 toohello 캔버스를 실험 하 고 연결 toohello 마지막 [데이터 집합의 열 선택] [ select-columns] 모듈입니다.

2. Hello 클릭 [분할 데이터] [ split] 모듈 tooselect 것입니다. Hello **hello의 행 비율 먼저 출력 데이터 집합** (hello에 **속성** hello 캔버스의 오른쪽 창 toohello) too0.75 설정 합니다. 이러한 방식으로 hello 데이터 tootrain hello 모델의 75%를 사용 하 여 알아보고 하겠습니다 보류 하 게 테스트를 위해 25% (이상 버전에서는 시험해 다른 백분율을 사용 하 여).

    ![Hello "데이터를 분할" 모듈 too0.75의 소수 부분을 분할 집합 hello][set-split-data-percentage]
    <br/>
    ***Hello "데이터를 분할" 모듈 too0.75의 소수 부분을 분할 집합 hello***

    > [!TIP]
    > Hello를 변경 하 여 **임의 초기값** 매개 변수를 학습 및 테스트에 서로 다른 무작위 샘플을 생성할 수 있습니다. 이 매개 변수는 hello hello 의사 (pseudo) 난수 생성기의 시드를 제어 합니다.

2. Hello 실험을 실행 합니다. Hello 실험을 실행 하는 경우 hello [데이터 집합의 열 선택] [ select-columns] 및 [분할 데이터] [ split] 모듈 열 정의 toohello 전달 다음 추가 되므로 모듈.  

3. 학습 알고리즘, tooselect hello hello 확장 **기계 학습** hello 모듈 색상표 toohello 왼쪽의 범주 hello의 캔버스를 확장 한 다음 **모델 초기화**합니다. 이 사용 되는 tooinitialize 기계 학습 알고리즘을 일 수 있는 모듈의 여러 범주가 표시 됩니다. 이 실험에 hello 선택 [선형 회귀] [ linear-regression] hello 아래의 모듈 **회귀** 범주 toohello 실험 캔버스를 끕니다.
(또한 모듈 찾을 수 있습니다 hello hello 색상표 검색 상자에 "선형 회귀"를 입력 합니다.)

4. 찾기 및 hello 끌어 [모델 학습] [ train-model] 모듈 toohello 실험 캔버스입니다. Hello hello 출력에 연결 [선형 회귀] [ linear-regression] 모듈 toohello 왼쪽 입력의 hello [모델 학습] [ train-model] 모듈 hello 연결 hello 데이터 출력 (왼쪽 포트) 학습 [분할 데이터] [ split] 모듈 toohello 오른쪽 입력의 hello [모델 학습] [ train-model] 모듈입니다.

    ![Hello "모델 학습" 모듈 tooboth hello "선형 회귀" 및 "데이터를 분할" 모듈에 연결][connect-train-model]
    <br/>
    ***Hello "모델 학습" 모듈 tooboth hello "선형 회귀" 및 "데이터를 분할" 모듈에 연결***

5. Hello 클릭 [모델 학습] [ train-model] 모듈을 클릭 하 여 **열 선택기 시작** hello에 **속성** 창과 선택 hello **가격** 열입니다. 이 모델을 하락 toopredict hello 값입니다.

    Hello 선택 **가격** hello에서 이동 하 여 hello 열 선택기의 열 **사용 가능한 열** toohello 목록 **선택한 열** 목록입니다.

    ![Hello "모델 학습" 모듈에 대 한 hello price 열을 선택 합니다.][select-price-column]
    <br/>
    ***Hello "모델 학습" 모듈에 대 한 hello price 열을 선택 합니다.***

6. Hello 실험을 실행 합니다.

사용 되는 tooscore 새로운 자동차 데이터 toomake 가격 예측 될 수 있는 학습 된 회귀 모델을 했습니다.

![를 실행 한 후 hello 실험은 이제 다음과 같은][second-experiment-run]
<br/>
***를 실행 한 후 hello 실험은 이제 다음과 같은***

## <a name="step-5-predict-new-automobile-prices"></a>5단계: 새 자동차 가격 예측

사용할 수 데이터의 75%를 사용 하 여 hello 모델을 학습 한 म 했으므로 tooscore hello hello 데이터 toosee 얼마나 잘의 25% 다른 우리의 모델 함수입니다.

1. 찾기 및 hello 끌어 [모델 점수 매기기] [ score-model] 모듈 toohello 실험 캔버스입니다. Hello hello 출력에 연결 [모델 학습] [ train-model] 왼쪽 입력된 포트의 모듈 toohello [모델 점수 매기기][score-model]합니다. Hello 테스트 데이터의 출력에 연결 (오른쪽 포트) hello [분할 데이터] [ split] 모듈 toohello 오른쪽 입력 포트의 [모델 점수 매기기][score-model]합니다.

    ![Hello "모델 점수 매기기" 모듈 tooboth hello "모델 학습" 및 "데이터를 분할" 모듈에 연결][connect-score-model]
    <br/>
    ***Hello "모델 점수 매기기" 모듈 tooboth hello "모델 학습" 및 "데이터를 분할" 모듈에 연결***

2. Hello 실험을 실행 하 고 hello hello 출력을 볼 [모델 점수 매기기] [ score-model] 모듈 (의 출력 포트 hello 클릭 [모델 점수 매기기] [ score-model] 선택 **시각화**). hello 출력과 hello 가격에 대 한 예측된 값 및 hello hello 테스트 데이터의 알려진된 값입니다.  

    ![Hello "모델 점수 매기기" 모듈의 출력][score-model-output]
    <br/>
    ***Hello "모델 점수 매기기" 모듈의 출력***

3. 마지막으로 hello 결과의 hello 품질을 테스트 합니다. 선택 하 고 hello 끌어 [모델 평가] [ evaluate-model] 모듈 toohello 캔버스를 실험 하 고 hello hello 출력에 연결 [모델 점수 매기기] [ score-model] 왼쪽 입력의 모듈 toohello [모델 평가][evaluate-model]합니다.

    > [!TIP]
    > Hello에는 두 개의 입력된 포트가 [모델 평가] [ evaluate-model] 모듈 toocompare 사용 되는 두 가지 모델 나란히 수 있도록 합니다. 다른 알고리즘 toohello 실험을 추가 하 고 사용 하 여 수 나중 [모델 평가] [ evaluate-model] toosee 한 더 나은 결과 제공 합니다.

4. Hello 실험을 실행 합니다.

hello tooview hello 출력 [모델 평가] [ evaluate-model] 모듈 hello 출력 포트를 클릭 한 다음 선택 **시각화**합니다.

![Hello 실험에 대 한 평가 결과][evaluation-results]
<br/>
***Hello 실험에 대 한 평가 결과***

이 모델에 대 한 통계를 다음 hello 표시 됩니다.

- **절대 평균 오차** (MAE): 평균 절대 오류 hello (한 *오류* hello 차이 hello 예측 값과 실제 값 hello).
- **루트 제곱 평균 오차** (RMSE): hello 테스트 데이터 집합에서 예측의 제곱 오류 hello 평균의 제곱근 hello 합니다.
- **상대 절대 오차**: hello 절대 오류 상대 toohello 절대 실제 값과 hello 평균의 차이의 모든 실제 값의 평균입니다.
- **상대 제곱 오차**: 상대 제곱된 오류 toohello의 hello 평균 hello 실제 값과 실제 값 집합 모든 hello 평균의 차이 제곱 합니다.
- **결정 계수**: 라고도 hello **R 제곱 값**를 얼마나 잘 맞는 hello 데이터는 모델을 나타내는 통계 메트릭을입니다.

각 hello 오류에 대 한 통계를 더 작은 좋습니다. 값이 작을수록 hello 예측 hello 실제 값과 보다 긴밀 하 게 일치 하는지 나타냅니다. 에 대 한 **결정 계수**, hello 곧 제공 될 해당 값이 더 나은 hello 예측 hello tooone (1.0).

## <a name="final-experiment"></a>최종 실험

hello 최종 실험 코드는 다음과 같아야 합니다.

![hello 최종 실험][complete-linear-regression-experiment]
<br/>
***hello 최종 실험***

## <a name="next-steps"></a>다음 단계

Hello 첫 번째 컴퓨터 학습 자습서를 완료 하 고 설정 하 여 실험 한 tooimprove hello 모델을 계속 한 다음 예측 웹 서비스로 배포 합니다.

- **Tootry tooimprove hello 모델 반복** -예를 들어 hello 기능 프로그램 예측에 사용 하 여 변경할 수 있습니다. Hello의 hello 속성을 수정할 수 있습니다 또는 [선형 회귀] [ linear-regression] 알고리즘 하거나 완전히 다른 알고리즘을 시도 하십시오. 도 여러 기계 학습 알고리즘 tooyour 실험을 한번에 추가 하 고 hello를 사용 하 여 그 중 두 개를 비교할 수 [모델 평가] [ evaluate-model] 모듈입니다.
어떻게 toocompare 단일 실험에서 여러 모델 참조의 예 [회귀 변수 비교](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) hello에 [Cortana 인텔리전스 갤러리](https://gallery.cortanaintelligence.com)합니다.

    > [!TIP]
    > toocopy hello 사용 하 여 실험 반복 **SAVE AS** hello hello 페이지 맨 아래에 단추입니다. 클릭 하 여 모든 hello 반복 하 여 실험을 볼 수 있습니다 **실행 기록 보기** hello hello 페이지 맨 아래에 있습니다. 자세한 내용은 [Azure Machine Learning 스튜디오에서 실험 반복 관리][runhistory]를 참조하세요.

[runhistory]: machine-learning-manage-experiment-iterations.md

- **Hello 모델 예측 웹 서비스로 배포** -만족 했으면 모델을 사용 하는 경우 웹 서비스 toobe toopredict 차량 가격을 사용 되는 새 데이터를 사용 하 여 배포할 수 있습니다. 자세한 내용은 [Azure Machine Learning 웹 서비스 배포][publish]를 참조하세요.

[publish]: machine-learning-publish-a-machine-learning-web-service.md

더 많은 toolearn 시겠습니까? Hello 프로세스의 생성, 학습, 상태 평가 및 배포 모델의 광범위 하 고 자세한 연습을 참조 하십시오. [Azure 기계 학습을 사용 하 여 예측 솔루션 개발][walkthrough]합니다.

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
