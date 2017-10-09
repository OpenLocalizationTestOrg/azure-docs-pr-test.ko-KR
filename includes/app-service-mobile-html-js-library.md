## <span data-ttu-id="60363-101"><a name="create-client"></a>클라이언트 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="60363-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="60363-102">`WindowsAzure.MobileServiceClient` 개체를 만들어 클라이언트 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60363-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="60363-103">대체 `appUrl` URL tooyour 모바일 앱 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60363-103">Replace `appUrl` with the URL tooyour Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="60363-104"><a name="table-reference"></a>테이블 작업</span><span class="sxs-lookup"><span data-stu-id="60363-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="60363-105">tooaccess 또는 update 데이터 참조 toohello 백 엔드 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="60363-105">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="60363-106">대체 `tableName` 테이블의 이름으로 hello와</span><span class="sxs-lookup"><span data-stu-id="60363-106">Replace `tableName` with hello name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="60363-107">테이블 참조가 있는 경우 테이블을 사용하여 더 많은 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60363-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="60363-108">테이블 쿼리</span><span class="sxs-lookup"><span data-stu-id="60363-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="60363-109">데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="60363-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="60363-110">데이터를 통한 페이징</span><span class="sxs-lookup"><span data-stu-id="60363-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="60363-111">데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="60363-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="60363-112">데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="60363-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="60363-113">데이터 수정</span><span class="sxs-lookup"><span data-stu-id="60363-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="60363-114">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="60363-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="60363-115"><a name="querying"></a>방법: 테이블 참조 쿼리</span><span class="sxs-lookup"><span data-stu-id="60363-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="60363-116">테이블 참조를 만든 후 데이터 hello 서버에 대 한 tooquery를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60363-116">Once you have a table reference, you can use it tooquery for data on hello server.</span></span>  <span data-ttu-id="60363-117">쿼리는 "LINQ와 유사한" 언어로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="60363-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="60363-118">tooreturn hello 테이블을 사용 하 여 hello 뒤의 모든 데이터 코드:</span><span class="sxs-lookup"><span data-stu-id="60363-118">tooreturn all data from hello table, use hello following code:</span></span>

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

<span data-ttu-id="60363-119">hello 성공 함수 hello 결과 함께 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60363-119">hello success function is called with hello results.</span></span>  <span data-ttu-id="60363-120">사용 하지 마십시오 `for (var i in results)` hello 성공에 함수 hello 결과에 포함 된 정보를 반복 하는 대로 때 다른 쿼리 함수 (같은 `.includeTotalCount()`) 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60363-120">Do not use `for (var i in results)` in hello success function as that will iterate over information that is included in hello results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="60363-121">Hello 쿼리 구문에 대 한 자세한 내용은 hello를 참조 하십시오. [개체 설명서 쿼리].</span><span class="sxs-lookup"><span data-stu-id="60363-121">For more information on hello Query syntax, see hello [Query object documentation].</span></span>

#### <span data-ttu-id="60363-122"><a name="table-filter"></a>Hello 서버에서 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="60363-122"><a name="table-filter"></a>Filtering data on hello server</span></span>
<span data-ttu-id="60363-123">사용할 수는 `where` hello 테이블 참조에는 절:</span><span class="sxs-lookup"><span data-stu-id="60363-123">You can use a `where` clause on hello table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="60363-124">Hello 개체를 필터링 하는 함수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60363-124">You can also use a function that filters hello object.</span></span>  <span data-ttu-id="60363-125">이 경우 hello `this` toothe 현재 개체를 필터링 할이 변수에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60363-125">In this case, hello `this` variable is assigned toothe current object being filtered.</span></span>  <span data-ttu-id="60363-126">코드 다음 hello은 기능적으로 동일한 toohello 이전 예입니다.</span><span class="sxs-lookup"><span data-stu-id="60363-126">hello following code is functionally equivalent toohello prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="60363-127"><a name="table-paging"></a>데이터를 통한 페이징</span><span class="sxs-lookup"><span data-stu-id="60363-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="60363-128">Hello 활용 `take()` 및 `skip()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="60363-128">Utilize hello `take()` and `skip()` methods.</span></span>  <span data-ttu-id="60363-129">예를 들어, 100 행 레코드로 toosplit hello 테이블을 원하는 경우:</span><span class="sxs-lookup"><span data-stu-id="60363-129">For example, if you wish toosplit hello table into 100-row records:</span></span>

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

