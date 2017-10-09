## <a name="create-client"></a>클라이언트 연결 만들기
`WindowsAzure.MobileServiceClient` 개체를 만들어 클라이언트 연결을 만듭니다.  대체 `appUrl` URL tooyour 모바일 앱 사용 합니다.

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a>테이블 작업
tooaccess 또는 update 데이터 참조 toohello 백 엔드 테이블을 만듭니다. 대체 `tableName` 테이블의 이름으로 hello와

```
var table = client.getTable(tableName);
```

테이블 참조가 있는 경우 테이블을 사용하여 더 많은 일을 할 수 있습니다.

* [테이블 쿼리](#querying)
  * [데이터 필터링](#table-filter)
  * [데이터를 통한 페이징](#table-paging)
  * [데이터 정렬](#sorting-data)
* [데이터 삽입](#inserting)
* [데이터 수정](#modifying)
* [데이터 삭제](#deleting)

### <a name="querying"></a>방법: 테이블 참조 쿼리
테이블 참조를 만든 후 데이터 hello 서버에 대 한 tooquery를 사용할 수 있습니다.  쿼리는 "LINQ와 유사한" 언어로 만들어집니다.
tooreturn hello 테이블을 사용 하 여 hello 뒤의 모든 데이터 코드:

```
/**
 * Process hello results that are received by a call tootable.read()
 *
 * @param {Object} results hello results as a pseudo-array
 * @param {int} results.length hello length of hello results array
 * @param {Object} results[] hello individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - hello properties are hello columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

hello 성공 함수 hello 결과 함께 호출 됩니다.  사용 하지 마십시오 `for (var i in results)` hello 성공에 함수 hello 결과에 포함 된 정보를 반복 하는 대로 때 다른 쿼리 함수 (같은 `.includeTotalCount()`) 사용 됩니다.

Hello 쿼리 구문에 대 한 자세한 내용은 hello를 참조 하십시오. [개체 설명서 쿼리].

#### <a name="table-filter"></a>Hello 서버에서 데이터 필터링
사용할 수는 `where` hello 테이블 참조에는 절:

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

Hello 개체를 필터링 하는 함수를 사용할 수 있습니다.  이 경우 hello `this` toothe 현재 개체를 필터링 할이 변수에 할당 됩니다.  코드 다음 hello은 기능적으로 동일한 toohello 이전 예입니다.

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a>데이터를 통한 페이징
Hello 활용 `take()` 및 `skip()` 메서드.  예를 들어, 100 행 레코드로 toosplit hello 테이블을 원하는 경우:

```
var totalCount = 0, pages = 0;

// Step 1 - get hello total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

hello `.includeTotalCount()` 메서드는 사용 되는 tooadd totalCount 필드 toohello 결과 개체입니다.  TotalCount 필드 없는 페이징을 사용 하는 경우 반환 되는 레코드의 총 수 hello로 채워집니다.

Hello 페이지 변수 및 일부 UI 단추 tooprovide 페이지 목록; 사용할 수 있습니다. 사용 하 여 `loadPage()` hello 각 페이지에 대 한 새 레코드를 로드할 수 있습니다.  이미 로드 된 캐싱 toospeed 액세스 toorecords를 구현 합니다.

#### <a name="sorting-data"></a>방법: 정렬된 데이터 반환
사용 하 여 hello `.orderBy()` 또는 `.orderByDescending()` 쿼리 메서드:

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

Hello 쿼리 개체에 대 한 자세한 내용은 hello를 참조 하십시오. [개체 설명서 쿼리].

### <a name="inserting"></a>방법: 데이터 삽입
Hello 적절 한 날짜 및 통화 JavaScript 개체를 만들 `table.insert()` 비동기적으로:

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

성공적인 삽입에서 동기화 작업에 필요한 hello 추가 필드가 포함 된 삽입 hello 항목이 반환 됩니다.  이후 업데이트를 위해 사용자 고유의 캐시를 이 정보로 업데이트합니다.

hello Azure 모바일 앱 Node.js 서버 SDK 개발을 위해 동적 스키마를 지원합니다.  동적 스키마에서는 삽입 또는 업데이트 작업에 지정 하 여 tooadd 열 toohello 테이블.  응용 프로그램 tooproduction 이동 하기 전에 동적 스키마를 해제 하는 것이 좋습니다.

### <a name="modifying"></a>방법: 데이터 수정
비슷한 toohello `.insert()` 메서드를 업데이트 개체를 만들고 다음 호출 `.update()`합니다.  hello 업데이트 개체 있어야 hello 레코드 toobe 업데이트의 hello ID-hello ID를 호출할 때 또는 hello 레코드를 읽을 때 가져온 `.insert()`합니다.

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <a name="deleting"></a>방법: 데이터 삭제
toodelete 레코드 호출 hello `.del()` 메서드.  개체 참조 hello ID를 전달 합니다.

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
