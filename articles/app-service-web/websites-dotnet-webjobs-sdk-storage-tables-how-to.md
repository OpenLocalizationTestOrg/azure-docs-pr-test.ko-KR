---
title: "WebJob SDK를 사용하여 Azure 테이블 저장소로 작업하는 방법"
description: "WebJobs SDK를 사용하여 Azure 테이블 저장소로 작업하는 방법에 대해 알아봅니다. 테이블을 만들고, 테이블에 엔터티를 추가하고, 기존 테이블을 읽습니다."
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
ms.openlocfilehash: 13cfc788c14d714df7022ce003d34691cf73d121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a><span data-ttu-id="4b4d1-104">WebJob SDK를 사용하여 Azure 테이블 저장소로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b4d1-104">How to use Azure table storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="4b4d1-105">개요</span><span class="sxs-lookup"><span data-stu-id="4b4d1-105">Overview</span></span>
<span data-ttu-id="4b4d1-106">이 가이드에서는 [WebJobs SDK](websites-dotnet-webjobs-sdk.md) 버전 1.x를 사용하여 Azure 저장소 테이블을 읽고 쓰는 방법을 보여 주는 C# 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="4b4d1-107">이 가이드에서는 [저장소 계정 또는 [여러 저장소 계정](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)을 가리키는 연결 문자열을 사용하여 Visual Studio에서 WebJob 프로젝트를 만드는 방법](websites-dotnet-webjobs-sdk-get-started.md)을 알고 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="4b4d1-108">일부 코드 조각에서는 `Table` 특성이 [수동으로 호출](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual)된 함수, 즉 트리거 특성 중 하나를 사용하지 않고 호출된 함수에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span></span> 

## <span data-ttu-id="4b4d1-109"><a id="ingress"></a> 테이블에 엔터티를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b4d1-109"><a id="ingress"></a> How to add entities to a table</span></span>
<span data-ttu-id="4b4d1-110">테이블에 엔터티를 추가하려면 `ICollector<T>` 또는 `IAsyncCollector<T>` 매개 변수와 함께 `Table` 특성을 사용합니다(여기서 `T`는 추가하려는 엔터티의 스키마를 지정).</span><span class="sxs-lookup"><span data-stu-id="4b4d1-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="4b4d1-111">특성 생성자는 테이블의 이름을 지정하는 문자열 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-111">The attribute constructor takes a string parameter that specifies the name of the table.</span></span> 

<span data-ttu-id="4b4d1-112">다음 코드 샘플은 `Person` 엔터티를 *Ingress*라는 테이블에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-112">The following code sample adds `Person` entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="4b4d1-113">일반적으로 `ICollector`에서 사용되는 유형은 `TableEntity`에서 파생되거나 `ITableEntity`를 구현하지만 반드시 그런 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="4b4d1-114">다음 `Person` 클래스 중 하나는 이전 `Ingress` 메서드에 표시된 코드와 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span></span>

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

<span data-ttu-id="4b4d1-115">Azure 저장소 API로 직접 작업하려는 경우 메서드 서명에 `CloudStorageAccount` 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span></span>

## <span data-ttu-id="4b4d1-116"><a id="monitor"></a> 실시간 모니터링</span><span class="sxs-lookup"><span data-stu-id="4b4d1-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="4b4d1-117">데이터 수신 함수는 많은 양의 데이터를 처리하는 경우가 많기 때문에 WebJobs SDK 대시보드에서는 실시간 모니터링 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="4b4d1-118">**호출 로그** 섹션에 함수가 여전히 실행 중인지 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-118">The **Invocation Log** section tells you if the function is still running.</span></span>

