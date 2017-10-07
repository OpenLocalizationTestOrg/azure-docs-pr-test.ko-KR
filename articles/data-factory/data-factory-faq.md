---
title: "데이터 팩터리-aaaAzure 질문과 대답"
description: "Azure 데이터 팩터리에 대한 질문과 대답입니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 532dec5a-7261-4770-8f54-bfe527918058
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 78289fb4b6e15d74772af6c71ec25c7d2ca1a0bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a>Azure 데이터 팩터리 - 질문과 대답
## <a name="general-questions"></a>일반적인 질문
### <a name="what-is-azure-data-factory"></a>Azure 데이터 팩터리란 무엇인가요?
데이터 팩터리는 클라우드 기반 데이터를 통합 하는 서비스 **데이터의 hello 이동 및 변환을 자동화**합니다. 데이터 팩터리 tootake 원자재 장비를 실행 하 고 완성 된 상품으로 변환 하는 팩터리와 마찬가지로 원시 데이터를 수집 하 고 사용 가능한 준비 정보로 변환 하는 기존 서비스를 조정 합니다.

데이터 팩터리에 온-프레미스 및 클라우드 데이터 저장소를 비롯해 Azure HDInsight Azure 데이터 레이크 분석 등의 계산 서비스를 사용 하 여 프로세스/변환 데이터 간에 toocreate 데이터 기반 워크플로 toomove 데이터 수 있습니다. 필요한 hello 동작을 수행 하는 파이프라인을 만든 후 toorun 주기적으로 (매시간, 매일, 매주 등) 예약할 수 있습니다.   

자세한 내용은 [개요 및 주요 개념](data-factory-introduction.md)을 참조하세요.

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a>Azure 데이터 팩터리에 대한 가격 정보는 어디서 찾을 수 있나요?
참조 [데이터 팩터리 가격 정보 페이지] [ adf-pricing-details] hello 가격 hello Azure Data Factory에 대 한 정보에 대 한 합니다.  

