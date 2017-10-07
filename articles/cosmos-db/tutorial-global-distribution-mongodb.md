---
title: "MongoDB API에 대 한 aaaAzure Cosmos DB 글로벌 메일 자습서 | Microsoft Docs"
description: "어떻게 MongoDB API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello에 대해 알아봅니다."
services: cosmos-db
keywords: "전역 배포, MongoDB"
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
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a>어떻게 MongoDB API를 사용 하 여 toosetup Azure Cosmos DB 글로벌 메일 hello

이 문서에서는 toouse hello Azure 포털 toosetup Azure Cosmos DB 글로벌 배포 하 고 다음 hello MongoDB API를 사용 하 여를 연결 하는 방법을 보여줍니다.

이 문서에서는 다음 작업 hello를 다룹니다. 

> [!div class="checklist"]
> * Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.
> * Hello를 사용 하 여 글로벌 배포를 구성 [MongoDB API](mongodb-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a>Hello MongoDB API를 사용 하 여 국가별 설치 확인
MongoDB toorun hello에 대 한 API 내에서 전역 구성을 검사 하는 double의 가장 간단한 방법은 hello *isMaster()* hello Mongo 셸 명령을 합니다.

Mongo Shell에서 다음을 수행합니다.

   ```
      db.isMaster()
   ```
   
결과 예:

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a>Hello MongoDB API를 사용 하 여 tooa 기본 영역 연결

hello MongoDB API를 사용 하면 있습니다 toospecify 세계적으로 분산 된 데이터베이스에 대 한 컬렉션의 읽기 기본 설정. 컬렉션의 읽기 기본 설정 지정 너무 권장 읽기 대기 시간 및 전역 높은 가용성, 낮은 둘 다에 대 한*가장 가까운*합니다. 기본 설정을 읽기 *가장 가까운* hello 가장 가까운 영역에서 구성 된 tooread 됩니다.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

응용 프로그램을 기본 읽기/쓰기가 지역과 보조 지역에 대 한 재해 복구 (DR) 시나리오에 대 한 컬렉션의 읽기 기본 설정 지정 너무는 것이 좋습니다*선호 하는 보조*합니다. 읽기 기본 설정을 *선호 하는 보조* hello 기본 지역에 사용할 수 없는 경우 hello 보조 지역에서 구성 된 tooread는 합니다.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

마지막으로 지정 하면 읽기 영역 toomanually와 같은 경우입니다. Hello 지역 태그 읽기 기본 설정 내에서 설정할 수 있습니다.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

이것으로 끝이며, 이 자습서를 완료했습니다! 읽어 toomanage 전역적으로 복제 된 계정의 일관성 hello 하는 방법을 학습할 수 있는 [Azure Cosmos DB의 일관성 수준](consistency-levels.md)합니다. 그리고 Azure Cosmos DB에서 전역 데이터베이스 복제가 작동하는 방법에 대한 자세한 내용은 [Azure Cosmos DB를 사용하여 전역적으로 데이터 배포](distribute-data-globally.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음 작업을 수행 하면:

> [!div class="checklist"]
> * Hello Azure 포털을 사용 하 여 글로벌 배포를 구성 합니다.
> * Hello DocumentDB Api를 사용 하 여 글로벌 배포를 구성 합니다.

다음 자습서 toolearn toohello 이제 진행할 수 있습니다 어떻게 사용 하 여 로컬로 toodevelop hello Azure Cosmos DB의 로컬 에뮬레이터입니다.

> [!div class="nextstepaction"]
> [Hello 에뮬레이터를 사용 하 여 로컬 개발](local-emulator.md)
