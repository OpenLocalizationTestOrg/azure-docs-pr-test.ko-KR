---
title: "Azure 포털을 사용 하 여 Azure Data Lake 분석 시작 aaaGet | Microsoft Docs"
description: "Toouse hello Azure 포털 toocreate Data Lake 분석 계정 U SQL을 사용 하 여 데이터 레이크 분석 작업 만들기 하 고 hello 작업을 제출 하는 방법을 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a>Azure Portal을 사용하여 Azure Data Lake Analytics 시작
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

에 작업을 정의 어떻게 toouse hello Azure 포털 toocreate Azure Data Lake 분석 계정에 알아봅니다 [U-SQL](data-lake-analytics-u-sql-get-started.md), 및 toohello Data Lake 분석 서비스 작업을 제출 합니다. 데이터 레이크 분석에 대한 자세한 내용은 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

이 자습서를 시작하기 전에 **Azure 구독**이 있어야 합니다. [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.

## <a name="create-a-data-lake-analytics-account"></a>Data Lake 분석 계정 만들기

이제 데이터 레이크 분석을 만들고 동일한 hello에 데이터 레이크 저장소 계정 시간입니다.  이 단계는 간단 하 고 60 초 toofinish 초가 소요만 합니다.

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. **새로 만들기** >  **데이터 + 분석** > **Data Lake Analytics**를 클릭합니다.
3. 다음 항목 hello에 대 한 값을 선택 합니다.
   * **이름**: Data Lake Analytics 계정의 이름을 지정합니다(소문자와 숫자만 허용).
   * **구독**: hello hello 분석 계정에 사용 되는 Azure 구독을 선택 합니다.
   * **리소스 그룹**. 기존 Azure 리소스 그룹을 선택하거나 리소스 그룹을 새로 만듭니다.
   * **위치** - Hello Data Lake 분석 계정에 대 한 Azure 데이터 센터를 선택 합니다.
   * **데이터 레이크 저장소**: hello 명령 toocreate 새 Data Lake 저장소 계정에 따라 하거나 기존 템플릿을 선택 합니다. 
4. 필요에 따라 Data Lake Analytics 계정에 대한 가격 책정 계층을 선택합니다.
5. **만들기**를 클릭합니다. 


## <a name="your-first-u-sql-script"></a>첫 번째 U-SQL 스크립트

텍스트 다음 hello는 매우 간단한 U-SQL 스크립트입니다. Hello 스크립트 내에서 작은 데이터 집합을 정의 하 고 다음 이라는 파일로 toohello 기본 데이터 레이크 저장소 아웃 해당 데이터 집합을 작성 하는 것이 전부 `/data.csv`합니다.

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

## <a name="submit-a-u-sql-job"></a>U-SQL 작업 제출

1. Data Lake 분석 계정 hello에서 클릭 **새 작업**합니다.
2. U-SQL 스크립트를 위에 표시 된 hello hello 텍스트에 붙여 넣습니다. 
3. **작업 제출**을 클릭합니다.   
4. 너무 hello 작업 상태가 변경 될 때까지 기다렸다가**Succeeded**합니다.
5. Hello 작업에 실패 한 경우 참조 [모니터 데이터 레이크 분석 문제를 해결 하 고](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)합니다.
6. Hello 클릭 **출력** 탭을 클릭 한 다음 `data.csv`합니다. 

## <a name="see-also"></a>참고 항목

* U-SQL 응용 프로그램 개발 시작 tooget 참조 [데이터 레이크 도구를 사용 하 여 Visual Studio에 대 한 개발 U-SQL 스크립트](data-lake-analytics-data-lake-tools-get-started.md)합니다.
* toolearn U SQL 참조 [Azure 데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)합니다.
* 관리 작업을 보려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.
