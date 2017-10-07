---
title: "Azure Data Lake 분석에서 R로 aaaExtend U-SQL 스크립트 | Microsoft Docs"
description: "U-SQL 스크립트에서 toorun R 코드가 하는 방식에 대해 알아봅니다"
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
ms.openlocfilehash: 24affd4963a08d30a7111b49af388e9c1268430e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="ddc24-103">자습서: R로 U-SQL 확장 시작</span><span class="sxs-lookup"><span data-stu-id="ddc24-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="ddc24-104">다음 예제는 hello hello R 코드를 배포 하기 위한 기본 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-104">hello following example illustrates hello basic steps for deploying R code:</span></span>
* <span data-ttu-id="ddc24-105">사용 하 여 hello `REFERENCE ASSEMBLY` hello U-SQL 스크립트에 대 한 문 tooenable R 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-105">Use hello `REFERENCE ASSEMBLY` statement tooenable R extensions for hello U-SQL Script.</span></span>
* <span data-ttu-id="ddc24-106">사용 하 여는` REDUCE` 작업 toopartition hello 입력 키에 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-106">Use the` REDUCE` operation toopartition hello input data on a key.</span></span>
* <span data-ttu-id="ddc24-107">U-SQL에 대 한 hello R 확장에는 기본 제공 리 듀 서 포함 (`Extension.R.Reducer`) 각 할당 된 꼭 짓 점 toohello 리 듀 서에서 R 코드를 실행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-107">hello R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned toohello reducer.</span></span> 
* <span data-ttu-id="ddc24-108">전용의 사용 데이터 프레임 라는 명명 된 `inputFromUSQL` 및 `outputToUSQL `toopass 데이터 각각 U-SQL 오른쪽 입력과 출력 간의 데이터 프레임 식별자 이름은 고정 되어 (즉, 사용자를 변경할 수 없습니다 이러한 미리 정의 된 이름을 입력의 출력 데이터 프레임 식별자)입니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively toopass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-hello-u-sql-script"></a><span data-ttu-id="ddc24-109">U-SQL 스크립트 hello에 R 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-109">Embedding R code in hello U-SQL script</span></span>

<span data-ttu-id="ddc24-110">Hello의 hello 명령 매개 변수를 사용 하 여 인라인 hello R 코드 U-SQL 스크립트 수 `Extension.R.Reducer`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-110">You can inline hello R code your U-SQL script by using hello command parameter of hello `Extension.R.Reducer`.</span></span> <span data-ttu-id="ddc24-111">예를 들어 hello 문자열 변수로 R 스크립트를 선언 하 고 매개 변수 toohello 리 듀 서 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-111">For example, you can declare hello R script as a string variable and pass it as a parameter toohello Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that hello column names are hello same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a><span data-ttu-id="ddc24-112">별도의 파일로 hello R 코드를 유지 하 고 hello U-SQL 스크립트를 참조</span><span class="sxs-lookup"><span data-stu-id="ddc24-112">Keep hello R code in a separate file and reference it  hello U-SQL script</span></span>

<span data-ttu-id="ddc24-113">다음 예제는 hello 더 복잡 한 사용법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-113">hello following example illustrates a more complex usage.</span></span> <span data-ttu-id="ddc24-114">이 경우 hello R 코드는 hello U-SQL 스크립트를 리소스로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-114">In this case, hello R code is deployed as a RESOURCE that is hello U-SQL script.</span></span>

<span data-ttu-id="ddc24-115">이 R 코드를 별도 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="ddc24-116">리소스 배포 문 hello로 U-SQL 스크립트 toodeploy 해당 R 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-116">Use a U-SQL script toodeploy that R script with hello DEPLOY RESOURCE statement.</span></span>

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
        OUTPUT @RScriptOutput too@OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="ddc24-117">R과 U-SQL 통합 방법</span><span class="sxs-lookup"><span data-stu-id="ddc24-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="ddc24-118">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="ddc24-118">Datatypes</span></span>
