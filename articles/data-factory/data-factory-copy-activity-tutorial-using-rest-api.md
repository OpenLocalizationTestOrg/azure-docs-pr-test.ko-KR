---
title: "자습서: REST API를 사용 toocreate Azure 데이터 팩터리 파이프라인 | Microsoft Docs"
description: "이 자습서에서는 Azure blob 저장소는 Azure SQL 데이터베이스에서 복사 작업 toocopy 데이터와 함께 REST API toocreate Azure 데이터 팩터리 파이프라인을 사용합니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a>자습서: REST API를 사용 toocreate Azure 데이터 팩터리 파이프라인 toocopy 데이터 
> [!div class="op_single_selector"]
> * [개요 및 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [복사 마법사](data-factory-copy-data-wizard-tutorial.md)
> * [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager 템플릿](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

이 문서에서는 어떻게 toouse REST API toocreate Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인으로 데이터 팩터리 방법을 배웁니다. 새 tooAzure 데이터 팩터리 인 경우 hello 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 이 자습서를 수행 하기 전에 문서입니다.   

이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다. hello 복사 작업 지원 되는 데이터 저장소 tooa 싱크를 지원 되는 데이터 저장소에서 데이터를 복사합니다. 원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요. hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다. Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.

파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다. 및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.

> [!NOTE]
> 이 문서에서 모든 hello 데이터 팩터리 REST API를 다루지 않습니다. 데이터 팩터리 REST API에 대한 포괄적인 설명서는 [데이터 팩터리 Cmdlet 참조](/rest/api/datafactory/) (영문)를 참조하세요.
>  
> 이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.

## <a name="prerequisites"></a>필수 조건
* 통해 이동 [자습서 개요](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 및 전체 hello **필수** 단계입니다.
* 컴퓨터에 [Curl](https://curl.haxx.se/dlwiz/) 을 설치합니다. 데이터 팩터리 REST 명령 toocreate와 hello Curl 도구를 사용 합니다. 
* [이 문서](../azure-resource-manager/resource-group-create-service-principal-portal.md) 의 지침에 따라 다음 작업을 수행합니다. 
  1. Azure Active Directory에서 **ADFCopyTutorialApp** 이라는 웹 응용 프로그램을 만듭니다.
  2. **클라이언트 ID** 및 **암호 키**를 가져옵니다. 
  3. **테넌트 ID**를 가져옵니다. 
  4. Hello 할당 **ADFCopyTutorialApp** 응용 프로그램 toohello **데이터 팩터리 참가자** 역할입니다.  
* [Azure PowerShell](/powershell/azure/overview)을 설치합니다.  
* 시작 **PowerShell** 및 다음 단계 hello지 않습니다. 이 자습서의 hello 끝날 때까지 Azure PowerShell를 열어 둡니다. 닫고 다시 열 경우 toorun hello 명령을 다시 필요 합니다.
  
  1. Hello 다음 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. 이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. 다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다. 대체  **&lt;NameOfAzureSubscription** &gt; hello 이름의 Azure 구독. 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. 라는 Azure 리소스 그룹 만들기 **ADFTutorialResourceGroup** hello 다음 hello PowerShell에서에서 명령을 실행 하 여:  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      Hello 리소스 그룹이 이미 있는 경우, 지정 여부 tooupdate 것 (Y) 하거나 (N)로 유지 합니다. 
     
      이 자습서의 hello 단계 중 일부 ADFTutorialResourceGroup 라는 hello 리소스 그룹을 사용 하는 것을 가정 합니다. 다른 리소스 그룹을 사용 하는 경우이 자습서의 ADFTutorialResourceGroup 대신 리소스 그룹의 toouse hello 이름이 필요 합니다.

## <a name="create-json-definitions"></a>JSON 정의 만들기
다음 JSON 파일 curl.exe 위치한 hello 폴더에 만듭니다. 

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Tooprefix/접미사 ADFCopyTutorialDF toomake 수 있도록 이름은 전역적으로 고유 해야 하기 고유 이름입니다. 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> **accountname** 및 **accountkey**를 Azure Storage 계정의 이름 및 키로 바꿉니다. toolearn 어떻게 tooget 저장소 액세스 키가 참조 [보기, 복사 및 다시 생성 저장소 액세스 키](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)합니다.

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

JSON 속성에 대한 자세한 내용은 [Azure Storage 연결된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service)를 참조하세요.

### <a name="azuersqllinkedservicejson"></a>azuersqllinkedservice.json
> [!IMPORTANT]
> 대체 **servername**, **databasename**, **username**, 및 **암호** SQL 데이터베이스의 이름, Azure SQL server의 이름으로 사용자 계정 및 hello 계정의 암호입니다.  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

JSON 속성에 대한 자세한 내용은 [Azure SQL 연결된 서비스](data-factory-azure-sql-connector.md#linked-service-properties)를 참조하세요.

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "AzureStorageLinkedService",
    "typeProperties": {
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ","
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

| 속성 | 설명 |
|:--- |:--- |
| type | hello type 속성이 너무 설정 되어**AzureBlob** 데이터는 Azure blob 저장소에 있기 때문에 있습니다. |
| linkedServiceName | Toohello 참조 **AzureStorageLinkedService** 앞에서 만든 합니다. |
| folderPath | Hello blob 지정 **컨테이너** 및 hello **폴더** 입력된 blob이 있는 합니다. 이 자습서에서는 adftutorial는 hello blob 컨테이너 및 폴더는 hello 루트 폴더입니다. | 
| fileName | 이 속성은 선택 사항입니다. 이 속성을 생략 하는 경우 hello folderPath에서 모든 파일을 선택 합니다. 이 자습서에서는 **emp.txt** hello 파일 이름, 해당 파일에만 선택 처리를 위해 지정 됩니다. |
| format -> type |사용 하도록 hello 입력된 파일은 hello 텍스트 형식 **TextFormat**합니다. |
| columnDelimiter | hello 입력된 파일에 hello 열으로 구분 됩니다 **쉼표 문자 (`,`)**합니다. |
| frequency/interval | hello 빈도가 너무 설정**시간** 간격이 너무 설정 되 고**1**, 즉, 해당 hello 입력 분할 영역을 사용할 수 있는 **매시간**합니다. 즉, hello 데이터 팩터리 서비스 검색 입력된 데이터에 대 한 1 시간 마다 blob 컨테이너의 hello 루트 폴더 (**adftutorial**) 사용자가 지정한 합니다. Hello 파이프라인 시작 및 종료 시간, 날짜부터 또는이 시간 이후로 내의 hello 데이터를 찾습니다.  |
| external | 이 속성은 너무**true** 경우 hello 데이터가이 파이프라인에서 생성 되지 않습니다. 이 자습서의 hello 입력된 데이터는 hello emp.txt 파일을 설정 하 여이 속성 tootrue 있으므로이 파이프라인에서 생성 되지 않습니다. |

이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "emp"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

| 속성 | 설명 |
|:--- |:--- |
| type | hello type 속성이 너무 설정 되어**AzureSqlTable** 데이터가 Azure SQL 데이터베이스에서 복사 된 tooa 테이블 되어 있습니다. |
| linkedServiceName | Toohello 참조 **AzureSqlLinkedService** 앞에서 만든 합니다. |
| tableName | 지정 된 hello **테이블** toowhich hello 데이터가 복사 됩니다. | 
| frequency/interval | hello 주기 설정 너무**시간** 간격은 및 **1**, hello 출력 조각만 생성 되는 것이 즉 **매시간** hello 파이프라인 시작 및 종료 시간, 이전은 아님 사이 또는 이 시간 후.  |

세 개의 열인 – **ID**, **FirstName**, 및 **LastName** – hello 데이터베이스의 hello emp 테이블에 있습니다. Toospecify만 필요 하므로 ID는 id 열 **FirstName** 및 **LastName** 여기 합니다.

이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL 커넥터 문서](data-factory-azure-sql-connector.md#dataset-properties)를 참조하세요.

### <a name="pipelinejson"></a>pipeline.json

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2017-05-11T00:00:00Z",
    "end": "2017-05-12T00:00:00Z"
  }
}
```

포인트 다음 참고 hello:

- Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다. Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다. Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.
- Hello 활동 너무 설정 되어 입력**AzureBlobInput** 및 hello 활동 너무 설정 되어 출력**AzureSqlOutput**합니다. 
- Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다. 원본 및 싱크도 hello 복사 작업에서 지 원하는 데이터 저장소의 전체 목록은 참조 하십시오. [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다. 소스/싱크도 toouse 지원 되는 특정 데이터를 저장 하는 방법 toolearn hello 표에 hello 링크를 클릭 합니다.  
 
Hello hello 값 바꾸기 **시작** hello 현재 날짜를 사용 하 여 속성 및 **끝** 다음날 hello 사용 하 여 값입니다. Hello 날짜 부분만 지정 하 고 날짜 시간 hello의 hello 시간 부분을 건너뛸 수 있습니다. 예를 들어 "2017-02-03", 즉 너무 "2017-02-03T00:00:00Z"
 
start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다. 예를 들어 2016-10-14T16:32:41Z입니다. hello **끝** 시간 선택 사항 이지만이 자습서에서 사용 했습니다. 
 
Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간**"입니다. toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다.
 
앞 예제는 hello에서 24 데이터 조각이 각 데이터 조각이 시간 단위로 생성 됩니다.

파이프라인 정의의 JSON 속성에 대한 설명은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요. 복사 활동 정의의 JSON 속성에 대한 설명은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요. BlobSource에서 지원하는 JSON 속성에 대한 설명은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md)를 참조하세요. SqlSink에서 지원하는 JSON 속성에 대한 설명은 [Azure SQL Database 커넥터 문서](data-factory-azure-sql-connector.md)를 참조하세요.

## <a name="set-global-variables"></a>전역 변수 설정
Azure PowerShell에서 명령을 직접 hello 값 바꾼 후 다음 hello를 실행 합니다.

> [!IMPORTANT]
> 클라이언트 ID, 클라이언트 암호, 테넌트 ID 및 구독 ID를 가져오는 지침은 [필수 구성 요소](#prerequisites) 섹션을 참조하세요.   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

Hello를 사용 하는 hello 데이터 팩터리의 hello 이름을 업데이트 한 후 다음 명령을 실행 합니다. 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a>AAD로 인증
Hello 명령 tooauthenticate와 Azure Active Directory (AAD) 다음을 실행 합니다. 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a>데이터 팩터리 만들기
이 단계에서는 **ADFCopyTutorialDF**라는 Azure Data Factory를 만듭니다. 데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 파이프라인에는 하나 이상의 작업이 있을 수 있습니다. 예를 들어 복사 작업 toocopy 데이터 소스 tooa 대상 데이터를 저장 합니다. HDInsight Hive 활동 toorun 하이브 스크립트 tootransform 데이터 tooproduct 출력 데이터를 입력 합니다. Hello 명령을 toocreate hello 데이터 팩터리를 다음을 실행 합니다. 

1. 명명 된 hello 명령 toovariable 할당 **cmd**합니다. 
   
    > [!IMPORTANT]
    > 여기에서 지정한 일치 하는 항목 (ADFCopyTutorialDF) hello hello에 지정 된 이름이 hello 데이터 팩터리의 hello 이름이 하는지 확인 **datafactory.json**합니다. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hello 결과 확인 합니다. Hello 데이터 팩토리에 hello에 대 한 JSON hello 참조 hello 데이터 팩터리 성공적으로 생성 된 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.  
   
    ```
    Write-Host $results
    ```

포인트 다음 참고 hello:

* Azure Data Factory hello의 hello 이름 전역적으로 고유 해야 합니다. 결과에 hello 오류가 나타나는 경우: **"ADFCopyTutorialDF" 데이터 팩터리 이름을 사용할 수 없으면**, 다음 단계 hello지 않습니다.  
  
  1. Hello에 hello 이름 변경 (예를 들어 yournameADFCopyTutorialDF) **datafactory.json** 파일입니다.
  2. Hello 첫 번째 명령은에 있는 hello **$cmd** 변수 ְ ÷ ° × ADFCopyTutorialDF hello 새 이름으로 바꾸고 hello 명령을 실행 합니다. 
  3. Hello 이후의 두 명령은 tooinvoke hello REST API toocreate hello 데이터 팩터리 및 인쇄 hello hello 작업 결과 실행 합니다. 
     
     데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.
* toocreate 데이터 팩터리 인스턴스 해야 toobe hello Azure 구독 참가자/관리자
* hello hello 데이터 팩터리의 이름입니다 hello 나중에 DNS 이름으로 등록 하 고 있으므로 공개 될 수 있습니다.
* Hello 오류가 나타나면: "**이 구독이 지원 되지 않으면 등록 된 toouse 네임 스페이스 microsoft.datafactory가**" hello 다음 중 하나를 수행 하 고 다시 게시 하십시오. 
  
  * Azure PowerShell에서 명령 tooregister hello 데이터 팩터리 공급자 hello를 실행 합니다. 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    데이터 팩터리 공급자가 등록 되어 해당 hello 명령 tooconfirm 다음 hello를 실행할 수 있습니다. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Hello에 Azure 구독을 hello 사용 하 여 로그인 [Azure 포털](https://portal.azure.com) tooa Data Factory 블레이드를 탐색 하 고 (또는) hello Azure 포털에서에서 데이터 팩터리를 만듭니다. 이 동작은 hello 공급자를 자동으로 등록합니다.

파이프라인을 만들기 전에 필요한 toocreate 몇 가지 Data Factory 엔터티에 먼저 합니다. 연결 된 서비스 toolink 소스를 먼저 만들어야 하 고 tooyour 데이터를 저장 하는 대상 데이터를 저장 합니다. 그런 다음 연결 된 데이터 저장소 모두에서 입력 및 출력 데이터 집합 toorepresent 데이터를 정의 합니다. 마지막으로 이러한 데이터 집합을 사용 하는 작업이 있는 hello 파이프라인을 만듭니다.

## <a name="create-linked-services"></a>연결된 서비스 만들기
데이터 팩터리 toolink 데이터 저장 및 계산 toohello 데이터 팩터리 서비스에에서 연결 된 서비스를 만듭니다. 이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다. Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다. 이에 따라 두 개의 연결된 서비스, 즉 AzureStorage와 AzureSqlDatabase 유형의 AzureStorageLinkedService와 AzureSqlLinkedService를 만듭니다.  

AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다. 이 저장소 계정은 hello 하나 컨테이너를 생성 하 고 hello 데이터의 일부로 업로드 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.   

AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다. hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다. 이 데이터베이스에 hello emp 테이블의 일부분으로 만든 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.  

### <a name="create-azure-storage-linked-service"></a>Azure 저장소 연결된 서비스 만들기
이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다. 이 섹션의 hello 이름 및 사용자의 Azure 저장소 계정 키를 지정합니다. 참조 [Azure 저장소 연결 된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 Azure 저장소 연결 된 서비스입니다.  

1. 명명 된 hello 명령 toovariable 할당 **cmd**합니다. 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hello 결과 확인 합니다. Hello 연결 되어 있는 경우 서비스가 성공적으로 만들어졌습니다., hello에 연결 하는 hello 서비스에 대 한 JSON hello 참조 **결과**, 그러지 않으면 오류 메시지가 나타납니다.

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a>Azure SQL 연결된 서비스 만들기
이 단계에서는 Azure SQL 데이터베이스 tooyour 데이터 팩터리를 연결할 수 있습니다. 이 섹션의 hello Azure SQL server 이름, 데이터베이스 이름, 사용자 이름 및 사용자 암호를 지정합니다. 참조 [Azure SQL 연결 된 서비스](data-factory-azure-sql-connector.md#linked-service-properties) JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 Azure SQL 연결 된 서비스입니다.

1. 명명 된 hello 명령 toovariable 할당 **cmd**합니다. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hello 결과 확인 합니다. Hello 연결 되어 있는 경우 서비스가 성공적으로 만들어졌습니다., hello에 연결 하는 hello 서비스에 대 한 JSON hello 참조 **결과**, 그러지 않으면 오류 메시지가 나타납니다.
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>데이터 집합 만들기
Hello 이전 단계에서 Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리에 연결 된 서비스 toolink을 만들었습니다. 이 단계에서는 AzureBlobInput 및 입력을 나타내는 AzureSqlOutput 각각 AzureStorageLinkedService 및 AzureSqlLinkedService에서 참조 하는 hello 데이터 저장소에 저장 되어 있는 출력 데이터 라는 두 개의 데이터 집합을 정의 합니다.

hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 고 hello 입력된 blob 데이터 집합 (AzureBlobInput) hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.  

마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 및 hello 출력 SQL 테이블의 데이터 집합 (OututDataset) hello blob 저장소에서 데이터를 복사 하는 hello 데이터베이스 toowhich hello에 hello 테이블을 지정 합니다. 

### <a name="create-input-dataset"></a>입력 데이터 집합 만들기
이 단계에서는 hello hello AzureStorageLinkedService 연결 된 서비스를 나타내는 Azure 저장소에서에서 blob 컨테이너 (adftutorial)의 hello 루트 폴더에 tooa blob 파일 (emp.txt)를 가리키는 AzureBlobInput 라는 데이터 집합이 만듭니다. 하지 hello 파일 이름에 대 한 값을 지정 (하거나 건너뛸 수), 데이터 hello 입력된 폴더의 모든 blob에서 됩니다 복사한 toohello 대상입니다. 이 자습서에서는 hello 파일 이름에 대 한 값을 지정합니다. 

1. 명명 된 hello 명령 toovariable 할당 **cmd**합니다. 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hello 결과 확인 합니다. Hello에 hello 데이터 집합에 대 한 JSON hello 참조 hello 데이터 집합에서 성공적으로 만든 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>출력 데이터 집합 만들기
hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. hello 출력 SQL 테이블 데이터 집합 (OututDataset)이이 단계에서 만드는 지정 hello 표 hello 데이터베이스 toowhich hello hello blob 저장소에서 데이터에서를 복사 합니다.

1. 명명 된 hello 명령 toovariable 할당 **cmd**합니다.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hello 결과 확인 합니다. Hello에 hello 데이터 집합에 대 한 JSON hello 참조 hello 데이터 집합에서 성공적으로 만든 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a>파이프라인 만들기
이 단계에서는 **AzureBlobInput**을 입력으로 사용하고 **AzureSqlOutput**을 출력으로 사용하는 **복사 작업**을 포함하는 파이프라인을 만듭니다.

현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다. 이 자습서에서는 출력 데이터 집합은 구성 된 tooproduce 조각을 두 번는 시간입니다. hello 파이프라인 시작 시간과 종료 시간이 되는 24 시간 이상 떨어져 1 일에 있습니다. 따라서 출력 데이터 집합의 24 조각은 hello 파이프라인에 의해 생성 됩니다. 

1. 명명 된 hello 명령 toovariable 할당 **cmd**합니다.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Hello 결과 확인 합니다. Hello에 hello 데이터 집합에 대 한 JSON hello 참조 hello 데이터 집합에서 성공적으로 만든 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.  

    ```PowerShell   
    Write-Host $results
    ```

**축하합니다.** Azure Blob 저장소 tooAzure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인와 Azure 데이터 팩터리를 성공적으로 만들었습니다.

## <a name="monitor-pipeline"></a>파이프라인 모니터링
이 단계에서는 hello 파이프라인에 의해 생성 되는 데이터 팩터리 REST API toomonitor 분할 영역을 사용 합니다.

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> Hello 시작 및 종료 시간 뒤에 지정 된 hello 명령 일치 hello 시작 및 종료 시간 hello 파이프라인의 있는지 확인 합니다. 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

실행 Invoke-command hello 및 hello 다음에 있는 분할 영역에 표시 될 때까지 **준비** 상태 또는 **실패** 상태입니다. Hello 조각 준비 상태에 있으면 확인 hello **emp** hello 출력 데이터에 대 한 Azure SQL 데이터베이스의 테이블에에서 있습니다. 

각 조각에 대 한 hello 소스 파일에서 데이터의 두 행이 hello Azure SQL 데이터베이스에서 복사 된 toohello emp 테이블 됩니다. 따라서 모든 hello 분할 영역 (준비 상태)에 성공적으로 처리 되 면 hello emp 테이블에 새 레코드를 24 참조 합니다. 

## <a name="summary"></a>요약
이 자습서에서는 REST API toocreate Azure blob tooan Azure SQL 데이터베이스에서 Azure 데이터 팩터리 toocopy 데이터를 사용 했습니다. 이 자습서에서 수행 하는 hello 상위 수준 단계는 다음과 같습니다.  

1. Azure **데이터 팩터리**를 만들었습니다.
2. **연결된 서비스**를 만들었습니다.
   1. Azure 저장소 입력된 데이터를 보유 하는 Azure 저장소 계정의 서비스 toolink에 연결 되어 있습니다.     
   2. Azure SQL 서비스 toolink hello 출력 데이터를 보유 하 여 Azure SQL 데이터베이스를 연결 합니다. 
3. 파이프라인의 입력 데이터와 출력 데이터를 설명하는 **데이터 집합**을 만들었습니다.
4. 원본인 BlobSource와 싱크인 SqlSink를 사용하여 복사 작업으로 **파이프라인** 을 만들었습니다. 

## <a name="next-steps"></a>다음 단계
이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다. hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn toocopy 데이터는 데이터를 저장 하는 방법에 대 한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다.
