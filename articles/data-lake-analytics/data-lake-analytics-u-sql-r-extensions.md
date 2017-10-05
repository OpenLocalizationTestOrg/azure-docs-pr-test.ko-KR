---
title: "Azure Data Lake Analytics에서 R로 U-SQL 스크립트 확장 | Microsoft Docs"
description: "U-SQL 스크립트에서 R 코드를 실행하는 방법을 알아봅니다"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: d479af515566f497d9611e75426f6acb8f8276d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="81305-103">자습서: R로 U-SQL 확장 시작</span><span class="sxs-lookup"><span data-stu-id="81305-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="81305-104">다음 예제에서는 R 코드를 배포하는 기본 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81305-104">The following example illustrates the basic steps for deploying R code:</span></span>
* <span data-ttu-id="81305-105">`REFERENCE ASSEMBLY` 문을 사용하여 U-SQL 스크립트에 대한 R 확장을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="81305-105">Use the `REFERENCE ASSEMBLY` statement to enable R extensions for the U-SQL Script.</span></span>
* <span data-ttu-id="81305-106">` REDUCE` 연산을 사용하여 키의 입력 데이터를 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="81305-106">Use the` REDUCE` operation to partition the input data on a key.</span></span>
* <span data-ttu-id="81305-107">U-SQL용 R 확장에는 리듀서에 할당된 각 꼭짓점에서 R 코드를 실행하는 기본 제공 리듀서(`Extension.R.Reducer`)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="81305-107">The R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned to the reducer.</span></span> 
* <span data-ttu-id="81305-108">각각 `inputFromUSQL` 및 `outputToUSQL `이라는 명명된 전용 데이터 프레임을 사용하여 U-SQL과 R 간에 데이터를 전달합니다. 입력 및 출력 DataFrame 식별자 이름은 고정되어 있습니다. 즉 사용자가 입력 및 출력 DataFrame 식별자의 미리 정의된 이름을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81305-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively to pass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-the-u-sql-script"></a><span data-ttu-id="81305-109">U-SQL 스크립트에 R 코드 포함</span><span class="sxs-lookup"><span data-stu-id="81305-109">Embedding R code in the U-SQL script</span></span>

<span data-ttu-id="81305-110">`Extension.R.Reducer`의 명령 매개 변수를 사용하여 U-SQL 스크립트에 R 코드를 인라인으로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81305-110">You can inline the R code your U-SQL script by using the command parameter of the `Extension.R.Reducer`.</span></span> <span data-ttu-id="81305-111">예를 들어 문자열 변수로 R 스크립트를 선언하고 리듀서에 매개 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81305-111">For example, you can declare the R script as a string variable and pass it as a parameter to the Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that the column names are the same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-the-r-code-in-a-separate-file-and-reference-it--the-u-sql-script"></a><span data-ttu-id="81305-112">별도 파일에 R 코드를 유지하고 U-SQL 스크립트에서 참조</span><span class="sxs-lookup"><span data-stu-id="81305-112">Keep the R code in a separate file and reference it  the U-SQL script</span></span>

<span data-ttu-id="81305-113">다음 예제에서는 좀 더 복잡한 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81305-113">The following example illustrates a more complex usage.</span></span> <span data-ttu-id="81305-114">이 경우 R 코드는 U-SQL 스크립트인 RESOURCE로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="81305-114">In this case, the R code is deployed as a RESOURCE that is the U-SQL script.</span></span>

<span data-ttu-id="81305-115">이 R 코드를 별도 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81305-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="81305-116">U-SQL 스크립트를 사용하여 DEPLOY RESOURCE 문과 함께 R 스크립트를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="81305-116">Use a U-SQL script to deploy that R script with the DEPLOY RESOURCE statement.</span></span>

    REFERENCE ASSEMBLY [ExtR];

    DEPLOY RESOURCE @"/usqlext/samples/R/RinUSQL_PredictUsingLinearModelasDF.R";
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT 
            SepalLength double,
            SepalWidth double,
            PetalLength double,
            PetalWidth double,
            Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT 
            Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput = REDUCE @ExtendedData ON Par
        PRODUCE Par, fit double, lwr double, upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile:"RinUSQL_PredictUsingLinearModelasDF.R", rReturnType:"dataframe", stringsAsFactors:false);
        OUTPUT @RScriptOutput TO @OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="81305-117">R과 U-SQL 통합 방법</span><span class="sxs-lookup"><span data-stu-id="81305-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="81305-118">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="81305-118">Datatypes</span></span>
