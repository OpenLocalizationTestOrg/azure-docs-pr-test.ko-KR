---
title: "Azure 데이터 팩터리에서 aaaFile 및 압축 형식 | Microsoft Docs"
description: "Azure Data Factory에서 지 원하는 hello 파일 형식에 알아봅니다."
keywords: "Blob 데이터, Azure Blob 복사"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="04efb-104">Azure Data Factory에서 지원하는 파일 및 압축 형식</span><span class="sxs-lookup"><span data-stu-id="04efb-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="04efb-105">*이 항목은 다음 커넥터 toohello 적용 됩니다.: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure 데이터 레이크 저장소](data-factory-azure-datalake-connector.md), [파일 시스템](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), 및 [SFTP](data-factory-sftp-connector.md)합니다.*</span><span class="sxs-lookup"><span data-stu-id="04efb-105">*This topic applies toohello following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="04efb-106">Azure Data Factory hello 다음 파일 형식 유형을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-106">Azure Data Factory supports hello following file format types:</span></span>

* [<span data-ttu-id="04efb-107">텍스트 형식</span><span class="sxs-lookup"><span data-stu-id="04efb-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="04efb-108">JSON 형식</span><span class="sxs-lookup"><span data-stu-id="04efb-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="04efb-109">Avro 형식</span><span class="sxs-lookup"><span data-stu-id="04efb-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="04efb-110">ORC 형식</span><span class="sxs-lookup"><span data-stu-id="04efb-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="04efb-111">Parquet 형식</span><span class="sxs-lookup"><span data-stu-id="04efb-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="04efb-112">텍스트 형식</span><span class="sxs-lookup"><span data-stu-id="04efb-112">Text format</span></span>
<span data-ttu-id="04efb-113">텍스트 파일에서 tooread를 싶거나 tooa 텍스트 파일 쓰기 설정 hello `type` hello에 대 한 속성 `format` hello 데이터 집합의 섹션 너무**TextFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-113">If you want tooread from a text file or write tooa text file, set hello `type` property in hello `format` section of hello dataset too**TextFormat**.</span></span> <span data-ttu-id="04efb-114">Hello 다음을 지정할 수도 있습니다 **선택적** hello에 대 한 속성 `format` 섹션.</span><span class="sxs-lookup"><span data-stu-id="04efb-114">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="04efb-115">참조 [TextFormat 예제](#textformat-example) 방법에 대 한 섹션 tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-115">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="04efb-116">속성</span><span class="sxs-lookup"><span data-stu-id="04efb-116">Property</span></span> | <span data-ttu-id="04efb-117">설명</span><span class="sxs-lookup"><span data-stu-id="04efb-117">Description</span></span> | <span data-ttu-id="04efb-118">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="04efb-118">Allowed values</span></span> | <span data-ttu-id="04efb-119">필수</span><span class="sxs-lookup"><span data-stu-id="04efb-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="04efb-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="04efb-120">columnDelimiter</span></span> |<span data-ttu-id="04efb-121">hello 문자는 파일에 tooseparate 열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-121">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="04efb-122">데이터의 확률이 높습니다 않은 드문 인쇄할 수 없는 char 존재 toouse를 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-122">You can consider toouse a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="04efb-123">예를 들어 헤딩의 시작(SOH)을 나타내는 "\u0001"을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="04efb-124">문자는 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-124">Only one character is allowed.</span></span> <span data-ttu-id="04efb-125">hello **기본** 값은 **쉼표 (',')**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-125">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="04efb-126">유니코드 문자를 toouse 너무 참조[유니코드 문자](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget에 해당 하는 코드를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-126">toouse a Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="04efb-127">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-127">No</span></span> |
| <span data-ttu-id="04efb-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="04efb-128">rowDelimiter</span></span> |<span data-ttu-id="04efb-129">hello 문자는 파일에 tooseparate 행을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-129">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="04efb-130">문자는 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-130">Only one character is allowed.</span></span> <span data-ttu-id="04efb-131">hello **기본** 값은 hello 읽기의 다음 값 중 하나: **["\r\n", "\r", "\n"]** 및 **"\r\n"** 쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-131">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="04efb-132">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-132">No</span></span> |
| <span data-ttu-id="04efb-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="04efb-133">escapeChar</span></span> |<span data-ttu-id="04efb-134">입력된 파일의 hello 내용 tooescape 열 구분 기호를 사용 하는 hello 특수 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-134">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="04efb-135">한 테이블에 대해 escapeChar 및 quoteChar을 둘 다 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="04efb-136">문자는 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-136">Only one character is allowed.</span></span> <span data-ttu-id="04efb-137">기본값은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-137">No default value.</span></span> <br/><br/><span data-ttu-id="04efb-138">예: 쉼표 있는 경우 (', ') toohave hello 쉼표 문자 hello 텍스트에는 원하는 수 있지만 hello 열 구분 기호 (예: "Hello, world"), '$' hello 이스케이프 문자로 정의 하 고 문자열을 사용할 수 "Hello$, world" hello 소스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-138">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="04efb-139">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-139">No</span></span> |
| <span data-ttu-id="04efb-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="04efb-140">quoteChar</span></span> |<span data-ttu-id="04efb-141">hello 문자 tooquote는 문자열 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-141">hello character used tooquote a string value.</span></span> <span data-ttu-id="04efb-142">hello 열 및 행 구분 기호 hello 인용 문자 내 hello 문자열 값의 일부분으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-142">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="04efb-143">이 속성은 적용 가능한 tooboth 입력 및 데이터 집합을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-143">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="04efb-144">한 테이블에 대해 escapeChar 및 quoteChar을 둘 다 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="04efb-145">문자는 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-145">Only one character is allowed.</span></span> <span data-ttu-id="04efb-146">기본값은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-146">No default value.</span></span> <br/><br/><span data-ttu-id="04efb-147">예를 들어, 쉼표가 있는 경우 (', ') hello 열 구분 기호 있지만 hello 텍스트에 쉼표 문자 toohave 원하는 만큼 (예: < Hello, world >), 정의할 수 있습니다 "(큰따옴표) hello 인용 문자 및 문자열 hello를 사용 하 여"Hello, world"hello 소스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-147">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="04efb-148">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-148">No</span></span> |
| <span data-ttu-id="04efb-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="04efb-149">nullValue</span></span> |<span data-ttu-id="04efb-150">하나 이상의 문자 toorepresent null 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-150">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="04efb-151">하나 이상의 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-151">One or more characters.</span></span> <span data-ttu-id="04efb-152">hello **기본** 값은 **"\N" 및 "NULL"** 읽기 및 **"\N"** 쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-152">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="04efb-153">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-153">No</span></span> |
| <span data-ttu-id="04efb-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="04efb-154">encodingName</span></span> |<span data-ttu-id="04efb-155">Hello 인코딩 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-155">Specify hello encoding name.</span></span> |<span data-ttu-id="04efb-156">유효한 인코딩 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-156">A valid encoding name.</span></span> <span data-ttu-id="04efb-157">[Encoding.EncodingName 속성](https://msdn.microsoft.com/library/system.text.encoding.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04efb-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="04efb-158">windows-1250 또는 shift_jis 등을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="04efb-159">hello **기본** 값은 **u t F-8**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-159">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="04efb-160">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-160">No</span></span> |
| <span data-ttu-id="04efb-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="04efb-161">firstRowAsHeader</span></span> |<span data-ttu-id="04efb-162">Tooconsider 첫 번째 행을 머리글로 hello 있는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-162">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="04efb-163">입력 데이터 집합의 경우 Data Factory는 첫 번째 행을 머리글로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="04efb-164">출력 데이터 집합의 경우에는 첫 번째 행을 머리글로 씁니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="04efb-165">샘플 시나리오의 경우 [`firstRowAsHeader` 및 `skipLineCount` 사용 시나리오](#scenarios-for-using-firstrowasheader-and-skiplinecount)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04efb-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="04efb-166">True</span><span class="sxs-lookup"><span data-stu-id="04efb-166">True</span></span><br/><span data-ttu-id="04efb-167"><b>False(기본값)</b></span><span class="sxs-lookup"><span data-stu-id="04efb-167"><b>False (default)</b></span></span> |<span data-ttu-id="04efb-168">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-168">No</span></span> |
| <span data-ttu-id="04efb-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="04efb-169">skipLineCount</span></span> |<span data-ttu-id="04efb-170">입력된 파일에서 데이터를 읽을 때 행 tooskip hello 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-170">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="04efb-171">SkipLineCount과 firstRowAsHeader 모두 지정 된 경우 hello 줄은 먼저 건너뜁니다 고 hello 헤더 정보 hello 입력된 파일에서 읽은 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-171">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="04efb-172">샘플 시나리오의 경우 [`firstRowAsHeader` 및 `skipLineCount` 사용 시나리오](#scenarios-for-using-firstrowasheader-and-skiplinecount)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04efb-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="04efb-173">Integer</span><span class="sxs-lookup"><span data-stu-id="04efb-173">Integer</span></span> |<span data-ttu-id="04efb-174">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-174">No</span></span> |
| <span data-ttu-id="04efb-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="04efb-175">treatEmptyAsNull</span></span> |<span data-ttu-id="04efb-176">Tootreat null 또는 빈 문자열을 null로 최대값 여부를 지정 합니다. 입력된 파일에서 데이터를 읽고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-176">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="04efb-177">**True(기본값)**</span><span class="sxs-lookup"><span data-stu-id="04efb-177">**True (default)**</span></span><br/><span data-ttu-id="04efb-178">False</span><span class="sxs-lookup"><span data-stu-id="04efb-178">False</span></span> |<span data-ttu-id="04efb-179">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="04efb-180">TextFormat 예제</span><span class="sxs-lookup"><span data-stu-id="04efb-180">TextFormat example</span></span>
<span data-ttu-id="04efb-181">다음 데이터 집합에 대 한 JSON 정의 hello, 일부 hello 선택적 속성 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-181">In hello following JSON definition for a dataset, some of hello optional properties are specified.</span></span>

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

<span data-ttu-id="04efb-182">toouse는 `escapeChar` 대신 `quoteChar`, 대체 hello 줄을 `quoteChar` 에서는 escapeChar 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="04efb-182">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="04efb-183">FirstRowAsHeader 및 skipLineCount 사용 시나리오</span><span class="sxs-lookup"><span data-stu-id="04efb-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="04efb-184">파일이 아닌 소스 tooa 텍스트 파일에서 복사 하 고 hello 스키마 메타 데이터가 포함 된 헤더 줄 tooadd ु (예: SQL 스키마).</span><span class="sxs-lookup"><span data-stu-id="04efb-184">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="04efb-185">지정 `firstRowAsHeader` 이 시나리오에 대 한 hello 출력 데이터 집합에 완전 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-185">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="04efb-186">헤더 줄 tooa 비파일 싱크를 포함 하는 텍스트 파일에서 복사 하는 및 줄 toodrop 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-186">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="04efb-187">지정 `firstRowAsHeader` hello 입력된 데이터 집합의 완전 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-187">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="04efb-188">텍스트 파일에서 복사 하는 및 tooskip 없는 데이터 나 헤더 정보가 포함 된 hello 시작 부분에 몇 줄을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-188">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="04efb-189">지정 `skipLineCount` tooindicate hello 개수의 줄 toobe 건너뛰도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-189">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="04efb-190">Hello 파일의 나머지 부분은 hello 포함 헤더 줄을 지정할 수도 있습니다 `firstRowAsHeader`합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-190">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="04efb-191">두 `skipLineCount` 및 `firstRowAsHeader` hello 줄은 먼저 건너뜁니다 고 hello 헤더 정보 hello 입력된 파일에서 읽은 다음 지정 된</span><span class="sxs-lookup"><span data-stu-id="04efb-191">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

## <a name="json-format"></a><span data-ttu-id="04efb-192">JSON 형식</span><span class="sxs-lookup"><span data-stu-id="04efb-192">JSON format</span></span>
<span data-ttu-id="04efb-193">너무**로 JSON 파일 가져오기/내보내기-Azure Cosmos DB에서 /으로**, hello 참조 [가져오기/내보내기 JSON 문서](data-factory-azure-documentdb-connector.md#importexport-json-documents) 섹션 [/Azure Cosmos DB에서 데이터를 이동](data-factory-azure-documentdb-connector.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="04efb-193">too**import/export a JSON file as-is into/from Azure Cosmos DB**, hello see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="04efb-194">Tooparse hello JSON 파일 또는 JSON 형식으로 hello 데이터를 쓸 경우 설정 hello `type` hello에 대 한 속성 `format` 너무 섹션**JsonFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-194">If you want tooparse hello JSON files or write hello data in JSON format, set hello `type` property in hello `format` section too**JsonFormat**.</span></span> <span data-ttu-id="04efb-195">Hello 다음을 지정할 수도 있습니다 **선택적** hello에 대 한 속성 `format` 섹션.</span><span class="sxs-lookup"><span data-stu-id="04efb-195">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="04efb-196">참조 [JsonFormat 예제](#jsonformat-example) 방법에 대 한 섹션 tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-196">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="04efb-197">속성</span><span class="sxs-lookup"><span data-stu-id="04efb-197">Property</span></span> | <span data-ttu-id="04efb-198">설명</span><span class="sxs-lookup"><span data-stu-id="04efb-198">Description</span></span> | <span data-ttu-id="04efb-199">필수</span><span class="sxs-lookup"><span data-stu-id="04efb-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04efb-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="04efb-200">filePattern</span></span> |<span data-ttu-id="04efb-201">각 JSON 파일에 저장 된 데이터의 hello 패턴을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-201">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="04efb-202">사용 가능한 값은 **setOfObjects** 및 **arrayOfObjects**이고</span><span class="sxs-lookup"><span data-stu-id="04efb-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="04efb-203">hello **기본** 값은 **setOfObjects**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-203">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="04efb-204">이러한 패턴에 대한 자세한 내용은 [JSON 파일 패턴](#json-file-patterns) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04efb-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="04efb-205">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-205">No</span></span> |
| <span data-ttu-id="04efb-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="04efb-206">jsonNodeReference</span></span> | <span data-ttu-id="04efb-207">Tooiterate을 배열 내에서 hello 개체에서 데이터를 추출 하는 경우 필드 hello로 동일한 패턴을 해당 배열의 hello JSON 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-207">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="04efb-208">이 속성은 JSON 파일에서 데이터를 복사할 때만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="04efb-209">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-209">No</span></span> |
| <span data-ttu-id="04efb-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="04efb-210">jsonPathDefinition</span></span> | <span data-ttu-id="04efb-211">각 열 매핑에 대 한 hello JSON 경로 식 (소문자로 시작)를 사용자 지정 된 열 이름으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-211">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="04efb-212">이 속성은 JSON 파일에서 데이터를 복사할 때만 지원되며 개체 또는 배열에서 데이터를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="04efb-213">루트 개체에서 필드에 대 한 루트 $;로 시작 필드에서 선택한 hello 배열 내에 대 한 `jsonNodeReference` 속성을 hello 배열 요소에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-213">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="04efb-214">참조 [JsonFormat 예제](#jsonformat-example) 방법에 대 한 섹션 tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-214">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="04efb-215">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-215">No</span></span> |
| <span data-ttu-id="04efb-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="04efb-216">encodingName</span></span> |<span data-ttu-id="04efb-217">Hello 인코딩 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-217">Specify hello encoding name.</span></span> <span data-ttu-id="04efb-218">유효한 인코딩 이름 목록은 hello, 참조: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-218">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="04efb-219">예: windows-1250 또는 shift_jis</span><span class="sxs-lookup"><span data-stu-id="04efb-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="04efb-220">hello **기본** 값은: **u t F-8**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-220">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="04efb-221">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-221">No</span></span> |
| <span data-ttu-id="04efb-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="04efb-222">nestingSeparator</span></span> |<span data-ttu-id="04efb-223">문자는 사용 되는 tooseparate 중첩 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-223">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="04efb-224">hello 기본값은 '.' (점)입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-224">hello default value is '.' (dot).</span></span> |<span data-ttu-id="04efb-225">아니요</span><span class="sxs-lookup"><span data-stu-id="04efb-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="04efb-226">JSON 파일 패턴</span><span class="sxs-lookup"><span data-stu-id="04efb-226">JSON file patterns</span></span>

<span data-ttu-id="04efb-227">복사 작업에는 hello JSON 파일의 패턴을 따르는 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-227">Copy activity can parse hello following patterns of JSON files:</span></span>

- <span data-ttu-id="04efb-228">**유형 I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="04efb-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="04efb-229">각 파일에 단일 개체 또는 줄로 구분된/연결된 여러 개체가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="04efb-230">출력 데이터 집합에서 이 옵션을 선택하는 경우 복사 활동에서는 줄마다 개체가 하나씩 포함된(각 개체가 줄로 구분된) JSON 파일 하나를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="04efb-231">**단일 개체 JSON 예제**</span><span class="sxs-lookup"><span data-stu-id="04efb-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="04efb-232">**줄로 구분된 JSON 예제**</span><span class="sxs-lookup"><span data-stu-id="04efb-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="04efb-233">**연결된 JSON 예제**</span><span class="sxs-lookup"><span data-stu-id="04efb-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="04efb-234">**유형 II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="04efb-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="04efb-235">각 파일에 개체 배열이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="04efb-236">JsonFormat 예제</span><span class="sxs-lookup"><span data-stu-id="04efb-236">JsonFormat example</span></span>

<span data-ttu-id="04efb-237">**사례 1: JSON 파일에서 데이터 복사**</span><span class="sxs-lookup"><span data-stu-id="04efb-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="04efb-238">Hello 두 개의 샘플 JSON 파일에서 데이터를 복사 하는 경우 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="04efb-238">See hello following two samples when copying data from JSON files.</span></span> <span data-ttu-id="04efb-239">일반적인 포인트 toonote hello:</span><span class="sxs-lookup"><span data-stu-id="04efb-239">hello generic points toonote:</span></span>

<span data-ttu-id="04efb-240">**샘플 1: 개체 및 배열에서 데이터 추출**</span><span class="sxs-lookup"><span data-stu-id="04efb-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="04efb-241">이 샘플에서는 하나의 루트 JSON 개체는 테이블 형식 결과의 toosingle 레코드 매핑합니다 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-241">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="04efb-242">콘텐츠를 다음 hello로 JSON 파일을 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-242">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="04efb-243">및 원하는 toocopy 개체 및 배열 둘 다에서 데이터를 추출 하 여 포맷 hello 다음에 Azure SQL 테이블에:</span><span class="sxs-lookup"><span data-stu-id="04efb-243">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="04efb-244">id</span><span class="sxs-lookup"><span data-stu-id="04efb-244">id</span></span> | <span data-ttu-id="04efb-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="04efb-245">deviceType</span></span> | <span data-ttu-id="04efb-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="04efb-246">targetResourceType</span></span> | <span data-ttu-id="04efb-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="04efb-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="04efb-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="04efb-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="04efb-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="04efb-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="04efb-250">PC</span><span class="sxs-lookup"><span data-stu-id="04efb-250">PC</span></span> | <span data-ttu-id="04efb-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="04efb-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="04efb-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="04efb-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="04efb-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="04efb-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="04efb-254">hello 입력된 데이터 집합을 **JsonFormat** 형식은 다음과 같이 정의 됩니다: (hello 관련 파트만 부분 정의).</span><span class="sxs-lookup"><span data-stu-id="04efb-254">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="04efb-255">더 구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-255">More specifically:</span></span>

- <span data-ttu-id="04efb-256">`structure`섹션은 tootabular 데이터를 변환 하는 동안 사용자 지정 하는 hello 열 이름 및 hello 해당 데이터 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-256">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="04efb-257">이 섹션은 **선택적** toodo 열 매핑이 필요 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-257">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="04efb-258">참조 [원본 데이터 집합 열 toodestination 데이터 집합 열 매핑](data-factory-map-columns.md) 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="04efb-258">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="04efb-259">`jsonPathDefinition`여기서 tooextract hello 데이터를 나타내는 각 열에 대 한 hello JSON 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-259">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="04efb-260">사용할 수 배열의 데이터 toocopy **배열 [x] 지 원하는** hello xth 개체의 속성을 지정 하는 hello tooextract 값 צ ְ ײ  **배열 [*] 지 원하는** toofind 이러한 속성을 포함 하는 개체 로부터 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-260">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="04efb-261">**예제 2: 교차 적용 hello 배열에서 동일한 패턴을 사용 하 여 여러 개체**</span><span class="sxs-lookup"><span data-stu-id="04efb-261">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="04efb-262">이 샘플에서는 테이블 형식 결과에서 여러 레코드로 tootransform 하나의 루트 JSON 개체를 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-262">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="04efb-263">콘텐츠를 다음 hello로 JSON 파일을 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-263">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="04efb-264">및 hello hello 배열 내에서 데이터를 병합 하 여 포맷 hello 다음에 Azure SQL 테이블에 toocopy을 크로스 조인 공용 루트 정보 hello로:</span><span class="sxs-lookup"><span data-stu-id="04efb-264">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="04efb-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="04efb-265">ordernumber</span></span> | <span data-ttu-id="04efb-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="04efb-266">orderdate</span></span> | <span data-ttu-id="04efb-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="04efb-267">order_pd</span></span> | <span data-ttu-id="04efb-268">order_price</span><span class="sxs-lookup"><span data-stu-id="04efb-268">order_price</span></span> | <span data-ttu-id="04efb-269">city</span><span class="sxs-lookup"><span data-stu-id="04efb-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="04efb-270">01</span><span class="sxs-lookup"><span data-stu-id="04efb-270">01</span></span> | <span data-ttu-id="04efb-271">20170122</span><span class="sxs-lookup"><span data-stu-id="04efb-271">20170122</span></span> | <span data-ttu-id="04efb-272">P1</span><span class="sxs-lookup"><span data-stu-id="04efb-272">P1</span></span> | <span data-ttu-id="04efb-273">23</span><span class="sxs-lookup"><span data-stu-id="04efb-273">23</span></span> | <span data-ttu-id="04efb-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="04efb-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="04efb-275">01</span><span class="sxs-lookup"><span data-stu-id="04efb-275">01</span></span> | <span data-ttu-id="04efb-276">20170122</span><span class="sxs-lookup"><span data-stu-id="04efb-276">20170122</span></span> | <span data-ttu-id="04efb-277">P2</span><span class="sxs-lookup"><span data-stu-id="04efb-277">P2</span></span> | <span data-ttu-id="04efb-278">13</span><span class="sxs-lookup"><span data-stu-id="04efb-278">13</span></span> | <span data-ttu-id="04efb-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="04efb-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="04efb-280">01</span><span class="sxs-lookup"><span data-stu-id="04efb-280">01</span></span> | <span data-ttu-id="04efb-281">20170122</span><span class="sxs-lookup"><span data-stu-id="04efb-281">20170122</span></span> | <span data-ttu-id="04efb-282">P3</span><span class="sxs-lookup"><span data-stu-id="04efb-282">P3</span></span> | <span data-ttu-id="04efb-283">231</span><span class="sxs-lookup"><span data-stu-id="04efb-283">231</span></span> | <span data-ttu-id="04efb-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="04efb-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="04efb-285">hello 입력된 데이터 집합을 **JsonFormat** 형식은 다음과 같이 정의 됩니다: (hello 관련 파트만 부분 정의).</span><span class="sxs-lookup"><span data-stu-id="04efb-285">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="04efb-286">더 구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-286">More specifically:</span></span>

- <span data-ttu-id="04efb-287">`structure`섹션은 tootabular 데이터를 변환 하는 동안 사용자 지정 하는 hello 열 이름 및 hello 해당 데이터 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-287">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="04efb-288">이 섹션은 **선택적** toodo 열 매핑이 필요 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-288">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="04efb-289">참조 [원본 데이터 집합 열 toodestination 데이터 집합 열 매핑](data-factory-map-columns.md) 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="04efb-289">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="04efb-290">`jsonNodeReference`hello에서 같은 패턴을 사용 하 여 hello 개체에서 데이터를 tooiterate 및 추출 나타냅니다 **배열** orderlines 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-290">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="04efb-291">`jsonPathDefinition`여기서 tooextract hello 데이터를 나타내는 각 열에 대 한 hello JSON 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-291">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="04efb-292">이 예제에서는 "ordernumber", "orderdate" 및 "city"가 루트 개체에서 "$" 하지 않고 hello 배열 요소에서 파생 된 경로로 정의 되지만 "order_pd" 및 "order_price" "$."로 시작 하는 JSON 경로.</span><span class="sxs-lookup"><span data-stu-id="04efb-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="04efb-293">**포인트 다음 참고 hello:**</span><span class="sxs-lookup"><span data-stu-id="04efb-293">**Note hello following points:**</span></span>

* <span data-ttu-id="04efb-294">경우 hello `structure` 및 `jsonPathDefinition` 정의 되어 있지 않은 hello Data Factory 데이터 집합에 hello 복사 작업에서 hello hello 첫 번째 개체에서 스키마 및 병합 된 hello 전체 개체를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-294">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="04efb-295">Hello JSON 입력 배열에 있는 경우 기본적으로 hello 복사 활동 hello 전체 배열 값을 문자열로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-295">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="04efb-296">사용 하 여 tooextract 데이터를 선택할 수 있습니다 `jsonNodeReference` 및/또는 `jsonPathDefinition`에서 지정 하 여 건너뛸 또는 `jsonPathDefinition`합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-296">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="04efb-297">가 중복 이름에 같은 수준 hello, hello 복사 작업은 마지막 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-297">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="04efb-298">속성 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-298">Property names are case-sensitive.</span></span> <span data-ttu-id="04efb-299">이름은 같지만 대/소문자가 다른 두 속성은 별도의 두 속성으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="04efb-300">**사례 2: 데이터 tooJSON 파일 쓰기**</span><span class="sxs-lookup"><span data-stu-id="04efb-300">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="04efb-301">다음 표에 SQL 데이터베이스의 hello 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-301">If you have hello following table in SQL Database:</span></span>

| <span data-ttu-id="04efb-302">id</span><span class="sxs-lookup"><span data-stu-id="04efb-302">id</span></span> | <span data-ttu-id="04efb-303">order_date</span><span class="sxs-lookup"><span data-stu-id="04efb-303">order_date</span></span> | <span data-ttu-id="04efb-304">order_price</span><span class="sxs-lookup"><span data-stu-id="04efb-304">order_price</span></span> | <span data-ttu-id="04efb-305">order_by</span><span class="sxs-lookup"><span data-stu-id="04efb-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="04efb-306">1</span><span class="sxs-lookup"><span data-stu-id="04efb-306">1</span></span> | <span data-ttu-id="04efb-307">20170119</span><span class="sxs-lookup"><span data-stu-id="04efb-307">20170119</span></span> | <span data-ttu-id="04efb-308">2000</span><span class="sxs-lookup"><span data-stu-id="04efb-308">2000</span></span> | <span data-ttu-id="04efb-309">David</span><span class="sxs-lookup"><span data-stu-id="04efb-309">David</span></span> |
| <span data-ttu-id="04efb-310">2</span><span class="sxs-lookup"><span data-stu-id="04efb-310">2</span></span> | <span data-ttu-id="04efb-311">20170120</span><span class="sxs-lookup"><span data-stu-id="04efb-311">20170120</span></span> | <span data-ttu-id="04efb-312">3500</span><span class="sxs-lookup"><span data-stu-id="04efb-312">3500</span></span> | <span data-ttu-id="04efb-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="04efb-313">Patrick</span></span> |
| <span data-ttu-id="04efb-314">3</span><span class="sxs-lookup"><span data-stu-id="04efb-314">3</span></span> | <span data-ttu-id="04efb-315">20170121</span><span class="sxs-lookup"><span data-stu-id="04efb-315">20170121</span></span> | <span data-ttu-id="04efb-316">4000</span><span class="sxs-lookup"><span data-stu-id="04efb-316">4000</span></span> | <span data-ttu-id="04efb-317">Jason</span><span class="sxs-lookup"><span data-stu-id="04efb-317">Jason</span></span> |

<span data-ttu-id="04efb-318">및 각 레코드에 대해이 원하는 toowrite tooa JSON 개체 형식에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="04efb-318">and for each record, you expect toowrite tooa JSON object in hello following format:</span></span>
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

<span data-ttu-id="04efb-319">hello 출력 데이터 집합으로 **JsonFormat** 형식은 다음과 같이 정의 됩니다: (hello 관련 파트만 부분 정의).</span><span class="sxs-lookup"><span data-stu-id="04efb-319">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="04efb-320">보다 구체적으로, `structure` 대상 파일에 사용자 지정 하는 hello 속성 이름을 정의 하는 섹션 `nestingSeparator` (기본값은 ".")는 hello 이름에서 사용 되는 tooidentify hello 중첩 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-320">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") are used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="04efb-321">이 섹션은 **선택적** toochange hello 속성 이름을 원본 열 이름과 비교 하거나 hello 속성 중 일부를 중첩 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-321">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="04efb-322">AVRO 형식</span><span class="sxs-lookup"><span data-stu-id="04efb-322">AVRO format</span></span>
<span data-ttu-id="04efb-323">Tooparse hello Avro 파일 또는 Avro 형식에서 hello 데이터를 작성 하는 경우 설정 hello `format` `type` 속성 너무**AvroFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-323">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="04efb-324">Toospecify 필요 하지 않습니다 hello typeProperties 섹션 내에서 hello 형식 섹션에서 모든 속성.</span><span class="sxs-lookup"><span data-stu-id="04efb-324">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="04efb-325">예제:</span><span class="sxs-lookup"><span data-stu-id="04efb-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="04efb-326">toouse Hive 테이블에서 Avro 형식으로 참조할 수 있습니다 너무[Apache Hive 자습서](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe)합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-326">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="04efb-327">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="04efb-327">Note hello following points:</span></span>  

* <span data-ttu-id="04efb-328">[복합 데이터 형식](http://avro.apache.org/docs/current/spec.html#schema_complex)은 지원되지 않습니다(레코드, 열거형, 배열, 매핑, 공용 구조체 및 고정).</span><span class="sxs-lookup"><span data-stu-id="04efb-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="04efb-329">ORC 형식</span><span class="sxs-lookup"><span data-stu-id="04efb-329">ORC format</span></span>
<span data-ttu-id="04efb-330">Tooparse hello ORC 파일 형식 ORC hello 데이터를 쓸 경우 설정 hello `format` `type` 속성 너무**OrcFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-330">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="04efb-331">Toospecify 필요 하지 않습니다 hello typeProperties 섹션 내에서 hello 형식 섹션에서 모든 속성.</span><span class="sxs-lookup"><span data-stu-id="04efb-331">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="04efb-332">예제:</span><span class="sxs-lookup"><span data-stu-id="04efb-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="04efb-333">ORC 파일을 복사 하지는 **으로-는** 온-프레미스와 클라우드 사이 데이터 저장소, tooinstall hello 8 JRE (Java Runtime Environment) 게이트웨이 컴퓨터에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="04efb-334">64비트 게이트웨이에는 64비트 JRE가 필요하고 32비트 게이트웨이에는 32비트 JRE가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="04efb-335">[여기서](http://go.microsoft.com/fwlink/?LinkId=808605)두 버전이 모두 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="04efb-336">적절 한 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-336">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="04efb-337">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="04efb-337">Note hello following points:</span></span>

* <span data-ttu-id="04efb-338">복합 데이터 형식(구조체, 맵, 목록, 공용 구조체)은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="04efb-339">ORC 파일에는 3개의 [압축 관련 옵션](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/)(NONE, ZLIB, SNAPPY)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="04efb-340">Data Factory에서는 이러한 압축 형식으로 된 데이터를 ORC 파일에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="04efb-341">Hello 압축을 사용 하 여 코덱은 hello 메타 데이터 tooread hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-341">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="04efb-342">그러나 tooan ORC 파일을 작성할 때 데이터 팩터리 선택 ZLIB, ORC에 대 한 hello 기본값 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-342">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="04efb-343">현재,이 없는 옵션 toooverride이이 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-343">Currently, there is no option toooverride this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="04efb-344">Parquet 형식</span><span class="sxs-lookup"><span data-stu-id="04efb-344">Parquet format</span></span>
<span data-ttu-id="04efb-345">Tooparse hello Parquet 파일 형식 Parquet hello 데이터를 쓸 경우 설정 hello `format` `type` 속성 너무**ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-345">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="04efb-346">Toospecify 필요 하지 않습니다 hello typeProperties 섹션 내에서 hello 형식 섹션에서 모든 속성.</span><span class="sxs-lookup"><span data-stu-id="04efb-346">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="04efb-347">예제:</span><span class="sxs-lookup"><span data-stu-id="04efb-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="04efb-348">Parquet 파일을 복사 하지는 **으로-는** 온-프레미스와 클라우드 사이 데이터 저장소, tooinstall hello 8 JRE (Java Runtime Environment) 게이트웨이 컴퓨터에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="04efb-349">64비트 게이트웨이에는 64비트 JRE가 필요하고 32비트 게이트웨이에는 32비트 JRE가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="04efb-350">[여기서](http://go.microsoft.com/fwlink/?LinkId=808605)두 버전이 모두 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="04efb-351">적절 한 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-351">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="04efb-352">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="04efb-352">Note hello following points:</span></span>

* <span data-ttu-id="04efb-353">복합 데이터 형식(MAP, LIST)은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="04efb-354">Parquet 파일에 다음 압축 관련 옵션 hello: NONE, SNAPPY, GZIP, 및 LZO 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-354">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="04efb-355">Data Factory에서는 이러한 압축 형식으로 된 데이터를 ORC 파일에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="04efb-356">Hello 압축 코덱 hello 메타 데이터 tooread hello 데이터에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-356">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="04efb-357">그러나 tooa Parquet 파일을 작성할 때 데이터 팩터리 선택 SNAPPY, Parquet 형식에 대 한 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-357">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="04efb-358">현재,이 없는 옵션 toooverride이이 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-358">Currently, there is no option toooverride this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="04efb-359">압축 지원</span><span class="sxs-lookup"><span data-stu-id="04efb-359">Compression support</span></span>
<span data-ttu-id="04efb-360">큰 데이터 집합을 처리하면 I/O 및 네트워크 병목 현상이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="04efb-361">따라서 압축된 데이터 저장소에 수 hello 네트워크를 통해 데이터 전송 속도 및 디스크 공간을 절약 뿐만 아니라 표시할 수도 빅 데이터 처리 성능이 크게 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-361">Therefore, compressed data in stores can not only speed up data transfer across hello network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="04efb-362">현재 압축은 Azure Blob 또는 온-프레미스 파일 시스템과 같은 파일 기반 데이터 저장소에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="04efb-363">데이터 집합을 사용 하 여 hello에 대 한 toospecify 압축 **압축** hello 다음 예제와 같이 hello 데이터 집합 JSON의에서 속성:</span><span class="sxs-lookup"><span data-stu-id="04efb-363">toospecify compression for a dataset, use hello **compression** property in hello dataset JSON as in hello following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="04efb-364">Hello 샘플 데이터 집합 복사 작업의 hello 출력으로 사용, 가정 hello 복사 활동 압축 hello 최적의 비율을 사용 하 여 GZIP 코덱을 사용 하 여 데이터를 출력 하 고 hello Azure Blob 저장소에서에서 pagecounts.csv.gz 라는 파일에 압축 hello 데이터를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-364">Suppose hello sample dataset is used as hello output of a copy activity, hello copy activity compresses hello output data with GZIP codec using optimal ratio and then write hello compressed data into a file named pagecounts.csv.gz in hello Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="04efb-365">데이터 hello에 대 한 압축 설정이 지원 되지 않습니다 **AvroFormat**, **OrcFormat**, 또는 **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-365">Compression settings are not supported for data in hello **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="04efb-366">이러한 형식의 파일을 읽을 때 데이터 팩터리 검색 하 고 hello 메타 데이터에 hello 압축 코덱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-366">When reading files in these formats, Data Factory detects and uses hello compression codec in hello metadata.</span></span> <span data-ttu-id="04efb-367">Data Factory toofiles 이러한 형식의 작성할 때 해당 형식에 대 한 기본 압축 코덱 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-367">When writing toofiles in these formats, Data Factory chooses hello default compression codec for that format.</span></span> <span data-ttu-id="04efb-368">예를 들어 OrcFormat에 대해 ZLIB를 사용하고 ParquetFormat에 대해 SNAPPY를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="04efb-369">hello **압축** 섹션에 다음 두 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-369">hello **compression** section has two properties:</span></span>  

* <span data-ttu-id="04efb-370">**형식:** 될 수 있는 hello 압축 코덱을 **GZIP**, **Deflate**, **BZIP2**, 또는 **ZipDeflate**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-370">**Type:** hello compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="04efb-371">**수준:** 될 수 있는 hello 압축률 **최적** 또는 **fastest 이면**합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-371">**Level:** hello compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="04efb-372">**가장 빠른:** hello 결과 파일 최적으로 압축 되지 않은 경우에 hello 압축 작업을 최대한 빨리 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-372">**Fastest:** hello compression operation should complete as quickly as possible, even if hello resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="04efb-373">**최적의**: hello 압축 작업 최적으로 압축 hello 연산이 더 긴 시간 toocomplete 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-373">**Optimal**: hello compression operation should be optimally compressed, even if hello operation takes a longer time toocomplete.</span></span>

    <span data-ttu-id="04efb-374">자세한 내용은 [압축 수준](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04efb-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="04efb-375">지정 하는 경우 `compression` 입력된 데이터 집합 JSON의에서 hello 파이프라인 hello 소스에서 압축 된 데이터를 읽을 수 속성과 hello 복사 작업 출력 데이터 집합 JSON에에서 hello 속성을 지정 하는 경우 압축 된 데이터 toohello 대상을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-375">When you specify `compression` property in an input dataset JSON, hello pipeline can read compressed data from hello source; and when you specify hello property in an output dataset JSON, hello copy activity can write compressed data toohello destination.</span></span> <span data-ttu-id="04efb-376">다음은 몇 가지 샘플 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="04efb-377">Azure blob에서 데이터 읽기 GZIP 압축, 압축을 풀고 결과 데이터 tooan Azure SQL 데이터베이스를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data tooan Azure SQL database.</span></span> <span data-ttu-id="04efb-378">Hello 입력된 hello로 Azure Blob 데이터 집합을 정의할 `compression` `type` GZIP으로 JSON 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-378">You define hello input Azure Blob dataset with hello `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="04efb-379">온-프레미스 파일 시스템에서 일반 텍스트 파일에서 데이터 읽기, GZip 형식을 사용 하 여 압축 및 압축 hello 데이터 tooan Azure blob를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write hello compressed data tooan Azure blob.</span></span> <span data-ttu-id="04efb-380">Hello로 출력 Azure Blob 데이터 집합 정의 `compression` `type` GZip으로 JSON 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-380">You define an output Azure Blob dataset with hello `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="04efb-381">FTP 서버에서.zip 파일 읽기, 내부 tooget hello 파일 압축을 풀고 Azure 데이터 레이크 저장소로 해당 파일을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-381">Read .zip file from FTP server, decompress it tooget hello files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="04efb-382">Hello로 입력된 FTP 데이터 집합 정의 `compression` `type` ZipDeflate로 JSON 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-382">You define an input FTP dataset with hello `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="04efb-383">Azure blob에서 GZIP 압축 데이터 읽기, 압축을 풀어, BZIP2를 사용 하 여 압축 및 결과 데이터 tooan Azure blob에 쓰기</span><span class="sxs-lookup"><span data-stu-id="04efb-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data tooan Azure blob.</span></span> <span data-ttu-id="04efb-384">Hello Azure Blob 된 입력된 데이터 집합 정의 `compression` `type` tooGZIP를 설정 하 고 출력 데이터 집합을 hello `compression` `type` tooBZIP2이 경우에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="04efb-384">You define hello input Azure Blob dataset with `compression` `type` set tooGZIP and hello output dataset with `compression` `type` set tooBZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="04efb-385">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04efb-385">Next steps</span></span>
<span data-ttu-id="04efb-386">Azure Data Factory에서 지원 되는 파일 기반 데이터 저장소에 대 한 아티클을 다음 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="04efb-386">See hello following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="04efb-387">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="04efb-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="04efb-388">Azure 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="04efb-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="04efb-389">FTP</span><span class="sxs-lookup"><span data-stu-id="04efb-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="04efb-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="04efb-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="04efb-391">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="04efb-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="04efb-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="04efb-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
