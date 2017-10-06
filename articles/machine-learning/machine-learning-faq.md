---
title: "질문과 대답 (Faq) 기계 학습 aaaAzure | Microsoft Docs"
description: "Azure 기계 학습 소개: 간소화된 예측 모델링에 대한 클라우드 서비스의 요금 청구, 기능 및 제한 사항을 다루는 FAQ."
keywords: "기계 학습 소개, 예측 모델링, 기계 학습이란 무엇인가요"
services: machine-learning
documentationcenter: 
author: garyericson
manager: paulettm
editor: cgronlun
ms.assetid: a4a32a06-dbed-4727-a857-c10da774ce66
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 3af84451dde064c3c9520ee520b541128b1eef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-frequently-asked-questions-billing-capabilities-limitations-and-support"></a>Azure Machine Learning 질문과 대답: 대금 청구, 기능, 제한 사항 및 지원
Azure Machine Learning, 예측 모델 개발을 위한 클라우드 서비스 및 웹 서비스를 통한 운용성 솔루션에 대한 질문(FAQ)과 해당하는 대답입니다. 이 Faq toouse 청구 모델, 기능, 제한 사항 및 지원 hello를 포함 하는 서비스를 hello 하는 방법에 대 한 질문을 제공 합니다.

**여기에서 찾을 수 없는 질문이 있나요?**

