## <a name="repeatability-during-copy"></a><span data-ttu-id="f789a-101">복사 중 반복성</span><span class="sxs-lookup"><span data-stu-id="f789a-101">Repeatability during Copy</span></span>
<span data-ttu-id="f789a-102">다른 데이터에서 복사 하는 데이터 tooAzure SQL/SQL Server 저장 하면 하나의 요구 tookeep 반복성 유의 tooavoid에 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-102">When copying data tooAzure SQL/SQL Server from other data stores one needs tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="f789a-103">데이터 tooAzure SQL/SQL Server 데이터베이스를 복사할 때 기본적으로 복사 활동 기본 추가 hello toohello 싱크 테이블 데이터 설정 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-103">When copying data tooAzure SQL/SQL Server Database, copy activity will by default APPEND hello data set toohello sink table by default.</span></span> <span data-ttu-id="f789a-104">예를 들어 tooAzure SQL/SQL Server 데이터베이스 레코드 두 개 포함 된 CSV (쉼표로 구분 된 값 데이터) 파일 원본에서 데이터를 복사 하는 경우이 테이블은 어떤 hello 테이블 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-104">For example, when copying data from a CSV (comma separated values data) file source containing two records tooAzure SQL/SQL Server Database, this is what hello table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="f789a-105">Hello 소스 파일의 소스 파일과 2 too4에서 아래로 튜브의 업데이트 된 hello 수량에서 오류를 발견 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-105">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4 in hello source file.</span></span> <span data-ttu-id="f789a-106">그 동안 hello 데이터 조각을 다시 실행 하면 tooAzure SQL/SQL Server 데이터베이스를 추가 하는 두 개의 새 레코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-106">If you re-run hello data slice for that period, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="f789a-107">아래 hello hello 테이블의 열 hello hello primary key 제약 조건이 없거나 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-107">hello below assumes none of hello columns in hello table have hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="f789a-108">tooavoid이 hello 아래 아래에서 설명 하는 2 메커니즘 중 하나를 활용 하 여 toospecify UPSERT 의미 체계를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-108">tooavoid this, you will need toospecify UPSERT semantics by leveraging one of hello below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="f789a-109">분할 영역 수 다시 실행할 수 자동으로 Azure Data Factory에 지정 된 hello 다시 시도 정책에 따라.</span><span class="sxs-lookup"><span data-stu-id="f789a-109">A slice can be re-run automatically in Azure Data Factory as per hello retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="f789a-110">메커니즘 1</span><span class="sxs-lookup"><span data-stu-id="f789a-110">Mechanism 1</span></span>
<span data-ttu-id="f789a-111">활용할 수 있는 **sqlWriterCleanupScript** 속성 toofirst 조각이 실행 될 때 정리 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-111">You can leverage **sqlWriterCleanupScript** property toofirst perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="f789a-112">hello 정리 스크립트 실행 hello SQL 테이블 해당 toothat 조각에서 hello 데이터를 삭제 하는 특정된 조각에 대 한 복사 중 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-112">hello cleanup script would be executed first during copy for a given slice which would delete hello data from hello SQL Table corresponding toothat slice.</span></span> <span data-ttu-id="f789a-113">hello 활동 hello 데이터가 hello SQL 테이블에 삽입 이후에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-113">hello activity will subsequently insert hello data into hello SQL Table.</span></span> 

<span data-ttu-id="f789a-114">Hello 조각을 다시 실행 하면 hello 수량으로 업데이트를 찾을 수 이제 경우 원하는입니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-114">If hello slice is now re-run, then you will find hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="f789a-115">Hello 원래 csv에서 hello 플랫 와셔 레코드를 제거 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-115">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="f789a-116">그런 다음 hello 조각을 다시 실행 결과 다음 hello을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-116">Then re-running hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="f789a-117">새 소식이 toobe 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-117">Nothing new had toobe done.</span></span> <span data-ttu-id="f789a-118">hello 복사 활동 hello 정리 스크립트 toodelete hello 해당 데이터에 대 한 해당 조각의 실행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-118">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="f789a-119">(을 1만 개의 레코드를 포함 한 다음) hello csv에서 hello 입력을 읽은 다음 hello 테이블에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-119">Then it read hello input from hello csv (which then contained only 1 record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="f789a-120">메커니즘 2</span><span class="sxs-lookup"><span data-stu-id="f789a-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f789a-121">sliceIdentifierColumnName은 이번에 Azure SQL 데이터 웨어하우스에 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="f789a-122">다른 메커니즘 tooachieve 반복 하는 전용된 열 것 (**sliceIdentifierColumnName**) hello에 대상 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-122">Another mechanism tooachieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in hello target Table.</span></span> <span data-ttu-id="f789a-123">이 열은 Azure Data Factory tooensure hello 원본 및 대상 된 상태로 유지 되 동기화에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-123">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="f789a-124">이 방법은 더 변경 하거나 hello 대상 SQL 테이블 스키마 정의에 유연성을 제공 하는 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-124">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="f789a-125">반복성을 위해 Azure 데이터 팩터리에서이 열을 사용할 수는 있으며 hello 프로세스에서 Azure 데이터 팩터리를 통해 하지 어떤 스키마도 toohello 테이블을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-125">This column would be used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory will not make any schema changes toohello Table.</span></span> <span data-ttu-id="f789a-126">방법은 toouse이 방법을이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-126">Way toouse this approach:</span></span>

1. <span data-ttu-id="f789a-127">Hello 대상 SQL 테이블에서에서 이진 형식 (32) 열을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-127">Define a column of type binary (32) in hello destination SQL Table.</span></span> <span data-ttu-id="f789a-128">이 열에는 제약 조건이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-128">There should be no constraints on this column.</span></span> <span data-ttu-id="f789a-129">이 예제에서는 이 열의 이름을 'ColumnForADFuseOnly'로 지정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="f789a-130">다음과 같이 hello 복사 활동에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-130">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="f789a-131">Azure Data Factory에는 필요에 따라이 열이 채워집니다 tooensure hello 원본 및 대상 동기화 상태를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-131">Azure Data Factory will populate this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="f789a-132">hello 사용자가이 열의 hello 값이이 컨텍스트 외부에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-132">hello values of this column should not be used outside of this context by hello user.</span></span> 

<span data-ttu-id="f789a-133">비슷한 toomechanism 1, 복사 작업 됩니다 hello hello 대상 SQL 테이블에서에서 분할 영역을 제공 하 고 hello 복사 작업을 정상적으로 실행 한 다음에 대 한 hello 데이터 정리를 자동으로 첫 번째 tooinsert hello 데이터에 대 한 해당 조각의 소스 toodestination에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f789a-133">Similar toomechanism 1, Copy Activity will automatically first clean up hello data for hello given slice from hello destination SQL Table and then run hello copy activity normally tooinsert hello data from source toodestination for that slice.</span></span> 

