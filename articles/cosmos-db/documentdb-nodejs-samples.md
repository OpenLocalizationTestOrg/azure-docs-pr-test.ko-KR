---
title: "Azure Cosmos DB aaaNode.js 예 | Microsoft Docs"
description: "CRUD 작업을 비롯한 Azure Cosmos DB의 일반적인 작업에 대한 github의 Node.js 예제를 찾습니다."
keywords: "Node.js 예제"
services: cosmos-db
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: nodejs
ms.assetid: d87d97be-47a5-4928-8d46-a541fbb33213
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: moderakh
ms.openlocfilehash: 55c8ebb9ff425aeeaa49fd0738649d33556a1635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-examples"></a>Azure Cosmos DB Node.js 예제
> [!div class="op_single_selector"]
> * [.NET 예제](documentdb-dotnet-samples.md)
> * [Node.js 예제](documentdb-nodejs-samples.md)
> * [Python 예제](documentdb-python-samples.md)
> * [Azure 코드 샘플 갤러리](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

샘플 솔루션을 CRUD 작업 및 Azure Cosmos DB 리소스에서 기타 일반적인 작업을 수행 하는 hello에 포함 된 [azure-documentdb-nodejs](https://github.com/Azure/azure-documentdb-node/tree/master/samples) GitHub 리포지토리 합니다. 이 문서는 다음을 제공합니다.

* 각 hello Node.js 예제 프로젝트 파일에서 링크 toohello 작업입니다.
* 링크 toohello 관련 API 참조 콘텐츠입니다.

**필수 구성 요소**

1. Azure 계정 toouse 이러한 Node.js 예제 필요합니다.
   * 할 수 있습니다 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/): 크레딧을 얻게 유료 Azure 서비스 아웃 tootry 사용할 수 있으며 사용 후에 최대 hello 계정 등에 사용 하 여 웹 사이트와 같은 Azure 서비스를 해제 합니다. 명시적으로 설정을 변경 하 고 청구 toobe 요청 하지 않는 한 신용 카드, 청구 됩니다 하지 않습니다.
     * [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.
2. 또한 hello 해야 [Node.js SDK](documentdb-sdk-node.md)합니다.
   
   > [!NOTE]
   > 각 샘플은 자체 포함되며 자체를 설정하고 자체를 정리합니다. 이와 같이 hello 샘플 발급 여러 번 호출 너무[DocumentClient.createCollection](http://azure.github.io/azure-documentdb-node/DocumentClient.html#createCollection)합니다. 구독에 영향을 주는 이렇게 될 때마다 생성 되 고 hello 컬렉션의 hello 성능 계층 당 사용량의 1 시간에 대 한 청구 됩니다.
   > 
   > 

## <a name="database-examples"></a>데이터베이스 예제
hello [app.js](https://github.com/Azure/azure-documentdb-node/blob/master/samples/DatabaseManagement/app.js) 파일의 hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-node/tree/master/samples/DatabaseManagement) 프로젝트 tooperform hello 다음 작업 방법을 보여 줍니다.

| 작업 | API 참조 |
| --- | --- |
| [데이터베이스 만들기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.DatabaseManagement/app.js#L121-L131) |[DocumentClient.createDatabase](http://azure.github.io/azure-documentdb-node/DocumentClient.html#createDatabase) |
| [데이터베이스에 대한 계정 쿼리](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.DatabaseManagement/app.js#L146-L171) |[DocumentClient.queryDatabases](http://azure.github.io/azure-documentdb-node/DocumentClient.html#queryDatabases) |
| [ID에서 데이터베이스 읽기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.DatabaseManagement/app.js#L89-L99) |[DocumentClient.readDatabase](http://azure.github.io/azure-documentdb-node/DocumentClient.html#readDatabase) |
| [계정에 대한 데이터베이스 나열](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.DatabaseManagement/app.js#L111-L119) |[DocumentClient.readDatabases](http://azure.github.io/azure-documentdb-node/DocumentClient.html#readDatabases) |
| [데이터베이스 삭제](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.DatabaseManagement/app.js#L133-L144) |[DocumentClient.deleteDatabase](http://azure.github.io/azure-documentdb-node/DocumentClient.html#deleteDatabase) |

## <a name="collection-examples"></a>컬렉션 예제
hello [app.js](https://github.com/Azure/azure-documentdb-node/blob/master/samples/CollectionManagement/app.js) 파일의 hello [CollectionManagement](https://github.com/Azure/azure-documentdb-node/tree/master/samples/CollectionManagement) 프로젝트 tooperform hello 다음 작업 방법을 보여 줍니다.

| 작업 | API 참조 |
| --- | --- |
| [컬렉션 만들기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.CollectionManagement/app.js#L97-L118) |[DocumentClient.createCollection](http://azure.github.io/azure-documentdb-node/DocumentClient.html#createCollection) |
| [데이터베이스에서 모든 컬렉션의 목록 읽기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.CollectionManagement/app.js#L120-L130) |[DocumentClient.readCollections](http://azure.github.io/azure-documentdb-node/DocumentClient.html#readCollections) |
| [_self에서 컬렉션 가져오기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.CollectionManagement/app.js#L132-L141) |[DocumentClient.readCollection](http://azure.github.io/azure-documentdb-node/DocumentClient.html#readCollection) |
| [ID에서 컬렉션 가져오기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.CollectionManagement/app.js#L143-L156) |[DocumentClient.readCollection](http://azure.github.io/azure-documentdb-node/DocumentClient.html#readCollection) |
| [컬렉션의 성능 계층 가져오기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.CollectionManagement/app.js#L158-L186) |[DocumentQueryable.queryOffers](http://azure.github.io/azure-documentdb-node/DocumentClient.html#queryOffers) |
| [컬렉션의 성능 계층 변경](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.CollectionManagement/app.js#L188-L202) |[DocumentClient.replaceOffer](http://azure.github.io/azure-documentdb-node/DocumentClient.html#replaceOffer) |
| [컬렉션 삭제](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.CollectionManagement/app.js#L204-L215) |[DocumentClient.deleteCollection](http://azure.github.io/azure-documentdb-node/DocumentClient.html#deleteCollection) |

## <a name="document-examples"></a>문서 예제
hello [app.js](https://github.com/Azure/azure-documentdb-node/blob/master/samples/DocumentManagement/app.js) 파일의 hello [DocumentManagement](https://github.com/Azure/azure-documentdb-node/tree/master/samples/DocumentManagement) 프로젝트 tooperform hello 다음 작업 방법을 보여 줍니다.

| 작업 | API 참조 |
| --- | --- |
| [문서 만들기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.DocumentManagement/app.js#L153-L177) |[DocumentClient.createDocument](http://azure.github.io/azure-documentdb-node/DocumentClient.html#createDocument) |
| [컬렉션에 대 한 피드 읽기 hello 문서](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.DocumentManagement/app.js#L179-L189) |[DocumentClient.readDocument](http://azure.github.io/azure-documentdb-node/DocumentClient.html#readDocument) |
| [ID로 문서 읽기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.DocumentManagement/app.js#L191-L201) |[DocumentClient.readDocument](http://azure.github.io/azure-documentdb-node/DocumentClient.html#readDocument) |
| [문서가 변경된 경우에만 문서 읽기](https://github.com/Azure/azure-documentdb-node/blob/0778eadea7abb2af41e8c22a239dc872c584f421/samples/DocumentManagement/app.js#L79-L107) |[DocumentClient.readDocument](http://azure.github.io/azure-documentdb-node/DocumentClient.html#readDocument)<br/>[RequestOptions.accessCondition](http://azure.github.io/azure-documentdb-node/global.html#RequestOptions) |
| [문서에 대한 쿼리](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.DocumentManagement/app.js#L82-L110) |[DocumentClient.queryDocuments](http://azure.github.io/azure-documentdb-node/DocumentClient.html#queryDocuments) |
| [문서 바꾸기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.DocumentManagement/app.js#L112-L119) |[DocumentClient.replaceDocument](http://azure.github.io/azure-documentdb-node/DocumentClient.html#replaceDocument) |
| [조건부 ETag 검사로 문서 바꾸기](https://github.com/Azure/azure-documentdb-node/blob/0778eadea7abb2af41e8c22a239dc872c584f421/samples/DocumentManagement/app.js#L147-L164) |[DocumentClient.replaceDocument](http://azure.github.io/azure-documentdb-node/DocumentClient.html#replaceDocument)<br/>[RequestOptions.accessCondition](http://azure.github.io/azure-documentdb-node/global.html#RequestOptions) |
| [문서 삭제](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.DocumentManagement/app.js#L122-L133) |[DocumentClient.deleteDocument](http://azure.github.io/azure-documentdb-node/DocumentClient.html#deleteDocument) |

## <a name="indexing-examples"></a>청구 예제
hello [app.js](https://github.com/Azure/azure-documentdb-node/blob/master/samples/IndexManagement/app.js) 파일의 hello [IndexManagement](https://github.com/Azure/azure-documentdb-node/tree/master/samples/IndexManagement) 프로젝트 tooperform hello 다음 작업 방법을 보여 줍니다.

| 작업 | API 참조 |
| --- | --- |
| [기본 인덱싱을 사용하여 컬렉션 만들기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.IndexManagement/app.js#L657-L701) |[DocumentClient.createCollection](http://azure.github.io/azure-documentdb-node/DocumentClient.html#createCollection) |
| [수동으로 특정 문서 인덱스](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.IndexManagement/app.js#L185-L238) |[RequestOptions.indexingDirective: 'include'](http://azure.github.io/azure-documentdb-node/global.html#RequestOptions) |
| [수동으로 특정 문서 hello 인덱스에서 제외](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.IndexManagement/app.js#L120-L183) |[RequestOptions.indexingDirective: 'exclude'](http://azure.github.io/azure-documentdb-node/global.html#RequestOptions) |
| [대량 가져오기에 대한 지연 인덱싱 사용 또는 많은 컬렉션 읽기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.IndexManagement/app.js#L240-L269) |[IndexingMode.Lazy](http://azure.github.io/azure-documentdb-node/global.html#IndexingMode) |
| [인덱싱에 문서의 특정 경로 포함](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.IndexManagement/app.js#L433-L444) |[IndexingPolicy.IncludedPaths](http://azure.github.io/azure-documentdb-node/global.html#IndexingPolicy) |
| [인덱싱에서 특정 경로 제외](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.IndexManagement/app.js#L427-L450) |[IndexingPolicy.ExcludedPath](http://azure.github.io/azure-documentdb-node/global.html#IndexingPolicy) |
| [범위 작업 중 문자열 경로에서 검색 허용](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.IndexManagement/app.js#L271-L347) |[FeedOptions.EnableScanInQuery](http://azure.github.io/azure-documentdb-node/global.html#FeedOptions) |
| [문자열 경로에 범위 인덱스 만들기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.IndexManagement/app.js#L349-L425) |[IndexKind.Range](http://azure.github.io/azure-documentdb-node/global.html#IndexKind), [IndexingPolicy](http://azure.github.io/azure-documentdb-node/global.html#IndexingPolicy), [DocumentClient.queryDocument](http://azure.github.io/azure-documentdb-node/DocumentClient.html#queryDocument) |
| [기본 indexPolicy로 컬렉션을 만든 다음 이 온라인 업데이트](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.IndexManagement/app.js#L519-L614) |[DocumentClient.createCollection](http://azure.github.io/azure-documentdb-node/DocumentClient.html#createCollection)<br> [DocumentClient.replaceCollection#replaceCollection](http://azure.github.io/azure-documentdb-node/DocumentClient.html) |

인덱싱에 대한 자세한 내용은 [Azure Cosmos DB 인덱싱 정책](indexing-policies.md)을 참조하세요.

## <a name="server-side-programming-examples"></a>서버 쪽 프로그래밍 예제
hello [app.js](https://github.com/Azure/azure-documentdb-node/blob/master/samples/ServerSideScripts/app.js) 파일의 hello [ServerSideScripts](https://github.com/Azure/azure-documentdb-node/tree/master/samples/ServerSideScripts) 프로젝트 tooperform hello 다음 작업 방법을 보여 줍니다.

| 작업 | API 참조 |
| --- | --- |
| [저장 프로시저 만들기](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.ServerSideScripts/app.js#L44-L71) |[DocumentClient.createStoredProcedure](http://azure.github.io/azure-documentdb-node/DocumentClient.html#createStoredProcedure) |
| [저장 프로시저 실행](https://github.com/Azure/azure-documentdb-node/blob/ef53e5f6707a5dc45920fb6ad54d9c7e008a6c18/samples/DocumentDB.Samples.ServerSideScripts/app.js#L73-L90) |[DocumentClient.executeStoredProcedure](http://azure.github.io/azure-documentdb-node/DocumentClient.html#executeStoredProcedure) |

서버 쪽 프로그래밍에 대한 자세한 내용은 [Azure Cosmos DB 서버 쪽 프로그래밍: 저장 프로시저, 데이터베이스 트리거 및 UDF](programming.md)를 참조하세요.

## <a name="partitioning-examples"></a>분할 예제
hello [app.js](https://github.com/Azure/azure-documentdb-node/blob/master/samples/Partitioning/app.js) 파일의 hello [Partitioning](https://github.com/Azure/azure-documentdb-node/tree/master/samples/Partitioning) 프로젝트 tooperform hello 다음 작업 방법을 보여 줍니다.

| 작업 | API 참조 |
| --- | --- |
| [HashPartitionResolver 사용](https://github.com/Azure/azure-documentdb-node/blob/ce0fc3c4e70b0279091a1e03620a668d93a14fc2/samples/Partitioning/app.js#L53-L103) |[HashPartitionResolver](http://azure.github.io/azure-documentdb-node/HashPartitionResolver.html) |

Azure Cosmos DB에서 데이터를 분할하는 방법에 대한 자세한 내용은 [Azure Cosmos DB에서 데이터 분할 및 크기 조정](partition-data.md)을 참조하세요.

