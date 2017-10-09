---
title: "Azure 테이블 저장소와 Python aaaHow toouse | Microsoft Docs"
description: "Azure 테이블 저장소에는 NoSQL 데이터 저장소를 사용 하 여 hello 클라우드에서 구조화 된 데이터를 저장 합니다."
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
ms.openlocfilehash: fd0e1b05cc12618f348eaf2d85d0dce5ac32702a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a><span data-ttu-id="c45d0-103">어떻게 toouse Python에서 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="c45d0-103">How toouse Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="c45d0-104">이 가이드에서는 알아봅니다 방법을 사용 하 여 Python에서 tooperform 일반적인 Azure 테이블 저장소 시나리오 hello [Python에 대 한 Microsoft Azure 저장소 SDK](https://github.com/Azure/azure-storage-python)합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-104">This guide shows you how tooperform common Azure Table storage scenarios in Python using hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="c45d0-105">가이드에서 다루는 hello 시나리오 만들기 및 테이블 삭제 및 삽입 및 엔터티를 쿼리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-105">hello scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="c45d0-106">이 자습서에서는 hello 시나리오를 통해 작업 하는 동안 toorefer toohello 수도 [Python API 참조에 대 한 Azure 저장소 SDK](https://azure-storage.readthedocs.io/en/latest/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-106">While working through hello scenarios in this tutorial, you may wish toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a><span data-ttu-id="c45d0-107">Python 용 hello Azure 저장소 SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-107">Install hello Azure Storage SDK for Python</span></span>

<span data-ttu-id="c45d0-108">다음 단계는 tooinstall hello 저장소 계정을 만들었으면 [Python에 대 한 Microsoft Azure 저장소 SDK](https://github.com/Azure/azure-storage-python)합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-108">Once you've created a storage account, your next step is tooinstall hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="c45d0-109">설치에 대 한 내용은 hello SDK에 대 한 참조 toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) GitHub에서 Python 저장소에 대 한 hello 저장소 SDK의에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-109">For details on installing hello SDK, refer toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="c45d0-110">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="c45d0-110">Create a table</span></span>

<span data-ttu-id="c45d0-111">Azure 테이블 서비스에서 Python hello로 toowork, 가져와야 hello [TableService] [ py_TableService] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-111">toowork with hello Azure Table service in Python, you must import hello [TableService][py_TableService] module.</span></span> <span data-ttu-id="c45d0-112">작업할 테이블 엔터티로, 또한 해야 hello [엔터티] [ py_Entity] 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-112">Since you'll be working with Table entities, you also need hello [Entity][py_Entity] class.</span></span> <span data-ttu-id="c45d0-113">프로그램 Python 파일 tooimport 모두 hello 맨 위 근처에이 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-113">Add this code near hello top your Python file tooimport both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="c45d0-114">저장소 계정 이름 및 계정 키를 제공하여 [TableService][py_TableService] 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="c45d0-115">대체 `myaccount` 및 `mykey` 계정 이름 및 키 및 호출 포함 [create_table] [ py_create_table] Azure 저장소의 toocreate hello 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] toocreate hello table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="c45d0-116">엔터티 tooa 테이블 추가</span><span class="sxs-lookup"><span data-stu-id="c45d0-116">Add an entity tooa table</span></span>

<span data-ttu-id="c45d0-117">엔터티 tooadd를 먼저 만들어야 패스 hello 개체 toohello 다음 엔터티를 나타내는 개체 [TableService][py_TableService].[ insert_entity] [ py_insert_entity] 메서드.</span><span class="sxs-lookup"><span data-stu-id="c45d0-117">tooadd an entity, you first create an object that represents your entity, then pass hello object toohello [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="c45d0-118">hello 엔터티 개체는 사전 또는 형식의 개체 일 수 있습니다 [엔터티][py_Entity], 회사의 속성 이름 및 값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-118">hello entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="c45d0-119">모든 엔터티에 필요한 hello 포함 되어야 합니다 [PartitionKey 및 RowKey](#partitionkey-and-rowkey) 속성, 더하기 tooany에서 다른 속성에 대해 정의한 hello 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c45d0-119">Every entity must include hello required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition tooany other properties you define for hello entity.</span></span>

<span data-ttu-id="c45d0-120">사전 개체를 만드는이 예제 toohello 전달 다음 엔터티를 나타내는 [insert_entity] [ py_insert_entity] 메서드 tooadd 것 toohello 테이블:</span><span class="sxs-lookup"><span data-stu-id="c45d0-120">This example creates a dictionary object representing an entity, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="c45d0-121">이 예제에서는 만듭니다는 [엔터티] [ py_Entity] 한 다음 toohello 전달 [insert_entity] [ py_insert_entity] 메서드 tooadd 것 toohello 테이블:</span><span class="sxs-lookup"><span data-stu-id="c45d0-121">This example creates an [Entity][py_Entity] object, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="c45d0-122">PartitionKey 및 RowKey</span><span class="sxs-lookup"><span data-stu-id="c45d0-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="c45d0-123">모든 엔터티에 대해 **PartitionKey** 및 **RowKey** 속성을 둘 다 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="c45d0-124">와 함께 이러한는 hello 고유 식별자를 엔터티의 hello 엔터티의 기본 키를 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-124">These are hello unique identifiers of your entities, as together they form hello primary key of an entity.</span></span> <span data-ttu-id="c45d0-125">이러한 속성만 인덱싱되므로 다른 엔터티 속성보다 이러한 값을 사용하면 훨씬 더 빠르게 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="c45d0-126">테이블 서비스 사용 hello **PartitionKey** toointelligently 저장소 노드에서 테이블 엔터티를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-126">hello Table service uses **PartitionKey** toointelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="c45d0-127">포함 된 엔터티를 같은 hello **PartitionKey** hello에 저장 된 동일한 노드.</span><span class="sxs-lookup"><span data-stu-id="c45d0-127">Entities that have hello same  **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="c45d0-128">**RowKey** hello hello 엔터티에 속한 hello 파티션 내에서 고유 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-128">**RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="c45d0-129">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="c45d0-129">Update an entity</span></span>

<span data-ttu-id="c45d0-130">모든 tooupdate hello을 호출 하는 엔터티의 속성 값의 [update_entity] [ py_update_entity] 메서드.</span><span class="sxs-lookup"><span data-stu-id="c45d0-130">tooupdate all of an entity's property values, call hello [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="c45d0-131">이 예에서는 어떻게 tooreplace 기존 엔터티 업데이트 된 버전:</span><span class="sxs-lookup"><span data-stu-id="c45d0-131">This example shows how tooreplace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="c45d0-132">Hello 엔터티를 업데이트 하는 존재 하지 않는 경우 hello 업데이트 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-132">If hello entity that is being updated doesn't already exist, then hello update operation will fail.</span></span> <span data-ttu-id="c45d0-133">존재 여부를 toostore 엔터티를 원하는 경우 사용 하 여 [insert_or_replace_entity][py_insert_or_replace_entity]합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-133">If you want toostore an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="c45d0-134">다음 예제는 hello, hello 첫 번째 호출은 hello 기존 엔터티를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-134">In hello following example, hello first call will replace hello existing entity.</span></span> <span data-ttu-id="c45d0-135">두 번째 호출 hello 새 엔터티를 삽입 하는, hello 테이블에 존재 하는 PartitionKey 및 RowKey hello로 엔터티가 지정 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-135">hello second call will insert a new entity, since no entity with hello specified PartitionKey and RowKey exists in hello table.</span></span>

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="c45d0-136">hello [update_entity] [ py_update_entity] 메서드 모든 속성 및 값도 수 있는 기존 엔터티를 바꾸고 기존 엔터티에서 tooremove 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-136">hello [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use tooremove properties from an existing entity.</span></span> <span data-ttu-id="c45d0-137">Hello를 사용할 수 있습니다 [merge_entity] [ py_merge_entity] 메서드 tooupdate 완전히 hello 엔터티를 바꾸지 않고 새 또는 수정 된 속성 값을 가진 기존 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c45d0-137">You can use hello [merge_entity][py_merge_entity] method tooupdate an existing entity with new or modified property values without completely replacing hello entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="c45d0-138">여러 엔터티 수정</span><span class="sxs-lookup"><span data-stu-id="c45d0-138">Modify multiple entities</span></span>

<span data-ttu-id="c45d0-139">tooensure hello 테이블 서비스에서 요청을 처리 원자성 hello를 함께 일괄 처리에에서 여러 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-139">tooensure hello atomic processing of a request by hello Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="c45d0-140">먼저, hello를 사용 하 여 [TableBatch] [ py_TableBatch] 클래스 tooadd 여러 작업 tooa 단일 일괄 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-140">First, use hello [TableBatch][py_TableBatch] class tooadd multiple operations tooa single batch.</span></span> <span data-ttu-id="c45d0-141">그런 다음 호출 [TableService][py_TableService].[ commit_batch] [ py_commit_batch] 원자 단위 작업에서 toosubmit hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] toosubmit hello operations in an atomic operation.</span></span> <span data-ttu-id="c45d0-142">일괄 처리에서 수정 하는 모든 엔터티 toobe hello에 있어야 합니다. 동일한 파티션에 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-142">All entities toobe modified in batch must be in hello same partition.</span></span>

<span data-ttu-id="c45d0-143">다음 예제에서는 두 엔터티를 일괄적으로 함께 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="c45d0-144">Hello 컨텍스트 관리자 구문을 사용 하 여 일괄 처리를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-144">Batches can also be used with hello context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="c45d0-145">엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="c45d0-145">Query for an entity</span></span>

<span data-ttu-id="c45d0-146">테이블의 엔터티에 대 한 tooquery 해당 PartitionKey 및 RowKey toohello 전달 [TableService][py_TableService].[ get_entity] [ py_get_entity] 메서드.</span><span class="sxs-lookup"><span data-stu-id="c45d0-146">tooquery for an entity in a table, pass its PartitionKey and RowKey toohello [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="c45d0-147">엔터티 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="c45d0-147">Query a set of entities</span></span>

<span data-ttu-id="c45d0-148">Hello로 필터 문자열을 제공 하 여 엔터티 집합을 쿼리할 수 있습니다 **필터** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-148">You can query for a set of entities by supplying a filter string with hello **filter** parameter.</span></span> <span data-ttu-id="c45d0-149">이 예제에서는 PartitionKey에 필터를 적용하여 Seattle에서의 모든 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="c45d0-150">엔터티 속성 하위 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="c45d0-150">Query a subset of entity properties</span></span>

<span data-ttu-id="c45d0-151">쿼리에서 각 엔터티에 대해 반환되는 속성을 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="c45d0-152">*프로젝션*이라고 하는 이 기술은 특히 대역폭을 줄이며 큰 엔터티 또는 결과 집합에 대한 쿼리 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="c45d0-153">사용 하 여 hello **선택** 원하는 hello 속성의 매개 변수 및 통과 hello 이름은 toohello 클라이언트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-153">Use hello **select** parameter and pass hello names of hello properties you want returned toohello client.</span></span>

<span data-ttu-id="c45d0-154">코드 다음 hello hello 쿼리 hello 테이블의 엔터티 hello 설명만를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-154">hello query in hello following code returns only hello descriptions of entities in hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="c45d0-155">다음 코드 조각 works hello Azure 저장소에 대해서만 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-155">hello following snippet works only against hello Azure Storage.</span></span> <span data-ttu-id="c45d0-156">Hello 저장소 에뮬레이터에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-156">It is not supported by hello storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="c45d0-157">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="c45d0-157">Delete an entity</span></span>

<span data-ttu-id="c45d0-158">엔터티는 PartitionKey 및 RowKey toohello 전달 하 여 삭제 [delete_entity] [ py_delete_entity] 메서드.</span><span class="sxs-lookup"><span data-stu-id="c45d0-158">Delete an entity by passing its PartitionKey and RowKey toohello [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="c45d0-159">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="c45d0-159">Delete a table</span></span>

<span data-ttu-id="c45d0-160">테이블 또는 hello 엔터티 내에서 더 이상 필요 하면 호출 hello [delete_table] [ py_delete_table] 메서드 toopermanently hello 테이블 Azure 저장소에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-160">If you no longer need a table or any of hello entities within it, call hello [delete_table][py_delete_table] method toopermanently delete hello table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="c45d0-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c45d0-161">Next steps</span></span>

* [<span data-ttu-id="c45d0-162"> 참조</span><span class="sxs-lookup"><span data-stu-id="c45d0-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="c45d0-163">Azure Storage SDK for Python</span><span class="sxs-lookup"><span data-stu-id="c45d0-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="c45d0-164">Python 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="c45d0-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="c45d0-165">[Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md): Windows, macOS, 및 Linux에서 Azure Storage 데이터를 시각적으로 사용하기 위한 플랫폼 간 무료 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c45d0-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

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
