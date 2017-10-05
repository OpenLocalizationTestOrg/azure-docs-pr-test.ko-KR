---
title: "Table Storage 및 Visual Studio 연결 서비스 시작(클라우드 서비스) | Microsoft Docs"
description: "Visual Studio 연결 서비스를 사용하여 저장소 계정에 연결한 후 Visual Studio 클라우드 서비스 프로젝트에서 Azure 테이블 저장소 사용을 시작하는 방법입니다."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 51b71d783806d9b0d58d4473b8c07f77441dadd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="26b95-103">Azure 테이블 저장소 및 Visual Studio 연결 서비스 시작(클라우드 서비스 프로젝트)</span><span class="sxs-lookup"><span data-stu-id="26b95-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="26b95-104">개요</span><span class="sxs-lookup"><span data-stu-id="26b95-104">Overview</span></span>
<span data-ttu-id="26b95-105">이 문서에서는 Visual Studio **연결된 서비스 추가** 대화 상자를 사용하여 클라우드 서비스 프로젝트에서 Azure 저장소 계정을 만들거나 참조한 후 Visual Studio에서 Azure 테이블 저장소를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-105">This article describes how to get started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="26b95-106">**연결된 서비스 추가** 작업은 프로젝트의 Azure 저장소에 액세스하는 데 적합한 NuGet 패키지를 설치하고 프로젝트 구성 파일에 저장소 계정에 대한 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="26b95-107">Azure 테이블 저장소 서비스를 사용하면 많은 양의 구조화된 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="26b95-108">이 서비스는 Azure 클라우드 내부 및 외부에서 인증된 호출을 수락하는 NoSQL 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="26b95-109">Azure 테이블은 구조화된 비관계형 데이터를 저장하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="26b95-110">시작하려면 먼저 저장소 계정에서 테이블을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-110">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="26b95-111">코드에서 Azure 테이블을 만드는 방법과 기본 테이블 및 테이블 엔터티 추가, 수정, 읽기와 같은 엔터티 작업을 수행하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-111">We'll show you how to create an Azure table in code, and also how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="26b95-112">샘플은 C\# 코드로 작성되었으며, [.NET용 Microsoft Azure Storage 클라이언트 라이브러리](https://msdn.microsoft.com/library/azure/dn261237.aspx)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-112">The samples are written in C\# code and use the [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="26b95-113">**참고:** Azure 저장소에 대한 호출을 수행하는 일부 API는 비동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-113">**NOTE:** Some of the APIs that perform calls out to Azure storage are asynchronous.</span></span> <span data-ttu-id="26b95-114">자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](http://msdn.microsoft.com/library/hh191443.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26b95-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="26b95-115">아래 코드에서는 비동기 프로그래밍 메서드를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-115">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="26b95-116">테이블을 프로그래밍 방식으로 조작하는 방법에 대한 자세한 내용은 [.NET을 사용하여 Azure 테이블 저장소 시작](../storage/storage-dotnet-how-to-use-tables.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26b95-116">See [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="26b95-117">Azure 저장소에 대한 일반적인 내용은 [저장소 설명서](https://azure.microsoft.com/documentation/services/storage/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26b95-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="26b95-118">Azure 클라우드 서비스에 대한 일반적인 내용은 [클라우드 서비스 설명서](https://azure.microsoft.com/documentation/services/cloud-services/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26b95-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="26b95-119">ASP.NET 응용 프로그램을 프로그래밍하는 방법에 대한 자세한 내용은 [ASP.NET](http://www.asp.net) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26b95-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="26b95-120">코드에서 테이블 액세스하기</span><span class="sxs-lookup"><span data-stu-id="26b95-120">Access tables in code</span></span>
<span data-ttu-id="26b95-121">클라우드 서비스 프로젝트의 테이블에 액세스하려면 Azure 테이블 저장소에 액세스하는 C# 소스 파일에 다음 항목을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-121">To access tables in cloud service projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="26b95-122">C# 파일 맨 위의 네임스페이스 선언에 이러한 **using** 문이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-122">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="26b95-123">저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="26b95-124">Azure 서비스 구성에서 저장소 연결 문자열 및 저장소 계정 정보를 가져오려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-124">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="26b95-125">다음 샘플의 코드 앞에 위의 코드를 모두 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-125">Use all of the above code in front of the code in the following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="26b95-126">저장소 계정의 테이블 개체를 참조하려면 **CloudTableClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-126">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>
   
         // Create the table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="26b95-127">특정 테이블과 엔터티를 참조하려면 **CloudTable** 참조 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-127">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="26b95-128">코드에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="26b95-128">Create a table in code</span></span>
