---
title: "Azure 저장소 및 Visual Studio 연결 서비스 시작(WebJob 프로젝트)"
description: "Visual Studio 연결된 서비스를 사용하여 저장소 계정에 연결한 후 Visual Studio Azure WebJobs 프로젝트에서 Azure 테이블 저장소 사용을 시작하는 방법입니다."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 79fba102377cdc6b681f6798699767961040a7e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="43fd1-103">Azure 저장소 시작(Azure WebJob 프로젝트)</span><span class="sxs-lookup"><span data-stu-id="43fd1-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="43fd1-104">개요</span><span class="sxs-lookup"><span data-stu-id="43fd1-104">Overview</span></span>
<span data-ttu-id="43fd1-105">이 문서에서는 Azure 테이블 저장소 서비스에서 Azure WebJobs SDK 버전 1.x를 사용하는 방법을 보여 주는 C# 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-105">This article provides C# code samples that show show how to use the Azure WebJobs SDK version 1.x with the Azure table storage service.</span></span> <span data-ttu-id="43fd1-106">코드 샘플에서는 [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) 버전 1.x를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="43fd1-107">Azure 테이블 저장소 서비스를 사용하면 많은 양의 구조화된 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="43fd1-108">이 서비스는 Azure 클라우드 내부 및 외부에서 인증된 호출을 수락하는 NoSQL 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="43fd1-109">Azure 테이블은 구조화된 비관계형 데이터를 저장하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="43fd1-110">자세한 내용은 [.NET을 사용하여 Azure 테이블 저장소 시작](storage-dotnet-how-to-use-tables.md#create-a-table) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43fd1-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span></span>

<span data-ttu-id="43fd1-111">일부 코드 조각에서는 **Table** 특성이 수동으로 호출된 함수, 즉 트리거 특성 중 하나를 사용하지 않고 호출된 함수에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-111">Some of the code snippets show the **Table** attribute used in functions that are called manually, that is, not by using one of the trigger attributes.</span></span>

## <a name="how-to-add-entities-to-a-table"></a><span data-ttu-id="43fd1-112">테이블에 엔터티를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="43fd1-112">How to add entities to a table</span></span>
<span data-ttu-id="43fd1-113">테이블에 엔터티를 추가하려면 **ICollector<T>** 또는 **IAsyncCollector<T>** 매개 변수와 함께 **Table** 특성을 사용합니다(여기서 **T**는 추가하려는 엔터티의 스키마를 지정).</span><span class="sxs-lookup"><span data-stu-id="43fd1-113">To add entities to a table, use the **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="43fd1-114">특성 생성자는 테이블의 이름을 지정하는 문자열 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-114">The attribute constructor takes a string parameter that specifies the name of the table.</span></span>

<span data-ttu-id="43fd1-115">다음 코드 샘플은 **Person** 엔터티를 *Ingress*라는 테이블에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-115">The following code sample adds **Person** entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="43fd1-116">일반적으로 **ICollector**에서 사용되는 유형은 **TableEntity**에서 파생되거나 **ITableEntity**를 구현하지만 반드시 그런 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-116">Typically the type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="43fd1-117">다음 **Person** 클래스 중 하나는 이전 **Ingress** 메서드에 표시된 코드와 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-117">Either of the following **Person** classes work with the code shown in the preceding **Ingress** method.</span></span>

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

<span data-ttu-id="43fd1-118">Azure 저장소 API로 직접 작업하려는 경우 메서드 서명에 **CloudStorageAccount** 매개 변수를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-118">If you want to work directly with the Azure storage API, you can add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="43fd1-119">실시간 모니터링</span><span class="sxs-lookup"><span data-stu-id="43fd1-119">Real-time monitoring</span></span>
<span data-ttu-id="43fd1-120">데이터 수신 함수는 많은 양의 데이터를 처리하는 경우가 많기 때문에 WebJobs SDK 대시보드에서는 실시간 모니터링 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-120">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="43fd1-121">**호출 로그** 섹션에 함수가 여전히 실행 중인지 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-121">The **Invocation Log** section tells you if the function is still running.</span></span>

