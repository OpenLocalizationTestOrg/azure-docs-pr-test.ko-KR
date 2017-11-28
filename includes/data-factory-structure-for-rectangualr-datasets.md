## <a name="specifying-structure-definition-for-rectangular-datasets"></a><span data-ttu-id="67d6c-101">사각형 데이터 집합의 구조 정의 지정</span><span class="sxs-lookup"><span data-stu-id="67d6c-101">Specifying structure definition for rectangular datasets</span></span>
<span data-ttu-id="67d6c-102">데이터 집합 JSON의 구조 섹션은 사각형 테이블(행 및 열 포함)에 대한 **선택적** 섹션으로, 해당 테이블에 대한 열 모음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-102">The structure section in the datasets JSON is an **optional** section for rectangular tables (with rows & columns) and contains a collection of columns for the table.</span></span> <span data-ttu-id="67d6c-103">형식 변환에 필요한 형식 정보를 제공하거나 열 매핑을 수행하기 위해 구조 섹션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-103">You will use the structure section for either providing type information for type conversions or doing column mappings.</span></span> <span data-ttu-id="67d6c-104">다음 섹션에서는 이러한 기능을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-104">The following sections describe these features in detail.</span></span> 

<span data-ttu-id="67d6c-105">각 열에는 다음 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-105">Each column contains the following properties:</span></span>

| <span data-ttu-id="67d6c-106">속성</span><span class="sxs-lookup"><span data-stu-id="67d6c-106">Property</span></span> | <span data-ttu-id="67d6c-107">설명</span><span class="sxs-lookup"><span data-stu-id="67d6c-107">Description</span></span> | <span data-ttu-id="67d6c-108">필수</span><span class="sxs-lookup"><span data-stu-id="67d6c-108">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67d6c-109">name</span><span class="sxs-lookup"><span data-stu-id="67d6c-109">name</span></span> |<span data-ttu-id="67d6c-110">열의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-110">Name of the column.</span></span> |<span data-ttu-id="67d6c-111">예</span><span class="sxs-lookup"><span data-stu-id="67d6c-111">Yes</span></span> |
| <span data-ttu-id="67d6c-112">type</span><span class="sxs-lookup"><span data-stu-id="67d6c-112">type</span></span> |<span data-ttu-id="67d6c-113">열의 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-113">Data type of the column.</span></span> <span data-ttu-id="67d6c-114">형식 정보를 지정해야 할 시기에 대한 자세한 내용은 아래의 형식 변환 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67d6c-114">See type conversions section below for more details regarding when should you specify type information</span></span> |<span data-ttu-id="67d6c-115">아니요</span><span class="sxs-lookup"><span data-stu-id="67d6c-115">No</span></span> |
| <span data-ttu-id="67d6c-116">culture</span><span class="sxs-lookup"><span data-stu-id="67d6c-116">culture</span></span> |<span data-ttu-id="67d6c-117">지정된 형식이 .NET 형식 Datetime 또는 Datetimeoffset일 때 사용할 .NET 기반 culture입니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-117">.NET based culture to be used when type is specified and is .NET type Datetime or Datetimeoffset.</span></span> <span data-ttu-id="67d6c-118">기본값은 "en-us"입니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-118">Default is “en-us”.</span></span> |<span data-ttu-id="67d6c-119">아니요</span><span class="sxs-lookup"><span data-stu-id="67d6c-119">No</span></span> |
| <span data-ttu-id="67d6c-120">format</span><span class="sxs-lookup"><span data-stu-id="67d6c-120">format</span></span> |<span data-ttu-id="67d6c-121">지정된 형식이 .NET 형식 Datetime 또는 Datetimeoffset일 때 사용할 형식 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-121">Format string to be used when type is specified and is .NET type Datetime or Datetimeoffset.</span></span> |<span data-ttu-id="67d6c-122">아니요</span><span class="sxs-lookup"><span data-stu-id="67d6c-122">No</span></span> |

<span data-ttu-id="67d6c-123">다음 샘플에서는 3개의 열 즉, userid, name 및 lastlogindate가 있는 테이블에 대한 구조 섹션 JSON을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-123">The following sample shows the structure section JSON for a table that has three columns userid, name, and lastlogindate.</span></span>

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

<span data-ttu-id="67d6c-124">"structure" 정보를 포함할 시기 및 **structure** 섹션에 포함할 항목에 대해서는 다음 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="67d6c-124">Please use the following guidelines for when to include “structure” information and what to include in the **structure** section.</span></span>

