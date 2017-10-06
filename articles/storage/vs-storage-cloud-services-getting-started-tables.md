---
title: "테이블 저장소 및 Visual Studio 시작 aaaGet 연결 된 서비스 (클라우드 서비스) | Microsoft Docs"
description: "연결 된 서비스를 Visual Studio를 사용 하 여 tooa 저장소 계정을 연결 후 Visual Studio에서 클라우드 서비스 프로젝트에서 Azure 테이블 저장소를 사용 하 여 tooget을 시작 하는 방법"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: efb16953e05764cb162cbdae4d0eab57f781682d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="f13cb-103">Azure 테이블 저장소 및 Visual Studio 연결 서비스 시작(클라우드 서비스 프로젝트)</span><span class="sxs-lookup"><span data-stu-id="f13cb-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="f13cb-104">개요</span><span class="sxs-lookup"><span data-stu-id="f13cb-104">Overview</span></span>
<span data-ttu-id="f13cb-105">이 문서에서는 tooget 시작 hello Visual Studio를 사용 하 여 클라우드 서비스 프로젝트에서 Azure 저장소 계정을 참조 하거나 만든 후 Visual Studio에서 Azure 테이블 저장소를 사용 하는 방법을 설명 **연결 된 서비스 추가** 대화 상자 .</span><span class="sxs-lookup"><span data-stu-id="f13cb-105">This article describes how tooget started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="f13cb-106">hello **연결 된 서비스 추가** 작업 프로젝트에 hello 적절 한 NuGet 패키지 tooaccess Azure 저장소를 설치 하 고 계정에 대 한 hello 저장소 tooyour 프로젝트 구성 파일 hello 연결 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="f13cb-107">hello Azure 테이블 저장소 서비스 사용 하면 많은 양의 구조화 된 데이터를 toostore 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="f13cb-108">hello 서비스는 내부 및 외부 hello Azure 클라우드에서 인증 된 호출을 허용 하는 NoSQL 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="f13cb-109">Azure 테이블은 구조화된 비관계형 데이터를 저장하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="f13cb-110">시작 tooget, 먼저 toocreate 테이블 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-110">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="f13cb-111">Toocreate Azure 테이블 코드에 어떻게 하 고 어떻게 tooperform 기본 테이블 및 엔터티 작업을 추가, 수정, 읽기, 읽기 등 테이블 엔터티도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-111">We'll show you how toocreate an Azure table in code, and also how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="f13cb-112">hello 샘플은 C로 작성 된\# 하 고 hello 사용 [.NET 용 Microsoft Azure 저장소 클라이언트 라이브러리](https://msdn.microsoft.com/library/azure/dn261237.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-112">hello samples are written in C\# code and use hello [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="f13cb-113">**참고:** hello 가끔씩 tooAzure 저장소 호출을 수행 하는 Api의 일부는 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-113">**NOTE:** Some of hello APIs that perform calls out tooAzure storage are asynchronous.</span></span> <span data-ttu-id="f13cb-114">자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](http://msdn.microsoft.com/library/hh191443.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f13cb-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="f13cb-115">아래 hello 코드는 비동기 프로그래밍 메서드를 사용 하 되 고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-115">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="f13cb-116">테이블을 프로그래밍 방식으로 조작하는 방법에 대한 자세한 내용은 [.NET을 사용하여 Azure 테이블 저장소 시작](storage-dotnet-how-to-use-tables.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f13cb-116">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="f13cb-117">Azure 저장소에 대한 일반적인 내용은 [저장소 설명서](https://azure.microsoft.com/documentation/services/storage/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f13cb-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="f13cb-118">Azure 클라우드 서비스에 대한 일반적인 내용은 [클라우드 서비스 설명서](https://azure.microsoft.com/documentation/services/cloud-services/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f13cb-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="f13cb-119">ASP.NET 응용 프로그램을 프로그래밍하는 방법에 대한 자세한 내용은 [ASP.NET](http://www.asp.net) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f13cb-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="f13cb-120">코드에서 테이블 액세스하기</span><span class="sxs-lookup"><span data-stu-id="f13cb-120">Access tables in code</span></span>
<span data-ttu-id="f13cb-121">클라우드 서비스 프로젝트에서 tooaccess 테이블 tooinclude hello 다음 Azure 테이블 저장소에 액세스 하는 항목 tooany C# 소스 파일이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-121">tooaccess tables in cloud service projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="f13cb-122">이러한 hello C# 파일의 hello 위쪽 hello 네임 스페이스 선언을 포함 **를 사용 하 여** 문.</span><span class="sxs-lookup"><span data-stu-id="f13cb-122">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="f13cb-123">저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f13cb-124">다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성에서 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-124">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="f13cb-125">다음 예제는 hello에서 모두 hello 코드 앞에 코드 위의 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-125">Use all of hello above code in front of hello code in hello following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="f13cb-126">가져오기는 **CloudTableClient** 개체 저장소 계정의 tooreference hello 테이블 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-126">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="f13cb-127">가져오기는 **CloudTable** 개체 tooreference 특정 테이블 및 엔터티를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-127">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="f13cb-128">코드에서 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="f13cb-128">Create a table in code</span></span>
<span data-ttu-id="f13cb-129">toocreate hello Azure 테이블 추가 호출 너무**CreateIfNotExistsAsync** toohello 확보 한 후 한 **CloudTable** hello "코드에서 액세스 테이블" 섹션에 설명 된 대로 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-129">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync** toohello after you get a **CloudTable** object as described in hello "Access tables in code" section.</span></span>

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="f13cb-130">엔터티 tooa 테이블 추가</span><span class="sxs-lookup"><span data-stu-id="f13cb-130">Add an entity tooa table</span></span>
<span data-ttu-id="f13cb-131">엔터티 tooa 테이블 tooadd hello 엔터티 속성을 정의 하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-131">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="f13cb-132">hello 다음 코드에서는 정의 라고 하는 엔터티 클래스 **CustomerEntity** hello 행 키로 고객의 이름 및 hello 성 hello 파티션 키로 사용 하 여 hello 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-132">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and hello last name as hello partition key.</span></span>

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

