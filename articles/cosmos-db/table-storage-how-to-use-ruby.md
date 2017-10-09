---
title: "Azure 테이블 저장소에서 Ruby aaaHow toouse | Microsoft Docs"
description: "Azure 테이블 저장소에는 NoSQL 데이터 저장소를 사용 하 여 hello 클라우드에서 구조화 된 데이터를 저장 합니다."
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 2f9eb5a9160b551d6d1d198869787070c402b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a><span data-ttu-id="30d86-103">어떻게 toouse Ruby에서 Azure 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="30d86-103">How toouse Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="30d86-104">개요</span><span class="sxs-lookup"><span data-stu-id="30d86-104">Overview</span></span>
<span data-ttu-id="30d86-105">이 가이드에서는 tooperform 일반적인 시나리오를 사용 하 여 Azure 테이블 서비스 hello 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="30d86-106">hello 샘플 hello Ruby API를 사용 하 여 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-106">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="30d86-107">hello 가이드에서 다루는 시나리오 포함 **생성 하 고 테이블을 삭제, 삽입 및 테이블에서 엔터티를 쿼리**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-107">hello scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="30d86-108">Ruby 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="30d86-108">Create a Ruby application</span></span>
<span data-ttu-id="30d86-109">어떻게 toocreate는 Ruby 응용 프로그램 참조 [Azure VM에서 레일 웹 응용 프로그램에 Ruby](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-109">For instructions how toocreate a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="30d86-110">사용자 응용 프로그램 tooaccess 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="30d86-110">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="30d86-111">Azure 저장소 toouse toodownload 및 사용 하 여 hello hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 Ruby azure 패키지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-111">toouse Azure Storage, you need toodownload and use hello Ruby azure package which includes a set of convenience libraries that communicate with hello Storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="30d86-112">RubyGems tooobtain hello 패키지 사용</span><span class="sxs-lookup"><span data-stu-id="30d86-112">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="30d86-113">**PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix)와 같은 명령줄 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="30d86-114">형식 **보석 설치 azure** hello 명령 창 tooinstall hello 보석 및 종속성의 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-114">Type **gem install azure** in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="30d86-115">Hello 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="30d86-115">Import hello package</span></span>
<span data-ttu-id="30d86-116">원하는 텍스트 편집기를 사용 하 여 hello toohello hello toouse 저장소 이점을 얻을 수 Ruby 파일 맨 뒤를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-116">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="30d86-117">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="30d86-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="30d86-118">hello azure 모듈 읽힙니다 hello 환경 변수 **AZURE\_저장소\_계정** 및 **AZURE\_저장소\_액세스\_키**정보에 대 한 tooconnect tooyour Azure 저장소 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-118">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required tooconnect tooyour Azure Storage account.</span></span> <span data-ttu-id="30d86-119">사용 하기 전에 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 **Azure::TableService** 코드 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="30d86-119">If these environment variables are not set, you must specify hello account information before using **Azure::TableService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="30d86-120">tooobtain hello Azure 포털에서에서 기존 또는 리소스 관리자 저장소에서 이러한 값 계정:</span><span class="sxs-lookup"><span data-stu-id="30d86-120">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="30d86-121">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-121">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="30d86-122">Toouse 사용할 toohello 저장소 계정을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-122">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="30d86-123">Hello 오른쪽에 hello 설정 블레이드에서 클릭 **선택 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-123">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="30d86-124">나타나는 hello 액세스 키 블레이드에서 hello 선택 키 1 및 2 선택 키 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-124">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="30d86-125">이 둘 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-125">You can use either of these.</span></span>
5. <span data-ttu-id="30d86-126">Hello 아이콘 toocopy hello 키 toohello 클립보드로 복사를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-126">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="30d86-127">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="30d86-127">Create a table</span></span>
<span data-ttu-id="30d86-128">hello **Azure::TableService** 개체 테이블 및 엔터티를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-128">hello **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="30d86-129">toocreate 테이블을 사용 하 여 hello **만들\_table()** 메서드.</span><span class="sxs-lookup"><span data-stu-id="30d86-129">toocreate a table, use hello **create\_table()** method.</span></span> <span data-ttu-id="30d86-130">hello 다음 예제에서는 테이블을 만들거나 인화 hello 오류가 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="30d86-130">hello following example creates a table or prints hello error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="30d86-131">엔터티 tooa 테이블 추가</span><span class="sxs-lookup"><span data-stu-id="30d86-131">Add an entity tooa table</span></span>
<span data-ttu-id="30d86-132">먼저 tooadd 엔터티, 엔터티 속성을 정의 하는 해시 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-132">tooadd an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="30d86-133">모든 엔터티에 대해 **PartitionKey** 및 **RowKey**를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-133">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="30d86-134">이러한는 hello를 엔터티의 고유 식별자 및 값이 다른 속성 보다 훨씬 빠르게 쿼리할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-134">These are hello unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="30d86-135">Azure 저장소를 사용 하 여 **PartitionKey** tooautomatically 많은 저장소 노드를 통해 hello 테이블의 엔터티를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-135">Azure Storage uses **PartitionKey** tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="30d86-136">엔터티와 동일한 hello **PartitionKey** hello에 저장 된 동일한 노드.</span><span class="sxs-lookup"><span data-stu-id="30d86-136">Entities with hello same **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="30d86-137">hello **RowKey** hello hello 엔터티에 속한 hello 파티션 내에서 고유 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-137">hello **RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="30d86-138">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="30d86-138">Update an entity</span></span>
<span data-ttu-id="30d86-139">기존 엔터티는 여러 방법을 사용할 수 있는 tooupdate:</span><span class="sxs-lookup"><span data-stu-id="30d86-139">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="30d86-140">**update\_entity():** 기존 엔터티를 바꿔서 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-140">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="30d86-141">**병합\_entity():** hello 기존 엔터티에 새 속성 값을 병합 하 여 기존 엔터티를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-141">**merge\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span>
* <span data-ttu-id="30d86-142">**insert\_or\_merge\_entity():** 기존 엔터티를 바꾸어서 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-142">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="30d86-143">엔터티가 없는 경우 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-143">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="30d86-144">**삽입\_또는\_대체\_entity():** hello 기존 엔터티에 새 속성 값을 병합 하 여 기존 엔터티를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-144">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span> <span data-ttu-id="30d86-145">엔터티가 없는 경우 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-145">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="30d86-146">hello 다음 예제에서는 사용 하 여 엔터티 업데이트 **업데이트\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="30d86-146">hello following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="30d86-147">와 **업데이트\_entity()** 및 **병합\_entity()**hello 업데이트 작업이 실패 hello 엔터티를 업데이트 하는 존재 하지 않는 경우, 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-147">With **update\_entity()** and **merge\_entity()**, if hello entity that you are updating doesn't exist then hello update operation will fail.</span></span> <span data-ttu-id="30d86-148">따라서 이미 존재 하는지 여부에 관계 없이 엔터티 toostore 하려는 경우 대신 사용 해야 **삽입\_또는\_대체\_entity()** 또는 **삽입\_또는 \_병합\_entity()**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-148">Therefore if you wish toostore an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="30d86-149">엔터티 그룹 작업</span><span class="sxs-lookup"><span data-stu-id="30d86-149">Work with groups of entities</span></span>
<span data-ttu-id="30d86-150">경우에 따라는 의미 toosubmit 여러 작업 함께 일괄 처리 tooensure에 원자성 hello 서버에서 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-150">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="30d86-151">tooaccomplish를 먼저 만들어야는 **일괄 처리** 개체를 사용 하 여 hello **실행\_batch()** 메서드를 **TableService**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-151">tooaccomplish that, you first create a **Batch** object and then use hello **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="30d86-152">hello 다음 예제에서는 RowKey 2를 가진 두 엔터티가 및 3 일괄 처리에 제출</span><span class="sxs-lookup"><span data-stu-id="30d86-152">hello following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="30d86-153">엔터티에 대 한 작동 hello 동일한 PartitionKey만 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="30d86-153">Notice that it only works for entities with hello same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="30d86-154">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="30d86-154">Query for an entity</span></span>
<span data-ttu-id="30d86-155">테이블을 사용 하 여 hello의 엔터티에 tooquery **가져오기\_entity()** hello 테이블 이름을 전달 하 여 메서드를 **PartitionKey** 및 **RowKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-155">tooquery an entity in a table, use hello **get\_entity()** method, by passing hello table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="30d86-156">엔터티 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="30d86-156">Query a set of entities</span></span>
<span data-ttu-id="30d86-157">테이블의 엔터티 집합 tooquery 쿼리 해시 개체를 만들고 hello를 사용 하 여 **쿼리\_entities()** 메서드.</span><span class="sxs-lookup"><span data-stu-id="30d86-157">tooquery a set of entities in a table, create a query hash object and use hello **query\_entities()** method.</span></span> <span data-ttu-id="30d86-158">hello 다음 예제에서는 모든 hello 엔터티 hello로 가져오는 동일한 **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="30d86-158">hello following example demonstrates getting all hello entities with hello same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="30d86-159">Hello 결과 집합에는 단일 쿼리 tooreturn에 비해 너무 큰 경우 연속 토큰이 반환 됩니다 사용할 수 있는 tooretrieve의 후속 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-159">If hello result set is too large for a single query tooreturn, a continuation token will be returned which you can use tooretrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="30d86-160">엔터티 속성 하위 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="30d86-160">Query a subset of entity properties</span></span>
<span data-ttu-id="30d86-161">쿼리 tooa 테이블 엔터티의 몇 개의 속성을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-161">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="30d86-162">"프로젝션"이라고 하는 이 기술은 대역폭을 줄이며 특히 큰 엔터티에 대한 쿼리 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-162">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="30d86-163">사용 하 여 hello select 절 및 패스 hello 형태의 hello 원하는 toobring toohello 클라이언트를 통해 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-163">Use hello select clause and pass hello names of hello properties you would like toobring over toohello client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="30d86-164">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="30d86-164">Delete an entity</span></span>
<span data-ttu-id="30d86-165">toodelete 엔터티를 사용 하 여 hello **삭제\_entity()** 메서드.</span><span class="sxs-lookup"><span data-stu-id="30d86-165">toodelete an entity, use hello **delete\_entity()** method.</span></span> <span data-ttu-id="30d86-166">Toopass hello 엔터티, hello PartitionKey 및 RowKey hello 엔터티를 포함 하는 hello 테이블의 hello 이름에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-166">You need toopass in hello name of hello table which contains hello entity, hello PartitionKey and RowKey of hello entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="30d86-167">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="30d86-167">Delete a table</span></span>
<span data-ttu-id="30d86-168">toodelete 테이블을 사용 하 여 hello **삭제\_table()** 메서드와의 hello 이름 전달 hello toodelete 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-168">toodelete a table, use hello **delete\_table()** method and pass in hello name of hello table you want toodelete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="30d86-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30d86-169">Next steps</span></span>

* <span data-ttu-id="30d86-170">[Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="30d86-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="30d86-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) (영문) 리포지토리</span><span class="sxs-lookup"><span data-stu-id="30d86-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

