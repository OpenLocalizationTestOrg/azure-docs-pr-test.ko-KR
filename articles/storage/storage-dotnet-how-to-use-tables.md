---
title: "aaaGet.NET을 사용 하 여 Azure 테이블 저장소 시작 | Microsoft Docs"
description: "Azure 테이블 저장소에는 NoSQL 데이터 저장소를 사용 하 여 hello 클라우드에서 구조화 된 데이터를 저장 합니다."
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
ms.openlocfilehash: 9635079d61d874ff7f4bc9e7d610e0ad54b4fd6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a>.NET을 사용하여 Azure 테이블 저장소 시작
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Azure 테이블 저장소는 구조화 된 NoSQL schemaless 디자인에 키/특성을 제공 하는 hello 클라우드에서 데이터 저장소를 저장 하는 서비스입니다. 테이블 저장소는 schemaless, 되므로 쉽게 tooadapt hello 데이터 응용 프로그램 evolve의 필요성을 해결 합니다. 액세스 tooTable 저장소 데이터 신속 하 고 다양 한 유형의 응용 프로그램에 대 한 비용 효율적인 및 비슷한 데이터 볼륨에 대 한 기존의 SQL 보다 비용에 일반적으로 낮은 합니다.

웹 응용 프로그램, 주소록, 장치 정보 또는 다른 유형의 서비스에 필요한 메타 데이터에 대 한 테이블 저장소 toostore 유연한 데이터 집합 사용자 데이터 등을 사용할 수 있습니다. 테이블의 모든 엔터티 수를 저장할 수 있습니다 및 저장소 계정은 임의 개수의 테이블 hello 저장소 계정의 toohello 용량 한계를 포함할 수 있습니다.

### <a name="about-this-tutorial"></a>이 자습서 정보
이 자습서에서는 어떻게 toouse hello [.NET 용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/) 몇 가지 일반적인 Azure 테이블 저장소 시나리오에 있습니다. 테이블 만들기 및 삭제, 테이블 데이터 삽입, 업데이트, 삭제 및 쿼리 등 C# 예제를 사용하는 다음과 같은 시나리오가 제시됩니다.

## <a name="prerequisites"></a>필수 조건

