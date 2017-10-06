---
title: "Azure 테이블 저장소와 Python aaaHow toouse | Microsoft Docs"
description: "Azure 테이블 저장소에는 NoSQL 데이터 저장소를 사용 하 여 hello 클라우드에서 구조화 된 데이터를 저장 합니다."
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: mimig
ms.openlocfilehash: 3382fcd5667a93d5533b5f8fad1d3d1c27f23482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a>어떻게 toouse Python에서 테이블 저장소

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

이 가이드에서는 알아봅니다 방법을 사용 하 여 Python에서 tooperform 일반적인 Azure 테이블 저장소 시나리오 hello [Python에 대 한 Microsoft Azure 저장소 SDK](https://github.com/Azure/azure-storage-python)합니다. 가이드에서 다루는 hello 시나리오 만들기 및 테이블 삭제 및 삽입 및 엔터티를 쿼리를 포함 합니다.

이 자습서에서는 hello 시나리오를 통해 작업 하는 동안 toorefer toohello 수도 [Python API 참조에 대 한 Azure 저장소 SDK](https://azure-storage.readthedocs.io/en/latest/index.html)합니다.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a>Python 용 hello Azure 저장소 SDK를 설치 합니다.

다음 단계는 tooinstall hello 저장소 계정을 만들었으면 [Python에 대 한 Microsoft Azure 저장소 SDK](https://github.com/Azure/azure-storage-python)합니다. 설치에 대 한 내용은 hello SDK에 대 한 참조 toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) GitHub에서 Python 저장소에 대 한 hello 저장소 SDK의에서 파일입니다.

## <a name="create-a-table"></a>테이블 만들기

Azure 테이블 서비스에서 Python hello로 toowork, 가져와야 hello [TableService] [ py_TableService] 모듈입니다. 작업할 테이블 엔터티로, 또한 해야 hello [엔터티] [ py_Entity] 클래스입니다. 프로그램 Python 파일 tooimport 모두 hello 맨 위 근처에이 코드를 추가 합니다.

```python
from azure.storage.table import TableService, Entity
```

저장소 계정 이름 및 계정 키를 제공하여 [TableService][py_TableService] 개체를 만듭니다. 대체 `myaccount` 및 `mykey` 계정 이름 및 키 및 호출 포함 [create_table] [ py_create_table] Azure 저장소의 toocreate hello 테이블입니다.

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a>엔터티 tooa 테이블 추가

엔터티 tooadd를 먼저 만들어야 패스 hello 개체 toohello 다음 엔터티를 나타내는 개체 [TableService][py_TableService].[ insert_entity] [ py_insert_entity] 메서드. hello 엔터티 개체는 사전 또는 형식의 개체 일 수 있습니다 [엔터티][py_Entity], 회사의 속성 이름 및 값을 정의 합니다. 모든 엔터티에 필요한 hello 포함 되어야 합니다 [PartitionKey 및 RowKey](#partitionkey-and-rowkey) 속성, 더하기 tooany에서 다른 속성에 대해 정의한 hello 엔터티.

사전 개체를 만드는이 예제 toohello 전달 다음 엔터티를 나타내는 [insert_entity] [ py_insert_entity] 메서드 tooadd 것 toohello 테이블:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

이 예제에서는 만듭니다는 [엔터티] [ py_Entity] 한 다음 toohello 전달 [insert_entity] [ py_insert_entity] 메서드 tooadd 것 toohello 테이블:

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a>PartitionKey 및 RowKey

모든 엔터티에 대해 **PartitionKey** 및 **RowKey** 속성을 둘 다 지정해야 합니다. 와 함께 이러한는 hello 고유 식별자를 엔터티의 hello 엔터티의 기본 키를 형성 합니다. 이러한 속성만 인덱싱되므로 다른 엔터티 속성보다 이러한 값을 사용하면 훨씬 더 빠르게 쿼리할 수 있습니다.

테이블 서비스 사용 hello **PartitionKey** toointelligently 저장소 노드에서 테이블 엔터티를 배포 합니다. 포함 된 엔터티를 같은 hello **PartitionKey** hello에 저장 된 동일한 노드. **RowKey** hello hello 엔터티에 속한 hello 파티션 내에서 고유 ID입니다.

## <a name="update-an-entity"></a>엔터티 업데이트

모든 tooupdate hello을 호출 하는 엔터티의 속성 값의 [update_entity] [ py_update_entity] 메서드. 이 예에서는 어떻게 tooreplace 기존 엔터티 업데이트 된 버전:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

Hello 엔터티를 업데이트 하는 존재 하지 않는 경우 hello 업데이트 작업이 실패 합니다. 존재 여부를 toostore 엔터티를 원하는 경우 사용 하 여 [insert_or_replace_entity][py_insert_or_replace_entity]합니다. 다음 예제는 hello, hello 첫 번째 호출은 hello 기존 엔터티를 바꿉니다. 두 번째 호출 hello 새 엔터티를 삽입 하는, hello 테이블에 존재 하는 PartitionKey 및 RowKey hello로 엔터티가 지정 되기 때문입니다.

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> hello [update_entity] [ py_update_entity] 메서드 모든 속성 및 값도 수 있는 기존 엔터티를 바꾸고 기존 엔터티에서 tooremove 속성을 사용 합니다. Hello를 사용할 수 있습니다 [merge_entity] [ py_merge_entity] 메서드 tooupdate 완전히 hello 엔터티를 바꾸지 않고 새 또는 수정 된 속성 값을 가진 기존 엔터티.

## <a name="modify-multiple-entities"></a>여러 엔터티 수정

tooensure hello 테이블 서비스에서 요청을 처리 원자성 hello를 함께 일괄 처리에에서 여러 작업을 제출할 수 있습니다. 먼저, hello를 사용 하 여 [TableBatch] [ py_TableBatch] 클래스 tooadd 여러 작업 tooa 단일 일괄 처리 합니다. 그런 다음 호출 [TableService][py_TableService].[ commit_batch] [ py_commit_batch] 원자 단위 작업에서 toosubmit hello 작업 합니다. 일괄 처리에서 수정 하는 모든 엔터티 toobe hello에 있어야 합니다. 동일한 파티션에 합니다.

다음 예제에서는 두 엔터티를 일괄적으로 함께 추가합니다.

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

Hello 컨텍스트 관리자 구문을 사용 하 여 일괄 처리를 사용할 수도 있습니다.

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a>엔터티 쿼리

테이블의 엔터티에 대 한 tooquery 해당 PartitionKey 및 RowKey toohello 전달 [TableService][py_TableService].[ get_entity] [ py_get_entity] 메서드.

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>엔터티 집합 쿼리

Hello로 필터 문자열을 제공 하 여 엔터티 집합을 쿼리할 수 있습니다 **필터** 매개 변수입니다. 이 예제에서는 PartitionKey에 필터를 적용하여 Seattle에서의 모든 작업을 찾습니다.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>엔터티 속성 하위 집합 쿼리

쿼리에서 각 엔터티에 대해 반환되는 속성을 제한할 수도 있습니다. *프로젝션*이라고 하는 이 기술은 특히 대역폭을 줄이며 큰 엔터티 또는 결과 집합에 대한 쿼리 성능을 향상시킬 수 있습니다. 사용 하 여 hello **선택** 원하는 hello 속성의 매개 변수 및 통과 hello 이름은 toohello 클라이언트를 반환 합니다.

코드 다음 hello hello 쿼리 hello 테이블의 엔터티 hello 설명만를 반환 합니다.

> [!NOTE]
> 다음 코드 조각 works hello Azure 저장소에 대해서만 번호입니다. Hello 저장소 에뮬레이터에서 지원 되지 않습니다.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>엔터티 삭제

엔터티는 PartitionKey 및 RowKey toohello 전달 하 여 삭제 [delete_entity] [ py_delete_entity] 메서드.

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a>테이블 삭제

테이블 또는 hello 엔터티 내에서 더 이상 필요 하면 호출 hello [delete_table] [ py_delete_table] 메서드 toopermanently hello 테이블 Azure 저장소에서 삭제 합니다.

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>다음 단계

* [ 참조](https://azure-storage.readthedocs.io/en/latest/index.html)
* [Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python)
* [Python 개발자 센터](https://azure.microsoft.com/develop/python/)
* [Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md): Windows, macOS, 및 Linux에서 Azure Storage 데이터를 시각적으로 사용하기 위한 플랫폼 간 무료 응용 프로그램입니다.

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
