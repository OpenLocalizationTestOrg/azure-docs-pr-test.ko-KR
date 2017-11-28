## <span data-ttu-id="d1b5e-101"><a name="create-client"></a>클라이언트 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="d1b5e-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="d1b5e-102">`WindowsAzure.MobileServiceClient` 개체를 만들어 클라이언트 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="d1b5e-103">`appUrl` 을 모바일 앱에 대한 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-103">Replace `appUrl` with the URL to your Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="d1b5e-104"><a name="table-reference"></a>테이블 작업</span><span class="sxs-lookup"><span data-stu-id="d1b5e-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="d1b5e-105">데이터에 액세스하거나 데이터를 업데이트하려면 백 엔드 테이블에 대한 참조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-105">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="d1b5e-106">`tableName` 을 테이블의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-106">Replace `tableName` with the name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="d1b5e-107">테이블 참조가 있는 경우 테이블을 사용하여 더 많은 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="d1b5e-108">테이블 쿼리</span><span class="sxs-lookup"><span data-stu-id="d1b5e-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="d1b5e-109">데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="d1b5e-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="d1b5e-110">데이터를 통한 페이징</span><span class="sxs-lookup"><span data-stu-id="d1b5e-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="d1b5e-111">데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="d1b5e-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="d1b5e-112">데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="d1b5e-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="d1b5e-113">데이터 수정</span><span class="sxs-lookup"><span data-stu-id="d1b5e-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="d1b5e-114">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="d1b5e-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="d1b5e-115"><a name="querying"></a>방법: 테이블 참조 쿼리</span><span class="sxs-lookup"><span data-stu-id="d1b5e-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="d1b5e-116">테이블 참조가 있는 경우 이를 사용하여 서버에서 데이터를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-116">Once you have a table reference, you can use it to query for data on the server.</span></span>  <span data-ttu-id="d1b5e-117">쿼리는 "LINQ와 유사한" 언어로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="d1b5e-118">테이블에서 모든 데이터를 반환하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-118">To return all data from the table, use the following code:</span></span>

```
/**
 * Process the results that are received by a call to table.read()
 *
 * @param {Object} results the results as a pseudo-array
 * @param {int} results.length the length of the results array
 * @param {Object} results[] the individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - the properties are the columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="d1b5e-119">결과에 대해 success 함수가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-119">The success function is called with the results.</span></span>  <span data-ttu-id="d1b5e-120">success 함수에 `for (var i in results)`를 사용하지 마세요. 다른 쿼리 함수(예: `.includeTotalCount()`)가 사용될 경우 결과에 포함된 정보를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-120">Do not use `for (var i in results)` in the success function as that will iterate over information that is included in the results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="d1b5e-121">쿼리 구문에 대한 자세한 내용은 [쿼리 개체 설명서]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-121">For more information on the Query syntax, see the [Query object documentation].</span></span>

#### <span data-ttu-id="d1b5e-122"><a name="table-filter"></a>서버에서 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="d1b5e-122"><a name="table-filter"></a>Filtering data on the server</span></span>
<span data-ttu-id="d1b5e-123">테이블 참조에서 `where` 절을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-123">You can use a `where` clause on the table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="d1b5e-124">개체를 필터링하는 함수도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-124">You can also use a function that filters the object.</span></span>  <span data-ttu-id="d1b5e-125">이 경우 `this` 변수가 필터링되는 현재 개체에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-125">In this case, the `this` variable is assigned to the current object being filtered.</span></span>  <span data-ttu-id="d1b5e-126">다음 코드는 이전 예와 기능적으로 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-126">The following code is functionally equivalent to the prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="d1b5e-127"><a name="table-paging"></a>데이터를 통한 페이징</span><span class="sxs-lookup"><span data-stu-id="d1b5e-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="d1b5e-128">`take()` 및 `skip()` 메서드를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-128">Utilize the `take()` and `skip()` methods.</span></span>  <span data-ttu-id="d1b5e-129">예를 들어 테이블을 100개 행 레코드로 분할하려는 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-129">For example, if you wish to split the table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get the total number of records
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

<span data-ttu-id="d1b5e-130">`.includeTotalCount()` 메서드는 결과 개체에 totalCount 필드를 추가하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-130">The `.includeTotalCount()` method is used to add a totalCount field to the results object.</span></span>  <span data-ttu-id="d1b5e-131">totalCount 필드는 페이징이 사용되지 않는 경우 반환되는 총 레코드 수로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-131">The totalCount field is filled with the total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="d1b5e-132">다음으로 페이지 변수 및 몇 가지 UI 단추를 사용하여 페이지 목록을 제공할 수 있습니다. 각 페이지에 대해 새 레코드를 로드하는 데 `loadPage()`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-132">You can then use the pages variable and some UI buttons to provide a page list; use `loadPage()` to load the new records for each page.</span></span>  <span data-ttu-id="d1b5e-133">이미 로드된 레코드에 대한 액세스 속도를 높이려면 캐싱을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-133">Implement caching to speed access to records that have already been loaded.</span></span>

#### <span data-ttu-id="d1b5e-134"><a name="sorting-data"></a>방법: 정렬된 데이터 반환</span><span class="sxs-lookup"><span data-stu-id="d1b5e-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="d1b5e-135">`.orderBy()` 또는 `.orderByDescending()` 쿼리 메서드 사용:</span><span class="sxs-lookup"><span data-stu-id="d1b5e-135">Use the `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="d1b5e-136">쿼리 개체에 대한 자세한 내용은 [쿼리 개체 설명서]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-136">For more information on the Query object, see the [Query object documentation].</span></span>

### <span data-ttu-id="d1b5e-137"><a name="inserting"></a>방법: 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="d1b5e-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="d1b5e-138">적절한 날짜로 JavaScript 개체를 만들고 `table.insert()`를 비동기적으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-138">Create a JavaScript object with the appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="d1b5e-139">성공적으로 삽입되면 동기화 작업에 필요한 추가 필드와 함께 삽입된 항목이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-139">On successful insertion, the inserted item is returned with the additional fields that are required for sync operations.</span></span>  <span data-ttu-id="d1b5e-140">이후 업데이트를 위해 사용자 고유의 캐시를 이 정보로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="d1b5e-141">Azure Mobile Apps Node.js 서버 SDK는 개발 목적으로 동적 스키마를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-141">The Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="d1b5e-142">동적 스키마를 통해 삽입 또는 업데이트 작업에 열을 지정하여 테이블에 열을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-142">Dynamic Schema allows you to add columns to the table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="d1b5e-143">응용 프로그램을 프로덕션으로 전환하기 전에 동적 스키마를 해제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-143">We recommend that you turn off dynamic schema before moving your application to production.</span></span>

### <span data-ttu-id="d1b5e-144"><a name="modifying"></a>방법: 데이터 수정</span><span class="sxs-lookup"><span data-stu-id="d1b5e-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="d1b5e-145">`.insert()` 메서드와 마찬가지로 업데이트 개체를 만든 후 `.update()`를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-145">Similar to the `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="d1b5e-146">업데이트 개체는 업데이트할 레코드의 ID를 포함해야 하며 레코드를 읽거나 `.insert()`를 호출할 때 ID를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-146">The update object must contain the ID of the record to be updated - the ID is obtained when reading the record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="d1b5e-147"><a name="deleting"></a>방법: 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="d1b5e-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="d1b5e-148">레코드를 삭제하려면 `.del()` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-148">To delete a record, call the `.del()` method.</span></span>  <span data-ttu-id="d1b5e-149">개체 참조에 ID를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b5e-149">Pass the ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
