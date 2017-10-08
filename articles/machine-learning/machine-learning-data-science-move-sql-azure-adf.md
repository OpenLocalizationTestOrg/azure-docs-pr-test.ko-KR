---
title: "온-프레미스 SQL Server tooSQL Azure 데이터 팩터리를 사용 하 여 Azure에서에서 aaaMove 데이터 | Microsoft Docs"
description: "함께 hello 클라우드 및 데이터베이스 온-프레미스 간의 매일 데이터를 이동 하는 두 가지 데이터 마이그레이션 작업을 구성 하는 ADF 파이프라인을 설정 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a>온-프레미스 SQL server tooSQL Azure 데이터 팩터리를 사용 하 여 Azure에서에서 데이터 이동
이 항목에서는 toomove 데이터를 사용 하 여 Azure Blob 저장소를 통해 온-프레미스 SQL Server 데이터베이스 tooa SQL Azure 데이터베이스를에서 Azure 데이터 팩터리 (ADF) hello 하는 방법을 보여 줍니다.

이동 데이터가 tooan Azure SQL 데이터베이스에 대 한 다양 한 옵션을 요약 하는 테이블에 대 한 참조 [Azure 기계 학습에 대 한 데이터 tooan Azure SQL 데이터베이스를 이동](machine-learning-data-science-move-sql-azure.md)합니다.

## <a name="intro"></a>소개: 무엇 ADF 이며 때 해야 것이 사용 되는 toomigrate 데이터?
Azure 데이터 팩터리는 오케스트레이션 하 고 데이터의 hello 이동 및 변환을 자동화 하는 클라우드 기반 데이터를 완전히 관리 되는 통합 서비스입니다. hello hello ADF 모델의 주요 개념은 파이프라인입니다. 파이프라인은 정의 하는 hello 동작 tooperform hello 데이터 데이터 집합에 포함 된 활동의 논리적 그룹입니다. 연결 된 서비스는 Data Factory tooconnect toohello 데이터 리소스에 필요한 사용 되는 toodefine hello 정보입니다.

ADF와 기존 데이터 처리 서비스는 항상 사용 가능 하 고 관리 되는 hello 클라우드에서 데이터 파이프라인으로 구성할 수 있습니다. 이러한 데이터 파이프라인 수 예약된 tooingest 수, 준비, 변환, 분석 및 데이터를 게시 및 ADF를 관리 하 고 hello 복잡 한 데이터 및 처리 종속성을 오케스트레이션 합니다. 솔루션 신속 하 게에 작성 되 고에 배포 된 hello 클라우드, 온-프레미스 점점 더 많은 연결 수 및 클라우드 데이터 원본 수 있습니다.

다음 경우에 ADF 사용을 고려합니다.

* 경우 데이터 요구 toobe 둘 다에 액세스 하는 하이브리드 시나리오에서 지속적으로 마이그레이션된 온-프레미스와 클라우드 리소스
* 때 hello 데이터는 트랜잭션 또는 요구 toobe 수정 되거나 비즈니스 논리 tooit 마이그레이션 중인 경우 추가 합니다.

