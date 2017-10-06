---
title: "4 단계: 학습 하 고 hello 예측 분석 모델을 평가 | Microsoft Docs"
description: "예측 솔루션 연습을 개발 하는 hello의 4 단계: 학습, 점수를 매길 및 Azure 기계 학습 스튜디오에서 여러 모델을 평가 합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a>4 단계를 연습: 학습 하 고 hello 예측 분석 모델 평가
이 항목에서는 hello 연습의 4 단계 hello [Azure 기계 학습에서 예측 분석 솔루션을 개발 합니다.](machine-learning-walkthrough-develop-predictive-solution.md)

1. [기계 학습 작업 영역 만들기](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [기존 데이터 업로드](machine-learning-walkthrough-2-upload-data.md)
3. [새 실험 만들기](machine-learning-walkthrough-3-create-new-experiment.md)
4. **학습 하 고 hello 모델 평가**
5. [Hello 웹 서비스를 배포 합니다.](machine-learning-walkthrough-5-publish-web-service.md)
6. [Hello 웹 서비스에 액세스](machine-learning-walkthrough-6-access-web-service.md)

- - -
Azure 기계 학습 스튜디오를 사용 하 여 기계 학습 모델을 만들기 위한의 hello 이점 중 하나는 hello 기능 tootry 둘 이상의 유형의 모델 단일 실험에서 한 번에 이며 hello 결과 비교 합니다. 이 유형의 실험을 사용 하면 문제에 대 한 hello 가장 적합 한 솔루션을 찾을 수 있습니다.

에서는이 연습에서 개발 하는 hello 실험에서 두 가지 유형의 모델 만든 하 해당 점수 매기기 결과 toodecide 알고리즘 비교 하겠습니다 toouse 우리의 마지막 실험에서 원하는 합니다.  

다양한 모델을 선택할 수 있습니다. 를 사용할 수 있는 toosee hello 모델 확장 hello **기계 학습** hello 모듈 색상표에 노드 펼친 다음 **모델 초기화** 및 그 아래의 hello 노드. Hello이이 실험에서는 hello 선택 하겠습니다 [2 클래스 지원 벡터 컴퓨터] [ two-class-support-vector-machine] (SVM) 및 hello [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree] 모듈입니다.    

> [!TIP]
> 기계 학습 알고리즘을 가장 잘 결정할 tooget 도움말 hello toosolve 만들려고 하는 특정 문제에 적합 한, 참조 [어떻게 toochoose Microsoft Azure 기계 학습 알고리즘](machine-learning-algorithm-choice.md)합니다.
> 
> 

## <a name="train-hello-models"></a>Hello 모델 학습

두 hello 추가 [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree] 모듈 및 [2 클래스 지원 벡터 컴퓨터] [ two-class-support-vector-machine] 이 모듈 시험 합니다.

### <a name="two-class-boosted-decision-tree"></a>2클래스 향상된 의사 결정 트리

첫째, hello 승격 된 의사 결정 트리 모델을 설정 해 보겠습니다.

1. Hello [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree] hello 모듈 색상표에 모듈 hello 캔버스로 끕니다.

2. Hello [모델 학습] [ train-model] hello 캔버스로 끌어 모듈과 다음 hello hello 출력에 연결 [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree]모듈 toohello 왼쪽 입력된 포트의 hello [모델 학습] [ train-model] 모듈입니다.
   
   hello [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree] 모듈 hello 일반 모델에서 초기화 및 [모델 학습] [ train-model] 학습 데이터를 사용 하 여 tootrain hello 모델입니다. 

3. Hello 왼쪽의 hello 왼쪽된 출력 연결 [R 스크립트 실행] [ execute-r-script] 모듈 toohello 오른쪽 입력 포트의 hello [모델 학습] [ train-model] (म 모듈 결정 [3 단계](machine-learning-walkthrough-3-create-new-experiment.md) hello 학습용 hello 분할 데이터 모듈의 왼쪽에서 들어오는이 연습에서는 toouse hello 데이터).
   
   > [!TIP]
   > Hello의 hello 출력 중 하나를 두 hello 입력이 필요 하지 않으므로 [R 스크립트 실행] [ execute-r-script] 하므로 삭제할 수 있습니다. 이러한 연결 되지 않은이 실험에는 모듈입니다. 
   > 
   > 

이제 hello 실험의이 부분에서는 다음과 같이 표시 됩니다.  

![모델 학습][1]

이제 tootell hello 필요 [모델 학습] [ train-model] 모듈 hello 모델 toopredict hello 신용 위험 값을 지정 했습니다.

1. 선택 hello [모델 학습] [ train-model] 모듈입니다. Hello에 **속성** 창에서 클릭 **열 선택기 시작**합니다.

2. Hello에 **단일 열 선택** 대화 상자에서 아래 hello 검색 필드에 "신용 위험"을 입력 **사용 가능한 열**, 아래 "신용 위험"을 선택 하 고 hello 오른쪽 화살표 단추를 클릭 ( **>** ) toomove "신용 위험" 너무**선택한 열**합니다. 

    ![Hello 모델 학습 모듈에 대 한 hello 신용 위험 열 선택][0]

3. Hello 클릭 **확인** 확인 표시 합니다.

### <a name="two-class-support-vector-machine"></a>2클래스 Support Vector Machine

다음으로 hello SVM 모델을 설정 합니다.  

먼저 SVM에 대한 간단한 설명입니다. 향상된 의사 결정 트리는 모든 기능 유형에서 제대로 작동합니다. 그러나 선형 분류자를 생성 하는 hello SVM 모듈, 이후 hello 모델 생성 하는 hello 최상의 테스트 오류 모든 숫자 기능이 hello 때 같은 눈금. 모든 숫자 tooconvert 기능 toohello 동일한 크기를 조정, "Tanh" 변환을 사용 하 여 우리 (hello로 [데이터 정규화] [ normalize-data] 모듈). 이 hello [0, 1] 범위에이 숫자를 변환합니다. 문자열 기능 toocategorical 기능 및 toobinary 0/1 기능으로 변환 하는 hello SVM 모듈, 하지 하므로 필요 toomanually 변환 문자열 기능입니다. 또한 tootransform hello 신용 위험 열 (열 21) 않도록-이 숫자 이면 하지만 hello 값을 학습 하는 것 때문에 tooleave 모델 toopredict hello 단독 것입니다.  

tooset hello SVM 모델을 따르는 hello지 않습니다.

1. Hello [2 클래스 지원 벡터 컴퓨터] [ two-class-support-vector-machine] hello 모듈 색상표에 모듈 hello 캔버스로 끕니다.

2. 마우스 오른쪽 단추로 클릭 hello [모델 학습] [ train-model] 모듈을 **복사**, hello 캔버스를 마우스 오른쪽 단추로 클릭 한 다음 및 선택 **붙여넣기**합니다. hello의 복사본을 hello [모델 학습] [ train-model] 모듈 hello에 원래 hello로 같은 열 항목을 선택 합니다.

3. Hello hello 출력에 연결 [2 클래스 지원 벡터 컴퓨터] [ two-class-support-vector-machine] 모듈 toohello 왼쪽 입력된 포트의 hello 둘째 [모델 학습] [ train-model] 모듈입니다.

4. Hello [데이터 정규화] [ normalize-data] 모듈 hello 캔버스로 끕니다.

5. Hello 왼쪽의 hello 왼쪽된 출력 연결 [R 스크립트 실행] [ execute-r-script] (모듈의 출력 포트 hello 다른 모듈 하나 보다 연결된 toomore 수 있다고 표시)이이 모듈의 모듈 toohello 입력 합니다.

6. 남아 있는 hello의 출력 포트 hello 연결 [데이터 정규화] [ normalize-data] 모듈 toohello 오른쪽 입력 포트의 hello 둘째 [모델 학습] [ train-model] 모듈입니다.

실험의 이 부분은 이제 다음과 같이 표시됩니다.  

![Hello 두 번째 모델 학습][2]  

이제 hello 구성할 [데이터 정규화] [ normalize-data] 모듈:

1. Tooselect hello 클릭 [데이터 정규화] [ normalize-data] 모듈입니다. Hello에 **속성** 창 선택 **Tanh** hello에 대 한 **변환 방법** 매개 변수입니다.

2. 클릭 **열 선택기 시작**, "열 선택 안 함"에 대 한 **Begin With**선택, **Include** hello 첫 번째 드롭다운에서 선택 **열 형식**에 두 번째 드롭다운에서 hello 및 선택 **숫자** hello 세 번째 드롭다운에서 합니다. 이 모든 hello 숫자 열 (및만 하는 숫자) 변환 지정 합니다.

3. 클릭 하 여이 행의 오른쪽 더하기 기호 (+) toohello hello-이 드롭다운의 행이 만들어집니다. 선택 **제외** hello 첫 번째 드롭다운에서 선택 **열 이름을** 에 두 번째 드롭다운에서 hello 및 hello 텍스트 필드에 "신용 위험"을 입력 합니다. 이 해당 hello 신용 위험 열을 무시 하도록 지정 (이 숫자 이므로이 열은 때문에 변환 됩니다 것을 제외 하지 않은 경우 toodo 필요).

4. Hello 클릭 **확인** 확인 표시 합니다.  

    ![Hello 데이터 정규화 모듈에 대 한 열 선택][5]

hello [데이터 정규화] [ normalize-data] 모듈 집합 tooperform hello 신용 위험 열을 제외한 모든 숫자 열에 Tanh 변환 되었습니다.  

## <a name="score-and-evaluate-hello-models"></a>점수와 hello 모델 평가

Hello 테스트 데이터 hello에서 분리를 사용 하 여 [분할 데이터] [ split] 모듈 tooscore 우리의 학습 된 모델입니다. 더 나은 결과 생성 된 hello 두 모델 toosee의 hello 결과 비교할 수 있습니다.  

### <a name="add-hello-score-model-modules"></a>Hello 모델 점수 매기기 모듈 추가

1. Hello [모델 점수 매기기] [ score-model] 모듈 hello 캔버스로 끕니다.

2. Hello 연결 [모델 학습] [ train-model] toohello 연결 된 모듈 [2 클래스 승격 된 의사 결정 트리] [ two-class-boosted-decision-tree] 모듈 toohello 왼쪽된 입력 포트의 hello [모델 점수 매기기] [ score-model] 모듈입니다.

3. Hello 오른쪽 연결 [R 스크립트 실행] [ execute-r-script] 모듈 (테스트 데이터) toohello 오른쪽 입력 포트의 hello [모델 점수 매기기] [ score-model] 모듈입니다.

    ![모델 점수 매기기 모듈이 연결됨][6]
   
   hello [모델 점수 매기기] [ score-model] 모듈 hello 모델을 통해 실행 데이터를 테스트 하는 hello에서 hello 신용 정보를 지금 사용할 수 있습니다 및 실제 hello로 hello 모델을 생성 하는 비교 hello 예측 신용 위험 hello 테스트 데이터의에서 열입니다.

4. 복사 및 붙여넣기 hello [모델 점수 매기기] [ score-model] 모듈 toocreate 두 번째 복사본입니다.

5. Hello SVM 모델의 hello 출력에 연결 (즉, hello 출력의 hello 포트 [모델 학습] [ train-model] toohello 연결 된 모듈 [2 클래스 지원 벡터 컴퓨터] [ two-class-support-vector-machine] 모듈) toohello 입력 포트의 hello 둘째 [모델 점수 매기기] [ score-model] 모듈입니다.

6. Hello SVM 모델에 대 한 toohello 학습 데이터와 같이 동일한 변환 toohello 테스트 데이터를 hello toodo를 해야 합니다. 따라서 복사한 hello [데이터 정규화] [ normalize-data] 모듈 toocreate 두 번째 사본 toohello 오른쪽 연결 [R 스크립트 실행] [ execute-r-script] 모듈입니다.

7. Hello hello 왼쪽된 출력에 두 번째 연결 [데이터 정규화] [ normalize-data] 모듈 toohello 오른쪽 입력 포트의 hello 둘째 [모델 점수 매기기] [ score-model] 모듈입니다.

    ![두 모델 점수 매기기 모듈이 연결됨][7]

### <a name="add-hello-evaluate-model-module"></a>Hello 모델 평가 모듈 추가

사용 하 여, tooevaluate 두 점수 매기기 결과 hello과 비교 하는 [모델 평가] [ evaluate-model] 모듈입니다.  

1. Hello [모델 평가] [ evaluate-model] 모듈 hello 캔버스로 끕니다.

2. Hello의 hello 출력 포트를 연결 [모델 점수 매기기] [ score-model] hello와 연관 된 모듈에는 의사 결정 트리 모델 toohello 왼쪽 입력 포트의 hello 승격 된 [모델 평가] [ evaluate-model] 모듈입니다.

3. 다른 hello 연결 [모델 점수 매기기] [ score-model] 모듈 toohello 오른쪽 입력 포트입니다.  

    ![모델 평가 모듈이 연결됨][8]

### <a name="run-hello-experiment-and-check-hello-results"></a>Hello 실험을 실행 하 고 hello 결과 확인 합니다.

toorun 실험 hello를 hello 클릭 **실행** hello 캔버스 아래 단추입니다. 몇 분이 걸릴 수 있습니다. 각 모듈에는 회전 표시기는이 서비스를 실행 하 고 hello 모듈 완료 되 면 녹색 확인 표시가 표시 하는 다음을 표시 합니다. 모든 hello 모듈 확인 표시가 있으면 hello 실험 이미 실행 중입니다.

hello 실험 같아야 이제 다음과 같이 합니다.  

![두 모델 모두 평가][3]

toocheck hello 결과 클릭 hello의 출력 포트 hello [모델 평가] [ evaluate-model] 모듈과 선택 **시각화**합니다.  

hello [모델 평가] [ evaluate-model] 모듈 곡선과 hello 두 점수가 매겨진된 모델의 toocompare hello 결과 허용 하는 메트릭을 만듭니다. 수신기 연산자 특성 (ROC) 곡선, 전체 자릿수/회수 곡선 또는 리프트 곡선으로 hello 결과 볼 수 있습니다. 혼동 행렬, (AUC) hello 곡선 아래의 영역 hello에 대 한 누적 값 및 기타 메트릭을 표시 하는 추가 데이터에 포함 되어 있습니다. 왼쪽 또는 오른쪽 이동 hello 슬라이더를 통해 hello 임계값을 변경 하 고 hello 메트릭 집합이 미치는 영향을 확인할 수 있습니다.  

toohello hello 그래프의 오른쪽 클릭 **점수가 매겨진 데이터 집합** 또는 **dataset toocompare 점수가 매겨진** toohighlight hello 관련된 곡선과 toodisplay hello 관련 메트릭 아래 합니다. Hello 곡선에 대 한 hello 범례에서 왼쪽 입력된 포트의 hello toohello 해당 "점수가 매겨진 데이터 집합" [모델 평가] [ evaluate-model] 모듈-경우에는 hello 승격 된 의사 결정 트리 모델입니다. "점수가 매겨진 데이터 집합 toocompare" toohello 오른쪽 입력된 포트-경우에 hello SVM 모델은 해당합니다. 이러한 레이블 중 하나를 클릭 하면 해당 모델에 대 한 hello 곡선은 강조 표시 하 고 hello 다음 그래픽에에서 표시 된 것과 같이 hello 해당 메트릭이 표시 됩니다.  

![모델에 대한 ROC 곡선][4]

이러한 값을 검사 하 여 모델에 대 한 원하는 결과 hello 가장 가까운 toogiving을 결정할 수 있습니다. 다시 돌아가서 hello 서로 다른 모델에 매개 변수 값을 변경 하 여 실험을 반복 합니다. 

hello 과학 및 이러한 결과 해석 하 고 hello 모델 성능을 튜닝의 기술에는이 연습의 외부 hello 범위입니다. 자세한 도움말을 보려면 다음 문서는 hello을 확인할 수 있습니다.
- [Tooevaluate는 Azure 기계 학습에서 성능을 모델링 하는 방법](machine-learning-evaluate-model-performance.md)
- [Azure 기계 학습에서 매개 변수 toooptimize 알고리즘을 선택 합니다.](machine-learning-algorithm-parameters-optimize.md)
- [Azure Machine Learning에서 모델 결과 해석](machine-learning-interpret-model-results.md)

> [!TIP]
> 해당 반복에 대 한 기록을 hello 실험을 실행할 때마다 hello 실행 기록에에서 보관 됩니다. 이러한 반복을 볼 수 있으며 그 중 tooany 클릭 하 여 반환 **실행 기록 보기** hello 캔버스 아래 합니다. 클릭할 수도 있습니다 **이전 실행** hello에 **속성** 창 tooreturn toohello 반복 바로 앞에 나오는 hello 열어 놓은 하나입니다.
> 
> 클릭 하 여 실험의 모든 반복의 복사본을 만들 수 있습니다 **SAVE AS** hello 캔버스 아래 합니다. 
> Hello 실험을 사용 하 여 **요약** 및 **설명** 속성 tookeep 레코드가 실험 반복에서 시도 하셨습니다.
> 
> 자세한 내용은 [Azure 기계 학습 스튜디오에서 실험 반복 관리](machine-learning-manage-experiment-iterations.md)를 참조하세요.  
> 
> 

- - -
**다음: [hello 웹 서비스를 배포 합니다.](machine-learning-walkthrough-5-publish-web-service.md)**

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
