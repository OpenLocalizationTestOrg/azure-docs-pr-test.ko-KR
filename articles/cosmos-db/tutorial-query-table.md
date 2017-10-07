---
title: "Azure Cosmos DB에서 aaaHow tooquery 테이블 데이터? | Microsoft Docs"
description: "Azure Cosmos DB에서 tooquery 테이블 데이터에 알아봅니다"
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a>어떻게 azure Cosmos DB: tooquery 테이블 데이터를 사용 하 여 테이블 API (미리 보기)를 hello?

hello Azure Cosmos DB [테이블 API](table-introduction.md) OData가 지원 (미리 보기) 및 [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) (테이블)에 대 한 키/값 데이터에 대해 쿼리 합니다.  

이 문서에서는 다음 작업 hello를 다룹니다. 

> [!div class="checklist"]
> * Hello 테이블 API를 사용 하 여 데이터를 쿼리합니다.

hello 쿼리에서이 문서의 사용 샘플 다음 hello `People` 테이블:

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

Azure Cosmos DB hello Azure 테이블 저장소 Api와 호환 이기 때문에 참조 [쿼리 하는 테이블 및 엔터티] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) 방법을 사용 하 여 tooquery hello에 대 한 자세한 내용은 테이블 API입니다. 

Cosmos DB Azure에서 제공 하는 hello 프리미엄 기능에 대 한 자세한 내용은 참조 하십시오. [Azure Cosmos DB: 테이블 API](table-introduction.md) 및 [hello.net에서 테이블 API로 개발](tutorial-develop-table-dotnet.md)합니다. 

## <a name="prerequisites"></a>필수 조건

이러한 쿼리 toowork Azure Cosmos DB 계정이 없고 hello 컨테이너에 대 한 엔터티 데이터를 해야 합니다. 이들 중 하나라도 없는가요? 전체 hello [5 분 퀵 스타트](https://aka.ms/acdbtnetqs) 또는 hello [개발자 자습서](https://aka.ms/acdbtabletut) toocreate 계정 데이터베이스를 채웁니다.

## <a name="query-on-partitionkey-and-rowkey"></a>PartitionKey 및 RowKey에 대한 쿼리
Hello PartitionKey 및 RowKey 속성은 엔터티의 기본 키를 형성 하므로 특수 구문을 tooidentify hello 엔터티에 따라 hello를 사용할 수 있습니다. 

**쿼리**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**결과**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

Hello의 일부로 이러한 속성을 지정할 수 또는 `$filter` hello 다음 섹션에에서 나와 있는 것 처럼 옵션입니다. Hello 키 속성 이름 및 상수 값은 대/소문자 구분을 참고 합니다. Hello PartitionKey 및 RowKey 속성 모두는 형식 문자열입니다. 

## <a name="query-by-using-an-odata-filter"></a>OData 필터를 사용하여 쿼리
필터 문자열을 생성할 때는 다음 규칙에 유의하세요. 

* OData 프로토콜 사양 toocompare 속성 tooa 값 hello에 정의 된 hello 논리 연산자를 사용 합니다. 참고 속성 tooa 동적 값을 비교할 수 없습니다. Hello 식의 한 쪽은 상수 여야 합니다. 
* hello 속성 이름, 연산자 및 상수 값을 URL로 인코딩된 공백으로 구분 되어야 합니다. URL로 인코딩된 공백은 `%20`입니다. 
* Hello 필터 문자열의 모든 부분은 대/소문자를 구분 하지 않습니다. 
* hello hello 상수 값 이어야 합니다 hello 필터 tooreturn 유효한 결과에서 hello 속성으로 동일한 데이터 형식입니다. 지원 되는 속성 형식에 대 한 자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model)합니다. 

여기에서 toofilter PartitionKey hello 하는 방법을 보여 주는 예제 쿼리입니다 속성 OData를 사용 하 여 전자 메일 및 `$filter`합니다.

**쿼리**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

Tooconstruct 다양 한 데이터 형식에 대 한 식을 필터링 하는 방법에 대 한 자세한 내용은 참조 하십시오. [쿼리 하는 테이블 및 엔터티](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities)합니다.

**결과**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>LINQ를 사용하여 쿼리 
Toohello 해당 OData 쿼리 식으로 변환 하는 LINQ를 사용 하 여 쿼리할 수 있습니다. Toobuild 쿼리를 사용 하 여.NET SDK hello 하는 방법의 예는 다음과 같습니다.

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 hello 다음 작업을 수행 하면:

> [!div class="checklist"]
> * 사용 하 여 tooquery 테이블 API (미리 보기) hello 하는 방법을 배웠습니다. 

이제 진행할 수 있습니다 다음 자습서 toolearn toohello 어떻게 toodistribute 데이터 전체적으로 합니다.

> [!div class="nextstepaction"]
> [전 세계로 데이터 배포](tutorial-global-distribution-documentdb.md)
