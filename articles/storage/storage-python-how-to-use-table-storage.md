---
title: "Python에서 Azure Table Storage를 사용하는 방법 | Microsoft Docs"
description: "Azure 테이블 저장소, NoSQL 데이터 저장소를 사용하여 클라우드에 구조화된 데이터를 저장합니다."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: marsma
ms.openlocfilehash: c310a52182bbc3cf44ed4dc6a04e97aa59200a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-in-python"></a><span data-ttu-id="468f1-103">Python에서 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="468f1-103">How to use Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="468f1-104">이 가이드에서는 [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python)을 사용하여 Python에서 일반적인 Azure Table Storage 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-104">This guide shows you how to perform common Azure Table storage scenarios in Python using the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="468f1-105">테이블 만들기 및 삭제, 엔터티 삽입 및 쿼리 등의 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-105">The scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="468f1-106">이 자습서의 시나리오를 진행하면서 [Azure Storage SDK for Python 참조](https://azure-storage.readthedocs.io/en/latest/index.html)를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-106">While working through the scenarios in this tutorial, you may wish to refer to the [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-the-azure-storage-sdk-for-python"></a><span data-ttu-id="468f1-107">Azure Storage SDK for Python 설치</span><span class="sxs-lookup"><span data-stu-id="468f1-107">Install the Azure Storage SDK for Python</span></span>

<span data-ttu-id="468f1-108">저장소 계정을 만들었으면 다음 단계는 [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python)을 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-108">Once you've created a storage account, your next step is to install the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="468f1-109">SDK 설치에 대한 자세한 내용은 GitHub의 Storage SDK for Python 리포지토리에서 [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="468f1-109">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in the Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="468f1-110">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="468f1-110">Create a table</span></span>

<span data-ttu-id="468f1-111">Python에서 Azure Table service를 사용하려면 [TableService][py_TableService] 모듈을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-111">To work with the Azure Table service in Python, you must import the [TableService][py_TableService] module.</span></span> <span data-ttu-id="468f1-112">Table 엔터티로 작업하게 되므로 [Entity][py_Entity] 클래스도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-112">Since you'll be working with Table entities, you also need the [Entity][py_Entity] class.</span></span> <span data-ttu-id="468f1-113">둘 다 가져오려면 Python 파일 위쪽에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-113">Add this code near the top your Python file to import both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="468f1-114">저장소 계정 이름 및 계정 키를 제공하여 [TableService][py_TableService] 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="468f1-115">`myaccount` 및 `mykey`를 계정 이름 및 키로 바꾸고 [create_table][py_create_table]을 호출하여 Azure Storage에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] to create the table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="468f1-116">테이블에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="468f1-116">Add an entity to a table</span></span>

<span data-ttu-id="468f1-117">엔터티를 추가하려면 먼저 엔터티를 나타내는 개체를 만든 후 [TableService][py_TableService].[insert_entity][ py_insert_entity] 메서드에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-117">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="468f1-118">엔터티 개체는 [Entity][py_Entity] 형식의 사전 또는 개체일 수 있으며 엔터티의 속성 이름 및 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-118">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="468f1-119">모든 엔터티에는 사용자가 엔터티에 정의하는 다른 속성 외에 필수 [PartitionKey 및 RowKey](#partitionkey-and-rowkey) 속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-119">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span></span>

<span data-ttu-id="468f1-120">이 예제에서는 엔터티를 나타내는 사전 개체를 만든 후 [insert_entity][py_insert_entity] 메서드에 전달하여 테이블에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-120">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="468f1-121">이 예제에서는 [Entity][py_Entity] 개체를 만든 후 [insert_entity][py_insert_entity] 메서드에 전달하여 테이블에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-121">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="468f1-122">PartitionKey 및 RowKey</span><span class="sxs-lookup"><span data-stu-id="468f1-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="468f1-123">모든 엔터티에 대해 **PartitionKey** 및 **RowKey** 속성을 둘 다 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="468f1-124">이러한 속성이 함께 모여 엔터티의 기본 키를 형성하므로 엔터티의 고유 식별자에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-124">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span></span> <span data-ttu-id="468f1-125">이러한 속성만 인덱싱되므로 다른 엔터티 속성보다 이러한 값을 사용하면 훨씬 더 빠르게 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="468f1-126">Table service에서는 **PartitionKey**를 사용하여 저장소 노드에서 테이블 엔터티를 지능적으로 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-126">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="468f1-127">동일한 **PartitionKey**를 가진 엔터티는 동일한 노드에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-127">Entities that have the same  **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="468f1-128">**RowKey** 는 엔터티가 속하는 파티션 내에서 엔터티의 고유한 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-128">**RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="468f1-129">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="468f1-129">Update an entity</span></span>

<span data-ttu-id="468f1-130">모든 엔터티의 속성 값을 업데이트하려면 [update_entity][py_update_entity] 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-130">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="468f1-131">이 예제에서는 기존 엔터티를 업데이트된 버전으로 바꾸는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-131">This example shows how to replace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="468f1-132">업데이트 중인 엔터티가 아직 없는 경우 업데이트 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-132">If the entity that is being updated doesn't already exist, then the update operation will fail.</span></span> <span data-ttu-id="468f1-133">존재 여부에 관계 없이 엔터티를 저장하려는 경우 [insert_or_replace_entity][py_insert_or_replace_entity]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-133">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="468f1-134">다음 예제에서 첫 번째 호출은 기존 엔터티를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-134">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="468f1-135">PartitionKey 및 RowKey가 지정된 엔터티가 테이블에 없으므로 두 번째 호출은 새 엔터티를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-135">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span></span>

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="468f1-136">[update_entity][py_update_entity] 메서드는 기존 엔터티의 모든 속성 및 값을 대체합니다. 기존 엔터티에서 속성을 제거할 때도 이 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-136">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span></span> <span data-ttu-id="468f1-137">[merge_entity][py_merge_entity] 메서드를 사용하여 엔터티를 완전히 바꾸지는 않으면서 기존 엔터티를 새 속성 값이나 수정된 속성 값으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-137">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="468f1-138">여러 엔터티 수정</span><span class="sxs-lookup"><span data-stu-id="468f1-138">Modify multiple entities</span></span>

<span data-ttu-id="468f1-139">Table service의 요청의 원자성 처리를 보장하기 위해 여러 작업을 일괄로 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-139">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="468f1-140">먼저 [TableBatch][py_TableBatch] 클래스를 사용하여 여러 작업을 단일 배치에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-140">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span></span> <span data-ttu-id="468f1-141">그런 다음 [TableService][py_TableService].[commit_batch][py_commit_batch]를 호출하여 작업을 원자성 작업으로 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span></span> <span data-ttu-id="468f1-142">일괄로 수정할 모든 엔터티는 동일한 파티션에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-142">All entities to be modified in batch must be in the same partition.</span></span>

<span data-ttu-id="468f1-143">다음 예제에서는 두 엔터티를 일괄적으로 함께 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="468f1-144">컨텍스트 관리자 구문에서 Batch를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-144">Batches can also be used with the context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="468f1-145">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="468f1-145">Query for an entity</span></span>

<span data-ttu-id="468f1-146">테이블의 엔터티를 쿼리하려면 PartitionKey 및 RowKey를 [TableService][py_TableService].[ get_entity][ py_get_entity] 메서드에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-146">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="468f1-147">엔터티 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="468f1-147">Query a set of entities</span></span>

<span data-ttu-id="468f1-148">필터 문자열에 **filter** 매개 변수를 제공하여 엔터티 집합을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-148">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span></span> <span data-ttu-id="468f1-149">이 예제에서는 PartitionKey에 필터를 적용하여 Seattle에서의 모든 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="468f1-150">엔터티 속성 하위 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="468f1-150">Query a subset of entity properties</span></span>

<span data-ttu-id="468f1-151">쿼리에서 각 엔터티에 대해 반환되는 속성을 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="468f1-152">*프로젝션*이라고 하는 이 기술은 특히 대역폭을 줄이며 큰 엔터티 또는 결과 집합에 대한 쿼리 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="468f1-153">**select** 매개 변수를 사용하고 반환하려는 가져올 속성의 이름을 클라이언트에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-153">Use the **select** parameter and pass the names of the properties you want returned to the client.</span></span>

<span data-ttu-id="468f1-154">다음 코드의 쿼리는 테이블에 있는 엔터티의 설명만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-154">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="468f1-155">다음 코드 조각은 Azure Storage에 대해서만 작동하며</span><span class="sxs-lookup"><span data-stu-id="468f1-155">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="468f1-156">저장소 에뮬레이터에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-156">It is not supported by the storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="468f1-157">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="468f1-157">Delete an entity</span></span>

<span data-ttu-id="468f1-158">PartitionKey 및 RowKey를 [delete_entity][ py_delete_entity] 메서드에 제공하여 엔터티를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-158">Delete an entity by passing its PartitionKey and RowKey to the [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="468f1-159">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="468f1-159">Delete a table</span></span>

<span data-ttu-id="468f1-160">테이블 또는 해당 엔터티가 더 이상 필요하지 않으면 [delete_table][py_delete_table] 메서드를 호출하여 Azure Storage에서 테이블을 영구적으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-160">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="468f1-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="468f1-161">Next steps</span></span>

* [<span data-ttu-id="468f1-162"> 참조</span><span class="sxs-lookup"><span data-stu-id="468f1-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="468f1-163">Azure Storage SDK for Python</span><span class="sxs-lookup"><span data-stu-id="468f1-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="468f1-164">Python 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="468f1-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="468f1-165">[Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md): Windows, macOS, 및 Linux에서 Azure Storage 데이터를 시각적으로 사용하기 위한 플랫폼 간 무료 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="468f1-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

[py_commit_batch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.commit_batch
[py_create_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.create_table
[py_delete_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_entity
[py_delete_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_table
[py_Entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.models.html#azure.storage.table.models.Entity
[py_get_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.get_entity
[py_insert_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_entity
[py_insert_or_replace_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_or_replace_entity
[py_merge_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.merge_entity
[py_update_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.update_entity
[py_TableService]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html
[py_TableBatch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tablebatch.html#azure.storage.table.tablebatch.TableBatch
