---
title: "Azure Cosmos DB에 대 한 aaaProvision 처리량 | Microsoft Docs"
description: "프로그램 Azure Cosmos DB containsers, 컬렉션, 그래프 및 테이블에 대 한 처리량 tooset 프로 비전 하는 방법을 알아봅니다."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>Azure Cosmos DB 컨테이너에 대한 처리량 설정

Hello Azure 포털에서에서 사용자 Azure Cosmos DB 컨테이너에 대 한 처리량을 설정 하거나 hello client Sdk를 사용 하 여 수 있습니다. 

다음 표에서 hello 컨테이너에 사용할 수 있는 hello 처리량을 보여 줍니다.

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>단일 파티션 컨테이너</strong></p></td>
            <td valign="top"><p><strong>분할된 컨테이너</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>최소 처리량</p></td>
            <td valign="top"><p>초당 요청 단위 400개</p></td>
            <td valign="top"><p>초당 요청 단위 2,500개</p></td>
        </tr>
        <tr>
            <td valign="top"><p>최대 처리량</p></td>
            <td valign="top"><p>초당 요청 단위 10,000개</p></td>
            <td valign="top"><p>Unlimited</p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a>hello Azure 포털을 사용 하 여 tooset hello 처리량

1. 새 창에서 열고 hello [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽된 모음에서 **Azure Cosmos DB**, 하거나 클릭 **더 서비스** hello 맨 아래에 다음 스크롤하여 너무**데이터베이스**, 클릭 하 고 **Azure Cosmos DB**.
3. Cosmos DB 계정을 선택합니다.
4. Hello 새 창에서 클릭 **데이터 탐색기 (미리 보기)** hello 탐색 메뉴에 있습니다.
5. Hello 새 창에서 데이터베이스와 컨테이너를 확장 한 다음 클릭 **배율 및 설정**합니다.
6. Hello 새 창에서 hello에 hello 새 처리량 값을 입력 **처리량** 상자를 선택한 다음 클릭 **저장**합니다.

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a>.NET 용 hello DocumentDB API를 사용 하 여 tooset hello 처리량

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a>처리량 FAQ

**내 처리량 tooless 400RU/s 보다를 설정할 수 있습니까?**

400RU/s는 hello 최소 처리량 (2500 000RU/s는 분할 된 컬렉션에 대 한 최소 hello) Cosmos DB 단일 파티션 컬렉션에 사용할 수 있습니다. 단위 000RU/s 간격 100 개에 설정 되어 있지만 처리량 설정할 수 없습니다 too100 000RU/s 이나 값 400RU/s 보다 작은 요청 합니다. 비용 효율적인 메서드 toodevelop 찾고 Cosmos DB를 테스트 하는 경우 무료 hello를 사용할 수 있습니다 [Azure Cosmos DB 에뮬레이터](local-emulator.md), 비용 없이 로컬로 배포할 수 있는 합니다. 

**Hello MongoDB API를 사용 하 여 througput를 설정 하려면 어떻게 해야 합니까?**

MongoDB API 확장 tooset 처리량 되지 않습니다. hello 좋습니다 toouse hello DocumentDB API와 같이 [.NET에 대 한 hello DocumentDB API를 사용 하 여 tooset hello 처리량](#set-throughput-sdk)합니다.

## <a name="next-steps"></a>다음 단계

프로 비전 및 Cosmos DB와 함께 진행 중인 지구 단위에 대해 자세히 toolearn 참조 [분할과 Cosmos DB와 함께 크기 조정](partition-data.md)합니다.