하면 필요한 hello toocomplete 다음이 자습서에서는 성공적으로:

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [.NET용 Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [.NET용 Azure 구성 관리자](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Azure 저장소 계정](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>추가 샘플
테이블 저장소를 사용하는 추가 예제는 [.NET에서 Azure 테이블 저장소 시작](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)을 참조하세요. Hello 샘플 응용 프로그램을 다운로드 하 고 실행 하거나 GitHub에서 hello 코드를 찾아보려면 수 있습니다.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>지시문을 사용하여 추가
Hello 다음 추가 **를 사용 하 여** 지시문 toohello 맨 hello `Program.cs` 파일:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a>Hello 연결 문자열을 구문 분석
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a>Hello 테이블 서비스 클라이언트 만들기
hello [CloudTableClient] [ dotnet_CloudTableClient] 클래스를 사용 하면 tooretrieve 테이블 및 테이블 저장소에 저장 된 엔터티. 한 가지 방법은 toocreate hello 테이블 서비스 클라이언트는 다음과 같습니다.

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

이제 준비 toowrite 코드에서 데이터를 읽고 tooTable 저장소 데이터를 기록 하는 합니다.

## <a name="create-a-table"></a>테이블 만들기
이 예에서는 어떻게 toocreate 아직 없는 경우 테이블:

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference toohello table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-tooa-table"></a>엔터티 tooa 테이블 추가
엔터티는 tooC # 개체에서 파생 된 사용자 지정 클래스를 사용 하 여 매핑할 [TableEntity][dotnet_TableEntity]합니다. 엔터티 tooa 테이블 tooadd hello 엔터티 속성을 정의 하는 클래스를 만듭니다. hello 다음 코드에서는 정의 hello 파티션 키로 hello 행 키 및 last name로 hello 고객 이름을 사용 하는 엔터티 클래스입니다. 함께 엔터티의 파티션과 행 키는 고유 하 게 식별 hello 테이블에 있습니다. Hello 동일한 파티션 키를 서로 다른 엔터티 보다 더 빠르게 쿼리할 수 있는 엔터티의 파티션 키, 하지만 다양 한 파티션 키를 사용 하 여 병렬 작업의 확장성이 높아집니다. 예를 들어 hello에서 파생 된 지원 되는 형식, 테이블에 저장 된 엔터티 toobe 이어야 [TableEntity] [ dotnet_TableEntity] 클래스입니다. 테이블의 toostore 원하는 엔터티 속성 hello 형식의 공용 속성 이어야 하 고 가져오고 값 설정을 지원 해야 합니다. 또한 엔터티 형식은 *반드시* 매개 변수가 없는 생성자를 표시해야 합니다.

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

Hello를 통해 엔터티를 포함 하는 테이블 작업을 수행할 [CloudTable] [ dotnet_CloudTable] hello "테이블 만들기" 섹션에서 만든 개체입니다. hello 수행 하는 작업 toobe로 표시 됩니다는 [TableOperation] [ dotnet_TableOperation] 개체입니다. hello 다음 코드 예제에서는 만드는 방법을 보여 줍니다 hello hello [CloudTable] [ dotnet_CloudTable] 개체 차례로 **CustomerEntity** 개체입니다. tooprepare hello 작업 한 [TableOperation] [ dotnet_TableOperation] 개체가 tooinsert hello 고객 엔터티 hello 테이블에 생성 됩니다. 호출 하 여 hello 작업을 실행 하는 마지막으로, [CloudTable][dotnet_CloudTable].[ 실행][dotnet_CloudTable_Execute]합니다.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>엔터티 일괄 삽입
하나의 쓰기 작업으로 테이블에 엔터티를 일괄 삽입할 수 있습니다. 일괄 작업에 대한 다른 참고 사항은 다음과 같습니다.

* 업데이트, 삭제 및 삽입을 수행할 수 있습니다 hello에 일괄 처리 작업을 단일 동일 합니다.
* 단일 일괄 처리 작업 too100 엔터티를 포함할 수 있습니다.
* 단일 일괄 처리 작업의 모든 엔터티가 hello 있어야 합니다. 동일한 파티션 키입니다.
* 일괄 처리 작업으로 쿼리 가능한 tooperform 상태인 동안 hello hello 일괄 처리에서 유일한 작업 이어야 합니다.

hello 다음 코드 예제에서는 두 엔터티 개체를 만들고 각각 너무 추가[에서는 TableBatchOperation] [ dotnet_TableBatchOperation] hello를 사용 하 여 [삽입] [ dotnet_TableBatchOperation_Insert] 메서드입니다. 그런 다음 [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] tooexecute hello 작업 이라고 합니다.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

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
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a>파티션의 모든 엔터티 검색
파티션에서 사용 하 여 모든 엔터티에 대 한 테이블 tooquery는 [TableQuery] [ dotnet_TableQuery] 개체입니다. hello 다음 코드 예제에서는 지정 엔터티 'Smith'는 hello 파티션 키에 대 한 필터입니다. 이 예제는 hello 쿼리 결과 toohello 콘솔의 각 엔터티에의 hello 필드를 인쇄합니다.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct hello query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print hello fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>파티션의 엔터티 범위 검색
않으려면 tooquery 파티션의 모든 엔터티, 행 키 필터와 hello 파티션 키 필터를 결합 하 여 범위를 지정할 수 있습니다. hello 다음 코드 예제에서는 두 개의 필터 tooget 모든 엔터티 파티션에 'Smith' hello 행 키 (이름) 'E' 전에 hello 알파벳에서 문자로 시작 후 hello 쿼리 결과 출력 위치입니다.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through hello results, displaying information about hello entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a>단일 엔터티 검색
단일, 특정 엔터티 쿼리 tooretrieve를 작성할 수 있습니다. hello 다음 코드에서는 [TableOperation] [ dotnet_TableOperation] toospecify hello 고객 ' 홍길동 '. 이 메서드는 컬렉션을이 아닌 하나의 엔터티를 반환 하 고 hello에 대 한 값을 반환 했습니다. [TableResult][dotnet_TableResult].[ 결과] [ dotnet_TableResult_Result] 는 **CustomerEntity** 개체입니다. 쿼리에서 모두 파티션 및 행 키를 지정 하는 hello 가장 빠른 방법은 tooretrieve hello 테이블 서비스에서 단일 엔터티입니다.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print hello phone number of hello result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("hello phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a>엔터티 바꾸기
엔터티에 tooupdate hello 테이블 서비스에서 검색, hello 엔터티 개체를 수정 및 다음 hello 변경 내용을 저장할 toohello 테이블 서비스를 다시 합니다. hello 다음 코드 기존 고객의 전화 번호를 변경합니다. 이 코드에서는 [Insert][dotnet_TableOperation_Insert]를 호출하는 대신 [Replace][dotnet_TableOperation_Replace]를 사용합니다. [대체] [ dotnet_TableOperation_Replace] hello 서버 hello 엔터티 hello 작업이 실패 하는 경우, 검색 된 이후 변경 되지 않은 원인을 hello 엔터티 toobe hello 서버에 완벽 하 게 대체 합니다. 이 오류는 tooprevent 검색 hello와 응용 프로그램의 다른 구성 요소 업데이트 간 응용 프로그램에서 변경 내용을 덮어쓰는 수행 합니다. hello 적절 한 처리가 오류는 tooretrieve hello 엔터티 다시를 원하는 대로 변경한 (여전히 유효한 경우) 한 다음 다른를 수행 [대체] [ dotnet_TableOperation_Replace] 작업 합니다. 다음 섹션 hello 방법을 살펴보겠습니다 toooverride이이 동작 합니다.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change hello phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create hello Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute hello operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a>엔터티 삽입 또는 바꾸기
[대체] [ dotnet_TableOperation_Replace] hello 엔터티 hello 서버에서 검색 된 이후 변경 된 경우 작업이 실패 합니다. 또한 검색 해야 hello 서버에서 엔터티를 hello 먼저 hello에 대 한 순서 대로 [대체] [ dotnet_TableOperation_Replace] 작업 toobe 성공 합니다. 그러나 경우에 따라 모르는 hello 엔터티 hello 서버에 있고 hello 현재 값에 저장 된 관련이 없는 경우. 업데이트로 모두 덮어써야 하는 경우도 있습니다. tooaccomplish이를 사용 하 여 프로그램 [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] 작업 합니다. 이 작업이 존재 하지 않으면 하거나 hello 마지막 업데이트가 수행 된 경우에 관계 없이 수행 하면 대체 하는 경우 hello 엔터티를 삽입 합니다.

다음 코드 예제는 hello, ' Fred Jones'에 대 한 고객 엔터티가 생성 되 고 hello '사람' 테이블에 삽입 합니다. Hello 사용 다음으로, [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] 작업 toosave hello로 엔터티가 동일한 파티션 키 (Jones)와 행 (Fred) toohello 서버 hello 전화 번호에 대 한이 이번에는 다른 값을를 키 속성입니다. [InsertOrReplace][dotnet_TableOperation_InsertOrReplace]를 사용하므로 모든 해당 속성 값이 바뀝니다. 그러나 ' Fred Jones' 엔터티는 hello 테이블에 이미 하지 않은, 것은 삽입 되어 있습니다.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute hello operation.
table.Execute(insertOperation);

// Create another customer entity with hello same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it toothe
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create hello InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute hello operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, hello entity would be
// added toohello table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a>엔터티 속성 하위 집합 쿼리
테이블 쿼리를 모든 hello 엔터티 속성 대신 엔터티에서 몇 개의 속성을 검색할 수 있습니다. 프로젝션이라고 하는 이 기술은 특히 대역폭을 줄이며 큰 엔터티에 대한 쿼리 성능을 향상시킬 수 있습니다. 코드 다음 hello hello 쿼리 hello 테이블의 엔터티만 hello 전자 메일 주소를 반환 합니다. 이렇게 하려면 [DynamicTableEntity][dotnet_DynamicTableEntity]의 쿼리와 [EntityResolver][dotnet_EntityResolver]를 사용합니다. Hello에 프로젝션 하는 방법에 대 한 자세히 알아볼 수 있습니다 [Upsert 소개 및 쿼리 프로젝션 블로그 게시물][blog_post_upsert]합니다. 이 코드는 hello 테이블 서비스에서 계정을 사용 하는 경우에 실행 되므로 프로젝션 hello 저장소 에뮬레이터에서 지원 되지 않습니다.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define hello query, and select only hello Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver toowork with hello entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a>엔터티 삭제
Hello를 사용 하 여 검색 한 후에 쉽게 엔터티를 삭제할 수 있습니다 엔터티 업데이트에 대 한 표시 된 같은 패턴입니다. hello 코드 다음 검색 하 고 고객 엔터티를 삭제 합니다.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create hello Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute hello operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve hello entity.");
}
```

## <a name="delete-a-table"></a>테이블 삭제
마지막으로, 다음 코드 예제는 hello 저장소 계정에서 테이블을 삭제 합니다. 삭제 된 테이블을 사용할 수 없는 toobe hello 삭제 시간 기간에 대 한 다시 생성 됩니다.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete hello table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a>페이지에서 엔터티를 비동기적으로 검색
많은 수의 엔터티를 읽고 있는 기다리지 모든 tooreturn를 검색할 수 있습니다 엔터티 세그먼트 쿼리를 사용 하는 것이 아니라 검색 된 대로 tooprocess/디스플레이 엔터티 하려는 경우. 이 예제에서는 다양 한 결과 tooreturn에 대 한 tooreturn 결과 실행 하는 동안 차단 되지 않은 비동기 Await hello 패턴을 사용 하 여 페이지를 기다리는 방법을 보여 줍니다. 사용 하 여 대 한 자세한 내용은.net에서 비동기 Await 패턴 hello, 참조 [Async 및 Await (C# 및 Visual Basic)를 사용한 비동기 프로그래밍](https://msdn.microsoft.com/library/hh191443.aspx)합니다.

```csharp
// Initialize a default TableQuery tooretrieve all hello entities in hello table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize hello continuation token toonull toostart from hello beginning of hello table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up too1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign hello new continuation token tootell hello service where to
    // continue on hello next iteration (or null if it has reached hello end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print hello number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating hello end of hello table.
} while(continuationToken != null);
```

## <a name="next-steps"></a>다음 단계
테이블 저장소의 hello 기본 사항 학습 한, 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn를 수행 합니다.

* [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.
* [.NET에서 Azure 테이블 저장소 시작](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)
* 사용 가능한 Api에 대 한 자세한 내용은 hello 테이블 서비스 참조 설명서를 봅니다.
* [Storage Client Library for .NET 참조](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [REST API 참조](http://msdn.microsoft.com/library/azure/dd179355)
* Toosimplify hello 코드 작성 방법에 대해 알아봅니다 hello를 사용 하 여 Azure 저장소와 toowork [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)
* Azure에 데이터를 저장 하기 위한 추가 옵션에 대 한 자세한 기능 가이드 toolearn을 봅니다.
* [.NET을 사용 하 여 Azure Blob 저장소 시작](storage-dotnet-how-to-use-blobs.md) toostore 구조화 되지 않은 데이터입니다.
* [.NET (C#)를 사용 하 여 데이터베이스 tooSQL 연결](../sql-database/sql-database-develop-dotnet-simple.md) toostore 관계형 데이터입니다.

[Download and install hello Azure SDK for .NET]: /develop/net/
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
