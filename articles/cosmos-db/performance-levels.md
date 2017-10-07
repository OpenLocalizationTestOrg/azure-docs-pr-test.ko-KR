---
title: "API aaaDocumentDB 성능 수준 | Microsoft Docs"
description: "어떻게 DocumentDB API 성능 수준을 사용 하면 컨테이너 당 기준 tooreserve 처리량에 알아봅니다."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a>Hello S1, S2, S3 성능 수준에 사용 중지

> [!IMPORTANT] 
> hello S1, S2, S3 성능 수준이이 문서에 설명 된 사용이 중지 되는 및 새 DocumentDB API 계정에 대해 사용할 수 없게 됩니다.
>

이 문서에서는 S1, S2, S3 성능 수준에 대해 간략하게 설명 하 고 이러한 성능 수준을 사용 하는 hello 컬렉션 되는 방식이 마이그레이션된 toosingle 파티션 컬렉션 2017 년 8 월 1 일에서 설명 합니다. 이 문서를 읽은 후 다음 질문 수 tooanswer hello 수 있습니다.

- [이유는 hello S1, S2, S3 성능 수준을 사용이 중지 되 고 있습니까?](#why-retired)
- [단일 파티션 컬렉션 및 분할 된 컬렉션 비교 하면 어떻게 toohello S1, S2, S3 성능 수준을?](#compare)
- [작업 중단 없이 toodo tooensure toomy 데이터에 액세스할 필요?](#uninterrupted-access)
- [Hello 마이그레이션 후 내 컬렉션은 어떻게 변경 됩니까?](#collection-change)
- [어떻게 청구 내 변경 마이그레이션된 toosingle 파티션 컬렉션 난 후?](#billing-change)
- [저장 용량이 10GB 이상 필요한 경우 어떻게 해야 합니까?](#more-storage-needed)
- [2017 년 8 월 1 하기 전에 hello S1, S2, S3 성능 수준 간에 변경할 수 있나요?](#change-before)
- [내 컬렉션이 마이그레이션된 시기는 어떻게 알 수 있습니까?](#when-migrated)
- [Hello S1, S2, S3 성능 수준 toosingle 파티션 컬렉션 직접에서 마이그레이션하려면 어떻게 해야 합니까?](#migrate-diy)
- [EA 고객에게 미치는 영향은?](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a>이유는 hello S1, S2, S3 성능 수준을 사용이 중지 되 고 있습니까?

hello S1, S2, S3 성능 수준 하지 제공 hello 유연성을 DocumentDB API 컬렉션에서 제공 하는 않습니다. Hello S1, S2, S3 성능 수준으로 두 hello 처리량 및 저장소 용량 미리 설정한 및 탄력성을 제공 하지 않습니다. Azure Cosmos DB 이제 제공 hello 기능 toocustomize 처리량 및 저장소를 필요에 따라 기능 tooscale에 훨씬 더 많은 유연성을 제공 합니다.

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a>단일 파티션 컬렉션 및 분할 된 컬렉션 비교 하면 어떻게 toohello S1, S2, S3 성능 수준을?

다음 표에서 hello 단일 파티션 컬렉션, 분할 된 컬렉션 및 S1, S2, S3 성능 수준에서 제공 하는 hello 처리량 및 저장소 옵션을 비교 합니다. 다음은 미국 동부 2 지역의 예입니다.

|   |분할된 컬렉션|단일 파티션 컬렉션|S1|S2|S3|
|---|---|---|---|---|---|
|최대 처리량|Unlimited|10,000RU/s|250RU/s|1,000RU/s|2,500RU/s|
|최소 처리량|2,500RU/s|400RU/s|250RU/s|1,000RU/s|2,500RU/s|
|최대 저장소|Unlimited|10 GB|10 GB|10 GB|10 GB|
|가격(월별)|처리량: $6/100RU/s<br><br>저장소: $0.25/GB|처리량: $6/100RU/s<br><br>저장소: $0.25/GB|$25(미화)|$50(미화)|$100(미화)|

EA 고객입니까? 그렇다면 [EA 고객에게 미치는 영향은?](#ea-customer)을 참조하세요.

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a>작업 중단 없이 toodo tooensure toomy 데이터에 액세스할 필요?

Nothing 이면 Cosmos DB 수에 대 한 hello 마이그레이션 처리 합니다. S1, S2 또는 S3 컬렉션을 설정한 경우 사용자의 현재 컬렉션 마이그레이션된 tooa 단일 파티션 컬렉션에 2017 년 7 월 31 됩니다. 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a>Hello 마이그레이션 후 내 컬렉션은 어떻게 변경 됩니까?

S1 컬렉션을 사용 하는 경우 400 000RU/s 처리량을 사용 하 여 마이그레이션된 tooa 단일 파티션 컬렉션 수 있습니다. 400RU/s은 단일 파티션 컬렉션으로 사용할 수 있는 가장 낮은 처리량 hello입니다. 그러나 단일 파티션 컬렉션은 지불 동일 S1 컬렉션으로 된 hello 약 hello에 400RU/s 및 250 000RU/s – 하지에 대 한 지불 하 게는 하므로 hello 비용이 추가 150 000RU/s 사용 가능한 tooyou를 hello 합니다.

S2 컬렉션을 사용 하는 경우 1, 000RU/s를 사용 하 여 마이그레이션된 tooa 단일 파티션 컬렉션 수 있습니다. 변경 tooyour 처리량 수준이 없는지를 확인할 수 있습니다.

S3 컬렉션을 사용 하는 경우, 000RU/s 2.5를 사용 하 여 마이그레이션된 tooa 단일 파티션 컬렉션 수 있습니다. 변경 tooyour 처리량 수준이 없는지를 확인할 수 있습니다.

각각의이 경우에 컬렉션 마이그레이션된 후를 수 수 toocustomize 처리량 수준을 아니면 필요한 tooprovide 대기 시간이 짧은 액세스 tooyour 사용자로 확장 및 축소 하는 것입니다. toochange hello 처리량 수준 컬렉션을 마이그레이션한 후 단순히 Cosmos DB 계정을 열고 hello Azure 포털에서에서 배율, 컬렉션을 선택를 hello 스크린 샷 다음 그림과 같이 hello 처리량 수준을 조정 합니다.

![어떻게 tooscale 처리량 hello Azure 포털](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a>어떻게 청구 내 변경 마이그레이션된 toohello 단일 파티션 컬렉션 난 후?

가정 하 고 10 S1 컬렉션, 1GB의 저장소에 대해 각각, hello 미국 동부 지역에 있고 400 RU/sec (hello 최소 수준)에서 이러한 10 S1 컬렉션 too10 단일 파티션 컬렉션을 마이그레이션하세요. 청구서 달에 대 한 hello 10 단일 파티션 컬렉션을 유지 하는 경우 다음과 같이 표시 됩니다.

![10 개의 컬렉션에 대 한 가격 책정 S1 too10 컬렉션을 비교 하는 방법을 단일 파티션 컬렉션에 대 한 가격을 사용 하 여](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a>저장 용량이 10GB 이상 필요한 경우 어떻게 해야 합니까?

데이터 tooa 사실상 사용 하 여 컬렉션을 분할 하는 hello Cosmos DB 데이터 마이그레이션 도구 toomigrate S1, S2 또는 S3 성능 수준에 따라 컬렉션 하는지 여부는 모두 10GB의 사용 가능한 저장 공간, 단일 파티션 컬렉션을 사용할 수 있습니다. 무제한 저장 합니다. 분할 된 컬렉션의 hello 이점에 대 한 정보를 참조 하십시오. [Partitioning 및 Azure Cosmos DB에 크기 조정](documentdb-partition-data.md)합니다. 방법에 대 한 내용은 toomigrate S1, S2, S3, 또는 단일 파티션 컬렉션 분할 tooa 컬렉션 참조 [toopartitioned 단일 파티션 컬렉션에서 마이그레이션](documentdb-partition-data.md#migrating-from-single-partition)합니다. 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a>2017 년 8 월 1 하기 전에 hello S1, S2, S3 성능 수준 간에 변경할 수 있나요?

기존 계정만 S1, S2, S3 성능 수 toochange 되며 hello 포털을 통해 또는 프로그래밍 방식으로 성능 수준의 계층을 변경 합니다. 2017 년 8 월 1 하 여 S1, S2, hello 및 S3 성능 수준을 사용할 수 없습니다. S1, S3, 또는 S3 tooa 단일 파티션 컬렉션에서 변경할 S1, S2 또는 S3 성능 수준 toohello 반환할 수 없습니다.

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a>내 컬렉션이 마이그레이션된 시기는 어떻게 알 수 있습니까?

hello 마이그레이션 2017 년 7 월 31에서 발생 합니다. 컬렉션 hello S1, S2를 사용 하 여 또는 S3 성능 수준 hello Cosmos DB 팀 연락을 드릴 전자 메일을 통해 hello 마이그레이션 수행 되기 전에 합니다. 2017 년 8 월 1에 hello 마이그레이션이 완료 되 면 Azure 포털 hello 컬렉션 표준 가격 책정을 사용 하도록 표시 됩니다.

![어떻게 tooconfirm 사용자 컬렉션에 toohello 표준 가격 책정 계층 마이그레이션](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a>Hello S1, S2, S3 성능 수준 toosingle 파티션 컬렉션 직접에서 마이그레이션하려면 어떻게 해야 합니까?

Hello S1, S2에서 마이그레이션할 수 있습니다 및 S3 성능 수준이 toosingle 파티션 컬렉션 hello Azure 포털을 사용 하 여 또는 프로그래밍 방식으로 합니다. 단일 파티션 컬렉션으로 사용할 수 있는 hello 유연한 처리량 옵션 중에서 8 월 1 일 전에 직접 toobenefit에 이렇게 하려면 또는 2017 년 7 월 31에서 사용자 컬렉션을 마이그레이션할 예정입니다.

**hello Azure 포털을 사용 하 여 toomigrate toosingle 파티션 컬렉션**

1. Hello에 [ **Azure 포털**](https://portal.azure.com), 클릭 **Azure Cosmos DB**, hello Cosmos DB 계정 toomodify를 선택 합니다. 
 
    경우 **Azure Cosmos DB** Jumpbar hello를 클릭 하지는 >, 너무 스크롤하여**데이터베이스**을 선택 **Azure Cosmos DB**, 한 다음 hello DocumentDB 계정을 선택 합니다.  

2. Hello 리소스 메뉴에서 아래 **컨테이너**, 클릭 **배율**hello 컬렉션 toomodify hello 드롭 다운 목록에서 선택한 다음 클릭 **가격 책정 계층**합니다. 미리 정의된 처리량을 사용하는 계정은 S1, S2 또는 S3의 가격 책정 계층을 보유합니다.  Hello에 **가격 책정 계층을 선택** 블레이드에서 클릭 **표준** toochange toouser 정의 된 처리량을 클릭 하 고 **선택** toosave 변경 합니다.

    ![여기서 toochange hello 처리량 값을 보여 주는 hello 설정 블레이드의 스크린샷](./media/performance-levels/change-performance-set-thoughput.png)

3. Hello에 다시 **배율** 블레이드, hello **가격 책정 계층** 너무 변경**표준** 및 hello **처리량 (000RU/s)** 된 상자가 표시 됩니다는 400의 기본값입니다. 400에서 10,000 사이 집합 hello 처리량 [요청 단위](request-units.md)-초당 (000RU/s). hello **예상 월별 요금 청구** hello hello 맨 아래에 페이지 자동으로 업데이트 tooprovide hello 월별 비용의 추정치입니다. 

    >[!IMPORTANT] 
    > 변경 내용을 저장 하 고 이동 toohello 표준 가격 책정 계층을 롤백할 수 없습니다 toohello S1, S2 또는 S3 성능 수준입니다.

4. 클릭 **저장** toosave 변경 내용을 합니다.

    더 많은 처리량(10,000RU/s 초과) 또는 더 많은 저장소(10GB 초과)가 필요하다고 판단되는 경우 분할된 컬렉션을 만들 수 있습니다. 단일 파티션 컬렉션 분할 tooa 컬렉션 toomigrate 참조 [toopartitioned 단일 파티션 컬렉션에서 마이그레이션](documentdb-partition-data.md#migrating-from-single-partition)합니다.

    > [!NOTE]
    > S1, S2 또는 S3 tooStandard에서 변경 too2 분을 차지할 수 있습니다.
    > 
    > 

**hello.NET SDK를 사용 하 여 toomigrate toosingle 파티션 컬렉션**

컬렉션의 성능 수준 변경에 대한 다른 옵션은 SDK를 통하는 것입니다. 이 섹션에만 컬렉션의 성능 변경 적용를 사용 하 여 수준 우리의 [DocumentDB.NET API](documentdb-sdk-dotnet.md), 하지만 hello 프로세스는 우리의 다른 Sdk에 대 한 유사 합니다.

초당 요청 단위 000 hello 컬렉션 처리량 too5 변경에 대 한 코드 조각을 다음과 같습니다.
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

방문 [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview 추가 예제 및 우리의 제안 방법에 대 한 자세한 정보:

* [**ReadOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [**ReadOffersFeedAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [**ReplaceOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [**CreateOfferQuery**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a>EA 고객에게 미치는 영향은?

EA 고객은 자신의 현재 계약 hello 끝날 때까지 보호 가격 됩니다.

## <a name="next-steps"></a>다음 단계
가격 및 관리 Azure Cosmos DB를 사용 하 여 데이터에 대해 자세히 toolearn이 리소스를 살펴봅니다.

1.  [Cosmos DB의 데이터 분할](documentdb-partition-data.md). 분할 전략 tooscale를 원활 하 게 구현에 대 한 팁 뿐만 아니라 단일 파티션 컨테이너 및 분할 된 컨테이너의 hello 차이점을 이해 합니다.
2.  [Cosmos DB 가격 책정](https://azure.microsoft.com/pricing/details/cosmos-db/). 처리량을 프로 비전 하 고 저장소 사용의 hello 비용에 알아봅니다.
3.  [요청 단위](request-units.md) 읽기, 쓰기, 쿼리 예를 들어, 다른 작업 형식에 대 한 처리량의 hello 사용량을 이해 합니다.
