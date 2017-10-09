---
title: "aaaHow toouse 테이블 저장소 (c + +) | Microsoft Docs"
description: "Azure 테이블 저장소에는 NoSQL 데이터 저장소를 사용 하 여 hello 클라우드에서 구조화 된 데이터를 저장 합니다."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 8096fe531427ba4858f7f4cb7f664f941892d1c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a>어떻게 toouse c + +에서 테이블 저장소
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>개요
이 가이드 어떻게 tooperform 일반적인 시나리오를 사용 하 여 hello Azure 테이블 저장소 서비스에 표시 됩니다. hello 예제 c + +에서 작성 되 고 hello를 사용 하 여 [c + +에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)합니다. hello 가이드에서 다루는 시나리오 포함 **만들고 테이블 삭제** 및 **테이블 엔터티 작업**합니다.

> [!NOTE]
> 이 가이드의 대상으로 c + + 버전 1.0.0 이상용 Azure 저장소 클라이언트 라이브러리를 hello 합니다. hello 권장 버전을 통해 사용할 수 있는 저장소 클라이언트 라이브러리, 2.2.0 [NuGet](http://www.nuget.org/packages/wastorage) 또는 [GitHub](https://github.com/Azure/azure-storage-cpp/)합니다.
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>C++ 응용 프로그램 만들기
이 가이드에서는 C++ 응용 프로그램 내에서 실행할 수 있는 저장소 기능을 사용합니다. toodo tooinstall, 나오는 c + +에 대 한 Azure 저장소 클라이언트 라이브러리를 hello 및 Azure 구독에 Azure 저장소 계정을 만듭니다.  

Azure 저장소 클라이언트 라이브러리 tooinstall hello c + +에 대 한 hello 다음 메서드를 사용할 수 있습니다.

* **Linux:** hello에 대 한 부여 hello 지침에 따라 [c + + 추가 정보에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 페이지.  
* **Windows:** Visual Studio에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**을 클릭합니다. Hello에 형식 hello 다음 명령은 [NuGet 패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) Enter 키를 누릅니다.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-table-storage"></a>사용자 응용 프로그램 tooaccess 테이블 저장소 구성
Hello 다음 포함 toouse hello Azure 저장소 Api tooaccess 테이블 저장할 hello c + + 파일의 문 toohello 맨 위에 추가 합니다.  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Azure 저장소 연결 문자열 설정
Azure 저장소 클라이언트는 저장소 연결 문자열 toostore 끝점을 사용 하 여 및 데이터 관리 서비스에 액세스 하기 위한 자격 증명입니다. 클라이언트 응용 프로그램을 실행할 때 형식에 따라 hello hello 저장소 연결 문자열을 제공 해야 합니다. 저장소 계정 및 hello 저장소 액세스 키 hello 저장소 계정에 대 한 hello 이름을 사용 하 여 hello에 나열 된 [Azure 포털](https://portal.azure.com) hello에 대 한 *AccountName* 및 *AccountKey* 값입니다. 저장소 계정 및 액세스 키에 대한 자세한 내용은 [Azure 저장소 계정 정보](../storage/common/storage-create-storage-account.md)를 참조하세요. 이 예에서는 정적 필드 toohold hello 연결 문자열을 선언할 수는 방법을 보여 줍니다.  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest 응용 프로그램에서 로컬 Windows 기반 컴퓨터를 Azure hello를 사용할 수 있습니다 [저장소 에뮬레이터](../storage/common/storage-use-emulator.md) hello로 설치 된 [Azure SDK](https://azure.microsoft.com/downloads/)합니다. hello 저장소 에뮬레이터는 로컬 개발 컴퓨터에서 사용할 수 있는 하는 hello Azure Blob, 큐 및 테이블 서비스를 시뮬레이션 하는 유틸리티입니다. hello 다음 예제는 어떻게는 정적 필드 toohold hello 연결 문자열 tooyour 로컬 저장소 에뮬레이터를 선언할 수 있습니다.  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello Azure 저장소 에뮬레이터, hello 클릭 **시작** hello Windows 키 단추를 클릭 하거나 키를 누릅니다. 입력을 시작 **Azure 저장소 에뮬레이터**를 선택한 후 **Microsoft Azure 저장소 에뮬레이터** hello 응용 프로그램 목록에서 합니다.  

hello 다음과 같은 샘플 가정 이러한 두 가지 방법 tooget hello 저장소 연결 문자열 중 하나 사용 하 합니다.  

## <a name="retrieve-your-connection-string"></a>연결 문자열 검색
Hello를 사용할 수 있습니다 **cloud_storage_account** 클래스 toorepresent 저장소 계정 정보. tooretrieve 저장소 계정 hello 저장소 연결 문자열 정보, hello 구문 분석 방법을 사용할 수 있습니다.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

다음으로, 참조 tooa 가져올 **cloud_table_client** 클래스를 엔터티 내에 저장 된 hello 테이블 저장소 서비스 및 테이블에 대 한 개체 참조를 가져올 수 있습니다. hello 다음 코드에서는 **cloud_table_client** 위에 검색에서는 hello 저장소 계정 개체를 사용 하 여 개체:  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>테이블 만들기
**cloud_table_client** 개체를 사용하면 테이블 및 엔터티에 대한 참조 개체를 가져올 수 있습니다. hello 다음 코드에서는 **cloud_table_client** 개체 및 toocreate 새 테이블을 사용 합니다.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a>엔터티 tooa 테이블 추가
tooadd은 엔터티 tooa 테이블을 새로 만들 **table_entity** 개체를 너무 전달**table_operation:: insert_entity**합니다. hello 다음 코드 hello 고객의 이름으로 사용 hello 행 키 이름 및 성 hello 파티션 키로 합니다. 함께 엔터티의 파티션과 행 키는 hello 엔터티 hello 테이블에 고유 하 게 식별 합니다. Hello 동일한 파티션 키를 서로 다른 것 보다 더 빠르게 쿼리할 수 있는 엔터티의 파티션 키, 하지만 다양 한 파티션 키를 사용 하 여 병렬 작업 확장성이 높아집니다. 자세한 내용은 [Microsoft Azure 저장소 성능 및 확장성 검사 목록](../storage/common/storage-performance-checklist.md)을 참조하세요.

hello 다음 코드에서는의 새 인스턴스 **table_entity** 저장 된 일부 고객 데이터 toobe 사용 합니다. 코드의 다음 호출 hello **table_operation:: insert_entity** toocreate는 **table_operation** tooinsert 엔터티를 테이블에 개체 및 연결 된 새 테이블 엔터티 hello 합니다. Hello hello에 메서드를 실행할 hello 코드 호출 마지막으로, **cloud_table** 개체입니다. 및 새 hello **table_operation** hello "people" 테이블로 요청 toohello 테이블 서비스 tooinsert hello 새 customer 엔터티를 보냅니다.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a>엔터티 일괄 삽입
한 번의 쓰기 작업에서 엔터티 toohello 테이블 서비스의 일괄 처리를 삽입할 수 있습니다. hello 다음 코드에서는 **table_batch_operation** 개체를 작업 tooit 삽입 3 개를 추가 합니다. 각 삽입 작업은 해당 값을 설정 하는 새 엔터티 개체를 만들어 추가 되 고 hello를 호출한 다음 insert 메서드 hello에 **table_batch_operation** 개체 tooassociate hello 엔터티를 새 작업을 삽입 합니다. 그런 다음 **cloud_table.execute** tooexecute hello 작업 이라고 합니다.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

일괄 처리 작업에 일부의 toonote:  

* Too100 insert, delete, merge, replace, 조합 단일 일괄 처리에서에서 삽입 또는 병합 및 삽입 또는 바꾸기 작업을 수행할 수 있습니다.  
* 일괄 처리 작업이 hello hello 일괄 처리에서 유일한 작업 하는 경우 검색 작업이 있을 수 있습니다.  
* 단일 일괄 처리 작업의 모든 엔터티가 hello 있어야 합니다. 동일한 파티션 키입니다.  
* 일괄 처리 작업은 제한 된 tooa 4MB 데이터 페이로드입니다.  

## <a name="retrieve-all-entities-in-a-partition"></a>파티션의 모든 엔터티 검색
파티션에서 사용 하 여 모든 엔터티에 대 한 테이블 tooquery는 **table_query** 개체입니다. hello 다음 코드 예제에서는 지정 엔터티 'Smith'는 hello 파티션 키에 대 한 필터입니다. 이 예제는 hello 쿼리 결과 toohello 콘솔의 각 엔터티에의 hello 필드를 인쇄합니다.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

이 예의 쿼리 hello hello 필터 조건과 일치 하는 모든 hello 엔터티를 제공 합니다. 큰 테이블을 한 toodownload hello 테이블 엔터티를 자주 사용 하는 경우 데이터 Azure 저장소 blob에 대신 저장 하는 것이 좋습니다.

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>파티션의 엔터티 범위 검색
않으려면 tooquery 파티션에서 모든 hello 엔터티, 행 키 필터와 hello 파티션 키 필터를 결합 하 여 범위를 지정할 수 있습니다. hello 다음 코드 예제에서는 두 개의 필터 tooget 모든 엔터티 파티션에 'Smith' hello 행 키 (이름)이 이전 hello 알파벳에서 사용 되는 'E'는 문자로 시작 하 고 다음 hello 쿼리 결과 출력 하는 위치입니다.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a>단일 엔터티 검색
단일, 특정 엔터티 쿼리 tooretrieve를 작성할 수 있습니다. hello 다음 코드에서는 **table_operation:: retrieve_entity** toospecify hello 고객 ' 홍길동 '. 이 메서드는 컬렉션을이 아닌 하나의 엔터티를 반환 하 고 hello 반환 된 값은 **table_result**합니다. 쿼리에서 모두 파티션 및 행 키를 지정 하는 hello 가장 빠른 방법은 tooretrieve hello 테이블 서비스에서 단일 엔터티입니다.  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a>엔터티 바꾸기
엔터티에 tooreplace hello 테이블 서비스에서 검색, hello 엔터티 개체를 수정 및 다음 hello 변경 내용을 저장할 toohello 테이블 서비스를 다시 합니다. hello 다음 코드 변경 기존 고객의 전화 번호 및 전자 메일 주소입니다. **table_operation::insert_entity**를 호출하는 대신, 이 코드에서는 **table_operation::replace_entity**를 사용합니다. 이렇게 하면 hello 서버 hello 엔터티 hello 작업이 실패 하는 경우, 검색 된 이후 변경 되지 않은 hello 엔터티 toobe hello 서버에서 완전히 대체 됩니다. 이 오류는 tooprevent 검색 hello와 응용 프로그램의 다른 구성 요소 업데이트 간 응용 프로그램에서 변경 내용을 덮어쓰는 수행 합니다. hello 적절 한 처리가 오류는 tooretrieve hello 엔터티 다시를 원하는 대로 변경한 (여전히 유효한 경우) 한 다음 다른를 수행 **table_operation:: replace_entity** 작업 합니다. 다음 섹션 hello 방법을 살펴보겠습니다 toooverride이이 동작 합니다.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a>엔터티 삽입 또는 바꾸기
**table_operation:: replace_entity** hello 엔터티 hello 서버에서 검색 된 이후 변경 된 경우 작업이 실패 합니다. 에 대 한 순서에서 첫 번째 hello 서버에서 hello 엔터티를 검색 해야 또한 **table_operation:: replace_entity** toobe 성공 합니다. 그러나 경우에 따라 모르는 hello 엔터티 hello 서버에 있고 hello 현재 값에 저장 된 관련 되지 않은 경우-업데이트 내용을 모두 덮어쓰도록 합니다. tooaccomplish이를 사용 하 여 한 **table_operation:: insert_or_replace_entity** 작업 합니다. 이 작업이 존재 하지 않으면 하거나 hello 마지막 업데이트가 수행 된 경우에 관계 없이 수행 하면 대체 하는 경우 hello 엔터티를 삽입 합니다. 다음 코드 예제는 hello, 홍길동에 대 한 hello customer 엔터티를 아직 검색, 하지만 한 다음 다시 toohello 서버를 통해 저장 **table_operation:: insert_or_replace_entity**합니다. Toohello 엔터티 간의 hello 검색 및 업데이트 작업의 모든 업데이트를 덮어쓰게 됩니다.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a>엔터티 속성 하위 집합 쿼리
쿼리 tooa 테이블 엔터티의 몇 개의 속성을 검색할 수 있습니다. hello 쿼리에서 hello 코드 다음에 사용 하 여 hello **table_query:: set_select_columns** 메서드 tooreturn hello 전자 메일 주소만 hello 테이블에 있는 엔터티.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> 모든 속성을 검색하는 것보다 엔터티의 몇 가지 속성을 쿼리하는 것이 더 효율적인 작업입니다.
> 
> 

## <a name="delete-an-entity"></a>엔터티 삭제
엔터티를 검색한 다음 쉽게 삭제할 수 있습니다. Hello 엔터티 검색 되 면 호출 **table_operation:: delete_entity** hello 엔터티 toodelete 사용 합니다. 그런 다음 hello 호출 **cloud_table.execute** 메서드. hello 다음 코드를 검색 하 고 파티션 키 "Smith"와 "Jeff"의 행 키가 있는 엔터티를 삭제 합니다.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a>테이블 삭제
마지막으로, 다음 코드 예제는 hello 저장소 계정에서 테이블을 삭제 합니다. 삭제 된 테이블을 사용할 수 없는 toobe hello 삭제 시간 기간에 대 한 다시 생성 됩니다.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a>다음 단계
테이블 저장소의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure 저장소에 대 한 자세한 수행 합니다.  

* [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.
* [어떻게 toouse c + +에서 Blob 저장소](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [어떻게 toouse c + +에서 큐 저장소](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [C++에서 Azure 저장소 리소스 나열](../storage/common/storage-c-plus-plus-enumeration.md)
* [C++용 Storage Client Library 참조(영문)](http://azure.github.io/azure-storage-cpp)
* [Azure 저장소 설명서](https://azure.microsoft.com/documentation/services/storage/)