<span data-ttu-id="f13cb-133">엔터티를 포함 된 테이블 작업을 마쳤으면 hello를 사용 하 여 **CloudTable** "테이블에에서 액세스 코드입니다." 앞부분에서 만든 개체</span><span class="sxs-lookup"><span data-stu-id="f13cb-133">Table operations involving entities are done using hello **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="f13cb-134">hello **TableOperation** 개체 hello 작업 toobe 완료를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-134">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="f13cb-135">코드 예제에서 보여 주는 방법을 다음 hello toocreate는 **CloudTable** 개체 및 **CustomerEntity** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-135">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="f13cb-136">tooprepare hello 작업 한 **TableOperation** hello 테이블로 tooinsert hello 고객 엔터티가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-136">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="f13cb-137">호출 하 여 hello 작업을 실행 하는 마지막으로, **CloudTable.ExecuteAsync**합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-137">Finally, hello operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="f13cb-138">엔터티 일괄 삽입</span><span class="sxs-lookup"><span data-stu-id="f13cb-138">Insert a batch of entities</span></span>
<span data-ttu-id="f13cb-139">하나의 쓰기 작업으로 테이블에 여러 엔터티를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="f13cb-140">hello 다음 코드 예제에서는 두 엔터티 개체 ("홍길동" 및 "Ben Smith")를 만들고, tooa 추가 **에서는 TableBatchOperation** 개체를 사용 하 여 hello 삽입 메서드를 다음 시작 작업을 호출 하 여 hello  **CloudTable.ExecuteBatchAsync**합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-140">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello Insert method, and then starts hello operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

    // Create hello batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a customer entity and add it toohello table.
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";
    customer1.PhoneNumber = "425-555-0104";

    // Create another customer entity and add it toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    customer2.PhoneNumber = "425-555-0102";

    // Add both customer entities toohello batch insert operation.
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);

    // Execute hello batch operation.
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="f13cb-141">파티션에서 모든 hello 엔터티가 가져오기</span><span class="sxs-lookup"><span data-stu-id="f13cb-141">Get all of hello entities in a partition</span></span>
<span data-ttu-id="f13cb-142">테이블의 모든 파티션에서 사용 하 여 hello 엔터티가 tooquery는 **TableQuery** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-142">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="f13cb-143">hello 다음 코드 예제에서는 지정 엔터티 'Smith'는 hello 파티션 키에 대 한 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-143">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="f13cb-144">이 예제는 hello 쿼리 결과 toohello 콘솔의 각 엔터티에의 hello 필드를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-144">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
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


## <a name="get-a-single-entity"></a><span data-ttu-id="f13cb-145">단일 엔터티 가져오기</span><span class="sxs-lookup"><span data-stu-id="f13cb-145">Get a single entity</span></span>
<span data-ttu-id="f13cb-146">단일, 특정 엔터티 쿼리 tooget를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-146">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="f13cb-147">hello 다음 코드에서는 **TableOperation** toospecify ' 홍길동 ' 이라고 하는 고객 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-147">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="f13cb-148">이 메서드는 컬렉션을이 아닌 하나의 엔터티를 반환 하 고 hello에 대 한 값을 반환 했습니다. **TableResult.Result** 는 **CustomerEntity** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-148">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="f13cb-149">Hello 가장 빠른 방법은 tooretrieve hello에서 단일 엔터티 쿼리의 모두 파티션 및 행 키를 지정 하는 **테이블** 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-149">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="f13cb-150">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="f13cb-150">Delete an entity</span></span>
<span data-ttu-id="f13cb-151">엔터티를 찾은 후 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="f13cb-152">hello 다음 코드에서 찾는 이름이 "Ben Smith" 인 customer 엔터티 하 고, 있을 경우 해당 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f13cb-152">hello following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a><span data-ttu-id="f13cb-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f13cb-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

