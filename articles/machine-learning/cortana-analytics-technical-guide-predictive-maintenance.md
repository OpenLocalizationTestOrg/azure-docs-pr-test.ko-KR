---
title: "azure-Cortana Intelligence 솔루션 기술 가이드 항공 aaaPredictive 유지 보수 | Microsoft Docs"
description: "항공, 유틸리티 및 운송의 예측 유지 관리는 기술 가이드 toohello 솔루션 템플릿을 Microsoft Cortana 정보를 바탕으로 합니다."
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2c4d2147-0f05-4705-8748-9527c2c1f033
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: 30ddc1c101007546ae1b303bccebae3ecdacb442
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>기술 가이드 toohello Cortana Intelligence 솔루션 템플릿을 항공 우주 및 기타 회사의 예측 유지 관리

## <a name="important"></a>**중요**
이 문서는 더 이상 사용되지 않습니다. hello 정보 //www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio toohello 문제와, 즉, 예측 유지 관리, 항공에 있지만 toodate 정보를 가장 hello로 hello 최신 문서를 찾을 수 [여기](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace)합니다. 

## <a name="acknowledgements"></a>**승인**
이 문서는 데이터 과학자 Yan Zhang, Gauher Shaheen, Fidan Boylu Uz 및 Microsoft의 소프트웨어 엔지니어 Dan Grecoe가 작성하였습니다.

## <a name="overview"></a>**개요**
솔루션 서식 파일은 위한 tooaccelerate hello 프로세스의 Cortana 인텔리전스 Suite 맨 위에 E2E 데모를 작성 합니다. 템플릿을 배포는 구독을 필요한 Cortana Intelligence 구성 요소를 프로 비전 하 고 이들 간의 관계 hello를 빌드합니다. 또한 다운로드 하 여 hello 솔루션 템플릿을 배포한 후 로컬 컴퓨터에 설치 하는 데이터 생성기 응용 프로그램에서 생성 된 샘플 데이터로 hello 데이터 파이프라인을 시드합니다. hello 생성기에서 생성 된 hello 데이터 hello 데이터 파이프라인 hydrate 되며 다음 Power BI 대시보드 hello에 시각화할 수 있는 기계 학습 예측 생성을 시작 합니다. hello 배포 프로세스 솔루션 자격 증명을 여러 단계 tooset 과정을 안내 합니다. 이러한 자격 증명 솔루션 이름, username 및 password hello 배포 하는 동안 제공 등을 기록할 수 있는지 확인 합니다.  

hello이 문서의 목적은 tooexplain hello 참조 아키텍처 및이 솔루션 서식 파일의 일부분으로 구독에서 사용자를 프로 비전 하는 다른 구성 요소입니다. 방법에 대 한 hello 문서도 발언 tooreplace toobe 수 toosee insights 및 예측 데이터에서의 실제 데이터로 샘플 데이터. 또한 hello 문서 hello toobe 사용자 고유의 데이터로 toocustomize hello 솔루션을 원하는 경우 수정 해야 하는 솔루션 서식 파일의 부분을 설명 합니다. Toobuild이 솔루션 템플릿은 대 한 Power BI 대시보드를 hello 하는 방법에 대 한 지침 hello 끝에서 제공 됩니다.

> [!TIP]
> [이 문서의 PDF 버전](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf)을 다운로드 및 인쇄할 수 있습니다.
> 
> 