<span data-ttu-id="60363-130">hello `.includeTotalCount()` 메서드는 사용 되는 tooadd totalCount 필드 toohello 결과 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="60363-130">hello `.includeTotalCount()` method is used tooadd a totalCount field toohello results object.</span></span>  <span data-ttu-id="60363-131">TotalCount 필드 없는 페이징을 사용 하는 경우 반환 되는 레코드의 총 수 hello로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="60363-131">The totalCount field is filled with hello total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="60363-132">Hello 페이지 변수 및 일부 UI 단추 tooprovide 페이지 목록; 사용할 수 있습니다. 사용 하 여 `loadPage()` hello 각 페이지에 대 한 새 레코드를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60363-132">You can then use hello pages variable and some UI buttons tooprovide a page list; use `loadPage()` to load hello new records for each page.</span></span>  <span data-ttu-id="60363-133">이미 로드 된 캐싱 toospeed 액세스 toorecords를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="60363-133">Implement caching toospeed access toorecords that have already been loaded.</span></span>

#### <span data-ttu-id="60363-134"><a name="sorting-data"></a>방법: 정렬된 데이터 반환</span><span class="sxs-lookup"><span data-stu-id="60363-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="60363-135">사용 하 여 hello `.orderBy()` 또는 `.orderByDescending()` 쿼리 메서드:</span><span class="sxs-lookup"><span data-stu-id="60363-135">Use hello `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="60363-136">Hello 쿼리 개체에 대 한 자세한 내용은 hello를 참조 하십시오. [개체 설명서 쿼리].</span><span class="sxs-lookup"><span data-stu-id="60363-136">For more information on hello Query object, see hello [Query object documentation].</span></span>

### <span data-ttu-id="60363-137"><a name="inserting"></a>방법: 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="60363-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="60363-138">Hello 적절 한 날짜 및 통화 JavaScript 개체를 만들 `table.insert()` 비동기적으로:</span><span class="sxs-lookup"><span data-stu-id="60363-138">Create a JavaScript object with hello appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="60363-139">성공적인 삽입에서 동기화 작업에 필요한 hello 추가 필드가 포함 된 삽입 hello 항목이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60363-139">On successful insertion, hello inserted item is returned with hello additional fields that are required for sync operations.</span></span>  <span data-ttu-id="60363-140">이후 업데이트를 위해 사용자 고유의 캐시를 이 정보로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="60363-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="60363-141">hello Azure 모바일 앱 Node.js 서버 SDK 개발을 위해 동적 스키마를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="60363-141">hello Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="60363-142">동적 스키마에서는 삽입 또는 업데이트 작업에 지정 하 여 tooadd 열 toohello 테이블.</span><span class="sxs-lookup"><span data-stu-id="60363-142">Dynamic Schema allows you tooadd columns toohello table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="60363-143">응용 프로그램 tooproduction 이동 하기 전에 동적 스키마를 해제 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="60363-143">We recommend that you turn off dynamic schema before moving your application tooproduction.</span></span>

### <span data-ttu-id="60363-144"><a name="modifying"></a>방법: 데이터 수정</span><span class="sxs-lookup"><span data-stu-id="60363-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="60363-145">비슷한 toohello `.insert()` 메서드를 업데이트 개체를 만들고 다음 호출 `.update()`합니다.</span><span class="sxs-lookup"><span data-stu-id="60363-145">Similar toohello `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="60363-146">hello 업데이트 개체 있어야 hello 레코드 toobe 업데이트의 hello ID-hello ID를 호출할 때 또는 hello 레코드를 읽을 때 가져온 `.insert()`합니다.</span><span class="sxs-lookup"><span data-stu-id="60363-146">hello update object must contain hello ID of hello record toobe updated - hello ID is obtained when reading hello record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="60363-147"><a name="deleting"></a>방법: 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="60363-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="60363-148">toodelete 레코드 호출 hello `.del()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="60363-148">toodelete a record, call hello `.del()` method.</span></span>  <span data-ttu-id="60363-149">개체 참조 hello ID를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="60363-149">Pass hello ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
