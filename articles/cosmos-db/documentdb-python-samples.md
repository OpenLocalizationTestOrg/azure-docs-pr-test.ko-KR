---
title: "Azure Cosmos DB에 대 한 API aaaDocumentDB Python 예제 | Microsoft Docs"
description: "CRUD 작업을 비롯한 Azure Cosmos DB의 일반적인 작업에 대한 github의 Python 예제를 찾습니다."
keywords: "Python 예제"
services: cosmos-db
author: moderakh
manager: jhubbard
editor: monicar
documentationcenter: python
ms.assetid: 7f4f8db3-e9db-4645-92ef-7819d486a349
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2016
ms.author: moderakh
ms.openlocfilehash: d8f240782b0997f2d32b68d310dc6f4ff6cb36d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-examples"></a>Azure Cosmos DB Python 예제
> [!div class="op_single_selector"]
> * [.NET 예제](documentdb-dotnet-samples.md)
> * [Node.js 예제](documentdb-nodejs-samples.md)
> * [Python 예제](documentdb-python-samples.md)
> * [Azure 코드 샘플 갤러리](https://azure.microsoft.com/documentation/samples/?service=documentdb)
> 
> 

샘플 솔루션을 CRUD 작업 및 Azure Cosmos DB 리소스에서 기타 일반적인 작업을 수행 하는 hello에 포함 된 [azure-documentdb-python](https://github.com/Azure/azure-documentdb-python/tree/master/samples) GitHub 리포지토리 합니다. 이 문서는 다음을 제공합니다.

* 각 hello Python 예제 프로젝트 파일에서 링크 toohello 작업입니다. 
* 링크 toohello 관련 API 참조 콘텐츠입니다.

**필수 구성 요소**

1. Azure 계정 toouse 이러한 Python 예제 필요합니다.
   * 할 수 있습니다 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/): 크레딧을 얻게 유료 Azure 서비스 아웃 tootry 사용할 수 있으며 사용 후에 최대 hello 계정 등에 사용 하 여 웹 사이트와 같은 Azure 서비스를 해제 합니다. 명시적으로 설정을 변경 하 고 청구 toobe 요청 하지 않는 한 신용 카드, 청구 됩니다 하지 않습니다.
     * [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.
2. 또한 hello 해야 [Python SDK](documentdb-sdk-python.md)합니다. 
   
   > [!NOTE]
   > 각 샘플은 자체 포함되며 자체를 설정하고 자체를 정리합니다. 이와 같이 hello 샘플 발급 여러 번 호출 너무[document_client 합니다. CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html)합니다. 구독에 영향을 주는 이렇게 될 때마다 생성 되 고 hello 컬렉션의 hello 성능 계층 당 사용량의 1 시간에 대 한 청구 됩니다. 
   > 
   > 

## <a name="database-examples"></a>데이터베이스 예제
hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement/Program.py) 파일의 hello [DatabaseManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/DatabaseManagement) 프로젝트 tooperform hello 다음 작업 방법을 보여 줍니다.

| 작업 | API 참조 |
| --- | --- |
| [데이터베이스 만들기](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L65-L76) |[document_client.CreateDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [데이터베이스에 대한 계정 쿼리](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L49-L62) |[document_client.QueryDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [ID에서 데이터베이스 읽기](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L79-L96) |[document_client.ReadDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [계정에 대한 데이터베이스 나열](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L99-L110) |[document_client.ReadDatabases](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |
| [데이터베이스 삭제](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/DatabaseManagement/Program.py#L113-L126) |[document_client.DeleteDatabase](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html) |

## <a name="collection-examples"></a>컬렉션 예제
hello [Program.py](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement/Program.py) 파일의 hello [CollectionManagement](https://github.com/Azure/azure-documentdb-python/tree/master/samples/CollectionManagement) 프로젝트 tooperform hello 다음 작업 방법을 보여 줍니다.

| 작업 | API 참조 |
| --- | --- |
| [컬렉션 만들기](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L84-L135) |[document_client.CreateCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [데이터베이스에서 모든 컬렉션의 목록 읽기](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L198-L225) |[document_client.ListCollections](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [ID에서 컬렉션 가져오기](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L178-L195) |[document_client.ReadCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [컬렉션의 성능 계층 가져오기](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L139-L161) |[DocumentQueryable.QueryOffers](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [컬렉션의 성능 계층 변경](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L163-L175) |[document_client.ReplaceOffer](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |
| [컬렉션 삭제](https://github.com/Azure/azure-documentdb-python/blob/d78170214467e3ab71ace1a7400f5a7fa5a7b5b0/samples/CollectionManagement/Program.py#L212-L225) |[document_client.DeleteCollection](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.document_client.html#CreateCollection) |

