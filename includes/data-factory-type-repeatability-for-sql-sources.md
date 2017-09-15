## <a name="repeatability-during-copy"></a><span data-ttu-id="32165-101">복사 중 반복성</span><span class="sxs-lookup"><span data-stu-id="32165-101">Repeatability during Copy</span></span>
<span data-ttu-id="32165-102">다른 데이터 저장소에서 Azure SQL/SQL Server로 데이터를 복사할 때 의도치 않은 결과를 방지하려면 반복성을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32165-102">When copying data to Azure SQL/SQL Server from other data stores one needs to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="32165-103">Azure SQL/SQL Server 데이터베이스에 데이터를 복사할 때 복사 작업이 기본적으로 싱크 테이블에 데이터 집합을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32165-103">When copying data to Azure SQL/SQL Server Database, copy activity will by default APPEND the data set to the sink table by default.</span></span> <span data-ttu-id="32165-104">예를 들어 두 레코드가 포함된 CSV(쉼표로 구분된 값 데이터) 파일 원본에서 Azure SQL/SQL Server 데이터베이스로 데이터를 복사하는 경우 테이블의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-104">For example, when copying data from a CSV (comma separated values data) file source containing two records to Azure SQL/SQL Server Database, this is what the table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="32165-105">원본 파일에서 오류를 발견하고 Down Tube의 수량을 2개에서 4개로 업데이트했다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-105">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4 in the source file.</span></span> <span data-ttu-id="32165-106">해당 기간에 대한 데이터 조각을 다시 실행하면 Azure/SQL Server 데이터베이스에 새 레코드가 2개 추가된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-106">If you re-run the data slice for that period, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="32165-107">아래에서는 테이블에 기본 키 제약 조건이 있는 열이 없다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="32165-107">The below assumes none of the columns in the table have the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="32165-108">이를 방지하려면 아래에 나온 두 메커니즘 중 하나를 활용하여 UPSERT 의미 체계를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32165-108">To avoid this, you will need to specify UPSERT semantics by leveraging one of the below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="32165-109">조각은 지정된 재시도 정책에 따라 Azure Data Factory에서 자동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-109">A slice can be re-run automatically in Azure Data Factory as per the retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="32165-110">메커니즘 1</span><span class="sxs-lookup"><span data-stu-id="32165-110">Mechanism 1</span></span>
<span data-ttu-id="32165-111">조각을 실행할 때 먼저 정리 작업을 수행하려면 **sqlWriterCleanupScript** 속성을 활용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32165-111">You can leverage **sqlWriterCleanupScript** property to first perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="32165-112">지정된 조각에 대한 복사 중에 정리 스크립트를 먼저 실행하면 SQL 테이블에서 해당 조각에 대한 데이터가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="32165-112">The cleanup script would be executed first during copy for a given slice which would delete the data from the SQL Table corresponding to that slice.</span></span> <span data-ttu-id="32165-113">이 작업은 이어서 SQL 테이블에 해당 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="32165-113">The activity will subsequently insert the data into the SQL Table.</span></span> 

<span data-ttu-id="32165-114">이제 조각을 다시 실행하면 원하는 수량으로 업데이트된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-114">If the slice is now re-run, then you will find the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="32165-115">원본 csv에서 Flat Washer 레코드가 제거되었다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-115">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="32165-116">이제 조각을 다시 실행하면 다음과 같은 결과가 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="32165-116">Then re-running the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="32165-117">새로운 어떤 작업도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-117">Nothing new had to be done.</span></span> <span data-ttu-id="32165-118">복사 작업에서는 정리 스크립트를 실행하여 해당 조각에 대한 데이터를 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-118">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="32165-119">그런 다음 csv(1개의 레코드만 포함)에서 입력을 읽어서 테이블에 삽입했습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-119">Then it read the input from the csv (which then contained only 1 record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="32165-120">메커니즘 2</span><span class="sxs-lookup"><span data-stu-id="32165-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="32165-121">sliceIdentifierColumnName은 이번에 Azure SQL 데이터 웨어하우스에 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="32165-122">반복성을 유지하는 또 다른 메커니즘은 대상 테이블에 전용 열(**sliceIdentifierColumnName**)을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="32165-122">Another mechanism to achieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in the target Table.</span></span> <span data-ttu-id="32165-123">이 열은 Azure 데이터 팩터리에서 원본 및 대상을 동기화 상태로 유지하도록 할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32165-123">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="32165-124">이 방법은 대상 SQL 테이블 스키마를 유연하게 변경하거나 정의할 수 있을 때 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="32165-124">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="32165-125">이 열은 반복성 용도로 Azure 데이터 팩터리에서 사용되며 Azure 데이터 팩터리가 테이블에 대해 어떠한 스키마 변경도 하지 않는 프로세스에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32165-125">This column would be used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory will not make any schema changes to the Table.</span></span> <span data-ttu-id="32165-126">이 방식을 사용하는 방법:</span><span class="sxs-lookup"><span data-stu-id="32165-126">Way to use this approach:</span></span>

1. <span data-ttu-id="32165-127">대상 SQL 테이블에서 이진 형식(32)으로 열을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="32165-127">Define a column of type binary (32) in the destination SQL Table.</span></span> <span data-ttu-id="32165-128">이 열에는 제약 조건이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32165-128">There should be no constraints on this column.</span></span> <span data-ttu-id="32165-129">이 예제에서는 이 열의 이름을 'ColumnForADFuseOnly'로 지정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="32165-130">복사 작업에서 다음과 같이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32165-130">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="32165-131">Azure 데이터 팩터리에서는 원본 및 대상을 동기화 상태로 유지하기 위해 필요에 따라 이 열을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="32165-131">Azure Data Factory will populate this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="32165-132">이 열의 값은 이 컨텍스트 외부에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="32165-132">The values of this column should not be used outside of this context by the user.</span></span> 

<span data-ttu-id="32165-133">메커니즘 1과 마찬가지로, 복사 작업은 먼저 대상 SQL 테이블에서 지정된 조각에 대한 데이터를 자동으로 정리한 다음, 정상적으로 복사 작업을 실행하여 원본에서 대상으로 해당 조각의 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="32165-133">Similar to mechanism 1, Copy Activity will automatically first clean up the data for the given slice from the destination SQL Table and then run the copy activity normally to insert the data from source to destination for that slice.</span></span> 

