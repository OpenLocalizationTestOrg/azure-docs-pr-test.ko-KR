---
title: "5 단계: hello 기계 학습 웹 서비스 배포 | Microsoft Docs"
description: "예측 솔루션 연습을 개발 하는 hello의 5 단계: 웹 서비스로 기계 학습 스튜디오에서 예측 실험을 배포 합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a>5 단계를 연습: hello Azure 기계 학습 웹 서비스를 배포 합니다.
이 hello 연습의 5 단계 hello [Azure 기계 학습에서 예측 분석 솔루션을 개발 합니다.](machine-learning-walkthrough-develop-predictive-solution.md)

1. [기계 학습 작업 영역 만들기](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [기존 데이터 업로드](machine-learning-walkthrough-2-upload-data.md)
3. [새 실험 만들기](machine-learning-walkthrough-3-create-new-experiment.md)
4. [학습 하 고 hello 모델 평가](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. **Hello 웹 서비스를 배포 합니다.**
6. [액세스 hello 웹 서비스](machine-learning-walkthrough-6-access-web-service.md)

- - -
toogive 다른 사용자에 게 기회 toouse hello이 연습에서 개발 했습니다 예측 모델에서는으로 배포 Azure에서 웹 서비스입니다.

Toothis 포인트 म 했으므로 되었습니다 작업할 수 있도록이 모델을 학습 합니다. 하지만 배포 된 hello 서비스 toodo 학습 하 고 더 이상 중임-hello 사용자의 입력이 모델을 기반으로 점수를 지정 하 여 새 예측 toogenerate 것입니다. Toodo 여기 되므로 일부 준비 tooconvert이 실험에서 ***학습*** tooa 실험 ***예측*** 시험 합니다. 

이 작업은 세 단계로 이루어집니다.  

1. Hello 모델 중 하나를 제거 합니다.
2. Hello 변환 *학습 실험* 에 만들었습니다는 *예측 실험*
3. Hello 예측 실험을 웹 서비스로 배포

## <a name="remove-one-of-hello-models"></a>Hello 모델 중 하나를 제거 합니다.

먼저 tootrim이이 실험 아래로 약간 합니다. 서로 다른 두 모델 hello 실험에 현재 있는 하지만이 웹 서비스로 배포 하기 때만 toouse 모델을 하나 포함 하려고 합니다.  

해당 hello 승격 된 트리 모델 보다 성능이 좋아졌다 hello SVM 모델 보다 하기로 한 경우를 가정해 봅니다. 첫 번째 사항은 toodo hello 제거 hello 이므로 [2 클래스 지원 벡터 컴퓨터] [ two-class-support-vector-machine] 모듈 및 학습에 사용 된 hello 모듈입니다. 클릭 하 여 toomake hello 실험의 복사본을 먼저 원하는 수 **다른 이름으로 저장** 실험 캔버스 hello hello 맨 아래에 있습니다.

다음 모듈 toodelete hello를 해야 합니다.  

* [2클래스 Support Vector Machine][two-class-support-vector-machine]
* [모델을 학습] [ train-model] 및 [모델 점수 매기기] [ score-model] 연결된 tooit 있던 모듈
* [데이터 표준화][normalize-data](둘 다)
* [모델 평가] [ evaluate-model] (hello 모델 평가 완료 하기)

각 모듈을 선택 하 고 hello Delete 키 또는 오른쪽 클릭 hello 모듈 키를 눌러 선택한 **삭제**합니다. 

![Hello SVM 모델 제거][3a]

모델은 다음과 같이 표시됩니다.

![Hello SVM 모델 제거][3]

Hello를 사용 하 여 모델이 이제 준비 toodeploy 우리 [2 클래스 승격 된 의사 결정 트리][two-class-boosted-decision-tree]합니다.

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Hello 학습 실험 tooa 예측 실험으로 변환

tooget이 준비에 대 한 모델 배포,이 항목이 필요한 tooconvert 실험 tooa 예측 실험을 학습 합니다. 이는 세 가지 단계를 포함합니다.

1. 한 학습 하 고 다음이 교육 모듈을 교체 하는 hello 모델 저장
2. 트리밍 학습용만 필요한 hello 실험 tooremove 모듈
3. Hello 웹 서비스 입력을 받아들입니다 위치 hello 출력을 생성 및 정의 합니다.

수동으로 할 수 있습니다 하지만 다행히 클릭 하 여 세 단계 모두를 수행할 수 있습니다 **웹 서비스 설정** hello hello 실험 캔버스 맨 아래에 (hello를 선택 하 고 **예측 웹 서비스** 옵션)입니다.

> [!TIP]
> 경우에 더 많은 세부 정보를 원하는 예측 학습 실험 tooa 변환 하면 어떤 일이 생기 실험을 참조 하십시오 [어떻게 tooprepare Azure 기계 학습 스튜디오에서 배포에 대 한 모델](machine-learning-convert-training-experiment-to-scoring-experiment.md)합니다.

**웹 서비스 설정**을 클릭하면 다음과 같은 결과가 발생합니다.

* hello 학습 된 모델은 변환 된 tooa 단일 **학습 된 모델** 모듈 및 모듈 색상표 toohello hello에에서 저장 된 hello 왼쪽 실험 캔버스 (아래에서 찾을 수 있습니다 **학습 된 모델**)
* 다음을 비롯하여 학습에 사용된 모듈은 제거됩니다.
  * [2클래스 향상된 의사 결정 트리][two-class-boosted-decision-tree]
  * [모델 학습][train-model]
  * [데이터 분할][split]
  * 두 번째 hello [R 스크립트 실행] [ execute-r-script] 테스트 데이터에 사용 된 모듈
* 학습 된 모델을 저장 하는 hello hello 실험에 다시 추가 된
* **웹 서비스 입력** 및 **웹 서비스 출력** 모듈 추가 됩니다 (여기 확인할 수 있는 hello 사용자의 데이터는 hello 모델 입력과 hello 웹 서비스에 액세스할 때 어떤 데이터가 반환 됩니다)

> [!NOTE]
> Hello 실험 hello 위쪽 hello 실험 캔버스에 추가 된 탭 아래의 두 부분으로 저장 되어 있음을 확인할 수 있습니다. hello 원래 학습 실험은 hello 탭 아래의 **학습 실험**, 하며은에서 새로 만든 예측 실험 hello **예측 실험**합니다. hello 예측 실험은 hello를 웹 서비스로 배포 하나입니다.

이 특정 실험으로 tootake 한 추가 단계가 필요합니다.
두 개의 추가 [R 스크립트 실행] [ execute-r-script] 모듈 tooprovide 가중치가 toohello 데이터 작동 합니다. 그건 hello 최종 모델에서 해당 모듈 파괴 하므로 학습 및 테스트에 필요 하는 트릭만.
기계 학습 스튜디오 제거 하나 [R 스크립트 실행] [ execute-r-script] hello를 제거할 때 모듈 [분할] [ split] 모듈입니다. 이제 제거할 수 있습니다 다른 hello 및 연결 [메타 데이터 편집기] [ metadata-editor] 직접 너무[모델 점수 매기기][score-model]합니다.    

이제 실험은 다음과 같이 표시됩니다.  

![Hello 학습 된 모델 점수 매기기][4]  

> [!NOTE]
> Hello 예측 실험에서 hello UCI 독일어 신용 카드 데이터 데이터 집합부터 이유 할까요? hello 서비스 tooscore hello 사용자 데이터를 하지 hello 원래 데이터 집합, 이유 두세요 hello 원래 데이터 집합 hello 모델에서 진행 되는?
> 
> Hello 서비스 하지 않는 원래 신용 카드 데이터 hello 필요 그렇습니다. 하지만 hello 스키마 열 개수와 같은 정보 포함 하는 열은 숫자 및 해당 데이터에 대 한 필요는 없습니다. 이 스키마 정보는 필요한 toointerpret hello 사용자의 데이터입니다. 이러한 구성 요소 hello 점수 매기기 모듈에 hello 데이터 집합 스키마 hello 서비스가 실행 되 고 있도록 연결 상태를 그대로 유지 합니다. hello 데이터 사용 되지 않는 hello 스키마만.  
> 
> 

Hello 실험 마지막으로 한 번 실행 (클릭 **실행**.) 모델 hello tooverify 여전히 작동 하는지, 클릭 hello의 hello 출력 [모델 점수 매기기] [ score-model] 모듈과 선택 **결과 보기**합니다. Hello 신용 위험 값 ("점수가 매겨진 레이블") 및 확률 값 ("점수가 매겨진 확률"입니다.) 점수 매기기 hello 함께 hello 원래 데이터 표시를 볼 수 있습니다. 

## <a name="deploy-hello-web-service"></a>Hello 웹 서비스를 배포 합니다.
Hello 실험 중 하나를 기본 웹 서비스로 또는 Azure 리소스 관리자에 기반 하는 새 웹 서비스로 배포할 수 있습니다.

### <a name="deploy-as-a-classic-web-service"></a>기존 웹 서비스로 배포
기존 웹 서비스는 실험에서 파생 된 toodeploy 클릭 **웹 서비스 배포** 선택한 hello 아래 캔버스로 **웹 서비스 배포 [기본]**합니다. 기계 학습 스튜디오를 웹 서비스로 hello 실험 하 고 해당 웹 서비스에 대 한 toohello 대시보드를 사용 합니다. 이 페이지에서 toohello 실험을 반환할 수 있습니다 (**스냅숏 보기** 또는 **최신 볼**) hello 웹 서비스의 간단한 테스트를 실행 하 고 (참조 **hello 웹 서비스를 테스트할** 아래). (에 자세히 설명 hello이 연습의 다음 단계에서) hello 웹 서비스에 액세스할 수 있는 응용 프로그램을 만들기 위한 여기 정보 이기도 합니다.

![웹 서비스 대시보드][6]

Hello를 클릭 하 여 hello 서비스를 구성할 수 있습니다 **구성** 탭 합니다. Hello 서비스 이름 (이 기본적으로 주어진된 hello 실험 이름)을 수정할 수는 여기 대 한 설명을 지정 합니다. Hello에 대 한 친숙 한 더 많은 레이블을 제공할 수도 입력 및 출력 데이터입니다.  

![Hello 웹 서비스 구성][5]  

### <a name="deploy-as-a-new-web-service"></a>새 웹 서비스로 배포

> [!NOTE] 
> 새 웹 서비스를 배포 하는 hello 구독 toowhich에 충분 한 권한이 있어야 합니다. toodeploy hello 웹 서비스입니다. 자세한 내용은 참조 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md)합니다. 

새 웹 서비스 toodeploy 우리의 실험에서 파생 된:

1. 클릭 **웹 서비스 배포** 선택한 hello 아래 캔버스로 **웹 서비스 배포 [New]**합니다. 기계 학습 스튜디오 toohello Azure 기계 학습 웹 서비스를 전송 **배포 실험** 페이지.

2. Hello 웹 서비스에 대 한 이름을 입력 합니다. 

3. 에 대 한 **가격 계획**가격 책정 기존 계획을 선택할 수 있습니다, 또는 계획 이름 및 선택 hello 월별 계획 옵션 선택 "새로 만들기" 및 새 제공 hello 합니다. hello 계획 계층 toohello 계획 기본 지역 및 웹 서비스에 대 한 기본 배포 toothat 영역입니다.

4. **배포**를 클릭합니다.

몇 분 후 hello **퀵 스타트** 웹 서비스에 대 한 페이지가 열립니다.

Hello를 클릭 하 여 hello 서비스를 구성할 수 있습니다 **구성** 탭 합니다. Hello 서비스를 수정할 수는 여기 제목 및 설명을 제공 합니다. 

tootest hello 웹 서비스를 hello 클릭 **테스트** 탭 (참조 **hello 웹 서비스를 테스트할** 아래). Hello 웹 서비스에 액세스할 수 있는 응용 프로그램을 만들기에 대 한 내용은 hello 클릭 **사용** 탭 (이 연습에서는 다음 단계를 hello 좀 더 자세히 논의할 됩니다).

> [!TIP]
> 배포 되었으며 후 hello 웹 서비스를 업데이트할 수 있습니다. 예를 들어 모델 toochange 하려는 경우 다음 hello 학습 실험, hello 모델 매개 변수를 수정할 편집한 클릭 **웹 서비스 배포**선택한 **웹 서비스 배포 [기본]** 또는  **웹 서비스 [New] 배포**합니다. Hello 실험을 다시 배포할 때 이제 업데이트 된 모델을 사용 하 여 hello 웹 서비스를 대체 합니다.  
> 
> 

## <a name="test-hello-web-service"></a>Hello 웹 서비스 테스트

Hello 웹 서비스에 액세스 하는 hello를 통해 hello 사용자의 데이터 입력 **웹 서비스 입력** 여기서 toohello 경과 모듈 [모델 점수 매기기] [ score-model] 모듈 및 점수가 매겨진 합니다. hello 예측 실험 설정 hello 방식으로 hello 모델 hello hello 원래 신용 위험 데이터 집합으로 동일한 형식에서 데이터를 필요로 합니다.
hello 결과 hello 통해 hello 웹 서비스에서 toohello 사용자를 반환 하는 **웹 서비스 출력** 모듈입니다.

> [!TIP]
> hello에서 결과 hello 예측 실험 구성, 전체 hello hello로 [모델 점수 매기기] [ score-model] 모듈 중 하나를 반환 합니다. 모든 입력된 데이터 hello와 hello 신용 위험 값 및 확률 점수 매기기 hello이 포함 됩니다. 하지만 원하는 경우 다른를 반환할 수 있습니다-예를 들어 hello 신용 위험 값만 반환할 수 있습니다. toodo이,이 삽입 한 [열 프로젝션] [ project-columns] 모듈 간에 [모델 점수 매기기] [ score-model] 및 hello **서비스 출력웹** 않을 tooeliminate 열 hello 웹 서비스 tooreturn 합니다. 
> 
> 

기본 웹을 테스트할 수 있습니다에 서비스 **기계 학습 스튜디오** 또는 hello **Azure 컴퓨터 학습 웹 서비스** 포털입니다.
Hello에만 새 웹 서비스를 테스트할 수 **컴퓨터 학습 웹 서비스** 포털입니다.

> [!TIP]
> Hello Azure 컴퓨터 학습 웹 서비스 포털을 테스트할 때 tootest hello 요청 응답 서비스를 사용할 수 있는 예제 데이터 만들기 hello 포털을 사용할 수 있습니다. Hello에 **구성** 페이지에서 "Yes"에 대 한 선택 **샘플 데이터 활성화?**합니다. Hello에 hello 요청-응답 탭을 열면 **테스트** hello 원래 신용 위험 데이터 집합에서 가져온 예제 데이터 페이지에서 hello 포털 채웁니다.

### <a name="test-a-classic-web-service"></a>기존 웹 서비스 테스트

기계 학습 스튜디오에서 이나 hello 컴퓨터 학습 웹 서비스 포털에서 기본 웹 서비스를 테스트할 수 있습니다. 

#### <a name="test-in-machine-learning-studio"></a>Machine Learning Studio에서 테스트

1. Hello에 **대시보드** hello 웹 서비스에 대 한 페이지에서 hello **테스트** 단추 **기본 끝점**합니다. 대화 상자를 표시 하 고 hello hello 서비스에 대 한 입력된 데이터 있습니다 요청 합니다. 이 hello hello 원래 신용 위험 데이터 집합에 표시 된 같은 열이 있습니다.  

2. 데이터 집합을 입력하고 **확인**을 클릭합니다. 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a>Hello 컴퓨터 학습 웹 서비스 포털에서 테스트

1. Hello에 **대시보드** hello 웹 서비스에 대 한 페이지에서 hello **테스트 미리 보기** 링크 **기본 끝점**합니다. hello 테스트 페이지 hello 웹 서비스 끝점에 대 한 hello Azure 컴퓨터 학습 웹 서비스 포털을 열고 hello hello 서비스에 대 한 입력된 데이터를 합니다. 이 hello hello 원래 신용 위험 데이터 집합에 표시 된 같은 열이 있습니다.

2. **요청-응답 테스트**를 클릭합니다. 

### <a name="test-a-new-web-service"></a>새 웹 서비스 테스트

Hello 컴퓨터 학습 웹 서비스 포털에만 새 웹 서비스를 테스트할 수 있습니다.

1. Hello에 [Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net/quickstart) 포털 **테스트** hello hello 페이지 위쪽에 있습니다. hello **테스트** 페이지가 열리고 hello 서비스에 대 한 데이터를 입력할 수 있습니다. hello 원래 신용 위험 데이터 집합에 표시 되었던 toohello 열을 해당 하는 hello 입력된 필드를 나열 합니다. 

2. 데이터 집합을 입력하고 **요청-응답 테스트**를 클릭합니다.

hello hello 테스트의 결과에 표시 됩니다 hello hello 출력 열에 hello 페이지의 오른쪽입니다. 


## <a name="manage-hello-web-service"></a>Hello 웹 서비스를 관리 합니다.

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a>Hello Azure 클래식 포털에서에서 기본 웹 서비스 관리

기본 웹 서비스를 배포 하 고 나면 hello에서 관리할 수 있습니다 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)
2. Hello Microsoft Azure 서비스 패널에서 **기계 학습**
3. 작업 영역을 클릭합니다.
4. Hello 클릭 **웹 서비스** 탭
5. 만든 hello 웹 서비스를 클릭 합니다.
6. Hello "기본" 끝점을 클릭 합니다.

여기에서는 hello 웹 서비스를 수행 하는 방법을 모니터링 하는 같은 작업을 수행할 수 있으며 개수 동시 호출 hello 서비스에서 처리할 수를 변경 하 여 가지 성능 조정을 만들 수 있습니다.

자세한 내용은 다음을 참조하세요.

* [끝점 만들기](machine-learning-create-endpoint.md)
* [웹 서비스 확장](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a>기본 또는 hello Azure 컴퓨터 학습 웹 서비스 포털에서 새 웹 서비스 관리

기존 또는 새 웹 서비스를 배포, 하 고 나면 hello에서 관리할 수 있습니다 [Microsoft Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net/quickstart) 포털입니다.

웹 서비스의 toomonitor hello 성능:

1. Toohello 로그인 [Microsoft Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net/quickstart) 포털
2. **웹 서비스**를 클릭합니다.
3. 해당 웹 서비스를 클릭합니다.
4. Hello 클릭 **대시보드**

- - -
**다음: [hello 웹 서비스에 액세스](machine-learning-walkthrough-6-access-web-service.md)**

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
