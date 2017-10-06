---
title: "Azure 데이터 레이크 저장소에서 데이터 tooand aaaCopy | Microsoft Docs"
description: "자세한 내용은 방법 toocopy 데이터 tooand 데이터 레이크 저장소에서 Azure 데이터 팩터리를 사용 하 여"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a>데이터 팩터리를 사용 하 여 데이터 tooand 데이터 레이크 저장소에서 복사
이 문서에서는 설명 방법에서 Azure 데이터 레이크 저장소에서 Azure Data Factory toomove 데이터 tooand toouse 복사 작업입니다. Hello에 기반 [데이터 이동 활동](data-factory-data-movement-activities.md) 문서 복사 작업으로 데이터 이동에 대 한 개요입니다.

## <a name="supported-scenarios"></a>지원되는 시나리오
데이터를 복사할 수 **Azure 데이터 레이크 저장소에서** toohello 데이터 저장소를 다음:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooAzure 데이터 레이크 저장소**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> 복사 작업을 사용하여 파이프라인을 만들기 전에 Data Lake Store 계정을 만듭니다. 자세한 내용은 [Azure Data Lake Store 시작](../data-lake-store/data-lake-store-get-started-portal.md)을 참조하세요.

## <a name="supported-authentication-types"></a>지원되는 인증 형식
데이터 레이크 저장소 커넥터 hello 이러한 인증 유형을 지원합니다.
* 서비스 주체 인증
* 사용자 자격 증명(OAuth) 인증 

