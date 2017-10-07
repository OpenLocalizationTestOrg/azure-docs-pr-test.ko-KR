---
title: "Azure 포털을 사용 하 여 aaaTroubleshoot Azure Data Lake 분석 작업 | Microsoft Docs"
description: "어떻게 toouse hello Azure 포털 tootroubleshoot Data Lake 분석 작업에 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a>Azure 포털을 사용하여 Azure 데이터 레이크 분석 작업 문제 해결
어떻게 toouse hello Azure 포털 tootroubleshoot Data Lake 분석 작업에 알아봅니다.

이 자습서에서는 누락 된 소스 파일 문제를 설정 및 hello Azure 포털 tootroubleshoot hello 문제를 사용 합니다.

## <a name="submit-a-data-lake-analytics-job"></a>데이터 레이크 분석 작업 제출

U-SQL 작업을 수행 하는 hello를 제출 합니다.

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
hello hello 스크립트에 정의 된 소스 파일은 **/Samples/Data/SearchLog.tsv1**, 여야 함 **/Samples/Data/SearchLog.tsv**합니다.


## <a name="troubleshoot-hello-job"></a>Hello 작업 문제 해결

**toosee 모든 hello 작업**

1. Hello Azure 포털에서에서 클릭 **Microsoft Azure** hello 왼쪽된 위 모퉁이에 있습니다.
2. Data Lake 분석 계정 이름과 함께 hello 타일을 클릭 합니다.  hello에 표시 되는 hello 작업 요약 **작업 관리** 바둑판식으로 배열입니다.

    ![Azure 데이터 레이크 분석 작업 관리](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    hello 작업 관리의 hello 작업 상태 보기를 제공합니다. 실패한 작업이 있는지 확인합니다.
3. Hello 클릭 **작업 관리** toosee hello 작업 바둑판식으로 배열 합니다. hello 작업으로 분류 됩니다 **실행**, **큐 대기**, 및 **종료 됨**합니다. Hello에 실패 한 작업 표시 **종료 됨** 섹션. Hello 목록의 첫 번째 여야 합니다. 많은 작업을 사용 하는 경우 클릭할 수 있는 **필터** toohelp toolocate 작업이 있습니다.

    ![Azure 데이터 레이크 분석 필터 작업](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. Hello hello 목록 tooopen hello에서에서 작업 세부 정보는 새 블레이드가에서 실패 한 작업을 클릭 합니다.

    ![Azure 데이터 레이크 분석 실패 작업](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    공지 hello **다시 전송** 단추입니다. Hello 문제를 해결 한 후에 hello 작업을 다시 전송할 수 있습니다.
5. Hello 이전 스크린 샷 tooopen hello 오류 정보에서 강조 표시 된 부분을 클릭 합니다.  다음과 같이 표시됩니다.

    ![Azure 데이터 레이크 분석 실패 작업 세부 정보](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    Hello 소스 폴더를 찾지 알려 줍니다.
6. **Duplicate Script**(스크립트 복제)를 클릭합니다.
7. 업데이트 hello **FROM** 경로 toohello 다음:

    "/Samples/Data/SearchLog.tsv"
8. **작업 제출**을 클릭합니다.

## <a name="see-also"></a>참고 항목
* [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)
* [Azure PowerShell을 사용하여 Azure 데이터 레이크 분석 시작](data-lake-analytics-get-started-powershell.md)
* [Visual Studio를 사용하여 Azure 데이터 레이크 분석 및 U-SQL 시작](data-lake-analytics-u-sql-get-started.md)
* [Azure 포털을 사용하여 Azure 데이터 레이크 분석 관리](data-lake-analytics-manage-use-portal.md)
