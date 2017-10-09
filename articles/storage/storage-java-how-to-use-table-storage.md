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
# <a name="how-toouse-table-storage-from-java"></a>어떻게 toouse Java에서 테이블 저장소
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>개요
이 가이드 어떻게 tooperform 일반적인 시나리오를 사용 하 여 hello Azure 테이블 저장소 서비스에 표시 됩니다. hello 샘플 Java 작성 되 고 hello를 사용 하 여 [Java 용 Azure 저장소 SDK][Azure Storage SDK for Java]합니다. hello 가이드에서 다루는 시나리오 포함 **만드는**, **나열**, 및 **삭제** 테이블으로 **삽입**,  **쿼리**, **수정**, 및 **삭제** 테이블의에서 엔터티. 테이블에 대 한 자세한 내용은 참조 hello [다음 단계](#Next-Steps) 섹션.

SDK는 Android 장치에서 Azure 저장소를 사용하는 개발자에게 제공됩니다. 자세한 내용은 참조 hello [Android 용 Azure 저장소 SDK][Azure Storage SDK for Android]합니다.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Java 응용 프로그램 만들기
이 가이드에서는 Java 응용 프로그램 내에서 로컬로 실행할 수 있거나 Azure의 웹 역할 또는 작업자 역할 내에서 실행되는 코드에서 실행할 수 있는 저장소 기능을 사용합니다.

toodo tooinstall, 나오는 Java Development Kit (JDK) hello 및 Azure 구독에 Azure 저장소 계정을 만듭니다. 그렇게 않은 후에 hello 최소 요구 사항 및 종속성 hello에 나열 되어 있는 개발 시스템 맞는 tooverify 해야 합니다 [Java 용 Azure 저장소 SDK] [ Azure Storage SDK for Java] GitHub의 리포지토리 합니다. 시스템에 이러한 요구 사항을 충족 하는 경우 다운로드 하 고 해당 리포지토리 로부터 시스템에 hello Java 용 Azure 저장소 라이브러리를 설치 하기 위한 hello 지침을 따를 수 있습니다. 이러한 작업을 완료 되 면이 문서의 hello 예제를 사용 하는 Java 응용 프로그램 수 toocreate 됩니다.

## <a name="configure-your-application-tooaccess-table-storage"></a>응용 프로그램 tooaccess 테이블 저장소 구성
Hello toouse Microsoft Azure 저장소 Api tooaccess 테이블 저장할 hello Java 파일 맨 문을 toohello 가져오기 뒤에 추가 합니다.

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Azure 저장소 연결 문자열 설정
Azure 저장소 클라이언트는 저장소 연결 문자열 toostore 끝점을 사용 하 여 및 데이터 관리 서비스에 액세스 하기 위한 자격 증명입니다. 형식에 따라, 사용자의 저장소 계정 hello 이름을 사용 하 여 hello hello 저장소 연결 문자열을 입력 하 고 hello에 나열 된 hello 저장소 계정의 기본 액세스 키를 hello 해야, 클라이언트 응용 프로그램에서 실행할 때는 [Azure 포털](https://portal.azure.com)hello에 대 한 *AccountName* 및 *AccountKey* 값입니다. 이 예에서는 정적 필드 toohold hello 연결 문자열을 선언할 수는 방법을 보여 줍니다.

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Microsoft Azure에서 역할 내에서 실행 하는 응용 프로그램을이 문자열 hello 서비스 구성 파일에 저장 될 수 *ServiceConfiguration.cscfg*, 호출 toohello로 액세스할 수 있습니다 및  **RoleEnvironment.getConfigurationSettings** 메서드. Hello 연결 문자열에서 가져오는의 예로 **설정** 라는 요소 *StorageConnectionString* hello 서비스 구성 파일에:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

hello 다음과 같은 샘플 가정 이러한 두 가지 방법 tooget hello 저장소 연결 문자열 중 하나 사용 하 합니다.

## <a name="how-to-create-a-table"></a>방법: 테이블 만들기
**CloudTableClient** 개체를 사용하면 테이블 및 엔터티에 대한 참조 개체를 가져올 수 있습니다. hello 다음 코드에서는 **CloudTableClient** 새 toocreate 사용 하 여 개체 **CloudTable** 테이블을 나타내는 개체 "사용자" 라는 합니다. (참고: 추가 방법을 알아볼 toocreate는 **CloudStorageAccount** 개체, 자세한 내용은 참조 **CloudStorageAccount** hello에 [Azure 저장소 클라이언트 SDK 참조].)

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

## <a name="how-to-list-hello-tables"></a>방법: hello 테이블을 나열
호출 hello 테이블 목록이 tooget **CloudTableClient.listTables()** 메서드 tooretrieve는 반복 가능한 테이블 이름 목록입니다.

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

## <a name="how-to-add-an-entity-tooa-table"></a>방법: 엔터티 tooa 테이블 추가
엔터티 tooJava 개체를 구현 하는 사용자 지정 클래스를 사용 하 여 매핑할 **TableEntity**합니다. 편의 위해 hello **TableServiceEntity** 클래스 구현 **TableEntity** 명명 된 toogetter 및 setter 메서드를 사용 하 여 리플렉션 toomap 속성 hello 속성 및 합니다. 먼저 tooadd은 엔터티 tooa 테이블 엔터티 hello 속성을 정의 하는 클래스를 만듭니다. hello 다음 코드에서는 정의 hello 파티션 키로 hello 고객의 이름 hello 행 키를 하 고 마지막 이름을 사용 하 여 엔터티 클래스입니다. 함께 엔터티의 파티션과 행 키는 hello 엔터티 hello 테이블에 고유 하 게 식별 합니다. Hello 동일한 파티션 키를 다른 파티션 키를 사용 하는 것 보다 더 빠르게 쿼리할 수 있는 엔터티.

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

엔터티를 포함하는 테이블 작업에는 **TableOperation** 개체가 필요합니다. 이 개체와 실행 될 수 있는 엔터티에 대해 수행 하는 hello 작업 toobe 정의 **CloudTable** 개체입니다. hello 다음 코드에서는 hello의 새 인스턴스 **CustomerEntity** 저장 된 일부 고객 데이터 toobe 클래스입니다. 코드의 다음 호출 hello **TableOperation.insertOrReplace** toocreate는 **TableOperation** tooinsert 엔터티를 테이블에 개체 및 associates 새로운 hello **CustomerEntity**함께 합니다. Hello 코드 hello를 호출 하는 마지막으로, **실행** 메서드 hello **CloudTable** hello "people" 테이블 및 새 hello를 지정 하는 개체, **TableOperation**, 어느 한 다음 보냅니다는 hello "people" 테이블로 toohello 저장소 서비스 tooinsert hello 새 customer 엔터티를 요청 하거나 이미 있는 경우 hello 엔터티를 바꿉니다.

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

## <a name="how-to-insert-a-batch-of-entities"></a>방법: 엔터티 일괄 삽입
한 번의 쓰기 작업에서 엔터티 toohello 테이블 서비스의 일괄 처리를 삽입할 수 있습니다. hello 다음 코드에서는 **에서는 TableBatchOperation** 개체를 다음 세 개의 삽입 작업 tooit 추가 합니다. 각 삽입 작업은 새 엔터티 개체를 만들고 해당 값을 설정 다음 hello를 호출 하 여 추가 **삽입** 메서드 hello **에서는 TableBatchOperation** tooassociate hello 엔터티를 새 개체 작업을 삽입 합니다. 다음 코드 호출을 hello **실행** hello에 **CloudTable** hello "people" 테이블과 hello를 지정 하는 개체, **에서는 TableBatchOperation** 테이블의 hello 일괄 처리를 전송 하는 개체 단일 요청에서 toohello 저장소 서비스 작업입니다.

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

일괄 처리 작업에 일부의 toonote:

* Too100 insert, delete, merge, replace, insert 또는 merge를 수행 하 고 삽입 하거나 바꾸기 작업을 단일 일괄 처리의 조합 수 있습니다.
* 일괄 처리 작업이 hello hello 일괄 처리에서 유일한 작업 하는 경우 검색 작업이 있을 수 있습니다.
* 단일 일괄 처리 작업의 모든 엔터티가 hello 있어야 합니다. 동일한 파티션 키입니다.
* 일괄 처리 작업은 제한 된 tooa 4MB 데이터 페이로드입니다.

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>방법: 파티션의 모든 엔터티 검색
사용할 수 있습니다 파티션의 엔터티에 대 한 테이블 tooquery는 **TableQuery**합니다. 호출 **TableQuery.from** toocreate 지정 된 결과 형식을 반환 하는 특정 테이블에 대 한 쿼리 합니다. hello 다음 코드 지정 엔터티 'Smith'는 hello 파티션 키에 대 한 필터입니다. **TableQuery.generateFilterCondition** 쿼리에 대 한 toocreate 필터는 도우미 메서드입니다. 호출 **여기서** hello에서 반환 된 hello 참조에 대해 **TableQuery.from** 메서드 tooapply hello 필터 toohello 쿼리 합니다. Hello 쿼리가 실행 될 때 호출 하 여 너무**실행** hello에 **CloudTable** 반환는 **반복기** hello로 **CustomerEntity**지정 된 형식 발생 합니다. Hello를 사용 하 여 있습니다 **반복기** 에서 반환 되는 각 루프 tooconsume hello 결과 대 한 합니다. 이 코드는 hello 쿼리 결과 toohello 콘솔의 각 엔터티에의 hello 필드를 인쇄합니다.

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

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>방법: 파티션의 엔터티 범위 검색
않으려면 tooquery 파티션에서 모든 hello 엔터티를 필터의 비교 연산자를 사용 하 여 범위를 지정할 수 있습니다. 다음 두 개의 필터 tooget 파티션 "Smith"의 모든 엔터티가 hello 행 키 (이름) 위로 too'E 문자로 시작 하는 위치 코드 결합 hello' hello 알파벳에서 합니다. 그러면 hello 쿼리 결과 표시 됩니다. 이 가이드의 섹션을 삽입 하는 hello 엔터티 추가 toohello hello 일괄 처리 테이블에에서 사용 하는 경우, 두 개의 엔터티가 (Ben 및 Denise Smith;)이이 시간에 반환 됩니다. 홍길동 포함 되지 않습니다.

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

## <a name="how-to-retrieve-a-single-entity"></a>방법: 단일 엔터티 검색
단일, 특정 엔터티 쿼리 tooretrieve를 작성할 수 있습니다. hello 다음 호출 코드 **TableOperation.retrieve** 고객과 파티션 키와 행 키 매개 변수 toospecify hello "홍길동"를 만드는 대신 한 **TableQuery** 필터 toodo hello를 사용 하 고 다릅니다. 를 실행 하면 hello 컬렉션이 아닌 작업 반환 하나의 엔터티를 검색 합니다. hello **getResultAsType** 메서드 캐스팅 hello 할당 대상 유형의 결과 toohello hello는 **CustomerEntity** 개체입니다. 이 형식은 hello 쿼리에 대해 지정 된 hello 형식과 호환 되지 않으면 예외가 throw 됩니다. 파티션과 행 키가 정확하게 일치하는 엔터티가 없는 경우 null 값이 반환됩니다. 쿼리에서 모두 파티션 및 행 키를 지정 하는 hello 가장 빠른 방법은 tooretrieve hello 테이블 서비스에서 단일 엔터티입니다.

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

## <a name="how-to-modify-an-entity"></a>엔터티 수정하는 방법
toomodify 엔터티, hello 테이블 서비스에서 검색 변경 toohello 엔터티 개체를 만들고 ब ा ळ hello 백 toohello 테이블 서비스 바꾸기 또는 병합 작업을 합니다. hello 다음 코드 기존 고객의 전화 번호를 변경합니다. 호출 하는 대신 **TableOperation.insert** 이 코드는 호출 tooinsert 수행한 것 처럼 **TableOperation.replace**합니다. hello **CloudTable.execute** 메서드 hello 테이블 서비스를 호출 하 고 변경 하지 않으면 다른 응용 프로그램 것 hello 시간에이 응용 프로그램 것으로 검색 한 이후 hello 엔터티 대체 됩니다. 에 도달 하면 예외가 throw 되 고 hello 엔터티 검색, 수정 및 해야 다시 저장 합니다. 이 낙관적 동시성 다시 시도 패턴은 분산된 저장소 시스템에서 일반적으로 발생합니다.

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

## <a name="how-to-query-a-subset-of-entity-properties"></a>방법: 엔터티 속성 하위 집합 쿼리
쿼리 tooa 테이블 엔터티의 몇 개의 속성을 검색할 수 있습니다. 프로젝션이라고 하는 이 기술은 특히 대역폭을 줄이며 큰 엔터티에 대한 쿼리 성능을 향상시킬 수 있습니다. hello 쿼리에서 hello 코드 다음에 사용 하 여 hello **선택** 메서드 tooreturn hello 전자 메일 주소만 hello 테이블에 있는 엔터티. hello 결과에 대 한 예측의 컬렉션인 **문자열** 사용 하 여 hello는 **EntityResolver**, hello 서버에서 반환 된 hello 엔터티에 대 한 형식 변환 hello지 않습니다입니다. [Azure 테이블: Upsert 및 쿼리 프로젝션 소개][Azure Tables: Introducing Upsert and Query Projection]에서 프로젝션에 대한 자세한 내용을 참조하세요. Note hello 테이블 서비스에 인 계정을 사용 하는 경우에이 코드를 실행 하므로 프로젝션 hello 로컬 저장소 에뮬레이터에서 지원 되지 않습니다.

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

## <a name="how-to-insert-or-replace-an-entity"></a>엔터티 삽입 또는 바꾸는 방법
Hello 테이블에 이미 있는 경우를 몰라도 tooadd 엔터티 tooa 테이블 할 경우가 있습니다. 삽입 또는 바꾸기 작업 toomake를 존재 하거나 그렇지 않으면 기존 자동 압축 hello를 대체 하지 않는 경우 hello 엔터티를 삽입 하는 단일 요청 수 있습니다. 이전 예제를 빌드한 hello 다음 코드를 삽입 하거나 교체 hello 엔터티 "Walter 하프"에 대 한 합니다. 이 코드는 새 엔터티를 만든 후 hello 호출 **TableOperation.insertOrReplace** 메서드. 이 코드는 다음 호출 **실행** hello에 **CloudTable** hello 테이블과 hello 삽입 된 개체 또는 테이블 작업 hello 매개 변수로 대체 합니다. 엔터티를 부분 tooupdate hello **TableOperation.insertOrMerge** 메서드를 대신 사용할 수 있습니다. Note hello 테이블 서비스에 인 계정을 사용 하는 경우에이 코드를 실행 하므로 해당 insert 또는-바꾸기 hello 로컬 저장소 에뮬레이터에서 지원 되지 않습니다. 이 [Azure 테이블: Upsert 및 쿼리 프로젝션 소개][Azure Tables: Introducing Upsert and Query Projection]에서 삽입 또는 바꾸기 및 삽입 또는 병합에 대해 자세히 알아볼 수 있습니다.

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

## <a name="how-to-delete-an-entity"></a>방법: 엔터티 삭제
엔터티를 검색한 다음 쉽게 삭제할 수 있습니다. Hello 엔터티 검색 되 면 호출 **TableOperation.delete** hello 엔터티 toodelete 사용 합니다. 그런 다음 호출 **실행** hello에 **CloudTable** 개체입니다. hello 코드 다음 검색 하 고 고객 엔터티를 삭제 합니다.

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

## <a name="how-to-delete-a-table"></a>방법: 테이블 삭제
마지막으로, hello 다음 코드는 테이블은 저장소 계정에서 삭제 합니다. 삭제 된 테이블을 사용할 수 없는 toobe hello 삭제, 일반적으로 미만 40 초 시간 기간에 대 한 다시 생성 됩니다.

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

## <a name="next-steps"></a>다음 단계

* [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.
* [Java용 Azure Storage SDK][Azure Storage SDK for Java]
* [Azure 저장소 클라이언트 SDK 참조][Azure 저장소 클라이언트 SDK 참조]
* [Azure Storage REST API][Azure Storage REST API]
* [Azure Storage 팀 블로그][Azure Storage Team Blog]

자세한 내용은 참고 항목 hello [Java 개발자 센터](/develop/java/)합니다.

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 저장소 클라이언트 SDK 참조]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