Azure 기계 학습 여기서 hello 데이터 과학 커뮤니티의 구성원에 대해 질문할 수 Azure 기계 학습 msdn 포럼을 있습니다. hello Azure 기계 학습 팀 hello 포럼을 모니터링합니다. Toohello 이동 [Azure 컴퓨터 학습 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toosearch toopost 자신만의 새 질문 또는 대답에 대 한 합니다.

## <a name="general-questions"></a>일반적인 질문
**Azure 기계 학습이란 무엇인가요?**

Azure 기계 학습 수 toocreate를 사용 하 여, 테스트, 작동 하는 hello 클라우드에서 예측 분석 솔루션 관리 완벽 하 게 관리 되는 서비스입니다. 브라우저만 있으면 로그인하고 데이터를 업로드하고 즉시 기계 학습 실험을 시작할 수 있습니다. 끌어서 놓기 예측 모델링, 모듈의 대형 팔레트 및 시작 템플릿의 라이브러리를 활용하면 일반적인 기계 학습 작업을 간단히, 빠르게 수행할 수 있습니다. 자세한 내용은 참조 hello [Azure 기계 학습 서비스 개요](https://azure.microsoft.com/services/machine-learning/)합니다. 주요 용어와 개념을 설명 하는 소개 toomachine 학습 참조 [기계 학습 소개 tooAzure](machine-learning-what-is-machine-learning.md)합니다.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**기계 학습 스튜디오란 무엇인가요?**

Machine Learning Studio는 웹 브라우저를 사용하여 액세스하는 워크벤치 환경입니다. 기계 학습 스튜디오의 모듈에는-종단을 작성 하는 데 도움이 되는 시각 컴퍼지션 인터페이스, 데이터 과학 워크플로 실험의 hello 형태로 팔레트를 호스팅합니다.

기계 학습 스튜디오에 대한 자세한 내용은 [기계 학습 스튜디오란 무엇인가요?](machine-learning-what-is-ml-studio.md)

**Hello 컴퓨터 학습 API 서비스는 무엇입니까?**

hello 컴퓨터 학습 API 서비스 확장성, 내결함성 웹 서비스로 기계 학습 스튜디오에 내장 되어 있는 것과 같은 toodeploy 예측 모델이 있습니다. hello 컴퓨터 학습 API 서비스에서 만들어지는 hello 웹 서비스는 외부 응용 프로그램 및 예측 분석 모델 간의 통신에 대 한 인터페이스를 제공 하는 REST Api입니다.

자세한 내용은 참조 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.

**내 클래식 웹 서비스는 어디에 나열되나요? 내 새 Azure Resource Manager 기반 웹 서비스는 어디에 나열되나요?**

Hello 클래식 배포 모델 및 웹 서비스 hello 새 Azure 리소스 관리자 배포 모델을 사용 하 여 만든를 사용 하 여 만든 웹 서비스는 hello에 나열 됩니다 [Microsoft Azure 컴퓨터 학습 웹 서비스](https://services.azureml.net/) 포털입니다.

클래식 웹 서비스에도 나와 [기계 학습 스튜디오](http://studio.azureml.net) hello에 **웹 서비스** 탭 합니다.

## <a name="azure-machine-learning-questions"></a>Azure Machine Learning 질문
**Azure Machine Learning 웹 서비스란?**

Machine Learning 웹 서비스는 응용 프로그램과 Machine Learning 워크플로 점수 매기기 모델 간의 인터페이스를 제공합니다. 외부 응용 프로그램 Azure 기계 학습 toocommunicate 실시간으로 기계 학습 워크플로 점수 매기기 모델 사용 수 있습니다. 호출 tooa 기계 학습 웹 서비스는 예측 결과 tooan 외부 응용 프로그램을 반환합니다. toomake 호출 tooa 웹 서비스는 API 키 hello 웹 서비스를 배포할 때 만들어진를 전달 합니다. Machine Learning 웹 서비스는 웹 프로그래밍 프로젝트에 일반적으로 사용되는 아키텍처인 REST를 기반으로 합니다.

Azure Machine Learning에는 다음 두 가지 유형의 웹 서비스가 있습니다.

* 요청-응답 서비스 (RR): 인터페이스 toohello 상태 비저장 모델을 제공 하는 확장성이 높은 서비스 짧은 대기 시간을 생성 하 고 기계 학습 스튜디오를 사용 하 여 배포 합니다.
* BES(일괄 처리 실행 서비스): 데이터 레코드의 점수를 일괄적으로 매기는 비동기 서비스입니다.

Tooconsume hello REST API 및 액세스 hello 웹 서비스는 여러 가지가. 예를 들어 hello 웹 서비스를 배포할 때 사용자에 대해 생성 되는 hello 샘플 코드를 사용 하 여 C#, R, 또는 Python 응용 프로그램을 작성할 수 있습니다.

hello 샘플 코드에서 제공 됩니다.
- hello 웹 포털에서 서비스의 hello Azure 컴퓨터 학습 웹 서비스에 대 한 hello 사용 페이지
- 기계 학습 스튜디오에서 웹 서비스 대시보드 hello에에서 hello API 도움말 페이지

만들어집니다. 이때 되며 hello 웹 서비스 대시보드에서 기계 학습 스튜디오에서 사용할 수 있는 hello 샘플 Microsoft Excel 통합 문서를 사용할 수 있습니다.

**Hello 주 업데이트 tooAzure 기계 학습 무엇입니까?**

Hello 최신 업데이트에 대 한 참조 [Azure 기계 학습의 새로운 기능](machine-learning-whats-new.md)합니다.

## <a name="machine-learning-studio-questions"></a>기계 학습 스튜디오 질문
### <a name="import-and-export-data-for-machine-learning"></a>Machine Learning에 대한 데이터 가져오기 및 내보내기
**기계 학습에서 지원하는 데이터 원본은 무엇인가요?**

데이터 tooa 세 가지 방법으로 기계 학습 스튜디오 실험을 다운로드할 수 있습니다.

- 데이터 집합으로 로컬 파일 업로드
- 클라우드 데이터 서비스에서 모듈 tooimport 데이터를 사용 하 여
- 다른 실험에서 저장된 데이터 집합 가져오기

지원 되는 파일 형식에 더 알아봅니다 toolearn, 참조 [기계 학습 스튜디오로 학습 데이터를 가져올](machine-learning-data-science-import-data.md)합니다.

#### <a id="ModuleLimit"></a>향 hello 데이터 집합 수 있는 모듈 내에 대 한 무엇입니까?
기계 학습 스튜디오의 모듈 일반적인 사용 사례에 대 한 too10 GB의 조밀한 숫자 데이터를 데이터 집합을 지원 합니다. 모듈은 둘 이상의 입력을 하는 경우 hello 10 g B 값은 hello 모든 입력된 크기의 총 합니다. Hive 또는 Azure SQL Database 쿼리를 사용하여 더 큰 데이터 집합을 샘플링하거나 수집하기 전에 Learning by Counts 전처리를 사용할 수 있습니다.  

hello 다음과 같은 유형의 데이터 기능 정규화 도중 toolarger 데이터 집합 확장 및 10GB 보다 제한 된 tooless 됩니다.

* 스파스
* 범주
* 문자열
* 이진 데이터

다음 모듈 hello 10GB 보다 작은 제한 toodatasets 됩니다.

* Recommender 모듈
* SMOTE(Synthetic Minority Oversampling Technique) 모듈
* Scripting 모듈: R, Python, SQL
* Hello 출력 데이터 크기 모듈 기능 해시 또는 조인 같은 입력된 데이터 크기 보다 클 수 있습니다.
* 교차 유효성 검사, 모델 하이퍼 조정, 서 수 회귀 및-One-vs-all 다중 클래스, hello 수의 반복이 매우 큰 경우

#### <a id="UploadLimit"></a>업로드 하려면 데이터에 대 한 hello 제한 사항은 무엇입니까?
몇 Gb 보다 큰 데이터 집합에 대해 데이터 tooAzure 저장소 또는 Azure SQL 데이터베이스 또는 Azure HDInsight를 사용 하지 않고 업로드 로컬 파일에서 직접 업로드 합니다.

**Amazon S3에서 데이터를 읽을 수 있나요?**

Hello 적은 양의 데이터를 있고 tooexpose를 원하는 경우 사용할 수 있습니다 다음 HTTP URL을 통해 [데이터 가져오기] [ import-data] 모듈입니다. 에 대 한 더 많은 양의 데이터를 전송 하는 데 저장소 tooAzure 먼저 및 hello를 사용 하 여 [데이터 가져오기] [ import-data] 모듈 toobring 실험에 있습니다.
<!--

<SEE CLOUD DS PROCESS>
-->

**기본 제공 이미지 입력 기능이 있나요?**

이미지 입력된 기능 hello에 대 한 학습할 수 있는 [가져오기 이미지] [ image-reader] 참조 합니다.

### <a name="modules"></a>모듈
**hello 알고리즘, 데이터 원본, 데이터 형식 또는 데이터 변환 작업에 대 한 원하는 Azure 기계 학습 스튜디오에 있지 않습니다. 어떻게 해야 하나요?**

Toohello 이동할 수 있습니다 [사용자 피드백 포럼](http://go.microsoft.com/fwlink/?LinkId=404231) toosee 기능은 추적 중인 것을 요청 합니다. 원하는 기능을 이미 요청 된 경우 응답 tooa 요청이 추가 합니다. 찾고 있는 hello 기능이 존재 하지 않는 경우 새 요청을 만듭니다. 이 포럼에 너무 hello 요청 상태를 볼 수 있습니다. 이 목록에 밀접 하 게 추적 하 고 hello 기능 가용성 상태를 자주 업데이트 합니다. 또한 R 및 Python toocreate 사용자 지정 변환을 위해 필요할 때 hello 기본 제공 지원을 사용할 수 있습니다.

**기존 코드를 기계 학습 스튜디오로 가져올 수 있나요?**

예, Azure 기계 학습 학습자를 시험해 동일 하 고 Azure 기계 학습을 통해 웹 서비스로 hello 솔루션을 배포 하는 hello에서 실행 되는 기계 학습 스튜디오에 기존 R, Python 코드를 가져올 수 있습니다. 자세한 내용은 [R을 사용하여 실험 확장](machine-learning-extend-your-experiment-with-r.md) 및 [Azure Machine Learning Studio에서 Python 기계 학습 스크립트 실행](machine-learning-execute-python-scripts.md)을 참조하세요.

**다음과 같은 가능한 toouse은 [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) toodefine 모델?**

아니요, PMML(Predictive Model Markup Language)은 지원되지 않습니다. 사용자 지정 R을 사용할 수 및 Python 코드 toodefine 모듈입니다.

**실험에서 병렬로 실행할 수 있는 모듈은 몇 개인가요?**  

실험에서 병렬로 toofour 모듈을 실행할 수 있습니다.

### <a name="data-processing"></a>데이터 처리
**이 기능 toovisualize 초과 하 여 데이터 (R 시각화) hello 실험에서 대화형으로 있습니까?**

모듈 toovisualize hello 데이터의 hello 출력을 클릭 하 고 통계를 가져옵니다.

**결과 또는 브라우저에서 데이터를 미리 볼 때 hello 행과 열 수가 제한 됩니다. 그 이유는 무엇일까요?**

Tooa 브라우저 많은 양의 데이터를 전송 될 수 있습니다, 때문에 데이터 크기는 기계 학습 스튜디오의 속도가 느려지지 제한 tooprevent입니다. toovisualize 데이터/결과 hello 모든, 더 나은 toodownload 데이터 hello 및 Excel 또는 다른 도구를 사용 합니다.

### <a name="algorithms"></a>알고리즘
**기계 학습 스튜디오에서 지원되는 기존 기계 학습 알고리즘은 무엇인가요?**

Machine Learning Studio는 Microsoft Research에서 개발된 확장 가능한 고급 의사 결정 트리, Bayesian 권장 시스템, 심층적인 신경망, 의사 결정 정글 등 최신 알고리즘을 제공합니다. Vowpal Wabbit과 같은 확장성 있는 오픈 소스 기계 학습 패키지도 포함되어 있습니다. 기계 학습 스튜디오는 여러 클래스의 이진 분류, 회귀 및 클러스터링을 위한 기계 학습 알고리즘을 지원합니다. 전체 목록은 hello 참조 [컴퓨터 학습 모듈][machine-learning-modules]합니다.

**Hello 오른쪽 기계 학습 알고리즘 toouse 내 데이터에 대 한 자동으로 제안 수 있습니까?**

아니요, 하지만 기계 학습 스튜디오의 각 알고리즘 toodetermine toocompare hello 결과 hello 문제에 적합 한 다양 한 방법입니다.

**제공 된 hello 알고리즘에 대 한 다른 하나의 알고리즘 선택에 대 한 모든 지침 있습니까?**

참조 [어떻게 toochoose 알고리즘](machine-learning-algorithm-choice.md)합니다.

**제공 된 hello 알고리즘 R 또는 Python으로 작성 된?**

아니요, 이러한 알고리즘 보다 나은 성능을 가져옵니다 컴파일된 언어 tooprovide 대부분 기록 됩니다.

**한 세부 정보를 제공 하는 hello 알고리즘?**

튜닝에 대 한 매개 변수는 사용에 대 한 설명된 toooptimize hello 알고리즘 및 hello 설명서 hello 알고리즘에 대 한 정보를 제공 합니다.  

**온라인 학습을 지원하나요?**

아니요, 현재는 프로그래밍 방식의 재학습만 지원됩니다.

**기본 제공 모듈 hello를 사용 하 여 Net 신경망 모델의 hello 레이어를 시각화 수 있습니까?**

아니요.

**C# 또는 일부 다른 언어로 모듈을 만들 수 있나요?**

현재 R toocreate 새 사용자 지정 모듈 에서만 사용할 수 있습니다.

### <a name="r-module"></a>R 모듈
**기계 학습 스튜디오에서 사용 가능한 R 패키지는 무엇인가요?**

기계 학습 스튜디오 CRAN R 오늘 패키징하는 400 개 이상의 지원 하며 여기에 hello [현재 목록](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) 모든 패키지를 포함 합니다. 참고: [R 사용 하 여 실험 확장](machine-learning-extend-your-experiment-with-r.md) toolearn 어떻게 tooretrieve이 목록에서 직접 합니다. Hello 패키지를이 목록에 없는 경우 hello에서 hello 패키지의 hello 이름을 제공 [사용자 피드백 포럼](http://go.microsoft.com/fwlink/?LinkId=404231)합니다.

**가능한 toobuild 사용자 지정 R 모듈 입니까?**

예, 자세한 내용은 [Azure 기계 학습에서 사용자 지정 R 모듈 작성](machine-learning-custom-r-modules.md) 을 참조하세요.

**R에 대한 REPL 환경이 있나요?**

아니요, hello studio에서 R에 대 한 읽기-평가-인쇄-루프 (REPL) 환경이 있습니다.

### <a name="python-module"></a>Python 모듈
**사용자 지정 Python 모듈 가능한 toobuild 입니까?**

현재는 하나 이상 사용할 수 있지만 [Python 스크립트 실행] [ python] 모듈 tooget hello 결과가 동일 합니다.

**Python에 대한 REPL 환경이 있나요?**

Hello Jupyter 노트북 기계 학습 스튜디오에서 사용할 수 있습니다. 자세한 내용은 [Azure Machine Learning Studio에 Jupyter 노트북 도입](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)을 참조하세요.

## <a name="web-service"></a>웹 서비스
### <a name="retrain"></a>다시 학습
**Azure Machine Learning 모델 프로그래밍 방식을 다시 학습하려면 어떻게 하나요?**

Api 재교육 hello를 사용 합니다. 자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](machine-learning-retrain-models-programmatically.md)을 참조하세요. 예제 코드는 hello에서 사용할 수 있는 [Microsoft Azure 컴퓨터 학습 재교육 데모](https://azuremlretrain.codeplex.com/)합니다.

### <a name="create"></a>생성
**배포할 수 있습니까 hello 모델에는 인터넷 연결이 없는 응용 프로그램 또는 로컬로?**

아니요.

**모든 웹 서비스에 예상되는 기준 대기 시간이 있나요?**

Hello 참조 [Azure 구독 제한](../azure-subscription-service-limits.md)합니다.

### <a name="use"></a>사용
**경우 표시 하는 toorun 예측 모델 내 요청 응답 서비스와 일괄 처리 실행 서비스?**

요청 응답 서비스 (RR) hello는 낮은 대기 시간, 확장성이 뛰어난 웹 서비스에 사용 되는 tooprovide 인터페이스 toostateless을 모델링 하는 생성 되 고 hello 실험 환경에서 배포 합니다. 일괄 처리 실행 서비스 (BES) hello 데이터 레코드의 일괄 처리를 비동기적으로 점수는 서비스입니다. hello BES에 대 한 입력 등 RR 사용 하 여 데이터 입력입니다. hello 주요 차이점은 BES 다양 한 Azure Blob 저장소, Azure 테이블 저장소, Azure SQL 데이터베이스, HDInsight (하이브 쿼리) 및 HTTP 소스와 같은 원본에서에서 레코드의 블록을 읽습니다. 자세한 내용은 참조 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.

**배포 된 hello 웹 서비스에 대 한 hello 모델을 업데이트 하려면 어떻게 해야 합니까?**

tooupdate 이미 배포 된 서비스에 대 한 예측 모델 수정 및 tooauthor를 사용 하 여 hello 실험을 다시 실행 하 고 hello 학습 된 모델을 저장 합니다. 새 버전의 hello 학습 된 모델을 사용할 수 있으면 기계 학습 스튜디오 묻는 경우 tooupdate 웹 서비스입니다. 자세한 내용은 방법에 대 한 tooupdate 배포 된 웹 서비스 참조 [기계 학습 웹 서비스를 배포](machine-learning-publish-a-machine-learning-web-service.md)합니다.

Hello Retraining Api를 사용할 수 있습니다.
자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](machine-learning-retrain-models-programmatically.md)을 참조하세요. 예제 코드는 hello에서 사용할 수 있는 [Microsoft Azure 컴퓨터 학습 재교육 데모](https://azuremlretrain.codeplex.com/)합니다.

**프로덕션에 배포된 웹 서비스를 모니터링하려면 어떻게 해야 하나요?**

예측 모델을 배포한 후 hello Azure 클래식에서 모니터링할 수 있습니다 (기본 웹 서비스에만 해당) 포털 또는 hello Azure 컴퓨터 학습 웹 서비스 포털입니다. 배포된 각 서비스에는 고유한 대시보드가 있어, 이 대시보드에서 해당 서비스에 대한 모니터링 정보를 볼 수 있습니다. Toomanage 배포 된 웹 서비스를 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 [hello Azure 컴퓨터 학습 웹 서비스 포털을 사용 하 여 웹 서비스 관리](machine-learning-manage-new-webservice.md) 및 [는 Azure 기계 학습 작업 영역을 관리](machine-learning-manage-workspace.md)합니다.

**내 RR/BES의 hello 출력을 어디에서 볼 수 있는 위치는 무엇입니까?**

Rr, hello 웹 서비스 응답은 일반적으로 hello 결과 표시 합니다. 작성할 수도 있습니다 것 tooAzure Blob 저장소입니다. BES, hello 출력 tooa blob 기본적으로 기록 됩니다. Hello를 사용 하 여 hello 출력 tooa 데이터베이스 또는 테이블을 작성할 수도 있습니다 [데이터 내보내기] [ export-data] 모듈입니다.

**Machine Learning Studio에서 만든 모델에서만 웹 서비스를 만들 수 있나요?**

아니요. Jupyter Notebook 및 RStudio를 사용하여 직접 웹 서비스를 만들 수도 있습니다.

**오류 코드에 대한 정보를 어디서 찾을 수 있습니까?**

오류 코드 목록 및 설명은 [Machine Learning 모듈 오류 코드](https://msdn.microsoft.com/library/azure/dn905910.aspx) 를 참조하세요.

## <a name="scalability"></a>확장성
**Hello 웹 서비스의 hello 확장성 이란?**

현재 hello 기본 끝점은 끝점당 동시 RRS 요청을 20으로 프로 비전 됩니다. 끝점, 당이 too200 동시 요청 수를 확장할 수 없으며에 설명 된 대로 각 웹 서비스 too10, 웹 서비스 당 000 끝점을 확장할 수 있습니다 [웹 서비스 크기 조정](machine-learning-scaling-webservice.md)합니다. BES의 경우 각 끝점은 한 번에 40개의 요청을 처리할 수 있으며 40개를 초과하는 추가 요청은 큐에 대기됩니다. 이러한 큐에 대기 중인된 요청 hello 큐 고갈 자동으로 실행 합니다.

**R 작업은 노드 간에 분산되나요?**

번호  

**학습에 사용할 수 있는 데이터의 양은 얼마인가요?**

기계 학습 스튜디오의 모듈 일반적인 사용 사례에 대 한 too10 GB의 조밀한 숫자 데이터를 데이터 집합을 지원 합니다. 모듈을 사용 하는 경우 둘 이상의 입력된을 hello 총 모든 입력에 대 한 크기는 10GB입니다. Hive 쿼리 또는 Azure SQL Database 쿼리를 통하거나 수집 전에 [개수로 알아보기][counts] 모듈로 전처리하여 더 큰 데이터 집합을 샘플링할 수도 있습니다.  

hello 다음과 같은 유형의 데이터 기능 정규화 도중 toolarger 데이터 집합 확장 및 10GB 보다 제한 된 tooless 됩니다.

* 스파스
* 범주
* 문자열
* 이진 데이터

다음 모듈 hello 10GB 보다 작은 제한 toodatasets 됩니다.

* Recommender 모듈
* SMOTE(Synthetic Minority Oversampling Technique) 모듈
* Scripting 모듈: R, Python, SQL
* Hello 출력 데이터 크기 모듈 기능 해시 또는 조인 같은 입력된 데이터 크기 보다 클 수 있습니다.
* Cross-Validate, Tune Model Hyperparameters, Ordinal Regression 및 One-vs-All Multiclass(반복 횟수가 매우 많은 경우)

몇 Gb 보다 큰 데이터 집합에 대해 데이터 tooAzure 저장소 또는 Azure SQL 데이터베이스 또는 HDInsight 사용 하지 않고 업로드 로컬 파일에서 직접 업로드 합니다.

**벡터 크기 제한이 있나요?**

행과 열은 각 제한 toohello.NET 제한인 최대 Int: 2147483647입니다.

**Hello 웹 서비스를 실행 하는 hello 가상 컴퓨터의 hello 크기를 조정할 수 있나요?**

아니요.  

## <a name="security-and-availability"></a>보안 및 사용 가능성
**기본적으로 hello 웹 서비스에 대 한 hello http 끝점에 액세스할 수 있는 사용자? 액세스 toohello 끝점 제한 어떻게 해야 합니까?**

웹 서비스가 배포된 후 해당 서비스에 대한 기본 끝점이 만들어집니다. 해당 API 키를 사용 하 여 hello 기본 끝점을 호출할 수 있습니다. 웹 서비스 관리 Api를 hello hello Azure 클래식 포털에서에서 또는 프로그래밍 방식으로 사용 하 여 고유 키를 가진 더 많은 끝점을 추가할 수 있습니다. 액세스 키 toohello 웹 서비스 필요한 toomake 호출 됩니다. 자세한 내용은 참조 [어떻게 tooconsume Azure 컴퓨터 학습 웹 서비스](machine-learning-consume-web-services.md)합니다.

**내 Azure Storage 계정을 찾을 수 없는 경우 어떻게 되나요?**

기계 학습 스튜디오 hello 워크플로 실행 하는 경우 사용자가 제공한 Azure 저장소 계정 toosave 중간 데이터에 의존 합니다. 이 저장소 계정은 작업 영역을 만들 때 학습 스튜디오 tooMachine 제공 됩니다. Hello 후 작업 영역 경우 생성 됩니다, 작동, hello 작업 영역을 중지할 및 작업 영역 못합니다 한다는 점에서 실험 하는 모든 hello 저장소 계정이 삭제 되 고 더 이상 찾을 수 없습니다.

Hello 저장소 계정이 실수로 삭제 하는 경우 다시 hello hello hello에 이름과 같은 이름을 사용 하는 저장소 계정 hello와 같은 지역의 저장소 계정을 삭제 합니다. 그 후 hello 액세스 키를 다시 동기화 합니다.

**저장소 계정 액세스 키가 동기화되지 않은 경우 어떻게 되나요?**

기계 학습 스튜디오 hello 워크플로 실행 하는 경우 사용자가 제공한 Azure 저장소 계정 toostore 중간 데이터에 의존 합니다. 이 저장소 계정은 hello 액세스 키가 해당 작업 영역과 연결 된 작업 영역을 만들 때 학습 스튜디오 tooMachine 제공 됩니다. Hello 선택 키 hello 작업 영역이 만들어진 후이 변경 되 면 hello 작업 영역 hello 저장소 계정을 더 이상 액세스할 수 없습니다. 작동이 중지되고 해당 작업 영역의 모든 실험이 실패합니다.

저장소 계정 액세스 키를 변경한 경우 hello Azure 클래식 포털을 사용 하 여 hello 작업 영역에서 hello 선택 키를 다시 동기화 합니다.  

## <a name="support-and-training"></a>지원 및 교육
**Azure 기계 학습에 대한 교육은 어디에서 받을 수 있나요?**

hello [Azure 기계 학습 설명서 센터](https://azure.microsoft.com/services/machine-learning/) 비디오 자습서 및 방법 tooguides를 호스팅합니다. 이 단계별 가이드 hello 서비스를 소개 하 고 데이터 가져오기, 데이터 정리, 예측 모델을 작성 및 Azure 기계 학습을 사용 하 여 프로덕션 환경에 배포의 hello 데이터 과학 수명 주기를 설명 합니다.

새로운 재질 toohello 기계 학습 센터를 지속적으로 추가합니다. Hello에 기계 학습 센터에 추가 학습 자료에 대 한 요청을 제출할 수 [사용자 피드백 포럼](https://windowsazure.uservoice.com/forums/257792-machine-learning)합니다.

[Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning)에서 교육을 찾을 수도 있습니다.

**Azure 기계 학습에 대한 지원을 받으려면 어떻게 해야 하나요?**

Azure 기계 학습에 대 한 기술 지원 tooget 너무 이동[Azure 지원](/support/options/)를 선택 하 고 **기계 학습**합니다.

또한 Azure Machine Learning은 MSDN에 커뮤니티 포럼을 갖고 있으며, 여기에서 Azure 기계 학습 관련 질문을 할 수 있습니다. hello Azure 기계 학습 팀 hello 포럼을 모니터링합니다. 너무 이동[Azure 포럼](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning)합니다.

## <a name="billing-questions"></a>대금 청구 관련 질문
**기계 학습 결제는 어떤 방식으로 이루어지나요?**

Azure Machine Learning은 Machine Learning Studio 및 Machine Learning 웹 서비스라는 두 구성 요소로 이루어집니다.

기계 학습 스튜디오를 평가 하는 동안에 hello 무료 청구 계층을 사용할 수 있습니다. 또한 hello 무료 계층 용량이 제한 된 클래식 웹 서비스를 배포할 수 있습니다.

Azure 기계 학습 요구 사항에 맞는에 등록할 수를 결정 한 경우에 표준 계층을 hello 합니다. toosign, Microsoft Azure 구독이 있어야 합니다.

Hello 표준 계층에 요금이 청구 됩니다 매월 기계 학습 스튜디오에서 정의 하는 각 작업 영역에 대 한 합니다. Hello studio의 실험을 실행 하면 청구 됩니다 계산 리소스에 대 한 실험을 실행 하는 경우. 배포 기본 웹 서비스, 트랜잭션 및 hello 선불 단위로 청구 됩니다. 시간을 계산 합니다.

새 Resource Manager 기반 웹 서비스는 비용을 예측할 수 있도록 청구 계획을 적용합니다. 계층화 된 가격 할인된 률 toocustomers 많은 양의 용량에 게 제공 합니다.

계획을 만들 경우에 고정는 포함 된 수량 API 계산 시간 및 트랜잭션 API와 함께 제공 되는 비용 tooa를 커밋합니다. 포함 된 수량 더 필요한 경우에 인스턴스 tooyour 계획을 추가할 수 있습니다. 포함된 수량이 더 많이 필요한 경우 포함된 수량을 훨씬 더 많이 제공하고 할인율이 더 나은 높은 계층 계획을 선택할 수 있습니다.

Hello 포함 된 수량에서 기존 인스턴스는 모두 사용 후 추가적인 사용 대금 청구 계획 계층 hello와 관련 된 hello 초과 속도로 대금이 청구 됩니다.

> [!NOTE]
포함 된 수량 30 일 마다 다시 할당 되 고 사용 하지 않는 포함 된 수량이 월 되지 않습니다 toohello 다음 기간.

추가 대금 청구 및 가격 책정 정보는 [기계 학습 가격](https://azure.microsoft.com/pricing/details/machine-learning/)을 참조하세요.

**Azure 기계 학습의 무료 평가판이 있나요?**

 Azure Machine Learning에는 무료 구독 옵션이 포함되며 이에 대한 내용은 [Machine Learning 가격 책정](https://azure.microsoft.com/pricing/details/machine-learning/)에 설명됩니다. 기계 학습 스튜디오에 너무에 로그인 할 때 제공 되는 8 시간 빠른 평가 평가판[기계 학습 스튜디오](https://studio.azureml.net/?selectAccess=true&o=2)합니다.

 또한 Azure 무료 평가판에 등록하면 한 달 동안 모든 Azure 서비스를 사용해볼 수 있습니다. hello Azure 무료 평가판에 대 한 자세한 toolearn 방문 [Azure 무료 평가판 FAQ](https://azure.microsoft.com/pricing/free-trial-faq/)합니다.

**트랜잭션이란?**

트랜잭션은 Azure Machine Learning이 응답하는 API 호출을 나타냅니다. RRS(요청-응답 서비스) 및 BES(배치 실행 서비스) 호출에서 트랜잭션이 집계되고 청구 계획에 대한 요금으로 부과됩니다.

**에서 사용할 수 있습니까 포함 하는 hello 트랜잭션 수량 계획 RR 및 BES 트랜잭션을 모두에 대 한?**

예, RRS와 BES에서 트랜잭션이 집계되고 청구 계획에 대한 요금으로 부과됩니다.

**API 계산 시간이란?**

API 계산 시간에는 기계 학습을 사용 하 여 API 호출 take toorun 계산 리소스 hello 시간에 대 한 hello 청구 단위입니다. 모든 호출은 청구 목적으로 집계됩니다.

**일반 프로덕션 API 호출은 얼마나 걸리나요?**

프로덕션 API 호출 시간 몇 초를 밀리초 tooa 수백에서 일반적으로 범위의 크게 달라질 수 있습니다. 일부 API 호출 hello 데이터 처리 및 기계 학습 모델의 hello 복잡성에 따라 분이 소요 될 수 있습니다. hello 가장 좋은 방법은 tooestimate 프로덕션 API 호출 toobenchmark hello 서비스 기계 학습에서 모델을가 하는 이유입니다.

**스튜디오 계산 시간이란?**

Studio 계산 시간에는 실험 studio에서 계산 리소스를 사용 하는 hello 집계 시간에 대 한 hello 청구 단위입니다.

**새 서비스 (Azure 리소스 관리자 기반) 웹 서비스의 hello 개발/테스트 계층 의미에 대 한?**

리소스 관리자 기반 웹 서비스를 사용할 수 있는 tooprovision 요금제 다중 계층 제공 합니다. hello 개발/테스트 가격 책정 계층 제공 tootest 할 수 있도록 제한, 즉 포함 된 수량 실험을 웹 서비스로 비용 부담 없이 합니다. 작동 방법 hello 기회 toosee를 해야 합니다.

**저장소 요금은 별도입니까?**

hello 컴퓨터 학습 무료 계층을 요구 또는 별도 저장소 허용 하지 않습니다. hello 컴퓨터 학습 표준 계층 사용자 toohave Azure 저장소 계정이 필요합니다. Azure Storage는 [별도로 청구됩니다](https://azure.microsoft.com/pricing/details/storage/).

**Machine Learning에서 고가용성 작업을 지원하나요?**

예. 자세한 내용은 참조 [컴퓨터 학습 가격](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) 에 대 한 설명은 hello 서비스 수준 계약 (SLA).

**내 프로덕션 API 호출이 실행될 계산 리소스의 구체적인 종류는 무엇인가요?**

hello 기계 학습 서비스는 다중 테 넌 트 서비스입니다. Hello 백 엔드에서 사용 되는 실제 계산 리소스 다 있으며, 성능 및 예측 가능성을 위해 최적화 됩니다.

### <a name="management-of-new-resource-manager-based-web-services"></a>새 Resource Manager 기반 웹 서비스 관리
**계획을 삭제하면 어떻게 되나요?**

구독에서 hello 계획이 제거 되 고 할부 사용에 대 한 요금이 청구 됩니다.

> [!NOTE]
웹 서비스에서 사용하는 계획을 삭제할 수 없습니다. toodelete hello 계획 하거나 할당 해야 새 toohello 웹 서비스를 계획 또는 hello 웹 서비스를 삭제 합니다.

**계획 인스턴스란?**

계획 인스턴스가 단위의 포함 된 수량 tooyour 청구 계획을 추가할 수 있습니다. 청구 계획에 대한 청구 계층을 선택하면 인스턴스 하나와 함께 제공됩니다. 포함 된 수량 더 필요한 경우에 hello 선택한 청구 계층 tooyour 계획의 인스턴스를 추가할 수 있습니다.

**계획 인스턴스를 얼마나 추가할 수 있나요?**

구독에 hello 개발/테스트 가격 책정 계층의 한 인스턴스를 사용할 수 있습니다.

표준 S1, 표준 S2, 표준 S3 계층의 경우 필요한 만큼을 추가할 수 있습니다.

> [!NOTE]
예상된 사용량에 따라 수 수량 포함 더 비용 효율이 tooupgrade tooa 계층 수 대신 인스턴스 toohello 현재 계층을 추가 합니다.

**계획 계층을 변경(업그레이드/다운그레이드)하는 경우 어떻게 되나요?**

현재 사용 현황을 hello 정도 청구 및 hello 이전 계획 삭제 됩니다. Hello 전체 포함 수량이 hello 업그레이드/다운 그레이드 계층의 새 계획 hello 나머지 hello 기간에 대해 만들어집니다.

> [!NOTE]
포함된 수량은 기간당 할당되고 사용하지 않은 수량은 롤오버되지 않습니다.

**계획의 hello 인스턴스를 늘리려면 어떻게 될까요?**

수량 정도 포함 되 고 24 시간 동안 toobe 효과적인 걸릴 수 있습니다.

**계획의 인스턴스를 삭제하면 어떻게 되나요?**

구독에서 hello 인스턴스를 제거 하 고 할부 사용에 대 한 요금이 청구 됩니다.

### <a name="sign-up-for-new-resource-manager-based-web-services-plans"></a>새 Resource Manager 기반 웹 서비스 계획 등록
**계획에 어떻게 등록하나요?**

두 가지 방법 toocreate 청구 계획 해야합니다.

Resource Manager 기반 웹 서비스를 처음 배포할 때 기존 계획을 선택하거나 새 계획을 만들 수 있습니다.

이런이 방식으로 만드는 계획에 해당 기본 지역에 있고 웹 서비스에 배포 된 toothat 영역 됩니다.

기본 지역 이외의 toodeploy 서비스 tooregions를 원하는 경우 toodefine 청구 계획에 서비스를 배포 하기 전에.

이 경우 toohello Azure 컴퓨터 학습 웹 서비스 포털에 로그인 하 고 toohello 계획 페이지를 이동할 수 있습니다. 거기에서 계획을 추가하고 삭제할 수 있을 뿐만 아니라 기존 계획을 수정할 수 있습니다.

**어떤 계획 선택 해야 toostart 해제와**

계층 Standard S1 hello로 시작 하는 하 고 사용에 대 한 서비스를 모니터링할는 것이 좋습니다. 에 포함 된 수량을 신속 하 게 사용 중인 경우 인스턴스를 추가 또는 이동 tooa 더 높은 계층이 가져올 수 할인된 률 더 잘 합니다. 청구 주기 동안 필요에 따라 청구 계획을 조정할 수 있습니다.

**사용할 수 있는 새 계획 hello 있는 지역은 무엇 인가요?**

hello 새 청구 계획 지원 hello 새 웹 서비스는 hello 세 프로덕션 지역에서 사용할 수 있습니다.

* 미국 중남부
* 서유럽
* 동남아시아

**여러 지역에서 웹 서비스를 사용합니다. 모든 지역에 대한 계획이 필요한가요?**

예. 지역에 따라 계획 가격 책정이 달라집니다. Tooassign 필요한 웹 서비스 tooanother 영역을 배포 하는 경우 여기에는 특정 toothat 지역 계획 합니다. 자세한 내용은 [지역별 사용 가능한 제품]( https://azure.microsoft.com/regions/services/)을 참조하세요.

### <a name="new-web-services-overages"></a>새 웹 서비스 - 초과분
**내 웹 서비스 사용량을 초과했는지 어떻게 확인하나요?**

Hello 계획 페이지 hello Azure 컴퓨터 학습 웹 서비스 포털에서 모든 계획 hello 사용량을 볼 수 있습니다. Toohello 포털에 로그인 하 고 클릭 hello **계획** 메뉴 옵션입니다.

Hello에 **트랜잭션을** 및 **계산** hello 테이블의 열을 포함 하는 hello 수량 hello 계획 및 사용 하는 hello 비율을 확인할 수 있습니다.

**Hello를 사용 하는 경우 어떤 일이 생기 hello 개발/테스트 가격 책정 계층에 수량을 포함 하 시겠습니까?**

다음 기간 또는 tooa 유료 계층을 이동할 때까지 서비스에 할당 된 계층 toothem 가격 개발/테스트 hello까지 중지 됩니다.

**클래식 웹 서비스 및 새 Resource Manager 기반 웹 서비스 초과분의 경우 RRS(요청 응답) 및 BES(배치) 워크로드에 대한 가격은 어떻게 계산되나요?**

RR 작업 해야 하는 모든 API 트랜잭션 호출에 대 한 및 이러한 요청을 연관 된 hello 계산 시간에 대 한 요금이 청구 됩니다. Hello 해야 하는 API 호출의 총 수 (개별 트랜잭션에 의해 비례하여 지정) 1, 000 트랜잭션당 hello 가격을 곱한 RR 프로덕션 API 트랜잭션 비용 계산 됩니다. RR API 프로덕션 API 계산 시간 비용이 hello 프로덕션 API 계산 시간 당 hello 가격을 곱한 API 트랜잭션의 총 수를 곱한 각 API 호출 toorun에 필요한 시간의 hello 금액으로 계산 됩니다.

예를 들어 표준 S1 초과 대 한 각 toorun 0.72 초를 사용 하는 API 트랜잭션 1000000 초래 (1000000 * $0.50/1k API 트랜잭션) 프로덕션 API 트랜잭션 비용 및 1000000 * 0.72 초 * $2/hr () 400 달러 프로덕션 API 계산에서 500에서 900 달러의 총 시간입니다.

BES 작업에 대 한 요금이 청구 됩니다 hello에서 동일한 방식으로 합니다. 그러나 hello API 트랜잭션 비용 hello 수가 일괄 처리 작업을 제출 하면 나타내고 hello 계산 비용이 이러한 일괄 처리 작업을 연관 된 hello 계산 시간을 나타냅니다. Hello 제출 된 작업의 총 수 (개별 트랜잭션에 의해 비례하여 지정) 1, 000 트랜잭션당 hello 가격을 곱한 BES 프로덕션 API 트랜잭션 비용 계산 됩니다. 프로덕션 API 계산 시간 BES API 비용이 hello hello 전체 프로덕션 API 당 hello 가격을 곱한 작업 수를 곱한 작업에 있는 행의 총 수를 곱한 작업 toorun 프로그램의 각 행에 필요한 시간의 hello 금액으로 계산 됩니다. 시간을 계산 합니다. 기계 학습 계산기 hello를 사용 하는 경우 hello 트랜잭션 미터 나타냅니다 hello toosubmit, 계획 및 hello 트랜잭션당 시간 필드가 나타내는 hello 작업 조합을 각 작업 toorun의 모든 행에는 데 필요한 시간입니다.

예를 들어 표준 S1 초과분에 대해 각 0.72초가 필요한 행 500개로 구성된 각 작업을 하루에 100개 제출한다고 가정해 보겠습니다. 월간 초과 비용은 프로덕션 API 트랜잭션 비용 $1.55(하루 100개 작업 = 3,100개 작업/1개월 $0.50/1K API 트랜잭션)이며 프로덕션 API 계산 시간은 $620(500행 0.72초 3,100개 작업 $2/시간)로 총 $621.55의 금액이 산정됩니다.

### <a name="azure-machine-learning-classic-web-services"></a>Azure Machine Learning 클래식 웹 서비스
**종량제를 계속 사용할 수 있나요?**

예, 기존 웹 서비스는 Azure Machine Learning에서 계속 사용할 수 있습니다.  

### <a name="azure-machine-learning-free-and-standard-tier"></a>Azure Machine Learning 무료 및 표준 계층
**요소에 포함 된 Azure 컴퓨터 학습 무료 계층 hello?**

hello Azure 컴퓨터 학습 무료 계층은 의도 한 tooprovide 심층 분석 소개 toohello Azure 기계 학습 스튜디오입니다. Microsoft 계정 toosign 된 하기만 하면 최대입니다. hello 무료 계층에 포함 되어 당 무료 액세스 tooone Azure 기계 학습 스튜디오 작업 영역 [Microsoft 계정](https://www.microsoft.com/account/default.aspx)합니다. 이 계층의 too10 g B의 스토리지를 사용할 수 있으며 준비 Api로 모델을 운용 키를 누릅니다. 무료 계층 작업은 SLA의 적용을 받지 않으며 개발 및 개인 용도로만 사용할 수 있습니다. 

무료 계층 작업 영역에는 다음과 같은 제한을 hello

* 작업은 SQL Server를 실행 하는 tooan 온-프레미스 서버를 연결 하 여 데이터를 액세스할 수 없습니다.
* 새 리소스 관리자 기반 웹 서비스를 배포할 수 없습니다.


**Hello Azure 컴퓨터 학습 표준 계층 및 계획에 포함은 무엇입니까?**

hello Azure 컴퓨터 학습 표준 계층은 Azure 기계 학습 스튜디오의 유료 제품 버전입니다. hello Azure 기계 학습 스튜디오에 월별 요금 청구는 작업 영역 당 월 별로 부분 개월에 대 한 계산 및 합니다. Azure Machine Learning 스튜디오 실험 시간은 실제 실험의 계산 시간을 기준으로 요금이 청구됩니다. 요금은 부분 시간별로 일할 계산됩니다.  

hello Azure 컴퓨터 학습 API 서비스는 기본 웹 서비스 또는 새 (리소스 관리자 기반) 웹 서비스 인지에 따라 요금이 청구 됩니다.

구독에 대 한 작업 영역당 hello 요금에 따라 집계 됩니다.

* 컴퓨터 학습 작업 영역 구독이: hello 기계 학습 작업 영역 구독 액세스 tooa 기계 학습 스튜디오 작업 영역을 제공 하는 월 요금입니다. hello 구독은 hello studio 및 tooutilize hello 프로덕션 Api의에서 필수 toorun 실험입니다.
* 스튜디오 실험 시간:이 미터는 기계 학습 스튜디오에서 실험을 실행 하 여 계산 하는 모든 계산 요금을 집계 하 고 hello 스테이징 환경에서에서 실행 중인 프로덕션 API를 호출 합니다.
* 교육에 대 한 모델의 SQL Server를 실행 하는 tooan 온-프레미스 서버를 연결 하 고 점수 매기기 데이터에 액세스 합니다.
* 클래식 웹 서비스의 경우:
  * 프로덕션 API 계산 시간: 이 미터에는 프로덕션에서 실행 중인 웹 서비스로 발생하는 계산 요금이 포함됩니다.
  * 프로덕션 API 트랜잭션 (단위: 1000s):이 미터 호출 tooyour 프로덕션 웹 서비스 당 계산 요금에 포함 됩니다.

Hello 요금, 리소스 관리자 기반 웹 서비스의 hello 대/소문자 앞에는 별도로 청구 금액 집계 toohello 선택한 계획은:

* 표준 S1/S2/S3 API 계획 (단위):이 미터 hello 유형을 리소스 관리자 기반 웹 서비스에 대해 선택 된 인스턴스를 나타냅니다.
* 표준 S1/S2/S3 초과 API 계산 시간:이 미터 기존 인스턴스를 포함 하는 hello 수량 소진 된 후 프로덕션 환경에서 실행 하는 리소스 관리자 기반 웹 서비스에 의해 계산 계산 비용이 포함 됩니다. hello 추가적인 사용 요금이 부과 됩니다 hello overate S3/S2 S1/계획 계층와 관련 된 속도입니다.
* 표준 S1/S2/S3 초과 API 트랜잭션 (단위: 1,000):이 미터 호출 tooyour 프로덕션 hello 기존 인스턴스에 수량을 포함 한 후에 리소스 관리자 기반 웹 서비스 사용 될 당 계산 요금에 포함 됩니다. hello 추가적인 사용 요금이 부과 됩니다 hello overate S3/S2 S1/계획 계층 연관 되는 속도입니다.
* 포함 된 수량 API 계산 시간: 리소스 관리자 기반 웹 서비스와 함께이 미터 hello 포함 된 수량을 API 계산 시간 나타냅니다.
* 수량 API 트랜잭션 (단위: 1,000)에 포함 된: 리소스 관리자와 기반 웹 서비스를이 미터는 hello 포함 된 수량 API 트랜잭션를 나타냅니다.

**Azure Machine Learning 무료 계층에 등록하려면 어떻게 하나요?**

Microsoft 계정만 있으면 됩니다. 너무 이동[Azure 기계 학습 홈](https://azure.microsoft.com/services/machine-learning/), 클릭 하 고 **지금 시작**합니다. Microsoft 계정으로 로그인하면 무료 계층에 작업 영역이 생성됩니다. Tooexplore 시작한 기계 학습 실험은 바로 만들 수 있습니다.

**Azure Machine Learning 표준 계층에 등록하려면 어떻게 하나요?**

있어야 액세스 tooan Azure 구독 toocreate 표준 기계 학습 작업 영역입니다. 30 일 무료 평가판 Azure 구독에 등록할 수 있습니다 및 업그레이드 이후 tooa 유료 Azure 구독 또는 유료 Azure 구독이 완전 한 구입할 수 있습니다. 그런 다음 액세스 toohello 구독을 사용할 수 hello Microsoft Azure 클래식 포털에서 기계 학습 작업 영역을 만들 수 있습니다. 보기 hello [단계별 지침](https://azure.microsoft.com/trial/get-started-machine-learning-b/)합니다.

또는 표준 기계 학습 작업 영역 소유자 tooaccess hello 소유자의 작업 영역에 의해 초대할 수 있습니다.

**Azure Blob 저장소 계정 toouse 나만의 hello 무료 계층으로 지정할 수 있습니까?**

아니요, hello 표준 계층은 hello hello 계층을 도입 하기 전에 제공 했던 기계 학습 서비스의 해당 toohello 버전입니다.

**Hello 무료 계층에서 Api로 모델을 학습 내 컴퓨터를 배포할 수 있습니까?**

운영 화 예, 기계 학습 hello 무료 계층의 일부로 toostaging API 서비스를 모델링 합니다. tooput 준비 API 서비스가 프로덕션 환경에 hello 및 병원 hello 서비스에 대 한 프로덕션 끝점을 가져올 hello 표준 계층을 사용 해야 합니다.

**Azure 무료 평가판 및 Azure 컴퓨터 학습 무료 계층 간의 hello 차이점은 무엇입니까?**

hello [Microsoft Azure 무료 평가판](https://azure.microsoft.com/free/) 크레딧 tooany Azure를 적용할 수 있는 한 달에 대 한 서비스를 제공 합니다. hello Azure 컴퓨터 학습 무료 계층 제공 연속 비-프로덕션 작업에 대 한 기계 학습을 tooAzure 구체적으로 액세스합니다.

**실험 hello 무료 계층 toohello 표준 계층에서 어떻게 이동 합니까?**

toocopy hello 무료 계층 toohello 표준 계층에서 실험:

1. TooAzure 기계 학습 스튜디오에에서 로그인 하 고 무료 작업 영역 hello와 hello 위쪽 탐색 모음에서 작업 영역 선택기 hello에에서 hello 표준 작업 영역을 볼 수 있는지 확인 합니다.
2. Hello 표준 작업 영역에 있는 경우 tooFree 작업 영역을 전환 합니다.
3. Hello 실험 목록 뷰에서 toocopy, 선택한 hello 클릭 실험 선택 **복사** 명령 단추입니다.
4. Hello 대화 상자가 열리면에서 hello 표준 작업 영역을 선택 하 고 클릭 hello **복사** 단추입니다.
   모든 관련된 데이터 집합을 hello, 학습 된 모델 등 hello 실험 hello 표준 작업 영역으로 함께 복사 됩니다.
5. Toorerun 필요한 실험 hello 및 hello 표준 작업 영역에서 웹 서비스를 다시 게시 합니다.

### <a name="studio-workspace"></a>스튜디오 작업 영역
**작업 영역마다 별도의 청구 내역을 볼 수 있습니까?**

작업 영역 요금은 단일 청구서에 해당하는 각 미터로 별도 청구됩니다.

**내 실험을 실행할 구체적인 계산 리소스 종류는 무엇입니까?**

hello 기계 학습 서비스는 다중 테 넌 트 서비스입니다. Hello 백 엔드에서 사용 되는 실제 계산 리소스 다 있으며, 성능 및 예측 가능성을 위해 최적화 됩니다.

### <a name="guest-access"></a>게스트 액세스
**게스트 액세스 tooAzure 기계 학습 스튜디오는 무엇입니까?**

게스트 액세스는 제한적인 체험 서비스입니다. Azure Machine Learning Studio에서 인증 없이 무료로 실험을 만들어 실행할 수 있습니다. 게스트 세션은 비 영구적인 (저장할 수 없습니다) tooeight 시간을 제한 합니다. 또한 R 및 Python이 제대로 지원되지 않고 스테이징 API가 충분하지 않으며 데이터 집합 크기와 저장소 용량도 제한됩니다. 이와 달리 Microsoft 계정으로 toosign 선택 사용자 기계 학습 스튜디오 이전에 설명 하는 영구 작업 영역 및 더 포괄적인 기능을 포함 하는의 모든 권한을 toohello 무료 계층을 갖습니다. toochoose 무료 기계 학습 사용자 경험 클릭 **시작** 에 [https://studio.azureml.net](https://studio.azureml.net)를 선택한 후 **추측 액세스** 또는 Microsoft로 로그인 합니다. 계정입니다.

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