특히 예약된 데이터 복사의 경우 서비스 주체 인증을 사용하는 것이 좋습니다. 사용자 자격 증명 인증의 경우 토큰 만료 동작이 발생할 수 있습니다. 구성 세부 정보 참조 hello [연결 된 서비스 속성](#linked-service-properties) 섹션.

## <a name="get-started"></a>시작
다른 도구/API를 사용하여 Azure Data Lake Store 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인 toocopy 데이터는 toouse hello **복사 마법사**합니다. Hello 복사 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 자습서를 참조 하십시오. [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md)합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. **데이터 팩터리**를 만듭니다. 데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 
2. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다. 예를 들어 Azure blob 저장소 tooan Azure 데이터 레이크 저장소에서에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink Azure 저장소 계정 및 Azure 데이터 레이크 저장소 tooyour 데이터 팩터리입니다. 데이터 레이크 저장소 특정 tooAzure 있는 연결 된 서비스 속성을 참조 하십시오. [연결 된 서비스 속성](#linked-service-properties) 섹션. 
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. Hello 마지막 단계에서 언급 한 hello 예제에서는 데이터 집합 toospecify hello blob 컨테이너 및 hello 입력된 데이터를 포함 된 폴더를 만듭니다. 고 hello blob 저장소에서 복사 하는 hello 데이터를 보유 하는 hello 데이터 레이크 저장소의 다른 데이터 집합 toospecify hello 폴더 및 파일 경로 만듭니다. 특정 tooAzure 데이터 레이크 저장소는 데이터 집합 속성을 참조 하십시오. [데이터 집합 속성](#dataset-properties) 섹션.
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 앞에서 언급 한 hello 예제에서는 사용 BlobSource 원본과 AzureDataLakeStoreSink 싱크도 hello 복사 작업에 대 한 합니다. 마찬가지로, Azure 데이터 레이크 저장소 tooAzure Blob 저장소에서에서 복사 하는 경우 AzureDataLakeStoreSource 및 사용 BlobSink hello 복사 활동에서. 복사 활동 속성을 특정 tooAzure 데이터 레이크 저장소를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션. 에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.  

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  샘플은 Azure 데이터 레이크 저장소에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-data-lake-store) 이 문서의 섹션.

다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooData Lake 저장소에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
연결 된 서비스는 데이터 저장소 tooa 데이터 팩터리를 연결합니다. 형식의 연결 된 서비스를 만들면 **AzureDataLakeStore** toolink 데이터 레이크 저장소 데이터 tooyour 데이터 팩터리입니다. 다음 표에서 hello JSON 요소 특정 tooData Lake 저장소 연결 된 서비스에 설명 합니다. 서비스 주체와 사용자 자격 증명 인증 중에서 선택할 수 있습니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| **type** | 너무 hello 유형 속성을 설정 해야**AzureDataLakeStore**합니다. | 예 |
| **dataLakeStoreUri** | Hello Azure 데이터 레이크 저장소 계정에 대 한 정보입니다. 이 정보는 hello 다음 형식 중 하나: `https://[accountname].azuredatalakestore.net/webhdfs/v1` 또는 `adl://[accountname].azuredatalakestore.net/`합니다. | 예 |
| **subscriptionId** | Azure 구독 ID toowhich hello Data Lake 저장소 계정에 속해 있습니다. | 싱크에 필요 |
| **resourceGroupName** | Azure 리소스 그룹 이름 toowhich hello Data Lake 저장소 계정에 속해 있습니다. | 싱크에 필요 |

### <a name="service-principal-authentication-recommended"></a>서비스 주체 인증(권장)
toouse 서비스 보안 주체 인증 레지스터 것 hello Azure Active Directory (Azure AD) 및 권한 부여의 응용 프로그램 엔터티 tooData 레이크 스토어에 액세스 합니다. 자세한 단계는 [서비스 간 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)을 참조하세요. 사용 되는 값을 다음 hello 기록 toodefine hello 연결 된 서비스:
* 응용 프로그램 UI
* 응용 프로그램 키 
* 테넌트 ID

> [!IMPORTANT]
> Hello 복사 마법사 tooauthor 데이터 파이프라인을 사용 하는 경우 hello 서비스 보안 주체에 부여 했는지 확인 적어도 **판독기** hello Data Lake 저장소 계정에 대 한 액세스 제어 (id 및 액세스 관리)에 역할입니다. 또한, 적어도 hello 서비스 사용자 권한을 부여 **읽기 + Execute** 권한 tooyour 데이터 레이크 저장소 루트 ("/") 및 해당 하위 항목입니다. 그렇지 않으면 "hello 지정한 자격 증명에 사용할 수 없습니다." hello 메시지를 표시 될 수 있습니다.<br/><br/>
만들거나 Azure AD에서 서비스 사용자를 업데이트 한 후 hello 변경 tootake 효과 대 일 분 정도 걸릴 수 있습니다. Hello 서비스 사용자와 데이터 레이크 저장소 액세스 제어 목록 (ACL) 구성을 확인 하십시오. "Hello 지정한 자격 증명에 사용할 수 없습니다" hello 메시지를 계속 나타나면 잠시 기다린 후 다시 시도 하십시오.

Hello 다음과 같은 속성을 지정 하 여 서비스 사용자 인증을 사용 합니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| **servicePrincipalId** | Hello 응용 프로그램의 클라이언트 ID를 지정 | 예 |
| **servicePrincipalKey** | Hello 응용 프로그램의 키를 지정 합니다. | 예 |
| **테넌트** | 응용 프로그램에 속한 아래 hello 테 넌 트 정보 (도메인 이름 또는 테 넌 트 ID)를 지정 합니다. Hello Azure 포털의 오른쪽 위 모서리 hello에에서 hello 마우스 호버 하 여 검색할 수 있습니다. | 예 |

**예제: 서비스 주체 인증**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>사용자 자격 증명 인증
또는 hello 다음과 같은 속성을 지정 하 여 사용자 자격 증명 인증 toocopy에서 또는 tooData Lake 저장소를 사용할 수 있습니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| **권한 부여** | Hello 클릭 **Authorize** hello 데이터 팩터리 편집기 단추를 선택한 hello 자동 생성 된 권한 부여 URL toothis 속성을 할당 하 여 자격 증명을 입력 합니다. | 예 |
| **sessionId** | Hello OAuth 권한 부여 세션에서 OAuth 세션 ID입니다. 각 세션 ID는 고유하고 한 번만 사용될 수 있습니다. 이 설정은 hello 데이터 팩터리 편집기를 사용 하는 경우 자동으로 생성 됩니다. | 예 |

**예제: 사용자 자격 증명 인증**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a>토큰 만료
hello를 사용 하 여 생성 하는 인증 코드를 hello **Authorize** 단추 시간이 지난 후에 만료 됩니다. hello 메시지의 뒤에 해당 hello 인증 토큰이 만료 되었습니다.을 의미 합니다.

자격 증명 작업 오류: invalid_grant - AADSTS70002: 자격 증명의 유효성 검사 오류. AADSTS70008: hello 액세스 권한 부여가 만료 되었거나 해지 제공 합니다. 추적 ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 상관관계 ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 타임스탬프: 2015-12-15 21-09-31Z

hello 다음 표에 다양 한 유형의 사용자 계정의 hello 만료 시간:


| 사용자 유형 | 다음 시간 후에 만료 |
|:--- |:--- |
| Azure Active Directory에서 관리되지 *않는* 사용자 계정(예: @hotmail.com 또는 @live.com) |12시간 |
| Azure Active Directory에서 관리되는 사용자 계정 |hello 마지막 조각 실행 한 후 14 일 <br/><br/>OAuth 기반 연결된 서비스를 기반으로 하는 조각이 14일마다 한 번 이상 실행된 경우 90일 |

Hello 토큰 만료 시간 전에 암호를 변경한 경우 hello 토큰 즉시 만료 됩니다. 이 섹션의 앞에서 언급 한 hello 메시지에 표시 됩니다.

Hello를 사용 하 여 hello 계정 권한을 다시 부여한 다음 수 **Authorize** hello 토큰 tooredeploy hello 만료 되 면 단추는 연결 된 서비스입니다. Hello에 대 한 값을 생성할 수도 있습니다 **sessionId** 및 **권한 부여** 다음 코드를 사용 하 여 프로그래밍 방식으로 속성 hello:


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
Hello 코드에서 사용 되는 hello 데이터 팩터리 클래스에 대 한 자세한 참조 hello [AzureDataLakeStoreLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), 및 [ AuthorizationSessionGetResponse 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) 항목입니다. 추가 참조 tooversion `2.9.10826.1824` 의 `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` hello에 대 한 `WindowsFormsWebAuthenticationDialog` hello 코드에서 사용 되는 클래스입니다.

## <a name="dataset-properties"></a>데이터 집합 속성
데이터 레이크 저장소에서 데이터 집합 toorepresent 입력된 데이터 toospecify 설정한 hello **형식** hello 데이터 집합의 속성 너무**AzureDataLakeStore**합니다. 집합 hello **linkedServiceName** hello 데이터 레이크 저장소의 hello dataset toohello 이름의 속성이 연결 된 서비스입니다. JSON 섹션 및 데이터 집합 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. **구조**, **가용성** 및 **정책**과 JSON의 데이터 집합 섹션은 모든 데이터 집합 형식(예: SQL Database, Azure Blob, Azure 테이블)에 대해 유사합니다. hello **typeProperties** 섹션은 데이터 집합의 각 유형에 대해 서로 다른 및 위치와 hello 데이터 저장소에 hello 데이터 형식과 같은 정보를 제공 합니다. 

hello **typeProperties** 형식의 데이터 집합에 대 한 섹션 **AzureDataLakeStore** hello 다음과 같은 속성을 포함 합니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| **folderPath** |경로 toohello 컨테이너 및 데이터 레이크 저장소의 폴더입니다. |예 |
| **fileName** |Azure 데이터 레이크 저장소의 hello 파일의 이름입니다. hello **fileName** 속성은 선택 사항이 고 대/소문자 구분 합니다. <br/><br/>지정 하는 경우 **fileName**, hello 특정 파일에서 작동 하는 hello 활동 (복사본 포함).<br/><br/>때 **fileName** 를 지정 하지 않으면에 모든 파일을 포함 하는 복사 **folderPath** hello 입력된 데이터 집합의 합니다.<br/><br/>때 **fileName** 출력 데이터 집합에 지정 되지 않은 및 **preserveHierarchy** hello hello 생성 된 파일의 이름이 데이터 hello 형태로 활동 싱크에 지정 되지 않은. _Guid_.txt'. 예제: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |아니요 |
| **partitionedBy** |hello **partitionedBy** 속성은 선택 사항입니다. 동적 경로 toospecify와 시계열 데이터에 대 한 파일 이름을 사용할 수 있습니다. 예를 들어 **folderPath**는 매시간 데이터에 대한 매개 변수화됩니다. 세부 정보 및 예제 참조 [partitionedBy 속성 hello](#using-partitionedby-property)합니다. |아니요 |
| **format** | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, 및  **ParquetFormat**합니다. 집합 hello **형식** 아래의 속성 **형식** tooone 다음이 값 중입니다. 자세한 내용은 참조 hello [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [JSON 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC 형식](data-factory-supported-file-and-compression-formats.md#orc-format), 및 [Parquet 형식 ](data-factory-supported-file-and-compression-formats.md#parquet-format) hello의 섹션에서는 [Azure Data Factory에서 지 원하는 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서. <br><br> Toocopy 파일 "으로-는" 파일 기반 저장소 (이진 복사), 간에 hello 건너뜁니다 `format` 두 입력 및 출력 데이터 집합 정의에 섹션. |아니요 |
| **compression** | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. **Optimal** 및 **Fastest** 수준이 지원됩니다. 자세한 내용은 [Azure Data Factory에서 지원되는 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |

### <a name="hello-partitionedby-property"></a>hello partitionedBy 속성
동적으로 지정할 수 **folderPath** 및 **fileName** hello 사용 하 여 시계열 데이터에 대 한 속성 **partitionedBy** 속성, 데이터 팩터리 함수 및 시스템 변수입니다. 자세한 내용은 참조 hello [Azure 데이터 팩터리-함수 및 시스템 변수](data-factory-functions-variables.md) 문서.


다음 예에서는, hello에 `{Slice}` hello hello 데이터 팩터리 시스템 변수 값으로 대체 됩니다 `SliceStart` hello 형식 지정 (`yyyyMMddHH`). hello 이름 `SliceStart` hello 조각의 toohello 시작 시간을 나타냅니다. hello `folderPath` 속성은 다음과 같이 각 조각에 대 한 다른 `wikidatagateway/wikisampledataout/2014100103` 또는 `wikidatagateway/wikisampledataout/2014100104`합니다.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

다음 예에서는, hello 연도, 월, 일 및 시간을 hello에 `SliceStart` hello에서 사용 되는 개별 변수로 추출 `folderPath` 및 `fileName` 속성:
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
시계열 데이터 집합에 대 한 자세한 내용은 예약 및 조각이 참조 hello [Azure Data Factory에서 데이터 집합](data-factory-create-datasets.md) 및 [Data Factory 예약 및 실행](data-factory-scheduling-and-execution.md) 문서입니다. 


## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

hello에 사용할 수 있는 속성 hello **typeProperties** 각 활동 유형에 활동의 섹션에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

**AzureDataLakeStoreSource** hello에서 속성을 다음 hello 지원 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| **recursive** |Hello 데이터 읽는지 재귀적으로 hello 지정 된 폴더 또는 hello 하위 폴더에서 나타냅니다. |True(기본값), False |아니요 |


**AzureDataLakeStoreSink** hello 다음과 같은 hello에 대 한 속성을 지 원하는 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| **copyBehavior** |Hello 복사 동작을 지정합니다. |<b>PreserveHierarchy</b>: hello 대상 폴더에서 hello 파일 계층 구조를 유지 합니다. hello 소스 파일 toosource 폴더의 상대 경로 동일한 toohello 대상 파일 tootarget 폴더의 상대 경로입니다.<br/><br/><b>FlattenHierarchy</b>: hello 원본 폴더에서 모든 파일은 hello 첫 번째 수준의 hello 대상 폴더에 만들어집니다. hello 대상 파일은 자동으로 생성 된 이름으로 만들어집니다.<br/><br/><b>MergeFiles</b>: hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다. Hello 파일이 나 blob 이름을 지정 하는 경우 hello 병합 된 파일 이름은 hello 지정 된 이름이입니다. 그렇지 않으면 hello 파일 이름이 자동으로 생성 됩니다. |아니요 |

### <a name="recursive-and-copybehavior-examples"></a>recursive 및 copyBehavior 예제
이 섹션에서는 hello 재귀 및 copyBehavior 값의 다른 조합에 대 한 hello 복사 작업의 결과 동작을 설명 합니다.

| recursive | copyBehavior | 결과 동작 |
| --- | --- | --- |
| true |preserveHierarchy |원본 폴더의 Folder1 구조를 다음 hello로: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 대상 폴더가 Folder1 hello 소스로 구조체 같은 hello로 만들어집니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| true |flattenHierarchy |원본 폴더의 Folder1 구조를 다음 hello로: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 대상 Folder1 hello 구조를 다음으로 만들어집니다. <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File3에 대해 자동 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File4에 대해 자동 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File5에 대해 자동 생성된 이름 |
| true |mergeFiles |원본 폴더의 Folder1 구조를 다음 hello로: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 대상 Folder1 hello 구조를 다음으로 만들어집니다. <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1, File2, File3, File4 및 File5의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다. |
| false |preserveHierarchy |원본 폴더의 Folder1 구조를 다음 hello로: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/><br/>File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다. |
| false |flattenHierarchy |원본 폴더의 Folder1 구조를 다음 hello로:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름<br/><br/><br/>File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다. |
| false |mergeFiles |원본 폴더의 Folder1 구조를 다음 hello로:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1과 File2의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다. File1에 대해 자동으로 생성된 이름<br/><br/>File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다. |

## <a name="supported-file-and-compression-formats"></a>지원되는 파일 및 압축 형식
자세한 내용은 참조 hello [Azure Data Factory에서 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서.

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a>데이터 레이크 저장소에서 데이터 tooand 복사 하기 위한 JSON 예제
hello 예제 따르는 샘플 JSON 정의 제공 합니다. 이러한 샘플 정의 toocreate 파이프라인을 사용 하 여 hello를 사용 하 여 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 예제에서는 보여 어떻게 hello 데이터 레이크 저장소 및 Azure Blob 저장소에서 데이터 tooand toocopy 합니다. 그러나 데이터를 복사할 수 있습니다 _직접_ 지원 hello 싱크 hello 소스 tooany 중 어디에서 든 합니다. 자세한 내용은 hello에서 "지원 되는 데이터 저장소와 형식" hello 섹션 참조 [복사 작업을 사용 하 여 데이터를 이동](data-factory-data-movement-activities.md) 문서.  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a>예: Azure Blob 저장소 tooAzure 데이터 레이크 저장소에서에서 데이터를 복사 합니다.
이 섹션의 예제 코드에서는 hello를 보여 줍니다.

* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
* [AzureDataLakeStore](#linked-service-properties) 형식의 연결된 서비스입니다.
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
* [AzureDataLakeStore](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.
* [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 및 [AzureDataLakeStoreSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 예제 방식을 보여 시계열 데이터를 Azure Blob 저장소 1 시간 마다 tooData Lake 저장소를 복사 합니다. 

**Azure 저장소 연결된 서비스**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**Azure Data Lake Store 연결된 서비스**

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> 구성 세부 정보 참조 hello [연결 된 서비스 속성](#linked-service-properties) 섹션.
>

**Azure Blob 입력 데이터 집합**

다음 예제는 hello에서 데이터를 선택 새 blob에서 매시간 (`"frequency": "Hour", "interval": 1`). hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 연도, 월 및 hello 시작 시간의 일 부분을 사용합니다. hello 파일 이름은 hello 시간 hello 부분의 시작 시간을 사용 합니다. hello `"external": true` 설정 알립니다 hello 데이터 팩터리 서비스는 hello 테이블 데이터 팩터리 외부 toohello 및 hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Azure Data Lake Store 출력 데이터 집합**

다음 예에서는 복사본 데이터 레이크 저장소 tooData 번호입니다. 새 데이터를 복사할 1 시간 마다 tooData Lake 저장소입니다.

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


**Blob 원본 및 Data Lake Store 싱크를 사용하는 파이프라인의 복사 작업**

다음 예제는 hello, hello 파이프라인에 구성 된 복사 활동 toouse hello 입력 및 출력 데이터 집합입니다. hello 복사 작업은 예약 된 toorun 마다 시간입니다. Hello 파이프라인 JSON 정의에서 hello `source` 형식이 너무 설정`BlobSource`, 및 hello `sink` 형식이 너무 설정`AzureDataLakeStoreSink`합니다.

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
        ]
    }
}
```

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a>예: Azure 데이터 레이크 저장소 tooan Azure blob에서에서 데이터를 복사 합니다.
이 섹션의 예제 코드에서는 hello를 보여 줍니다.

* [AzureDataLakeStore](#linked-service-properties) 형식의 연결된 서비스입니다.
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
* [AzureDataLakeStore](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
* [AzureDataLakeStoreSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 코드 시계열 데이터 복사 Data Lake 저장소 tooan Azure blob에서에서 1 시간 마다 합니다. 

**Azure Data Lake Store 연결된 서비스**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> 구성 세부 정보 참조 hello [연결 된 서비스 속성](#linked-service-properties) 섹션.
>

**Azure 저장소 연결된 서비스**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Azure Data Lake 입력 데이터 집합**

이 예제에서는 설정 `"external"` 너무`true` 알리고 hello Data Factory 서비스가 해당 hello 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
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
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
        "policy": {
              "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
              }
        }
      }
}
```
**Azure Blob 출력 데이터 집합:**

다음 예제는 hello, 데이터 작성 된 새 blob tooa 매시간 (`"frequency": "Hour", "interval": 1`). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 연도, 월, 일 및 시간 부분의 hello 시작 시간을 사용합니다.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Azure Data Lake Store 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업**

다음 예제는 hello, hello 파이프라인에 구성 된 복사 활동 toouse hello 입력 및 출력 데이터 집합입니다. hello 복사 작업은 예약 된 toorun 마다 시간입니다. Hello 파이프라인 JSON 정의에서 hello `source` 형식이 너무 설정`AzureDataLakeStoreSource`, 및 hello `sink` 형식이 너무 설정`BlobSink`합니다.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

Hello 복사 활동 정의의 hello 원본 데이터 집합 toocolumns hello 싱크 데이터 집합의 열을 매핑할 수도 있습니다. 자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
복사 활동 성능에 영향을 주는 hello 요소에 대해 toolearn와 방법을 toooptimize, hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) 문서.
