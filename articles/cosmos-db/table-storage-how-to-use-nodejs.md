---
title: "Node.js에서 Azure 테이블 저장소 aaaHow toouse | Microsoft Docs"
description: "Azure 테이블 저장소에는 NoSQL 데이터 저장소를 사용 하 여 hello 클라우드에서 구조화 된 데이터를 저장 합니다."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 21022491a9a21a5365628de93582ea3a325ed869
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a>어떻게 toouse Node.js에서 Azure 테이블 저장소
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>개요
이 항목에서는 tooperform hello Azure 테이블을 사용 하는 일반적인 시나리오는 Node.js 응용 프로그램에서 서비스 하는 방법을 보여 줍니다.

이 항목의 hello 코드 예제는 Node.js 응용 프로그램에 이미 있으면 가정 합니다. 방법에 대 한 정보에 대 한 Azure에서 Node.js 응용 프로그램 toocreate 다음이 항목 중 하나를 참조 하세요.

* [Azure App Service에서 Node.js 웹앱 만들기](../app-service-web/app-service-web-get-started-nodejs.md)
* [빌드 및 WebMatrix를 사용 하는 Node.js 웹 응용 프로그램 tooAzure 배포](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* [빌드 및 Node.js 응용 프로그램 tooan Azure 클라우드 서비스 배포](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (Windows PowerShell 사용)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a>사용자 응용 프로그램 tooaccess Azure 저장소를 구성 합니다.
Azure 저장소 toouse hello 저장소 REST 서비스와 통신 하는 편리한 라이브러리의 집합을 포함 하는 Node.js 용 hello Azure 저장소 SDK 할 수 있습니다.

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a>노드 패키지 관리자 (NPM) tooinstall hello 패키지 사용
1. 와 같은 명령줄 인터페이스를 사용 하 여 **PowerShell** (Windows) **터미널** (Mac) 또는 **를 이용한 적** (Unix) 응용 프로그램을 만든 toohello 폴더를 이동 합니다.
2. 형식 **npm 설치 azure storage** hello 명령 창에서. Hello 명령 출력은 다음 예제와 비슷한 toohello입니다.

       azure-storage@0.5.0 node_modules\azure-storage
       +-- extend@1.2.1
       +-- xmlbuilder@0.4.3
       +-- mime@1.2.11
       +-- node-uuid@1.4.3
       +-- validator@3.22.2
       +-- underscore@1.4.4
       +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
       +-- xml2js@0.2.7 (sax@0.5.2)
       +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. Hello를 수동으로 실행할 수 있습니다 **ls** 명령 tooverify 하는 **노드\_모듈** 폴더를 만들었습니다. 해당 폴더에 있습니다. hello **azure 저장소** tooaccess 저장소가 필요한 hello 라이브러리를 포함 하는 패키지입니다.

### <a name="import-hello-package"></a>Hello 패키지 가져오기
다음 코드 toohello 맨 hello hello 추가 **server.js** 응용 프로그램에서 파일:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Azure 저장소 연결 설정
hello azure 모듈 AZURE hello 환경 변수는 읽기\_저장소\_계정 및 AZURE\_저장소\_액세스\_키 또는 AZURE\_저장소\_연결 \_필요한 정보 tooconnect tooyour Azure 저장소 계정에 대 한 문자열입니다. 호출할 때 hello 계정 정보를 지정 해야 이러한 환경 변수가 설정 되지 않은 경우 **TableService**합니다.

Hello에 hello 환경 변수 설정에 대 한 예제 [Azure 포털](https://portal.azure.com) 는 Azure 웹 사이트를 참조 하십시오. [Azure 테이블 서비스 hello 사용 하 여 Node.js 웹 응용 프로그램](../app-service-web/storage-nodejs-use-table-storage-web-site.md)합니다.

## <a name="create-a-table"></a>테이블 만들기
hello 다음 코드에서는 **TableService** 개체 및 toocreate 새 테이블을 사용 합니다. hello 위쪽 hello 다음 추가 **server.js**합니다.

```nodejs
var tableSvc = azure.createTableService();
```

호출을 너무 hello**createTableIfNotExists** 아직 없는 경우 새 테이블 hello 지정한 이름을 가진 만듭니다. hello 다음 예제에서는 새 라는 테이블을 만들어 'mytable' 아직 없는 경우:

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

hello `result.created` 됩니다 `true` 새 테이블을 만들 경우 및 `false` hello 테이블이 이미 존재 합니다. hello `response` hello 요청에 대 한 정보가 포함 됩니다.

### <a name="filters"></a>필터
(옵션) 필터링 작업이 적용 된 toooperations 사용 하 여 수행 될 수 있습니다 **TableService**합니다. 필터링 작업은 로깅, 자동 재시도 등을 포함할 수 있습니다. 필터는 hello 서명으로 메서드를 구현 하는 개체:

```nodejs
function handle (requestOptions, next)
```

Hello 요청 옵션에 전처리를 수행한 후 hello 메서드는 toocall "다음" 필요 콜백을 뒤 서명에 hello로 전달 합니다.

```nodejs
function (returnObject, finalCallback, next)
```

이 콜백에서 hello returnObject (hello toohello 서버 요청에서에서 응답 hello)를 처리 한 후, hello 콜백 필요 tooeither 다른 필터를 처리 하는 toocontinue 있는 경우 다음에 호출할 단순히 finalCallback를 호출 하거나 그렇지 않으면 tooend hello 서비스 호출 합니다.

재시도 논리를 구현 하는 두 개의 필터 hello Node.js 용 Azure SDK에 포함 된 **ExponentialRetryPolicyFilter** 및 **LinearRetryPolicyFilter**합니다. hello 다음 만듭니다는 **TableService** hello를 사용 하는 개체 **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a>엔터티 tooa 테이블 추가
먼저 tooadd 엔터티, 엔터티 속성을 정의 하는 개체를 만듭니다. 모든 엔터티를 포함 해야 합니다는 **PartitionKey** 및 **RowKey**, 하는 hello 엔터티에 대 한 고유 식별자입니다.

* **PartitionKey** -hello 엔터티에 저장 되어 있는 hello 파티션을 결정 합니다.
* **RowKey** -고유 하 게 hello 파티션 내의 hello 엔터티를 식별 합니다.

**PartitionKey**와 **RowKey**는 모두 문자열 값이어야 합니다. 자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](http://msdn.microsoft.com/library/azure/dd179338.aspx)합니다.

hello 다음은 엔터티 정의의 예입니다. **dueDate**는 **Edm.DateTime** 형식으로 정의됩니다. Hello 형식을 지정 하는 선택적 이며 형식 됩니다 유추 되지 않으면 될 지정 합니다.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> 각 레코드에는 엔터티가 삽입되거나 업데이트될 경우 Azure에서 설정되는 **Timestamp** 필드도 있습니다.
>
>

Hello를 사용할 수도 있습니다 **entityGenerator** toocreate 엔터티. hello 다음 예제에서는 hello hello를 사용 하 여 동일한 작업 엔터티 **entityGenerator**합니다.

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

엔터티 tooyour 테이블 tooadd 전달 hello 엔터티 개체 toohello **insertEntity** 메서드.

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

Hello 작업이 완료 되 면 하는 경우 `result` hello 포함 될 [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) hello의 레코드를 삽입 하 고 `response` hello 작업에 대 한 정보가 포함 됩니다.

예제 응답:

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> 기본적으로 **insertEntity** hello의 일환으로 삽입 하는 hello 엔터티를 반환 하지 않는 `response` 정보입니다. 이 엔터티에 대 한 다른 작업 수행에 계획 하거나 toocache hello 정보를 원하는 경우는 것이 유용한 toohave hello의 일부로 반환 된 `result`합니다. 다음과 같이 **echoContent** 를 사용하도록 설정하면 됩니다.
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>엔터티 업데이트
기존 엔터티는 여러 방법을 사용할 수 있는 tooupdate:

* **replaceEntity** - 기존 엔터티를 바꾸어서 업데이트합니다.
* **mergeEntity** -새 속성 값 hello 기존 엔터티와 병합 하 여 기존 엔터티를 업데이트 합니다.
* **insertOrReplaceEntity** - 기존 엔터티를 바꾸어서 업데이트합니다. 엔터티가 없는 경우 새 엔터티를 삽입합니다.
* **insertOrMergeEntity** -hello 기존에 새 속성 값을 병합 하 여 기존 엔터티를 업데이트 합니다. 엔터티가 없는 경우 새 엔터티를 삽입합니다.

hello 다음 예제에서는 사용 하 여 엔터티 업데이트 **replaceEntity**:

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> 기본적으로 엔터티 업데이트 확인 하지 않습니다 toosee 업데이트 되는 hello 데이터가 이전에 다른 프로세스에 의해 수정 된 경우. toosupport 동시 업데이트:
>
> 1. Hello를 업데이트 되 고 hello 개체의 ETag를 가져옵니다. Hello의 일부분으로이 값이 반환 `response` 모든 엔터티 관련 작업을 통해 검색할 수 있습니다 `response['.metadata'].etag`합니다.
> 2. 엔터티에 대 한 업데이트 작업을 수행할 때는 hello ETag 정보 toohello 새 엔터티를 이전에 검색을 추가 합니다. 예:
>
>       entity2['.metadata'].etag = currentEtag;
> 3. Hello 업데이트 작업을 수행 합니다. 응용 프로그램의 다른 인스턴스와 같이 hello ETag 값을 검색 한 이후 수정 되었으면 hello 엔터티는 `error` 알리는 hello 요청에 지정 된 hello 업데이트 조건이 충족 되지 않았습니다 반환 됩니다.
>
>

와 **replaceEntity** 및 **mergeEntity**, hello 엔터티를 업데이트 하는 존재 하지 않으면 hello 업데이트 작업이 실패 합니다. 따라서 toostore 이미 존재 하는지 여부에 관계 없이 엔터티를 사용 하 여 **insertOrReplaceEntity** 또는 **insertOrMergeEntity**합니다.

hello `result` 작업으로 성공한 업데이트에 대 한 hello 포함 됩니다 **Etag** hello의 엔터티를 업데이트 합니다.

## <a name="work-with-groups-of-entities"></a>엔터티 그룹 작업
경우에 따라는 의미 toosubmit 여러 작업 함께 일괄 처리 tooensure에 원자성 hello 서버에서 처리 합니다. hello를 사용 하는 tooaccomplish **TableBatch** toocreate 일괄 처리, 클래스 및 hello를 사용 하 여 **executeBatch** 방식의 **TableService** tooperform hello 일괄 처리 작업 합니다.

 다음 예제는 hello 일괄 처리에서 두 개의 엔터티를 제출 하는 방법을 보여 줍니다.

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

성공적으로 일괄 처리 작업에 대 한 `result` hello 일괄 처리의 각 작업에 대 한 정보가 포함 됩니다.

### <a name="work-with-batched-operations"></a>일괄 처리 작업
작업은 hello를 확인 하 여 검사할 수 tooa 일괄 처리 추가 `operations` 속성입니다. 작업 메서드 toowork 다음 hello를 사용할 수 있습니다.

* **clear** - 배치에서 모든 작업을 지웁니다.
* **getOperations** -hello 일괄 처리에서 작업을 가져옵니다.
* **hasOperations** -hello 일괄 처리 작업을 포함 하는 경우 true를 반환
* **removeOperations** - 작업을 제거합니다.
* **크기** -반환 hello hello 일괄 처리 작업의 수

## <a name="retrieve-an-entity-by-key"></a>키를 통해 엔터티 검색
특정 엔터티 hello에 따라 tooreturn **PartitionKey** 및 **RowKey**, hello를 사용 하 여 **retrieveEntity** 메서드.

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

이 작업이 완료 되 면 `result` hello 엔터티가 포함 됩니다.

## <a name="query-a-set-of-entities"></a>엔터티 집합 쿼리
tooquery 테이블을 사용 하 여 hello **TableQuery** hello 다음 절을 사용 하 여 쿼리 식을 toobuild 개체:

* **선택** -hello 쿼리에서 반환 된 hello 필드 toobe
* **여기서** -hello 여기서 절

  * **and** - `and` where 조건입니다.
  * **or** - `or` where 조건입니다.
* **top** -hello toofetch 항목의 수

hello 다음 예제에서는 hello 'hometasks'는 PartitionKey와 상위 5 개 항목을 반환 하는 쿼리.

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

**select** 가 사용되지 않았기 때문에 모든 필드가 반환됩니다. 테이블을 사용 하 여 대상 tooperform hello 쿼리 **queryEntities**합니다. hello 다음 예제에서는 'mytable'에서이 쿼리 tooreturn 엔터티.

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

성공 하면 `result.entries` hello 쿼리와 일치 하는 엔터티 배열이 포함 됩니다. Hello 쿼리 수 없습니다 tooreturn 되었으면 모든 엔터티 `result.continuationToken` 됩니다 비-*null* 의 세 번째 매개 변수를 hello 사용할 수 있는 **queryEntities** tooretrieve 더 결과입니다. Hello 초기 쿼리를 사용 하 여 *null* hello 세 번째 매개 변수에 대 한 합니다.

### <a name="query-a-subset-of-entity-properties"></a>엔터티 속성 하위 집합 쿼리
쿼리 tooa 테이블 엔터티의 필드를 몇 개만 검색할 수 있습니다.
따라서 대역폭이 줄어들며 특히 큰 엔터티의 경우 쿼리 성능이 향상될 수 있습니다. 사용 하 여 hello **선택** hello 필드 toobe의 절과 패스 hello 이름을 반환 합니다. 예를 들어 hello 다음 쿼리는 반환만 hello **설명** 및 **dueDate** 필드입니다.

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>엔터티 삭제
파티션 및 행 키를 사용하여 엔터티를 삭제할 수 있습니다. 이 예제에서는 hello **task1** hello 개체에 포함 되어 **RowKey** 및 **PartitionKey** hello 엔터티 toobe 삭제의 값입니다. Hello 개체가 toohello 전달 되며 다음 **deleteEntity** 메서드.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> 다른 프로세스에 의해 수정 되지 않은 항목을 항목 hello tooensure 삭제 하는 경우에 Etag를 사용 하는 것이 좋습니다. ETag 사용 방법에 대한 자세한 내용은 [엔터티 업데이트](#update-an-entity) 를 참조하세요.
>
>

## <a name="delete-a-table"></a>테이블 삭제
hello 코드 다음 저장소 계정에서 테이블을 삭제 합니다.

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

사용 하 여 hello 테이블이 존재 하는지 여부 잘 모르는 경우 **deleteTableIfExists**합니다.

## <a name="use-continuation-tokens"></a>연속토큰 사용
많은 양의 결과를 얻기 위해 테이블을 쿼리하는 경우 연속 토큰을 찾습니다. 제공 될 수 있습니다 많은 양의 데이터 쿼리에 연속 토큰이 있는 경우 볼륨 toorecognize을 작성 하지 마십시오를 인식 하지 수도 있습니다.

hello 결과 엔터티 집합을 쿼리 하는 동안 반환 된 개체는 `continuationToken` 이러한 토큰에 있는 경우에 속성입니다. 사용할 수 있습니다 다음 hello 파티션 및 테이블 엔터티 간에 쿼리 toocontinue toomove를 수행 합니다.

을 쿼리할 때 continuationToken 매개 변수 hello 콜백 함수 hello 쿼리 개체 인스턴스 사이의 제공 될 수 있습니다.

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

Hello를 검사 하는 경우 `continuationToken` 개체를 찾을 수 있습니다 속성 같은 `nextPartitionKey`, `nextRowKey` 및 `targetLocation`, 모든 hello 결과를 사용 하는 tooiterate 될 수 있습니다.

GitHub의 hello Azure 저장소 Node.js 리포지토리 내 연속 샘플 이기도합니다. `examples/samples/continuationsample.js`를 찾아보세요.

## <a name="work-with-shared-access-signatures"></a>공유 액세스 서명 작업
공유 액세스 서명 (SAS) 저장소 계정 이름 또는 키를 제공 하지 않고 안전 하 게 tooprovide 세부적인 액세스 tootables 됩니다. SAS는 tooquery 레코드 모바일 앱을 허용 하는 등 사용 되는 tooprovide 제한 된 액세스 tooyour 데이터 경우가 많습니다.

클라우드 기반 서비스 등는 신뢰할 수 있는 응용 프로그램 hello를 사용 하 여 SAS를 생성 **generateSharedAccessSignature** 의 hello **TableService**, tooan 제공 하 고 신뢰할 수 없는 또는 부분적으로 신뢰할 수 있는 응용 프로그램 같은 모바일 응용 프로그램. hello SAS hello 시작에 설명 하는 정책 및 SAS는 hello 하는 동안 유효는 종료 날짜를 사용 하 여 생성으로 액세스 수준 부여한 toohello SAS 소유자 hello.

hello 다음 예제에서는 hello SAS 소유자 tooquery (r) hello 테이블을 사용 하면 되는 새 공유 액세스 정책 및 100 분 후에 생성 하는 hello 시 만료.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

Note 또한 필요에 따라 hello SAS 소유자가 시도할 때 tooaccess hello 테이블 제공 hello 호스트 정보 이어야 합니다.

클라이언트 응용 프로그램을 사용 하 여 hello SAS와 다음 hello **TableServiceWithSAS** hello 테이블에 대해 tooperform 작업 합니다. 다음 예제는 hello toohello 테이블을 연결 하 고 쿼리를 수행 합니다.

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

Hello SAS 생성 된만 쿼리 액세스를 시도 tooinsert, 업데이트 또는 엔터티를 삭제 된 경우 이후 오류가 반환 됩니다.

### <a name="access-control-lists"></a>액세스 제어 목록
SAS에 대 한 액세스 제어 목록 (ACL) tooset hello 액세스 정책을 사용할 수도 있습니다. 각 클라이언트에 대 한 다른 액세스 정책을 제공 하지만 tooallow 여러 클라이언트 tooaccess hello 테이블을 원하는 경우에 유용 합니다.

ACL은 각 정책에 ID가 연결된 액세스 정책 배열을 사용하여 구현됩니다. 다음 예제는 hello 'user1' 및 'user2'에 대 한 두 개의 정책을 정의 합니다.

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

다음 예제에서는 hello hello hello에 대 한 현재 ACL **hometasks** 테이블을 선택한 다음 사용 하 여 hello 새 정책을 추가 **setTableAcl**합니다. 이 접근 방식을 통해 다음을 수행할 수 있습니다.

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

한 번 ACL 설정 된 hello, 만들 수 있습니다는 정책에 대 한 hello ID에 따라 SAS 합니다. 다음 예제는 hello 사용자 '2'에 대 한 새 SAS를 만듭니다.

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 리소스는 hello를 참조 하세요.

* [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.
* [Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) 리포지토리
* [Node.js 개발자 센터](/develop/nodejs/)
* [만들기 및 Node.js 응용 프로그램 tooan Azure 웹 사이트를 배포 합니다.](../app-service-web/app-service-web-get-started-nodejs.md)
