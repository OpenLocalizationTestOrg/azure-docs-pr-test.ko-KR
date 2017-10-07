---
title: "에너지 기술 가이드에는 예측 aaaDemand | Microsoft Docs"
description: "에너지의 예측 요청에 대 한는 기술 가이드 toohello 솔루션 템플릿을 Microsoft Cortana 정보를 바탕으로 합니다."
services: cortana-analytics
documentationcenter: 
author: yijichen
manager: ilanr9
editor: yijichen
ms.assetid: 7f1a866b-79b7-4b97-ae3e-bc6bebe8c756
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: inqiu;yijichen;ilanr9
ms.openlocfilehash: c97b7c19c9e3a317aecc329e61a0692d2f1ec53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-demand-forecast-in-energy"></a>에너지의 예측 요청에 대 한 기술 가이드 toohello Cortana Intelligence 솔루션 템플릿
## <a name="overview"></a>**개요**
솔루션 서식 파일은 위한 tooaccelerate hello 프로세스의 Cortana 인텔리전스 Suite 맨 위에 E2E 데모를 작성 합니다. 템플릿을 배포는 구독을 필요한 Cortana Intelligence 구성 요소를 프로 비전 하 고 hello 관계를 빌드합니다. 또한 데이터 시뮬레이션 응용 프로그램에서 생성 하는 예제 데이터로 hello 데이터 파이프라인을 시드합니다. Hello 데이터 시뮬레이터 hello에 제공 된 링크에서 다운로드 하 고 로컬 컴퓨터에 설치 hello 시뮬레이터를 사용 하 여에 대 한 toohello readme.txt 파일을 참조 하세요. Hello 시뮬레이터에서 생성 된 데이터는 hello 데이터 파이프라인 및 다음 hello Power BI 대시보드에 시각화할 수 있는 컴퓨터 학습 예측을 생성 하는 시작 hydrate 됩니다.