* <span data-ttu-id="ddc24-119">U-SQL의 문자열 및 숫자 열은 R DataFrame과 U-SQL 간에 있는 그대로 변환됩니다[지원되는 형식: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="ddc24-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="ddc24-120">hello `Factor` U-SQL에서 데이터 형식이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-120">hello `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="ddc24-121">`byte[]`는 base64로 인코딩된 `string`로 직렬화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="ddc24-122">U-SQL 문자열 U-SQL R 입력된 데이터 프레임을 작성 하거나 hello 리 듀 서 매개 변수를 설정 하 여 R 코드에서 변환 된 toofactors 수 `stringsAsFactors: true`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-122">U-SQL strings can be converted toofactors in R code, once U-SQL create R input dataframe or by setting hello reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="ddc24-123">스키마</span><span class="sxs-lookup"><span data-stu-id="ddc24-123">Schemas</span></span>
* <span data-ttu-id="ddc24-124">U-SQL 데이터 집합에는 열 이름이 중복될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="ddc24-125">U-SQL 데이터 집합 열 이름은 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="ddc24-126">열 이름은 U SQL과 R 스크립트에서 동일한 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-126">Column names must be hello same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="ddc24-127">읽기 전용 열에는 hello 출력 데이터 프레임의 일부가 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-127">Readonly column cannot be part of hello output dataframe.</span></span> <span data-ttu-id="ddc24-128">읽기 전용 열은 UDO의 출력 스키마의 일부인 경우 hello U-SQL 테이블에 다시 자동으로 삽입 됩니다 때문에.</span><span class="sxs-lookup"><span data-stu-id="ddc24-128">Because readonly columns are automatically injected back in hello U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="ddc24-129">기능 제한 사항</span><span class="sxs-lookup"><span data-stu-id="ddc24-129">Functional limitations</span></span>
* <span data-ttu-id="ddc24-130">hello R 엔진 인스턴스화할 수 없습니다 두 번에 같은 프로세스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-130">hello R Engine can't be instantiated twice in hello same process.</span></span> 
* <span data-ttu-id="ddc24-131">현재, U-SQL 중단은 리듀셔 UDO를 사용하여 생성된 분할된 모델을 사용하는 예측에 결합 UDO를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="ddc24-132">사용자는 리소스로 분할 하는 hello 모델을 선언 하 고 자신의 R 스크립트에서 사용할 수 (예제 코드는 `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="ddc24-132">Users can declare hello partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="ddc24-133">R 버전</span><span class="sxs-lookup"><span data-stu-id="ddc24-133">R Versions</span></span>
<span data-ttu-id="ddc24-134">R 3.2.2만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="ddc24-135">표준 R 모듈</span><span class="sxs-lookup"><span data-stu-id="ddc24-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="ddc24-136">입력 및 출력 크기 제한</span><span class="sxs-lookup"><span data-stu-id="ddc24-136">Input and Output size limitations</span></span>
<span data-ttu-id="ddc24-137">모든 꼭에 tooit 할당 된 메모리 양이 제한 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-137">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="ddc24-138">Hello 입력 및 출력 데이터 프레임에에서 존재 해야 하므로 hello R 코드에서 메모리를 hello 입력 및 출력의 총 크기 hello 500MB를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-138">Because hello input and output DataFrames must exist in memory in hello R code, hello total size for hello input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="ddc24-139">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="ddc24-139">Sample Code</span></span>
<span data-ttu-id="ddc24-140">더 많은 샘플 코드가 hello U-SQL 고급 분석 확장을 설치한 후 Data Lake 저장소 계정이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-140">More sample code is available in your Data Lake Store account after you install hello U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="ddc24-141">hello에 대 한 더 많은 샘플 코드가 경로가: `<your_account_address>/usqlext/samples/R`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-141">hello path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="ddc24-142">U-SQL을 사용한 사용자 지정 R 모듈 배포</span><span class="sxs-lookup"><span data-stu-id="ddc24-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="ddc24-143">먼저 사용자 지정 R 모듈 및 것 zip 만들고 R 사용자 지정 모듈 파일 tooyour ADL 저장소 압축 hello를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-143">First, create an R custom module and zip it and then upload hello zipped R custom module file tooyour ADL store.</span></span> <span data-ttu-id="ddc24-144">Hello 예제에서 우리는 ADLA 계정 사용 하 여 hello에 대 한 hello 기본 ADLS 계정의 magittr_1.5.zip toohello 루트를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-144">In hello example, we will upload magittr_1.5.zip toohello root of hello default ADLS account for hello ADLA account we are using.</span></span> <span data-ttu-id="ddc24-145">Hello 모듈 tooADL 저장소 업로드 선언 toomake 배포할 리소스를 사용 하 여 U-SQL 스크립트와 호출에서 사용할 수 `install.packages` tooinstall 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ddc24-145">Once you upload hello module tooADL store, declare it as use DEPLOY RESOURCE toomake it available in your U-SQL script and call `install.packages` tooinstall it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script toorun
    DECLARE @myRScript = @"
    # install hello magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load hello magrittr package,
    require(magrittr),
    # demonstrate use of hello magrittr package,
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

    OUTPUT @RScriptOutput too@OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="ddc24-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ddc24-146">Next Steps</span></span>
* [<span data-ttu-id="ddc24-147">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="ddc24-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="ddc24-148">Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="ddc24-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="ddc24-149">Azure 데이터 레이크 분석 작업에 U-SQL 창 함수 사용</span><span class="sxs-lookup"><span data-stu-id="ddc24-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
