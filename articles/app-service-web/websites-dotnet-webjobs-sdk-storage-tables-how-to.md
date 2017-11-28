---
title: "aaaHow toouse hello WebJobs SDK로 Azure 테이블 저장소"
description: "Toouse Azure 테이블 저장소 hello WebJobs SDK로 하는 방법에 대해 알아봅니다. 테이블을 만들고 추가 엔터티 tootables 기존 테이블을 읽을 합니다."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="6dd8c-104">Toouse Azure 테이블 저장소 hello WebJobs SDK로 하는 방법</span><span class="sxs-lookup"><span data-stu-id="6dd8c-104">How toouse Azure table storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="6dd8c-105">개요</span><span class="sxs-lookup"><span data-stu-id="6dd8c-105">Overview</span></span>
<span data-ttu-id="6dd8c-106">이 가이드를 사용 하 여 테이블 tooread 및 Azure 저장소 쓰기 보여 주는 C# 코드 샘플을 제공 [WebJobs SDK](websites-dotnet-webjobs-sdk.md) 버전 1.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-106">This guide provides C# code samples that show how tooread and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="6dd8c-107">hello 가이드 알고 있다고 가정 [toocreate 연결이 포함 된 Visual Studio에서 WebJob 프로젝트의 해당 지점 tooyour 저장소 계정 문자열 어떻게](websites-dotnet-webjobs-sdk-get-started.md) 또는 너무[여러 저장소 계정을](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="6dd8c-108">일부 hello 코드 조각 표시 hello `Table` 된 함수에 사용 된 특성 [수동으로 호출](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), 즉, hello 트리거 특성 중 하나를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-108">Some of hello code snippets show hello `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of hello trigger attributes.</span></span> 

## <span data-ttu-id="6dd8c-109"><a id="ingress"></a>어떻게 tooadd 엔터티 tooa 테이블</span><span class="sxs-lookup"><span data-stu-id="6dd8c-109"><a id="ingress"></a> How tooadd entities tooa table</span></span>
<span data-ttu-id="6dd8c-110">tooadd 엔터티 tooa 테이블을 사용 하 여 hello `Table` 특성이 `ICollector<T>` 또는 `IAsyncCollector<T>` 매개 변수 위치 `T` hello 스키마 지정 원하는 tooadd hello 엔터티.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-110">tooadd entities tooa table, use hello `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="6dd8c-111">hello 특성 생성자 hello 테이블의 hello 이름을 지정 하는 문자열 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-111">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span> 

<span data-ttu-id="6dd8c-112">hello 다음 코드 샘플 추가 `Person` 라는 엔터티 tooa 테이블 *수신*합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-112">hello following code sample adds `Person` entities tooa table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() { 
                        PartitionKey = "Test", 
                        RowKey = i.ToString(), 
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="6dd8c-113">일반적으로 함께 사용 하면 형식 hello `ICollector` 에서 파생 `TableEntity` 구현 또는 `ITableEntity`, 하지만 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-113">Typically hello type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="6dd8c-114">Hello 다음 중 하나 `Person` 클래스 hello 앞에 표시 된 hello 코드와 작업 `Ingress` 메서드.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-114">Either of hello following `Person` classes work with hello code shown in hello preceding `Ingress` method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="6dd8c-115">원하는 경우 toowork hello Azure 저장소 API 사용 하 여 직접 추가할 수 있습니다는 `CloudStorageAccount` toohello 메서드 서명 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-115">If you want toowork directly with hello Azure storage API, you can add a `CloudStorageAccount` parameter toohello method signature.</span></span>

## <span data-ttu-id="6dd8c-116"><a id="monitor"></a> 실시간 모니터링</span><span class="sxs-lookup"><span data-stu-id="6dd8c-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="6dd8c-117">데이터 수신 함수 종종 많은 양의 데이터를 처리 하기 때문에 hello WebJobs SDK 대시보드 실시간 모니터링 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-117">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="6dd8c-118">hello **호출 로그** 섹션에서 설명 하겠습니다 hello 함수가 실행 되 고 계속 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-118">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![수신 함수 실행](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="6dd8c-120">hello **호출 정보** 페이지 hello 함수의 진행률 (작성 하는 엔터티의 수)를 보고 실행 되 고 기회 tooabort을 제공 하는 동안 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-120">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span> 

