---
title: "Visual Studio에 대 한 데이터 레이크 도구를 사용 하 여 aaaDevelop U-SQL 스크립트 | Microsoft Docs"
description: "Tooinstall 데이터 레이크 Tools for Visual Studio 방법 등에 대해 알아보기 toodevelop 및 테스트 U-SQL 스크립트입니다."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a>Data Lake Tools for Visual Studio를 사용하여 U-SQL 스크립트 개발
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


자세한 내용은 toouse Visual Studio toocreate Azure Data Lake 분석 계정에 있는 작업을 정의 하는 방법을 [U-SQL](data-lake-analytics-u-sql-get-started.md), 및 toohello Data Lake 분석 서비스 작업을 제출 합니다. 데이터 레이크 분석에 대한 자세한 내용은 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.


## <a name="prerequisites"></a>필수 조건

* **Visual Studio**: Express를 제외한 모든 버전이 지원됩니다.
    * Visual Studio 2017
    * Visual Studio 2015
    * Visual Studio 2013
* **.NET용 Microsoft Azure SDK** 버전 2.7.1 이상.  Hello를 사용 하 여 설치 [웹 플랫폼 설치 관리자](http://www.microsoft.com/web/downloads/platform.aspx)합니다.
* **Data Lake Analytics** 계정. 계정에는 toocreate 참조 [Azure 포털을 사용 하 여 Azure Data Lake 분석 시작](data-lake-analytics-get-started-portal.md)합니다.

## <a name="install-azure-data-lake-tools-for-visual-studio"></a>Azure Data Lake Tools for Visual Studio 설치 

다운로드 하 여 Azure 데이터 레이크 Tools for Visual Studio 설치 [hello 다운로드 센터에서에서](http://aka.ms/adltoolsvs)합니다. 설치가 끝나면 다음을 확인할 수 있습니다.
* hello **서버 탐색기** > **Azure** 노드를 포함 한 **Data Lake 분석** 노드. 
* hello **도구** 메뉴에는 **데이터 레이크** 항목입니다.

## <a name="connect-tooan-azure-data-lake-analytics-account"></a>Tooan Azure Data Lake 분석 계정을 연결 하세요.

1. Visual Studio를 엽니다.
2. **보기** > **서버 탐색기**를 선택하여 서버 탐색기를 엽니다.
3. **Azure**를 마우스 오른쪽 단추로 클릭합니다. 그런 다음 선택 **tooMicrosoft Azure 구독 연결** hello 지침을 따릅니다.
4. 서버 탐색기에서 선택 **Azure** > **Data Lake Analytics**를 선택합니다. Data Lake Analytics 계정 목록이 표시됩니다.


## <a name="write-your-first-u-sql-script"></a>첫 번째 U-SQL 스크립트 작성

hello 텍스트 다음은 간단한 U-SQL 스크립트입니다. 작은 데이터 집합 및 데이터 집합 toohello 기본 데이터 레이크 저장소 파일로 라는 쓰기 정의 `/data.csv`합니다.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a>데이터 레이크 분석 작업 제출

1. **파일** > **새로 만들기** > **프로젝트**를 선택합니다.

2. 선택 hello **U-SQL 프로젝트** 종류를 선택한 다음 클릭 **확인**합니다. Visual Studio는 **Script.usql** 파일로 솔루션을 만듭니다.

3. Hello에 hello 앞의 스크립트를 붙여 **Script.usql** 창.

4. Hello의 hello 왼쪽 위 모서리에 **Script.usql** 창의 hello Data Lake 분석 계정을 지정 합니다.

    ![U-SQL Visual Studio 프로젝트 제출](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. Hello의 hello 왼쪽 위 모서리에 **Script.usql** 창에서 **전송**합니다.
6. Hello 확인 **분석 계정**를 선택한 후 **전송**합니다. Hello 전송이 완료 된 후 제출 결과 hello 데이터 레이크 Tools for Visual Studio 결과에 표시 됩니다.

    ![U-SQL Visual Studio 프로젝트 제출](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. toosee hello 최신 작업 상태 및 새로 고침 hello 화면을 클릭 하 여 **새로 고침**합니다. Hello 표시 hello 작업 성공 시 **작업 그래프**, **메타 데이터 작업**, **상태 기록**, 및 **진단**:

    ![U-SQL Visual Studio 데이터 레이크 분석 작업 성능 그래프](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * **작업 요약** 표시 hello hello 작업의 요약입니다.   
   * **작업 세부 정보** hello 스크립트, 리소스 및 꼭 짓 점을 포함 하 여 hello 작업에 대 한 보다 구체적인 정보를 표시 합니다.
   * **작업 그래프** hello 작업의 hello 진행률을 시각화 합니다.
   * **메타 데이터 작업** hello U-SQL 카탈로그에 대해 수행 된 모든 hello 작업을 보여 줍니다.
   * **데이터** 모든 hello 입 / 출력을 보여 줍니다.
   * **진단**에서는 작업 실행 및 성능 최적화에 대한 고급 분석을 제공합니다.

### <a name="toocheck-job-state"></a>toocheck 작업 상태

1. 서버 탐색기에서 선택 **Azure** > **Data Lake Analytics**를 선택합니다. 
2. Hello Data Lake 분석 계정 이름을 확장 합니다.
3. **작업**을 두 번 클릭합니다.
4. 이전에 제출 hello 작업을 선택 합니다.

### <a name="toosee-hello-output-of-a-job"></a>작업의 toosee hello 출력

1. 서버 탐색기에서 제출한 toohello 작업을 찾습니다.
2. Hello 클릭 **데이터** 탭 합니다.
3. Hello에 **작업 출력** 탭, 선택 hello `"/data.csv"` 파일입니다.

## <a name="next-steps"></a>다음 단계

* [테스트 및 디버깅을 위해 고유한 워크스테이션에서 U-SQL 스크립트 실행](data-lake-analytics-data-lake-tools-local-run.md)
* [U-SQL 작업에서 C# 코드 디버그](data-lake-analytics-debug-u-sql-jobs.md)
* [Visual Studio 코드에 대 한 hello Azure 데이터 레이크 도구를 사용 합니다.](data-lake-analytics-data-lake-tools-for-vscode.md)
