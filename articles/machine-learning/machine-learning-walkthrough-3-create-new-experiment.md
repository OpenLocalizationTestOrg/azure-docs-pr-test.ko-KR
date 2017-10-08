---
title: "3단계: 새 Machine Learning 실험 만들기 | Microsoft Docs"
description: "예측 솔루션 연습을 개발 하는 hello의 3 단계: Azure 기계 학습 스튜디오에서 새 학습 실험을 만듭니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a>연습 3단계: 새 Azure 기계 학습 실험 만들기
이 hello 연습의 hello 세 번째 단계 [Azure 기계 학습에서 예측 분석 솔루션을 개발 합니다.](machine-learning-walkthrough-develop-predictive-solution.md)

1. [기계 학습 작업 영역 만들기](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [기존 데이터 업로드](machine-learning-walkthrough-2-upload-data.md)
3. **새 실험 만들기**
4. [학습 하 고 hello 모델 평가](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Hello 웹 서비스를 배포 합니다.](machine-learning-walkthrough-5-publish-web-service.md)
6. [Hello 웹 서비스에 액세스](machine-learning-walkthrough-6-access-web-service.md)

- - -
이 연습에서는 다음 단계를 hello에는 toocreate 업로드할 hello 데이터 집합을 사용 하는 기계 학습 스튜디오에서 실험입니다.  

1. Studio에서, **+ 새로 만들기** hello hello 창 맨 아래에 있습니다.
2. **실험**을 선택하고 "빈 실험"을 선택합니다. 

    ![새로운 실험 만들기][0]

2. 선택 hello 기본 hello hello 캔버스 맨 위에 있는 이름 실험 및 toosomething 의미 있는 이름을 바꿉니다.

    ![실험 이름 바꾸기][5]
   
   > [!TIP]
   > 중인 좋습니다 toofill **요약** 및 **설명** hello에 hello 실험에 **속성** 창. 이러한 속성 목표와 방법을 이해 하 게 하 고 나중에 있도록 기회 toodocument hello 실험 hello를 제공 합니다.
   > 
   > ![실험 속성][6]
   > 
3. Hello 모듈 색상표 toohello 왼쪽 hello 실험 캔버스의 확장 **저장 된 데이터 집합**합니다.
4. 찾기 hello 데이터 집합 아래에 만든 **내 데이터 집합** hello 캔버스로 끕니다. Hello에 hello 이름을 입력 하 여 hello 데이터 집합을 찾을 수도 있습니다 **검색** hello 색상표 위의 상자입니다.  

    ![Hello, toohello 실험 데이터 집합 추가][7]

## <a name="prepare-hello-data"></a>Hello 데이터 준비
볼 수 있습니다 hello 데이터의 처음 100 개의 행과 hello 전체 데이터 집합에 대 한 몇 가지 통계 정보 hello: hello 데이터 집합 (hello 맨 아래에 작은 원 hello)의 hello 출력 포트를 클릭 하 고 선택 **시각화**합니다.  

Studio가 일반 머리글 제공 hello 데이터 파일 열 머리글과 함께 제공 되지 않은, 때문에 (Col1, Col2, *등*). 좋은 머리글 필수 toocreating 모델 아니지만 할 있습니다 hello 데이터와 함께 보다 쉽게 toowork hello 실험에 있습니다. 또한 결국 웹 서비스에서이 모델을 게시 했습니다 hello 머리글 식별할 hello 서비스의 hello 열 toohello 사용자.  

Hello를 사용 하 여 열 머리글을 추가할 수 있습니다 [메타 데이터 편집] [ edit-metadata] 모듈입니다.
Hello를 사용 하 여 [메타 데이터 편집] [ edit-metadata] 모듈 toochange 메타 데이터에 연결 된 데이터 집합입니다. 이 경우에서는 tooprovide 자세한 이름에 사용할 열 머리글. 

toouse [메타 데이터 편집][edit-metadata], 어떤 열 toomodify에 (이 경우 이러한 모든.)를 먼저 지정 해당 열 (이 경우 열 머리글을 변경 합니다.)에 대해 수행 하는 hello 동작 toobe를 지정 하는 다음으로,

1. Hello 모듈 팔레트에서 "메타 데이터" hello에 입력 **검색** 상자입니다. hello [메타 데이터 편집] [ edit-metadata] hello 모듈 목록에 나타납니다.

2. 클릭 하 고 hello 끌어 [메타 데이터 편집] [ edit-metadata] hello에 모듈 캔버스 및 이전에 추가한 hello 데이터 집합 아래에 놓습니다.

3. 데이터 집합 toohello hello 연결 [메타 데이터 편집][edit-metadata]: hello 데이터 집합 (hello 데이터 집합의 hello 맨 아래에 작은 원 hello)의 출력 포트 hello 클릭, toohello 입력된 포트의 끌어 [메타 데이터 편집 ] [ edit-metadata] (hello 작은 원이 hello 모듈의 hello 위쪽) hello 마우스 단추를 놓습니다. hello 데이터 집합 및 모듈 이동 하거나 hello 캔버스에 있는 경우에 연결 되어 있습니다.
   
   hello 실험 같아야 이제 다음과 같이 합니다.  
   
   ![메타데이터 편집 추가][1]
   
   hello 빨간색 느낌표 म이 모듈에 대 한 hello 속성을 아직 설정 하지 않은 것을 나타냅니다. 다음에 수행합니다.
   
   > [!TIP]
   > 클릭 hello 모듈 및 텍스트를 입력할 주석 tooa 모듈을 추가할 수 있습니다. 한 눈에 볼 수 있습니다이 실험에서 hello 모듈을 수행 합니다. 이 경우 hello를 두 번 클릭 [메타 데이터 편집] [ edit-metadata] 모듈 및 형식 hello 주석 "추가 열 머리글"입니다. Hello 캔버스 tooclose hello 텍스트 상자에 다른 곳을 클릭 합니다. toodisplay 주석 hello hello 모듈에서 hello 아래쪽 화살표를 클릭 합니다.
   > 
   > ![주석이 추가된 메타데이터 모듈 편집][8]
   > 
4. 선택 [메타 데이터 편집][edit-metadata], 및 hello **속성** hello 캔버스의 오른쪽 창 toohello 클릭 **열 선택기 시작**합니다.

5. Hello에 **열 선택** 대화 상자에서 모든 hello의 행 선택 **사용 가능한 열** 클릭 > toomove에 너무**선택한 열**합니다.
   hello 대화는 다음과 같이 표시 됩니다.

   ![모든 열이 선택된 열 선택기][2]

6. Hello 클릭 **확인** 확인 표시 합니다.

7. Hello에 다시 **속성** 창 hello에 대 한 **새 열 이름** 매개 변수입니다. 이 필드에 열 순서 및 쉼표로 구분 된 hello 데이터 집합의 hello 21 열에 대 한 이름 목록을 입력 합니다. Hello UCI 웹 사이트에서 데이터 집합 설명서 hello에서에서 hello 열 이름을 가져올 수 있습니다 또는 편의 위해 복사 및 붙여넣기 목록 다음 hello 수 있습니다.  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   hello 속성 창의 모양은 다음과 같습니다.
   
   ![메타데이터 편집에 대한 속성][3]

> [!TIP]
> Tooverify hello 열 머리글 hello 실험을 실행 합니다 (클릭 **실행** hello 실험 캔버스 아래). 실행 완료 되 면 (에 녹색 확인 표시가 나타납니다 [메타 데이터 편집][edit-metadata]), hello의 hello 출력 포트를 클릭 [메타 데이터 편집] [ edit-metadata] 모듈 및 선택 **시각화**합니다. Hello에서 모든 모듈의 hello 출력을 볼 수 있습니다 hello 실험을 통해 hello 데이터의 동일한 방식으로 tooview hello 진행 합니다.
> 
> 

## <a name="create-training-and-test-datasets"></a>학습 및 테스트 데이터 집합 만들기
일부 데이터 tootrain hello 모델 및 몇 가지 tootest 필요 것입니다.
Hello 데이터 집합 두 개의 별도 데이터 집합으로 분할에서는 hello 실험 hello 다음 단계에서는 하므로: 하나는 예제의 모델을 테스트 하기 위한 학습 합니다.

toodo이를 사용 하 여 hello [분할 데이터] [ split] 모듈입니다.  

1. Hello [분할 데이터] [ split] hello 캔버스로 끌어 모듈과 toohello 연결 [메타 데이터 편집] [ edit-metadata] 모듈입니다.

2. 기본적으로 hello 분할 비율이 0.5 및 hello **임의 분할** 매개 변수를 설정 합니다. 따라서 hello 데이터의 임의 절반의 hello 하나의 포트를 통해 출력을 [분할 데이터] [ split] 모듈과 절반 통해 hello 다른 합니다. 있습니다 수 이러한 매개 변수 조정으로 hello **임의 초기값** 매개 변수를 학습 및 테스트 데이터 간에 분할 toochange hello 합니다. 이 예제에서는 그대로 유지합니다.
   
   > [!TIP]
   > 속성을 hello **hello의 행 비율 먼저 출력 데이터 집합** hello 통해 출력은 hello 데이터의 양을 결정 *왼쪽* 출력 포트입니다. 예를 들어 hello 비율 too0.7로 설정 하면 hello 데이터의 70%는 왼쪽의 포트 및 30 %hello 오른쪽 포트를 통해 hello 통해 출력입니다.  
   > 
   > 

3. Hello를 두 번 클릭 [분할 데이터] [ split] 모듈 hello 설명을 입력 하 고, "학습/테스트 데이터가 50%로 분할"입니다. 

그러나 Hello의 hello 출력에 사용할 수 있습니다 [분할 데이터] [ split] 같이 테스트 데이터를 출력 하는 모듈 학습 데이터로 왼쪽된 출력 hello 및 오른쪽 hello 우리 있지만 toouse 선택 해 보겠습니다.  

Hello에 설명 된 대로 [이전 단계](machine-learning-walkthrough-2-upload-data.md), hello 낮은 신용 위험 misclassifying 비용은 high로 낮은 신용 위험 misclassifying hello 비용 보다 5 배로 더 높은 합니다. 이 대 한 tooaccount,이 비용 함수를 반영 하는 새 데이터 집합을 생성 합니다. Hello 새 데이터 집합을 각 위험 수준이 높은 예에서는 각 낮은 위험 예제 복제 되지 않은 동안 5 번 복제 됩니다.   

R 코드를 사용하여 이 복제를 수행할 수 있습니다.  

1. 찾기 및 hello 끌어 [R 스크립트 실행] [ execute-r-script] hello 실험 캔버스로 모듈입니다. 

2. 남아 있는 hello의 출력 포트 hello 연결 [분할 데이터] [ split] 모듈 toohello hello의 포트 ("Dataset1")의 첫 번째 입력 [R 스크립트 실행] [ execute-r-script] 모듈입니다.

3. Hello를 두 번 클릭 [R 스크립트 실행] [ execute-r-script] 모듈 hello 설명을 입력 하 고 "조정 비용 집합"입니다.

4. Hello에 **속성** hello 삭제 hello 기본 텍스트 창 **R 스크립트** 매개 변수가이 스크립트를 입력 합니다.
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Hello R 스크립트 실행 모듈에서 R 스크립트][9]

