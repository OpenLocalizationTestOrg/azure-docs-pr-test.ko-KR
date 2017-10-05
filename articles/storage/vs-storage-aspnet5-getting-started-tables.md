---
title: "테이블 저장소 및 Visual Studio 연결된 서비스 시작 방법(ASP.NET Core) | Microsoft Docs"
description: "Visual Studio 연결 서비스를 사용하여 저장소 계정에 연결한 후 Visual Studio ASP.NET Core 프로젝트에서 Azure 테이블 저장소 사용을 시작하는 방법입니다."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: b64d4f7e55977c7ce144987f7600e5ddcb25596c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-get-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="74703-103">Azure 테이블 저장소 및 Visual Studio 연결된 서비스를 시작하는 방법</span><span class="sxs-lookup"><span data-stu-id="74703-103">How to get started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="74703-104">개요</span><span class="sxs-lookup"><span data-stu-id="74703-104">Overview</span></span>
<span data-ttu-id="74703-105">이 문서에서는 Visual Studio의 **연결된 서비스 추가** 대화 상자를 사용하여 ASP.NET Core 프로젝트에서 Azure Storage 계정을 만들거나 참조한 후 Visual Studio에서 Azure 테이블 저장소를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="74703-106">Azure 테이블 저장소 서비스를 사용하면 많은 양의 구조화된 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74703-106">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="74703-107">이 서비스는 Azure 클라우드 내부 및 외부에서 인증된 호출을 수락하는 NoSQL 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="74703-107">The service is a NoSQL data store that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="74703-108">Azure 테이블은 구조화된 비관계형 데이터를 저장하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="74703-109">**연결된 서비스 추가** 작업은 프로젝트의 Azure 저장소에 액세스하는 데 적합한 NuGet 패키지를 설치하고 프로젝트 구성 파일에 저장소 계정에 대한 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="74703-110">Azure 테이블 저장소를 사용하는 방법에 대한 자세한 내용은 [.NET을 사용하여 Azure 테이블 저장소 시작](storage-dotnet-how-to-use-tables.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74703-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="74703-111">시작하려면 먼저 저장소 계정에서 테이블을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-111">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="74703-112">코드에서 Azure 테이블을 만드는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="74703-112">We'll show you how to create an Azure table in code.</span></span> <span data-ttu-id="74703-113">또한 기본 테이블 및 테이블 엔터티 추가, 수정, 읽기와 같은 엔터티 작업을 수행하는 방법도 알려드립니다.</span><span class="sxs-lookup"><span data-stu-id="74703-113">We'll also show you how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="74703-114">샘플은 C\# 코드로 작성되었으며 Azure Storage Client Library for .NET을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-114">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="74703-115">**참고** - ASP.NET Core에서 Azure Storage에 대한 호출을 수행하는 일부 API는 비동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="74703-115">**NOTE** - Some of the APIs that perform calls out to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="74703-116">자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](http://msdn.microsoft.com/library/hh191443.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74703-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="74703-117">아래 코드에서는 비동기 프로그래밍 메서드를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-117">The code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="74703-118">코드에서 테이블 액세스하기</span><span class="sxs-lookup"><span data-stu-id="74703-118">Access tables in code</span></span>
<span data-ttu-id="74703-119">ASP.NET Core 프로젝트의 테이블에 액세스하려면 Azure 테이블 저장소에 액세스하는 C# 소스 파일에 다음 항목을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-119">To access tables in ASP.NET Core projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="74703-120">C# 파일 맨 위의 네임스페이스 선언에 이러한 **using** 문이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-120">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="74703-121">저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="74703-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="74703-122">Azure 서비스 구성에서 저장소 연결 문자열 및 저장소 계정 정보를 가져오려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-122">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="74703-123">**참고:** 다음 샘플의 코드 앞에 위의 코드를 모두 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-123">**NOTE** - Use all of the above code in front of the code in the following samples.</span></span>
3. <span data-ttu-id="74703-124">저장소 계정의 테이블 개체를 참조하려면 **CloudTableClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="74703-124">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>  
   
        // Create the table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="74703-125">특정 테이블과 엔터티를 참조하려면 **CloudTable** 참조 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="74703-125">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="74703-126">코드에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="74703-126">Create a table in code</span></span>