![수신 함수 실행](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="43fd1-123">**호출 세부 정보** 페이지에는 실행 중인 함수의 진행률(작성된 엔터티 수)이 보고되고 실행을 중단할 수 있는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-123">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span>

![수신 함수 실행](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="43fd1-125">함수가 완료되면 **호출 세부 정보** 페이지에 작성된 행 수가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-125">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![수신 함수 완료](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-to-read-multiple-entities-from-a-table"></a><span data-ttu-id="43fd1-127">테이블에서 여러 엔터티를 읽는 방법</span><span class="sxs-lookup"><span data-stu-id="43fd1-127">How to read multiple entities from a table</span></span>
<span data-ttu-id="43fd1-128">테이블을 읽으려면 **IQueryable<T>** 매개 변수와 함께 **Table** 특성을 사용합니다. 여기서 **T** 유형은 **TableEntity**에서 파생되거나 **ITableEntity**를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-128">To read a table, use the **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="43fd1-129">다음 코드 샘플은 **Ingress** 테이블에서 모든 행을 읽고 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-129">The following code sample reads and logs all rows from the **Ingress** table:</span></span>

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

### <a name="how-to-read-a-single-entity-from-a-table"></a><span data-ttu-id="43fd1-130">테이블에서 단일 엔터티를 읽는 방법</span><span class="sxs-lookup"><span data-stu-id="43fd1-130">How to read a single entity from a table</span></span>
<span data-ttu-id="43fd1-131">단일 테이블 엔터티에 바인딩할 때 파티션 키 및 행 키를 지정할 수 있는 추가 매개 변수 두 개가 포함된 **Table** 특성 생성자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-131">There is a **Table** attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="43fd1-132">다음 코드 샘플은 큐 메시지에서 받은 파티션 키 및 행 키를 기반으로 **Person** 엔터티에 대한 테이블 행을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-132">The following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="43fd1-133">이 예제의 **Person** 클래스는 **ITableEntity**를 구현할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-133">The **Person** class in this example does not have to implement **ITableEntity**.</span></span>

## <a name="how-to-use-the-net-storage-api-directly-to-work-with-a-table"></a><span data-ttu-id="43fd1-134">.NET 저장소 API를 직접 사용하여 테이블로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="43fd1-134">How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="43fd1-135">**CloudTable** 개체에서 **Table** 특성을 사용하여 테이블 작업을 보다 유연하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-135">You can also use the **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="43fd1-136">다음 코드 샘플은 **CloudTable** 개체를 사용하여 *Ingress* 테이블에 단일 엔터티를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-136">The following code sample uses a **CloudTable** object to add a single entity to the *Ingress* table.</span></span>

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

<span data-ttu-id="43fd1-137">**CloudTable** 개체를 사용하는 방법에 대한 자세한 내용은 [.NET을 사용하여 Azure 테이블 저장소 시작](storage-dotnet-how-to-use-tables.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43fd1-137">For more information about how to use the **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-the-queues-how-to-article"></a><span data-ttu-id="43fd1-138">큐 방법 문서에서 다루는 관련 항목</span><span class="sxs-lookup"><span data-stu-id="43fd1-138">Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="43fd1-139">큐 메시지에 의해 트리거되는 테이블을 처리하는 방법 또는 테이블 처리에 특정하지 않은 WebJobs SDK 시나리오에 대한 자세한 내용은 [Azure 큐 저장소 및 Visual Studio 연결된 서비스(WebJob 프로젝트) 시작](vs-storage-webjobs-getting-started-queues.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43fd1-139">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43fd1-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43fd1-140">Next steps</span></span>
<span data-ttu-id="43fd1-141">이 문서에서는 Azure 테이블 작업에 대한 일반적인 시나리오를 처리하는 방법을 보여 주는 코드 샘플을 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="43fd1-141">This article has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="43fd1-142">Azure Webjob 및 Webjob SDK를 사용하는 방법에 대한 자세한 내용은 [Azure WebJobs 설명서 리소스](http://go.microsoft.com/fwlink/?linkid=390226)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43fd1-142">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

