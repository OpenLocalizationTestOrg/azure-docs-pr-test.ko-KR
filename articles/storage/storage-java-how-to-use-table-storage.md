---
title: "Java에서 테이블 저장소를 사용하는 방법 | Microsoft Docs"
description: "Azure 테이블 저장소, NoSQL 데이터 저장소를 사용하여 클라우드에 구조화된 데이터를 저장합니다."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: a4d6f144cc6940ffe2b2c6f27553cd7aa3bcb381
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-java"></a><span data-ttu-id="c2b78-103">Java에서 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="c2b78-103">How to use Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="c2b78-104">개요</span><span class="sxs-lookup"><span data-stu-id="c2b78-104">Overview</span></span>
<span data-ttu-id="c2b78-105">이 가이드에서는 Azure 테이블 저장소 서비스를 사용하여 일반 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-105">This guide will show you how to perform common scenarios using the Azure Table storage service.</span></span> <span data-ttu-id="c2b78-106">샘플은 Java로 작성되었으며 [Java용 Azure Storage SDK][Azure Storage SDK for Java](영문)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-106">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="c2b78-107">여기에서 다루는 시나리오에는 **creating**, **listing**, **deleting** 테이블과 테이블의 **inserting**, **querying**, **modifying**, **deleting** 엔터티가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-107">The scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="c2b78-108">테이블에 대한 자세한 내용은 [다음 단계](#Next-Steps) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="c2b78-108">For more information on tables, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="c2b78-109">SDK는 Android 장치에서 Azure 저장소를 사용하는 개발자에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="c2b78-110">자세한 내용은 [Android용 Azure Storage SDK][Azure Storage SDK for Android]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2b78-110">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="c2b78-111">Java 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c2b78-111">Create a Java application</span></span>
<span data-ttu-id="c2b78-112">이 가이드에서는 Java 응용 프로그램 내에서 로컬로 실행할 수 있거나 Azure의 웹 역할 또는 작업자 역할 내에서 실행되는 코드에서 실행할 수 있는 저장소 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="c2b78-113">그러려면 JDK(Java Development Kit)를 설치하고 Azure 구독에서 Azure 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-113">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="c2b78-114">그러고 나면 개발 시스템에서 GitHub의 [Java용 Azure Storage SDK][Azure Storage SDK for Java] 리포지토리에 있는 최소 요구 사항과 종속성을 충족하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-114">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="c2b78-115">시스템에서 해당 요구 사항을 충족하는 경우에는 리포지토리에서 시스템의 Java용 Azure Storage Library를 다운로드 및 설치하기 위한 지침을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-115">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="c2b78-116">작업을 완료하고 나면 이 문서의 예를 사용하는 Java 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-116">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="c2b78-117">테이블 저장소에 액세스하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="c2b78-117">Configure your application to access table storage</span></span>
<span data-ttu-id="c2b78-118">테이블에 액세스하기 위해 Microsoft Azure 저장소 API를 사용하려는 Java 파일의 맨 위에 다음 import 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-118">Add the following import statements to the top of the Java file where you want to use Microsoft Azure storage APIs to access tables:</span></span>