Toodo hello의 각 출력에 대 한 동일한이 복제 연산 해야 [분할 데이터] [ split] 모듈 학습 및 테스트 데이터에는 해당 hello 동일 hello 있어야 하므로 비용 조정 합니다. 이 hello를 복제 하 여 가장 쉬운 방법은 toodo hello [R 스크립트 실행] [ execute-r-script] 모듈에서는 방금 만든 및 출력 toohello 연결의 hello 포트 [분할 데이터] [ split] 모듈입니다.

1. 마우스 오른쪽 단추로 클릭 hello [R 스크립트 실행] [ execute-r-script] 모듈과 선택 **복사**합니다.

2. Hello 실험 캔버스를 마우스 오른쪽 단추로 클릭 하 고 선택 **붙여넣기**합니다.

3. 다음의 hello hello 오른쪽 출력 포트를 연결와 hello 새 모듈 위치에 끌어 [분할 데이터] [ split] toohello 모듈의 첫 번째 입력이 포트 새로운 [R 스크립트 실행] [ execute-r-script] 모듈입니다. 

4. Hello 캔버스의 hello 아래쪽 클릭 **실행**합니다. 

> [!TIP]
> hello R 스크립트 실행 모듈의 hello 복사본 hello hello 원래 모듈과 동일한 스크립트를 포함 합니다. 복사한 hello 캔버스에 모듈을 붙여 넣는 hello 복사 모든 hello 속성의 원래 hello에 유지 됩니다.  
> 
> 

이제 실험은 다음과 같이 표시됩니다.

![분할 모듈 및 R 스크립트 추가][4]

실험에서의 R 스크립트 사용에 대한 자세한 내용은 [R을 사용하여 실험 확장](machine-learning-extend-your-experiment-with-r.md)을 참조하세요.

**다음: [학습 하 고 hello 모델 평가](machine-learning-walkthrough-4-train-and-evaluate-models.md)**

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
