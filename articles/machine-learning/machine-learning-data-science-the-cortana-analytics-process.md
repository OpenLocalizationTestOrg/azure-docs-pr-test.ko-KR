---
title: "aaaWhat 팀 데이터 과학 프로세스 인가요?  | Microsoft Docs"
description: "hello 팀 데이터 과학 프로세스는 고급 분석 기능을 활용 하는 지능형 응용 프로그램을 구축 하기 위한 체계적인 방법."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a098aa2e-fd79-4543-8e15-9aae9d8b3ee6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: bradsev
ROBOTS: NOINDEX
redirect_url: data-science-process-overview
redirect_document_id: True
ms.openlocfilehash: 57187be9c884389c13c226eab74aff137f5514a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-team-data-science-process-tdsp"></a>Hello 팀 데이터 과학 프로세스 (TDSP) 이란?
hello [팀 데이터 과학 프로세스 (TDSP)](data-science-process-overview.md) hello 필요한 활동의 전체 수명 주기를 통한 데이터 과학자 toocollaborate의 팀을 효과적으로 수 있도록 toobuilding 지능형 응용 프로그램 체계적 접근 방법 제공 tooturn 제품에 이러한 응용 프로그램입니다. 일련의 단계를 제공 하는 hello TDSP에 간략하게 설명 **지침** 에 어떻게 toodefine hello 문제를 hello 도구 설정 및 필요한 환경 관련 데이터를 분석 및 예측 모델을 평가 빌드하고 다음에서 이러한 모델을 배포 엔터프라이즈 응용 프로그램입니다. 

Hello 단계에는 다음과 같습니다 **팀 데이터 과학 프로세스**:  

