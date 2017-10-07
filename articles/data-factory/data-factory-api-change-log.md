---
title: ".NET API 변경 로그 aaaData 공장-| Microsoft Docs"
description: "주요 변경 내용, 추가 기능, 버그 수정 등을 설명... Azure Data Factory hello에 대 한.NET API의 특정 버전입니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8208271b-7f4c-4214-b665-d2ff503c4470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: spelluru
ms.openlocfilehash: 1d44b45c3dc8f9d483d1f1cef7068edacc610932
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---net-api-change-log"></a>Azure 데이터 팩터리 - .NET API 변경 로그
이 문서에서는 특정 버전에서 변경 내용 tooAzure 데이터 팩터리 SDK에 대 한 정보를 제공 합니다. Azure Data Factory에 대 한 hello 최신 NuGet 패키지를 찾을 수 있습니다 [여기](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)

## <a name="version-4110"></a>버전 4.11.0
기능 추가 사항:

* hello 다음 연결 된 서비스 유형에 추가 되었습니다.
  * [OnPremisesMongoDbLinkedService](https://msdn.microsoft.com/library/mt765129.aspx)
  * [AmazonRedshiftLinkedService](https://msdn.microsoft.com/library/mt765121.aspx)
  * [AwsAccessKeyLinkedService](https://msdn.microsoft.com/library/mt765144.aspx)
* 데이터 집합 형식에 따라 hello 추가 되었습니다.
  * [MongoDbCollectionDataset](https://msdn.microsoft.com/library/mt765145.aspx)
  * [AmazonS3Dataset](https://msdn.microsoft.com/library/mt765112.aspx)
* hello 다음 형식이 추가 된 소스를 복사 합니다.
  * [MongoDbSource](https://msdn.microsoft.com/library/mt765123.aspx)

## <a name="version-4100"></a>4.10.0 버전
* 다음과 같은 선택적 속성 hello tooTextFormat 추가 되었습니다.
  * [SkipLineCount](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.skiplinecount.aspx)
  * [FirstRowAsHeader](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.firstrowasheader.aspx)
  * [TreatEmptyAsNull](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.treatemptyasnull.aspx)
* hello 다음 연결 된 서비스 유형에 추가 되었습니다.
  * [OnPremisesCassandraLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandralinkedservice.aspx)
  * [SalesforceLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.salesforcelinkedservice.aspx)
* 데이터 집합 형식에 따라 hello 추가 되었습니다.
  * [OnPremisesCassandraTableDataset](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandratabledataset.aspx)
* hello 다음 형식이 추가 된 소스를 복사 합니다.
  * [CassandraSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.cassandrasource.aspx)
* 추가 [WebServiceInputs](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azuremlbatchexecutionactivity.webserviceinputs.aspx) 속성 tooAzureMLBatchExecutionActivity
  * 여러 웹 서비스 입력 tooan Azure 기계 학습 실험 전달 사용

## <a name="version-491"></a>버전 4.9.1
### <a name="bug-fix"></a>버그 수정
* [WebLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.weblinkedservice.authenticationtype.aspx)에 대한 WebApi 기반 인증이 더 이상 사용되지 않습니다.

## <a name="version-490"></a>버전 4.9.0
### <a name="feature-additions"></a>기능 추가 사항
* 추가 [EnableStaging](https://msdn.microsoft.com/library/mt767916.aspx) 및 [StagingSettings](https://msdn.microsoft.com/library/mt767918.aspx) 속성 tooCopyActivity 합니다. 참조 [복사본을 스테이징](data-factory-copy-activity-performance.md#staged-copy) hello 기능에 대 한 자세한 내용은 합니다.

### <a name="bug-fix"></a>버그 수정
* [ActivityWindowOperationExtensions.List](https://msdn.microsoft.com/library/mt767915.aspx) 인스턴스를 사용하는 [ActivityWindowsByActivityListParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.activitywindowsbyactivitylistparameters.aspx) 메서드의 오버로드를 지정합니다.
* [WriteBatchSize](https://msdn.microsoft.com/library/dn884293.aspx) 및 [WriteBatchTimeout](https://msdn.microsoft.com/library/dn884245.aspx)를 CopySink에 옵션으로 표시합니다.

## <a name="version-480"></a>버전 4.8.0
### <a name="feature-additions"></a>기능 추가 사항
* 다음과 같은 선택적 속성 hello tooCopy 활동 추가 된 tooenable 복사 성능 튜닝 입력:
  * [ParallelCopies](https://msdn.microsoft.com/library/mt767910.aspx)
  * [CloudDataMovementUnits](https://msdn.microsoft.com/library/mt767912.aspx)

## <a name="version-470"></a>버전 4.7.0
### <a name="feature-additions"></a>기능 추가 사항
* 새 StorageFormat 형식을 추가 [OrcFormat](https://msdn.microsoft.com/library/mt723391.aspx) 최적화 된 행의 열 (ORC) 형식의 toocopy 파일을 입력 합니다.
* 추가 [AllowPolyBase](https://msdn.microsoft.com/library/mt723396.aspx) 및 PolyBaseSettings 속성 tooSqlDWSink 합니다.
  * SQL 데이터 웨어하우스로 PolyBase toocopy 데이터를 hello 사용 하도록 설정 합니다.

## <a name="version-461"></a>버전 4.6.1
### <a name="bug-fixes"></a>버그 수정
* 작업 창을 나열하기 위한 HTTP 요청을 해결합니다.
  * Hello 요청 페이로드에서 hello 리소스 그룹 이름 및 데이터 팩토리 이름이 hello 제거합니다.

## <a name="version-460"></a>버전 4.6.0
### <a name="feature-additions"></a>기능 추가 사항
* hello 다음과 같은 속성이 추가 되었습니다 너무[PipelineProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties_properties.aspx):
  * [PipelineMode](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.pipelinemode.aspx)
  * [ExpirationTime](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.expirationtime.aspx)
  * [데이터 집합](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.datasets.aspx)
* hello 다음과 같은 속성이 추가 되었습니다 너무[PipelineRuntimeInfo](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.aspx):
  * [PipelineState](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.pipelinestate.aspx)
* 새로 추가 [StorageFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.storageformat.aspx) 형식 [JsonFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.jsonformat.aspx) toodefine 데이터 집합을 JSON 형식에서 해당 데이터를 입력 합니다.

## <a name="version-450"></a>버전 4.5.0
### <a name="feature-additions"></a>기능 추가 사항
* [작업 창에 대한 작업 목록](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.activitywindowoperationsextensions.aspx)이 추가되었습니다.
  * Hello 엔터티 형식 (데이터 팩터리, 데이터 집합, 파이프라인 및 활동) 기반 필터와 tooretrieve 활동 창 메서드를 추가 합니다.
* hello 다음 연결 된 서비스 유형에 추가 되었습니다.
  * [ODataLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odatalinkedservice.aspx), [WebLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.weblinkedservice.aspx)
* 데이터 집합 형식에 따라 hello 추가 되었습니다.
  * [ODataResourceDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odataresourcedataset.aspx), [WebTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.webtabledataset.aspx)
* hello 다음 형식이 추가 된 소스를 복사 합니다.     
  * [WebSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.websource.aspx)

## <a name="version-440"></a>버전 4.4.0
### <a name="feature-additions"></a>기능 추가 사항
* hello 다음 연결 된 서비스 유형의 데이터 원본으로 추가 된 및 복사 작업에 대 한 싱크:
  * [AzureStorageSasLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azurestoragesaslinkedservice.aspx). 개념 정보 및 예제는 [Azure 저장소 SAS 연결된 서비스](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) 를 참조하세요.

## <a name="version-430"></a>버전 4.3.0
### <a name="feature-additions"></a>기능 추가 사항
* 연결 된 서비스 형식 숙소 다음 hello 된 복사 작업에 대 한 데이터 원본으로 추가 합니다.
  * [HdfsLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.hdfslinkedservice.aspx). 개념 정보 및 예제는 [Data Factory를 사용하여 HDFS에서 데이터 이동](data-factory-hdfs-connector.md) 을 참조하세요.
  * [OnPremisesOdbcLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisesodbclinkedservice.aspx). 개념 정보 및 예제는 [Azure Data Factory를 사용하여 ODBC 데이터 저장소에서 데이터 이동](data-factory-odbc-connector.md) 을 참조하세요.

## <a name="version-420"></a>버전 4.2.0
### <a name="feature-additions"></a>기능 추가 사항
* 추가 된 새 활동 유형을 다음 hello: [AzureMLUpdateResourceActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremlupdateresourceactivity.aspx)합니다. Hello 활동에 대 한 세부 정보를 참조 하십시오. [업데이트 Azure ML 모델을 사용 하 여 hello 업데이트 리소스 작업](data-factory-azure-ml-batch-execution-activity.md)합니다.
* 새 선택적 속성 [updateResourceEndpoint](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.updateresourceendpoint.aspx) toohello 추가 된 [AzureMLLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.aspx)합니다.
* [LongRunningOperationInitialTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationinitialtimeout.aspx) 및 [LongRunningOperationRetryTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationretrytimeout.aspx) 속성이 toohello 추가 된 [DataFactoryManagementClient](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.aspx) 클래스입니다.
* 클라이언트 호출 toohello 데이터 팩터리 서비스에 대 한 hello 시간 제한 구성은 허용 합니다.

## <a name="version-410"></a>Version 4.1.0
### <a name="feature-additions"></a>기능 추가 사항
* hello 다음 연결 된 서비스 유형에 추가 되었습니다.
  * [AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)
  * [AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)
* hello 활동 유형만 추가 되었습니다.
  * [DataLakeAnalyticsUSQLActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datalakeanalyticsusqlactivity.aspx)
* 데이터 집합 형식에 따라 hello 추가 되었습니다.
  * [AzureDataLakeStoreDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoredataset.aspx)
* hello 복사 작업에 대 한 다음 원본 및 싱크 형식 추가 되었습니다.
  * [AzureDataLakeStoreSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresource.aspx)
  * [AzureDataLakeStoreSink](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresink.aspx)

## <a name="version-401"></a>버전 4.0.1
### <a name="breaking-changes"></a>주요 변경 내용
아래의 클래스가 hello 이름이 바뀌었습니다. hello 새 이름을 4.0.0 해제 하기 전에 클래스의 원래 이름을 hello 했습니다.

| 4.0.0의 이름 | 4.0.1의 이름 |
|:--- |:--- |
| AzureSqlDataWarehouseDataset |[AzureSqlDataWarehouseTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqldatawarehousetabledataset.aspx) |
| AzureSqlDataset |[AzureSqlTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqltabledataset.aspx) |
| AzureDataset |[AzureTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuretabledataset.aspx) |
| OracleDataset |[OracleTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.oracletabledataset.aspx) |
| RelationalDataset |[RelationalTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.relationaltabledataset.aspx) |
| SqlServerDataset |[SqlServerTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.sqlservertabledataset.aspx) |

## <a name="version-400"></a>버전 4.0.0
### <a name="breaking-changes"></a>주요 변경 내용
* hello 클래스/인터페이스에 따라 변경 되었습니다.

| 이전 이름 | 새 이름 |
|:--- |:--- |
| ITableOperations |[IDatasetOperations](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.idatasetoperations.aspx) |
| 테이블 |[데이터 집합](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.dataset.aspx) |
| TableProperties |[DatasetProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetproperties.aspx) |
| TableTypeProprerties |[DatasetTypeProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasettypeproperties.aspx) |
| TableCreateOrUpdateParameters |[DatasetCreateOrUpdateParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateparameters.aspx) |
| TableCreateOrUpdateResponse |[DatasetCreateOrUpdateResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateresponse.aspx) |
| TableGetResponse |[DatasetGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetgetresponse.aspx) |
| TableListResponse |[DatasetListResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetlistresponse.aspx) |
| CreateOrUpdateWithRawJsonContentParameters |[DatasetCreateOrUpdateWithRawJsonContentParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdatewithrawjsoncontentparameters.aspx) |

* hello **목록** 메서드 이제 페이지 된 결과 반환 합니다. 비어 있지 않은 hello 응답에 포함 된 경우 **NextLink** 속성 hello 클라이언트 응용 프로그램에서 필요로 toocontinue 반입 hello 다음 페이지 모든 페이지는 반환 될 때까지 합니다.  다음은 예제입니다.

    ```csharp
    PipelineListResponse response = client.Pipelines.List("ResourceGroupName", "DataFactoryName");
    var pipelines = new List<Pipeline>(response.Pipelines);

    string nextLink = response.NextLink;
    while (!string.IsNullOrEmpty(nextLink))
    {
        PipelineListResponse nextResponse = client.Pipelines.ListNext(nextLink);
        pipelines.AddRange(nextResponse.Pipelines);

        nextLink = nextResponse.NextLink;
    }
    ```
* **목록** 파이프라인 API 반환만 파이프라인 전체 정보 대신 요약 hello 합니다. 예를 들어 파이프라인 요약의 작업에는 이름과 형식만 포함됩니다.

### <a name="feature-additions"></a>기능 추가 사항
* hello [SqlDWSink](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsink.aspx) 클래스에는 두 개의 새로운 속성이 지원 **SliceIdentifierColumnName** 및 **SqlWriterCleanupScript**, toosupport idempotent 복사본 tooAzure SQL 데이터 웨어하우스입니다. Hello 참조 [Azure SQL 데이터 웨어하우스](data-factory-azure-sql-data-warehouse-connector.md) 이러한 속성에 대 한 세부 정보에 대 한 문서입니다.
* 이제 hello 복사 작업의 일부로 Azure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스 원본에 대 한 저장된 프로시저 실행을 지원 합니다. hello [SqlSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqlsource.aspx) 및 [SqlDWSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsource.aspx) 클래스에는 다음과 같은 속성 hello: **SqlReaderStoredProcedureName** 및 **StoredProcedureParameters** . Hello 참조 [Azure SQL 데이터베이스](data-factory-azure-sql-connector.md#sqlsource) 및 [Azure SQL 데이터 웨어하우스](data-factory-azure-sql-data-warehouse-connector.md#sqldwsource) 대 한 이러한 속성에 대 한 자세한 내용은 Azure.com에 대 한 문서입니다.  
