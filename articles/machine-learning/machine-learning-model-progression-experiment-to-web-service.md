---
title: "Azure 기계 학습 모델 aaaHow 되는 웹 서비스 | Microsoft Docs"
description: "어떻게 하면 Azure 기계 학습 모델의에서 진행 되 면 개발 실험 tooan의 hello 메커니즘에 대해 간략하게 병원 웹 서비스입니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 25e0c025-f8b0-44ab-beaf-d0f2d485eb91
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 2bbe09fa8fa22662cf8ec4a8b6249d23c87c8ddf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-a-machine-learning-model-progresses-from-an-experiment-tooan-operationalized-web-service"></a>실험 tooan의 기계 학습 모델 진행 되 면 웹 서비스를 병원 하는 방법
Azure 기계 학습 스튜디오에서는 toodevelop, 실행을 허용 하는 대화형 캔버스, 테스트 및 반복는 ***실험*** 예측 분석 모델을 나타내는입니다. 다음 작업에 사용할 수 있는 모듈을 매우 다양하게 갖추고 있습니다.

* 실험에 대한 데이터 입력
* Hello 데이터 조작
* 기계 학습 알고리즘을 통한 모델 학습
* Hello 모델 점수 매기기
* Hello 결과 평가
* 최종 값 출력

실험에 만족했으면 사용자가 새 데이터를 전송하고 그 결과를 다시 받을 수 있도록 해당 실험을 ***기존 Azure Machine Learning 웹 서비스*** 또는 ***새 Azure Machine Learning 웹 서비스***로 배포할 수 있습니다.

이 문서에서는 어떻게 여 기계 학습 모델의에서 진행 되 면 개발 실험 tooan 병원 웹 서비스의 hello 메커니즘에 대해 간략하게를 제공 합니다.