ADF hello 일정 예약 및 hello 주기적으로 데이터 이동을 관리 하는 간단한 JSON 스크립트를 사용 하 여 작업에 대 한 모니터링을 허용 합니다. 또한 복잡한 작업을 지원하는 기타 기능도 포함하고 있습니다. ADF에 대 한 자세한 내용은 hello 설명서를 참조 [Azure 데이터 팩터리 (ADF)](https://azure.microsoft.com/services/data-factory/)합니다.

## <a name="scenario"></a>hello 시나리오
두 가지 데이터 마이그레이션 작업을 구성하는 ADF 파이프라인을 설정했습니다. 함께 온-프레미스 SQL 데이터베이스와 hello 클라우드에서 Azure SQL 데이터베이스 간의 매일 데이터 이동 합니다. hello 두 활동은:

* 온-프레미스 SQL Server 데이터베이스 tooan Azure Blob 저장소 계정에서에서 데이터 복사
* hello Azure Blob 저장소 계정 tooan Azure SQL 데이터베이스에서에서 데이터를 복사 합니다.

> [!NOTE]
> 더 자세한 자습서 hello ADF 팀에서 제공 하는 hello에서 변형 된 여기 설명 된 단계 hello: [온-프레미스 원본 및 데이터 관리 게이트웨이 클라우드 간 데이터 이동](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) toohello 해당 항목의 관련 섹션을 참조 합니다. 적절 한 경우에 제공 됩니다.
>
>

## <a name="prereqs"></a>필수 조건
이 자습서에서는 사용자가 다음을 보유하고 있다고 가정합니다.

* **Azure 구독**. 구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.
* **Azure 저장소 계정**. Azure 저장소 계정 '를 사용 하 여이 자습서에서 hello 데이터를 저장 합니다. Azure 저장소 계정이 없으면 참조 hello [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 문서. Hello 저장소 계정을 만든 후 tooobtain hello 계정 키 tooaccess hello 저장소를 사용 해야 합니다. [저장소 액세스 키 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)를 참조하세요.
* 액세스 tooan **Azure SQL 데이터베이스**합니다. Azure SQL 데이터베이스를 설정 해야 하는 경우 hello tpoic [Microsoft Azure SQL 데이터베이스 시작 ](../sql-database/sql-database-get-started.md) 방법에 대해 설명 tooprovision Azure SQL 데이터베이스의 새 인스턴스.
* 로컬로 설치 및 구성된 **Azure PowerShell** . 자세한 내용은 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

> [!NOTE]
> 이 절차에서는 hello [Azure 포털](https://portal.azure.com/)합니다.
>
>

## <a name="upload-data"></a>업로드 hello 데이터 tooyour 온-프레미스 SQL Server
사용 하 여 hello [NYC 택시 dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello 마이그레이션 프로세스입니다. hello NYC 택시 데이터 집합은 사용할 수 있는, Azure blob 저장소에서 해당 게시물에서 설명한 것 처럼 [NYC 택시 데이터](http://www.andresmh.com/nyctaxitrips/)합니다. hello 데이터에는 두 개의 파일, 여행 세부 정보를 포함 하는 hello trip_data.csv 파일 및 각 여정에 대해 지불한 hello 요금에 대 한 세부 정보를 포함 하는 hello trip_far.csv 파일에 있습니다. 이러한 파일의 샘플 및 설명은 [NYC Taxi Trips 데이터 집합 설명](machine-learning-data-science-process-sql-walkthrough.md#dataset)에 제공됩니다.

여기 tooa 자신만 데이터 집합에 제공 된 hello 절차를 조정 하거나 hello NYC 택시 데이터 집합을 사용 하 여 hello 단계에 따라 수 있습니다. tooupload hello를 온-프레미스 SQL Server 데이터베이스를 사용 하 여 NYC 택시 데이터 집합에 설명 된 hello 절차에 따라 [SQL Server 데이터베이스에 데이터 대량 가져오기](machine-learning-data-science-process-sql-walkthrough.md#dbload)합니다. 이러한 지침은 SQL Server에는 Azure 가상 컴퓨터를 위한 하지만 온-프레미스 SQL Server가 toohello 업로드 하기 위한 hello 프로시저 hello 동일 합니다.

## <a name="create-adf"></a> Azure 데이터 팩터리 만들기
hello에 새 Azure Data Factory와 리소스 그룹을 만들기 위한 지침 hello [Azure 포털](https://portal.azure.com/) 제공 [Azure 데이터 팩터리를 만들어](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory)합니다. ADF 인스턴스에 새 이름이 hello *adfdsp* 및 이름 hello 리소스 그룹을 만든 *adfdsprg*합니다.

## <a name="install-and-configure-up-hello-data-management-gateway"></a>설치 하 고 hello 데이터 관리 게이트웨이를 구성 합니다.
tooenable 파이프라인 tooadd 해야 온-프레미스 SQL Server와 Azure 데이터 팩터리 toowork로 연결 된 서비스 toohello 데이터 팩터리입니다. 온-프레미스 SQL Server에 대 한 연결 된 서비스는 toocreate를 해야합니다.

* 다운로드 하 여 hello 온-프레미스 컴퓨터에 Microsoft 데이터 관리 게이트웨이 설치 합니다.
* hello 온-프레미스 데이터 원본 toouse hello 게이트웨이에 대 한 hello 연결 된 서비스를 구성 합니다.

hello 데이터 관리 게이트웨이 또는 그 반대로 serialize 하 고 그 데이터베이스가 호스팅될 hello 컴퓨터에 hello 원본 및 싱크 데이터를 역직렬화 합니다.

데이터 관리 게이트웨이에 대한 설치 지침 및 세부 정보에 대한 내용은 [데이터 관리 게이트웨이 클라우드를 사용하여 온-프레미스 원본과 클라우드 간에 데이터 이동](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)

## <a name="adflinkedservices"></a>연결 된 서비스 tooconnect toohello 데이터 리소스 만들기
연결 된 서비스는 Azure Data Factory tooconnect tooa 데이터 리소스에 대 한 필요한 hello 정보를 정의 합니다. 에 연결 된 서비스를 만들기 위한 단계별 절차 hello 제공 [연결 된 서비스를 만들](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services)합니다.

이 시나리오에는 연결된 서비스가 필요한 3개의 리소스가 있습니다.

1. [온-프레미스 SQL Server에 대한 연결된 서비스](#adf-linked-service-onprem-sql)
2. [Azure Blob 저장소에 대한 연결된 서비스](#adf-linked-service-blob-store)
3. [Azure SQL 데이터베이스에 대한 연결된 서비스](#adf-linked-service-azure-sql)

### <a name="adf-linked-service-onprem-sql"></a>온-프레미스 SQL Server 데이터베이스에 대한 연결된 서비스
hello에 대 한 연결 된 hello 서비스 toocreate 온-프레미스 SQL Server:

* hello 클릭 **데이터 저장소** Azure 클래식 포털에서 hello ADF 방문 페이지에서
* 선택 **SQL** hello 입력 *username* 및 *암호* hello 온-프레미스 SQL Server 자격 증명입니다. 필요한 tooenter hello 서버 이름으로는 **정규화 servername 백슬래시 인스턴스 이름 (servername\instancename)**합니다. 연결 된 서비스 이름 hello *adfonpremsql*합니다.

### <a name="adf-linked-service-blob-store"></a>Blob에 대한 연결된 서비스
toocreate hello hello Azure Blob 저장소 계정에 대 한 연결 된 서비스:

* hello 클릭 **데이터 저장소** Azure 클래식 포털에서 hello ADF 방문 페이지에서
* **Azure Storage Account**
* hello Azure Blob 저장소 계정 키 및 컨테이너 이름을 입력 합니다. 연결 된 서비스 이름 hello *adfds*합니다.

### <a name="adf-linked-service-azure-sql"></a>Azure SQL 데이터베이스에 대한 연결된 서비스
toocreate hello hello Azure SQL 데이터베이스에 대 한 연결 된 서비스:

* hello 클릭 **데이터 저장소** Azure 클래식 포털에서 hello ADF 방문 페이지에서
* 선택 **Azure SQL** hello 입력 *username* 및 *암호* hello Azure SQL 데이터베이스에 대 한 자격 증명입니다. hello *username* 으로 지정 해야  *user@servername* 합니다.   

## <a name="adf-tables"></a>정의 하 고 테이블 toospecify를 만드는 방법을 tooaccess hello 데이터 집합
스크립트 기반 절차를 수행 하는 hello로 hello 구조, 위치 및 hello 데이터 집합의 가용성을 지정 하는 테이블을 만듭니다. JSON 파일은 사용 되는 toodefine hello 테이블입니다. 이러한 파일의 hello 구조에 대 한 자세한 내용은 참조 하십시오. [데이터 집합](../data-factory/data-factory-create-datasets.md)합니다.

> [!NOTE]
> Hello를 실행 해야 `Add-AzureAccount` hello를 실행 하기 전에 cmdlet [새로 AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) hello 명령 실행에 대 한 구독을 오른쪽 hello cmdlet tooconfirm을 선택 합니다. 이 cmdlet의 설명서는 [Add-azureaccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0)를 참조하세요.
>
>

hello 테이블에서 JSON 기반 정의 hello 이름 다음 hello를 사용 합니다.

* hello **테이블 이름** hello 온-프레미스 SQL server가 *nyctaxi_data*
* hello **컨테이너 이름** hello Azure Blob 저장소 계정은 *containername*  

이 ADF 파이프라인에는 3개의 테이블 정의가 필요합니다.

1. [SQL 온-프레미스 테이블](#adf-table-onprem-sql)
2. [Blob 테이블 ](#adf-table-blob-store)
3. [SQL Azure 테이블](#adf-table-azure-sql)

> [!NOTE]
> 이러한 프로시저 toodefine Azure PowerShell을 사용 하 여 및 hello ADF 활동을 만듭니다. 하지만 hello Azure 포털을 사용 하 여 이러한 작업 수행할 수도 있습니다. 자세한 내용은 [데이터 집합 만들기](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets)를 참조하세요.
>
>

### <a name="adf-table-onprem-sql"></a>SQL 온-프레미스 테이블
hello 테이블 정의 hello에 대 한 온-프레미스 SQL Server hello 다음 JSON 파일에에서 지정 된:

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

hello 열 이름은 포함 되지 않은 여기 합니다. 여기 포함 하 여 hello 열 이름에 하위 선택할 수 있습니다 (세부 정보 확인 hello [ADF 설명서](../data-factory/data-factory-data-movement-activities.md) 항목입니다.

Hello 테이블의 JSON 정의 hello 라는 파일에 복사 *onpremtabledef.json* 파일을 저장 위치를 알려진 tooa (여기 toobe 가정 *C:\temp\onpremtabledef.json*). Azure PowerShell cmdlet을 다음 hello로 ADF에 hello 테이블을 만듭니다.

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a>Blob 테이블
Blob 위치 (온-프레미스 tooAzure blob에서 데이터 수집 된 hello 매핑합니다) hello 다음에는 hello에 대 한 hello 테이블에 대 한 정의 출력 합니다.

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

Hello 테이블의 JSON 정의 hello 라는 파일에 복사 *bloboutputtabledef.json* 파일을 저장 위치를 알려진 tooa (여기 toobe 가정 *C:\temp\bloboutputtabledef.json*). Azure PowerShell cmdlet을 다음 hello로 ADF에 hello 테이블을 만듭니다.

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sq"></a>SQL Azure 테이블
SQL Azure 출력 hello에 대 한 hello 테이블에 대 한 정의 hello 다음 (이 스키마는 hello blob에서 들어오는 hello 데이터를 매핑합니다)입니다.

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

Hello 테이블의 JSON 정의 hello 라는 파일에 복사 *AzureSqlTable.json* 파일을 저장 위치를 알려진 tooa (여기 toobe 가정 *C:\temp\AzureSqlTable.json*). Azure PowerShell cmdlet을 다음 hello로 ADF에 hello 테이블을 만듭니다.

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a>정의 및 hello 파이프라인 만들기
스크립트 기반 절차를 수행 하는 hello로 hello 파이프라인을 만들고와 파이프라인 toohello 속하는 hello 활동을 지정 합니다. JSON 파일에 사용 되는 toodefine hello 파이프라인 속성입니다.

* hello 스크립트 가정 해당 hello **파이프라인 이름** 은 *AMLDSProcessPipeline*합니다.
* 또한 hello 파이프라인 toobe 매일 사용 하 여 기준 hello 기본 실행 시간은 hello 작업 (오전 12 시 UTC)에 대 한 실행의 hello 주기 성을 설정 했으므로 note 합니다.

> [!NOTE]
> hello 다음 절차 toodefine Azure PowerShell을 사용 하 고 hello ADF 파이프라인을 만듭니다. 그러나 이러한 작업은 Azure 포털을 사용해서도 수행할 수 있습니다. 자세한 내용은 [파이프라인 만들기](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline)를 참조하세요.
>
>

Hello 테이블 정의 사용 하 여 ADF 다음과 같이 지정 하는 hello에 대 한 hello 파이프라인 정의 이전에 제공 합니다.

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

이 JSON 정의 hello 파이프라인의 라는 파일에 복사 *pipelinedef.json* 파일을 저장 위치를 알려진 tooa (여기 toobe 가정 *C:\temp\pipelinedef.json*). Azure PowerShell cmdlet을 다음 hello로 ADF에 hello 파이프라인을 만듭니다.

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

표시 되는지 확인 수 hello 파이프라인 ADF hello Azure 클래식 포털에서에서 표시 하는 hello에 다음과 같이 (hello 다이어그램을 클릭) 하는 경우

![ADF 파이프라인](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <a name="adf-pipeline-start"></a>Hello 파이프라인을 시작 합니다.
다음 명령을 hello를 사용 하 여 hello 파이프라인을 실행할 수 있습니다.

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

hello *startdate* 및 *enddate* 매개 변수 값 toobe hello 실제 날짜 원하는 hello 파이프라인 toorun 구분으로 대체 해야 합니다.

Hello 파이프라인 실행 되 면 수 toosee hello 데이터에에서 표시 hello 컨테이너 blob hello 하루에 하나의 파일에 대해 선택 해야 합니다.

증분 ADF toopipe 데이터에서 제공 하는 hello 기능 활용 하지 있을 것을 참고 합니다. Toodo이 및 ADF에서 제공 하는 다른 기능 확인 하려면 어떻게 해야 대 한 자세한 내용은 hello [ADF 설명서](https://azure.microsoft.com/services/data-factory/)합니다.