hello 솔루션 템플릿을 찾을 수 [여기](https://gallery.cortanaintelligence.com/SolutionTemplate/Demand-Forecasting-for-Energy-1)

hello 배포 프로세스 솔루션 자격 증명을 여러 단계 tooset 과정을 안내 합니다. 이러한 자격 증명 솔루션 이름, username 및 password hello 배포 하는 동안 제공 등을 기록할 수 있는지 확인 합니다.

hello이 문서의 목적은 tooexplain hello 참조 아키텍처 및이 솔루션 서식 파일의 일부분으로 구독에서 사용자를 프로 비전 하는 다른 구성 요소입니다. hello 문서도 어떻게 tooreplace hello 고유한 toobe 수 toosee insights/예측 데이터를이 사용자의 실제 데이터와 함께 샘플 데이터에 대해 소개 합니다. 또한 hello 문서는 방법에 대해 hello toobe 사용자 고유의 데이터로 toocustomize hello 솔루션을 원하는 경우 수정 해야 하는 솔루션 템플릿을의 hello 부분입니다. Toobuild이 솔루션 템플릿은 대 한 Power BI 대시보드를 hello 하는 방법에 대 한 지침 hello 끝에서 제공 됩니다.

## <a name="big-picture"></a>**큰 그림**
![](media/cortana-analytics-technical-guide-demand-forecast/ca-topologies-energy-forecasting.png)

### <a name="architecture-explained"></a>아키텍처 설명
Cortana 분석 도구 모음 내에서 다양 한 Azure 서비스는 활성화 hello 솔루션이 배포 될 때 (*즉,* 이벤트 허브, 스트림 분석, HDInsight, 데이터 팩터리, 기계 학습 *등*) 위의 hello 아키텍처 다이어그램에 나와 상위 수준에서 종단 간 솔루션 템플릿을 에너지에 대 한 수요를 예측 하는 hello 생성 방법입니다. 이러한 서비스를 클릭 하 여 hello hello 솔루션의 hello 배포를 사용 하 여 만든 솔루션 템플릿을 다이어그램 수 tooinvestigate 됩니다. 다음 섹션 hello 각 부분을 설명 합니다.

## <a name="data-source-and-ingestion"></a>**데이터 원본 및 수집**
### <a name="synthetic-data-source"></a>가상 데이터 원본
이 서식 파일 hello 데이터에 대 한 사용 되는 원본 다운로드 되며, 로컬로 배포 된 후 실행 하는 데스크톱 응용 프로그램에서 생성 됩니다. Hello 지침 toodownload 찾 및 예측 데이터 시뮬레이터 에너지 hello 솔루션 템플릿 다이어그램에서 호출 하는 hello 첫 번째 노드를 선택할 때 hello 속성 모음에서이 응용 프로그램을 설치 합니다. 이 응용 프로그램 피드 hello [Azure 이벤트 허브](#azure-event-hub) 서비스 데이터 요소 또는 hello 솔루션 흐름의 hello 나머지 부분에 사용 되는 이벤트입니다.

컴퓨터에서 실행 하는 동안에 hello 이벤트 생성 응용 프로그램에서는 hello를 Azure 이벤트 허브를 채웁니다.

### <a name="azure-event-hub"></a>Azure Event Hub
hello [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 서비스는 hello 위에서 설명한 통합 데이터 원본에서 제공 하는 hello 입력의 hello 수신자입니다.

## <a name="data-preparation-and-analysis"></a>**데이터 준비 및 분석**
### <a name="azure-stream-analytics"></a>Azure Stream Analytics
hello [Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/) 서비스는 hello에서 입력된 스트림 hello에 대 한 실시간 분석 근처 사용 되는 tooprovide [Azure 이벤트 허브](#azure-event-hub) 에 결과 게시 하 고 서비스는 [Power BI](https://powerbi.microsoft.com) 대시보드도 들어오는 모든 원시 이벤트 toohello 보관 [Azure 저장소](https://azure.microsoft.com/services/storage/) 나중에 처리할 hello 서비스 [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) 서비스입니다.

### <a name="hd-insights-custom-aggregation"></a>HD Insights 사용자 지정 집계
hello Azure HD Insight 서비스는 사용 되는 toorun [하이브](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) hello Azure 스트림 분석 서비스를 사용 하 여 보관 된 하는 hello 원시 이벤트 (Azure Data Factory에 의해 오케스트레이션) 스크립트 tooprovide 집계 합니다.

### <a name="azure-machine-learning"></a>Azure 기계 학습
hello [Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) (Azure Data Factory에 의해 오케스트레이션) 서비스를 사용 하는 toomake 수신 hello 입력이 주어진 특정 지역의 향후 전력 소비를 예측 합니다.

## <a name="data-publishing"></a>**데이터 게시**
### <a name="azure-sql-database-service"></a>Azure SQL 데이터베이스 서비스
hello [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/) 서비스는 hello hello에서 소비 될 Azure 기계 학습 서비스에서 받은 (Azure 데이터 팩터리에서 관리 되는) 사용 하는 toostore hello 예측 [Power BI](https://powerbi.microsoft.com) 대시보드 합니다.

## <a name="data-consumption"></a>**데이터 사용량**
### <a name="power-bi"></a>Power BI
hello [Power BI](https://powerbi.microsoft.com) 서비스를 사용 하는 tooshow hello에서 제공 하는 집계를 포함 하는 대시보드로 [Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/) 요청 뿐 아니라 서비스에 저장 된 결과 예측 [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/) hello를 사용 하 여 생성 된 [Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) 서비스입니다. Toobuild이 솔루션 서식 파일에 대 한 Power BI 대시보드를 hello 하는 방법에 지침은 아래의 toohello 섹션을 참조 하십시오.

## <a name="how-toobring-in-your-own-data"></a>**어떻게 toobring 자신만 데이터에서**
이 섹션에서는 어떻게 toobring 사용자 고유의 데이터 tooAzure 및 해야 영역 변경한 hello 데이터에 대 한 설명이 아키텍처를 가져옵니다.

그럴 가능성은 가져오는 모든 데이터 집합이 솔루션 서식 파일에 사용 되는 hello 데이터 집합을 일치 합니다. 데이터 및 요구 사항을 이해 사용자 고유의 데이터로이 서식 파일 toowork 수정 방법에서 중요 한 됩니다. Azure 기계 학습 서비스에 첫 번째 노출 toohello 이면 hello 예제에서 사용 하 여 소개 tooit를 가져올 수 있습니다 [어떻게 toocreate 첫 번째 실험](machine-learning/machine-learning-create-experiment.md)합니다.

hello 다음 섹션에서는 새 데이터 집합을 도입 하는 경우 수정 해야 하는 hello 템플릿의 hello 섹션을 설명 합니다.

### <a name="azure-event-hub"></a>Azure Event Hub
hello [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 서비스는 매우 일반적인 등 데이터를 CSV 또는 JSON 형식 toohello 허브 게시할 수 있습니다. 공급 되는 hello 데이터 확인이 중요 하지만 없는 특수 한 처리 hello Azure 이벤트 허브에서에서 발생 합니다.

이 문서 tooingest 이지만 데이터를 보낼 수 있는 방법을 쉽게 이벤트 또는 데이터 tooan Azure 이벤트 허브 설명 하지 않으면 hello를 사용 하 여 [이벤트 허브 API](event-hubs/event-hubs-programming-guide.md)합니다.

### <a name="azure-stream-analytics"></a>Azure Stream Analytics
hello [Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/) 고 서비스를 사용 하는 tooprovide 실시간 분석 근처 데이터 스트림에서 읽기 원본 tooany 수 데이터를 출력 하는 중입니다.

에너지 솔루션 템플릿에 대 한 수요를 예측 하는 hello에 대 한 hello Azure 스트림 분석 쿼리는 각 입력으로 hello Azure 이벤트 허브 서비스에서에서 이벤트를 사용 하 고 출력 tootwo 위치에 있는 두 개의 하위 쿼리 구성 됩니다. 이러한 출력은 하나의 Power BI 데이터 집합 및 하나의 Azure 저장소 위치로 구성됩니다.

hello [Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/) 여 쿼리를 찾을 수 있습니다.

* Hello에 로그인 할 [Azure 관리 포털](https://manage.windowsazure.com/)
* Hello 스트림 분석 작업 찾기 ![](media/cortana-analytics-technical-guide-demand-forecast/icon-stream-analytics.png) hello 솔루션 배포 된 경우 생성 된입니다. 하나 데이터 tooblob 저장소 (예: mytest1streaming432822asablob) 밀어 넣는 이며 다른 하나는 데이터 tooPower (예: mytest1streaming432822asapbi) BI를 밀어 넣는 hello.
* 선택

  * ***입력*** tooview hello 쿼리 입력
  * ***쿼리*** tooview hello 쿼리 자체
  * ***출력*** tooview hello 여러 출력

Hello에서 Azure 스트림 분석 쿼리를 생성 하는 방법에 대 한 정보를 확인할 수 있습니다 [스트림 분석 쿼리 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx) msdn 합니다.

이 솔루션에서는 hello hello 들어오는 데이터 스트림에 tooa Power BI 대시보드에 대 한 실시간 분석 정보를 거의 포함 된 데이터 집합은이 솔루션 서식 파일의 일부로 제공 되는 출력 하는 Azure 스트림 분석 작업 합니다. 이러한 쿼리 변경 toobe 해야 hello 들어오는 데이터 형식에 대 한 암시적 기술 이기 때문에 데이터 형식을 기반으로 합니다.

hello 다른 Azure 스트림 분석 작업에서 출력 모든 [이벤트 허브](https://azure.microsoft.com/services/event-hubs/) 이벤트를 [Azure 저장소](https://azure.microsoft.com/services/storage/) 따라서 hello 전체 이벤트 정보는 스트리밍됩니다 데이터 형식에 관계 없이 변경 되지 않아야 하 고 toostorage 합니다.

### <a name="azure-data-factory"></a>Azure 데이터 팩터리
hello [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) 서비스 hello 이동 및 데이터의 처리를 조정 합니다. 에너지 솔루션 템플릿을 hello 데이터에 대 한 수요 예측 hello에서 팩터리 이루어진 12 [파이프라인](data-factory/data-factory-create-pipelines.md) 이동 하 고 다양 한 기술을 사용 하 여 hello 데이터를 처리 합니다.

  데이터 팩터리 hello 솔루션 템플릿 다이어그램 hello 솔루션의 hello 배포를 사용 하 여 만든 hello 맨 아래에 hello Data Factory 노드를 열어 액세스할 수 있습니다. 이렇게 하면 toohello 데이터 팩터리에 Azure 관리 포털에 걸립니다. 데이터 집합 아래에서 오류를 표시 되 면 hello 데이터 생성기를 시작 하기 전에 배포 중인 toodata 팩터리 인해 멤버인 것 무시할 수 있습니다. 이러한 오류가 발생해도 데이터 팩터리가 제대로 작동합니다.

이 섹션에서는 hello 필요한 [파이프라인](data-factory/data-factory-create-pipelines.md) 및 [활동](data-factory/data-factory-create-pipelines.md) hello에 포함 된 [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)합니다. 다음은 hello 솔루션의 hello 다이어그램 보기입니다.

![](media/cortana-analytics-technical-guide-demand-forecast/ADF2.png)

이 팩터리의 hello 파이프라인 중 5 개 포함 [하이브](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 스크립트를 사용 하는 toopartition 및 집계 hello 데이터입니다. 설명이 없는 한, hello 스크립트 hello에 배치 됩니다 [Azure 저장소](https://azure.microsoft.com/services/storage/) 설치 과정에서 생성 하는 계정입니다. 해당 위치는 demandforecasting\\\\script\\\\hive\\\\(또는 https://[솔루션 이름].blob.core.windows.net/demandforecasting)입니다.

비슷한 toohello [Azure 스트림 분석](#azure-stream-analytics-1) 쿼리는 [하이브](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) toobe 변경 해야 이러한 쿼리, 스크립트에 hello 들어오는 데이터 형식에 대 한 지식이 암시적 데이터 형식 및 사항에따라[엔지니어링 기능](machine-learning/machine-learning-feature-selection-and-engineering.md) 요구 사항입니다.

#### <a name="aggregatedemanddatato1hrpipeline"></a>*AggregateDemandDataTo1HrPipeline*
이 [파이프라인](data-factory/data-factory-create-pipelines.md) 단일 활동-파이프라인에 포함 된 프로그램 [HDInsightHive](data-factory/data-factory-hive-activity.md) 사용 하 여 활동을 [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) 를 실행 하는 [하이브](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)스크립트 tooaggregate hello 10 초 마다 변전소 수준 toohourly 지역 수준에서 데이터 요청에에서 스트리밍에 넣은 [Azure 저장소](https://azure.microsoft.com/services/storage/) hello Azure 스트림 분석 작업을 통해.

이 분할 작업에 대한 [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 스크립트는 ***AggregateDemandRegion1Hr.hql***입니다.

#### <a name="loadhistorydemanddatapipeline"></a>*LoadHistoryDemandDataPipeline*
이 [파이프라인](data-factory/data-factory-create-pipelines.md)은 다음 두 작업을 포함합니다.

* [HDInsightHive](data-factory/data-factory-hive-activity.md) 사용 하 여 활동을 [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) 하이브 스크립트를 실행 하 tooaggregate hello 시간별 기록 요청 데이터를 변전소 수준 toohourly 지역 수준 hello Azure 중 Azure 저장소에 적용 합니다. 스트림 분석 작업
* [복사](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello를 이동 하는 활동 Azure 저장소 blob toohello hello 솔루션 템플릿 설치의 일부로 프로 비전 된 Azure SQL 데이터베이스에서에서 데이터를 집계 합니다.

hello [하이브](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) 이 작업에 대 한 스크립트 ***AggregateDemandHistoryRegion.hql***합니다.

#### <a name="mlscoringregionxpipeline"></a>*MLScoringRegionXPipeline*
이러한 [파이프라인](data-factory/data-factory-create-pipelines.md) 여러 활동을 포함 하 고 최종 결과인 hello 점수는이 솔루션 템플릿에 연결 된 hello Azure 기계 학습 실험에서 예측 합니다. 각각의 다른 RegionID 각 지역에 대 한 hello ADF 파이프라인과 hello 하이브 스크립트에 전달 하 여 수행 되는 hello 다른 지역 처리 점을 제외 하 고 거의 동일 합니다.  
가이에 포함 된 hello 작업입니다.

* [HDInsightHive](data-factory/data-factory-hive-activity.md) 사용 하 여 활동을 [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) 하이브 스크립트를 실행 하 tooperform 집계 hello Azure 기계 학습 실험에 필요한 엔지니어링 기능입니다. hello이 작업에 대 한 하이브 스크립트는 해당 ***PrepareMLInputRegionX.hql***합니다.
* [복사](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello에서 hello 결과 이동 하는 활동 [HDInsightHive](data-factory/data-factory-hive-activity.md) 활동 tooa 단일 Azure 저장소 blob hello 액세스할 수 있는 [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) 활동입니다.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) hello 결과적 hello Azure 기계 학습 실험을 호출 하는 작업을 단일 Azure 저장소 blob에 보관할가 발생 합니다.

#### <a name="copyscoredresultregionxpipeline"></a>*CopyScoredResultRegionXPipeline*
이러한 [파이프라인](data-factory/data-factory-create-pipelines.md) 단일 활동-를 포함 한 [복사](https://msdn.microsoft.com/library/azure/dn835035.aspx) 각각 hello에서 hello Azure 기계 학습 실험의 hello 결과 이동 하는 활동 ***MLScoringRegionXPipeline *** toohello hello 솔루션 템플릿 설치의 일부로 프로 비전 된 Azure SQL 데이터베이스입니다.

#### <a name="copyaggdemandpipeline"></a>*CopyAggDemandPipeline*
이 [파이프라인](data-factory/data-factory-create-pipelines.md) 단일 활동-를 포함 한 [복사](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello를 이동 하는 활동에서 진행 중인 요청 데이터를 집계 ***LoadHistoryDemandDataPipeline*** toohello Azure Hello 솔루션 템플릿 설치의 일부로 프로 비전 된 SQL 데이터베이스입니다.

#### <a name="copyregiondatapipeline-copysubstationdatapipeline-copytopologydatapipeline"></a>*CopyRegionDataPipeline, CopySubstationDataPipeline, CopyTopologyDataPipeline*
이러한 [파이프라인](data-factory/data-factory-create-pipelines.md) 단일 활동-를 포함 한 [복사](https://msdn.microsoft.com/library/azure/dn835035.aspx) hello 않은 지역/변전소/Topologygeo의 참조 데이터를 이동 하는 활동 hello 솔루션의 일부로 tooAzure 저장소 blob 업로드 서식 파일 설치 toohello hello 솔루션 템플릿 설치의 일부로 프로 비전 된 Azure SQL 데이터베이스

### <a name="azure-machine-learning"></a>Azure 기계 학습
hello [Azure 기계 학습](https://azure.microsoft.com/services/machine-learning/) 실험이 솔루션 템플릿은 제공 영역의 수요의 예측 hello에 대 한 사용 합니다. hello 실험 특정 toohello 데이터 집합을 사용 하 고 따라서의 상태가 수정 이나 대체 특정 toohello 데이터를 필요 합니다.

## <a name="monitor-progress"></a>**진행률 모니터링**
Hello 데이터 생성기가 시작 되 면 hello 파이프라인 하이드레이션 tooget 차고 hello 솔루션의 다른 구성 요소 시작 hello Data Factory에서 발급 한 다음 hello 명령 실행을 시작한 합니다. 두 가지 방법으로 hello 파이프라인을 모니터링할 수 있습니다.

1. Azure Blob 저장소에서 hello 데이터를 확인 합니다.

    Hello 스트림 분석 작업 중 하나는 hello 원시 들어오는 데이터 tooblob 저장소를 씁니다. 클릭 하면 **Azure Blob 저장소** hello에서 솔루션의 구성 요소를 성공적으로 배포 된 hello 솔루션을 화면 및 클릭 **열려** hello 오른쪽 패널에서 이동할 수 toohello [Azure 관리 포털](https://portal.azure.com)합니다. **Blobs**을 클릭합니다. Hello 다음 창에서 컨테이너 목록이 표시 됩니다. **"energysadata"**를 클릭합니다. Hello hello 다음 패널에 나타납니다 **"demandongoing"** 폴더입니다. Hello rawdata 폴더 안에 날짜와 같은 이름 가진 폴더가 나타납니다 2016-01-28 = 등입니다. 이러한 폴더 표시 되 면 것을 의미 hello 원시 데이터가 성공적으로 컴퓨터에 생성 되어 blob 저장소에 저장 합니다. 해당 폴더에 한정된 크기(MB)로 있어야 하는 파일이 표시됩니다.
2. Azure SQL 데이터베이스에서 hello 데이터를 확인 합니다.

    hello hello 파이프라인의 마지막 단계는 SQL 데이터베이스로 toowrite 데이터 (예: 기계 학습에서 예측). Toowait 최대 2 시간 데이터 tooappear hello에 대 한 SQL 데이터베이스에서 할 수 있습니다. 한 가지 방법은 toomonitor 얼마나 많은 데이터를 SQL 데이터베이스에서 사용할 수 있는 방식은 [Azure 관리 포털](https://manage.windowsazure.com/)합니다. Hello 왼쪽된 패널에서 SQL 데이터베이스를 찾습니다![](media/cortana-analytics-technical-guide-demand-forecast/SQLicon2.png) 클릭 합니다. 그런 다음 데이터베이스(예: demo123456db)를 찾고 클릭합니다. Hello 아래에서 다음 페이지에서 **"Connect tooyour 데이터베이스"** 섹션에서 클릭 **"SQL 데이터베이스에 대 한 실행 Transact SQL 쿼리"**합니다.

    여기에서 클릭할 수 새 쿼리 및 쿼리 hello 개수의 행 (예: select 그룹 DemandRealHourly에서)에 대 한 "데이터베이스 확장 되면서 hello hello 테이블의 행 수는 증가 해야 합니다.)
3. Power BI 대시보드에서 hello 데이터를 확인 합니다.

    Power BI 실행 부하 과다 경로 대시보드 toomonitor hello 원시 들어오는 데이터를 설정할 수 있습니다. Hello "Power BI 대시보드" 섹션에 있는 hello 명령을 수행 하십시오.

## <a name="power-bi-dashboard"></a>**Power BI 대시보드**
### <a name="overview"></a>개요
이 섹션에서는 어떻게 tooset Power BI 대시보드 toovisualize Azure에서 실시간으로 데이터 분석 (실행 부하 과다 경로)로 스트리밍할도 같이 예측된 결과를 설명 Azure 기계 학습 (콜드 경로).

### <a name="setup-hot-path-dashboard"></a>실행 부하 과다 경로 대시보드 설정
어떻게 toovisualize 실시간으로 데이터에서에서 출력 스트림 분석 솔루션 배포의 hello 시 생성 된 작업 단계를 수행 하는 hello는 안내 합니다. A [Power BI 온라인](http://www.powerbi.com/) 계정은 필요한 tooperform hello 단계를 수행 합니다. 계정이 없는 경우 [새로 만들](https://powerbi.microsoft.com/pricing)수 있습니다.

1. Azure 스트림 분석(ASA)에 Power BI 출력을 추가합니다.

   * 지침에 toofollow hello 해야 [Azure Stream Analytics 및 Power BI: 스트리밍 데이터의 실시간 표시 여부에 대 한 실시간 분석 대시보드](stream-analytics/stream-analytics-power-bi-dashboard.md) tooset Power로 Azure 스트림 분석 작업의 hello 출력을 BI 대시보드입니다.
   * Hello 스트림 분석 작업에서 찾은 프로그램 [Azure 관리 포털](https://manage.windowsazure.com)합니다. hello 작업의 hello 이름 이어야 합니다: YourSolutionName + "streamingjob" + 임의의 번호 + "asapbi" (즉, demostreamingjob123456asapbi).
   * Hello ASA 작업에 대 한 PowerBI 출력을 추가 합니다. 집합 hello **출력 별칭** 으로 **'PBIoutput'**합니다. **데이터 집합 이름**과 **테이블 이름**을 **‘EnergyStreamData’**로 설정합니다. Hello 출력을 추가한 후 클릭 **"Start"** hello 페이지 toostart hello 스트림 분석 작업의 hello 맨 아래에 있습니다. 확인 메시지를 받아야 합니다(*예:*"스트림 분석 작업 myteststreamingjob12345asablob 시작 성공").
2. 로그 너무[Power BI 온라인](http://www.powerbi.com)

   * 내 작업 영역에서 왼쪽 패널 데이터 집합 구역 hello에서 수 toosee hello Power BI의 왼쪽된 패널에 새 데이터 집합 표시 해야 합니다. 이 스트리밍 데이터 hello 이전 단계에서 Azure 스트림 분석에서 푸시 hello입니다.
   * 있는지 hello 확인 ***시각화*** 창 열려 있고 hello 화면 오른쪽에 표시 됩니다.
3. Hello "요청 하 여 타임 스탬프" 타일을 만듭니다.

   * 데이터 집합 클릭 **'EnergyStreamData'** hello 왼쪽 패널 데이터 집합 섹션에 있습니다.
   * **"꺾은선형 차트"** 아이콘 ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic8.png)을 클릭합니다.
   * **필드** 패널에서 'EnergyStreamData'를 클릭합니다.
   * **"타임스탬프"** 를 클릭하고 "축" 아래에 표시되는지 확인합니다. **"로드"** 를 클릭하고 "값" 아래에 표시되는지 확인합니다.
   * 클릭 **저장** 위쪽 hello 되 고 "EnergyStreamDataReport"으로 hello 보고서의 이름을 지정 합니다. "EnergyStreamDataReport" 라는 hello 보고서 hello 왼쪽 탐색기 창에 보고서 섹션에 표시 됩니다.
   * 클릭 **"Pin 시각적"** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) 이 꺾은선형 차트의 오른쪽 위 모서리에서 아이콘을 "Pin tooDashboard" 창이 나타날 toochoose 있습니다에 대 한 대시보드 합니다. "EnergyStreamDataReport"를 선택한 후 "고정"을 클릭하세요.
   * Hello 대시보드에서이 타일을 통해 "편집" 클릭 toochange 오른쪽 위 모퉁이에서 아이콘 "요청 하 여 타임 스탬프" 제목 hello 마우스를 가져가고
4. 적절한 데이터 집합에 따라 다른 대시보드 타일을 만듭니다. hello 최종 대시보드 보기는 다음과 같습니다.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PBIFullScreen.png)

### <a name="setup-cold-path-dashboard"></a>콜드 경로 대시보드 설정
콜드 경로 데이터 파이프라인에서 hello 필수 ´ ֲ 각 영역의 tooget hello 수요를 예측 합니다. Power BI를 hello 예측 결과 저장 된 데이터 원본으로 tooan Azure SQL 데이터베이스를 연결 합니다.

> [!NOTE]
> 1) 몇 시간 toocollect hello 대시보드에 대 한 충분 한 예측된 결과 필요합니다. 2 ~ 3 시간이 hello 데이터 생성기 점심 후이 프로세스를 시작 하는 것이 좋습니다. 2)이이 단계에서는 hello 필수 구성 요소가 설치 하 고 toodownload hello 무료 소프트웨어 [Power BI desktop](https://powerbi.microsoft.com/desktop)합니다.
>
>

1. Hello 데이터베이스 자격 증명을 가져옵니다.

   해야 **데이터베이스 서버 이름, 데이터베이스 이름, 사용자 이름 및 암호** toonext 단계 이동 하기 전에. 다음 hello 단계 tooguide은 있습니다 어떻게 toofind 해당 합니다.

   * 솔루션 템플릿 다이어그램의 **"Azure SQL Database"**가 녹색으로 바뀌면 클릭한 다음 **"열기"**를 클릭합니다. 안내 tooAzure 관리 포털을 사용할 수 및 데이터베이스 정보 페이지도 열립니다.
   * Hello 페이지에서 "데이터베이스" 섹션을 찾을 수 있습니다. 만든 hello 데이터베이스도 나열 합니다. 데이터베이스의 이름은 hello 해야 **"프로그램 솔루션 이름 + 임의의 번호 + 'db'"** (예: "mytest12345db").
   * 패널 팝아웃를 찾을 수 있습니다 프로그램 데이터베이스 서버 이름 hello 맨 위에 새 hello에서 데이터베이스를 클릭 합니다. 데이터베이스 서버 이름은 **"솔루션 이름 + 난수 + 'database.windows.net,1433'"**(예: "mytest12345.database.windows.net,1433")이어야 합니다.
   * 데이터베이스 **username** 및 **암호** username hello와 동일 hello 및 암호 중 이전에 기록한 hello 솔루션의 배포 합니다.
2. Hello hello 콜드 경로 Power BI 파일의 데이터 소스 업데이트

   * 최신 버전의 hello를 설치 했는지 확인 [Power BI desktop](https://powerbi.microsoft.com/desktop)합니다.
   * Hello에 **"DemandForecastingDataGeneratorv1.0"** 다운로드 폴더, 두 번 클릭 hello **' Power BI Template\DemandForecastPowerBI.pbix'** 파일입니다. hello 초기 시각화 더미 데이터를 기반으로 합니다. **참고:** 오류 메시지로 전송, hello Power BI Desktop의 최신 버전을 설치 해야 하는 경우 표시 합니다.

     사용자가 열 hello 파일의 hello 상단에서을 클릭 **쿼리 편집 '**합니다. Hello 창 팝아웃에서 두 번 클릭 **'Source'** hello 오른쪽 패널에 있습니다.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic1.png)
   * Hello 창 팝아웃, 바꿉니다 **"Server"** 및 **"Database"** 고유한 서버 및 데이터베이스 이름 및 클릭 **"확인"**합니다. 서버 이름에 대 한 지정 했는지 확인 hello 포트 1433 (**YourSolutionName.database.windows.net, 1433**). Hello 화면에 표시 된 hello 경고 메시지를 무시 합니다.
   * 다음 팝업 창 hello에 hello 왼쪽된 창에서 두 가지 옵션이 표시 됩니다 (**Windows** 및 **데이터베이스**). 클릭 **"Database"**, 입력 프로그램 **"Username"** 및 **"Password"** (이 hello 사용자 이름 및 먼저 hello 솔루션을 배포 하 고 만들 때 입력 한 암호는 Azure SQL 데이터베이스)입니다. ***있는 수준 tooapply 하도록 이러한 설정을 선택***, 데이터베이스 수준 옵션을 선택 합니다. 그런 다음 **"연결"**을 클릭합니다.
   * 을 사용 하는 안내 방식된 백 toohello 이전 페이지 되 면 hello 창을 닫습니다. 메시지가 나타나면 **적용**을 클릭합니다. 마지막으로, hello 클릭 **저장** toosave hello 변경 단추입니다. Power BI 파일은 이제 연결 toohello 서버를 설정 합니다. 시각화 비어 있으면 hello 오른쪽 위 모서리의 hello 범례 hello 지우개 아이콘을 클릭 하 여 hello 시각화 toovisualize hello 선택 항목을 hello 데이터를 모두 해제 해야 합니다. Hello 시각화에 hello tooreflect 새 데이터 새로 고침 단추를 사용 합니다. 처음에 표시 됩니다 hello 데이터 시각화에 있는 그대로 hello 데이터 팩터리 예약된 toorefresh 3 시간 마다. 3 시간 후 hello 데이터를 새로 고칠 때 시각화에 반영 하는 새 예측을 확인할 수 있습니다.
3. (선택 사항) Hello 콜드 경로 대시보드를 너무 게시[Power BI 온라인](http://www.powerbi.com/)합니다. 이 단계는 Power BI 계정(또는 Office 365 계정)이 필요합니다.

   * 클릭 **"Publish"** 몇 초 후는 창이 표시 "게시" tooPower BI 성공! 나타납니다. 창이 나타납니다. "Power BI에서 열기 demoprediction.pbix" 아래의 hello 링크를 클릭 합니다. toofind 자세한 지침을 참조 [Power BI Desktop에서 게시](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop)합니다.
   * 새 대시보드 toocreate: hello 클릭  **+**  다음 toothe 서명 **대시보드** hello 왼쪽된 창에서 섹션. 이 새 대시보드에 대 한 "요청 예측 데모" hello 이름을 입력 합니다.
   * 클릭 하 여 hello 보고서를 열면 ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) toopin 모든 시각화 tooyour 대시보드 합니다. toofind 자세한 지침을 참조 [보고서에서 타일 tooa Power BI 대시보드 고정](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report)합니다.
     Toohello 대시보드 페이지로 이동 하 고 시각화의 hello 크기와 위치를 조정 하 고 직함을 편집 합니다. toofind tooedit 타일을 확인 하려면 어떻게 해야에 대 한 지침을 자세히 [Edit 타일-크기 조정, 이동, 이름 바꾸기, 고정, 삭제, 하이퍼링크 추가](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename)합니다. 일부 콜드 경로 고정 된 시각화 tooit의 예제 대시보드는 다음과 같습니다.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic7.png)
4. (선택 사항) Hello 데이터 원본의 새로 고침을 예약 합니다.

   * hello 데이터의 새로 고침 tooschedule hello 마우스 포인터로 **EnergyBPI 최종** 데이터 집합을 클릭 하 여 ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic3.png) 선택한 후 **새로 고침 예약**합니다.
     **참고:** 표시를 클릭 하는 경고 마사지 **자격 증명 편집** 데이터베이스 자격 증명 1 단계에서 설명 된 것과 동일한 hello 되 고 있는지 확인 합니다.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic4.png)
   * Hello 확장 **새로 고침 예약** 섹션. "데이터를 최신 상태로 유지"를 켭니다.
   * 필요에 따라 hello 새로 고침을 예약 합니다. toofind 자세한 내용은 참조 [Power BI에서 데이터 새로 고침](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)합니다.

## <a name="how-toodelete-your-solution"></a>**어떻게 toodelete 솔루션**
중이지 않은 비용이 더 많이 부과할 hello 데이터 생성기를 실행 하는 대로 hello 솔루션을 사용 하는 경우 hello 데이터 생성기를 중지 하는 확인 하십시오. 사용 하지 않는 경우 hello 솔루션을 삭제 하십시오. 솔루션을 삭제 하면 hello 솔루션을 배포할 때 구독에 사용자를 프로 비전 hello 구성 요소를 모두 삭제 됩니다. toodelete hello 솔루션 hello hello 솔루션 템플릿의 왼쪽된 창에서 솔루션 이름을 클릭 하 고 삭제를 클릭 합니다.

## <a name="cost-estimation-tools"></a>**비용 예측 도구**
hello 다음 두 가지 도구를 사용할 수 있는 toohelp 구독에서 에너지 솔루션 템플릿에 대 한 수요 예측 hello를 실행 하는 데 필요한 총 비용을 더 잘 이해:

* [Microsoft Azure 비용 추정 도구(온라인)](https://azure.microsoft.com/pricing/calculator/)
* [Microsoft Azure 비용 추정 도구(데스크톱)](http://www.microsoft.com/download/details.aspx?id=43376)

## <a name="acknowledgements"></a>**승인**
이 문서는 Microsoft 소속 데이터 과학자 Yijing Chen과 소프트웨어 엔지니어 Qiu Min이 작성하였습니다.
