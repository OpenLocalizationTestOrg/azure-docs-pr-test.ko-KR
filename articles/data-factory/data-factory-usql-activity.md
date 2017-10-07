---
title: "U-SQL 스크립트-Azure를 사용 하 여 aaaTransform 데이터 | Microsoft Docs"
description: "Azure Data Lake 분석 U-SQL 스크립트를 실행 하 여 tooprocess 또는 변환 데이터 서비스를 계산 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a>Azure Data Lake Analytics에서 U-SQL 스크립트를 실행하여 데이터 변환 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive 작업](data-factory-hive-activity.md) 
> * [Pig 작업](data-factory-pig-activity.md)
> * [MapReduce 작업](data-factory-map-reduce.md)
> * [Hadoop 스트리밍 작업](data-factory-hadoop-streaming-activity.md)
> * [Spark 작업](data-factory-spark.md)
> * [Machine Learning Batch 실행 작업](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning 업데이트 리소스 작업](data-factory-azure-ml-update-resource-activity.md)
> * [저장 프로시저 작업](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL 작업](data-factory-usql-activity.md)
> * [.NET 사용자 지정 작업](data-factory-use-custom-activities.md)

Azure 데이터 팩터리의 파이프라인은 연결된 저장소 서비스의 데이터를 연결된 계산 서비스를 사용하여 처리합니다. 파이프라인에는 일련의 작업이 포함되며 각 작업에서는 특정 처리 작업을 수행합니다. 이 문서에서는 hello 설명 **데이터 레이크 분석 U-SQL 작업** 를 실행 하는 **U-SQL** 스크립트는 **Azure 데이터 레이크 분석** 계산 연결 된 서비스입니다. 

> [!NOTE]
> Data Lake Analytics U-SQL 작업이 포함된 파이프라인을 만들기 전에 Azure Data Lake Analytics 계정을 만듭니다. Azure Data Lake 분석에 대 한 toolearn 참조 [Azure Data Lake 분석 시작](../data-lake-analytics/data-lake-analytics-get-started-portal.md)합니다.
> 
> 검토 hello [첫 번째 파이프라인 자습서 빌드하](data-factory-build-your-first-pipeline.md) 연결 된 서비스, 데이터 집합 및 파이프라인에 대 한 자세한 단계 toocreate 데이터 팩터리입니다. 데이터 팩터리 편집기 또는 Visual Studio 또는 Azure PowerShell toocreate Data Factory 엔터티에 JSON 조각을 사용 합니다.

## <a name="supported-authentication-types"></a>지원되는 인증 형식
U-SQL 작업은 Data Lake Analytics에 대해 아래 인증 유형을 지원합니다.
* 서비스 주체 인증
* 사용자 자격 증명(OAuth) 인증 