* <span data-ttu-id="67d6c-125">**구조화된 데이터 원본** 의 경우, 싱크의 특정 열에 대해 특정 원본 열의 열 매핑을 수행하려 하고 해당 이름이 동일하지는 않은 경우(아래 열 매핑 섹션의 세부 정보 참조)에만 "structure" 섹션을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-125">**For structured data sources** that store data schema and type information along with the data itself (sources like SQL Server, Oracle, Azure table etc.), you should specify the “structure” section only if you want do column mapping of specific source columns to specific columns in sink and their names are not the same (see details in column mapping section below).</span></span> 
  
    <span data-ttu-id="67d6c-126">위에서 설명했듯이 형식 정보는 "structure" 섹션에서 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-126">As mentioned above, the type information is optional in “structure” section.</span></span> <span data-ttu-id="67d6c-127">구조화된 원본의 경우는 데이터 저장소에서 데이터 집합 정의의 일부로 형식 정보를 이미 사용할 수 있으므로 "structure" 섹션을 포함할 때는 형식 정보를 포함시키지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-127">For structured sources, type information is already available as part of dataset definition in the data store, so you should not include type information when you do include the “structure” section.</span></span>
* <span data-ttu-id="67d6c-128">**읽기 데이터 원본(특히 Azure Blob)의 스키마인 경우** 스키마 또는 형식 정보를 데이터와 함께 저장하지 않고도 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-128">**For schema on read data sources (specifically Azure blob)**  you can choose to store data without storing any schema or type information with the data.</span></span> <span data-ttu-id="67d6c-129">이러한 유형의 데이터 원본에서 다음 2가지 경우는 "structure"를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-129">For these types of data sources you should include “structure” in the following 2 cases:</span></span>
  * <span data-ttu-id="67d6c-130">열 매핑을 수행하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="67d6c-130">You want to do column mapping.</span></span>
  * <span data-ttu-id="67d6c-131">데이터 집합이 복사 작업의 원본이면 "structure"에 형식 정보를 제공할 수 있으며 데이터 팩터리는 싱크에 대한 네이티브 형식으로 변환하기 위해 이 형식 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-131">When the dataset is a source in a Copy activity, you can provide type information in “structure” and data factory will use this type information for conversion to native types for the sink.</span></span> <span data-ttu-id="67d6c-132">자세한 내용은 [Azure Blob 저장소의 데이터 이동](../articles/data-factory/data-factory-azure-blob-connector.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67d6c-132">See [Move data to and from Azure Blob](../articles/data-factory/data-factory-azure-blob-connector.md) article for more information.</span></span>

### <a name="supported-net-based-types"></a><span data-ttu-id="67d6c-133">지원되는 .NET 기반 형식</span><span class="sxs-lookup"><span data-stu-id="67d6c-133">Supported .NET-based types</span></span>
<span data-ttu-id="67d6c-134">데이터 팩터리는 Azure Blob과 같은 읽기 데이터 원본의 스키마에 대해 "structure"에 형식 정보를 제공하기 위해 다음과 같은 CLS 규격 .NET 기반 형식 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-134">Data factory supports the following CLS compliant .NET based type values for providing type information in “structure” for schema on read data sources like Azure blob.</span></span>

* <span data-ttu-id="67d6c-135">Int16</span><span class="sxs-lookup"><span data-stu-id="67d6c-135">Int16</span></span>
* <span data-ttu-id="67d6c-136">Int32</span><span class="sxs-lookup"><span data-stu-id="67d6c-136">Int32</span></span> 
* <span data-ttu-id="67d6c-137">Int64</span><span class="sxs-lookup"><span data-stu-id="67d6c-137">Int64</span></span>
* <span data-ttu-id="67d6c-138">Single</span><span class="sxs-lookup"><span data-stu-id="67d6c-138">Single</span></span>
* <span data-ttu-id="67d6c-139">Double</span><span class="sxs-lookup"><span data-stu-id="67d6c-139">Double</span></span>
* <span data-ttu-id="67d6c-140">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="67d6c-140">Decimal</span></span>
* <span data-ttu-id="67d6c-141">Byte[]</span><span class="sxs-lookup"><span data-stu-id="67d6c-141">Byte[]</span></span>
* <span data-ttu-id="67d6c-142">Bool</span><span class="sxs-lookup"><span data-stu-id="67d6c-142">Bool</span></span>
* <span data-ttu-id="67d6c-143">문자열</span><span class="sxs-lookup"><span data-stu-id="67d6c-143">String</span></span> 
* <span data-ttu-id="67d6c-144">Guid</span><span class="sxs-lookup"><span data-stu-id="67d6c-144">Guid</span></span>
* <span data-ttu-id="67d6c-145">Datetime</span><span class="sxs-lookup"><span data-stu-id="67d6c-145">Datetime</span></span>
* <span data-ttu-id="67d6c-146">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="67d6c-146">Datetimeoffset</span></span>
* <span data-ttu-id="67d6c-147">Timespan</span><span class="sxs-lookup"><span data-stu-id="67d6c-147">Timespan</span></span> 

<span data-ttu-id="67d6c-148">Datetime 및 Datetimeoffset의 경우 사용자 지정 Datetime 문자열의 구문 분석을 용이하게 하려면 "culture" 및 "format" 문자열을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67d6c-148">For Datetime & Datetimeoffset you can also optionally specify “culture” & “format” string to facilitate parsing of your custom Datetime string.</span></span> <span data-ttu-id="67d6c-149">아래의 형식 변환 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67d6c-149">See sample for type conversion below.</span></span>

