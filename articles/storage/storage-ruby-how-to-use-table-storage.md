---
title: "Azure 테이블 저장소에서 Ruby aaaHow toouse | Microsoft Docs"
description: "Azure 테이블 저장소에는 NoSQL 데이터 저장소를 사용 하 여 hello 클라우드에서 구조화 된 데이터를 저장 합니다."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 9c77ff9f384a776c9bc075b60b351685c61acc36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a>어떻게 toouse Ruby에서 Azure 테이블 저장소
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>개요
이 가이드에서는 tooperform 일반적인 시나리오를 사용 하 여 Azure 테이블 서비스 hello 하는 방법을 알아봅니다. hello 샘플 hello Ruby API를 사용 하 여 기록 됩니다. hello 가이드에서 다루는 시나리오 포함 **생성 하 고 테이블을 삭제, 삽입 및 테이블에서 엔터티를 쿼리**합니다.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Ruby 응용 프로그램 만들기
어떻게 toocreate는 Ruby 응용 프로그램 참조 [Azure VM에서 레일 웹 응용 프로그램에 Ruby](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)합니다.

## <a name="configure-your-application-tooaccess-storage"></a>사용자 응용 프로그램 tooaccess 저장소 구성
Azure 저장소 toouse toodownload 및 사용 하 여 hello hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 Ruby azure 패키지 해야 합니다.

### <a name="use-rubygems-tooobtain-hello-package"></a>RubyGems tooobtain hello 패키지 사용
1. **PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix)와 같은 명령줄 인터페이스를 사용합니다.
2. 형식 **보석 설치 azure** hello 명령 창 tooinstall hello 보석 및 종속성의 합니다.

### <a name="import-hello-package"></a>Hello 패키지 가져오기
원하는 텍스트 편집기를 사용 하 여 hello toohello hello toouse 저장소 이점을 얻을 수 Ruby 파일 맨 뒤를 추가 합니다.

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Azure 저장소 연결 설정
hello azure 모듈 읽힙니다 hello 환경 변수 **AZURE\_저장소\_계정** 및 **AZURE\_저장소\_액세스\_키**정보에 대 한 tooconnect tooyour Azure 저장소 계정이 필요 합니다. 사용 하기 전에 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 **Azure::TableService** 코드 다음 hello로:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain hello Azure 포털에서에서 기존 또는 리소스 관리자 저장소에서 이러한 값 계정:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Toouse 사용할 toohello 저장소 계정을 이동 합니다.
3. Hello 오른쪽에 hello 설정 블레이드에서 클릭 **선택 키**합니다.
4. 나타나는 hello 액세스 키 블레이드에서 hello 선택 키 1 및 2 선택 키 표시 됩니다. 이 둘 중 하나를 사용할 수 있습니다.
5. Hello 아이콘 toocopy hello 키 toohello 클립보드로 복사를 클릭 합니다.

tooobtain 클래식 저장소에서 이러한 값 hello 클래식 Azure 포털의 계정:

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Toouse 사용할 toohello 저장소 계정을 이동 합니다.
3. 클릭 **액세스 키 관리** hello hello 탐색 창 맨 아래에 있습니다.
4. Hello 팝업 대화 상자에서 hello 저장소 계정 이름, 기본 액세스 키 및 보조 액세스 키 표시 됩니다. 선택 키에 대 한 hello 기본 또는 보조 로케이터로 hello 중 하나를 사용할 수 있습니다.
5. Hello 아이콘 toocopy hello 키 toohello 클립보드로 복사를 클릭 합니다.

## <a name="create-a-table"></a>테이블 만들기
hello **Azure::TableService** 개체 테이블 및 엔터티를 사용할 수 있습니다. toocreate 테이블을 사용 하 여 hello **만들\_table()** 메서드. hello 다음 예제에서는 테이블을 만들거나 인화 hello 오류가 있는 경우.

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a>엔터티 tooa 테이블 추가
먼저 tooadd 엔터티, 엔터티 속성을 정의 하는 해시 개체를 만듭니다. 모든 엔터티에 대해 **PartitionKey** 및 **RowKey**를 지정해야 합니다. 이러한는 hello를 엔터티의 고유 식별자 및 값이 다른 속성 보다 훨씬 빠르게 쿼리할 수 있는 합니다. Azure 저장소를 사용 하 여 **PartitionKey** tooautomatically 많은 저장소 노드를 통해 hello 테이블의 엔터티를 배포 합니다. 엔터티와 동일한 hello **PartitionKey** hello에 저장 된 동일한 노드. hello **RowKey** hello hello 엔터티에 속한 hello 파티션 내에서 고유 ID입니다.

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>엔터티 업데이트
기존 엔터티는 여러 방법을 사용할 수 있는 tooupdate:

