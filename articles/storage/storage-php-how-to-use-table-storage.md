---
title: "PHP에서 aaaHow toouse 테이블 저장소 | Microsoft Docs"
description: "Toouse hello PHP toocreate에서 테이블 서비스 하 고 테이블 및 삽입, 삭제 및 쿼리 hello 테이블을 삭제 하는 방법에 대해 알아봅니다."
services: storage
documentationcenter: php
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 1e1036118e208280b4c205da7d7eea61e79359c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a>어떻게 toouse 테이블 PHP에서 저장소
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>개요
이 가이드에서는 tooperform 일반적인 시나리오를 사용 하 여 Azure 테이블 서비스 hello 하는 방법을 알아봅니다. hello PHP로 작성 된 100 개의 샘플과 hello를 사용 하 여 [PHP 용 Azure SDK][download]합니다. hello 가이드에서 다루는 시나리오 포함 **만들기 및 테이블 삭제 및 삽입, 삭제 및 테이블에서 엔터티를 쿼리**합니다. Hello Azure 테이블 서비스에 대 한 자세한 내용은 참조 hello [다음 단계](#next-steps) 섹션.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>PHP 응용 프로그램 만들기
hello Azure 테이블 서비스에 액세스 하는 PHP 응용 프로그램을 만들기 위한 요구 사항은 hello만 hello 코드 내에서 hello Azure SDK의에서 클래스 중에서 PHP에 대 한 참조입니다. 모든 개발 도구 toocreate 메모장 등 응용 프로그램을 사용할 수 있습니다.

이 가이드에서는 PHP 응용 프로그램 내에서 로컬로 또는 Azure 웹 역할, 작업자 역할 또는 웹 사이트 내에서 실행되는 코드에서 호출할 수 있는 테이블 서비스 기능을 사용합니다.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure 클라이언트 라이브러리 가져오기
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a>응용 프로그램 tooaccess hello 테이블 서비스를 구성 합니다.
toouse hello Azure 테이블 서비스 Api 해야합니다.

1. Hello를 사용 하 여 참조 hello 자동 로더에 파일 [require_once] [ require_once] 문 및
2. 사용할 수 있는 모든 클래스 참조

hello 다음 예제에서는 어떻게 tooinclude hello 자동 로더 파일과 참조 hello **ServicesBuilder** 클래스입니다.

> [!NOTE]
> 이 문서의 hello 예제 hello 작성기를 통해 Azure에 대 한 PHP 클라이언트 라이브러리를 설치한 경우를 가정 합니다. Hello 라이브러리를 수동으로 설치 해야 tooreference hello <code>WindowsAzure.php</code> 자동 로더에 파일입니다.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

아래의 hello 예제 hello `require_once` 문에 항상 표시 되지만 hello 클래스만 hello 예제 tooexecute에 필요한 참조 됩니다.

## <a name="set-up-an-azure-storage-connection"></a>Azure 저장소 연결 설정
Azure 테이블 서비스 클라이언트 tooinstantiate 먼저 유효한 연결 문자열이 있어야 합니다. hello hello 테이블 서비스 연결 문자열 형식은 다음과 같습니다.

Live 서비스에 액세스하는 경우:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Hello 에뮬레이터 저장소에 액세스 합니다.

```php
UseDevelopmentStorage=true
```

toocreate 모든 Azure 서비스 클라이언트 toouse hello 해야 **ServicesBuilder** 클래스입니다. 다음을 수행할 수 있습니다.

* Hello 연결을 통과할 tooit 직접 문자열 또는
* 사용 하 여 hello **CloudConfigurationManager (CCM)** toocheck hello 연결 문자열에 대 한 여러 외부 원본:
  * 기본적으로 하나의 외부 소스, 환경 변수에 대한 지원이 제공됩니다.
  * hello를 확장 하 여 새 원본을 추가할 수 있습니다 **ConnectionStringSource** 클래스

Hello 여기에 설명 된 예제를 보려면 hello 연결 문자열을 직접 전달 됩니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a>테이블 만들기
A **TableRestProxy** 개체를 사용 하면 hello로 테이블을 만들 **createTable** 메서드. 테이블을 만들 때 hello 테이블 서비스 제한 시간을 설정할 수 있습니다. (Hello 테이블 서비스 제한 시간에 대 한 자세한 내용은 참조 [테이블 서비스 작업에 대 한 제한 시간 설정][table-service-timeouts].)

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

테이블 이름에 제한에 대 한 정보를 참조 하십시오. [테이블 서비스 데이터 모델 이해 hello][table-data-model]합니다.

## <a name="add-an-entity-tooa-table"></a>엔터티 tooa 테이블 추가
tooadd은 엔터티 tooa 테이블을 새로 만들 **엔터티** 개체를 너무 전달**TableRestProxy insertEntity->**합니다. 엔터티를 만들 때 `PartitionKey` 및 `RowKey`를 지정해야 한다는 점에 주의하세요. 이러한는 hello 엔터티에 대 한 고유 식별자와는 다른 엔터티 속성 보다 훨씬 빠르게 쿼리할 수 있는 값입니다. hello 시스템 사용 하 여 `PartitionKey` tooautomatically 많은 저장소 노드를 통해 hello 테이블의 엔터티를 배포 합니다. 엔터티와 동일한 hello `PartitionKey` hello에 저장 된 동일한 노드. (동일한 노드에서 수행할 hello에 저장 된 여러 엔터티에 대 한 작업을 통해 서로 다른 노드에 저장 되는 엔터티에 대 보다 더 나은.) hello `RowKey` hello 고유 파티션 내의 엔터티 ID입니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

테이블 속성 및 형식에 대 한 정보를 참조 하십시오. [테이블 서비스 데이터 모델 이해 hello][table-data-model]합니다.

hello **TableRestProxy** 클래스에는 엔터티를 삽입 하기 위한 두 가지 대체 방법을 제공: **insertOrMergeEntity** 및 **insertOrReplaceEntity**합니다. toouse 이러한 메서드를 만들 새 **엔터티** 매개 변수 tooeither 메서드로 전달 합니다. 각 메서드는 존재 하지 않는 경우 hello 엔터티를 삽입 합니다. Hello 엔터티 이미 있는 경우 **insertOrMergeEntity** hello 속성이 이미 존재 하는 경우 속성 값을 업데이트 하 고 새 속성 추가 하는 동안 존재 하지 않는 경우 **insertOrReplaceEntity** 완전히 기존 엔터티를 바꿉니다. hello 방법을 예제와 다음 toouse **insertOrMergeEntity**합니다. 하는 경우와 엔터티 hello `PartitionKey` "tasksSeattle" 및 `RowKey` "1"가 아직 없으면, 삽입 됩니다. 그러나 (hello 예제 에서처럼 위의) 이전에 삽입 한, 경우 hello `DueDate` 속성, 업데이트 되 고 hello `Status` 속성에 추가 됩니다. hello `Description` 및 `Location` 값으로는 효과적으로 변경할지 아니면 변경 하지 않고 하지만 속성은도 업데이트 됩니다. 두 속성의 이러한 hello 예제와 같이 추가 되지 되었다가 hello 대상 entity에 존재 하는, 경우 기존의 값은 변경 되지 않습니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified hello DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace hello entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a>단일 엔터티 검색
hello **TableRestProxy getEntity->** 방법을 사용 하면 tooretrieve 엔터티 하나에 대 한 쿼리를 통해 해당 `PartitionKey` 및 `RowKey`합니다. Hello 아래의 예제에서는 파티션 키 hello `tasksSeattle` 와 행 키 `1` toohello 전달 **getEntity** 메서드.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a>파티션의 모든 엔터티 검색
엔터티 쿼리는 필터를 사용하여 구성됩니다(자세한 내용은 [테이블 및 엔터티 쿼리][filters] 참조). tooretrieve hello 필터를 사용 하 여 파티션의 모든 엔터티 "PartitionKey eq *partition_name*"입니다. hello 방법을 예제와 다음 tooretrieve hello에 있는 모든 엔터티 `tasksSeattle` 필터 toohello 전달 하 여 파티션 **queryEntities** 메서드.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a>파티션의 엔터티 하위 집합 검색
hello 이전 예제에서 사용 된 동일한 패턴을 hello 사용된 tooretrieve 파티션에 엔터티 부분이 될 수 있습니다. 검색할 엔터티 hello 하위 집합 사용 hello 필터에 의해 결정 됩니다 (자세한 내용은 참조 [쿼리 하는 테이블 및 엔터티][filters]) 방법을 예제와 다음.hello toouse 필터 tooretrieve 특정 포함 된 모든 엔터티 `Location` 및 `DueDate` 지정된 된 날짜 보다 작아야 합니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a>엔터티 속성 하위 집합 검색
쿼리를 통해 엔터티 속성 하위 집합을 검색할 수 있습니다. *프로젝션*이라고 하는 이 기술은 특히 대역폭을 줄이며 큰 엔터티에 대한 쿼리 성능을 향상시킬 수 있습니다. toospecify 속성 toobe 검색, hello 속성 toohello의 hello 이름을 전달 **쿼리 addSelectField->** 메서드. 더 많은 속성이 여러 번 tooadd이이 메서드를 호출할 수 있습니다. 실행 한 후 **TableRestProxy queryEntities->**, hello 반환 엔터티를 선택 하는 hello 속성 하나만 됩니다. (Tooreturn 테이블 엔터티의 하위 집합을 사용 하도록 하려는 경우 사용할 필터를 위의 hello 쿼리 에서처럼.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in hello table are returned, regardless of whether
// they have hello Description field.
// toolimit hello results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a>엔터티 업데이트
Hello를 사용 하 여 기존 엔터티를 업데이트할 수 있습니다 **엔터티 setProperty->** 및 **엔터티 addProperty->** hello 엔터티와 다음 호출에 대 한 메서드 **TableRestProxy updateEntity->** . hello 다음 예제에서는 엔터티를 검색, 수정 하나의 속성, 다른 속성을 제거 하 고 새 속성을 추가 합니다. 참고 너무 값을 설정 하 여 속성을 제거할 수 있습니다**null**합니다.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a>엔터티 삭제
hello 테이블 이름과 hello 엔터티의 엔터티, toodelete 전달 `PartitionKey` 및 `RowKey` toohello **TableRestProxy deleteEntity->** 메서드.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

동시성 검사에는 엔터티 toobe hello를 사용 하 여 삭제에 대 한 Etag hello 설정할 수 있습니다 **DeleteEntityOptions setEtag->** 메서드와 전달 hello **DeleteEntityOptions** 너무 개체**deleteEntity** 네 번째 매개 변수로 합니다.

## <a name="batch-table-operations"></a>테이블 일괄 작업
hello **TableRestProxy 일괄 처리->** 방법을 tooexecute을 사용 하면 단일 요청에서 여러 작업 합니다. hello 패턴 여기 추가 해야 작업 너무**BatchRequest** 개체와 전달 hello **BatchRequest** toohello 개체 **TableRestProxy 일괄 처리->** 메서드. 작업 tooa tooadd **BatchRequest** 개체를 메서드에 여러 번 수행 하는 hello을 호출할 수 있습니다.

* **addInsertEntity** (insertEntity 작업 추가)
* **addUpdateEntity** (updateEntity 작업 추가)
* **addMergeEntity** (mergeEntity 작업 추가)
* **addInsertOrReplaceEntity** (insertOrReplaceEntity 작업 추가)
* **addInsertOrMergeEntity** (insertOrMergeEntity 작업 추가)
* **addDeleteEntity** (deleteEntity 작업 추가)

hello 방법을 예제와 다음 tooexecute **insertEntity** 및 **deleteEntity** 단일 요청에 작업:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation toolist of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation toolist of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

테이블 일괄 작업에 대한 자세한 내용은 [엔터티 그룹 트랜잭션 수행][entity-group-transactions]을 참조하십시오.

## <a name="delete-a-table"></a>테이블 삭제
테이블을 toodelete hello 테이블 이름 toohello를 전달 하는 마지막으로, **TableRestProxy deleteTable->** 메서드.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>다음 단계
Hello Azure 테이블 서비스의 기본 사항 hello를 알아보았습니다 했으므로 더 복잡 한 저장소 작업에 대 한 이러한 링크 toolearn를 수행 합니다.

* [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.

* [PHP 개발자 센터](/develop/php/)

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
