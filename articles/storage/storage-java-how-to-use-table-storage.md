---
title: "Java에서 테이블 저장소 aaaHow toouse | Microsoft Docs"
description: "Azure 테이블 저장소에는 NoSQL 데이터 저장소를 사용 하 여 hello 클라우드에서 구조화 된 데이터를 저장 합니다."
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
ms.openlocfilehash: f72cac3fc10cf0aef74780b84c515d93d715d787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a><span data-ttu-id="e6ed3-103">어떻게 toouse Java에서 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="e6ed3-103">How toouse Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="e6ed3-104">개요</span><span class="sxs-lookup"><span data-stu-id="e6ed3-104">Overview</span></span>
<span data-ttu-id="e6ed3-105">이 가이드 어떻게 tooperform 일반적인 시나리오를 사용 하 여 hello Azure 테이블 저장소 서비스에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-105">This guide will show you how tooperform common scenarios using hello Azure Table storage service.</span></span> <span data-ttu-id="e6ed3-106">hello 샘플 Java 작성 되 고 hello를 사용 하 여 [Java 용 Azure 저장소 SDK][Azure Storage SDK for Java]합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-106">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="e6ed3-107">hello 가이드에서 다루는 시나리오 포함 **만드는**, **나열**, 및 **삭제** 테이블으로 **삽입**,  **쿼리**, **수정**, 및 **삭제** 테이블의에서 엔터티.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-107">hello scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="e6ed3-108">테이블에 대 한 자세한 내용은 참조 hello [다음 단계](#Next-Steps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-108">For more information on tables, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="e6ed3-109">SDK는 Android 장치에서 Azure 저장소를 사용하는 개발자에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="e6ed3-110">자세한 내용은 참조 hello [Android 용 Azure 저장소 SDK][Azure Storage SDK for Android]합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-110">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="e6ed3-111">Java 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e6ed3-111">Create a Java application</span></span>
<span data-ttu-id="e6ed3-112">이 가이드에서는 Java 응용 프로그램 내에서 로컬로 실행할 수 있거나 Azure의 웹 역할 또는 작업자 역할 내에서 실행되는 코드에서 실행할 수 있는 저장소 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="e6ed3-113">toodo tooinstall, 나오는 Java Development Kit (JDK) hello 및 Azure 구독에 Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-113">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="e6ed3-114">그렇게 않은 후에 hello 최소 요구 사항 및 종속성 hello에 나열 되어 있는 개발 시스템 맞는 tooverify 해야 합니다 [Java 용 Azure 저장소 SDK] [ Azure Storage SDK for Java] GitHub의 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-114">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="e6ed3-115">시스템에 이러한 요구 사항을 충족 하는 경우 다운로드 하 고 해당 리포지토리 로부터 시스템에 hello Java 용 Azure 저장소 라이브러리를 설치 하기 위한 hello 지침을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-115">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="e6ed3-116">이러한 작업을 완료 되 면이 문서의 hello 예제를 사용 하는 Java 응용 프로그램 수 toocreate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-116">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="e6ed3-117">응용 프로그램 tooaccess 테이블 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="e6ed3-117">Configure your application tooaccess table storage</span></span>
<span data-ttu-id="e6ed3-118">Hello toouse Microsoft Azure 저장소 Api tooaccess 테이블 저장할 hello Java 파일 맨 문을 toohello 가져오기 뒤에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-118">Add hello following import statements toohello top of hello Java file where you want toouse Microsoft Azure storage APIs tooaccess tables:</span></span>

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="e6ed3-119">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="e6ed3-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="e6ed3-120">Azure 저장소 클라이언트는 저장소 연결 문자열 toostore 끝점을 사용 하 여 및 데이터 관리 서비스에 액세스 하기 위한 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-120">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="e6ed3-121">형식에 따라, 사용자의 저장소 계정 hello 이름을 사용 하 여 hello hello 저장소 연결 문자열을 입력 하 고 hello에 나열 된 hello 저장소 계정의 기본 액세스 키를 hello 해야, 클라이언트 응용 프로그램에서 실행할 때는 [Azure 포털](https://portal.azure.com)hello에 대 한 *AccountName* 및 *AccountKey* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-121">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="e6ed3-122">이 예에서는 정적 필드 toohold hello 연결 문자열을 선언할 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-122">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="e6ed3-123">Microsoft Azure에서 역할 내에서 실행 하는 응용 프로그램을이 문자열 hello 서비스 구성 파일에 저장 될 수 *ServiceConfiguration.cscfg*, 호출 toohello로 액세스할 수 있습니다 및  **RoleEnvironment.getConfigurationSettings** 메서드.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-123">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="e6ed3-124">Hello 연결 문자열에서 가져오는의 예로 **설정** 라는 요소 *StorageConnectionString* hello 서비스 구성 파일에:</span><span class="sxs-lookup"><span data-stu-id="e6ed3-124">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="e6ed3-125">hello 다음과 같은 샘플 가정 이러한 두 가지 방법 tooget hello 저장소 연결 문자열 중 하나 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-125">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="e6ed3-126">방법: 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="e6ed3-126">How to: Create a table</span></span>
<span data-ttu-id="e6ed3-127">**CloudTableClient** 개체를 사용하면 테이블 및 엔터티에 대한 참조 개체를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="e6ed3-128">hello 다음 코드에서는 **CloudTableClient** 새 toocreate 사용 하 여 개체 **CloudTable** 테이블을 나타내는 개체 "사용자" 라는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-128">hello following code creates a **CloudTableClient** object and uses it toocreate a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="e6ed3-129">(참고: 추가 방법을 알아볼 toocreate는 **CloudStorageAccount** 개체, 자세한 내용은 참조 **CloudStorageAccount** hello에 [Azure 저장소 클라이언트 SDK 참조].)</span><span class="sxs-lookup"><span data-stu-id="e6ed3-129">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a><span data-ttu-id="e6ed3-130">방법: hello 테이블을 나열</span><span class="sxs-lookup"><span data-stu-id="e6ed3-130">How to: List hello tables</span></span>
<span data-ttu-id="e6ed3-131">호출 hello 테이블 목록이 tooget **CloudTableClient.listTables()** 메서드 tooretrieve는 반복 가능한 테이블 이름 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-131">tooget a list of tables, call hello **CloudTableClient.listTables()** method tooretrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a><span data-ttu-id="e6ed3-132">방법: 엔터티 tooa 테이블 추가</span><span class="sxs-lookup"><span data-stu-id="e6ed3-132">How to: Add an entity tooa table</span></span>
<span data-ttu-id="e6ed3-133">엔터티 tooJava 개체를 구현 하는 사용자 지정 클래스를 사용 하 여 매핑할 **TableEntity**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-133">Entities map tooJava objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="e6ed3-134">편의 위해 hello **TableServiceEntity** 클래스 구현 **TableEntity** 명명 된 toogetter 및 setter 메서드를 사용 하 여 리플렉션 toomap 속성 hello 속성 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-134">For convenience, hello **TableServiceEntity** class implements **TableEntity** and uses reflection toomap properties toogetter and setter methods named for hello properties.</span></span> <span data-ttu-id="e6ed3-135">먼저 tooadd은 엔터티 tooa 테이블 엔터티 hello 속성을 정의 하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-135">tooadd an entity tooa table, first create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="e6ed3-136">hello 다음 코드에서는 정의 hello 파티션 키로 hello 고객의 이름 hello 행 키를 하 고 마지막 이름을 사용 하 여 엔터티 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-136">hello following code defines an entity class which uses hello customer's first name as hello row key, and last name as hello partition key.</span></span> <span data-ttu-id="e6ed3-137">함께 엔터티의 파티션과 행 키는 hello 엔터티 hello 테이블에 고유 하 게 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-137">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="e6ed3-138">Hello 동일한 파티션 키를 다른 파티션 키를 사용 하는 것 보다 더 빠르게 쿼리할 수 있는 엔터티.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-138">Entities with hello same partition key can be queried faster than those with different partition keys.</span></span>

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

<span data-ttu-id="e6ed3-139">엔터티를 포함하는 테이블 작업에는 **TableOperation** 개체가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="e6ed3-140">이 개체와 실행 될 수 있는 엔터티에 대해 수행 하는 hello 작업 toobe 정의 **CloudTable** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-140">This object defines hello operation toobe performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="e6ed3-141">hello 다음 코드에서는 hello의 새 인스턴스 **CustomerEntity** 저장 된 일부 고객 데이터 toobe 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-141">hello following code creates a new instance of hello **CustomerEntity** class with some customer data toobe stored.</span></span> <span data-ttu-id="e6ed3-142">코드의 다음 호출 hello **TableOperation.insertOrReplace** toocreate는 **TableOperation** tooinsert 엔터티를 테이블에 개체 및 associates 새로운 hello **CustomerEntity**함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-142">hello code next calls **TableOperation.insertOrReplace** toocreate a **TableOperation** object tooinsert an entity into a table, and associates hello new **CustomerEntity** with it.</span></span> <span data-ttu-id="e6ed3-143">Hello 코드 hello를 호출 하는 마지막으로, **실행** 메서드 hello **CloudTable** hello "people" 테이블 및 새 hello를 지정 하는 개체, **TableOperation**, 어느 한 다음 보냅니다는 hello "people" 테이블로 toohello 저장소 서비스 tooinsert hello 새 customer 엔터티를 요청 하거나 이미 있는 경우 hello 엔터티를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-143">Finally, hello code calls hello **execute** method on hello **CloudTable** object, specifying hello "people" table and hello new **TableOperation**, which then sends a request toohello storage service tooinsert hello new customer entity into hello "people" table, or replace hello entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="e6ed3-144">방법: 엔터티 일괄 삽입</span><span class="sxs-lookup"><span data-stu-id="e6ed3-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="e6ed3-145">한 번의 쓰기 작업에서 엔터티 toohello 테이블 서비스의 일괄 처리를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-145">You can insert a batch of entities toohello table service in one write operation.</span></span> <span data-ttu-id="e6ed3-146">hello 다음 코드에서는 **에서는 TableBatchOperation** 개체를 다음 세 개의 삽입 작업 tooit 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-146">hello following code creates a **TableBatchOperation** object, then adds three insert operations tooit.</span></span> <span data-ttu-id="e6ed3-147">각 삽입 작업은 새 엔터티 개체를 만들고 해당 값을 설정 다음 hello를 호출 하 여 추가 **삽입** 메서드 hello **에서는 TableBatchOperation** tooassociate hello 엔터티를 새 개체 작업을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-147">Each insert operation is added by creating a new entity object, setting its values, and then calling hello **insert** method on hello **TableBatchOperation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="e6ed3-148">다음 코드 호출을 hello **실행** hello에 **CloudTable** hello "people" 테이블과 hello를 지정 하는 개체, **에서는 TableBatchOperation** 테이블의 hello 일괄 처리를 전송 하는 개체 단일 요청에서 toohello 저장소 서비스 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-148">Then hello code calls **execute** on hello **CloudTable** object, specifying hello "people" table and hello **TableBatchOperation** object, which sends hello batch of table operations toohello storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="e6ed3-149">일괄 처리 작업에 일부의 toonote:</span><span class="sxs-lookup"><span data-stu-id="e6ed3-149">Some things toonote on batch operations:</span></span>

* <span data-ttu-id="e6ed3-150">Too100 insert, delete, merge, replace, insert 또는 merge를 수행 하 고 삽입 하거나 바꾸기 작업을 단일 일괄 처리의 조합 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-150">You can perform up too100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="e6ed3-151">일괄 처리 작업이 hello hello 일괄 처리에서 유일한 작업 하는 경우 검색 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-151">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>
* <span data-ttu-id="e6ed3-152">단일 일괄 처리 작업의 모든 엔터티가 hello 있어야 합니다. 동일한 파티션 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-152">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="e6ed3-153">일괄 처리 작업은 제한 된 tooa 4MB 데이터 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-153">A batch operation is limited tooa 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="e6ed3-154">방법: 파티션의 모든 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="e6ed3-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="e6ed3-155">사용할 수 있습니다 파티션의 엔터티에 대 한 테이블 tooquery는 **TableQuery**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-155">tooquery a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="e6ed3-156">호출 **TableQuery.from** toocreate 지정 된 결과 형식을 반환 하는 특정 테이블에 대 한 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-156">Call **TableQuery.from** toocreate a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="e6ed3-157">hello 다음 코드 지정 엔터티 'Smith'는 hello 파티션 키에 대 한 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-157">hello following code specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="e6ed3-158">**TableQuery.generateFilterCondition** 쿼리에 대 한 toocreate 필터는 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-158">**TableQuery.generateFilterCondition** is a helper method toocreate filters for queries.</span></span> <span data-ttu-id="e6ed3-159">호출 **여기서** hello에서 반환 된 hello 참조에 대해 **TableQuery.from** 메서드 tooapply hello 필터 toohello 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-159">Call **where** on hello reference returned by hello **TableQuery.from** method tooapply hello filter toohello query.</span></span> <span data-ttu-id="e6ed3-160">Hello 쿼리가 실행 될 때 호출 하 여 너무**실행** hello에 **CloudTable** 반환는 **반복기** hello로 **CustomerEntity**지정 된 형식 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-160">When hello query is executed with a call too**execute** on hello **CloudTable** object, it returns an **Iterator** with hello **CustomerEntity** result type specified.</span></span> <span data-ttu-id="e6ed3-161">Hello를 사용 하 여 있습니다 **반복기** 에서 반환 되는 각 루프 tooconsume hello 결과 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-161">You can then use hello **Iterator** returned in a for each loop tooconsume hello results.</span></span> <span data-ttu-id="e6ed3-162">이 코드는 hello 쿼리 결과 toohello 콘솔의 각 엔터티에의 hello 필드를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-162">This code prints hello fields of each entity in hello query results toohello console.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="e6ed3-163">방법: 파티션의 엔터티 범위 검색</span><span class="sxs-lookup"><span data-stu-id="e6ed3-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="e6ed3-164">않으려면 tooquery 파티션에서 모든 hello 엔터티를 필터의 비교 연산자를 사용 하 여 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-164">If you don't want tooquery all hello entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="e6ed3-165">다음 두 개의 필터 tooget 파티션 "Smith"의 모든 엔터티가 hello 행 키 (이름) 위로 too'E 문자로 시작 하는 위치 코드 결합 hello' hello 알파벳에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-165">hello following code combines two filters tooget all entities in partition "Smith" where hello row key (first name) starts with a letter up too'E' in hello alphabet.</span></span> <span data-ttu-id="e6ed3-166">그러면 hello 쿼리 결과 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-166">Then it prints hello query results.</span></span> <span data-ttu-id="e6ed3-167">이 가이드의 섹션을 삽입 하는 hello 엔터티 추가 toohello hello 일괄 처리 테이블에에서 사용 하는 경우, 두 개의 엔터티가 (Ben 및 Denise Smith;)이이 시간에 반환 됩니다. 홍길동 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-167">If you use hello entities added toohello table in hello batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="e6ed3-168">방법: 단일 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="e6ed3-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="e6ed3-169">단일, 특정 엔터티 쿼리 tooretrieve를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-169">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="e6ed3-170">hello 다음 호출 코드 **TableOperation.retrieve** 고객과 파티션 키와 행 키 매개 변수 toospecify hello "홍길동"를 만드는 대신 한 **TableQuery** 필터 toodo hello를 사용 하 고 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-170">hello following code calls **TableOperation.retrieve** with partition key and row key parameters toospecify hello customer "Jeff Smith", instead of creating a **TableQuery** and using filters toodo hello same thing.</span></span> <span data-ttu-id="e6ed3-171">를 실행 하면 hello 컬렉션이 아닌 작업 반환 하나의 엔터티를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-171">When executed, hello retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="e6ed3-172">hello **getResultAsType** 메서드 캐스팅 hello 할당 대상 유형의 결과 toohello hello는 **CustomerEntity** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-172">hello **getResultAsType** method casts hello result toohello type of hello assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="e6ed3-173">이 형식은 hello 쿼리에 대해 지정 된 hello 형식과 호환 되지 않으면 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-173">If this type is not compatible with hello type specified for hello query, an exception will be thrown.</span></span> <span data-ttu-id="e6ed3-174">파티션과 행 키가 정확하게 일치하는 엔터티가 없는 경우 null 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="e6ed3-175">쿼리에서 모두 파티션 및 행 키를 지정 하는 hello 가장 빠른 방법은 tooretrieve hello 테이블 서비스에서 단일 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-175">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
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
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="e6ed3-176">엔터티 수정하는 방법</span><span class="sxs-lookup"><span data-stu-id="e6ed3-176">How to: Modify an entity</span></span>
<span data-ttu-id="e6ed3-177">toomodify 엔터티, hello 테이블 서비스에서 검색 변경 toohello 엔터티 개체를 만들고 ब ा ळ hello 백 toohello 테이블 서비스 바꾸기 또는 병합 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-177">toomodify an entity, retrieve it from hello table service, make changes toohello entity object, and save hello changes back toohello table service with a replace or merge operation.</span></span> <span data-ttu-id="e6ed3-178">hello 다음 코드 기존 고객의 전화 번호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-178">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="e6ed3-179">호출 하는 대신 **TableOperation.insert** 이 코드는 호출 tooinsert 수행한 것 처럼 **TableOperation.replace**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-179">Instead of calling **TableOperation.insert** like we did tooinsert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="e6ed3-180">hello **CloudTable.execute** 메서드 hello 테이블 서비스를 호출 하 고 변경 하지 않으면 다른 응용 프로그램 것 hello 시간에이 응용 프로그램 것으로 검색 한 이후 hello 엔터티 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-180">hello **CloudTable.execute** method calls hello table service, and hello entity is replaced, unless another application changed it in hello time since this application retrieved it.</span></span> <span data-ttu-id="e6ed3-181">에 도달 하면 예외가 throw 되 고 hello 엔터티 검색, 수정 및 해야 다시 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-181">When that happens, an exception is thrown, and hello entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="e6ed3-182">이 낙관적 동시성 다시 시도 패턴은 분산된 저장소 시스템에서 일반적으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="e6ed3-183">방법: 엔터티 속성 하위 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="e6ed3-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="e6ed3-184">쿼리 tooa 테이블 엔터티의 몇 개의 속성을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-184">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="e6ed3-185">프로젝션이라고 하는 이 기술은 특히 대역폭을 줄이며 큰 엔터티에 대한 쿼리 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="e6ed3-186">hello 쿼리에서 hello 코드 다음에 사용 하 여 hello **선택** 메서드 tooreturn hello 전자 메일 주소만 hello 테이블에 있는 엔터티.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-186">hello query in hello following code uses hello **select** method tooreturn only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="e6ed3-187">hello 결과에 대 한 예측의 컬렉션인 **문자열** 사용 하 여 hello는 **EntityResolver**, hello 서버에서 반환 된 hello 엔터티에 대 한 형식 변환 hello지 않습니다입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-187">hello results are projected into a collection of **String** with hello help of an **EntityResolver**, which does hello type conversion on hello entities returned from hello server.</span></span> <span data-ttu-id="e6ed3-188">[Azure 테이블: Upsert 및 쿼리 프로젝션 소개][Azure Tables: Introducing Upsert and Query Projection]에서 프로젝션에 대한 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="e6ed3-189">Note hello 테이블 서비스에 인 계정을 사용 하는 경우에이 코드를 실행 하므로 프로젝션 hello 로컬 저장소 에뮬레이터에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-189">Note that projection is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="e6ed3-190">엔터티 삽입 또는 바꾸는 방법</span><span class="sxs-lookup"><span data-stu-id="e6ed3-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="e6ed3-191">Hello 테이블에 이미 있는 경우를 몰라도 tooadd 엔터티 tooa 테이블 할 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-191">Often you want tooadd an entity tooa table without knowing if it already exists in hello table.</span></span> <span data-ttu-id="e6ed3-192">삽입 또는 바꾸기 작업 toomake를 존재 하거나 그렇지 않으면 기존 자동 압축 hello를 대체 하지 않는 경우 hello 엔터티를 삽입 하는 단일 요청 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-192">An insert-or-replace operation allows you toomake a single request which will insert hello entity if it does not exist or replace hello existing one if it does.</span></span> <span data-ttu-id="e6ed3-193">이전 예제를 빌드한 hello 다음 코드를 삽입 하거나 교체 hello 엔터티 "Walter 하프"에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-193">Building on prior examples, hello following code inserts or replaces hello entity for "Walter Harp".</span></span> <span data-ttu-id="e6ed3-194">이 코드는 새 엔터티를 만든 후 hello 호출 **TableOperation.insertOrReplace** 메서드.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-194">After creating a new entity, this code calls hello **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="e6ed3-195">이 코드는 다음 호출 **실행** hello에 **CloudTable** hello 테이블과 hello 삽입 된 개체 또는 테이블 작업 hello 매개 변수로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-195">This code then calls **execute** on hello **CloudTable** object with hello table and hello insert or replace table operation as hello parameters.</span></span> <span data-ttu-id="e6ed3-196">엔터티를 부분 tooupdate hello **TableOperation.insertOrMerge** 메서드를 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-196">tooupdate only part of an entity, hello **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="e6ed3-197">Note hello 테이블 서비스에 인 계정을 사용 하는 경우에이 코드를 실행 하므로 해당 insert 또는-바꾸기 hello 로컬 저장소 에뮬레이터에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-197">Note that insert-or-replace is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span> <span data-ttu-id="e6ed3-198">이 [Azure 테이블: Upsert 및 쿼리 프로젝션 소개][Azure Tables: Introducing Upsert and Query Projection]에서 삽입 또는 바꾸기 및 삽입 또는 병합에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="e6ed3-199">방법: 엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="e6ed3-199">How to: Delete an entity</span></span>
<span data-ttu-id="e6ed3-200">엔터티를 검색한 다음 쉽게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="e6ed3-201">Hello 엔터티 검색 되 면 호출 **TableOperation.delete** hello 엔터티 toodelete 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-201">Once hello entity is retrieved, call **TableOperation.delete** with hello entity toodelete.</span></span> <span data-ttu-id="e6ed3-202">그런 다음 호출 **실행** hello에 **CloudTable** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-202">Then call **execute** on hello **CloudTable** object.</span></span> <span data-ttu-id="e6ed3-203">hello 코드 다음 검색 하 고 고객 엔터티를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-203">hello following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="e6ed3-204">방법: 테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="e6ed3-204">How to: Delete a table</span></span>
<span data-ttu-id="e6ed3-205">마지막으로, hello 다음 코드는 테이블은 저장소 계정에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-205">Finally, hello following code deletes a table from a storage account.</span></span> <span data-ttu-id="e6ed3-206">삭제 된 테이블을 사용할 수 없는 toobe hello 삭제, 일반적으로 미만 40 초 시간 기간에 대 한 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-206">A table which has been deleted will be unavailable toobe recreated for a period of time following hello deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="e6ed3-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6ed3-207">Next steps</span></span>

* <span data-ttu-id="e6ed3-208">[Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="e6ed3-209">[Java용 Azure Storage SDK][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="e6ed3-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="e6ed3-210">[Azure 저장소 클라이언트 SDK 참조][Azure 저장소 클라이언트 SDK 참조]</span><span class="sxs-lookup"><span data-stu-id="e6ed3-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="e6ed3-211">[Azure Storage REST API][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="e6ed3-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="e6ed3-212">[Azure Storage 팀 블로그][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="e6ed3-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="e6ed3-213">자세한 내용은 참고 항목 hello [Java 개발자 센터](/develop/java/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ed3-213">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 저장소 클라이언트 SDK 참조]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