* **update\_entity():** 기존 엔터티를 바꿔서 업데이트합니다.
* **병합\_entity():** hello 기존 엔터티에 새 속성 값을 병합 하 여 기존 엔터티를 업데이트 합니다.
* **insert\_or\_merge\_entity():** 기존 엔터티를 바꾸어서 업데이트합니다. 엔터티가 없는 경우 새 엔터티를 삽입합니다.
* **삽입\_또는\_대체\_entity():** hello 기존 엔터티에 새 속성 값을 병합 하 여 기존 엔터티를 업데이트 합니다. 엔터티가 없는 경우 새 엔터티를 삽입합니다.

hello 다음 예제에서는 사용 하 여 엔터티 업데이트 **업데이트\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

와 **업데이트\_entity()** 및 **병합\_entity()**hello 업데이트 작업이 실패 hello 엔터티를 업데이트 하는 존재 하지 않는 경우, 합니다. 따라서 이미 존재 하는지 여부에 관계 없이 엔터티 toostore 하려는 경우 대신 사용 해야 **삽입\_또는\_대체\_entity()** 또는 **삽입\_또는 \_병합\_entity()**합니다.

## <a name="work-with-groups-of-entities"></a>엔터티 그룹 작업
경우에 따라는 의미 toosubmit 여러 작업 함께 일괄 처리 tooensure에 원자성 hello 서버에서 처리 합니다. tooaccomplish를 먼저 만들어야는 **일괄 처리** 개체를 사용 하 여 hello **실행\_batch()** 메서드를 **TableService**합니다. hello 다음 예제에서는 RowKey 2를 가진 두 엔터티가 및 3 일괄 처리에 제출 엔터티에 대 한 작동 hello 동일한 PartitionKey만 유의 하십시오.

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>엔터티 쿼리
테이블을 사용 하 여 hello의 엔터티에 tooquery **가져오기\_entity()** hello 테이블 이름을 전달 하 여 메서드를 **PartitionKey** 및 **RowKey**합니다.

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>엔터티 집합 쿼리
테이블의 엔터티 집합 tooquery 쿼리 해시 개체를 만들고 hello를 사용 하 여 **쿼리\_entities()** 메서드. hello 다음 예제에서는 모든 hello 엔터티 hello로 가져오는 동일한 **PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> Hello 결과 집합에는 단일 쿼리 tooreturn에 비해 너무 큰 경우 연속 토큰이 반환 됩니다 사용할 수 있는 tooretrieve의 후속 페이지입니다.
>
>

## <a name="query-a-subset-of-entity-properties"></a>엔터티 속성 하위 집합 쿼리
쿼리 tooa 테이블 엔터티의 몇 개의 속성을 검색할 수 있습니다. "프로젝션"이라고 하는 이 기술은 대역폭을 줄이며 특히 큰 엔터티에 대한 쿼리 성능을 향상시킬 수 있습니다. 사용 하 여 hello select 절 및 패스 hello 형태의 hello 원하는 toobring toohello 클라이언트를 통해 속성입니다.

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>엔터티 삭제
toodelete 엔터티를 사용 하 여 hello **삭제\_entity()** 메서드. Toopass hello 엔터티, hello PartitionKey 및 RowKey hello 엔터티를 포함 하는 hello 테이블의 hello 이름에 필요 합니다.

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>테이블 삭제
toodelete 테이블을 사용 하 여 hello **삭제\_table()** 메서드와의 hello 이름 전달 hello toodelete 테이블입니다.

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>다음 단계

* [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.
* [Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) (영문) 리포지토리

