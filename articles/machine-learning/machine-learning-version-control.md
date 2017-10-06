---
title: "Azure 기계 학습에서 aaaALM | Microsoft Docs"
description: "Azure Machine Learning 스튜디오에서 응용 프로그램 수명 주기 관리 모범 사례 적용"
keywords: "AML, ALM, Azure ML, 응용 프로그램 수명 주기 관리, 버전 제어"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1be6577d-f2c7-425b-b6b9-d5038e52b395
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: haining
ms.openlocfilehash: 99470ff72fea7ab59d9d44f3fded7b9dd49a38c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-lifecycle-management-in-azure-machine-learning-studio"></a>Azure Machine Learning 스튜디오에서 응용 프로그램 수명 주기 관리
Azure 기계 학습 스튜디오는 hello Azure 클라우드 플랫폼에서 병원 기계 학습 실험을 개발 하기 위한 도구입니다. Visual Studio IDE 및 확장 가능한 클라우드 서비스에 단일 플랫폼 병합 hello 라는 것 같습니다. Azure 기계 학습 스튜디오에 표준 관리 ALM (Application Lifecycle) 사례 버전 관리를 다양 한 자산 tooautomated 실행 및 배포를 통합할 수 있습니다. 이 문서에는 hello 옵션 및 접근 방식 중 일부를 설명합니다.

## <a name="versioning-experiment"></a>실험 버전 관리
실험은 두 가지 권장된 방법은 tooversion 합니다. 기본 제공 실행된 기록이에 의존 하거나 hello 실험 개체 JSON (JavaScript Notation) 형식으로 내보낼 하 고 외부에서 관리 수 합니다. 각 접근 방식에는 장단점이 있습니다.

### <a name="experiment-snapshots-using-run-history"></a>실행 기록을 사용하는 실험 스냅숏
Hello hello를 클릭할 때마다 Azure 기계 학습 스튜디오 학습 실험의 실행 모델 hello에서에서 **실행** hello 실험 편집기는 변경할 수 없는 스냅숏 hello 실험 단추는 제출 된 toohello 작업 스케줄러입니다. Hello를 클릭 하 여이 스냅숏 목록을 볼 수 있습니다 **실행 기록** hello 실험 편집기 뷰에서 hello 명령 모음에서 단추입니다.

![실행 기록 단추](media/machine-learning-version-control/runhistory.png)

할 수 있습니다 하 고 hello 시간 hello 실험에서 hello 실험 hello 이름을 클릭 하 여 잠금 모드에서 열린 hello 스냅숏이 toorun 제출된 된 hello 스냅숏이 만들어진 합니다. Hello 현재 실험을 나타내며 hello 목록에서 첫 번째 항목을 hello만 하는 편집 가능한 상태에 있습니다. 또한 각 스냅숏은 완료(부분 실행), 실패, 실패(부분 실행) 또는 초안을 비롯한 다양한 상태라는 점을 기억합니다.

![실행 기록 목록](media/machine-learning-version-control/runhistorylist.png)

가 열리고 나면 새 실험으로 hello 스냅숏 실험을 저장 하 고 수정할 수 있습니다. 학습 된 모델, 변환 또는 데이터 집합 등의 버전 업데이트 된 자산을 포함 하는 실험 스냅숏, hello 스냅숏을 만들었을 때 hello 스냅숏 hello 참조 toohello 원래 버전을 유지 합니다. 잠긴 hello를 저장 하는 경우 새 실험으로 스냅숏 Azure 기계 학습 스튜디오 검색 이러한 자산의 최신 버전의 hello 존재 하 고 hello 새 실험에서이 자동으로 업데이트 합니다.

Hello 실험을 삭제 하면 해당 실험의 모든 스냅숏은 삭제 됩니다.

