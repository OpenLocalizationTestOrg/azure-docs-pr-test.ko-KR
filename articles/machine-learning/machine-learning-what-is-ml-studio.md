---
title: "aaaWhat은 Azure 기계 학습 스튜디오는? | Microsoft Docs"
description: "Azure ML Studio의 개요로, 알고리즘 및 모듈의 사용할 준비가 되어 있는 라이브러리에서 신속하게 모델을 빌드하기 위한 끌어서 놓기 도구입니다."
keywords: "azure 기계 학습, azure ml, 기계 학습 스튜디오"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: a25f2d9e75d088a37930de98240c6e14c9567fa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-machine-learning-studio"></a>Azure 기계 학습 스튜디오란?
Microsoft Azure 기계 학습 스튜디오 toobuild, 사용할 수 있는 공동 작업, 끌어서 놓기 도구는 테스트 및 사용자 데이터에 대 한 예측 분석 솔루션을 배포 합니다. 기계 학습 스튜디오는 Excel과 같은 BI 도구 또는 사용자 지정 앱에서 쉽게 사용할 수 있는 웹 서비스로 모델을 게시합니다.

기계 학습 스튜디오는 데이터 과학, 예측 분석, 클라우드 리소스 및 데이터가 만나는 장소입니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-machine-learning-studio-interactive-workspace"></a>대화형 hello 기계 학습 스튜디오 작업 영역
예측 분석 모델 toodevelop 일반적으로 사용 데이터 하나 이상의 소스에서 변환 및 다양 한 데이터 조작 및 통계 함수를 통해 해당 데이터를 분석 하 고 결과 집합을 생성 합니다. 이와 같은 모델을 개발하는 과정은 반복 프로세스이며, 다양 한 기능 및 해당 매개 변수에 hello, 결과 수렴 만족할 때까지 수정 하면 효과적인 모델을 학습된 해야 합니다.

**Azure 기계 학습 스튜디오** 대화형, 시각적 작업 영역 tooeasily 프로젝트를 빌드하면 제공 테스트 및 예측 분석 모델을 반복 합니다. 끌어서 놓기 있습니다 ***데이터 집합*** 및 분석 ***모듈*** 는 대화형 캔버스로 연결 함께 tooform는 ***실험***, 기계 학습에서 실행 Studio 지정 합니다. 모델 디자인에 대해 tooiterate, 원하는 경우 복사본을 저장 hello 실험 편집한 다시 실행 합니다. 준비 되 면 경우 변환할 수 있습니다 프로그램 ***학습 실험*** tooa ***예측 실험***,으로 다음 게시는 ***웹 서비스*** 모델에 액세스할 수 있도록 다른 사용자입니다.

필수, 예측 분석 모델 데이터 집합 및 모듈 tooconstruct를 시각적으로 바로 연결 없는 프로그래밍 있습니다.

> [!TIP]
> 기계 학습 스튜디오의 hello 기능의 개요 다이어그램 참조 toodownload 및 인쇄 [Azure 기계 학습 스튜디오 기능의 개요 다이어그램](machine-learning-studio-overview-diagram.md)합니다.
> 
> 