<span data-ttu-id="74703-127">Azure 테이블을 만들려면 **CreateIfNotExistsAsync()**에 대한 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-127">To create the Azure table, just add a call to **CreateIfNotExistsAsync()**.</span></span>

    // Create the CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="74703-128">테이블에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="74703-128">Add an entity to a table</span></span>
<span data-ttu-id="74703-129">테이블에 엔터티를 추가하려면 엔터티의 속성을 정의하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74703-129">To add an entity to a table you create a class that defines the properties of your entity.</span></span> <span data-ttu-id="74703-130">다음 코드에서는 고객의 이름을 행 키로 사용하고 성을 파티션 키로 사용하는 **CustomerEntity** 라는 엔터티 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-130">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }

        public string PhoneNumber { get; set; }
    }

<span data-ttu-id="74703-131">엔터티와 관련된 테이블 작업은 이전에 "코드에서 테이블 액세스"에서 만든 **CloudTable** 개체를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="74703-131">Table operations involving entities are done using the **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="74703-132">**TableOperation** 개체를 수행할 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="74703-132">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="74703-133">다음 코드 예제에서는 **CloudTable** 개체와 **CustomerEntity** 개체를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="74703-133">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="74703-134">작업을 준비하기 위해 고객 엔터티를 테이블에 삽입하는 **TableOperation** 이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="74703-134">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="74703-135">마지막으로 CloudTable.ExecuteAsync를 호출하여 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="74703-135">Finally, the operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="74703-136">엔터티 일괄 삽입</span><span class="sxs-lookup"><span data-stu-id="74703-136">Insert a batch of entities</span></span>
<span data-ttu-id="74703-137">하나의 쓰기 작업으로 테이블에 여러 엔터티를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74703-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="74703-138">다음 코드 예제에서는 두 개의 엔터티 개체("Jeff Smith" 및 "Ben Smith")를 만들고 **Insert** 메서드를 사용하여 **TableBatchOperation** 개체에 이 두 개체를 추가한 다음 CloudTable.ExecuteBatchAsync를 호출하여 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-138">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the **Insert** method, and then starts the operation by calling CloudTable.ExecuteBatchAsync.</span></span>

    // Create the batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a customer entity and add it to the table.
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";
    customer1.PhoneNumber = "425-555-0104";

    // Create another customer entity and add it to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    customer2.PhoneNumber = "425-555-0102";

    // Add both customer entities to the batch insert operation.
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);

    // Execute the batch operation.
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="74703-139">파티션의 모든 엔터티 가져오기</span><span class="sxs-lookup"><span data-stu-id="74703-139">Get all of the entities in a partition</span></span>
<span data-ttu-id="74703-140">테이블에서 파티션의 모든 엔터티를 쿼리하려면 **TableQuery** 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-140">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="74703-141">다음 코드 예제에서는 'Smith'가 파티션 키인 엔터티에 대한 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-141">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="74703-142">이 예제에서는 쿼리 결과에 있는 각 엔터티의 필드를 콘솔에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-142">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print the fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

## <a name="get-a-single-entity"></a><span data-ttu-id="74703-143">단일 엔터티 가져오기</span><span class="sxs-lookup"><span data-stu-id="74703-143">Get a single entity</span></span>
<span data-ttu-id="74703-144">단일 특정 엔터티를 가져오는 쿼리를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74703-144">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="74703-145">다음 코드에서는 **TableOperation** 개체를 사용하여 'Ben Smith'라는 고객을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-145">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="74703-146">이 메서드는 컬렉션 대신 엔터티 하나만 반환하며, **TableResult.Result**에서 반환되는 값은 **CustomerEntity** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="74703-146">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="74703-147">쿼리에 파티션과 행 키를 모두 지정하는 것이 **테이블** 서비스에서 단일 엔터티를 검색하는 가장 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="74703-147">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="74703-148">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="74703-148">Delete an entity</span></span>
<span data-ttu-id="74703-149">엔터티를 찾은 후 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74703-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="74703-150">다음 코드에서는 "Ben Smith"라는 고객 엔터티를 찾아 보고 찾으면 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="74703-150">The following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign the result to a CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create the Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute the operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete the entity.");

## <a name="next-steps"></a><span data-ttu-id="74703-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="74703-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

