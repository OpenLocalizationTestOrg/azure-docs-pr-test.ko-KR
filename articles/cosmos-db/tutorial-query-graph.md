---
title: "Azure Cosmos DB에서 aaaHow tooquery 그래프 데이터? | Microsoft Docs"
description: "Azure Cosmos DB에서 tooquery 그래프 데이터에 알아봅니다"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a>어떻게 azure Cosmos DB: tooquery로 Graph API (미리 보기)를 hello?

hello Azure Cosmos DB [Graph API](graph-introduction.md) 지원 (미리 보기) [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) 쿼리 합니다. 이 문서는 예제 문서를 제공 하 고 시작한 tooget를 쿼리 합니다. 자세한 참조 정보 Gremlin hello에 제공 된 [Gremlin 지원](gremlin-support.md) 문서.

이 문서에서는 다음 작업 hello를 다룹니다. 

> [!div class="checklist"]
> * Gremlin을 사용한 데이터 쿼리

## <a name="prerequisites"></a>필수 조건

이러한 쿼리 toowork Azure Cosmos DB 계정이 없고 hello 컨테이너에 대 한 그래프 데이터를 해야 합니다. 이들 중 하나라도 없는가요? 전체 hello [5 분 퀵 스타트](create-graph-dotnet.md) 또는 hello [개발자 자습서](tutorial-query-graph.md) toocreate 계정 데이터베이스를 채웁니다. Hello 다음 hello를 사용 하 여 쿼리를 실행할 수 있습니다 [Azure Cosmos DB.NET 그래프 라이브러리](graph-sdk-dotnet.md), [Gremlin 콘솔](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), 또는 즐겨 찾는 Gremlin 드라이버입니다.

## <a name="count-vertices-in-hello-graph"></a>Hello 그래프에 꼭 짓 점 수

다음 코드 조각 hello toocount hello 그래프에 꼭 짓 점 수가 hello 하는 방법을 보여 줍니다.

```
g.V().count()
```

## <a name="filters"></a>필터

Gremlin의를 사용 하 여 필터를 수행할 수 있습니다 `has` 및 `hasLabel` 둘을 결합 하 여 단계를 사용 하 여 `and`, `or`, 및 `not` toobuild 보다 복잡 한 필터링 합니다. Azure Cosmos DB는 빠른 쿼리를 위해 꼭짓점과 각도 내의 모든 속성에 대해 스키마 독립적 인덱싱을 제공합니다.

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>프로젝션

Hello를 사용 하 여 hello 쿼리 결과에서 특정 속성을 프로젝션 할 수 `values` 단계:

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>관련 가장자리 및 꼭짓점 찾기

지금까지 모든 데이터베이스에서 작동하는 쿼리 연산자만 보았습니다. Toonavigate toorelated 가장자리과 꼭지점 필요한 경우 그래프를 신속 하 고 통과 작업에 대 한 효율적인 있습니다. Thomas의 친구들을 모두 찾아 보겠습니다. Gremlin의를 사용 하 여 수행 `outE` Thomas에서 모든 hello 송신 가장자리 toofind 시작한 다음 Gremlin의를 사용 하 여 해당 가장자리부터 꼭지점에 toohello 통과 `inV` 단계:

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

hello 다음 쿼리는 두 가지 홉 toofind 수행 Thomas' "친구의 친구"를 호출 하 여 모든 `outE` 및 `inV` 두 배입니다. 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

더 복잡 한 쿼리를 작성 하 고 Gremlin를 비롯 한 혼합 필터를 사용 하 여 반복을 수행 하는 식, hello를 사용 하 여 강력한 그래프 순회 논리 구현 `loop` 단계 및 hello를 사용 하 여 구현 조건부 탐색 `choose` 단계입니다. [Gremlin 지원](gremlin-support.md)에서 수행할 수 있는 작업에 대해 자세히 알아보세요!

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음 작업을 수행 하면:

> [!div class="checklist"]
> * 방법에 대해 배웠습니다 tooquery 그래프를 사용 하 여 

이제 진행할 수 있습니다 다음 자습서 toolearn toohello 어떻게 toodistribute 데이터 전체적으로 합니다.

> [!div class="nextstepaction"]
> [전 세계로 데이터 배포](tutorial-global-distribution-documentdb.md)