---
title: "U-SQL 언어 시작 | Microsoft Docs"
description: "Hello U SQL 언어의 hello 기본 사항에 알아봅니다."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a>U-SQL 시작
U-SQL는 선언적 SQL 결합 하는 언어에 있는 아무 눈금에는 데이터 toolet C# 명령적으로 처리 합니다. U-SQL의 hello 확장성, 분산 쿼리 기능을 통해 Azure SQL 데이터베이스 같은 관계형 저장소에서 데이터를 효율적으로 분석할 수 있습니다. U-SQL을 사용하면 읽기에 대한 스키마를 적용하고 사용자 지정 논리 및 UDF를 삽입하여 구조화되지 않은 데이터를 처리할 수 있습니다. 또한 U-SQL 포함 방법 세부적으로 제어를 제공 하는 확장성이 배율로 tooexecute 합니다. 

## <a name="learning-resources"></a>학습 리소스

* hello [U-SQL 자습서](http://aka.ms/usqltutorial) hello U-SQL 언어의 대부분의는 안내 방식된 연습을 제공 합니다. 이 문서 toolearn U-SQL 하려는 모든 개발자가 읽는 것이 좋습니다.
* Hello에 대 한 자세한 내용은 **U-SQL 언어 구문을**, hello 참조 [U SQL 언어 참조](http://go.microsoft.com/fwlink/p/?LinkId=691348)합니다.
* toounderstand hello **U-SQL 디자인 원칙**, hello Visual Studio 블로그 게시물을 참조 [소개 U-SQL – 쉽게 빅 데이터 처리 하는 언어](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/)합니다.

## <a name="prerequisites"></a>필수 조건

이 문서에 hello U-SQL 샘플을 통한 진행 하기 전에 읽고 완료 [자습서: 데이터 레이크 도구를 사용 하 여 Visual Studio에 대 한 개발 U-SQL 스크립트](data-lake-analytics-data-lake-tools-get-started.md)합니다. 해당 자습서는 Azure 데이터 레이크 도구로 U-SQL를 사용 하 여 Visual studio의 hello 메커니즘을 설명 합니다.

## <a name="your-first-u-sql-script"></a>첫 번째 U-SQL 스크립트

U-SQL 스크립트를 다음 hello은 단순 하며 많은 측면 hello U-SQL 언어를 탐색할 수 있습니다.

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
    USING Extractors.Tsv();

OUTPUT @searchlog   
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

이 스크립트에는 변환 단계가 없습니다. 호출 하는 hello 소스 파일에서 읽을 `SearchLog.tsv`schematizes, 및 hello 행 집합을 다시 첫 번째 u sql.csv SearchLog 라는 파일에 기록 합니다.

Hello 매개 변수 다음 toohello 데이터 형식에 hello 확인 `Duration` 필드입니다. 해당 hello 의미 `Duration` 필드는 null 일 수 없습니다.

### <a name="key-concepts"></a>주요 개념
* **행 집합 변수**: 행 집합을 생성 하는 각 쿼리 식 tooa 변수를 할당할 수 있습니다. U-SQL hello T-SQL 변수 명명 패턴을 따릅니다 (`@searchlog`예를 들면) hello 스크립트에 있습니다.
* hello **추출** 키워드 파일에서 데이터를 읽고 읽기의 hello 스키마를 정의 합니다. `Extractors.Tsv`는 탭으로 구분된 값 파일에 대한 기본 제공 U-SQL 추출기입니다. 사용자 지정 추출기를 개발할 수 있습니다.
* hello **출력** 행 집합 tooa 파일에서 데이터를 씁니다. `Outputters.Csv()`기본 제공 U-SQL outputter toocreate 쉼표로 구분 된 값 파일입니다. 사용자 지정 출력기를 개발할 수 있습니다.

### <a name="file-paths"></a>파일 경로

hello 추출 및 문의 출력 파일 경로 사용 합니다. 파일 경로는 절대 경로 또는 상대 경로일 수 있습니다.

이 다음 절대 파일 경로 참조 라는 데이터 레이크 저장소의 tooa 파일 `mystore`:

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

다음에 나오는 이 파일 경로는 `"/"`로 시작합니다. Hello 기본 데이터 레이크 저장소 계정에서 tooa 파일 참조:

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a>스칼라 변수 사용

으로 사용할 수 있습니다 스칼라 변수 잘 toomake 스크립트 유지 관리 보다 쉽게 합니다. 으로 hello 이전 U-SQL 스크립트를 작성할 수도 있습니다.

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a>변환 행 집합

사용 하 여 **선택** tootransform 행 집합:

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

WHERE 절 사용 하 여 hello는 [C# 부울 식](https://msdn.microsoft.com/library/6a71f45d.aspx)합니다. Hello C# 식 언어 toodo 고유한 식 및 함수에 사용할 수 있습니다. 식 및 함수를 논리 결합(ANDs) 및 분리(ORs)와 결합하여 더 복잡한 필터링을 수행할 수 있습니다.

hello 다음 스크립트에서는 hello DateTime.Parse() 메서드 및 결합 합니다.

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 >hello 두 번째 쿼리는 두 개의 필터 hello의 합성을 만드는 hello 첫 번째 행의 hello 결과에 작동 합니다. 변수 이름으로도 다시 사용할 수 있습니다 및 hello 이름이 어휘 적으로 범위가 지정 됩니다.

## <a name="aggregate-rowsets"></a>집계 행 집합
친숙 한 ORDER BY, GROUP BY 및 집계 hello U-SQL 제공 합니다.

hello 다음 쿼리에서 hello 총 기간 / 지역당을 찾아 다음 순서로 hello 상위 5 개 기간이 표시 합니다.

U-SQL 행 집합에서 다음 쿼리 hello에 대 한 순서를 유지 하지 않습니다. 출력, 따라서 tooorder tooadd ORDER BY toohello 출력 문이 필요 합니다.

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

hello U-SQL ORDER BY 절 hello FETCH 절을 사용 하 여 SELECT 식에 필요 합니다.

hello U-SQL HAVING 절에 사용 되는 toorestrict hello 출력 toogroups hello HAVING 조건에 맞는 될 수 있습니다.

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

집계 고급 시나리오에 대 한 hello hello U-SQL 참조 설명서를 참조 하십시오. [분석, 집계 및 함수를 참조할](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)

## <a name="next-steps"></a>다음 단계
* [Microsoft Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)
* [Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md)
