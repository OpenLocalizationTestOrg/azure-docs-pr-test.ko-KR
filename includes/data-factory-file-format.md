## <a name="specifying-formats"></a><span data-ttu-id="06744-101">형식 지정</span><span class="sxs-lookup"><span data-stu-id="06744-101">Specifying formats</span></span>
<span data-ttu-id="06744-102">Azure Data Factory hello 형식 유형만 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-102">Azure Data Factory supports hello following format types:</span></span>

* [<span data-ttu-id="06744-103">텍스트 형식</span><span class="sxs-lookup"><span data-stu-id="06744-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="06744-104">JSON 형식</span><span class="sxs-lookup"><span data-stu-id="06744-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="06744-105">Avro 형식</span><span class="sxs-lookup"><span data-stu-id="06744-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="06744-106">ORC 형식</span><span class="sxs-lookup"><span data-stu-id="06744-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="06744-107">Parquet 형식</span><span class="sxs-lookup"><span data-stu-id="06744-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="06744-108">TextFormat 지정</span><span class="sxs-lookup"><span data-stu-id="06744-108">Specifying TextFormat</span></span>
<span data-ttu-id="06744-109">Tooparse hello 텍스트 파일 또는 텍스트 형식으로 hello 데이터를 쓸 경우 설정 hello `format` `type` 속성 너무**TextFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-109">If you want tooparse hello text files or write hello data in text format, set hello `format` `type` property too**TextFormat**.</span></span> <span data-ttu-id="06744-110">Hello 다음을 지정할 수도 있습니다 **선택적** hello에 대 한 속성 `format` 섹션.</span><span class="sxs-lookup"><span data-stu-id="06744-110">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="06744-111">참조 [TextFormat 예제](#textformat-example) 방법에 대 한 섹션 tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-111">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="06744-112">속성</span><span class="sxs-lookup"><span data-stu-id="06744-112">Property</span></span> | <span data-ttu-id="06744-113">설명</span><span class="sxs-lookup"><span data-stu-id="06744-113">Description</span></span> | <span data-ttu-id="06744-114">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="06744-114">Allowed values</span></span> | <span data-ttu-id="06744-115">필수</span><span class="sxs-lookup"><span data-stu-id="06744-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="06744-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="06744-116">columnDelimiter</span></span> |<span data-ttu-id="06744-117">hello 문자는 파일에 tooseparate 열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-117">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="06744-118">데이터에서 toouse 확률이 높습니다 존재 하는 드문 인쇄할 수 없는 char을 고려할 수 있습니다: 예: 시작의 제목 (SOH)을 나타내는 "\u0001"를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-118">You can consider toouse a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="06744-119">문자는 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-119">Only one character is allowed.</span></span> <span data-ttu-id="06744-120">hello **기본** 값은 **쉼표 (',')**합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-120">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="06744-121">유니코드 문자를 toouse 너무 참조[유니코드 문자](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget에 해당 하는 코드를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-121">toouse an Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="06744-122">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-122">No</span></span> |
| <span data-ttu-id="06744-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="06744-123">rowDelimiter</span></span> |<span data-ttu-id="06744-124">hello 문자는 파일에 tooseparate 행을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-124">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="06744-125">문자는 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-125">Only one character is allowed.</span></span> <span data-ttu-id="06744-126">hello **기본** 값은 hello 읽기의 다음 값 중 하나: **["\r\n", "\r", "\n"]** 및 **"\r\n"** 쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-126">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="06744-127">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-127">No</span></span> |
| <span data-ttu-id="06744-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="06744-128">escapeChar</span></span> |<span data-ttu-id="06744-129">입력된 파일의 hello 내용 tooescape 열 구분 기호를 사용 하는 hello 특수 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-129">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="06744-130">한 테이블에 대해 escapeChar 및 quoteChar을 둘 다 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="06744-131">문자는 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-131">Only one character is allowed.</span></span> <span data-ttu-id="06744-132">기본값은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-132">No default value.</span></span> <br/><br/><span data-ttu-id="06744-133">예: 쉼표 있는 경우 (', ') toohave hello 쉼표 문자 hello 텍스트에는 원하는 수 있지만 hello 열 구분 기호 (예: "Hello, world"), '$' hello 이스케이프 문자로 정의 하 고 문자열을 사용할 수 "Hello$, world" hello 소스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-133">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="06744-134">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-134">No</span></span> |
| <span data-ttu-id="06744-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="06744-135">quoteChar</span></span> |<span data-ttu-id="06744-136">hello 문자 tooquote는 문자열 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-136">hello character used tooquote a string value.</span></span> <span data-ttu-id="06744-137">hello 열 및 행 구분 기호 hello 인용 문자 내 hello 문자열 값의 일부분으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06744-137">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="06744-138">이 속성은 적용 가능한 tooboth 입력 및 데이터 집합을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-138">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="06744-139">한 테이블에 대해 escapeChar 및 quoteChar을 둘 다 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="06744-140">문자는 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-140">Only one character is allowed.</span></span> <span data-ttu-id="06744-141">기본값은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-141">No default value.</span></span> <br/><br/><span data-ttu-id="06744-142">예를 들어, 쉼표가 있는 경우 (', ') hello 열 구분 기호 있지만 hello 텍스트에 쉼표 문자 toohave 원하는 만큼 (예: < Hello, world >), 정의할 수 있습니다 "(큰따옴표) hello 인용 문자 및 문자열 hello를 사용 하 여"Hello, world"hello 소스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-142">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="06744-143">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-143">No</span></span> |
| <span data-ttu-id="06744-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="06744-144">nullValue</span></span> |<span data-ttu-id="06744-145">하나 이상의 문자 toorepresent null 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-145">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="06744-146">하나 이상의 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-146">One or more characters.</span></span> <span data-ttu-id="06744-147">hello **기본** 값은 **"\N" 및 "NULL"** 읽기 및 **"\N"** 쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-147">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="06744-148">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-148">No</span></span> |
| <span data-ttu-id="06744-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="06744-149">encodingName</span></span> |<span data-ttu-id="06744-150">Hello 인코딩 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-150">Specify hello encoding name.</span></span> |<span data-ttu-id="06744-151">유효한 인코딩 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-151">A valid encoding name.</span></span> <span data-ttu-id="06744-152">[Encoding.EncodingName 속성](https://msdn.microsoft.com/library/system.text.encoding.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06744-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="06744-153">windows-1250 또는 shift_jis 등을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="06744-154">hello **기본** 값은 **u t F-8**합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-154">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="06744-155">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-155">No</span></span> |
| <span data-ttu-id="06744-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="06744-156">firstRowAsHeader</span></span> |<span data-ttu-id="06744-157">Tooconsider 첫 번째 행을 머리글로 hello 있는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-157">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="06744-158">입력 데이터 집합의 경우 Data Factory는 첫 번째 행을 머리글로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="06744-159">출력 데이터 집합의 경우에는 첫 번째 행을 머리글로 씁니다.</span><span class="sxs-lookup"><span data-stu-id="06744-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="06744-160">샘플 시나리오의 경우 [`firstRowAsHeader` 및 `skipLineCount` 사용 시나리오](#scenarios-for-using-firstrowasheader-and-skiplinecount)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06744-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="06744-161">True</span><span class="sxs-lookup"><span data-stu-id="06744-161">True</span></span><br/><span data-ttu-id="06744-162">**False(기본값)**</span><span class="sxs-lookup"><span data-stu-id="06744-162">**False (default)**</span></span> |<span data-ttu-id="06744-163">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-163">No</span></span> |
| <span data-ttu-id="06744-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="06744-164">skipLineCount</span></span> |<span data-ttu-id="06744-165">입력된 파일에서 데이터를 읽을 때 행 tooskip hello 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="06744-165">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="06744-166">SkipLineCount과 firstRowAsHeader 모두 지정 된 경우 hello 줄은 먼저 건너뜁니다 고 hello 헤더 정보 hello 입력된 파일에서 읽은 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-166">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="06744-167">샘플 시나리오의 경우 [`firstRowAsHeader` 및 `skipLineCount` 사용 시나리오](#scenarios-for-using-firstrowasheader-and-skiplinecount)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06744-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="06744-168">Integer</span><span class="sxs-lookup"><span data-stu-id="06744-168">Integer</span></span> |<span data-ttu-id="06744-169">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-169">No</span></span> |
| <span data-ttu-id="06744-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="06744-170">treatEmptyAsNull</span></span> |<span data-ttu-id="06744-171">Tootreat null 또는 빈 문자열을 null로 최대값 여부를 지정 합니다. 입력된 파일에서 데이터를 읽고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-171">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="06744-172">**True(기본값)**</span><span class="sxs-lookup"><span data-stu-id="06744-172">**True (default)**</span></span><br/><span data-ttu-id="06744-173">False</span><span class="sxs-lookup"><span data-stu-id="06744-173">False</span></span> |<span data-ttu-id="06744-174">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="06744-175">TextFormat 예제</span><span class="sxs-lookup"><span data-stu-id="06744-175">TextFormat example</span></span>
<span data-ttu-id="06744-176">hello 다음 샘플에서는 hello 형식 속성 중 일부를 TextFormat에 대 한</span><span class="sxs-lookup"><span data-stu-id="06744-176">hello following sample shows some of hello format properties for TextFormat.</span></span>

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

<span data-ttu-id="06744-177">toouse는 `escapeChar` 대신 `quoteChar`, 대체 hello 줄을 `quoteChar` 에서는 escapeChar 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="06744-177">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="06744-178">FirstRowAsHeader 및 skipLineCount 사용 시나리오</span><span class="sxs-lookup"><span data-stu-id="06744-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="06744-179">파일이 아닌 소스 tooa 텍스트 파일에서 복사 하 고 hello 스키마 메타 데이터가 포함 된 헤더 줄 tooadd ु (예: SQL 스키마).</span><span class="sxs-lookup"><span data-stu-id="06744-179">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="06744-180">지정 `firstRowAsHeader` 이 시나리오에 대 한 hello 출력 데이터 집합에 완전 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-180">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="06744-181">헤더 줄 tooa 비파일 싱크를 포함 하는 텍스트 파일에서 복사 하는 및 줄 toodrop 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-181">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="06744-182">지정 `firstRowAsHeader` hello 입력된 데이터 집합의 완전 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-182">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="06744-183">텍스트 파일에서 복사 하는 및 tooskip 없는 데이터 나 헤더 정보가 포함 된 hello 시작 부분에 몇 줄을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-183">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="06744-184">지정 `skipLineCount` tooindicate hello 개수의 줄 toobe 건너뛰도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-184">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="06744-185">Hello 파일의 나머지 부분은 hello 포함 헤더 줄을 지정할 수도 있습니다 `firstRowAsHeader`합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-185">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="06744-186">두 `skipLineCount` 및 `firstRowAsHeader` hello 줄은 먼저 건너뜁니다 고 hello 헤더 정보 hello 입력된 파일에서 읽은 다음 지정 된</span><span class="sxs-lookup"><span data-stu-id="06744-186">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="06744-187">JsonFormat 지정</span><span class="sxs-lookup"><span data-stu-id="06744-187">Specifying JsonFormat</span></span>
<span data-ttu-id="06744-188">너무**로 JSON 파일 가져오기/내보내기-Azure Cosmos DB에서 /으로**, 참조 [가져오기/내보내기 JSON 문서](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) 세부 정보와 함께 hello Azure Cosmos DB 커넥터의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-188">too**import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in hello Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="06744-189">Tooparse hello JSON 파일 또는 JSON 형식으로 hello 데이터를 쓸 경우 설정 hello `format` `type` 속성 너무**JsonFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-189">If you want tooparse hello JSON files or write hello data in JSON format, set hello `format` `type` property too**JsonFormat**.</span></span> <span data-ttu-id="06744-190">Hello 다음을 지정할 수도 있습니다 **선택적** hello에 대 한 속성 `format` 섹션.</span><span class="sxs-lookup"><span data-stu-id="06744-190">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="06744-191">참조 [JsonFormat 예제](#jsonformat-example) 방법에 대 한 섹션 tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-191">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="06744-192">속성</span><span class="sxs-lookup"><span data-stu-id="06744-192">Property</span></span> | <span data-ttu-id="06744-193">설명</span><span class="sxs-lookup"><span data-stu-id="06744-193">Description</span></span> | <span data-ttu-id="06744-194">필수</span><span class="sxs-lookup"><span data-stu-id="06744-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06744-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="06744-195">filePattern</span></span> |<span data-ttu-id="06744-196">각 JSON 파일에 저장 된 데이터의 hello 패턴을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="06744-196">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="06744-197">사용 가능한 값은 **setOfObjects** 및 **arrayOfObjects**이고</span><span class="sxs-lookup"><span data-stu-id="06744-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="06744-198">hello **기본** 값은 **setOfObjects**합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-198">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="06744-199">이러한 패턴에 대한 자세한 내용은 [JSON 파일 패턴](#json-file-patterns) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06744-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="06744-200">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-200">No</span></span> |
| <span data-ttu-id="06744-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="06744-201">jsonNodeReference</span></span> | <span data-ttu-id="06744-202">Tooiterate을 배열 내에서 hello 개체에서 데이터를 추출 하는 경우 필드 hello로 동일한 패턴을 해당 배열의 hello JSON 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-202">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="06744-203">이 속성은 JSON 파일에서 데이터를 복사할 때만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="06744-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="06744-204">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-204">No</span></span> |
| <span data-ttu-id="06744-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="06744-205">jsonPathDefinition</span></span> | <span data-ttu-id="06744-206">각 열 매핑에 대 한 hello JSON 경로 식 (소문자로 시작)를 사용자 지정 된 열 이름으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-206">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="06744-207">이 속성은 JSON 파일에서 데이터를 복사할 때만 지원되며 개체 또는 배열에서 데이터를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="06744-208">루트 개체에서 필드에 대 한 루트 $;로 시작 필드에서 선택한 hello 배열 내에 대 한 `jsonNodeReference` 속성을 hello 배열 요소에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-208">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="06744-209">참조 [JsonFormat 예제](#jsonformat-example) 방법에 대 한 섹션 tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-209">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="06744-210">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-210">No</span></span> |
| <span data-ttu-id="06744-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="06744-211">encodingName</span></span> |<span data-ttu-id="06744-212">Hello 인코딩 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-212">Specify hello encoding name.</span></span> <span data-ttu-id="06744-213">유효한 인코딩 이름 목록은 hello, 참조: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-213">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="06744-214">예: windows-1250 또는 shift_jis</span><span class="sxs-lookup"><span data-stu-id="06744-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="06744-215">hello **기본** 값은: **u t F-8**합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-215">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="06744-216">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-216">No</span></span> |
| <span data-ttu-id="06744-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="06744-217">nestingSeparator</span></span> |<span data-ttu-id="06744-218">문자는 사용 되는 tooseparate 중첩 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-218">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="06744-219">hello 기본값은 '.' (점)입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-219">hello default value is '.' (dot).</span></span> |<span data-ttu-id="06744-220">아니요</span><span class="sxs-lookup"><span data-stu-id="06744-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="06744-221">JSON 파일 패턴</span><span class="sxs-lookup"><span data-stu-id="06744-221">JSON file patterns</span></span>

<span data-ttu-id="06744-222">복사 작업에서는 JSON 파일의 다음 패턴을 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="06744-223">**유형 I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="06744-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="06744-224">각 파일에 단일 개체 또는 줄로 구분된/연결된 여러 개체가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="06744-225">출력 데이터 집합에서 이 옵션을 선택하는 경우 복사 활동에서는 줄마다 개체가 하나씩 포함된(각 개체가 줄로 구분된) JSON 파일 하나를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="06744-226">**단일 개체 JSON 예제**</span><span class="sxs-lookup"><span data-stu-id="06744-226">**single object JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * <span data-ttu-id="06744-227">**줄로 구분된 JSON 예제**</span><span class="sxs-lookup"><span data-stu-id="06744-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="06744-228">**연결된 JSON 예제**</span><span class="sxs-lookup"><span data-stu-id="06744-228">**concatenated JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- <span data-ttu-id="06744-229">**유형 II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="06744-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="06744-230">각 파일에 개체 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="06744-230">Each file contains an array of objects.</span></span>

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

#### <a name="jsonformat-example"></a><span data-ttu-id="06744-231">JsonFormat 예제</span><span class="sxs-lookup"><span data-stu-id="06744-231">JsonFormat example</span></span>

<span data-ttu-id="06744-232">**사례 1: JSON 파일에서 데이터 복사**</span><span class="sxs-lookup"><span data-stu-id="06744-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="06744-233">JSON 파일에서 데이터를 복사할 때 두 가지 유형의 샘플 아래를 참조 하십시오 및 일반적인 포인트 toonote hello:</span><span class="sxs-lookup"><span data-stu-id="06744-233">See below two types of samples when copying data from JSON files, and hello generic points toonote:</span></span>

<span data-ttu-id="06744-234">**샘플 1: 개체 및 배열에서 데이터 추출**</span><span class="sxs-lookup"><span data-stu-id="06744-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="06744-235">이 샘플에서는 하나의 루트 JSON 개체는 테이블 형식 결과의 toosingle 레코드 매핑합니다 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-235">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="06744-236">콘텐츠를 다음 hello로 JSON 파일을 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="06744-236">If you have a JSON file with hello following content:</span></span>  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
<span data-ttu-id="06744-237">및 원하는 toocopy 개체 및 배열 둘 다에서 데이터를 추출 하 여 포맷 hello 다음에 Azure SQL 테이블에:</span><span class="sxs-lookup"><span data-stu-id="06744-237">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="06744-238">id</span><span class="sxs-lookup"><span data-stu-id="06744-238">id</span></span> | <span data-ttu-id="06744-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="06744-239">deviceType</span></span> | <span data-ttu-id="06744-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="06744-240">targetResourceType</span></span> | <span data-ttu-id="06744-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="06744-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="06744-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="06744-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="06744-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="06744-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="06744-244">PC</span><span class="sxs-lookup"><span data-stu-id="06744-244">PC</span></span> | <span data-ttu-id="06744-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="06744-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="06744-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="06744-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="06744-247">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="06744-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="06744-248">hello 입력된 데이터 집합을 **JsonFormat** 형식은 다음과 같이 정의 됩니다: (hello 관련 파트만 부분 정의).</span><span class="sxs-lookup"><span data-stu-id="06744-248">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="06744-249">더 구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-249">More specifically:</span></span>

- <span data-ttu-id="06744-250">`structure`섹션은 tootabular 데이터를 변환 하는 동안 사용자 지정 하는 hello 열 이름 및 hello 해당 데이터 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-250">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="06744-251">이 섹션은 **선택적** toodo 열 매핑이 필요 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-251">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="06744-252">자세한 내용은 [사각형 데이터 집합의 구조 정의 지정](#specifying-structure-definition-for-rectangular-datasets) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06744-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="06744-253">`jsonPathDefinition`여기서 tooextract hello 데이터를 나타내는 각 열에 대 한 hello JSON 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-253">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="06744-254">사용할 수 배열의 데이터 toocopy **배열 [x] 지 원하는** hello xth 개체의 속성을 지정 하는 hello tooextract 값 צ ְ ײ  **배열 [*] 지 원하는** toofind 이러한 속성을 포함 하는 개체 로부터 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-254">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

<span data-ttu-id="06744-255">**예제 2: 교차 적용 hello 배열에서 동일한 패턴을 사용 하 여 여러 개체**</span><span class="sxs-lookup"><span data-stu-id="06744-255">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="06744-256">이 샘플에서는 테이블 형식 결과에서 여러 레코드로 tootransform 하나의 루트 JSON 개체를 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-256">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="06744-257">콘텐츠를 다음 hello로 JSON 파일을 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="06744-257">If you have a JSON file with hello following content:</span></span>  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
<span data-ttu-id="06744-258">및 hello hello 배열 내에서 데이터를 병합 하 여 포맷 hello 다음에 Azure SQL 테이블에 toocopy을 크로스 조인 공용 루트 정보 hello로:</span><span class="sxs-lookup"><span data-stu-id="06744-258">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="06744-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="06744-259">ordernumber</span></span> | <span data-ttu-id="06744-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="06744-260">orderdate</span></span> | <span data-ttu-id="06744-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="06744-261">order_pd</span></span> | <span data-ttu-id="06744-262">order_price</span><span class="sxs-lookup"><span data-stu-id="06744-262">order_price</span></span> | <span data-ttu-id="06744-263">city</span><span class="sxs-lookup"><span data-stu-id="06744-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="06744-264">01</span><span class="sxs-lookup"><span data-stu-id="06744-264">01</span></span> | <span data-ttu-id="06744-265">20170122</span><span class="sxs-lookup"><span data-stu-id="06744-265">20170122</span></span> | <span data-ttu-id="06744-266">P1</span><span class="sxs-lookup"><span data-stu-id="06744-266">P1</span></span> | <span data-ttu-id="06744-267">23</span><span class="sxs-lookup"><span data-stu-id="06744-267">23</span></span> | <span data-ttu-id="06744-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="06744-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="06744-269">01</span><span class="sxs-lookup"><span data-stu-id="06744-269">01</span></span> | <span data-ttu-id="06744-270">20170122</span><span class="sxs-lookup"><span data-stu-id="06744-270">20170122</span></span> | <span data-ttu-id="06744-271">P2</span><span class="sxs-lookup"><span data-stu-id="06744-271">P2</span></span> | <span data-ttu-id="06744-272">13</span><span class="sxs-lookup"><span data-stu-id="06744-272">13</span></span> | <span data-ttu-id="06744-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="06744-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="06744-274">01</span><span class="sxs-lookup"><span data-stu-id="06744-274">01</span></span> | <span data-ttu-id="06744-275">20170122</span><span class="sxs-lookup"><span data-stu-id="06744-275">20170122</span></span> | <span data-ttu-id="06744-276">P3</span><span class="sxs-lookup"><span data-stu-id="06744-276">P3</span></span> | <span data-ttu-id="06744-277">231</span><span class="sxs-lookup"><span data-stu-id="06744-277">231</span></span> | <span data-ttu-id="06744-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="06744-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="06744-279">hello 입력된 데이터 집합을 **JsonFormat** 형식은 다음과 같이 정의 됩니다: (hello 관련 파트만 부분 정의).</span><span class="sxs-lookup"><span data-stu-id="06744-279">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="06744-280">더 구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-280">More specifically:</span></span>

- <span data-ttu-id="06744-281">`structure`섹션은 tootabular 데이터를 변환 하는 동안 사용자 지정 하는 hello 열 이름 및 hello 해당 데이터 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-281">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="06744-282">이 섹션은 **선택적** toodo 열 매핑이 필요 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-282">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="06744-283">자세한 내용은 [사각형 데이터 집합의 구조 정의 지정](#specifying-structure-definition-for-rectangular-datasets) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06744-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="06744-284">`jsonNodeReference`hello에서 같은 패턴을 사용 하 여 hello 개체에서 데이터를 tooiterate 및 추출 나타냅니다 **배열** orderlines 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-284">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="06744-285">`jsonPathDefinition`여기서 tooextract hello 데이터를 나타내는 각 열에 대 한 hello JSON 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-285">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="06744-286">이 예제에서는 "ordernumber", "orderdate" 및 "city"가 루트 개체에서 "$" 하지 않고 hello 배열 요소에서 파생 된 경로로 정의 되지만 "order_pd" 및 "order_price" "$."로 시작 하는 JSON 경로.</span><span class="sxs-lookup"><span data-stu-id="06744-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

<span data-ttu-id="06744-287">**포인트 다음 참고 hello:**</span><span class="sxs-lookup"><span data-stu-id="06744-287">**Note hello following points:**</span></span>

* <span data-ttu-id="06744-288">경우 hello `structure` 및 `jsonPathDefinition` 정의 되어 있지 않은 hello Data Factory 데이터 집합에 hello 복사 작업에서 hello hello 첫 번째 개체에서 스키마 및 병합 된 hello 전체 개체를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-288">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="06744-289">Hello JSON 입력 배열에 있는 경우 기본적으로 hello 복사 활동 hello 전체 배열 값을 문자열로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-289">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="06744-290">사용 하 여 tooextract 데이터를 선택할 수 있습니다 `jsonNodeReference` 및/또는 `jsonPathDefinition`에서 지정 하 여 건너뛸 또는 `jsonPathDefinition`합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-290">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="06744-291">가 중복 이름에 같은 수준 hello, hello 복사 작업은 마지막 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-291">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="06744-292">속성 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-292">Property names are case-sensitive.</span></span> <span data-ttu-id="06744-293">이름은 같지만 대/소문자가 다른 두 속성은 별도의 두 속성으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="06744-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="06744-294">**사례 2: 데이터 tooJSON 파일 쓰기**</span><span class="sxs-lookup"><span data-stu-id="06744-294">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="06744-295">SQL Database에 아래 테이블이 있고</span><span class="sxs-lookup"><span data-stu-id="06744-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="06744-296">id</span><span class="sxs-lookup"><span data-stu-id="06744-296">id</span></span> | <span data-ttu-id="06744-297">order_date</span><span class="sxs-lookup"><span data-stu-id="06744-297">order_date</span></span> | <span data-ttu-id="06744-298">order_price</span><span class="sxs-lookup"><span data-stu-id="06744-298">order_price</span></span> | <span data-ttu-id="06744-299">order_by</span><span class="sxs-lookup"><span data-stu-id="06744-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="06744-300">1</span><span class="sxs-lookup"><span data-stu-id="06744-300">1</span></span> | <span data-ttu-id="06744-301">20170119</span><span class="sxs-lookup"><span data-stu-id="06744-301">20170119</span></span> | <span data-ttu-id="06744-302">2000</span><span class="sxs-lookup"><span data-stu-id="06744-302">2000</span></span> | <span data-ttu-id="06744-303">David</span><span class="sxs-lookup"><span data-stu-id="06744-303">David</span></span> |
| <span data-ttu-id="06744-304">2</span><span class="sxs-lookup"><span data-stu-id="06744-304">2</span></span> | <span data-ttu-id="06744-305">20170120</span><span class="sxs-lookup"><span data-stu-id="06744-305">20170120</span></span> | <span data-ttu-id="06744-306">3500</span><span class="sxs-lookup"><span data-stu-id="06744-306">3500</span></span> | <span data-ttu-id="06744-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="06744-307">Patrick</span></span> |
| <span data-ttu-id="06744-308">3</span><span class="sxs-lookup"><span data-stu-id="06744-308">3</span></span> | <span data-ttu-id="06744-309">20170121</span><span class="sxs-lookup"><span data-stu-id="06744-309">20170121</span></span> | <span data-ttu-id="06744-310">4000</span><span class="sxs-lookup"><span data-stu-id="06744-310">4000</span></span> | <span data-ttu-id="06744-311">Jason</span><span class="sxs-lookup"><span data-stu-id="06744-311">Jason</span></span> |

<span data-ttu-id="06744-312">및 원하는 형식 아래 toowrite tooa JSON 개체에서 각 레코드에 대해:</span><span class="sxs-lookup"><span data-stu-id="06744-312">and for each record, you expect toowrite tooa JSON object in below format:</span></span>
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

<span data-ttu-id="06744-313">hello 출력 데이터 집합으로 **JsonFormat** 형식은 다음과 같이 정의 됩니다: (hello 관련 파트만 부분 정의).</span><span class="sxs-lookup"><span data-stu-id="06744-313">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="06744-314">보다 구체적으로, `structure` 대상 파일에 사용자 지정 하는 hello 속성 이름을 정의 하는 섹션 `nestingSeparator` (기본값은 ".") hello 이름에서 사용 되는 tooidentify hello 중첩 레이어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06744-314">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") will be used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="06744-315">이 섹션은 **선택적** toochange hello 속성 이름을 원본 열 이름과 비교 하거나 hello 속성 중 일부를 중첩 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-315">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

### <a name="specifying-avroformat"></a><span data-ttu-id="06744-316">AvroFormat 지정</span><span class="sxs-lookup"><span data-stu-id="06744-316">Specifying AvroFormat</span></span>
<span data-ttu-id="06744-317">Tooparse hello Avro 파일 또는 Avro 형식에서 hello 데이터를 작성 하는 경우 설정 hello `format` `type` 속성 너무**AvroFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-317">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="06744-318">Toospecify 필요 하지 않습니다 hello typeProperties 섹션 내에서 hello 형식 섹션에서 모든 속성.</span><span class="sxs-lookup"><span data-stu-id="06744-318">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="06744-319">예제:</span><span class="sxs-lookup"><span data-stu-id="06744-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="06744-320">toouse Hive 테이블에서 Avro 형식으로 참조할 수 있습니다 너무[Apache Hive 자습서](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe)합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-320">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="06744-321">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="06744-321">Note hello following points:</span></span>  

* <span data-ttu-id="06744-322">[복합 데이터 형식](http://avro.apache.org/docs/current/spec.html#schema_complex)은 지원되지 않습니다(레코드, 열거형, 배열, 매핑, 공용 구조체 및 고정).</span><span class="sxs-lookup"><span data-stu-id="06744-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="06744-323">OrcFormat 지정</span><span class="sxs-lookup"><span data-stu-id="06744-323">Specifying OrcFormat</span></span>
<span data-ttu-id="06744-324">Tooparse hello ORC 파일 형식 ORC hello 데이터를 쓸 경우 설정 hello `format` `type` 속성 너무**OrcFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-324">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="06744-325">Toospecify 필요 하지 않습니다 hello typeProperties 섹션 내에서 hello 형식 섹션에서 모든 속성.</span><span class="sxs-lookup"><span data-stu-id="06744-325">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="06744-326">예제:</span><span class="sxs-lookup"><span data-stu-id="06744-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="06744-327">ORC 파일을 복사 하지는 **으로-는** 온-프레미스와 클라우드 사이 데이터 저장소, tooinstall hello 8 JRE (Java Runtime Environment) 게이트웨이 컴퓨터에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="06744-328">64비트 게이트웨이에는 64비트 JRE가 필요하고 32비트 게이트웨이에는 32비트 JRE가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="06744-329">[여기서](http://go.microsoft.com/fwlink/?LinkId=808605)두 버전이 모두 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="06744-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="06744-330">적절 한 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-330">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="06744-331">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="06744-331">Note hello following points:</span></span>

* <span data-ttu-id="06744-332">복합 데이터 형식(구조체, 맵, 목록, 공용 구조체)은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="06744-333">ORC 파일에는 3개의 [압축 관련 옵션](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/)(NONE, ZLIB, SNAPPY)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="06744-334">Data Factory에서는 이러한 압축 형식으로 된 데이터를 ORC 파일에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="06744-335">Hello 압축을 사용 하 여 코덱은 hello 메타 데이터 tooread hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-335">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="06744-336">그러나 tooan ORC 파일을 작성할 때 데이터 팩터리 선택 ZLIB, ORC에 대 한 hello 기본값 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-336">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="06744-337">현재,이 없는 옵션 toooverride이이 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-337">Currently, there is no option toooverride this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="06744-338">ParquetFormat 지정</span><span class="sxs-lookup"><span data-stu-id="06744-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="06744-339">Tooparse hello Parquet 파일 형식 Parquet hello 데이터를 쓸 경우 설정 hello `format` `type` 속성 너무**ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-339">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="06744-340">Toospecify 필요 하지 않습니다 hello typeProperties 섹션 내에서 hello 형식 섹션에서 모든 속성.</span><span class="sxs-lookup"><span data-stu-id="06744-340">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="06744-341">예제:</span><span class="sxs-lookup"><span data-stu-id="06744-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="06744-342">Parquet 파일을 복사 하지는 **으로-는** 온-프레미스와 클라우드 사이 데이터 저장소, tooinstall hello 8 JRE (Java Runtime Environment) 게이트웨이 컴퓨터에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="06744-343">64비트 게이트웨이에는 64비트 JRE가 필요하고 32비트 게이트웨이에는 32비트 JRE가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="06744-344">[여기서](http://go.microsoft.com/fwlink/?LinkId=808605)두 버전이 모두 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="06744-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="06744-345">적절 한 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-345">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="06744-346">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="06744-346">Note hello following points:</span></span>

* <span data-ttu-id="06744-347">복합 데이터 형식(MAP, LIST)은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="06744-348">Parquet 파일에 다음 압축 관련 옵션 hello: NONE, SNAPPY, GZIP, 및 LZO 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-348">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="06744-349">Data Factory에서는 이러한 압축 형식으로 된 데이터를 ORC 파일에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06744-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="06744-350">Hello 압축 코덱 hello 메타 데이터 tooread hello 데이터에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-350">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="06744-351">그러나 tooa Parquet 파일을 작성할 때 데이터 팩터리 선택 SNAPPY, Parquet 형식에 대 한 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="06744-351">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="06744-352">현재,이 없는 옵션 toooverride이이 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="06744-352">Currently, there is no option toooverride this behavior.</span></span>
