---
title: ".NET을 사용하여 Azure 테이블 저장소 시작 | Microsoft Docs"
description: "Azure 테이블 저장소, NoSQL 데이터 저장소를 사용하여 클라우드에 구조화된 데이터를 저장합니다."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: marsma
ms.openlocfilehash: 16a9dad1b01fdbef5ec8949bf9ff25497f33d994
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="b49da-103">.NET을 사용하여 Azure 테이블 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="b49da-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="b49da-104">Azure Table Storage는 클라우드에 구조화된 NoSQL 데이터를 저장하는 서비스로, 스키마 없이 디자인된 키/특성 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-104">Azure Table storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="b49da-105">테이블 저장소는 스키마가 없기 때문에 응용 프로그램의 요구 사항이 변화함에 따라 데이터를 쉽게 적응시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-105">Because Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="b49da-106">Table Storage 데이터에 대한 액세스는 많은 응용 프로그램 유형에 대해 빠르고 비용 효율적이며 비슷한 양의 데이터일 때 일반적으로 전통적인 SQL에 비해 비용이 매우 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-106">Access to Table storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="b49da-107">Table Storage를 사용하여 웹 응용 프로그램의 사용자 데이터, 주소록, 장치 정보 및 서비스에 필요한 다른 유형의 메타데이터와 같은 유연한 데이터 집합을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-107">You can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="b49da-108">테이블에 저장할 수 있는 엔터티 수에는 제한이 없으며, 저장소 계정에 포함할 수 있는 테이블의 수에는 저장소 계정의 최대 용량 한도까지 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="b49da-109">이 자습서 정보</span><span class="sxs-lookup"><span data-stu-id="b49da-109">About this tutorial</span></span>
<span data-ttu-id="b49da-110">이 자습서에서는 몇 가지 일반적인 Azure Table Storage 시나리오에서 [.NET용 Azure Storage 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-110">This tutorial shows you how to use the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="b49da-111">테이블 만들기 및 삭제, 테이블 데이터 삽입, 업데이트, 삭제 및 쿼리 등 C# 예제를 사용하는 다음과 같은 시나리오가 제시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b49da-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b49da-112">Prerequisites</span></span>

<span data-ttu-id="b49da-113">이 자습서를 성공적으로 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-113">You need the following to complete this tutorial successfully:</span></span>

* [<span data-ttu-id="b49da-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b49da-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="b49da-115">.NET용 Azure 저장소 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b49da-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="b49da-116">.NET용 Azure 구성 관리자</span><span class="sxs-lookup"><span data-stu-id="b49da-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="b49da-117">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="b49da-117">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="b49da-118">추가 샘플</span><span class="sxs-lookup"><span data-stu-id="b49da-118">More samples</span></span>
<span data-ttu-id="b49da-119">테이블 저장소를 사용하는 추가 예제는 [.NET에서 Azure 테이블 저장소 시작](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b49da-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="b49da-120">GitHub에서 샘플 응용 프로그램을 다운로드하고 실행하거나 코드를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-120">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="b49da-121">지시문을 사용하여 추가</span><span class="sxs-lookup"><span data-stu-id="b49da-121">Add using directives</span></span>
<span data-ttu-id="b49da-122">다음 **using** 지시문을 `Program.cs` 파일 맨 위에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-122">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="b49da-123">연결 문자열 구문 분석</span><span class="sxs-lookup"><span data-stu-id="b49da-123">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-table-service-client"></a><span data-ttu-id="b49da-124">테이블 서비스 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="b49da-124">Create the Table service client</span></span>
<span data-ttu-id="b49da-125">[CloudTableClient][dotnet_CloudTableClient] 클래스를 사용하면 Table Storage에 저장된 테이블 및 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-125">The [CloudTableClient][dotnet_CloudTableClient] class enables you to retrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="b49da-126">Table service 클라이언트를 만드는 한 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-126">Here's one way to create the Table service client:</span></span>

```csharp
// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="b49da-127">이제 데이터를 읽어 오고 테이블 저장소에 데이터를 기록하는 코드를 작성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-127">Now you are ready to write code that reads data from and writes data to Table storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="b49da-128">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="b49da-128">Create a table</span></span>
<span data-ttu-id="b49da-129">이 예제에서는 테이블이 없는 경우 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-129">This example shows how to create a table if it does not already exist:</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference to the table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="b49da-130">테이블에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="b49da-130">Add an entity to a table</span></span>
<span data-ttu-id="b49da-131">엔터티는 [TableEntity][dotnet_TableEntity]에서 파생된 사용자 지정 클래스를 사용하여 C# 개체에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-131">Entities map to C# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="b49da-132">테이블에 엔터티를 추가하려면 엔터티의 속성을 정의하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-132">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="b49da-133">다음 코드에서는 고객의 이름을 행 키로 사용하고 성을 파티션 키로 사용하는 엔터티 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-133">The following code defines an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="b49da-134">엔터티의 파티션과 행 키가 결합되어 테이블에서 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-134">Together, an entity's partition and row key uniquely identify it in the table.</span></span> <span data-ttu-id="b49da-135">동일한 파티션 키를 가진 엔터티는 다른 파티션 키를 가진 엔터티보다 더 빨리 쿼리할 수 있지만 다양한 파티션 키를 사용하면 병렬 작업 확장성이 커집니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-135">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="b49da-136">테이블에 저장되는 엔터티는 예를 들어 [TableEntity][dotnet_TableEntity] 클래스에서 파생되는 지원되는 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-136">Entities to be stored in tables must be of a supported type, for example derived from the [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="b49da-137">테이블에 저장하려는 엔터티 속성은 해당 형식의 공용 속성이어야 하며 값의 가져오기 및 설정하기를 모두 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-137">Entity properties you'd like to store in a table must be public properties of the type, and support both getting and setting of values.</span></span> <span data-ttu-id="b49da-138">또한 엔터티 형식은 *반드시* 매개 변수가 없는 생성자를 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

```csharp
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
```

<span data-ttu-id="b49da-139">엔터티와 관련된 테이블 작업은 이전의 “테이블 만들기” 섹션에서 만든 [CloudTable][dotnet_CloudTable] 개체를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-139">Table operations that involve entities are performed via the [CloudTable][dotnet_CloudTable] object that you created earlier in the "Create a table" section.</span></span> <span data-ttu-id="b49da-140">수행할 작업은 [TableOperation][dotnet_TableOperation] 개체로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-140">The operation to be performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="b49da-141">다음 코드 예제에서는 [CloudTable][dotnet_CloudTable] 개체, **CustomerEntity** 개체의 생성을 차례로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-141">The following code example shows the creation of the [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="b49da-142">작업을 준비하기 위해 고객 엔터티를 테이블에 삽입하는 [TableOperation][dotnet_TableOperation] 개체가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-142">To prepare the operation, a [TableOperation][dotnet_TableOperation] object is created to insert the customer entity into the table.</span></span> <span data-ttu-id="b49da-143">마지막으로, [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute]를 호출하여 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-143">Finally, the operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="b49da-144">엔터티 일괄 삽입</span><span class="sxs-lookup"><span data-stu-id="b49da-144">Insert a batch of entities</span></span>
<span data-ttu-id="b49da-145">하나의 쓰기 작업으로 테이블에 엔터티를 일괄 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="b49da-146">일괄 작업에 대한 다른 참고 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="b49da-147">동일한 단일 일괄 작업에서 업데이트, 삭제 및 삽입을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-147">You can perform updates, deletes, and inserts in the same single batch operation.</span></span>
* <span data-ttu-id="b49da-148">단일 일괄 작업에 최대 100개의 엔터티가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-148">A single batch operation can include up to 100 entities.</span></span>
* <span data-ttu-id="b49da-149">단일 일괄 작업의 모든 엔터티에 동일한 파티션 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-149">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="b49da-150">쿼리를 일괄 작업으로 수행할 수 있지만 일괄 작업의 유일한 작업이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-150">While it is possible to perform a query as a batch operation, it must be the only operation in the batch.</span></span>

<span data-ttu-id="b49da-151">다음 코드 예제에서는 엔터티 개체 두 개를 만들고 [Insert][dotnet_TableBatchOperation_Insert] 메서드를 사용하여 [TableBatchOperation][dotnet_TableBatchOperation]에 각 개체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-151">The following code example creates two entity objects and adds each to [TableBatchOperation][dotnet_TableBatchOperation] by using the [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="b49da-152">그런 다음 [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch]가 호출되어 작업이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called to execute the operation.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

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
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="b49da-153">파티션의 모든 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="b49da-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="b49da-154">테이블에서 파티션의 모든 엔터티를 쿼리하려면 [TableQuery][dotnet_TableQuery] 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-154">To query a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="b49da-155">다음 코드 예제에서는 'Smith'가 파티션 키인 엔터티에 대한 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-155">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="b49da-156">이 예제에서는 쿼리 결과에 있는 각 엔터티의 필드를 콘솔에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-156">This example prints the fields of each entity in the query results to the console.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct the query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print the fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="b49da-157">파티션의 엔터티 범위 검색</span><span class="sxs-lookup"><span data-stu-id="b49da-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="b49da-158">파티션의 모든 엔터티를 쿼리하지 않으려면 파티션 키 필터를 행 키 필터와 결합하여 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-158">If you don't want to query all entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="b49da-159">다음 코드 예제에서는 두 개의 필터를 사용하여 행 키(이름)가 알파벳에서 'E'보다 앞에 오는 문자로 시작하는 'Smith' 파티션의 모든 엔터티를 가져온 다음 쿼리 결과를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-159">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter before 'E' in the alphabet, then prints the query results.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through the results, displaying information about the entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="b49da-160">단일 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="b49da-160">Retrieve a single entity</span></span>
<span data-ttu-id="b49da-161">단일 특정 엔터티를 검색하는 쿼리를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-161">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="b49da-162">다음 코드에서는 [TableOperation][dotnet_TableOperation]을 사용하여 고객 'Ben Smith'를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-162">The following code uses [TableOperation][dotnet_TableOperation] to specify the customer 'Ben Smith'.</span></span> <span data-ttu-id="b49da-163">이 메서드는 컬렉션 대신 엔터티 하나만 반환하며, [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result]에서 반환되는 값은 **CustomerEntity** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-163">This method returns just one entity rather than a collection, and the returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="b49da-164">쿼리에 파티션과 행 키를 모두 지정하는 것이 테이블 서비스에서 단일 엔터티를 검색하는 가장 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-164">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print the phone number of the result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("The phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="b49da-165">엔터티 바꾸기</span><span class="sxs-lookup"><span data-stu-id="b49da-165">Replace an entity</span></span>
<span data-ttu-id="b49da-166">엔터티를 업데이트하려면 테이블 서비스에서 검색하고 엔터티 개체를 수정한 다음 변경 내용을 다시 테이블 서비스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-166">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="b49da-167">다음 코드에서는 기존 고객의 전화 번호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-167">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="b49da-168">이 코드에서는 [Insert][dotnet_TableOperation_Insert]를 호출하는 대신 [Replace][dotnet_TableOperation_Replace]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="b49da-169">[Replace][dotnet_TableOperation_Replace]를 실행하면 서버의 엔터티가 검색된 후 변경되어 작업이 실패하는 경우를 제외하고 서버에서 엔터티가 완전히 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-169">[Replace][dotnet_TableOperation_Replace] causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="b49da-170">이러한 실패는 응용 프로그램이 검색 및 업데이트 사이에 다른 응용 프로그램 구성 요소에 의해 변경된 내용을 실수로 덮어쓰는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-170">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="b49da-171">이 실패를 올바르게 처리하려면 엔터티를 다시 검색하고 변경한 다음(유효한 경우) 다른 [Replace][dotnet_TableOperation_Replace] 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-171">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="b49da-172">다음 섹션에서는 이 동작을 재정의하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-172">The next section will show you how to override this behavior.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change the phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create the Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute the operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="b49da-173">엔터티 삽입 또는 바꾸기</span><span class="sxs-lookup"><span data-stu-id="b49da-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="b49da-174">서버에서 검색한 엔터티를 변경하면 [Replace][dotnet_TableOperation_Replace] 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-174">[Replace][dotnet_TableOperation_Replace] operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="b49da-175">또한 [Replace][dotnet_TableOperation_Replace] 작업이 성공하려면 먼저 서버에서 엔터티를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-175">Furthermore, you must retrieve the entity from the server first in order for the [Replace][dotnet_TableOperation_Replace] operation to be successful.</span></span> <span data-ttu-id="b49da-176">그러나 서버에 엔터티가 있는지 알지 못하며 저장된 현재 값이 부적절하여</span><span class="sxs-lookup"><span data-stu-id="b49da-176">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant.</span></span> <span data-ttu-id="b49da-177">업데이트로 모두 덮어써야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-177">Your update should overwrite them all.</span></span> <span data-ttu-id="b49da-178">이렇게 하려면 [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-178">To accomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="b49da-179">이 작업은 마지막 업데이트가 수행된 시기에 관계없이 엔터티가 없는 경우 삽입하고, 엔터티가 있는 경우 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-179">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span>

<span data-ttu-id="b49da-180">다음 코드 예제에서는 'Fred Jones'에 대한 고객 엔터티가 만들어지고 'people' 테이블에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-180">In the following code example, a customer entity for 'Fred Jones' is created and inserted into the 'people' table.</span></span> <span data-ttu-id="b49da-181">다음으로, [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] 작업을 사용하여 동일한 파티션 키(Jones)와 행 키(Fred)를 사용하여 서버에 엔터티를 저장합니다. 이때 PhoneNumber 속성으로 다른 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-181">Next, we use the [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation to save an entity with the same partition key (Jones) and row key (Fred) to the server, this time with a different value for the PhoneNumber property.</span></span> <span data-ttu-id="b49da-182">[InsertOrReplace][dotnet_TableOperation_InsertOrReplace]를 사용하므로 모든 해당 속성 값이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="b49da-183">하지만 'Fred Jones' 엔터티가 테이블에 아직 존재하지 않으면 삽입되었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-183">However, if a 'Fred Jones' entity hadn't already existed in the table, it would have been inserted.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute the operation.
table.Execute(insertOperation);

// Create another customer entity with the same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it to the
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create the InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute the operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, the entity would be
// added to the table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="b49da-184">엔터티 속성 하위 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="b49da-184">Query a subset of entity properties</span></span>
<span data-ttu-id="b49da-185">테이블 쿼리는 모든 엔터티 속성 대신 엔터티에서 몇 개의 속성만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-185">A table query can retrieve just a few properties from an entity instead of all the entity properties.</span></span> <span data-ttu-id="b49da-186">프로젝션이라고 하는 이 기술은 특히 대역폭을 줄이며 큰 엔터티에 대한 쿼리 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="b49da-187">다음 코드의 쿼리는 테이블에 있는 엔터티의 전자 메일 주소만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-187">The query in the following code returns only the email addresses of entities in the table.</span></span> <span data-ttu-id="b49da-188">이렇게 하려면 [DynamicTableEntity][dotnet_DynamicTableEntity]의 쿼리와 [EntityResolver][dotnet_EntityResolver]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="b49da-189">[Upsert 및 쿼리 프로젝션 소개 블로그 게시물][blog_post_upsert]에서 프로젝션에 대한 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b49da-189">You can learn more about projection in the [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="b49da-190">저장소 에뮬레이터에서는 프로젝션이 지원되지 않으므로 이 코드는 Table service의 계정을 사용하는 경우에만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-190">Projection is not supported by the storage emulator, so this code runs only when you're using an account in the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define the query, and select only the Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver to work with the entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="b49da-191">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="b49da-191">Delete an entity</span></span>
<span data-ttu-id="b49da-192">엔터티를 검색한 후 엔터티 업데이트를 위해 표시된 것과 동일한 패턴을 사용하여 엔터티를 쉽게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-192">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="b49da-193">다음 코드는 고객 엔터티를 검색하고 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-193">The following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create the Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute the operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve the entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="b49da-194">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="b49da-194">Delete a table</span></span>
<span data-ttu-id="b49da-195">마지막으로, 다음 코드 예제에서는 저장소 계정에서 테이블을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-195">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="b49da-196">삭제된 테이블은 삭제 후 일정 기간 동안 다시 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-196">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete the table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="b49da-197">페이지에서 엔터티를 비동기적으로 검색</span><span class="sxs-lookup"><span data-stu-id="b49da-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="b49da-198">많은 수의 엔터티를 읽고 있는데 모든 엔터티가 반환될 때까지 기다리지 않고 엔터티가 검색되는 동안 프로세스/표시하고자 한다면 분할된 쿼리를 사용하여 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-198">If you are reading a large number of entities, and you want to process/display entities as they are retrieved rather than waiting for them all to return, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="b49da-199">이 예제에서는 여러 페이지에서 Async-Await 패턴을 사용하여 결과를 반환하는 방법을 보여 주므로 큰 결과 집합이 반환되도록 기다리는 동안 실행이 차단되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-199">This example shows how to return results in pages by using the Async-Await pattern so that execution is not blocked while you're waiting for a large set of results to return.</span></span> <span data-ttu-id="b49da-200">.NET에서 Async-Await 패턴의 사용에 대한 자세한 내용은 [Async 및 Await(C# 및 Visual Basic)를 사용한 비동기 프로그래밍](https://msdn.microsoft.com/library/hh191443.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b49da-200">For more details on using the Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery to retrieve all the entities in the table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize the continuation token to null to start from the beginning of the table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up to 1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign the new continuation token to tell the service where to
    // continue on the next iteration (or null if it has reached the end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print the number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating the end of the table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="b49da-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b49da-201">Next steps</span></span>
<span data-ttu-id="b49da-202">이제 테이블 저장소의 기본 사항을 배웠으므로 다음 링크를 따라 좀 더 복잡한 저장소 작업에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b49da-202">Now that you've learned the basics of Table storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="b49da-203">[Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)는 Windows, MacOS 및 Linux에서 Azure Storage 데이터로 시각적으로 작업할 수 있도록 해주는 Microsoft의 독립 실행형 무료 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="b49da-204">[.NET에서 Azure 테이블 저장소 시작](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="b49da-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="b49da-205">사용 가능한 API에 대한 자세한 내용은 테이블 서비스 참조 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b49da-205">View the Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="b49da-206">Storage Client Library for .NET 참조</span><span class="sxs-lookup"><span data-stu-id="b49da-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="b49da-207">REST API 참조</span><span class="sxs-lookup"><span data-stu-id="b49da-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="b49da-208">[Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="b49da-208">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="b49da-209">Azure에 데이터를 저장하기 위한 추가 옵션에 대한 자세한 내용은 추가 기능 가이드를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="b49da-209">View more feature guides to learn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="b49da-210">[.NET을 사용하여 Azure Blob 저장소를 시작](storage-dotnet-how-to-use-blobs.md) 하여 구조화되지 않은 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-210">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
* <span data-ttu-id="b49da-211">[.NET(C#)을 사용하여 SQL Database에 연결](../sql-database/sql-database-develop-dotnet-simple.md)하여 관계형 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b49da-211">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[Creating an Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx

[blog_post_upsert]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx

[dotnet_api_ref]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[dotnet_CloudTableClient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtableclient.aspx
[dotnet_CloudTable]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.aspx
[dotnet_CloudTable_Execute]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.execute.aspx
[dotnet_CloudTable_ExecuteBatch]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.executebatch.aspx
[dotnet_DynamicTableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.dynamictableentity.aspx
[dotnet_EntityResolver]: https://msdn.microsoft.com/library/jj733144.aspx
[dotnet_TableBatchOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx
[dotnet_TableBatchOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.insert.aspx
[dotnet_TableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableentity.aspx
[dotnet_TableOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.aspx
[dotnet_TableOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insert.aspx
[dotnet_TableOperation_InsertOrReplace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insertorreplace.aspx
[dotnet_TableOperation_Replace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.replace.aspx
[dotnet_TableQuery]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablequery.aspx
[dotnet_TableResult]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.aspx
[dotnet_TableResult_Result]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.result.aspx