```java
// Include the following imports to use table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="c2b78-119">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="c2b78-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="c2b78-120">Azure 저장소 클라이언트는 저장소 연결 문자열을 사용하여 데이터 관리 서비스에 액세스하기 위한 끝점 및 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-120">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="c2b78-121">클라이언트 응용 프로그램에서 실행할 경우 *AccountName*과 *AccountKey* 값에 대해 [Azure Portal](https://portal.azure.com)에 나열된 저장소 계정의 이름과 기본 선택키를 사용하여 다음 형식의 저장소 연결 문자열을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-121">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="c2b78-122">이 예제는 정적 필드가 연결 문자열을 포함할 수 있도록 선언하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-122">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="c2b78-123">Microsoft Azure의 역할 내에서 실행되는 응용 프로그램에서는 이 문자열이 서비스 구성 파일 *ServiceConfiguration.cscfg*에 저장될 수 있고, **RoleEnvironment.getConfigurationSettings** 메서드 호출을 통해 이 문자열에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-123">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="c2b78-124">다음은 서비스 구성 파일에서 이름이 **StorageConnectionString** 인 *설정* 요소에서 연결 문자열을 가져오는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-124">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="c2b78-125">다음 샘플에서는 저장소 연결 문자열을 가져오기 위해 위의 두 메서드 중 하나를 사용한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-125">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="c2b78-126">방법: 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="c2b78-126">How to: Create a table</span></span>
<span data-ttu-id="c2b78-127">**CloudTableClient** 개체를 사용하면 테이블 및 엔터티에 대한 참조 개체를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="c2b78-128">다음 코드에서는 한 **CloudTableClient** 개체를 만들고 이 개체를 사용하여 “people”이라는 테이블을 나타내는 새 **CloudTable** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-128">The following code creates a **CloudTableClient** object and uses it to create a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="c2b78-129">(참고: **CloudStorageAccount** 개체를 만들 수 있는 방법이 더 있습니다. 자세한 내용은 **Azure Storage 클라이언트 SDK 참조**에서 [CloudStorageAccount]를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="c2b78-129">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create the table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-tables"></a><span data-ttu-id="c2b78-130">테이블 나열하는 방법</span><span class="sxs-lookup"><span data-stu-id="c2b78-130">How to: List the tables</span></span>
<span data-ttu-id="c2b78-131">테이블의 목록을 가져오려면 **CloudTableClient.listTables()** 메서드를 호출하여 반복 가능한 테이블 이름 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-131">To get a list of tables, call the **CloudTableClient.listTables()** method to retrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through the collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-to-a-table"></a><span data-ttu-id="c2b78-132">방법: 테이블에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="c2b78-132">How to: Add an entity to a table</span></span>
<span data-ttu-id="c2b78-133">엔터티는 **TableEntity**를 구현하는 사용자 지정 클래스를 사용하여 Java 개체에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-133">Entities map to Java objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="c2b78-134">사용 편의를 위해 **TableServiceEntity** 클래스는 **TableEntity**를 구현하고, 리플렉션을 사용하여 속성에 맞춰 명명된 getter 및 setter 메서드에 속성을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-134">For convenience, the **TableServiceEntity** class implements **TableEntity** and uses reflection to map properties to getter and setter methods named for the properties.</span></span> <span data-ttu-id="c2b78-135">테이블에 엔터티를 추가하려면 먼저 엔터티의 속성을 정의하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-135">To add an entity to a table, first create a class that defines the properties of your entity.</span></span> <span data-ttu-id="c2b78-136">다음 코드에서는 고객의 이름을 행 키로 사용하고 성을 파티션 키로 사용하는 엔터티 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-136">The following code defines an entity class which uses the customer's first name as the row key, and last name as the partition key.</span></span> <span data-ttu-id="c2b78-137">엔터티의 파티션과 행 키가 결합되어 테이블에서 엔터티를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-137">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="c2b78-138">동일한 파티션 키를 가진 엔터티는 다른 파티션 키를 가진 엔터티보다 더 빨리 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-138">Entities with the same partition key can be queried faster than those with different partition keys.</span></span>

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

<span data-ttu-id="c2b78-139">엔터티를 포함하는 테이블 작업에는 **TableOperation** 개체가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="c2b78-140">이 개체는 엔터티에서 수행될 작업을 정의하고, 이 작업은 **CloudTable** 개체와 함께 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-140">This object defines the operation to be performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="c2b78-141">다음 코드에서는 **CustomerEntity** 클래스의 새 인스턴스를 저장될 일부 고객 데이터와 함께 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-141">The following code creates a new instance of the **CustomerEntity** class with some customer data to be stored.</span></span> <span data-ttu-id="c2b78-142">그런 다음 엔터티를 테이블에 삽입하기 위해 **TableOperation.insertOrReplace**를 호출하여 **TableOperation** 개체를 만들고, 새로운 **CustomerEntity**를 이 개체와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-142">The code next calls **TableOperation.insertOrReplace** to create a **TableOperation** object to insert an entity into a table, and associates the new **CustomerEntity** with it.</span></span> <span data-ttu-id="c2b78-143">끝으로 이 코드는 **CloudTable** 개체에 대해 **execute** 메서드를 호출하여 'people' 테이블 및 새로운 **TableOperation**을 지정한 후, 새 고객 엔터티를 'people' 테이블에 삽입하거나, 이미 있는 경우 바꾸기 위해 저장소 서비스로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-143">Finally, the code calls the **execute** method on the **CloudTable** object, specifying the "people" table and the new **TableOperation**, which then sends a request to the storage service to insert the new customer entity into the "people" table, or replace the entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="c2b78-144">방법: 엔터티 일괄 삽입</span><span class="sxs-lookup"><span data-stu-id="c2b78-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="c2b78-145">하나의 쓰기 작업으로 테이블 서비스에 엔터티를 일괄 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-145">You can insert a batch of entities to the table service in one write operation.</span></span> <span data-ttu-id="c2b78-146">다음 코드는 **TableBatchOperation** 개체를 만든 다음, 이 개체에 3개의 삽입 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-146">The following code creates a **TableBatchOperation** object, then adds three insert operations to it.</span></span> <span data-ttu-id="c2b78-147">각 삽입 작업을 추가하기 위해 새 엔터티 개체를 만들고 값을 설정한 후 **insert** 메서드를 **TableBatchOperation** 개체에 대해 호출하여 해당 엔터티를 새로운 삽입 작업과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-147">Each insert operation is added by creating a new entity object, setting its values, and then calling the **insert** method on the **TableBatchOperation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="c2b78-148">그런 다음, 이 코드는 **CloudTable** 개체에 대해 **execute**를 호출하여 'people' 테이블 및 **TableBatchOperation** 개체를 지정한 후, 테이블 일괄 작업을 단일 요청으로 저장소 서비스로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-148">Then the code calls **execute** on the **CloudTable** object, specifying the "people" table and the **TableBatchOperation** object, which sends the batch of table operations to the storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity to add to the table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity to add to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity to add to the table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute the batch of operations on the "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="c2b78-149">일괄 작업에 대해 유의할 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-149">Some things to note on batch operations:</span></span>

* <span data-ttu-id="c2b78-150">최대 100개의 삽입, 삭제, 병합, 바꾸기, 삽입 또는 병합 및 삽입 또는 바꾸기 작업을 임의로 조합하여 단일 일괄 작업으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-150">You can perform up to 100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="c2b78-151">검색 작업이 일괄 작업의 유일한 작업이면 일괄 작업에 검색 작업이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-151">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>
* <span data-ttu-id="c2b78-152">단일 일괄 작업의 모든 엔터티에 동일한 파티션 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-152">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="c2b78-153">일괄 작업은 4MB 데이터 페이로드로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-153">A batch operation is limited to a 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="c2b78-154">방법: 파티션의 모든 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="c2b78-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="c2b78-155">테이블에서 파티션의 엔터티를 쿼리하려는 경우 **TableQuery**를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-155">To query a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="c2b78-156">지정된 결과 유형을 반환하는 쿼리를 특정 테이블에 대해 만들려면 **TableQuery.from** 을 호출하십시오.</span><span class="sxs-lookup"><span data-stu-id="c2b78-156">Call **TableQuery.from** to create a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="c2b78-157">다음 코드는 'Smith'가 파티션 키인 엔터티에 대한 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-157">The following code specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="c2b78-158">**TableQuery.generateFilterCondition** 은 쿼리에 필요한 필터를 만들기 위한 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-158">**TableQuery.generateFilterCondition** is a helper method to create filters for queries.</span></span> <span data-ttu-id="c2b78-159">쿼리에 필터를 적용하려면 **TableQuery.from** 메서드에 의해 반환된 참조에 대해 **where**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-159">Call **where** on the reference returned by the **TableQuery.from** method to apply the filter to the query.</span></span> <span data-ttu-id="c2b78-160">**CloudTable** 개체에 대해 **execute**를 호출하여 쿼리가 실행되면 쿼리는 **CustomerEntity** 결과 유형이 지정된 **반복기**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-160">When the query is executed with a call to **execute** on the **CloudTable** object, it returns an **Iterator** with the **CustomerEntity** result type specified.</span></span> <span data-ttu-id="c2b78-161">그러면 반환된 **반복기** 를 for each 루프에서 사용하여 결과를 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-161">You can then use the **Iterator** returned in a for each loop to consume the results.</span></span> <span data-ttu-id="c2b78-162">이 코드는 쿼리 결과에 있는 각 엔터티의 필드를 콘솔에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-162">This code prints the fields of each entity in the query results to the console.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as the partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through the results, displaying information about the entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="c2b78-163">방법: 파티션의 엔터티 범위 검색</span><span class="sxs-lookup"><span data-stu-id="c2b78-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="c2b78-164">파티션의 모든 엔터티를 쿼리하지 않으려면 비교 연산자를 필터에서 사용하여 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-164">If you don't want to query all the entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="c2b78-165">다음 코드는 두 개의 필터를 결합하여 행 키(이름)가 알파벳에서 'E'까지의 문자로 시작하는 'Smith' 파티션의 모든 엔터티를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-165">The following code combines two filters to get all entities in partition "Smith" where the row key (first name) starts with a letter up to 'E' in the alphabet.</span></span> <span data-ttu-id="c2b78-166">그런 다음 쿼리 결과를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-166">Then it prints the query results.</span></span> <span data-ttu-id="c2b78-167">이 가이드의 일괄 삽입 섹션에 있는 테이블에 추가된 엔터티를 사용할 경우 두 개의 엔터티(Ben 및 Denise Smith)만 반환되고 Jeff Smith는 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-167">If you use the entities added to the table in the batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where the row key is less than the letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine the two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as the partition key,
    // with the row key being up to the letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through the results, displaying information about the entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="c2b78-168">방법: 단일 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="c2b78-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="c2b78-169">단일 특정 엔터티를 검색하는 쿼리를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-169">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="c2b78-170">다음 코드는 **TableQuery**를 만들고 필터를 사용하는 대신, **TableOperation.retrieve**를 파티션 키 및 행 키 매개 변수와 함께 호출하여 고객 'Jeff Smith'를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-170">The following code calls **TableOperation.retrieve** with partition key and row key parameters to specify the customer "Jeff Smith", instead of creating a **TableQuery** and using filters to do the same thing.</span></span> <span data-ttu-id="c2b78-171">코드가 실행되면 검색 작업은 컬렉션 대신 엔터티 1개만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-171">When executed, the retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="c2b78-172">**getResultAsType** 메서드는 결과를 할당 대상, 즉 **CustomerEntity** 개체의 형식으로 캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-172">The **getResultAsType** method casts the result to the type of the assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="c2b78-173">이 형식이 쿼리에 지정된 형식과 호환되지 않으면 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-173">If this type is not compatible with the type specified for the query, an exception will be thrown.</span></span> <span data-ttu-id="c2b78-174">파티션과 행 키가 정확하게 일치하는 엔터티가 없는 경우 null 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="c2b78-175">쿼리에 파티션과 행 키를 모두 지정하는 것이 테이블 서비스에서 단일 엔터티를 검색하는 가장 빠른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-175">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output the entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="c2b78-176">엔터티 수정하는 방법</span><span class="sxs-lookup"><span data-stu-id="c2b78-176">How to: Modify an entity</span></span>
<span data-ttu-id="c2b78-177">엔터티를 수정하려면 테이블 서비스에서 엔터티를 검색하고 엔터티 개체를 변경한 후, 바꾸기 또는 병합 작업으로 변경 사항을 테이블 서비스에 다시 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="c2b78-177">To modify an entity, retrieve it from the table service, make changes to the entity object, and save the changes back to the table service with a replace or merge operation.</span></span> <span data-ttu-id="c2b78-178">다음 코드에서는 기존 고객의 전화 번호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-178">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="c2b78-179">삽입하기 위해 사용했던 **TableOperation.insert**를 호출하는 대신, 이 코드는 **TableOperation.replace**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-179">Instead of calling **TableOperation.insert** like we did to insert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="c2b78-180">이 응용 프로그램에서 엔터티를 검색한 이후에 다른 응용 프로그램에서 엔터티를 변경하지 않은 경우 **CloudTable.execute** 메서드가 테이블 서비스를 호출하고 엔터티는 교체됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-180">The **CloudTable.execute** method calls the table service, and the entity is replaced, unless another application changed it in the time since this application retrieved it.</span></span> <span data-ttu-id="c2b78-181">다른 응용 프로그램에서 엔터티를 변경한 경우에는 예외가 발생하고 엔터티를 다시 검색하고 수정한 다음 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-181">When that happens, an exception is thrown, and the entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="c2b78-182">이 낙관적 동시성 다시 시도 패턴은 분산된 저장소 시스템에서 일반적으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation to replace the entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit the operation to the table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="c2b78-183">방법: 엔터티 속성 하위 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="c2b78-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="c2b78-184">테이블 쿼리에서는 엔터티에서 일부 속성만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-184">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="c2b78-185">프로젝션이라고 하는 이 기술은 특히 대역폭을 줄이며 큰 엔터티에 대한 쿼리 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="c2b78-186">다음 코드의 쿼리는 **select** 메서드를 사용하여 테이블에 있는 엔터티의 전자 메일 주소만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-186">The query in the following code uses the **select** method to return only the email addresses of entities in the table.</span></span> <span data-ttu-id="c2b78-187">이 결과는 서버에서 반환된 엔터티에 대해 형식 변환을 수행하는 **EntityResolver**를 통해 **String** 컬렉션에 프로젝트됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-187">The results are projected into a collection of **String** with the help of an **EntityResolver**, which does the type conversion on the entities returned from the server.</span></span> <span data-ttu-id="c2b78-188">[Azure 테이블: Upsert 및 쿼리 프로젝션 소개][Azure Tables: Introducing Upsert and Query Projection]에서 프로젝션에 대한 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2b78-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="c2b78-189">로컬 저장소 에뮬레이터에서는 프로젝션이 지원되지 않으므로 이 코드는 테이블 서비스의 계정을 사용하는 경우에만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-189">Note that projection is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only the Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver to project the entity to the Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through the results, displaying the Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="c2b78-190">엔터티 삽입 또는 바꾸는 방법</span><span class="sxs-lookup"><span data-stu-id="c2b78-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="c2b78-191">엔터티가 테이블에 이미 있는지 모르는 상태에서 테이블에 엔터티를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-191">Often you want to add an entity to a table without knowing if it already exists in the table.</span></span> <span data-ttu-id="c2b78-192">이 경우 삽입 또는 바꾸기 작업을 사용하여 엔터티가 없는 경우 엔터티를 삽입하고 엔터티가 있는 경우 기존 엔터티를 바꾸도록 하는 단일 요청을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-192">An insert-or-replace operation allows you to make a single request which will insert the entity if it does not exist or replace the existing one if it does.</span></span> <span data-ttu-id="c2b78-193">이전의 예를 기반으로 하는 다음 코드에서는 'Walter Harp'에 대한 엔터티를 삽입하거나 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-193">Building on prior examples, the following code inserts or replaces the entity for "Walter Harp".</span></span> <span data-ttu-id="c2b78-194">이 코드에서는 새 엔터티를 만든 후 **TableOperation.insertOrReplace** 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-194">After creating a new entity, this code calls the **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="c2b78-195">그런 다음, 이 코드는 테이블 및 테이블 삽입 또는 바꾸기 작업을 매개 변수로 하여 **CloudTable** 개체에 대해 **execute**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-195">This code then calls **execute** on the **CloudTable** object with the table and the insert or replace table operation as the parameters.</span></span> <span data-ttu-id="c2b78-196">엔터티의 일부만 업데이트하려면 **TableOperation.insertOrMerge** 메서드를 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-196">To update only part of an entity, the **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="c2b78-197">로컬 저장소 에뮬레이터에서는 삽입 또는 바꾸기가 지원되지 않으므로 이 코드는 테이블 서비스의 계정을 사용하는 경우에만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-197">Note that insert-or-replace is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span> <span data-ttu-id="c2b78-198">이 [Azure 테이블: Upsert 및 쿼리 프로젝션 소개][Azure Tables: Introducing Upsert and Query Projection]에서 삽입 또는 바꾸기 및 삽입 또는 병합에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="c2b78-199">방법: 엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="c2b78-199">How to: Delete an entity</span></span>
<span data-ttu-id="c2b78-200">엔터티를 검색한 다음 쉽게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="c2b78-201">엔터티를 검색한 후, 삭제할 엔터티와 함께 **TableOperation.delete** 를 호출하십시오.</span><span class="sxs-lookup"><span data-stu-id="c2b78-201">Once the entity is retrieved, call **TableOperation.delete** with the entity to delete.</span></span> <span data-ttu-id="c2b78-202">그런 다음 **CloudTable** 개체에 대해 **execute**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-202">Then call **execute** on the **CloudTable** object.</span></span> <span data-ttu-id="c2b78-203">다음 코드는 고객 엔터티를 검색하고 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-203">The following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation to delete the entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit the delete operation to the table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="c2b78-204">방법: 테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="c2b78-204">How to: Delete a table</span></span>
<span data-ttu-id="c2b78-205">마지막으로, 다음 코드는 저장소 계정에서 테이블을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-205">Finally, the following code deletes a table from a storage account.</span></span> <span data-ttu-id="c2b78-206">삭제된 테이블은 삭제 후 일정 기간(일반적으로 40초 미만) 동안 다시 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-206">A table which has been deleted will be unavailable to be recreated for a period of time following the deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete the table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="c2b78-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c2b78-207">Next steps</span></span>

* <span data-ttu-id="c2b78-208">[Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)는 Windows, MacOS 및 Linux에서 Azure Storage 데이터로 시각적으로 작업할 수 있도록 해주는 Microsoft의 독립 실행형 무료 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="c2b78-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="c2b78-209">[Java용 Azure Storage SDK][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="c2b78-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="c2b78-210">[CloudStorageAccount][CloudStorageAccount]</span><span class="sxs-lookup"><span data-stu-id="c2b78-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="c2b78-211">[Azure Storage REST API][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="c2b78-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="c2b78-212">[Azure Storage 팀 블로그][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="c2b78-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="c2b78-213">자세한 내용은 [Java 개발자 센터](/develop/java/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2b78-213">For more information, see also the [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="c2b78-214">[CloudStorageAccount]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="c2b78-214">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