* <span data-ttu-id="81305-119">U-SQL의 문자열 및 숫자 열은 R DataFrame과 U-SQL 간에 있는 그대로 변환됩니다[지원되는 형식: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="81305-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="81305-120">`Factor` 데이터 형식은 U-SQL에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81305-120">The `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="81305-121">`byte[]`는 base64로 인코딩된 `string`로 직렬화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81305-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="81305-122">일단 U-SQL에서 R 입력 데이터 프레임을 만들거나 `stringsAsFactors: true` 리듀서 매개 변수를 설정하여 U-SQL 문자열을 R 코드의 요소로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81305-122">U-SQL strings can be converted to factors in R code, once U-SQL create R input dataframe or by setting the reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="81305-123">스키마</span><span class="sxs-lookup"><span data-stu-id="81305-123">Schemas</span></span>
* <span data-ttu-id="81305-124">U-SQL 데이터 집합에는 열 이름이 중복될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81305-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="81305-125">U-SQL 데이터 집합 열 이름은 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81305-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="81305-126">열 이름은 U-SQL 및 R 스크립트에서 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81305-126">Column names must be the same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="81305-127">읽기 전용 열이 UDO의 출력 스키마의 일부이면 U-SQL 테이블에 자동으로 다시 주입되기 때문에</span><span class="sxs-lookup"><span data-stu-id="81305-127">Readonly column cannot be part of the output dataframe.</span></span> <span data-ttu-id="81305-128">이 읽기 전용 열은 출력 데이터 프레임의 일부가 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81305-128">Because readonly columns are automatically injected back in the U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="81305-129">기능 제한 사항</span><span class="sxs-lookup"><span data-stu-id="81305-129">Functional limitations</span></span>
* <span data-ttu-id="81305-130">R 엔진은 동일한 프로세스에서 두 번 인스턴스화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81305-130">The R Engine can't be instantiated twice in the same process.</span></span> 
* <span data-ttu-id="81305-131">현재, U-SQL 중단은 리듀셔 UDO를 사용하여 생성된 분할된 모델을 사용하는 예측에 결합 UDO를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81305-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="81305-132">사용자는 리소스로 분할된 모델을 선언하고 R 스크립트에서 모델을 사용할 수 있습니다(샘플 코드 `ExtR_PredictUsingLMRawStringReducer.usql` 참조).</span><span class="sxs-lookup"><span data-stu-id="81305-132">Users can declare the partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="81305-133">R 버전</span><span class="sxs-lookup"><span data-stu-id="81305-133">R Versions</span></span>
<span data-ttu-id="81305-134">R 3.2.2만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="81305-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="81305-135">표준 R 모듈</span><span class="sxs-lookup"><span data-stu-id="81305-135">Standard R modules</span></span>

    base
    boot
    Class
    Cluster
    codetools
    compiler
    datasets
    doParallel
    doRSR
    foreach
    foreign
    Graphics
    grDevices
    grid
    iterators
    KernSmooth
    lattice
    MASS
    Matrix
    Methods
    mgcv
    nlme
    Nnet
    Parallel
    pkgXMLBuilder
    RevoIOQ
    revoIpe
    RevoMods
    RevoPemaR
    RevoRpeConnector
    RevoRsrConnector
    RevoScaleR
    RevoTreeView
    RevoUtils
    RevoUtilsMath
    Rpart
    RUnit
    spatial
    splines
    Stats
    stats4
    survival
    Tcltk
    Tools
    translations
    utils
    XML

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="81305-136">입력 및 출력 크기 제한</span><span class="sxs-lookup"><span data-stu-id="81305-136">Input and Output size limitations</span></span>
<span data-ttu-id="81305-137">모든 정점에는 할당되는 메모리 양이 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81305-137">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="81305-138">입력 및 출력 DataFrames는 R 코드의 메모리에 있어야 하므로 입력 및 출력의 총 크기는 500MB를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81305-138">Because the input and output DataFrames must exist in memory in the R code, the total size for the input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="81305-139">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="81305-139">Sample Code</span></span>
<span data-ttu-id="81305-140">U-SQL Advanced Analytics 확장을 설치하면 더 많은 샘플 코드가 Data Lake Store 계정에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="81305-140">More sample code is available in your Data Lake Store account after you install the U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="81305-141">더 많은 샘플 코드에 대한 경로는 `<your_account_address>/usqlext/samples/R`입니다.</span><span class="sxs-lookup"><span data-stu-id="81305-141">The path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="81305-142">U-SQL을 사용한 사용자 지정 R 모듈 배포</span><span class="sxs-lookup"><span data-stu-id="81305-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="81305-143">먼저, R 사용자 지정 모듈을 만들어 압축(zip)한 후 압축된 R 사용자 지정 모듈 파일을 ADL 저장소에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="81305-143">First, create an R custom module and zip it and then upload the zipped R custom module file to your ADL store.</span></span> <span data-ttu-id="81305-144">예제에서는 사용 중인 ADLA 계정에 대해 기본 ADLS 계정의 루트로 magittr_1.5.zip을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="81305-144">In the example, we will upload magittr_1.5.zip to the root of the default ADLS account for the ADLA account we are using.</span></span> <span data-ttu-id="81305-145">모듈을 ADL 저장소에 업로드한 후 DEPLOY RESOURCE 사용으로 선언하여 U-SQL 스크립트에서 사용할 수 있도록 하고 `install.packages`를 호출하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="81305-145">Once you upload the module to ADL store, declare it as use DEPLOY RESOURCE to make it available in your U-SQL script and call `install.packages` to install it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script to run
    DECLARE @myRScript = @"
    # install the magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load the magrittr package,
    require(magrittr),
    # demonstrate use of the magrittr package,
    2 %>% sqrt
    ";

    @InputData =
    EXTRACT SepalLength double,
    SepalWidth double,
    PetalLength double,
    PetalWidth double,
    Species string
    FROM @IrisData
    USING Extractors.Csv();

    @ExtendedData =
    SELECT 0 AS Par,
    *
    FROM @InputData;

    @RScriptOutput = REDUCE @ExtendedData ON Par
    PRODUCE Par, RowId int, ROutput string
    READONLY Par
    USING new Extension.R.Reducer(command:@myRScript, rReturnType:"charactermatrix");

    OUTPUT @RScriptOutput TO @OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="81305-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81305-146">Next Steps</span></span>
* [<span data-ttu-id="81305-147">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="81305-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="81305-148">Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="81305-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="81305-149">Azure 데이터 레이크 분석 작업에 U-SQL 창 함수 사용</span><span class="sxs-lookup"><span data-stu-id="81305-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