## <a name="big-picture"></a>**큰 그림**
![예측 유지 관리 아키텍처](media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

Cortana 분석 도구 모음 내에서 다양 한 Azure 서비스는 활성화 hello 솔루션이 배포 될 때 (*즉,* 이벤트 허브, 스트림 분석, HDInsight, 데이터 팩터리, 기계 학습 *등*) 위의 hello 아키텍처 다이어그램에 나와 높은 수준에서 끝-예측 유지 관리에 대 한 항공 솔루션 템플릿을 hello 생성 방법입니다. 수 tooinvestigate hello 관련 있는 경우이 서비스 hdinsight hello 예외로 hello 솔루션의 hello 배포를 사용 하 여 만든 hello 솔루션 템플릿 다이어그램에서를 클릭 하 여 hello azure 포털에서 이러한 서비스 필요에 따라 프로 비전 됩니다. 파이프라인 작업이 필요한 toorun 이며 나중에 삭제할.
다운로드할 수 있습니다는 [hello 다이어그램의 전체 크기 버전](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png)합니다.

다음 섹션 hello 각 부분을 설명 합니다.

## <a name="data-source-and-ingestion"></a>**데이터 원본 및 수집**
### <a name="synthetic-data-source"></a>가상 데이터 원본
이 서식 파일 hello 데이터에 대 한 사용 되는 원본 다운로드 되며, 로컬로 배포 된 후 실행 하는 데스크톱 응용 프로그램에서 생성 됩니다. Hello 지침 toodownload 찾을 쿼리하고 hello 솔루션 템플릿 다이어그램에서 예측 유지 관리 데이터 생성기를 호출 하는 hello 첫 번째 노드를 선택할 때 hello 속성 모음에서이 응용 프로그램을 설치 합니다. 이 응용 프로그램 피드 hello [Azure 이벤트 허브](#azure-event-hub) 서비스 데이터 요소 또는 hello 솔루션 흐름의 hello 나머지 부분에 사용 되는 이벤트입니다. 이 데이터 원본으로 구성 되었거나에서 공개적으로 사용할 수 있는 데이터에서 파생 된 [NASA 데이터 리포지토리](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/) hello를 사용 하 여 [Turbofan 엔진 저하 시뮬레이션 데이터 집합](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan)합니다.

컴퓨터에서 실행 하는 동안에 hello 이벤트 생성 응용 프로그램에서는 hello를 Azure 이벤트 허브를 채웁니다.

### <a name="azure-event-hub"></a>Azure 이벤트 허브
hello [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 서비스는 hello 위에서 설명한 통합 데이터 원본에서 제공 하는 hello 입력의 hello 수신자입니다.

## <a name="data-preparation-and-analysis"></a>**데이터 준비 및 분석**
### <a name="azure-stream-analytics"></a>Azure Stream Analytics
hello [Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/) 서비스는 hello에서 입력된 스트림 hello에 대 한 실시간 분석 근처 사용 되는 tooprovide [Azure 이벤트 허브](#azure-event-hub) 에 결과 게시 하 고 서비스는 [Power BI](https://powerbi.microsoft.com) 대시보드도 들어오는 모든 원시 이벤트 toohello 보관 [Azure 저장소](https://azure.microsoft.com/services/storage/) 나중에 처리할 hello 서비스 [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) 서비스입니다.

### <a name="hd-insights-custom-aggregation"></a>HD Insights 사용자 지정 집계
hello Azure HD Insight 서비스는 사용 되는 toorun [하이브](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) hello Azure 스트림 분석 서비스를 사용 하 여 보관 된 하는 hello 원시 이벤트 (Azure Data Factory에 의해 오케스트레이션) 스크립트 tooprovide 집계 합니다.

### <a name="azure-machine-learning"></a>Azure 기계 학습
hello [Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) (Azure Data Factory에 의해 오케스트레이션) 서비스를 사용 하는 hello 연수 (RUL) 받은 hello 입력이 주어진 특정 비행기 엔진의 남은에 toomake 예측 합니다.

## <a name="data-publishing"></a>**데이터 게시**
### <a name="azure-sql-database-service"></a>Azure SQL 데이터베이스 서비스
hello [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/) 서비스는 hello hello에서 소비 될 Azure 기계 학습 서비스에서 받은 (Azure 데이터 팩터리에서 관리 되는) 사용 하는 toostore hello 예측 [Power BI](https://powerbi.microsoft.com) 대시보드 합니다.

## <a name="data-consumption"></a>**데이터 사용량**
### <a name="power-bi"></a>Power BI
hello [Power BI](https://powerbi.microsoft.com) 서비스를 사용 하는 집계 및 hello에서 제공 하는 경고를 포함 하는 대시보드로 tooshow [Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/) 에 저장 된 RUL 예측 뿐만 아니라 서비스 [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/) hello를 사용 하 여 생성 된 [Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) 서비스입니다. Toobuild이 솔루션 서식 파일에 대 한 Power BI 대시보드를 hello 하는 방법에 지침은 아래의 toohello 섹션을 참조 하십시오.

## <a name="how-toobring-in-your-own-data"></a>**어떻게 toobring 자신만 데이터에서**
이 섹션에서는 어떻게 toobring 사용자 고유의 데이터 tooAzure 및 해야 영역 변경한 hello 데이터에 대 한 설명이 아키텍처를 가져옵니다.

가져올 데이터 집합 hello에서 사용 하는 hello 데이터 집합을 일치는 그럴 가능성은 [Turbofan 엔진 저하 시뮬레이션 데이터 집합](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan) 이 솔루션 서식 파일에 사용 합니다. 데이터 및 요구 사항을 이해 사용자 고유의 데이터로이 서식 파일 toowork 수정 방법에서 중요 한 됩니다. Azure 기계 학습 서비스에 첫 번째 노출 toohello 이면 hello 예제에서 사용 하 여 소개 tooit를 가져올 수 있습니다 [어떻게 toocreate 첫 번째 실험](machine-learning-create-experiment.md)합니다.

hello 다음 섹션에서는 새 데이터 집합을 도입 하는 경우 수정 해야 하는 hello 템플릿의 hello 섹션을 설명 합니다.

### <a name="azure-event-hub"></a>Azure Event Hub
hello Azure 이벤트 허브 서비스는 매우 일반적인 등 데이터를 CSV 또는 JSON 형식 toohello 허브 게시할 수 있습니다. Azure 이벤트 허브 hello 공급 되는 hello 데이터를 이해 하는 것이 중요 하지만 없는 특수 한 처리에서 발생 합니다.

이 문서에는 어떻게 tooingest 수 있지만 데이터를 쉽게 보낼 수 이벤트 또는 이벤트 허브 API hello 사용 하 여 데이터 tooan Azure 이벤트 허브 설명 하지 않습니다.

### <a name="azure-stream-analytics"></a>Azure Stream Analytics
hello Azure 스트림 분석 서비스 데이터 스트림을 읽고 원본 tooany 수 데이터를 출력으로 사용 되는 tooprovide 실시간 분석 근처 됨

Azure 스트림 분석 쿼리 hello 항공 솔루션 템플릿에 대 한 예측 유지 관리에 대 한 4 개의 하위 쿼리를 사용 중인 각 이벤트 hello Azure 이벤트 허브 서비스 하 고 출력 4 개의 서로 다른 위치에서 구성 됩니다. 이러한 출력은 세 개의 Power BI 데이터 집합 및 하나의 Azure 저장소 위치로 구성됩니다.

하 여 hello Azure 스트림 분석 쿼리를 찾을 수 있습니다.

* Hello Azure 포털에 로그인
* Hello 스트림 분석 작업 찾기 ![스트림 분석 아이콘](media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png) hello 솔루션 배포 된 경우 만들어졌다는 (*예:*, **maintenancesa02asapbi** 및 **maintenancesa02asablob** 예측 유지 관리 솔루션에 대 한)
* 선택
  
  * ***입력*** tooview hello 쿼리 입력
  * ***쿼리*** tooview hello 쿼리 자체
  * ***출력*** tooview hello 여러 출력

Hello에서 Azure 스트림 분석 쿼리를 생성 하는 방법에 대 한 정보를 확인할 수 있습니다 [스트림 분석 쿼리 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx) msdn 합니다.

이 솔루션에서는 hello 쿼리 hello 들어오는 데이터 스트림에 tooa Power BI 대시보드가 솔루션 서식 파일의 일부로 제공 되는 방법에 대 한 실시간 분석 정보를 거의 세 개의 데이터 집합을 출력 합니다. 이러한 쿼리 변경 toobe 해야 hello 들어오는 데이터 형식에 대 한 암시적 기술 이기 때문에 데이터 형식을 기반으로 합니다.

hello 두 번째 Stream Analytics 작업에서 hello 쿼리 **maintenancesa02asablob** 단순히 모든 출력 [이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 이벤트를 [Azure 저장소](https://azure.microsoft.com/services/storage/) 따라서 없는 변경 필요 hello로 사용자 데이터 형식에 관계 없이 전체 이벤트 정보는 toostorage가 스트리밍됩니다.

### <a name="azure-data-factory"></a>Azure 데이터 팩터리
hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) 서비스 hello 이동 및 데이터의 처리를 조정 합니다. 항공 솔루션 템플릿을 hello 데이터에 대 한 예측 유지 관리에서 팩터리 구성 된 세 개의 [파이프라인](../data-factory/data-factory-create-pipelines.md) 이동 하 고 다양 한 기술을 사용 하 여 hello 데이터를 처리 합니다.  데이터 팩터리 hello 솔루션 템플릿 다이어그램 hello 솔루션의 hello 배포를 사용 하 여 만든 hello 맨 아래에 hello hello Data Factory 노드를 열어 액세스할 수 있습니다. 이렇게 하면 toohello 데이터 팩터리에 Azure 포털에 걸립니다. 데이터 집합 아래에서 오류를 표시 되 면 hello 데이터 생성기를 시작 하기 전에 배포 중인 toodata 팩터리 인해 멤버인 것 무시할 수 있습니다. 이러한 오류가 발생해도 데이터 팩터리가 제대로 작동합니다.

![Data Factory 데이터 집합 오류](media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

이 섹션에서는 hello 필요한 [파이프라인](../data-factory/data-factory-create-pipelines.md) 및 [활동](../data-factory/data-factory-create-pipelines.md) hello에 포함 된 [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)합니다. 다음은 hello 솔루션의 hello 다이어그램 보기입니다.

![Azure 데이터 팩터리](media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

포함이 팩터리의 hello 파이프라인의 두 [하이브](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 스크립트를 사용 하는 toopartition 및 집계 hello 데이터입니다. 설명이 없는 한, hello 스크립트 hello에 배치 됩니다 [Azure 저장소](https://azure.microsoft.com/services/storage/) 설치 과정에서 생성 하는 계정입니다. 해당 위치는 maintenancesascript\\\\script\\\\hive\\\\(또는 https://[Your solution name].blob.core.windows.net/maintenancesascript)입니다.

비슷한 toohello [Azure 스트림 분석](#azure-stream-analytics-1) 쿼리는 [하이브](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) toobe 변경 해야 이러한 쿼리, 스크립트에 hello 들어오는 데이터 형식에 대 한 지식이 암시적 데이터 형식 및 사항에따라[엔지니어링 기능](machine-learning-feature-selection-and-engineering.md) 요구 사항입니다.

#### <a name="aggregateflightinfopipeline"></a>*AggregateFlightInfoPipeline*
이 [파이프라인](../data-factory/data-factory-create-pipelines.md) 단일 활동-를 포함 한 [HDInsightHive](../data-factory/data-factory-hive-activity.md) 사용 하 여 활동을 [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) 를 실행 하는 [하이브](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 스크립트 toopartition hello 데이터 모드로 [Azure 저장소](https://azure.microsoft.com/services/storage/) 중는 [Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/) 작업 합니다.

이 분할 작업에 대한 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 스크립트는 ***AggregateFlightInfo.hql***입니다.

#### <a name="mlscoringpipeline"></a>*MLScoringPipeline*
이 [파이프라인](../data-factory/data-factory-create-pipelines.md) 여러 활동 및 해당 최종 결과 hello에서 예측 점수가 매겨진 hello 포함 [Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) 이 솔루션 템플릿에 연결 된 실험 합니다.

가이에 포함 된 hello 작업입니다.

* [HDInsightHive](../data-factory/data-factory-hive-activity.md) 사용 하 여 활동은 [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) 를 실행 하는 [하이브](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) tooperform 집계를 스크립팅하고 hello에 필요한 엔지니어링 기능 [Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) 시험 합니다.
  이 분할 작업에 대한 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 스크립트는 ***PrepareMLInput.hql***입니다.
* [복사](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello 결과를 이동 하는 활동의 [HDInsightHive](../data-factory/data-factory-hive-activity.md) 단일 활동 tooa [Azure 저장소](https://azure.microsoft.com/services/storage/) 액세스할 수 있는 blob의 [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) 활동입니다.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) hello를 호출 하는 활동 [Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) hello 결과 단일에 보관할 결과적 실험 [Azure 저장소](https://azure.microsoft.com/services/storage/) blob입니다.

#### <a name="copyscoredresultpipeline"></a>*CopyScoredResultPipeline*
이 [파이프라인](../data-factory/data-factory-create-pipelines.md) 단일 활동-를 포함 한 [복사](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello의 hello 결과 이동 하는 활동 [Azure 기계 학습](#azure-machine-learning) 에서 실험는 *** MLScoringPipeline*** toohello [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/) 솔루션 템플릿 설치의 일부로 프로 비전 된입니다.

### <a name="azure-machine-learning"></a>Azure 기계 학습
hello [Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) 실험 사용 되는이 솔루션 템플릿은 제공에 대 한 hello 나머지 유용한 수명 (RUL) 비행기 엔진입니다. hello 실험 특정 toohello 데이터 집합을 사용 하 고 따라서의 상태가 수정 이나 대체 특정 toohello 데이터를 필요 합니다.

Azure 기계 학습 실험 hello를 만드는 방법에 대 한 정보를 참조 하십시오. [예측 유지 관리: 1 / 3, 데이터 준비 및 기능 엔지니어링 단계](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2)합니다.

## <a name="monitor-progress"></a>**진행률 모니터링**
 Hello 데이터 생성기가 시작 되 면 hello 파이프라인 하이드레이션 tooget 차고 hello 솔루션의 다른 구성 요소 시작 hello Data Factory에서 발급 한 다음 hello 명령 실행을 시작한 합니다. 두 가지 방법으로 hello 파이프라인을 모니터링할 수 있습니다.

1. Hello 스트림 분석 작업 중 하나는 hello 원시 들어오는 데이터 tooblob 저장소를 씁니다. Hello 화면에서 솔루션의 Blob 저장소 구성 요소에 대해 하면 성공적으로 배포 된 hello 솔루션 클릭 하 고 hello 오른쪽 패널에서 열기를 클릭 한 다음 이동할 수 toohello [관리 포털](https://portal.azure.com/)합니다. Blob을 클릭합니다. Hello 다음 창에서 컨테이너 목록이 표시 됩니다. **maintenancesadata**를 클릭합니다. Hello hello 다음 패널에 나타납니다 **rawdata** 폴더입니다. Hello rawdata 폴더 안에 시간 처럼 이름 가진 폴더가 나타납니다 = 17, 시간 = 18 등입니다. 이러한 폴더 표시 되 면 것을 의미 hello 원시 데이터가 성공적으로 컴퓨터에 생성 되어 blob 저장소에 저장 합니다. 해당 폴더에 MB의 한정된 크기로 있어야 하는 csv 파일이 표시됩니다.
2. hello hello 파이프라인의 마지막 단계는 SQL 데이터베이스로 toowrite 데이터 (예: 기계 학습에서 예측). Toowait 최대 3 개의 시간 데이터 tooappear hello에 대 한 SQL 데이터베이스에서 할 수 있습니다. 한 가지 방법은 toomonitor 얼마나 많은 데이터를 SQL 데이터베이스에서 사용할 수 있는 방식은 [azure 포털](https://manage.windowsazure.com/)합니다. Hello 왼쪽된 패널에서 SQL 데이터베이스를 찾습니다 ![SQL 아이콘](media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png) 클릭 합니다. 그런 다음 데이터베이스 **pmaintenancedb**를 찾고 클릭합니다. Hello hello 맨 아래에 다음 페이지에서 관리 클릭
   
    ![관리 아이콘](media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png)에서도 확인할 수 있습니다.
   
    여기에서 새 쿼리 및 hello 개수의 행 (예: PMResult에서 선택 그룹)에 대 한 쿼리를 클릭할 수 있습니다. 데이터베이스 크기가 hello hello 테이블의 행 수는 증가 해야 합니다.

## <a name="power-bi-dashboard"></a>**Power BI 대시보드**
### <a name="overview"></a>개요
이 섹션에서는 어떻게 tooset Power BI 대시보드 toovisualize 일괄 처리 예측 뿐만 아니라 Azure 스트림 분석 (실행 부하 과다 경로)에서 실시간으로 데이터에서 결과 설명 Azure 기계 학습 (콜드 경로).

### <a name="setup-cold-path-dashboard"></a>콜드 경로 대시보드 설정
Hello 콜드 경로 데이터 파이프라인에서 hello 필수 목표 비행 (순환) 완료 되 면 tooget 각 비행기 엔진의 예측 RUL (나머지 연수)입니다. hello 예측 결과 있는 동안 완료 된 비행 hello 지난 3 시간 hello 비행기 엔진을 예측 하기 위해 3 시간 마다 업데이트 됩니다.

Power BI를 예측 결과 저장 된 데이터 원본으로 tooan Azure SQL 데이터베이스를 연결 합니다. 참고: 1) 솔루션을 배포 시 한 실제 예측에에서 표시 됩니다 hello 데이터베이스 3 시간 이내입니다.
hello 생성기 다운로드와 함께 제공 된 hello pbix 파일 바로 hello Power BI 대시보드를 만들 수 있도록 일부 데이터를 포함 합니다. 2)이이 단계에서는 hello 필수 구성 요소가 설치 하 고 toodownload hello 무료 소프트웨어 [Power BI desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)합니다.

hello 다음 단계는 안내해 tooconnect hello pbix hello hello 데이터를 포함 하는 솔루션 배포 시 생성 된 SQL 데이터베이스에 파일에 (*예:*합니다. 연결하는 방법을 안내합니다.

1. Hello 데이터베이스 자격 증명을 가져옵니다.
   
   필요한 **데이터베이스 서버 이름, 데이터베이스 이름, 사용자 이름 및 암호** toonext 단계 이동 하기 전에. 다음 hello 단계 tooguide은 있습니다 어떻게 toofind 해당 합니다.
   
   * 솔루션 템플릿 다이어그램의 **"Azure SQL Database"**가 녹색으로 바뀌면 클릭한 다음 **"열기"**를 클릭합니다.
   * 새 브라우저 탭/창을 hello Azure 포털 페이지를 표시 하는 표시 됩니다. 클릭 **'리소스 그룹'** hello 왼쪽된 패널에 있습니다.
   * Hello 솔루션을 배포 하는 데 사용 중인 hello 구독을 선택한 다음 선택 **' YourSolutionName\_ResourceGroup'**합니다.
   * 패널을 새 팝업 hello 클릭 hello ![SQL 아이콘](media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png) 아이콘 tooaccess 데이터베이스입니다. 데이터베이스 이름은 다음 toohello이이 아이콘은 (*예:*, **'pmaintenancedb'**), 및 hello **데이터베이스 서버 이름** hello 서버 name 속성 아래에 있는지와 같아야 합니다 비슷한 너무**YourSoutionName.database.windows.net**합니다.
   * 데이터베이스 **username** 및 **암호** username hello와 동일 hello 및 암호 중 이전에 기록한 hello 솔루션의 배포 합니다.
2. Power BI Desktop으로 hello 콜드 경로 보고서 파일의 hello 데이터 소스를 업데이트 합니다.
   
   * 다운로드 하 여 생성기 파일에 압축을 PC에서 hello 폴더를 두 번 클릭은 **PowerBI\\PredictiveMaintenanceAerospace.pbix** 파일입니다. Hello 파일을 열 때 모든 경고 메시지를 표시 하는 경우 무시 합니다. Hello hello 파일의 위쪽에 클릭 **쿼리 편집 '**합니다.
     
     ![쿼리 편집](media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * 두 개의 테이블, **RemainingUsefulLife** 및 **PMResult**가 표시됩니다. Hello 첫 번째 테이블을 선택 하 고 클릭 ![쿼리 설정 아이콘](media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png) 다음 너무**'Source'** 아래 **' 적용 된 단계 '** hello 오른쪽에 **' 쿼리 설정 '**패널입니다. 표시되는 경고 메시지를 무시합니다.
   * Hello 창 팝아웃, 바꿉니다 **'Server'** 및 **'Database'** 고유한 서버 및 데이터베이스 이름 및 클릭 **'확인'**합니다. 서버 이름에 대 한 지정 했는지 확인 hello 포트 1433 (**YourSoutionName.database.windows.net, 1433**). 으로 hello 데이터베이스 필드를 둡니다 **pmaintenancedb**합니다. Hello 화면에 표시 된 hello 경고 메시지를 무시 합니다.
   * 다음 팝업 창 hello에 hello 왼쪽된 창에서 두 가지 옵션이 표시 됩니다 (**Windows** 및 **데이터베이스**). 클릭 **'Database'**, 입력 프로그램 **'Username'** 및 **'Password'** (이 hello 사용자 이름 및 먼저 hello 솔루션을 배포 하 고 만들 때 입력 한 암호는 Azure SQL 데이터베이스)입니다. ***있는 수준 tooapply 하도록 이러한 설정을 선택***, 데이터베이스 수준 옵션을 선택 합니다. 그런 다음 **'연결'**을 클릭합니다.
   * Hello 두 번째 테이블에서 클릭 **PMResult** 클릭 ![탐색 아이콘](media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png) 다음 너무**'Source'** 아래 **' 적용 된 단계 '** hello 오른쪽에 **' 쿼리 설정 '** 패널 및 hello 서버 및 hello 단계에서 같이 데이터베이스 이름을 업데이트 한 다음 확인을 클릭 합니다.
   * 을 사용 하는 안내 방식된 백 toohello 이전 페이지 되 면 hello 창을 닫습니다. 메시지가 나타나면 **적용**을 클릭합니다. 마지막으로, hello 클릭 **저장** toosave hello 변경 단추입니다. Power BI 파일은 이제 연결 toohello 서버를 설정 합니다. 시각화 비어 있으면 hello 오른쪽 위 모서리의 hello 범례 hello 지우개 아이콘을 클릭 하 여 hello 시각화 toovisualize hello 선택 항목을 hello 데이터를 모두 해제 해야 합니다. Hello 시각화에 hello tooreflect 새 데이터 새로 고침 단추를 사용 합니다. 처음에 표시 됩니다 hello 데이터 시각화에 있는 그대로 hello 데이터 팩터리 예약된 toorefresh 3 시간 마다. 3 시간 후 hello 데이터를 새로 고칠 때 시각화에 반영 하는 새 예측을 확인할 수 있습니다.
3. (선택 사항) Hello 콜드 경로 대시보드를 너무 게시[Power BI 온라인](http://www.powerbi.com/)합니다. 이 단계는 Power BI 계정(또는 Office 365 계정)이 필요합니다.
   
   * 클릭 **[게시]** 몇 초 후는 창이 표시 "게시" tooPower BI 성공! 나타납니다. 창이 나타납니다. "열기 PredictiveMaintenanceAerospace.pbix에서 Power BI" 아래의 hello 링크를 클릭 합니다. toofind 자세한 지침을 참조 [Power BI Desktop에서 게시](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop)합니다.
   * 새 대시보드 toocreate: hello 클릭  **+**  다음 toothe 서명 **대시보드** hello 왼쪽된 창에서 섹션. 이 새 대시보드에 대 한 "예측 유지 관리 데모" hello 이름을 입력 합니다.
   * 클릭 하 여 hello 보고서를 열면 ![고정 아이콘](media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png) toopin 모든 시각화 tooyour 대시보드 합니다. toofind 자세한 지침을 참조 [보고서에서 타일 tooa Power BI 대시보드 고정](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report)합니다.
     Toohello 대시보드 페이지로 이동 하 고 시각화의 hello 크기와 위치를 조정 하 고 직함을 편집 합니다. toofind tooedit 타일을 확인 하려면 어떻게 해야에 대 한 지침을 자세히 [Edit 타일-크기 조정, 이동, 이름 바꾸기, 고정, 삭제, 하이퍼링크 추가](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename)합니다. 일부 콜드 경로 고정 된 시각화 tooit의 예제 대시보드는 다음과 같습니다.  데이터 생성기를 실행 하는 시간에 따라 hello 시각화에에서 번호가 달라질 수 있습니다.
     <br/>
     ![최종 보기](media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * hello 데이터의 새로 고침 tooschedule hello 마우스 포인터로 **PredictiveMaintenanceAerospace** 데이터 집합을 클릭 하 여 ![예제 아이콘](media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png) 선택한 후 **새로 고침 예약**합니다.
     <br/>
     **참고:** 표시를 클릭 하는 경고 마사지 **자격 증명 편집** 데이터베이스 자격 증명 1 단계에서 설명 된 것과 동일한 hello 되 고 있는지 확인 합니다.
     <br/>
     ![새로 고침 예약](media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * Hello 확장 **새로 고침 예약** 섹션. "데이터를 최신 상태로 유지"를 켭니다.
     <br/>
   * 필요에 따라 hello 새로 고침을 예약 합니다. toofind 자세한 내용은 참조 [Power BI에서 데이터 새로 고침](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi)합니다.

### <a name="setup-hot-path-dashboard"></a>실행 부하 과다 경로 대시보드 설정
어떻게 toovisualize 실시간으로 데이터에서에서 출력 스트림 분석 솔루션 배포의 hello 시 생성 된 작업 단계를 수행 하는 hello는 안내 합니다. A [Power BI 온라인](http://www.powerbi.com/) 계정은 필요한 tooperform hello 단계를 수행 합니다. 계정이 없는 경우 [새로 만들](https://powerbi.microsoft.com/pricing)수 있습니다.

1. Azure 스트림 분석(ASA)에 Power BI 출력을 추가합니다.
   
   * 지침에 toofollow hello 해야 [Azure Stream Analytics 및 Power BI: 스트리밍 데이터의 실시간 표시 여부에 대 한 실시간 분석 대시보드](../stream-analytics/stream-analytics-power-bi-dashboard.md) tooset Power로 Azure 스트림 분석 작업의 hello 출력을 BI 대시보드입니다.
   * hello ASA 쿼리가 3 개의 출력이 있는 **aircraftmonitor**, **aircraftalert**, 및 **flightsbyhour**합니다. 쿼리 탭을 클릭 하 여 hello 쿼리를 볼 수 있습니다. 해당 tooeach 이러한 테이블의 출력 tooASA tooadd 필요 합니다. Hello 첫 번째 출력을 추가 하는 경우 (*예:* **aircraftmonitor**) 되었는지 hello 확인 **출력 별칭**, **데이터 집합 이름** 및  **테이블 이름** 동일 hello 됩니다 (**aircraftmonitor**). 에 대 한 반복 hello 단계 tooadd 출력 **aircraftalert**, 및 **flightsbyhour**합니다. 확인 메시지를 받아야 테이블을 출력 하 고 hello ASA 작업으로 시작 세 개 모두가 추가 하면 (*예:*, "시작 Stream Analytics maintenancesa02asapbi 성공한 작업 하는 데 사용").
2. 로그 너무[Power BI 온라인](http://www.powerbi.com)
   
   * Hello 내 작업 영역에서 왼쪽 패널 데이터 집합 구역에는 ***DATASET*** 이름 **aircraftmonitor**, **aircraftalert**, 및 **flightsbyhour**표시 되어야 합니다. 이 스트리밍 데이터 hello 이전 step.hello 데이터 집합에서 Azure 스트림 분석에서 푸시 hello **flightsbyhour** hello에 표시 되지 않을 수 있습니다 hello hello SQL 쿼리를의 toohello 특성 때문에 두 개의 다른 데이터 집합으로 동일한 시간 것입니다. 그러나 한 시간 후에 표시됩니다.
   * 있는지 hello 확인 ***시각화*** 창 열려 있고 hello 화면 오른쪽에 표시 됩니다.
3. Power BI로 흐르는 hello 데이터를 만든 후 hello 스트리밍 데이터 시각화를 시작할 수 있습니다. 아래 몇 가지 실행 부하 과다 경로 시각화가 포함 된 예제 대시보드 고정 tooit는입니다. 적절한 데이터 집합에 따라 다른 대시보드 타일을 만들 수 있습니다. 데이터 생성기를 실행 하는 시간에 따라 hello 시각화에에서 번호가 달라질 수 있습니다.

    ![대시보드 보기](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. 다음은 몇 가지 단계 toocreate 위의 – hello 타일 중 하나 hello "센서 11 vs 함 대 보기입니다. 임계값 48.26” 타일:
   
   * 데이터 집합 클릭 **aircraftmonitor** hello 왼쪽 패널 데이터 집합 섹션에 있습니다.
   * Hello 클릭 **꺾은선형 차트** 아이콘입니다.
   * 클릭 **Processed** hello에 **필드** 창 표시 된다는 "축" hello에 있도록 **시각화** 창.
   * "값" 아래에 모두 표시되도록 "s11" 및 "s11\_alert"을 클릭합니다. 다음 너무 hello 작은 화살표를 클릭**s11** 및 **s11\_경고**, "Sum" 변경 "평균" 너무 합니다.
   * 클릭 **저장** 위쪽 hello 되 고 hello 보고서 "aircraftmonitor"의 이름을 지정 합니다. "Aircraftmonitor" 라는 보고서 hello에 표시 될 **보고서** hello 섹션인 **탐색기** hello 왼쪽 창.
   * Hello 클릭 **Pin Visual** hello의 오른쪽 위 모서리가 꺾은선형 차트에서 아이콘입니다. 대시보드를 선택할 수 있습니다 "Pin tooDashboard" 창 표시 될 수 있습니다. "예측 유지 관리 데모"를 선택한 다음 "고정"을 클릭합니다.
   * 이 타일 hello 대시보드에서 hello 마우스 위로 아이콘을 클릭 hello "edit" hello 오른쪽 위 모서리 toochange에 제목 너무 "센서 11의 Fleet 보기 vs. 임계값이 48.26"및 부제목 너무"평균 시간이 지남에 따라 fleet 걸쳐"입니다.

## <a name="how-toodelete-your-solution"></a>**어떻게 toodelete 솔루션**
중이지 않은 비용이 더 많이 부과할 hello 데이터 생성기를 실행 하는 대로 hello 솔루션을 사용 하는 경우 hello 데이터 생성기를 중지 하는 확인 하십시오. 사용 하지 않는 경우 hello 솔루션을 삭제 하십시오. 솔루션을 삭제 하면 hello 솔루션을 배포할 때 구독에 사용자를 프로 비전 hello 구성 요소를 모두 삭제 됩니다. toodelete hello 솔루션 hello hello 솔루션 템플릿의 왼쪽된 창에서 솔루션 이름을 클릭 하 고 삭제를 클릭 합니다.

## <a name="cost-estimation-tools"></a>**비용 예측 도구**
hello 다음 두 가지 도구를 사용할 수 있는 toohelp 항공 솔루션 템플릿에 대 한 구독에서 hello 예측 유지 관리를 실행 하는 데 필요한 총 비용을 더 잘 이해:

* [Microsoft Azure 비용 추정 도구(온라인)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure 비용 추정 도구(데스크톱)](http://www.microsoft.com/download/details.aspx?id=43376)

