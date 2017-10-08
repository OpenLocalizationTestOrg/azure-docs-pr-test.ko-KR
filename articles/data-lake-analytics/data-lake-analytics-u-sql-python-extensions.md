---
title: "Azure 데이터 레이크 분석에서 python aaaExtend U-SQL 스크립트 | Microsoft Docs"
description: "U-SQL 스크립트에서 toorun Python 코드가 하는 방식에 대해 알아봅니다"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="d8880-103">자습서: Python으로 U-SQL 확장 시작하기</span><span class="sxs-lookup"><span data-stu-id="d8880-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="d8880-104">U-SQL에 대 한 Python 확장 Python 코드의 개발자 tooperform 대규모 병렬 실행을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-104">Python Extensions for U-SQL enable developers tooperform massively parallel execution of Python code.</span></span> <span data-ttu-id="d8880-105">다음 예제는 hello hello 기본 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-105">hello following example illustrates hello basic steps:</span></span>

* <span data-ttu-id="d8880-106">사용 하 여 hello `REFERENCE ASSEMBLY` hello U-SQL 스크립트에 대 한 문 tooenable Python 확장</span><span class="sxs-lookup"><span data-stu-id="d8880-106">Use hello `REFERENCE ASSEMBLY` statement tooenable Python extensions for hello U-SQL Script</span></span>
* <span data-ttu-id="d8880-107">Hello를 사용 하 여 `REDUCE` 작업 toopartition hello 입력 키에 대 한 데이터</span><span class="sxs-lookup"><span data-stu-id="d8880-107">Using hello `REDUCE` operation toopartition hello input data on a key</span></span>
* <span data-ttu-id="d8880-108">hello U-SQL에 대 한 Python 확장 포함 기본 제공 리 듀 서 (`Extension.Python.Reducer`) 각 할당 된 꼭 짓 점 toohello 리 듀 서에서 Python 코드를 실행 하는</span><span class="sxs-lookup"><span data-stu-id="d8880-108">hello Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned toohello reducer</span></span>
* <span data-ttu-id="d8880-109">호출 함수를 가진 hello 포함 된 Python 코드를 포함 하는 hello U-SQL 스크립트 `usqlml_main` 팬더 데이터 프레임 입력으로 허용 하 고 팬더 출력 데이터 프레임을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-109">hello U-SQL script contains hello embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="d8880-110">Python과 U-SQL 통합 방법</span><span class="sxs-lookup"><span data-stu-id="d8880-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="d8880-111">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="d8880-111">Datatypes</span></span>

* <span data-ttu-id="d8880-112">U-SQL의 문자열 및 숫자 열은 Pandas와 U-SQL 간에 있는 그대로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="d8880-113">U-SQL Null은 팬더에서 변환 된 tooand `NA` 값</span><span class="sxs-lookup"><span data-stu-id="d8880-113">U-SQL Nulls are converted tooand from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="d8880-114">스키마</span><span class="sxs-lookup"><span data-stu-id="d8880-114">Schemas</span></span>

* <span data-ttu-id="d8880-115">Pandas의 인덱스 벡터는 U-SQL에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="d8880-116">모든 입력된 데이터 프레임 hello Python 함수에는 항상 0k hello 행 수-1에서에서 64 비트 숫자 인덱스를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-116">All input data frames in hello Python function always have a 64-bit numerical index from 0 through hello number of rows minus 1.</span></span> 
* <span data-ttu-id="d8880-117">U-SQL 데이터 집합에는 중복된 열 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="d8880-118">문자열이 아닌 U-SQL 데이터 집합 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="d8880-119">Python 버전</span><span class="sxs-lookup"><span data-stu-id="d8880-119">Python Versions</span></span>
<span data-ttu-id="d8880-120">Python 3.5.1(Windows용으로 컴파일)만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="d8880-121">표준 Python 모듈</span><span class="sxs-lookup"><span data-stu-id="d8880-121">Standard Python modules</span></span>
<span data-ttu-id="d8880-122">Hello 기본 Python 모듈을 모두 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-122">All hello standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="d8880-123">추가 Python 모듈</span><span class="sxs-lookup"><span data-stu-id="d8880-123">Additional Python modules</span></span>
<span data-ttu-id="d8880-124">표준 Python 라이브러리 hello, 외에 몇 가지 자주 사용 되는 python 라이브러리가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-124">Besides hello standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="d8880-125">예외 메시지</span><span class="sxs-lookup"><span data-stu-id="d8880-125">Exception Messages</span></span>
<span data-ttu-id="d8880-126">현재 Python 코드의 예외는 일반적인 정점 오류로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="d8880-127">Hello 이후에서 hello U-SQL 작업 오류 메시지는 hello Python 예외 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-127">In hello future, hello U-SQL Job error messages will display hello Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="d8880-128">입력 및 출력 크기 제한</span><span class="sxs-lookup"><span data-stu-id="d8880-128">Input and Output size limitations</span></span>
<span data-ttu-id="d8880-129">모든 꼭에 tooit 할당 된 메모리 양이 제한 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-129">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="d8880-130">현재 이 제한은 AU의 경우 6GB입니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="d8880-131">Hello 입력 및 출력 데이터 프레임에에서 존재 해야 하므로 hello Python 코드에서 메모리를 hello hello 입력 및 출력에 대 한 총 크기는 6GB를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8880-131">Because hello input and output DataFrames must exist in memory in hello Python code, hello total size for hello input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="d8880-132">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d8880-132">See also</span></span>
* [<span data-ttu-id="d8880-133">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="d8880-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="d8880-134">Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발</span><span class="sxs-lookup"><span data-stu-id="d8880-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="d8880-135">Azure 데이터 레이크 분석 작업에 U-SQL 창 함수 사용</span><span class="sxs-lookup"><span data-stu-id="d8880-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