![Azure ML Studio 다이어그램: 실험을 만들고, 여러 원본에 대한 데이터 읽고, 점수 데이터를 쓰고, 모델을 작성합니다.][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a>기계 학습 스튜디오 시작
처음 입력할 때 [기계 학습 스튜디오](https://studio.azureml.net) hello 참조 **홈** 페이지. 여기에서 설명서, 동영상, 웹 세미나를 보고 다른 유용한 리소스를 찾을 수 있습니다.

Hello 왼쪽 위 메뉴를 클릭 합니다. ![메뉴](media/machine-learning-what-is-ml-studio/menu.png) 몇 가지 옵션이 표시됩니다.

### <a name="cortana-intelligence"></a>Cortana Intelligence
클릭 **Cortana 인텔리전스** hello의 toohello 홈 페이지로 이동 됩니다 및 [Cortana 인텔리전스 Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite)합니다. hello Cortana Intelligence Suite는 완전히 관리 되는 큰 데이터 및 분석 suite tootransform 데이터 지능형 동작으로 고급 합니다. Hello Suite 홈 페이지를 고객의 이야기를 포함 한 전체 설명서를 참조 하십시오.

### <a name="azure-machine-learning"></a>Azure 기계 학습
두 가지 옵션이 여기에서 **홈**, 시작 위치, hello 페이지 및 **Studio**합니다.

클릭 **Studio** toohello 이동 됩니다 및 **Azure 기계 학습 스튜디오**합니다. 먼저 만들라는 메시지가 Microsoft 계정 또는 회사 또는 학교 계정을 사용 하 여 toosign 합니다. 로그인 한 후에 hello 탭에 나오는 hello 왼쪽에 표시 됩니다.

* **프로젝트** - 단일 프로젝트를 나타내는 실험, 데이터 집합, notebooks 및 기타 리소스의 컬렉션입니다.
* **실험** - 만들고 실행하거나 초안으로 저장한 실험입니다.
* **웹 서비스** - 실험에서 배포한 웹 서비스입니다.
* **노트북** - 사용자가 만든 Jupyter 노트북입니다.
* **데이터 집합** - 스튜디오로 업로드한 데이터 집합입니다.
* **학습된 모델** - 실험에서 학습하고 스튜디오에 저장한 모델입니다.
* **설정** -계정 및 리소스 tooconfigure를 사용할 수 있는 설정의 컬렉션입니다.

### <a name="gallery"></a>갤러리
클릭 **갤러리** toohello 이동 됩니다 및  **[Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com/)**합니다. hello 갤러리에는 데이터 과학자 및 개발자의 커뮤니티 hello Cortana Intelligence 제품군의 구성 요소를 사용 하 여 만든 솔루션을 공유 하는 곳입니다.

Hello 갤러리에 대 한 자세한 내용은 참조 [공유 hello Cortana Intelligence 갤러리에서에서 솔루션을 검색 하 고](machine-learning-gallery-how-to-use-contribute-publish.md)합니다.

## <a name="components-of-an-experiment"></a>실험 구성 요소
실험 서로 연결 하는 데이터 tooanalytical 모듈을 제공 하는 데이터 집합으로 이루어져 tooconstruct 예측 분석 모델입니다. 특히 유효한 실험에는 다음 특성이 포함됩니다.

* hello 실험에 하나 이상의 데이터 집합 및 하나의 모듈
* 데이터 집합에 연결 된 유일한 toomodules 될 수 있습니다.
* 연결 된 tooeither 데이터 집합 또는 다른 모듈 모듈 일 수 있습니다.
* 모듈에 대 한 모든 입력된 포트에는 일부 연결 toohello 데이터를 사용 해야 합니다. 흐름
* 각 모듈에 대한 모든 필수 매개 변수를 설정해야 합니다.

실험을 처음부터 만들거나 기존 샘플 실험을 템플릿으로 사용할 수 있습니다. 자세한 내용은 참조 [코드 예제에서는 실험 toocreate 새 기계 학습 실험](machine-learning-sample-experiments.md)합니다.

간단한 실험을 만드는 예는 [Azure 기계 학습 스튜디오에서 간단한 실험 만들기](machine-learning-create-experiment.md)를 참조하세요.

예측 분석 솔루션을 만드는 자세한 연습 과정은 [Azure 기계 학습을 사용한 예측 솔루션 개발](machine-learning-walkthrough-develop-predictive-solution.md)을 참조하세요.

### <a name="datasets"></a>데이터 집합
데이터 집합은 모델링 프로세스 hello에 사용할 수 있도록 된 데이터 tooMachine 학습 스튜디오를 업로드 합니다. 다양 한 예제 데이터 집합, tooexperiment에 대 한 기계 학습 스튜디오에 포함 되며 필요에 따라 더 많은 데이터 집합을 업로드할 수 있습니다. 포함된 데이터 집합의 몇 가지 예제는 다음과 같습니다.

* **다양한 자동차에 대한 MPG 데이터** - 실린더 수, 마력 등으로 식별되는 자동차에 대한 MPG 값
* **유방암 데이터** - 유방암 진단 데이터
* **산불 데이터** - 포르투갈 북동부에서 발생한 산불 규모

실험을 만들 때 선택할 수 있습니다 사용할 수 있는 데이터 집합의 hello 목록에서 toohello hello 캔버스의 왼쪽.

목록이 기계 학습 스튜디오에 포함 된 샘플 데이터 집합에 대 한 참조 [hello 예제 데이터 집합을 사용 하 여 Azure 기계 학습 스튜디오에서](machine-learning-use-sample-datasets.md)합니다.

### <a name="modules"></a>모듈
모듈은 데이터에 대해 수행할 수 있는 알고리즘입니다. 기계 학습 스튜디오에 데이터 유입 함수 tootraining, 상태 평가 및 유효성 검사 프로세스에서 사이의 모듈의 수입니다. 포함된 모듈의 몇 가지 예제는 다음과 같습니다.

* [TooARFF 변환] [ convert-to-arff] -변환 직렬화 된.NET dataset tooAttribute 관계 파일 형식 (ARFF).
* [기본 통계 계산][elementary-statistics] - 평균, 표준 편차 등의 기본 통계를 계산합니다.
* [선형 회귀][linear-regression] - 온라인 기울기 하강 기반 선형 회귀 모델을 만듭니다.
* [모델 점수 매기기][score-model] - 학습된 분류 또는 회귀 모델의 점수를 매깁니다.

실험을 만들 때 선택할 수 있습니다 사용할 수 있는 모듈의 hello 목록에서 toohello hello 캔버스의 왼쪽.  

모듈은 tooconfigure hello 모듈의 내부 알고리즘을 사용할 수 있는 매개 변수 집합이 있을 수 있습니다. Hello에 hello 모듈의 매개 변수가 표시 됩니다 hello 캔버스에 모듈을 선택 하면 **속성** hello 캔버스의 오른쪽 창 toohello 합니다. 모델의 해당 창 tootune hello 매개 변수를 수정할 수 있습니다.

일부 도움말 탐색 하는 데 사용할 수 있는 기계 학습 알고리즘의 대규모 라이브러리 hello 참조 하세요. [어떻게 toochoose Microsoft Azure 기계 학습 알고리즘](machine-learning-algorithm-choice.md)합니다.

## <a name="deploying-a-predictive-analytics-web-service"></a>예측 분석 웹 서비스 배포
예측 분석 모델이 준비되면 기계 학습 스튜디오에서 곧바로 해당 모델을 웹 서비스로 배포할 수 있습니다. 이 프로세스에 대한 자세한 내용은 [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
