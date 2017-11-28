---
title: "Ruby에서 Azure 테이블 저장소를 사용하는 방법 | Microsoft Docs"
description: "Azure 테이블 저장소, NoSQL 데이터 저장소를 사용하여 클라우드에 구조화된 데이터를 저장합니다."
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
ms.openlocfilehash: 372bc89f75ad4730f0defbf9d6f9f041ae5ce1bf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-from-ruby"></a><span data-ttu-id="e7881-103">Ruby에서 Azure 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="e7881-103">How to use Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="e7881-104">개요</span><span class="sxs-lookup"><span data-stu-id="e7881-104">Overview</span></span>
<span data-ttu-id="e7881-105">이 가이드에서는 Azure 테이블 서비스를 사용하여 일반 시나리오를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="e7881-106">샘플은 Ruby API를 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-106">The samples are written using the Ruby API.</span></span> <span data-ttu-id="e7881-107">**테이블 만들기 및 삭제, 테이블에서 엔터티 삽입 및 쿼리**등의 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-107">The scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="e7881-108">Ruby 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e7881-108">Create a Ruby application</span></span>
<span data-ttu-id="e7881-109">Ruby 응용 프로그램을 만드는 방법에 대한 지침은 [Azure VM의 Ruby on Rails 웹 응용 프로그램](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7881-109">For instructions how to create a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="e7881-110">저장소에 액세스하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="e7881-110">Configure your application to access Storage</span></span>
<span data-ttu-id="e7881-111">Azure 저장소를 사용하려면 저장소 REST 서비스와 통신하는 편리한 라이브러리 집합이 포함된 Ruby Azure 패키지를 다운로드하여 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-111">To use Azure Storage, you need to download and use the Ruby azure package which includes a set of convenience libraries that communicate with the Storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="e7881-112">RubyGems를 사용하여 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="e7881-112">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="e7881-113">**PowerShell**(Windows), **Terminal**(Mac) 또는 **Bash**(Unix)와 같은 명령줄 인터페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="e7881-114">명령 창에 **gem install azure** 를 입력하여 gem 및 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-114">Type **gem install azure** in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="e7881-115">패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="e7881-115">Import the package</span></span>
<span data-ttu-id="e7881-116">주로 사용하는 텍스트 편집기에서 저장소를 사용할 Ruby 파일의 맨 위에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-116">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="e7881-117">Azure 저장소 연결 설정</span><span class="sxs-lookup"><span data-stu-id="e7881-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="e7881-118">Azure 모듈은 **AZURE\_STORAGE\_ACCOUNT** 및 **AZURE\_STORAGE\_ACCESS\_KEY** 환경 변수를 읽고 Azure Storage 계정에 연결하는 데 필요한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-118">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required to connect to your Azure Storage account.</span></span> <span data-ttu-id="e7881-119">이러한 환경 변수가 설정되지 않으면 **Azure::TableService** 를 사용하기 전에 다음 코드로 계정 정보를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-119">If these environment variables are not set, you must specify the account information before using **Azure::TableService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="e7881-120">Azure 포털의 클래식 또는 Resource Manager 저장소 계정에서 이러한 값을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="e7881-120">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="e7881-121">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-121">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e7881-122">사용하려는 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-122">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="e7881-123">오른쪽의 설정 블레이드에서 **액세스 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-123">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="e7881-124">나타나는 액세스 키 블레이드에 액세스 키 1 및 액세스 키 2가 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-124">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="e7881-125">이 둘 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-125">You can use either of these.</span></span>
5. <span data-ttu-id="e7881-126">복사 아이콘을 클릭하여 키를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-126">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="e7881-127">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="e7881-127">Create a table</span></span>
<span data-ttu-id="e7881-128">**Azure::TableService** 개체를 통해 테이블 및 엔터티에 대한 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-128">The **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="e7881-129">테이블을 만들려면 **create\_table()** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-129">To create a table, use the **create\_table()** method.</span></span> <span data-ttu-id="e7881-130">다음 예제는 테이블을 만들거나 테이블이 있으면 오류를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-130">The following example creates a table or prints the error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="e7881-131">테이블에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="e7881-131">Add an entity to a table</span></span>
<span data-ttu-id="e7881-132">엔터티를 추가하려면 먼저 엔터티 속성을 정의하는 해시 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-132">To add an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="e7881-133">모든 엔터티에 대해 **PartitionKey** 및 **RowKey**를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-133">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="e7881-134">이 두 키는 엔터티의 고유한 식별자이며, 다른 속성보다 훨씬 더 빠르게 쿼리할 수 있는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-134">These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="e7881-135">Azure 저장소는 **PartitionKey** 를 사용하여 여러 저장소 노드를 통해 테이블의 엔터티를 자동으로 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-135">Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="e7881-136">**PartitionKey** 가 동일한 엔터티는 동일한 노드에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-136">Entities with the same **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="e7881-137">**RowKey** 는 엔터티가 속하는 파티션 내에서 엔터티의 고유한 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-137">The **RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="e7881-138">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="e7881-138">Update an entity</span></span>
<span data-ttu-id="e7881-139">다음과 같은 여러 메서드를 사용하여 기존 엔터티를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-139">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="e7881-140">**update\_entity():** 기존 엔터티를 바꿔서 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-140">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="e7881-141">**merge\_entity():** 새 속성 값을 기존 엔터티에 병합하여 기존 엔터티를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-141">**merge\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span>
* <span data-ttu-id="e7881-142">**insert\_or\_merge\_entity():** 기존 엔터티를 바꾸어서 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-142">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="e7881-143">엔터티가 없는 경우 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-143">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="e7881-144">**insert\_or\_replace\_entity():** 새 속성 값을 기존 엔터티에 병합하여 기존 엔터티를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-144">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span> <span data-ttu-id="e7881-145">엔터티가 없는 경우 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-145">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="e7881-146">다음 예제에서는 **update\_entity()**를 사용하여 엔터티를 업데이트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-146">The following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="e7881-147">**update\_entity()** 및 **merge\_entity()**를 사용할 때 업데이트 중인 엔터티가 없는 경우 업데이트 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-147">With **update\_entity()** and **merge\_entity()**, if the entity that you are updating doesn't exist then the update operation will fail.</span></span> <span data-ttu-id="e7881-148">따라서 엔터티의 존재 여부에 상관없이 엔터티를 저장하려면 **insert\_or\_replace\_entity()** 또는 **insert\_or\_merge\_entity()**를 대신 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-148">Therefore if you wish to store an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="e7881-149">엔터티 그룹 작업</span><span class="sxs-lookup"><span data-stu-id="e7881-149">Work with groups of entities</span></span>
<span data-ttu-id="e7881-150">서버에서 원자성 처리를 수행하도록 여러 작업을 일괄적으로 제출하는 것이 좋은 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-150">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="e7881-151">이렇게 하려면 먼저 **Batch** 개체를 만든 다음 **TableService**에서 **execute\_batch()** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-151">To accomplish that, you first create a **Batch** object and then use the **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="e7881-152">다음 예제에서는 RowKey 2와 3을 가진 두 엔터티를 일괄 제출하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-152">The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="e7881-153">동일한 PartitionKey를 가진 엔터티에 대해서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-153">Notice that it only works for entities with the same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="e7881-154">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="e7881-154">Query for an entity</span></span>
<span data-ttu-id="e7881-155">테이블에서 엔터티를 쿼리하려면 테이블 이름인 **PartitionKey** 및 **RowKey**를 전달하여 **get\_entity()** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-155">To query an entity in a table, use the **get\_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="e7881-156">엔터티 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="e7881-156">Query a set of entities</span></span>
<span data-ttu-id="e7881-157">테이블에서 엔터티 집합을 쿼리하려면 쿼리 해시 개체를 만들고 **query\_entities()** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-157">To query a set of entities in a table, create a query hash object and use the **query\_entities()** method.</span></span> <span data-ttu-id="e7881-158">다음 예제에서는 동일한 **PartitionKey**를 가진 엔터티를 모두 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-158">The following example demonstrates getting all the entities with the same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="e7881-159">단일 쿼리에서 반환할 결과 집합이 너무 크면 후속 페이지를 가져오는 데 사용할 수 있는 연속 토큰이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-159">If the result set is too large for a single query to return, a continuation token will be returned which you can use to retrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="e7881-160">엔터티 속성 하위 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="e7881-160">Query a subset of entity properties</span></span>
<span data-ttu-id="e7881-161">테이블 쿼리에서는 엔터티에서 일부 속성만 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-161">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="e7881-162">"프로젝션"이라고 하는 이 기술은 대역폭을 줄이며 특히 큰 엔터티에 대한 쿼리 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-162">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="e7881-163">select 절을 사용하고 가져올 속성의 이름을 클라이언트에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-163">Use the select clause and pass the names of the properties you would like to bring over to the client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="e7881-164">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="e7881-164">Delete an entity</span></span>
<span data-ttu-id="e7881-165">엔터티를 삭제하려면 **delete\_entity()** 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-165">To delete an entity, use the **delete\_entity()** method.</span></span> <span data-ttu-id="e7881-166">엔터티, 엔터티의 PartitionKey 및 RowKey가 포함된 테이블의 이름을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-166">You need to pass in the name of the table which contains the entity, the PartitionKey and RowKey of the entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="e7881-167">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="e7881-167">Delete a table</span></span>
<span data-ttu-id="e7881-168">테이블을 삭제하려면 **delete\_table()** 메서드를 사용하고 삭제하려는 테이블의 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-168">To delete a table, use the **delete\_table()** method and pass in the name of the table you want to delete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="e7881-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e7881-169">Next steps</span></span>

* <span data-ttu-id="e7881-170">[Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)는 Windows, MacOS 및 Linux에서 Azure Storage 데이터로 시각적으로 작업할 수 있도록 해주는 Microsoft의 독립 실행형 무료 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="e7881-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="e7881-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) (영문) 리포지토리</span><span class="sxs-lookup"><span data-stu-id="e7881-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