![수신 함수 실행](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="4b4d1-120">**호출 세부 정보** 페이지에는 실행 중인 함수의 진행률(작성된 엔터티 수)이 보고되고 실행을 중단할 수 있는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span> 

![수신 함수 실행](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="4b4d1-122">함수가 완료되면 **호출 세부 정보** 페이지에 작성된 행 수가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![수신 함수 완료](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="4b4d1-124"><a id="multiple"></a> 테이블에서 여러 엔터티를 읽는 방법</span><span class="sxs-lookup"><span data-stu-id="4b4d1-124"><a id="multiple"></a> How to read multiple entities from a table</span></span>
<span data-ttu-id="4b4d1-125">테이블을 읽으려면 `IQueryable<T>` 매개 변수와 함께 `Table` 특성을 사용합니다. 여기서 `T` 유형은 `TableEntity`에서 파생되거나 `ITableEntity`를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="4b4d1-126">다음 코드 샘플은 `Ingress` 테이블에서 모든 행을 읽고 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-126">The following code sample reads and logs all rows from the `Ingress` table:</span></span>

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

### <span data-ttu-id="4b4d1-127"><a id="readone"></a> 테이블에서 단일 엔터티를 읽는 방법</span><span class="sxs-lookup"><span data-stu-id="4b4d1-127"><a id="readone"></a> How to read a single entity from a table</span></span>
<span data-ttu-id="4b4d1-128">단일 테이블 엔터티에 바인딩할 때 파티션 키 및 행 키를 지정할 수 있는 추가 매개 변수 두 개가 포함된 `Table` 특성 생성자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="4b4d1-129">다음 코드 샘플은 큐 메시지에서 받은 파티션 키 및 행 키를 기반으로 `Person` 엔터티에 대한 테이블 행을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="4b4d1-130">이 예제의 `Person` 클래스는 `ITableEntity`를 구현할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-130">The `Person` class in this example does not have to implement `ITableEntity`.</span></span>

## <span data-ttu-id="4b4d1-131"><a id="storageapi"></a> .NET 저장소 API를 직접 사용하여 테이블로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b4d1-131"><a id="storageapi"></a> How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="4b4d1-132">`CloudTable` 개체에서 `Table` 특성을 사용하여 테이블 작업을 보다 유연하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="4b4d1-133">다음 코드 샘플은 `CloudTable` 개체를 사용하여 *Ingress* 테이블에 단일 엔터티를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span></span> 

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

<span data-ttu-id="4b4d1-134">`CloudTable` 개체를 사용하는 방법에 대한 자세한 내용은 [.NET에서 테이블 저장소를 사용하는 방법](../cosmos-db/table-storage-how-to-use-dotnet.md)을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="4b4d1-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="4b4d1-135"><a id="queues"></a>큐 방법 문서에서 다루는 관련 항목</span><span class="sxs-lookup"><span data-stu-id="4b4d1-135"><a id="queues"></a>Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="4b4d1-136">큐 메시지에 의해 트리거되는 테이블을 처리하는 방법 또는 테이블 처리에 특정하지 않은 WebJobs SDK 시나리오에 대한 자세한 내용은 [WebJobs SDK를 사용하여 Azure 큐 저장소로 작업하는 방법](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="4b4d1-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="4b4d1-137">이 문서에서 다루는 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-137">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="4b4d1-138">비동기 함수</span><span class="sxs-lookup"><span data-stu-id="4b4d1-138">Async functions</span></span>
* <span data-ttu-id="4b4d1-139">여러 인스턴스</span><span class="sxs-lookup"><span data-stu-id="4b4d1-139">Multiple instances</span></span>
* <span data-ttu-id="4b4d1-140">정상 종료</span><span class="sxs-lookup"><span data-stu-id="4b4d1-140">Graceful shutdown</span></span>
* <span data-ttu-id="4b4d1-141">함수 본문에 WebJobs SDK 특성 사용</span><span class="sxs-lookup"><span data-stu-id="4b4d1-141">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="4b4d1-142">코드에서 SDK 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="4b4d1-142">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="4b4d1-143">코드에서 WebJobs SDK 생성자 매개 변수 값 설정</span><span class="sxs-lookup"><span data-stu-id="4b4d1-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="4b4d1-144">수동으로 함수 트리거</span><span class="sxs-lookup"><span data-stu-id="4b4d1-144">Trigger a function manually</span></span>
* <span data-ttu-id="4b4d1-145">로그 작성</span><span class="sxs-lookup"><span data-stu-id="4b4d1-145">Write logs</span></span>

## <span data-ttu-id="4b4d1-146"><a id="nextsteps"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b4d1-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="4b4d1-147">이 가이드에서는 Azure 테이블 작업에 대한 일반적인 시나리오를 처리하는 방법을 보여 주는 코드 샘플을 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="4b4d1-148">Azure WebJob 및 WebJob SDK를 사용하는 방법에 대한 자세한 내용은 [Azure WebJob 권장 리소스](http://go.microsoft.com/fwlink/?linkid=390226)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b4d1-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

