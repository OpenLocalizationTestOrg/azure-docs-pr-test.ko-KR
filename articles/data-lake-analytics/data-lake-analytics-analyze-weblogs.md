---
title: "Azure 데이터 레이크 분석을 사용 하 여 웹 사이트 aaaAnalyze 로그 | Microsoft Docs"
description: "데이터 레이크 분석을 사용 하 여 웹 사이트 tooanalyze을 기록 하는 방법에 대해 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a>Azure Data Lake Analytics를 사용하여 웹 사이트 로그 분석
Toovisit hello 웹 사이트를 만들려고 tooanalyze 웹 사이트 로그는 참조 페이지 찾기에 특히 Data Lake 분석을 사용 하 여 오류가 발생 했습니다 방법에 대해 알아봅니다.

## <a name="prerequisites"></a>필수 조건
* **Visual Studio 2015 또는 Visual Studio 2013**.
* **[Visual Studio용 Data Lake 도구](http://aka.ms/adltoolsvs)**.

    데이터 레이크 Tools for Visual Studio가 설치 되 면 표시 됩니다는 **데이터 레이크** hello에서 항목 **도구** Visual Studio에서 메뉴:

    ![U-SQL Visual Studio 메뉴](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* **데이터 레이크 분석 워크 로드와 hello 데이터 레이크 Tools for Visual Studio에 대 한 기본 지식이**합니다. 시작 tooget 참조:

  * [Visual Studio용 데이터 레이크 도구를 사용하여 U-SQL 스크립트 개발](data-lake-analytics-data-lake-tools-get-started.md).
* **데이터 레이크 분석 계정.**  [Azure Data Lake Analytics 계정 만들기](data-lake-analytics-get-started-portal.md)를 참조하세요.
* **Hello 샘플 데이터 toohello Data Lake 분석 계정에 업로드 합니다.** 참조 [toocopy 예제 데이터 파일과](data-lake-analytics-get-started-portal.md)합니다.

    데이터 레이크 분석 작업 toorun 일부 데이터가 필요 합니다. 데이터 레이크 도구 hello 업로드 데이터를 지 원하는 경우에이 자습서 쉽게 toofollow hello 포털 tooupload hello 샘플 데이터 toomake 사용 합니다.

## <a name="connect-tooazure"></a>TooAzure 연결
빌드 및 모든 U-SQL 스크립트를 테스트 수, 전에 tooAzure 먼저 연결 해야 합니다.

**tooconnect tooData Lake 분석**

1. Visual Studio를 엽니다.
2. **Data Lake > 옵션 및 설정**을 클릭합니다.
3. 클릭 **로그인**, 또는 **사용자 변경** 경우 사용자가에 로그인을 hello 지침을 따릅니다.
4. 클릭 **확인** tooclose hello 옵션 및 설정 대화 상자.

**toobrowse Data Lake 분석 계정**

1. Visual Studio에서 **CTRL+ALT+S**를 눌러 **서버 탐색기**를 엽니다.
2. **서버 탐색기**에서 **Azure**를 확장한 후 **Data Lake Analytics**을 확장합니다. 계정이 있을 경우 해당 데이터 레이크 분석 계정 목록이 표시됩니다. Data Lake 분석 계정 hello studio에서 만들 수 없습니다. 계정에는 toocreate 참조 [Azure 포털을 사용 하 여 Azure Data Lake 분석 시작](data-lake-analytics-get-started-portal.md) 또는 [Azure PowerShell을 사용 하 여 Azure Data Lake 분석 시작](data-lake-analytics-get-started-powershell.md)합니다.

## <a name="develop-u-sql-application"></a>U-SQL 응용 프로그램 개발
U-SQL 응용 프로그램은 대부분 U-SQL 스크립트입니다. U SQL에 대해 자세히 toolearn 참조 [U-SQL 시작](data-lake-analytics-u-sql-get-started.md)합니다.

추가 사용자 정의 연산자 toohello 응용 프로그램을 추가할 수 있습니다.  자세한 내용은 [데이터 레이크 분석 작업을 위한 U-SQL 사용자 정의 연산자 개발](data-lake-analytics-u-sql-develop-user-defined-operators.md)을 참조하십시오.

**toocreate Data Lake 분석 작업을 제출 하 고**

1. Hello 클릭 **파일 > 새로 만들기 > 프로젝트**합니다.
2. Hello U-SQL 프로젝트 형식을 선택 합니다.

    ![새 U-SQL Visual Studio 프로젝트](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. **확인**을 클릭합니다. Visual studio는 Script.usql 파일로 솔루션을 만듭니다.
4. Hello 스크립트 hello Script.usql 파일에 다음을 입력 합니다.

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    toounderstand hello U SQL 참조 [데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)합니다.    
5. 새로운 U-SQL 스크립트 tooyour 프로젝트에 추가 하 고 hello 다음을 입력 합니다.

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. U-SQL 스크립트를 첫 번째 백 toohello 전환한 다음 toohello **전송** 단추, 분석 계정을 지정 합니다.
7. **솔루션 탐색기**에서 **Script.usql**을 마우스 오른쪽 클릭하고 **빌드 스크립트**를 클릭합니다. Hello 출력 창에 hello 결과 확인 합니다.
8. **솔루션 탐색기**에서 **Script.usql**을 마우스 오른쪽 단추로 클릭하고 **스크립트 제출**을 클릭합니다.
9. Hello 확인 **분석 계정** 는 hello toorun hello 작업 하 고 클릭 하나 **전송**합니다. 제출 결과 및 작업 링크는 hello 전송이 완료 되 면 Visual Studio 결과 창에 대 한 hello 데이터 레이크 도구에서에서 사용할 수 있는입니다.
10. Hello 작업이 성공적으로 완료 될 때까지 기다립니다.  Hello 작업에 실패 한 경우 hello 소스 파일을 가능성이 없습니다.  이 자습서의 hello 필수 구성 요소 섹션을 참조 하십시오. 추가적인 문제 해결 정보는 [Azure 데이터 레이크 분석 작업 모니터링 및 문제 해결](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)을 참조하세요.

    Hello 작업이 완료 될 때 hello 화면에 따라 표시 되어야 합니다.

    ![데이터 레이크 분석은 웹 로그와 웹 사이트 로그를 분석합니다.](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. **Script1.usql**에 대해 7-10단계를 반복합니다.

**toosee hello 작업 출력**

1. **서버 탐색기**를 확장 하 고 **Azure**를 확장 하 고 **Data Lake 분석**, Data Lake 분석 계정, **저장소계정**hello 기본 데이터 레이크 저장소 계정을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **탐색기**합니다.
2. 두 번 클릭 **샘플** tooopen hello 폴더를 차례로 두 번 클릭 한 다음 **출력**합니다.
3. **UnsuccessfulResponsees.log**를 두 번 클릭합니다.
4. Toohello 출력 직접 순서 toonavigate에서 hello 작업의 hello 그래프 뷰 내 hello 출력 파일을 두 번 수도 있습니다.

## <a name="see-also"></a>참고 항목
다양 한 도구를 사용 하 여 Data Lake 분석 시작 tooget 참조:

* [Azure 포털을 사용하여 데이터 레이크 분석 시작](data-lake-analytics-get-started-portal.md)
* [Azure PowerShell을 사용하여 데이터 레이크 분석 시작](data-lake-analytics-get-started-powershell.md)
* [.NET SDK를 사용하여 데이터 레이크 분석 시작](data-lake-analytics-get-started-net-sdk.md)
