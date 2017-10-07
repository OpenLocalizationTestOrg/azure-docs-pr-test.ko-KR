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
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a>자습서: R로 U-SQL 확장 시작

다음 예제는 hello hello R 코드를 배포 하기 위한 기본 단계를 보여 줍니다.
* 사용 하 여 hello `REFERENCE ASSEMBLY` hello U-SQL 스크립트에 대 한 문 tooenable R 확장 합니다.
* 사용 하 여는` REDUCE` 작업 toopartition hello 입력 키에 데이터를 필터링 합니다.
* U-SQL에 대 한 hello R 확장에는 기본 제공 리 듀 서 포함 (`Extension.R.Reducer`) 각 할당 된 꼭 짓 점 toohello 리 듀 서에서 R 코드를 실행 하는 합니다. 
* 전용의 사용 데이터 프레임 라는 명명 된 `inputFromUSQL` 및 `outputToUSQL `toopass 데이터 각각 U-SQL 오른쪽 입력과 출력 간의 데이터 프레임 식별자 이름은 고정 되어 (즉, 사용자를 변경할 수 없습니다 이러한 미리 정의 된 이름을 입력의 출력 데이터 프레임 식별자)입니다.

## <a name="embedding-r-code-in-hello-u-sql-script"></a>U-SQL 스크립트 hello에 R 코드를 포함합니다.

Hello의 hello 명령 매개 변수를 사용 하 여 인라인 hello R 코드 U-SQL 스크립트 수 `Extension.R.Reducer`합니다. 예를 들어 hello 문자열 변수로 R 스크립트를 선언 하 고 매개 변수 toohello 리 듀 서 변수로 전달할 수 있습니다.


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

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a>별도의 파일로 hello R 코드를 유지 하 고 hello U-SQL 스크립트를 참조

다음 예제는 hello 더 복잡 한 사용법을 보여 줍니다. 이 경우 hello R 코드는 hello U-SQL 스크립트를 리소스로 배포 됩니다.

이 R 코드를 별도 파일로 저장합니다.

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

리소스 배포 문 hello로 U-SQL 스크립트 toodeploy 해당 R 스크립트를 사용 합니다.

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

## <a name="how-r-integrates-with-u-sql"></a>R과 U-SQL 통합 방법

### <a name="datatypes"></a>데이터 형식
* U-SQL의 문자열 및 숫자 열은 R DataFrame과 U-SQL 간에 있는 그대로 변환됩니다[지원되는 형식: `double`, `string`, `bool`, `integer`, `byte`].
* hello `Factor` U-SQL에서 데이터 형식이 지원 되지 않습니다.
* `byte[]`는 base64로 인코딩된 `string`로 직렬화되어야 합니다.
* U-SQL 문자열 U-SQL R 입력된 데이터 프레임을 작성 하거나 hello 리 듀 서 매개 변수를 설정 하 여 R 코드에서 변환 된 toofactors 수 `stringsAsFactors: true`합니다.

### <a name="schemas"></a>스키마
* U-SQL 데이터 집합에는 열 이름이 중복될 수 없습니다.
* U-SQL 데이터 집합 열 이름은 문자열이어야 합니다.
* 열 이름은 U SQL과 R 스크립트에서 동일한 hello 해야 합니다.
* 읽기 전용 열에는 hello 출력 데이터 프레임의 일부가 될 수 없습니다. 읽기 전용 열은 UDO의 출력 스키마의 일부인 경우 hello U-SQL 테이블에 다시 자동으로 삽입 됩니다 때문에.

### <a name="functional-limitations"></a>기능 제한 사항
* hello R 엔진 인스턴스화할 수 없습니다 두 번에 같은 프로세스 hello 합니다. 
* 현재, U-SQL 중단은 리듀셔 UDO를 사용하여 생성된 분할된 모델을 사용하는 예측에 결합 UDO를 지원하지 않습니다. 사용자는 리소스로 분할 하는 hello 모델을 선언 하 고 자신의 R 스크립트에서 사용할 수 (예제 코드는 `ExtR_PredictUsingLMRawStringReducer.usql`)

### <a name="r-versions"></a>R 버전
R 3.2.2만 지원됩니다.

### <a name="standard-r-modules"></a>표준 R 모듈

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

### <a name="input-and-output-size-limitations"></a>입력 및 출력 크기 제한
모든 꼭에 tooit 할당 된 메모리 양이 제한 되어 있습니다. Hello 입력 및 출력 데이터 프레임에에서 존재 해야 하므로 hello R 코드에서 메모리를 hello 입력 및 출력의 총 크기 hello 500MB를 초과할 수 없습니다.

### <a name="sample-code"></a>샘플 코드
더 많은 샘플 코드가 hello U-SQL 고급 분석 확장을 설치한 후 Data Lake 저장소 계정이 제공 됩니다. hello에 대 한 더 많은 샘플 코드가 경로가: `<your_account_address>/usqlext/samples/R`합니다. 

## <a name="deploying-custom-r-modules-with-u-sql"></a>U-SQL을 사용한 사용자 지정 R 모듈 배포

먼저 사용자 지정 R 모듈 및 것 zip 만들고 R 사용자 지정 모듈 파일 tooyour ADL 저장소 압축 hello를 업로드 합니다. Hello 예제에서 우리는 ADLA 계정 사용 하 여 hello에 대 한 hello 기본 ADLS 계정의 magittr_1.5.zip toohello 루트를 업로드 합니다. Hello 모듈 tooADL 저장소 업로드 선언 toomake 배포할 리소스를 사용 하 여 U-SQL 스크립트와 호출에서 사용할 수 `install.packages` tooinstall 것입니다.

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

## <a name="next-steps"></a>다음 단계
* [Microsoft Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)
* [Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)
* [Azure 데이터 레이크 분석 작업에 U-SQL 창 함수 사용](data-lake-analytics-use-window-functions.md)