![수신 함수 실행](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="6dd8c-122">Hello 함수 완료 되 면 hello **호출 정보** 페이지 hello 작성 된 행 수를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-122">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![수신 함수 완료](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="6dd8c-124"><a id="multiple"></a>어떻게 tooread 테이블에서 여러 엔터티</span><span class="sxs-lookup"><span data-stu-id="6dd8c-124"><a id="multiple"></a> How tooread multiple entities from a table</span></span>
<span data-ttu-id="6dd8c-125">tooread 테이블을 사용 하 여 hello `Table` 특성이 `IQueryable<T>` 매개 변수를 입력 `T` 에서 파생 `TableEntity` 구현 또는 `ITableEntity`합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-125">tooread a table, use hello `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="6dd8c-126">hello 다음 코드 샘플을 읽고 hello에서 모든 행을 로그 `Ingress` 테이블:</span><span class="sxs-lookup"><span data-stu-id="6dd8c-126">hello following code sample reads and logs all rows from hello `Ingress` table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}", 
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <span data-ttu-id="6dd8c-127"><a id="readone"></a>어떻게 tooread 테이블에서 단일 엔터티</span><span class="sxs-lookup"><span data-stu-id="6dd8c-127"><a id="readone"></a> How tooread a single entity from a table</span></span>
<span data-ttu-id="6dd8c-128">한 `Table` 특성 생성자 toobind tooa 단일 테이블 엔터티를 원하는 때 hello 파티션 키와 행 키를 지정할 수 있는 두 개의 추가 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-128">There is a `Table` attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="6dd8c-129">hello 다음 코드 샘플 행을 읽고 테이블에 대 한는 `Person` 엔터티의 파티션 키와 행 키 값에 기반 큐 메시지에 수신:</span><span class="sxs-lookup"><span data-stu-id="6dd8c-129">hello following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="6dd8c-130">hello `Person` 이 예제는 클래스에 tooimplement 없는 `ITableEntity`합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-130">hello `Person` class in this example does not have tooimplement `ITableEntity`.</span></span>

## <span data-ttu-id="6dd8c-131"><a id="storageapi"></a>어떻게 toouse hello.NET 저장소 API를 테이블로 직접 toowork</span><span class="sxs-lookup"><span data-stu-id="6dd8c-131"><a id="storageapi"></a> How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="6dd8c-132">Hello를 사용할 수도 있습니다 `Table` 특성이 `CloudTable` 개체 작업 테이블을 보다 더 유연 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-132">You can also use hello `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="6dd8c-133">hello 다음 코드 예제는 `CloudTable` tooadd 단일 엔터티 toohello 개체 *수신* 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-133">hello following code sample uses a `CloudTable` object tooadd a single entity toohello *Ingress* table.</span></span> 

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="6dd8c-134">방법에 대 한 자세한 내용은 toouse hello `CloudTable` 개체, 참조 [어떻게 toouse 테이블 저장소.NET에서](../cosmos-db/table-storage-how-to-use-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-134">For more information about how toouse hello `CloudTable` object, see [How toouse Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="6dd8c-135"><a id="queues"></a>Hello 큐 방법 tooarticle에서 포함 된 관련된 항목</span><span class="sxs-lookup"><span data-stu-id="6dd8c-135"><a id="queues"></a>Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="6dd8c-136">어떻게 toohandle 테이블 처리도 트리거된 큐 메시지 또는 WebJobs에 대 한 SDK 시나리오에 대 한 정보에 대 한 특정 tootable 참조 처리 [toouse Azure WebJobs SDK hello 사용 하 여 저장소를 대기 하는 방법을](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-136">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="6dd8c-137">이 문서에서 다루는 항목 hello 다음과를 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-137">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="6dd8c-138">비동기 함수</span><span class="sxs-lookup"><span data-stu-id="6dd8c-138">Async functions</span></span>
* <span data-ttu-id="6dd8c-139">여러 인스턴스</span><span class="sxs-lookup"><span data-stu-id="6dd8c-139">Multiple instances</span></span>
* <span data-ttu-id="6dd8c-140">정상 종료</span><span class="sxs-lookup"><span data-stu-id="6dd8c-140">Graceful shutdown</span></span>
* <span data-ttu-id="6dd8c-141">WebJobs SDK 특성 hello 함수 본문에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6dd8c-141">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="6dd8c-142">코드에서 hello SDK 연결 문자열을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-142">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="6dd8c-143">코드에서 WebJobs SDK 생성자 매개 변수 값 설정</span><span class="sxs-lookup"><span data-stu-id="6dd8c-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="6dd8c-144">수동으로 함수 트리거</span><span class="sxs-lookup"><span data-stu-id="6dd8c-144">Trigger a function manually</span></span>
* <span data-ttu-id="6dd8c-145">로그 작성</span><span class="sxs-lookup"><span data-stu-id="6dd8c-145">Write logs</span></span>

## <span data-ttu-id="6dd8c-146"><a id="nextsteps"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="6dd8c-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="6dd8c-147">이 가이드는 코드를 제공 하는 방법을 보여 주는 샘플 toohandle Azure 테이블 작업에 대 한 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-147">This guide has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="6dd8c-148">Azure WebJobs toouse 및 hello WebJobs SDK를 참조 하는 방법에 대 한 자세한 내용은 [Azure WebJobs 리소스 권장](http://go.microsoft.com/fwlink/?linkid=390226)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dd8c-148">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