<span data-ttu-id="26b95-129">Azure 테이블을 만들려면 "코드에서 테이블 액세스" 섹션에 설명된 대로 **CloudTable** 개체를 가져온 후 **CreateIfNotExistsAsync** 호출을 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-129">To create the Azure table, just add a call to **CreateIfNotExistsAsync** to the after you get a **CloudTable** object as described in the "Access tables in code" section.</span></span>

    // Create the CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="26b95-130">테이블에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="26b95-130">Add an entity to a table</span></span>
<span data-ttu-id="26b95-131">테이블에 엔터티를 추가하려면 엔터티의 속성을 정의하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-131">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="26b95-132">다음 코드에서는 고객의 이름을 행 키로 사용하고 성을 파티션 키로 사용하는 **CustomerEntity** 라는 엔터티 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-132">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and the last name as the partition key.</span></span>

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

<span data-ttu-id="26b95-133">엔터티와 관련된 테이블 작업은 이전에 "코드에서 테이블 액세스"에서 만든 **CloudTable** 개체를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-133">Table operations involving entities are done using the **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="26b95-134">**TableOperation** 개체를 수행할 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-134">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="26b95-135">다음 코드 예제에서는 **CloudTable** 개체와 **CustomerEntity** 개체를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-135">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="26b95-136">작업을 준비하기 위해 고객 엔터티를 테이블에 삽입하는 **TableOperation** 이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-136">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="26b95-137">마지막으로 **CloudTable.ExecuteAsync**를 호출하여 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-137">Finally, the operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="26b95-138">엔터티 일괄 삽입</span><span class="sxs-lookup"><span data-stu-id="26b95-138">Insert a batch of entities</span></span>
<span data-ttu-id="26b95-139">하나의 쓰기 작업으로 테이블에 여러 엔터티를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="26b95-140">다음 코드 예제에서는 두 개의 엔터티 개체("Jeff Smith" 및 "Ben Smith")를 만들고 Insert 메서드를 사용하여 **TableBatchOperation** 개체에 이 두 개체를 추가한 다음 **CloudTable.ExecuteBatchAsync**를 호출하여 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-140">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the Insert method, and then starts the operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="26b95-141">파티션의 모든 엔터티 가져오기</span><span class="sxs-lookup"><span data-stu-id="26b95-141">Get all of the entities in a partition</span></span>
<span data-ttu-id="26b95-142">테이블에서 파티션의 모든 엔터티를 쿼리하려면 **TableQuery** 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-142">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="26b95-143">다음 코드 예제에서는 'Smith'가 파티션 키인 엔터티에 대한 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-143">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="26b95-144">이 예제에서는 쿼리 결과에 있는 각 엔터티의 필드를 콘솔에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-144">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="26b95-145">단일 엔터티 가져오기</span><span class="sxs-lookup"><span data-stu-id="26b95-145">Get a single entity</span></span>
<span data-ttu-id="26b95-146">단일 특정 엔터티를 가져오는 쿼리를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-146">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="26b95-147">다음 코드에서는 **TableOperation** 개체를 사용하여 'Ben Smith'라는 고객을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-147">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="26b95-148">이 메서드는 컬렉션 대신 엔터티 하나만 반환하며, **TableResult.Result**에서 반환되는 값은 **CustomerEntity** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-148">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="26b95-149">쿼리에 파티션과 행 키를 모두 지정하는 것이 **테이블** 서비스에서 단일 엔터티를 검색하는 가장 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-149">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="26b95-150">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="26b95-150">Delete an entity</span></span>
<span data-ttu-id="26b95-151">엔터티를 찾은 후 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="26b95-152">다음 코드에서는 "Ben Smith"라는 고객 엔터티를 검색하고, 찾으면 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="26b95-152">The following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="26b95-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26b95-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