### <a name="exportimport-experiment-in-json-format"></a>JSON 형식으로 실험 내보내기/가져오기
실행 하는 hello 기록 스냅숏을 제출 된 toorun 될 때마다 Azure 기계 학습 스튜디오에서 hello 실험 하는 변경할 수 없는 버전을 유지 합니다. Hello 실험의 로컬 복사본을 저장할 수도 및 Team Foundation Server와 같은 tooyour 즐겨 찾는 소스 제어 시스템에서 확인 하 고 나중에 해당 로컬 파일에서 실험을 다시 만들 수 있습니다. Hello를 사용할 수 있습니다 [Azure 컴퓨터 학습 PowerShell](http://aka.ms/amlps) commandlet [ *내보내기 AmlExperimentGraph* ](https://github.com/hning86/azuremlps#export-amlexperimentgraph) 및 [  *가져오기 AmlExperimentGraph* ](https://github.com/hning86/azuremlps#import-amlexperimentgraph) tooaccomplish입니다.

hello JSON 파일은 hello의 텍스트 표현을 실험 그래프 참조 tooassets 학습 된 모델 또는 데이터 집합을 같은 hello 작업 영역에 포함 될 수 있습니다. Hello asset의 직렬화 된 버전이 포함 되어 있지 합니다. Tooimport hello JSON 문서 hello 작업 영역에 다시 시도 하면 참조 하는 hello 자산 이미 있어야 hello로 동일 자산 hello 실험에서 참조 되는 Id입니다. 그렇지 않으면 수 tooaccess 가져온 hello 실험 되지 않습니다.

## <a name="versioning-trained-model"></a>학습된 모델 버전 관리
Azure 기계 학습에서 학습된 된 모델.iLearner 파일로 알려진 형식으로 직렬화 되 고 hello 작업 영역과 연결 된 hello Azure Blob 저장소 계정에 저장 됩니다. 한 가지 방법은 tooget hello.iLearner 파일의 복사본을 hello 재교육 API를 통해 수행 됩니다. [이 문서](machine-learning-retrain-models-programmatically.md) API 재교육 hello 작동 하는 방법을 설명 합니다. hello 상위 수준 단계:

1. 학습 실험을 설정합니다.
2. 웹 서비스 출력 포트 toohello 모델 학습 모듈 또는 모델 Hyperparameter 튜닝 또는 R 모델 만들기와 같은 hello 학습 된 모델을 생성 하는 hello 모듈을 추가 합니다.
3. 학습 실험을 실행한 다음 모델 학습 웹 서비스로 배포합니다.
4. Hello hello 학습 웹 서비스의 끝점 BES 호출할 수 있으며, hello 원하는.iLearner 파일 이름 및 저장 될 Blob 저장소 계정 위치 지정.
5. 수집 생성 hello.iLearner 파일 hello BES 호출을 완료 합니다.

Hello PowerShell commandlet을 통해 다른 방식으로 tooretrieve hello.iLearner 파일은 [ *다운로드 AmlExperimentNodeOutput*](https://github.com/hning86/azuremlps#download-amlexperimentnodeoutput)합니다. 이 려 tooget hello.iLearner의 복사본을 파일 hello 필요 tooretrain hello 모델 없이 프로그래밍 방식으로 보다 쉽게 지정할 수 있습니다.

Hello 학습 된 모델을 포함 하는 hello.iLearner 파일을 설정한 후 다음 버전 관리 전략을 직접 사용할 수 있습니다. hello 전략 명명 규칙으로 전/후 위를 적용 하 고 방금 Blob 저장소의 hello.iLearner 파일을 유지 하거나 복사/가져오기 버전 제어 시스템 처럼 간단할 수 있습니다.

hello 저장된.iLearner 파일 배포 된 웹 서비스를 통해 점수를 매기기 위해 사용할 수 있습니다.

## <a name="versioning-web-service"></a>웹 서비스 버전 관리
Azure Machine Learning 실험에서 두 종류의 웹 서비스를 배포할 수 있습니다. hello 클래식 웹 서비스는 hello 실험 뿐만 아니라 hello 작업 영역 밀접 하 게 관련 됩니다. hello Azure 리소스 관리자 프레임 워크를 사용 하는 hello 새 웹 서비스 및는 더 이상 hello 원래 실험 또는 작업 영역 hello와 연관 되어 없습니다.

### <a name="classic-web-service"></a>클래식 웹 서비스
클래식 웹 서비스 tooversion hello 웹 서비스 끝점 구문 활용을 걸릴 수 있습니다. 일반적인 흐름은 다음과 같습니다.

1. 예측면 실험에서 기본 끝점을 포함하는 새로운 클래식 웹 서비스를 배포할 수 있습니다.
2. 라는 ep2 hello 현재 버전의 hello 실험/학습 모델을 노출 시키는 새로운 끝점을 만듭니다.
3. 다시 이동하여 예측 실험 및 학습된 모델을 업데이트합니다.
4. Hello 기본 끝점을 업데이트 한 다음 하면 hello 예측 실험을 다시 배포 합니다. 하지만 이 작업은 ep2를 변경하지 않습니다.
5. Hello 새로운 버전의 hello 실험 및 학습 된 모델을 노출 시키는 ep3 라는 추가 끝점을 만듭니다.
6. 필요한 경우 toostep 3에 게 이동 합니다.

시간이 지남에 따라 여러 끝점을 만듭니다 해야할 hello에 동일한 웹 서비스입니다. 각 끝점에는 hello 실험 hello 학습 된 모델의 hello 지정 시간 버전이 포함 된 지정 시간 복사본을 나타냅니다. Hello의 버전을 선택 하면 의미 하는 어떤 끝점 toocall hello 점수 매기기 실행에 대 한 모델을 학습 하는 외부 논리 toodetermine를 유도할 수 있습니다.

많은 동일한 웹 서비스 끝점을 만들 수도 있고 서로 다른 버전의 hello.iLearner 파일 toohello 끝점 tooachieve 비슷한 효과 패치 합니다. [이 문서](machine-learning-create-models-and-endpoints-with-powershell.md) 에 대해 더 자세히 설명 어떻게 tooaccomplish입니다.

### <a name="new-web-service"></a>새 웹 서비스
새 Azure 리소스 관리자 기반 웹 서비스를 만드는 경우 hello 끝점 구문은 더 이상 사용할 수 없습니다. Hello를 사용 하 여 예측 실험에서 JSON 형식으로 웹 서비스 정의 (WSD) 파일을 생성할 수는 대신, [내보내기 AmlWebServiceDefinitionFromExperiment](https://github.com/hning86/azuremlps#export-amlwebservicedefinitionfromexperiment) PowerShell commandlet 또는 hello를사용하여[ *내보내기 AzureRmMlWebservice* ](https://msdn.microsoft.com/library/azure/mt767935.aspx) 배포 된 리소스 관리자 기반 웹 서비스에서 PowerShell commandlet 합니다.

Hello 내보낸 후 WSD 파일 및 버전 제어, 다른 Azure 지역의 다른 웹 서비스 계획의 hello WSD 새 웹 서비스로 배포할 수도 있습니다. 서비스 계획의 id입니다. 새로운 웹 구성 뿐 아니라 hello hello 적절 한 저장소 계정을 제공 해야 다른.iLearner 파일에 toopatch, hello WSD 파일을 수정할 수 있습니다 및 학습 hello의 업데이트 hello 위치 참조 모델링 하 고 새 웹 서비스로 배포 합니다.

## <a name="automate-experiment-execution-and-deployment"></a>실험 실행 및 배포 자동화
ALM의 중요 한 측면은 toobe 수 tooautomate hello 실행 및 hello 응용 프로그램의 배포 프로세스 Azure 기계 학습에서이 수행할 수 있습니다 hello를 사용 하 여 [PowerShell 모듈](http://aka.ms/amlps)합니다. 종단 간 단계 hello를 사용 하 여 관련 tooa 표준 ALM 자동화 된 실행/배포 프로세스에의 한 예로 [Azure 컴퓨터 학습 Studio PowerShell 모듈](http://aka.ms/amlps)합니다. 각 단계에는 연결 된 tooone 또는 더 많은 PowerShell commandlet tooaccomplish를 사용할 수 있는 해당 단계입니다.

1. [데이터 집합을 업로드](https://github.com/hning86/azuremlps#upload-amldataset)합니다.
2. 학습 실험에서 hello 작업 영역에 복사는 [작업 영역](https://github.com/hning86/azuremlps#copy-amlexperiment) 또는 [갤러리](https://github.com/hning86/azuremlps#copy-amlexperimentfromgallery), 또는 [가져올](https://github.com/hning86/azuremlps#import-amlexperimentgraph) 는 [내보낸](https://github.com/hning86/azuremlps#export-amlexperimentgraph) 에서 실험 로컬 디스크입니다.
3. [Hello 데이터 집합을 업데이트](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) hello 학습 실험에서 합니다.
4. [Hello 학습 실험을 실행](https://github.com/hning86/azuremlps#start-amlexperiment)합니다.
5. [학습 된 모델 hello 승격](https://github.com/hning86/azuremlps#promote-amltrainedmodel)합니다.
6. [예측 실험 복사](https://github.com/hning86/azuremlps#copy-amlexperiment) hello 작업 영역에 있습니다.
7. [학습 된 모델 업데이트 hello](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) hello 예측 실험에서 합니다.
8. [Hello 예측 실험 실행](https://github.com/hning86/azuremlps#start-amlexperiment)합니다.
9. [웹 서비스를 배포](https://github.com/hning86/azuremlps#new-amlwebservice) hello 예측 실험에서 합니다.
10. Hello 웹 서비스 테스트 [RR](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) 또는 [BES](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint) 끝점입니다.

## <a name="next-steps"></a>다음 단계
* Hello 다운로드 [Azure 컴퓨터 학습 Studio PowerShell](http://aka.ms/amlps) 모듈 및 시작 tooautomate ALM 작업 합니다.
* 너무 방법에 대해 알아봅니다[만들고는 단일 실험에만 사용 하 여 많은 수의 기계 학습 모델을 관리](machine-learning-create-models-and-endpoints-with-powershell.md) 재교육 API 및 PowerShell을 통해.
* [Azure Machine Learning 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)에 대해 자세히 알아봅니다.