### <a name="how-do-i-get-started-with-azure-data-factory"></a>Azure 데이터 팩터리를 시작하려면 어떻게 해야 하나요?
* Azure Data Factory의 개요를 참조 하십시오. [소개 tooAzure Data Factory](data-factory-introduction.md)합니다.
* 방법에 대 한 자습서에 대 한 너무**복사/이동 데이터** 복사 작업을 사용 하 여, 참조 [Azure Blob 저장소 tooAzure SQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.
* 방법에 대 한 자습서에 대 한 너무**데이터 변환** HDInsight Hive 활동 사용 합니다. [Process data by running Hive script on Hadoop cluster](data-factory-build-your-first-pipeline.md)(Hadoop 클러스터에서 Hive 스크립트를 실행하여 데이터 처리)를 참조하세요.

### <a name="what-is-hello-data-factorys-region-availability"></a>Hello 데이터 팩토리 영역 가용성 란?
Data Factory는 **미국 서부** 및 **북유럽**에서 사용할 수 있습니다. hello 계산 및 데이터 팩터리에서 사용 하는 저장소 서비스는 다른 지역 들에 될 수 있습니다. [지원되는 지역](data-factory-introduction.md#supported-regions)을 참조하세요.

### <a name="what-are-hello-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a>다양 한 데이터 팩터리/파이프라인/활동/datasets에 hello 제한 사항은 무엇입니까?
참조 **Azure 데이터 팩터리 제한** hello 섹션 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md#data-factory-limits) 문서.

### <a name="what-is-hello-authoringdeveloper-experience-with-azure-data-factory-service"></a>Azure Data Factory 서비스와 hello 제작/개발자 환경 이란?
작성자/만들면 hello 도구/Sdk를 다음 중 하나를 사용 하 여 데이터 팩터리 됩니다.

* **Azure 포털** hello Data Factory 블레이드 hello Azure 포털에서에서 다양 한 사용자 인터페이스를 제공할 toocreate 데이터 팩터리 ad 연결 된 서비스입니다. hello **데이터 팩터리 편집기**, hello 포털의 일부 이기도 하면 tooeasily 이러한 아티팩트에 대 한 JSON 정의 지정 하 여 연결 된 서비스, 테이블, 데이터 집합 및 파이프라인을 만듭니다. 참조 [Azure 포털을 사용 하 여 첫 번째 데이터 파이프라인을 빌드](data-factory-build-your-first-pipeline-using-editor.md) 사용 하는 예제 포털/편집기 toocreate hello 및 데이터 팩터리를 배포 합니다.
* **Visual Studio** Visual Studio toocreate Azure 데이터 팩터리를 사용할 수 있습니다. 자세한 내용은 [Build your first data pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) (Visual Studio를 사용하여 첫 번째 데이터 파이프라인 빌드)를 참조하세요.
* **Azure PowerShell** PowerShell을 사용하여 Data Factory를 만드는 자습서는 [Create and monitor Azure Data Factory using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md) (Azure PowerShell을 사용하여 Azure Data Factory 만들기 및 모니터링)을 참조하세요. 데이터 팩터리 cmdlet의 포괄적인 설명서는 MSDN 라이브러리의 [데이터 팩터리 Cmdlet 참조][adf-powershell-reference] 콘텐츠를 참조하세요.
* **.NET 클래스 라이브러리** Data Factory .NET SDK를 사용하여 프로그래밍 방식으로 데이터 팩터리를 만들 수 있습니다. .NET SDK를 사용하여 데이터 팩터리를 만드는 연습은 [.NET SDK를 사용하여 데이터 팩터리 만들기, 모니터링 및 관리](data-factory-create-data-factories-programmatically.md)를 참조하세요. 데이터 팩터리 .NET SDK의 포괄적인 설명서는 [데이터 팩터리 클래스 라이브러리 참조][msdn-class-library-reference]를 참조하세요.
* **REST API** hello hello Azure Data Factory 서비스 toocreate에 의해 노출 되는 REST API를 사용 하 고 데이터 팩터리를 배포할 수도 있습니다. 데이터 팩터리 REST API의 포괄적인 설명서는 [데이터 팩터리 REST API 참조][msdn-rest-api-reference]를 참조하세요.
* **Azure Resource Manager 템플릿** 자세한 내용은 [자습서: Azure Resource Manager 템플릿을 사용하여 첫 번째 Azure Data Factory 빌드](data-factory-build-your-first-pipeline-using-arm.md) 를 참조하세요.

### <a name="can-i-rename-a-data-factory"></a>Data Factory의 이름을 바꿀 수 있나요?
아니요. 다른 Azure 리소스와 마찬가지로 Azure 데이터 팩터리에의 hello 이름을 변경할 수 없습니다.

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-tooanother"></a>하나의 Azure 구독 tooanother에서 데이터 팩터리를 이동할 수 있습니까?
예. 사용 하 여 hello **이동** hello 다음 다이어그램에에서 표시 된 대로 데이터 팩터리 블레이드에서 단추:

![데이터 팩터리 이동](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-hello-compute-environments-supported-by-data-factory"></a>Data Factory에서 지 원하는 hello 계산 환경 이란?
hello 다음 표에서 계산 환경에서 실행할 수 있는 Data Factory와 hello 활동에서 지 원하는 목록을.

| 컴퓨팅 환경 | 작업 |
| --- | --- |
| [주문형 HDInsight 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 또는 [사용자 고유의 HDInsight 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop 스트리밍](data-factory-hadoop-streaming-activity.md) |
| [Azure 배치](data-factory-compute-linked-services.md#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure 기계 학습](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[Machine Learning 작업: 배치 실행 및 업데이트 리소스](data-factory-azure-ml-batch-execution-activity.md) |
| [Azure 데이터 레이크 분석](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[데이터 레이크 분석 U-SQL](data-factory-usql-activity.md) |
| [Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service), [Azure SQL Data Warehouse](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service), [SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service) |[저장 프로시저](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a>Azure Data Factory를 SSIS(SQL Server Integration Services)와 비교하면 어떻게 다른가요? 
Hello 참조 [Azure Data Factory vs. SSIS](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS) 프레젠테이션을 참조하세요. 데이터 팩터리 hello 최근 변경 사항 중 일부 hello 슬라이드 모음에 나열 되지 않을 수 있습니다. 더 많은 기능 tooAzure Data Factory 지속적으로 추가 됩니다. 더 많은 기능 tooAzure Data Factory 지속적으로 추가 됩니다. 우리는 이러한 업데이트에 통합 hello Microsoft의 데이터 통합 기술 비교 올해 후반 잠시 합니다.   

## <a name="activities---faq"></a>작업 - FAQ
### <a name="what-are-hello-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a>데이터 팩터리 파이프라인에서 사용할 수는 활동의 hello 다른 유형은 무엇 인가요?
* [데이터 이동 작업](data-factory-data-movement-activities.md) toomove 데이터입니다.
* [데이터 변환 작업](data-factory-data-transformation-activities.md) tooprocess/변환 데이터입니다.

### <a name="when-does-an-activity-run"></a>작업은 언제 실행되나요?
hello **가용성** hello 구성 설정을 출력 데이터 테이블 hello 활동 실행 되는 시기를 결정 합니다. 입력된 데이터 집합을 지정 하는 경우 hello 활동 모든 hello 입력된 데이터 종속성을 충족 하는지 여부를 확인 (즉, **준비** 상태) 실행을 시작 하기 전에.

## <a name="copy-activity---faq"></a>복사 작업 - FAQ
### <a name="is-it-better-toohave-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a>여러 작업이 포함 된 파이프라인 또는 각 활동에 대해 별도 파이프라인 더 나은 toohave 입니까?
파이프라인 되어야 하는 toobundle 관련 활동입니다. Hello 데이터 집합을 연결 하는 hello 파이프라인의 외부에 있는 다른 모든 작업에 사용 되지 않는, 경우에 파이프라인 하나에 hello 활동을 유지할 수 있습니다. 이 이렇게 하지 해야 toochain 파이프라인 활성 기간 서로 배열 되도록 합니다. 또한 hello 테이블 내부 toohello 파이프라인에서 데이터 무결성 hello hello 파이프라인을 업데이트할 때에 더 잘 유지 됩니다. 파이프라인 업데이트 기본적으로 hello 파이프라인 내의 모든 hello 활동, 제거, 멈추고으로 다시 만듭니다. 큐브를 제작할 수도 있습니다 hello와 관련 된 내부 데이터의 toosee hello 흐름을 보다 쉽게 hello 파이프라인에 대 한 JSON의 작업 파일입니다.

### <a name="what-are-hello-supported-data-stores"></a>데이터 저장소를 지원 hello 이란?
복사 활동 Data Factory에는 원본 데이터 저장소 tooa 싱크 데이터 저장소에서 데이터를 복사합니다. 데이터 팩터리 hello 다음 데이터 저장소를 지원 합니다. 데이터 소스에서 tooany 싱크를 작성할 수 있습니다. 데이터 저장소 toolearn 방법을 클릭 해당 저장소에서 데이터 tooand toocopy 합니다.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> 데이터 저장소와 * 온-프레미스 될 수 있습니다 또는 Azure IaaS에서 고 tooinstall 있어야 하며 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 에-프레미스/Azure IaaS 컴퓨터에 있습니다.

### <a name="what-are-hello-supported-file-formats"></a>파일 형식 지원 이란 hello?
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-hello-copy-operation-performed"></a>Hello 복사 작업을 수행 하는 위치
자세한 내용은 [전역적으로 사용 가능한 데이터 이동](data-factory-data-movement-activities.md#global) 섹션을 참조하세요. 즉, 온-프레미스 데이터 저장소와 관련 되어 온-프레미스 환경에 데이터 관리 게이트웨이 hello 하 여 hello 복사 작업이 수행 됩니다. Hello 지역 가장 가까운 toohello 싱크에서에서 위치에 있는 hello hello 복사 작업은 수행 hello 데이터 이동 클라우드 저장소 사이 있는 경우와 동일한 지리적 위치입니다.

## <a name="hdinsight-activity---faq"></a>HDInsight 작업 - FAQ
### <a name="what-regions-are-supported-by-hdinsight"></a>HDInsight에서 지원하는 지역은 어디인가요?
참조 지리적 가용성 섹션에서 다음 문서는 hello hello: 또는 [HDInsight 가격 정보][hdinsight-supported-regions]합니다.

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a>주문형 HDInsight 클러스터가 사용되는 지역은 어디인가요?
hello 주문형 HDInsight 클러스터를 만드는 hello에 동일한 toobe hello 클러스터와 사용을 지정 하는 hello 저장소가 있는 영역입니다.    

### <a name="how-tooassociate-additional-storage-accounts-tooyour-hdinsight-cluster"></a>어떻게 tooassociate 추가 저장소 계정 tooyour HDInsight 클러스터?
사용자 고유의 HDInsight 클러스터 (BYOC-고유의 클러스터 가져오기)를 사용 하는 경우 hello 다음 항목을 참조 하세요.

* [대체 저장소 계정 및 메타스토어와 HDInsight 클러스터 사용][hdinsight-alternate-storage]
* [HDInsight Hive와 추가 저장소 계정 사용][hdinsight-alternate-storage-2]

Hello 데이터 팩터리 서비스에 의해 만들어진 주문형 클러스터를 사용 하는 경우에 hello 데이터 팩터리 서비스에서 사용자 대신 등록할 수 있도록 HDInsight hello에 대 한 추가 저장소 계정을 연결 된 서비스를 지정 합니다. Hello hello 주문형 연결 된 서비스에 대 한 JSON 정의에서 사용 하 여 **additionalLinkedServiceNames** 다음 JSON 코드 조각은 hello와 같이 속성 toospecify 대체 저장소 계정:

```JSON
{
    "name": "MyHDInsightOnDemandLinkedService",
    "properties":
    {
        "type": "HDInsightOnDemandLinkedService",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "LinkedService-SampleData",
            "additionalLinkedServiceNames": [ "otherLinkedServiceName1", "otherLinkedServiceName2" ]
        }
    }
}
```
Hello 위의 예에서 otherLinkedServiceName1 및 otherLinkedServiceName2 정의가 hello HDInsight 클러스터 요구 tooaccess 대체 저장소 계정 자격 증명을 포함 하는 연결 된 서비스를 나타냅니다.

## <a name="slices---faq"></a>조각 - FAQ
### <a name="why-are-my-input-slices-not-in-ready-state"></a>내 입력 조각이 준비 상태가 아닌 이유는 무엇인가요?
일반적인 실수는 설정 하지 않으면 **외부** 속성 너무**true** hello에 hello 입력 데이터를 필터링 하는 경우 입력된 데이터 집합은 외부 toohello 데이터 팩터리의 (hello 데이터 팩터리에 의해 생성 되지 않은).

다음 예제는 hello, 데이터만 필요 tooset **외부** 에 tootrue **dataset1**합니다.  

**DataFactory1** 파이프라인 1: dataset1 -> activity1 -> dataset2 -> activity2 -> dataset3 파이프라인 2: dataset3-> activity3 -> dataset4

Dataset4 (데이터 팩터리 1에서에서 2 파이프라인에서 생성 된)를 사용 하는 파이프라인이 포함 된 다른 데이터 팩터리를 사용 하도록 설정한 경우는 hello 데이터 집합 (DataFactory1, 하지 DataFactory2) 다른 데이터 팩터리에서 생성 하기 때문에 외부 데이터 집합으로 dataset4를 표시 합니다.  

**DataFactory2**    
파이프라인 1: activity4->dataset4->dataset5

Hello 외부 속성을 올바르게 설정 하는 경우 입력된 데이터 hello hello 입력된 데이터 집합 정의에 지정 된 hello 위치에 있는지 여부를 확인 합니다.

### <a name="how-toorun-a-slice-at-another-time-than-midnight-when-hello-slice-is-being-produced-daily"></a>어떻게 toorun hello slice가 생성 될 때 되 고 매일 자정 보다 나중에 한 조각?
사용 하 여 hello **오프셋** hello 조각 toobe 원하는 속성 toospecify hello 시간 생성 합니다. 이 속성에 대한 자세한 내용은 [데이터 집합 가용성](data-factory-create-datasets.md#dataset-availability) 섹션을 참조하세요. 간단한 예제는 다음과 같습니다.

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
일별 조각화가 시작 시 **오전 6 시** hello 기본 자정 대신 합니다.     

### <a name="how-can-i-rerun-a-slice"></a>어떻게 조각을 다시 실행할 수 있나요?
Hello 같은 방법으로 다음 중 하나에 있는 분할 영역을 다시 실행할 수 있습니다.

* 모니터 및 앱 관리 toorerun 활동 또는 분할 영역을 사용 합니다. 지침에 대해서는 [선택한 작업 창 다시 실행](data-factory-monitor-manage-app.md#perform-batch-actions)을 참조하세요.   
* 클릭 **실행** hello에 hello 명령 모음에서 **데이터 조각을** 블레이드 hello Azure 포털에서에서 hello 조각에 대 한 합니다.
* 실행 **집합 AzureRmDataFactorySliceStatus** 상태를 사용 하 여 cmdlet 너무 설정**대기** hello 조각에 대 한 합니다.   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
참조 [집합 AzureRmDataFactorySliceStatus] [ set-azure-datafactory-slice-status] hello cmdlet에 대 한 세부 정보에 대 한 합니다.

### <a name="how-long-did-it-take-tooprocess-a-slice"></a>얼마나 오래 걸린 tooprocess 조각을?
활동 창 탐색기를 사용 하 여 모니터링 및 앱 관리 tooknow 걸린 tooprocess 데이터 조각에에서 있습니다. 자세한 내용은 [작업 창 탐색기](data-factory-monitor-manage-app.md#activity-window-explorer)를 참조하세요.

수행할 수 있습니다 hello Azure 포털에서에서 다음 hello:  

1. 클릭 **데이터 집합** hello 타일 **DATA FACTORY** 블레이드 데이터 팩토리에 대 한 합니다.
2. Hello에 특정 데이터 집합 hello 클릭 **데이터 집합** 블레이드입니다.
3. Hello에 관심 있는 선택 hello 조각 **최근 조각** hello 목록 **테이블** 블레이드입니다.
4. Hello에서를 실행 하는 hello 활동 클릭 **활동을 실행** hello 목록 **데이터 조각을** 블레이드입니다.
5. 클릭 **속성** hello 타일 **작업 실행 세부 정보** 블레이드입니다.
6. Hello 표시 되어야 **기간** 값이 있는 필드입니다. 이 값은 hello 시간이 tooprocess hello 조각화를 수행 합니다.   

### <a name="how-toostop-a-running-slice"></a>어떻게 toostop 실행 중인 조각?
Toostop hello 파이프라인을 실행 해야 하는 경우 사용할 수 있습니다 [Suspend AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) cmdlet. 현재 hello 파이프라인을 일시 중단 해도 진행 중인 hello 조각 실행 중지 되지 않습니다. Hello 진행 중인 실행 될 때 완료 되 면 추가 슬라이스 선택 되었습니다.

원하는 경우 toostop 모든 hello 실행 즉시, hello만 방식으로 toodelete hello 파이프라인 하 고 다시 만드십시오. Toodelete hello 파이프라인을 선택 하면 불필요 toodelete 테이블과 hello 파이프라인에서 사용 되는 연결 된 서비스입니다.

[create-factory-using-dotnet-sdk]: data-factory-create-data-factories-programmatically.md
[msdn-class-library-reference]: /dotnet/api/microsoft.azure.management.datafactories.models
[msdn-rest-api-reference]: /rest/api/datafactory/

[adf-powershell-reference]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/azurerm.datafactories
[azure-portal]: http://portal.azure.com
[set-azure-datafactory-slice-status]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/set-azurermdatafactoryslicestatus

[adf-pricing-details]: http://go.microsoft.com/fwlink/?LinkId=517777
[hdinsight-supported-regions]: http://azure.microsoft.com/pricing/details/hdinsight/
[hdinsight-alternate-storage]: http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx
[hdinsight-alternate-storage-2]: http://blogs.msdn.com/b/cindygross/archive/2014/05/05/use-additional-storage-accounts-with-hdinsight-hive.aspx
