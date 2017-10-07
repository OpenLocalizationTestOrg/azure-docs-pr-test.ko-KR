---
title: "2단계: Machine Learning 실험에 데이터 업로드 | Microsoft Docs"
description: "예측 솔루션 연습을 개발 하는 hello의 2 단계: Azure 기계 학습 스튜디오에 저장 된 공용 데이터를 업로드 합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a>연습 2단계: Azure 기계 학습 실험에 기존 데이터 업로드
이 hello 연습의 두 번째 단계 hello [Azure 기계 학습에서 예측 분석 솔루션을 개발 합니다.](machine-learning-walkthrough-develop-predictive-solution.md)

1. [기계 학습 작업 영역 만들기](machine-learning-walkthrough-1-create-ml-workspace.md)
2. **기존 데이터 업로드**
3. [새 실험 만들기](machine-learning-walkthrough-3-create-new-experiment.md)
4. [학습 하 고 hello 모델 평가](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Hello 웹 서비스를 배포 합니다.](machine-learning-walkthrough-5-publish-web-service.md)
6. [Hello 웹 서비스에 액세스](machine-learning-walkthrough-6-access-web-service.md)

- - -
toodevelop 신용 위험에 대 한 예측 모델, 데이터를 म 수 tootrain를 사용 하 여 다음 hello 모델을 테스트 해야 합니다. 이 연습에서는 "UCI Statlog (독일 신용 데이터) 데이터 집합" hello hello UC Irvine 기계 학습 리포지토리에서 사용 합니다. 이 데이터 집합은   
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a>

라는 hello 파일에서는 **german.data**합니다. 이 파일 tooyour 로컬 하드 드라이브를 다운로드 합니다.  

hello **german.data** 1000 지난 신청자 신용에 대 한 20 변수의 행 데이터 집합에 있는 합니다. 20 이러한 변수는 hello 데이터 집합의 기능 집합을 나타냅니다 (hello *기능 벡터*), 각 신용 신청자 위한 식별 특성을 제공 합니다. 각 행에는 추가 열 700 지원자는 높은 위험 수준으로 낮은 신용 위험 및 300으로 식별 된 hello 신청자의 계산 된 신용 위험을 나타냅니다.

hello UCI 웹 사이트에이 데이터에 대 한 hello 기능 벡터의 hello 특성에 대 한 설명을 제공합니다. 여기에는 재무 정보, 신용 기록, 고용 상태 및 개인 정보가 포함됩니다. 각 지원자에 대해 신용 위험이 낮은지 아니면 높은지 여부를 나타내는 이진 등급이 제공되었습니다. 

이 데이터 tootrain 예측 분석 모델을 사용 합니다. 작업이 끝났을 때, 예제의 모델 수 tooaccept 새 개인에 대 한 기능 벡터와 자신이 인지 낮거나 높은 신용 위험을 예측 합니다.  

흥미로운 변형이 있습니다. 개인의 신용 위험 misclassify म 경우 비용이 어떤 hello hello UCI 웹 사이트 언급 되어 데이터 집합의 설명 hello 합니다.
Hello 모델 낮은 신용 위험 실제로 장애가 있는 사용자에 대 한 신용 위험을 예측 하는 경우는 오 분류 hello 모델에 구성 됩니다.
Hello 역방향 오 분류 5 배 더 비용이 많이 드는 toohello 금융 기관 이지만: hello 모델 신용 위험 실제로 장애가 있는 사용자에 대 한 낮은 신용 위험을 예측 하는 경우.

따라서 원하는 tootrain 예제의 모델 hello이 두번째 유형의 오 분류 비용 보다 높습니다. 5 번 hello 다른 방법으로 misclassifying 되도록 합니다.
하나의 간단한 방법 toodo이 때 (5 번) 해당 나타내는 항목이 신용 위험을 가진 사용자를 복제 하 여이 우리의 실험에서 hello 모델을 학습 합니다. 그런 다음 있으면 hello 모델 잘못 분류 낮은 신용 위험으로 누군가가 실제로 위험 수준이 높은 경우, hello 모델에서 해당 동일한 오 분류 다섯 번 한 번 각 복제본에 대 한 합니다. 이렇게 하면 hello 학습 결과에서이 오류의 hello 비용을 증가 합니다.


## <a name="convert-hello-dataset-format"></a>Hello 데이터 집합 형식으로 변환
hello 원래 집합에 빈 구분 된 형식을 사용합니다. 기계 학습 스튜디오 작업 쉼표로 공간을 대체 하 여 hello 데이터 집합으로 변환 합니다 하므로 쉼표로 구분 된 값 (CSV) 파일을 더 합니다.  

이 데이터는 여러 방법으로 tooconvert 합니다. 한 가지 방법은 hello 다음 Windows PowerShell 명령을 사용 하 여:   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

또 다른 방법은 hello Unix sed 명령을 사용 하 여입니다.  

    sed 's/ /,/g' german.data > german.csv  

두 경우 모두 쉼표로 구분 된 데이터 버전의 hello 라는 파일에 만들어져 **german.csv** 우리의 실험에서 사용할 수 있는 합니다.

## <a name="upload-hello-dataset-toomachine-learning-studio"></a>Hello dataset tooMachine 학습 스튜디오에 업로드
Tooupload 필요 hello 데이터에 대 한 형식 변환 된 tooCSV를 수행한 후 기계 학습 스튜디오에 넣습니다. 

1. 열기 hello 기계 학습 스튜디오 홈 페이지 ([https://studio.azureml.net](https://studio.azureml.net)). 

2. Hello 메뉴를 클릭 ![메뉴][1] hello 창의 hello 왼쪽 위 모퉁이 **Azure 기계 학습**선택, **Studio**에 로그인 합니다.

3. 클릭 **+ 새로 만들기** hello hello 창 맨 아래에 있습니다.

4. **데이터 집합**을 선택합니다.

5. **로컬 파일에서**를 선택합니다.

    ![로컬 파일에서 데이터 집합 추가][2]

6. Hello에 **새 데이터 집합을 업로드** 대화 상자에서 클릭 **찾아보기** hello 및 **german.csv** 만든 파일입니다.

7. Hello 데이터 집합에 대 한 이름을 입력 합니다. 이 연습에서는 데이터 집합을 "UCI 독일 신용 카드 데이터"라고 합니다.

8. 데이터 형식으로 **머리글 없는 일반 CSV 파일(.nh.csv)**을 선택합니다.

9. 원하는 경우 설명을 추가합니다.

10. Hello 클릭 **확인** 확인 표시 합니다.  

    ![Hello 데이터 집합을 업로드 합니다.][3]

이 실험에서 사용할 수 있는 데이터 집합 모듈로 hello 데이터를 업로드 합니다.

Hello를 클릭 하 여 tooStudio를 업로드 한 데이터 집합을 관리할 수 있습니다 **데이터 집합** 탭 toohello 왼쪽 hello Studio 창입니다.

![데이터 집합 관리][4]

다른 데이터 형식을 실험으로 가져오는 방법에 대한 자세한 내용은 [Azure Machine Learning Studio로 학습 데이터 가져오기](machine-learning-data-science-import-data.md)를 참조하세요.

**다음 단계: [새 실험 만들기](machine-learning-walkthrough-3-create-new-experiment.md)**

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