특히 예약된 U-SQL 실행의 경우 서비스 주체 인증을 사용하는 것이 좋습니다. 사용자 자격 증명 인증의 경우 토큰 만료 동작이 발생할 수 있습니다. 구성 세부 정보 참조 hello [연결 된 서비스 속성](#azure-data-lake-analytics-linked-service) 섹션.

## <a name="azure-data-lake-analytics-linked-service"></a>Azure 데이터 레이크 분석 연결된 서비스
만들 프로그램 **Azure 데이터 레이크 분석** 서비스 toolink Azure Data Lake 분석 계산 서비스 tooan Azure 데이터 팩터리에 연결 합니다. 데이터 레이크 분석 U-SQL 작업 hello 파이프라인의 hello toothis 연결 된 서비스를 참조합니다. 

hello 다음 표에서 hello에 대 한 설명을 hello JSON 정의에서 사용 되는 일반 속성. 서비스 주체와 사용자 자격 증명 인증 중에서 추가로 선택할 수 있습니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| **type** |hello type 속성이로 설정 해야: **AzureDataLakeAnalytics**합니다. |예 |
| **accountName** |Azure 데이터 레이크 분석 계정 이름입니다. |예 |
| **dataLakeAnalyticsUri** |Azure 데이터 레이크 분석 URI입니다. |아니요 |
| **subscriptionId** |Azure 구독 ID |아니요 (지정 하지 않으면 데이터 팩터리에 사용 되는 hello의 구독) 하는 경우. |
| **resourceGroupName** |Azure 리소스 그룹 이름 |아니요 (지정 하지 않으면 리소스 그룹의 데이터 팩터리에 사용 되는 hello) 하는 경우. |

### <a name="service-principal-authentication-recommended"></a>서비스 주체 인증(권장)
toouse 서비스 보안 주체 인증 레지스터 것 hello Azure Active Directory (Azure AD) 및 권한 부여의 응용 프로그램 엔터티 tooData 레이크 스토어에 액세스 합니다. 자세한 단계는 [서비스 간 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)을 참조하세요. 사용 되는 값을 다음 hello 기록 toodefine hello 연결 된 서비스:
* 응용 프로그램 UI
* 응용 프로그램 키 
* 테넌트 ID

Hello 다음과 같은 속성을 지정 하 여 서비스 사용자 인증을 사용 합니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| **servicePrincipalId** | Hello 응용 프로그램의 클라이언트 ID를 지정 | 예 |
| **servicePrincipalKey** | Hello 응용 프로그램의 키를 지정 합니다. | 예 |
| **테넌트** | 응용 프로그램에 속한 아래 hello 테 넌 트 정보 (도메인 이름 또는 테 넌 트 ID)를 지정 합니다. Hello Azure 포털의 오른쪽 위 모서리 hello에에서 hello 마우스 호버 하 여 검색할 수 있습니다. | 예 |

**예제: 서비스 주체 인증**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>사용자 자격 증명 인증
또는 hello 다음과 같은 속성을 지정 하 여 Data Lake 분석에 대 한 사용자 자격 증명 인증을 사용할 수 있습니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| **권한 부여** | Hello 클릭 **Authorize** hello 데이터 팩터리 편집기 단추를 선택한 hello 자동 생성 된 권한 부여 URL toothis 속성을 할당 하 여 자격 증명을 입력 합니다. | 예 |
| **sessionId** | Hello OAuth 권한 부여 세션에서 OAuth 세션 ID입니다. 각 세션 ID는 고유하고 한 번만 사용될 수 있습니다. 이 설정은 hello 데이터 팩터리 편집기를 사용 하는 경우 자동으로 생성 됩니다. | 예 |

**예제: 사용자 자격 증명 인증**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>토큰 만료
hello를 사용 하 여 생성 하는 인증 코드를 hello **Authorize** 단추 잠시 후에 만료 됩니다. 다음 표에 다양 한 유형의 사용자 계정에 대 한 만료 시간 hello에 대 한 hello를 참조 하십시오. Hello 다음과 같은 오류 메시지가 표시 될 수 있습니다 때 인증 hello **토큰이 만료 된**: 작업 오류를 자격 증명: invalid_grant-AADSTS70002: 자격 증명 유효성 검사 오류입니다. AADSTS70008: hello 액세스 권한 부여가 만료 되었거나 해지 제공 합니다. 추적 ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 상관관계 ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 타임스탬프: 2015-12-15 21:09:31Z

| 사용자 유형 | 다음 시간 후에 만료 |
|:--- |:--- |
| Azure Active Directory에서 관리되지 않는 사용자 계정(@hotmail.com, @live.com 등) |12시간 |
| AAD(Azure Active Directory)에서 관리되는 사용자 계정 |hello 마지막 조각 실행 한 후 14 일입니다. <br/><br/>OAuth 기반 연결된 서비스를 기반으로 하는 조각이 14일마다 한 번 이상 실행된 경우 90일 |

tooavoid/resolve이 오류를 hello를 사용 하 여 권한을 다시 부여 **Authorize** 때 hello 단추 **토큰이 만료 되** hello 연결 된 서비스를 다시 배포 합니다. 다음과 같은 코드를 사용하여 프로그래밍 방식으로 **sessionId** 및 **권한 부여** 속성의 값을 생성할 수도 있습니다.

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

참조 [AzureDataLakeStoreLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), 및 [AuthorizationSessionGetResponse 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) 세부 정보에 대 한 항목 hello Data Factory 클래스 hello 코드에 사용 정보 합니다. 에 대 한 참조 추가: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll hello WindowsFormsWebAuthenticationDialog 클래스에 대 한 합니다. 

## <a name="data-lake-analytics-u-sql-activity"></a>Data Lake Analytics U-SQL 작업
다음 JSON 코드 조각은 hello 파이프라인 데이터 레이크 분석 U-SQL 작업을 정의 합니다. hello 활동 정의 참조 toohello 앞에서 만든 연결 된 Azure Data Lake 분석 서비스입니다.   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

hello 다음 표에서 설명 특정 toothis이 작동 하는 속성의 이름 및 설명 합니다. 

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| type |너무 hello 유형 속성을 설정 해야**DataLakeAnalyticsU SQL**합니다. |예 |
| scriptPath |Hello U-SQL 스크립트를 포함 하는 경로 toofolder 합니다. Hello 파일의 이름은 대/소문자 구분입니다. |아니요(스크립트를 사용하는 경우) |
| scriptLinkedService |Hello 스크립트 toohello 데이터 팩터리를 포함 하는 hello 저장소를 연결 하는 연결 된 서비스 |아니요(스크립트를 사용하는 경우) |
| script |scriptPath 및 scriptLinkedService를 지정하는 대신 인라인 스크립트를 지정합니다. 예: `"script": "CREATE DATABASE test"` |아니요(scriptPath 및 scriptLinkedService를 사용하는 경우) |
| degreeOfParallelism |hello 최대 노드 수는 동시에 toorun hello 작업을 사용 합니다. |아니요 |
| 우선 순위 |먼저 어떤 작업에서 대기 중인 모든 선택한 toorun 해야를 결정 합니다. hello 낮은 hello 수치로 hello hello 우선 순위가 높습니다. |아니요 |
| 매개 변수 |Hello U-SQL 스크립트의 매개 변수 |아니요 |
| runtimeVersion | Hello U-SQL 엔진 toouse의 런타임 버전 | 아니요 | 
| compilationMode | <p>U-SQL의 컴파일 모드 다음 값 중 하나여야 합니다.</p> <ul><li>**의미 체계:** 의미 체계 검사 및 필수 온전성 검사만 수행합니다.</li><li>**전체:** 구문 검사, 최적화, 코드 생성 등을 포함 하 여 hello 전체 컴파일을 수행 합니다.</li><li>**SingleBox:** TargetType 설정 tooSingleBox와 hello 전체 컴파일을 수행 합니다.</li></ul><p>이 속성에 대 한 값을 지정 하지 않으면, hello 서버 hello 최적의 컴파일 모드를 결정 합니다. </p>| 아니요 | 

참조 [SearchLogProcessing.txt 스크립트 정의](#sample-u-sql-script) hello 스크립트 정의 대 한 합니다. 

## <a name="sample-input-and-output-datasets"></a>샘플 입력 및 출력 데이터 집합
### <a name="input-dataset"></a>입력 데이터 집합
이 예제에서는 hello 입력된 데이터는 Azure 데이터 레이크 저장소 (SearchLog.tsv hello datalake/입력 폴더에 파일)에 상주합니다. 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a>출력 데이터 집합
이 예제에서는 hello U-SQL 스크립트에서 생성 하는 hello 출력 데이터는 Azure 데이터 레이크 저장소 (datalake/출력 폴더)에 저장 됩니다. 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a>샘플 Azure Data Lake Store 연결된 서비스
Azure 데이터 레이크 저장소 연결 된 hello 입/출력 데이터 집합에서 사용 하는 서비스는 hello 샘플의 hello 정의 다음과 같습니다. 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

참조 [Azure 데이터 레이크 저장소에서 데이터 tooand 이동](data-factory-azure-datalake-connector.md) 문서 JSON 속성에 대 한 설명입니다. 

## <a name="sample-u-sql-script"></a>샘플 U-SQL 스크립트

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

에 대 한 값을 hello  **@in**  및  **@out**  hello U-SQL 스크립트의 매개 변수는 전달 되 동적으로 ADF hello 'parameters' 섹션을 사용 하 여 합니다. Hello 파이프라인 정의 hello 'parameters' 섹션을 참조 합니다.

Hello Azure Data Lake 분석 서비스에서 실행 되는 hello 작업에 대 한 파이프라인 정의에 degreeOfParallelism 및 우선 순위와 같은 기타 속성을 지정할 수 있습니다.

## <a name="dynamic-parameters"></a>동적 매개 변수
시작 및 종료 hello 샘플 파이프라인 정의에서 매개 변수 하드 코드 된 값으로 할당 됩니다. 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

호스팅하려는 가능한 toouse 동적 매개 변수입니다. 예: 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

이 경우 hello /datalake/input 폴더에서 입력된 파일은 여전히 획득 하 고 hello /datalake/output 폴더에 출력 파일이 생성 됩니다. hello 파일 이름은 hello 조각 시작 시간에 기반 하는 동적입니다.  