> [!NOTE]
> 다른 방법으로 toodevelop는 기계 학습 모델을 배포 하 고 있지만이 문서는 기계 학습 스튜디오를 사용 하는 방법에 데 사용 됩니다. 예를 들어 tooread 어떻게 toocreate R 통해 클래식 예측 웹 서비스 hello 블로그 게시물을 참조에 대 한 설명 [빌드 및 배포 예측 웹 응용 프로그램 사용 하 여 RStudio 및 Azure ML](http://blogs.technet.com/b/machinelearning/archive/2015/09/25/build-and-deploy-a-predictive-web-app-using-rstudio-and-azure-ml.aspx)합니다.
> 
> 

개발 및 배포 하면 Azure 기계 학습 스튜디오는 디자인 된 toohelp는 *예측 분석 모델*, 가능한 toouse Studio toodevelop 실험 예측 분석 모델을 포함 하지 않는 것이 있습니다. 한 다음 출력 hello 결과 조작, 실험 방금 입력된 데이터를 수도 있습니다는 예를 들어 있습니다. 예측 분석 실험에서와 마찬가지로이 아닌 예측 실험 웹 서비스로 배포할 수 있습니다 하지만 hello 실험 학습 아니거나 기계 학습 모델 점수 매기기 때문에 더 간단한 프로세스입니다. 이러한 방식으로 hello 일반적인 toouse Studio 없을 때 합니다 포함 hello 토론 Studio 작동 하는 방법에 대 한 전체 설명은 제공할 수 있도록 합니다.

## <a name="developing-and-deploying-a-predictive-web-service"></a>예측 웹 서비스 개발 및 배포
일반적인 솔루션을 개발 하 고 기계 학습 스튜디오를 사용 하 여 배포 뒤에 오는 hello 단계는 다음과 같습니다.

![배포 흐름](media/machine-learning-model-progression-experiment-to-web-service/model-stages-from-experiment-to-web-service.png)

*그림 1 - 일반적인 예측 분석 모델의 단계*

### <a name="hello-training-experiment"></a>hello 학습 실험
hello ***학습 실험*** 기계 학습 스튜디오에서 웹 서비스를 개발의 초기 단계 hello입니다. hello hello 학습 실험의 목적은 toogive 장소 toodevelop 테스트, 반복, 및 결국 기계 학습 모델을 학습 합니다. 있습니다 수도 모델을 학습 여러 동시에 hello 최상의 솔루션에 대 한 보이지만 실험 있습니다 학습 하는 단일 선택 작업이 끝난 후으로 모델링 한 hello rest hello 실험에서 제거 합니다. 예측 분석 실험 개발의 예를 보려면 [Azure 기계 학습의 신용 위험 평가에 대한 예측 분석 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)을 참조하세요.

### <a name="hello-predictive-experiment"></a>hello 예측 실험
학습 실험에서 학습된 된 모델을 설정한 후 클릭 **웹 서비스 설정** 선택 **예측 웹 서비스** 교육을 변환 하는 기계 학습 스튜디오 tooinitiate hello in-process tooa 실험 ***예측 실험***합니다. hello 예측 실험의 목적은 hello toouse를 사용 하 여 학습 된 모델 tooscore 새 데이터를 Azure 웹 서비스로 결국 병원 되 고의 hello 목표 됩니다.

이 변환은 있습니다에 대 한 단계를 수행 하는 hello를 통해 수행 됩니다.

* 단일 모듈에는 학습에 사용 되는 모듈의 hello 집합을 변환 하 고 학습 된 모델로 저장
* 관련 되지 않은 불필요 한 모듈을 모두 제거 tooscoring
* 입력을 추가 하 고 hello 최종 웹 서비스가 사용 하는 포트를 출력 합니다.

웹 서비스로 사용자 예측 실험 준비 toodeploy toomake tooget 원하는 변경 작업을 더 있을 수 있습니다. 예를 들어 hello 웹 서비스 toooutput 결과의 하위 집합만 원하는 경우 hello 출력 포트 하기 전에 필터링 모듈을 추가할 수 있습니다.

이 변환 프로세스에서 hello 학습 실험 삭제 된 경우. Studio에서 두 개의 탭이 있는 hello 프로세스가 완료 되 면: hello 학습 실험 및 hello 예측 실험에 한 합니다. 이러한 방식으로 변경할 수 있습니다 toohello 학습 실험 하 여 웹 서비스를 배포 하 고 hello 예측 실험을 다시 작성 하기 전에. 또는 실험의 다른 줄 hello 학습 실험 toostart의 복사본을 저장할 수 있습니다.

> [!NOTE]
> 클릭할 때 **예측 웹 서비스** 자동 프로세스 tooconvert 학습 실험 tooa 예측 실험를 시작 하 고 대부분의 경우에 작동 합니다. 학습 실험 요소가 복잡 하면 (예를 들어 있으면 함께 조인 하는 학습에 대 한 여러 경로) 할 것 toodo이이 변환은 수동으로 합니다. 자세한 내용은 참조 [어떻게 tooprepare Azure 기계 학습 스튜디오에서 배포에 대 한 모델](machine-learning-convert-training-experiment-to-scoring-experiment.md)합니다.
> 
> 

### <a name="hello-web-service"></a>hello 웹 서비스
예측 실험이 준비되었으면 서비스를 기존 웹 서비스 또는 Azure Resource Manager에 기반한 새 웹 서비스로 배포할 수 있습니다. toooperationalize로 배포 하 여 모델에는 *클래식 컴퓨터 학습 웹 서비스*, 클릭 **웹 서비스 배포** 선택 **웹 서비스 배포 [기본]**합니다. 으로 toodeploy *새 컴퓨터 학습 웹 서비스*, 클릭 **웹 서비스 배포** 선택 **웹 서비스 배포 [New]**합니다. 사용자가 이제 hello 웹 서비스 REST API를 사용 하 여 데이터 tooyour 모델 보내고 받을 수 백 hello 결과입니다. 자세한 내용은 참조 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.

## <a name="hello-non-typical-case-creating-a-non-predictive-web-service"></a>일반적인 아닌 경우 hello: 예측 웹 서비스 만들기
실험을 학습 하지 않는 경우 다음 예측 분석 모델을 학습 실험 및 점수 매기기 실험 모두 toocreate를 필요 하지 않습니다-하나만 실험 되며 웹 서비스로 배포할 수 있습니다. 기계 학습 스튜디오 실험 사용한 적이 있다면 hello 모듈을 분석 하 여 예측 모델을 포함 되는지 여부를 검색 합니다.

실험을 반복한 후 만족한 경우:

1. **웹 서비스 설정**을 클릭하고 **재학습 웹 서비스**를 선택합니다. 입력 및 출력 노드가 자동으로 추가됩니다.
2. **실행**을 클릭합니다.
3. 클릭 **웹 서비스 배포** 선택 **웹 서비스 배포 [기본]** 또는 **웹 서비스 배포 [New]** 원하는 toodeploy hello 환경 toowhich 따라 합니다.

이제 웹 서비스가 배포되고 예측 웹 서비스처럼 액세스하고 관리할 수 있습니다.

## <a name="updating-your-web-service"></a>웹 서비스 업데이트
웹 서비스 실험을 배포한 경우에 어떻게 해야 tooupdate 것?

필요한 항목에 종속 된 tooupdate:

**Toochange hello 입력 또는 출력으로 원하는 또는 toomodify 원하는 hello 웹 서비스에서 데이터를 조작 하는 방법**

Hello 예측 실험을 편집 하 고 클릭 수 hello 모델을 변경 하지 않는 해도 hello 웹 서비스에서 데이터를 처리 하는 방법을 변경만 하는 경우 **웹 서비스 배포** 선택 **[기본]웹서비스배포** 또는 **웹 서비스 배포 [New]** 다시 합니다. hello 웹 서비스를 중지 하 고 hello 업데이트 된 예측 실험 배포 된 hello 웹 서비스를 다시 시작 합니다.

다음은 예제: hello hello 사용 하 여 입력된 데이터의 전체 행을 반환 하는 예측 실험 가정 결과 예측 합니다. Hello 웹 서비스 toojust 반환 hello 결과 한다는 것을 결정할 수 있습니다. 추가할 수 있도록는 **열 프로젝션** hello 예측 실험에서 모듈, hello 출력 포트를 배치 하기 바로 전에 hello 이외의 tooexclude 열 발생 합니다. 클릭할 때 **웹 서비스 배포** 선택 **웹 서비스 배포 [기본]** 또는 **웹 서비스 배포 [New]** hello 웹 서비스를 다시 업데이트 됩니다.

**Tooretrain hello 모델에 새 데이터를 원합니다**

Tookeep 기계 학습 모델을를 원하지만 tooretrain 원하는 경우이 새 데이터로 두 가지 옵션이 있습니다.

1. **Hello 웹 서비스가 실행 되는 동안 hello 모델을 다시 학습** -원할 경우 tooretrain 모델 hello 예측 하는 웹 서비스가 실행 중인 동안 할 수 있는이 몇 가지 수정 사항을 toohello 학습 실험 toomake 함으로써 것는 *** 실험 재교육***, 다음으로 배포할 수는  ***재교육 웹* 서비스**합니다. 방법에 대 한 지침은 toodo이,이 참조 [기계 학습을 다시 학습을 프로그래밍 방식으로 모델링](machine-learning-retrain-models-programmatically.md)합니다.
2. **원래 학습 실험 toohello 돌아가서 다른 학습 데이터 toodevelop 모델에 사용 하 여** -예측 실험은 연결 된 toohello 웹 서비스를 유지 하지만 hello 학습 실험 이러한 방식으로 직접 연결 되어 있지 않습니다. Hello 원래 학습 실험을 수정 하 고 클릭 **웹 서비스 설정**, 만들어집니다는 *새* 예측을 실험 배포 될 때 만들어집니다는 *새* 웹 서비스입니다. 웹 서비스를 원래 hello 방금 업데이트 하지는 않습니다.
   
   Toomodify hello 학습 실험 해야 할 경우 열고 클릭 **다른 이름으로 저장** toomake 복사본입니다. 이렇게 하면 원래 학습 실험 그대로 hello, 예측 실험 및 웹 서비스 유지 됩니다. 이제 변경 내용을 포함한 새 웹 서비스를 만들 수 있습니다. Hello 결정할 수 있습니다는 새 웹 서비스를 배포 하 고 나면 toostop는 hello 이전 웹 서비스 또는 새 hello와 함께 실행 하기 위해서는 여부.

**다른 모델 tootrain 원합니다**

Toomake tooyour 원래 예측 실험에서는 여러 기계 학습 알고리즘을 선택 하는 등을 변경 하려는 경우 등 서로 다른 학습 메서드 시도 다음 필요한 모델 학습을 다시 수행할 위에서 설명한 toofollow hello 두 번째 절차: hello 학습 실험을 열고 **다른 이름으로 저장** toomake 복사본을 한 후 시작 모델을 개발, hello 예측 실험 만들기 및 배포의 새 경로로 hello 아래로 hello 웹 서비스입니다. 이렇게 하면 새 만들어집니다 웹 서비스와 관련 없는 toohello 원래-실행 하는 한 개 또는 두 위치에서 모두 tookeep 결정할 수 있습니다.

## <a name="next-steps"></a>다음 단계
개발 하 고 실험의 hello 프로세스에 대 한 자세한 내용은 다음 문서는 hello 참조:

* hello 실험-변환 [어떻게 tooprepare Azure 기계 학습 스튜디오에서 배포에 대 한 모델](machine-learning-convert-training-experiment-to-scoring-experiment.md)
* hello 웹 서비스-배포 [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)
* 재교육 hello 모델- [기계 학습을 다시 학습을 프로그래밍 방식으로 모델링](machine-learning-retrain-models-programmatically.md)

Hello 전체 프로세스의 예를 참조 합니다.

* [기계 학습 자습서: Azure 기계 학습 스튜디오에서 첫 번째 실험 만들기](machine-learning-create-experiment.md)
* [연습: Azure Machine Learning의 신용 위험 평가에 대한 예측 분석 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)

