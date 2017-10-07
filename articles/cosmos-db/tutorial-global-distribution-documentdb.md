---
title: "DocumentDB API에 대 한 aaaAzure Cosmos DB 글로벌 메일 자습서 | Microsoft Docs"
description: "어떻게 DocumentDB API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello에 대해 알아봅니다."
services: cosmos-db
keywords: "전역 배포, DocumentDB"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a>어떻게 DocumentDB API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello

이 문서에서는 toouse hello Azure 포털 toosetup Azure Cosmos DB 글로벌 배포 하 고 다음 hello DocumentDB API를 사용 하 여를 연결 하는 방법을 보여줍니다.

이 문서에서는 다음 작업 hello를 다룹니다. 

> [!div class="checklist"]
> * Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.
> * Hello를 사용 하 여 글로벌 배포를 구성 [DocumentDB Api](documentdb-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a>Hello DocumentDB API를 사용 하 여 tooa 기본 영역 연결

순서 tootake 활용에 [글로벌 메일](distribute-data-globally.md), 클라이언트 응용 프로그램에서 hello tooperform 문서 작업을 사용 하는 기본 설정 목록은 영역 toobe 정렬를 지정할 수 있습니다. Hello 연결 정책을 설정 하 여이 작업을 수행할 수 있습니다. Hello Azure Cosmos DB 계정 구성에 따라 현재 국가별 가용성 및 hello 기본 설정 목록 지정 hello 대부분 최적의 끝점 hello DocumentDB SDK tooperform 쓰기 및 읽기 작업에 의해 선택 됩니다.

이 기본 설정 목록은 hello DocumentDB Sdk를 사용 하는 연결을 초기화할 때 지정 됩니다. hello Sdk에는 선택적 매개 변수 "PreferredLocations" 동의 Azure 지역의 정렬된 된 목록입니다.

hello SDK에서는 모든 쓰기 toohello 현재 쓰기 지역 자동으로 전송 합니다.

모든 읽기 hello PreferredLocations 목록에서 첫 번째 사용 가능한 지역 toohello 전송 됩니다. Hello 요청이 실패할 경우 hello 클라이언트 hello 목록 toohello 다음 영역을 아래로 실패를 업데이트 하 고 등 됩니다.

hello Sdk PreferredLocations에 지정 된 hello 지역에서 tooread를 시도 합니다. 따라서 예를 들어 3 개의 영역에서 데이터베이스 계정 hello를 사용할 수 있어도 hello 클라이언트만 두 hello 쓰기 이외의 영역에 대 한 지정 PreferredLocations 다음 읽기는 제공 장애 조치의 hello 경우에도 hello 쓰기 영역 외부로.

hello 응용 프로그램 hello 현재 쓰기 끝점을 확인 하 고 확인 하는 중 두 가지 속성인 WriteEndpoint 및 ReadEndpoint SDK 버전 1.8 이상 사용할 수 있는 hello SDK가 선택한 끝점을 읽을 수 있습니다.

Hello PreferredLocations 속성을 설정 하지 않으면 모든 요청은 hello 현재 쓰기 영역에서 처리 됩니다.

## <a name="net-sdk"></a>.NET SDK
hello SDK 코드 변경 없이 사용할 수 있습니다. 이 경우 SDK hello 자동으로 다이렉트 모두 읽기 및 toohello 현재 쓰기 영역을 씁니다.

Hello.NET SDK 1.8 이상 버전에서는 hello DocumentClient 생성자에 대 한 hello ConnectionPolicy 매개 변수에는 Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations 라는 속성이 있습니다. 이 속성은 컬렉션 `<string>` 형식이며 지역 이름 목록을 포함합니다. hello에 대 한 hello 지역 이름 열당 hello 문자열 값에 형식을 지정할 [Azure 지역] [ regions] 처음으로 페이지를 앞 이나 뒤 hello 공백 없이 및 문자를 각각 마지막 합니다.

hello 현재 쓰기 및 읽기 끝점 각각 DocumentClient.WriteEndpoint 및 DocumentClient.ReadEndpoint에서 제공 됩니다.

> [!NOTE]
> hello 끝점에 대 한 hello Url 수명이 긴 상수로 간주 되지 않아야 합니다. hello 서비스는 언제 든 지 이러한 업데이트할 수 있습니다. hello SDK는이 변경 내용을 자동으로 처리합니다.
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a>NodeJS, JavaScript 및 Python SDK
hello SDK 코드 변경 없이 사용할 수 있습니다. 이 경우 SDK는 자동으로 연결 하는 hello 모두 읽기 및 쓰기 toohello 현재 쓰기 지역.

버전 1.8 및 각 SDK의 나중 hello ConnectionPolicy 매개 변수에서 hello DocumentClient 생성자 DocumentClient.ConnectionPolicy.PreferredLocations 라는 새 속성에 대 한 합니다. 이 매개 변수는 지역 이름 목록을 가지는 문자열 배열입니다. hello에 대 한 hello 지역 이름 열당 hello 이름의 형식은 [Azure 지역] [ regions] 페이지. Hello 편의 개체 AzureDocuments.Regions에에서 미리 정의 된 hello 상수를 사용할 수도 있습니다.

hello 현재 쓰기 및 읽기 끝점 각각 DocumentClient.getWriteEndpoint 및 DocumentClient.getReadEndpoint에서 제공 됩니다.

> [!NOTE]
> hello 끝점에 대 한 hello Url 수명이 긴 상수로 간주 되지 않아야 합니다. hello 서비스는 언제 든 지 이러한 업데이트할 수 있습니다. hello SDK는이 변경 내용을 자동으로 처리 합니다.
>
>

다음은 NodeJS/Javascript의 코드 예제입니다. Hello Python 및 Java에 따라 동일한 패턴입니다.

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a>REST (영문)
데이터베이스 계정을 수 있게 된 여러 지역에서 되 면 클라이언트 hello 다음 URI에 GET 요청을 수행 하 여 가용성을 쿼리할 수 있습니다.

    https://{databaseaccount}.documents.azure.com/

hello 서비스는 영역 및 hello 복제본에 대 한 자신의 해당 Azure Cosmos DB 끝점 Uri의 목록을 반환 합니다. hello 현재 쓰기 지역 hello 응답에 표시 됩니다. 그런 다음 hello 클라이언트 hello 이후 모든 REST API 요청에 대 한 적절 한 끝점을 다음과 같이 선택할 수 있습니다.

예제 응답

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* 모든 PUT, POST 및 DELETE 요청 다음에 야 toohello 표시 된 URI를 작성 합니다.
* 모든 GETs 및 다른 읽기 전용 요청 (예: 쿼리) hello 클라이언트의 선택한 tooany 끝점 전환 될 수 있습니다.

쓰기 요청 tooread 전용 영역 HTTP 오류 코드 403 ("사용할 수 없음")와 함께 실패 합니다.

Hello 쓰기 지역 후 변경 되 면 hello 클라이언트의 초기 검색 단계에서 후속 씁니다 toohello 이전 쓰기 지역 HTTP 오류 코드 403 ("사용할 수 없음")와 함께 실패 합니다. 클라이언트 hello 다음 구해야 hello 지역 목록이 다시 tooget hello 업데이트 쓰기 영역 합니다.

이것으로 끝이며, 이 자습서를 완료했습니다! 읽어 toomanage 전역적으로 복제 된 계정의 일관성 hello 하는 방법을 학습할 수 있는 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)합니다. 그리고 Azure Cosmos DB에서 전역 데이터베이스 복제가 작동하는 방법에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포](distribute-data-globally.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음 작업을 수행 하면:

> [!div class="checklist"]
> * Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.
> * Hello DocumentDB Api를 사용 하 여 글로벌 배포를 구성 합니다.

다음 자습서 toolearn toohello 이제 진행할 수 있습니다 어떻게 사용 하 여 로컬로 toodevelop hello Azure Cosmos DB의 로컬 에뮬레이터입니다.

> [!div class="nextstepaction"]
> [Hello 에뮬레이터를 사용 하 여 로컬 개발](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