![CAP-워크플로](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

hello 프로세스는 **반복**:의 새 이해 하 고 기존 hello 또는 hello 모델에 대 한 상세 진화 함에 따라 이루어지며 hello 시퀀스에서 이전에 완료 된 단계를 다시 작업 하도록 합니다. 기존 조직 개발 및 프로젝트 계획 프로세스는 **손쉽게 적용할** toowork hello TDSP 정의 된 일련의 단계를 사용 합니다. 

hello hello 프로세스의 단계는 사실 및 hello에서 연결 된 [TDSP 학습 경로](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 아래에서 설명 하 고 있습니다.  

## <a name="preparation-steps"></a>준비 단계
## <a name="p1-plan-hello-analytics-project"></a>P1. Hello 분석 프로젝트를 계획
비즈니스 목표 및 문제를 정의하여 분석 프로젝트를 시작합니다. 이들을 **비즈니스 요구 사항**측면에서 지정합니다. 이 단계는 중앙 목적은 tooidentify hello 주요 비즈니스 변수 (판매 예측 또는 예를 들어, 사기성이 있는 되 고 순서의 확률 hello) 이러한 요구 사항을 분석 요구 toopredict toosatisfy hello를 사용 하는 것입니다. 추가 계획은 일반적으로 필수 toodevelop hello 이해 한 다음 **데이터 원본** tooaddress 분석 관점에서 hello 프로젝트 목표를 hello 필요 합니다. 일반적을 예를 들어 기존 시스템 toocollect 필요한 및 다른 종류의 데이터 tooaddress 기록할 toofind 문제 hello hello 프로젝트 목표를 달성 합니다. 지침은 [hello 팀 데이터 과학 프로세스에 대 한 환경을 계획](machine-learning-data-science-plan-your-environment.md) 및 [Azure 기계 학습에서 고급 분석에 대 한 시나리오](machine-learning-data-science-plan-sample-scenarios.md)합니다.  

## <a name="p2-setup-analytics-environment"></a>P2. 분석 환경 설정
Hello 팀 데이터 과학 프로세스에 대 한 분석 환경에는 몇 가지 구성 요소가 포함 됩니다. 

* **데이터 작업 영역** hello 데이터를 분석 및 모델링을 위해 준비 하는 경우 
* **처리 인프라** 전처리, 탐색 및 hello 데이터 모델링
* **런타임 인프라** toooperationalize 분석 모델 hello 및 hello 모델을 사용 하는 hello 지능형 클라이언트 응용 프로그램을 실행 합니다.  

hello 분석 인프라 toobe 설치 해야 하는 종종 코어 운영 체제와에서 별개인 환경의 일부입니다. 하지만 일반적으로 데이터 소스 외부 toohello 회사에서 뿐만 아니라 hello 엔터프라이즈 내에서 여러 시스템에서 활용 합니다. 두 개의 온-프레미스 설치 프로그램 또는의 하이브리드 hello 또는 hello 분석 인프라 순수 하 게 클라우드 기반 수 있습니다. 옵션을 참조 하십시오. [hello 팀 데이터 과학 프로세스에서에서 사용 하기 위해 데이터 과학 환경을 설정](machine-learning-data-science-environment-setup.md)합니다.

## <a name="analytics-steps"></a>분석 단계:
## <a name="1-ingest-data-into-hello-analytical-environment"></a>1. Hello 분석 환경으로 데이터 수집
hello 첫 번째 단계 중 하나에서 또는 hello 데이터를 처리할 수 있는 분석 환경으로 외부 hello 엔터프라이즈 내에서 다양 한 소스에서 toobring hello 관련 데이터는입니다. hello **형식** hello의 소스에서 데이터 hello 대상에 필요한 hello 형식에서 다 수 있습니다. 따라서 일부 데이터 변환 hello 수집 도구 수행한 toobe를 가질 수도 있습니다. 옵션에 대해서는 [분석용 저장소 환경에 데이터 로드](machine-learning-data-science-ingest-data.md)

또한 데이터의 초기 수집을 toohello에서 많은 지능형 응용 프로그램은 지속적인 학습 프로세스의 일부로 정기적으로 필요한 toorefresh hello 데이터입니다. **데이터 파이프라인** 또는 워크플로를 설정하여 이 작업을 수행할 수 있습니다. 이 부분에서는 hello 다시 빌드하고 다시 배포 hello 솔루션 hello 지능형 응용 프로그램에서 사용 하는 hello 분석 모델을 평가 포함 하는 hello 프로세스의 반복 부분을 형성 합니다. 예를 들어 참조 [온-프레미스 SQL server tooSQL Azure 데이터 팩터리를 사용 하 여 Azure에서에서 데이터 이동](machine-learning-data-science-move-sql-azure-adf.md)합니다.

## <a name="2-explore-and-pre-process-data"></a>2. 데이터 탐색 및 전처리
hello 다음 단계를 조사 하 여 hello 데이터에 대 한 깊은 이해가 tooobtain는 해당 **요약 통계** , 관계 및 이러한 기술을 사용 하 여 **시각화**합니다. 또한 **데이터 품질** 과, 값 누락, 데이터 형식 불일치, 일관되지 않은 데이터 관계 등의 무결성 문제도 이 단계에서 처리됩니다. 전처리 변환은 추가 분석 하기 전에 hello 원시 데이터를 사용 하는 tooclean 및 모델링을 수행할 수 있습니다. 에 대 한 참조 [작업에 대 한 향상 된 기계 학습 tooprepare 데이터](machine-learning-data-science-prepare-data.md)합니다.

## <a name="3-develop-features"></a>3. 기능 개발
데이터 과학자 도메인 전문가와 공동 작업에 있는 및 hello 데이터 집합의 캡처 hello 관련 된 특정 속성 사용된 toopredict hello 주요 비즈니스 변수 계획 하는 동안 식별을 일 수 있습니다 가장 hello 기능을 식별 해야 합니다. 이러한 새로운 기능이 기존 데이터에서 파생 될 수 나 추가 데이터 toobe 수집 해야 할 수 있습니다. 이 프로세스 라고 **엔지니어링 기능** hello 중 하나는 효과적인 예측 분석 시스템의 주요 단계입니다. 이 단계는 창조적인 과정 조합의 hello 데이터 탐색 단계에서 가져온 도메인 기술력과 hello insights 필요 합니다. 지침은 [hello 데이터 과학 프로세스 팀에서에서 엔지니어링 팀 기능](machine-learning-data-science-create-features.md)합니다.

## <a name="4-create-predictive-models"></a>4. 예측 모델 만들기
데이터 과학자 hello 정리 된 데이터를 사용 하 여 단계 및 들어가지 않고 기능화 계획에 정의 된 hello 비즈니스 요구 사항에 의해 식별 된 toopredict hello 키 변수 분석 모델을 작성 합니다. 컴퓨터 학습 시스템 여러 개 지원 **알고리즘 모델링** 경우 광범위 한 적용 가능한 tooa 됩니다. 지침은 [어떻게 팀 Azure 기계 학습 알고리즘 toochoose](machine-learning-algorithm-choice.md)합니다.

데이터 과학자의 예측 작업에 대 한 hello 가장 적합 한 모델을 선택 해야 하 고 여러 모델의 결과가 결합 toobe tooobtain hello에 대 한 최상의 결과 필요 하며도 드물지 않습니다. hello 모델링에 대 한 입력된 데이터는 일반적으로 임의로 세 부분으로 나뉘어:

* 학습 데이터 집합, 
* 유효성 검사 데이터 집합 
* 테스트 데이터 집합 

hello를 사용 하 여 hello 모델이 생성 된 **학습 데이터 집합**합니다. hello 최적 조합을 조정 매개 변수) (사용 하 여 모델의 선택 hello 모델 실행 hello에 대 한 hello 예측 오류를 측정 하 여 **유효성 검사 데이터 집합**합니다. 마지막으로 hello **테스트 데이터 집합이** 는 독립 된 데이터를 사용 하는 tootrain에 hello 선택한 모델의 사용 되는 tooevaluate hello 성능 또는 hello 모델의 유효성을 검사 합니다.  프로시저 참조 [tooevaluate Azure 기계 학습에서 성능을 모델링 하는 방법을](machine-learning-evaluate-model-performance.md)합니다.

## <a name="5-deploy-and-consume-models"></a>5. 배포 및 사용 모델
될 수 있습니다 잘 수행 하는 모델 집합이 있으면, **병원** 다른 응용 프로그램 tooconsume에 대 한 합니다. Hello 비즈니스 요구 사항에 따라은 예측의 기반이 **실시간으로** 또는 **일괄 처리** 기준입니다. 병원 toobe, hello 모델 toobe로 노출 하는 요소가 **API 인터페이스를 열고** 쉽게 다양 한 응용 프로그램에서 사용 된 이러한 온라인 웹 사이트, 스프레드시트, 대시보드 또는 일련의 비즈니스 및 백 엔드 응용 프로그램입니다. [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.

## <a name="summary-and-next-steps"></a>요약 및 다음 단계
hello [팀 데이터 과학 프로세스](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 일련의 단계를 반복된으로 모델링 됩니다는 **지침을 제공** hello 작업에 필요한 toouse 고급 분석 toobuild는 지능형 응용 프로그램입니다. 또한 각 단계는 다양 한 Microsoft 기술을 toocomplete hello 작업 설명 하는 toouse 방법과에 세부 정보를 제공 합니다. 

TDSP 특정 유형의 규정 하지 않는 동안 **설명서** 아티팩트는 hello 데이터 탐색, 모델링 및 평가, 모범 사례 toodocument hello 결과 및 분석 하는 hello 하므로 toosave hello 관련 코드 필요할 때를 반복할 수 있습니다. 또한 hello 분석 유사한 데이터 및 예측 태스크와 관련 된 다른 응용 프로그램에서 작업할 때 작업을 다시 사용할 수 있습니다.

에 대 한 hello 프로세스의 모든 hello 단계를 보여 주는 종단 간 연습을 전체 **특정 시나리오에 맞춰** 도 제공 됩니다. 예를 들어 다음을 참조하세요.

* [작업에 팀 데이터 과학 프로세스 hello: SQL Server를 사용 하 여](machine-learning-data-science-process-sql-walkthrough.md)
* [작업에 팀 데이터 과학 프로세스 hello: HDInsight Hadoop 클러스터를 사용 하 여](machine-learning-data-science-process-hive-walkthrough.md)합니다.
* [Azure HD.mdnsight에서 Spark를 사용하는 데이터 과학](machine-learning-data-science-spark-overview.md)
* [Azure Data Lake에서 확장성 있는 데이터 과학: 종단 간 연습](machine-learning-data-science-process-data-lake-walkthrough.md)

