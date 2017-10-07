---
title: "Power BI를 사용 하 여 데이터 레이크 저장소의 데이터를 aaaAnalyze | Microsoft Docs"
description: "Azure 데이터 레이크 저장소에 저장 된 Power BI tooanalyze 데이터를 사용 하 여"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a>Power BI를 사용하여 Data Lake 저장소의 데이터 분석
이 문서에 설명 합니다 방법을 toouse Power BI Desktop tooanalyze 및 Azure 데이터 레이크 저장소에 저장 된 데이터를 시각화 합니다.

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure Data Lake Store 계정**. Hello 지침에 따라 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다. 이 문서에서는 호출에 데이터 레이크 저장소 계정이 이미 만들었다고 가정 **mybidatalakestore**, 예제 데이터 파일을 업로드 (**Drivers.txt**) tooit 합니다. 이 샘플 파일은 [Azure Data Lake Git 리포지토리](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)에서 다운로드할 수 있습니다.
* **Power BI Desktop**. [Microsoft 다운로드 센터](https://www.microsoft.com/en-us/download/details.aspx?id=45331)에서 다운로드할 수 있습니다. 

## <a name="create-a-report-in-power-bi-desktop"></a>Power BI Desktop에서 보고서 만들기
1. 컴퓨터에서 Power BI Desktop을 시작합니다.
2. Hello에서 **홈** 리본에서 클릭 **데이터 가져오기**, 자세히를 클릭 합니다. Hello에 **데이터 가져오기** 대화 상자를 클릭 **Azure**, 클릭 **Azure 데이터 레이크 저장소**, 클릭 하 고 **연결**합니다.
   
    ![Connect tooData Lake 저장소](./media/data-lake-store-power-bi/get-data-lake-store-account.png "연결 tooData Lake 저장소")
3. 개발 단계에 있는 것 hello 커넥터에 대 한 대화 상자를 표시 하는 경우 toocontinue 방법을 선택 합니다.
4. Hello에 **Microsoft Azure 데이터 레이크 저장소** 대화 상자, hello URL tooyour Data Lake 저장소 계정에를 입력 한 다음 **확인**합니다.
   
    ![Data Lake Store URL](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "Data Lake Store URL")
5. Hello 다음 대화 상자에서 클릭 **로그인** toosign Data Lake 저장소 계정에 있습니다. 됩니다 tooyour 조직의 로그인 페이지로 리디렉션됩니다. Hello 프롬프트 toosign hello 계정으로 수행 합니다.
   
    ![Data Lake Store에 로그인](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Data Lake Store에 로그인")
6. 성공적으로 로그인한 후에 **연결**을 클릭합니다.
   
    ![Connect tooData Lake 저장소](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "연결 tooData Lake 저장소")
7. 다음 대화 상자 hello tooyour 데이터 레이크 저장소 계정에 업로드할 hello 파일을 보여 줍니다. Hello 정보를 확인 한 다음 클릭 **부하**합니다.
   
    ![Data Lake Store에서 데이터 로드](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Data Lake Store에서 데이터 로드")
8. Hello 데이터가 Power BI에 성공적으로 로드 된 hello의 필드를 다음 hello 나타납니다 **필드** 탭 합니다.
   
    ![가져온 필드](./media/data-lake-store-power-bi/imported-fields.png "가져온 필드")
   
    그러나 toovisualize hello 데이터를 분석 하 고, hello 데이터 toobe 필드 뒤 hello 당 사용 가능한 것이 좋습니다
   
    ![원하는 필드](./media/data-lake-store-power-bi/desired-fields.png "원하는 필드")
   
    Hello 다음 단계에서 hello 쿼리 tooconvert hello 가져온 데이터를 원하는 형식 hello 업데이트 됩니다.
9. Hello에서 **홈** 리본에서 클릭 **쿼리 편집**합니다.
   
    ![쿼리 편집](./media/data-lake-store-power-bi/edit-queries.png "쿼리 편집")
10. Hello에서 hello 쿼리 편집기에서에서 **콘텐츠** 열을 클릭 하 여 **이진**합니다.
    
    ![쿼리 편집](./media/data-lake-store-power-bi/convert-query1.png "쿼리 편집")
11. Hello를 나타내는 파일 아이콘을 나타납니다 **Drivers.txt** 업로드 한 파일입니다. Hello 파일을 마우스 오른쪽 단추로 클릭 하 고 클릭 **CSV**합니다.    
    
    ![쿼리 편집](./media/data-lake-store-power-bi/convert-query2.png "쿼리 편집")
12. 아래와 같이 출력이 표시됩니다. 데이터는 toocreate 시각화를 사용할 수 있는 형식으로 제공 되었습니다.
    
    ![쿼리 편집](./media/data-lake-store-power-bi/convert-query3.png "쿼리 편집")
13. Hello에서 **홈** 리본에서 클릭 **닫고 적용**, 클릭 하 고 **닫고 적용**합니다.
    
    ![쿼리 편집](./media/data-lake-store-power-bi/load-edited-query.png "쿼리 편집")
14. Hello 쿼리를 업데이트 후 hello **필드** 탭 hello 시각화에 사용할 수 있는 새 필드가 표시 됩니다.
    
    ![업데이트된 필드](./media/data-lake-store-power-bi/updated-query-fields.png "업데이트된 필드")
15. 주세요 특정된 국가 대 한 각 도시에 원형 차트 toorepresent hello 드라이버를 만듭니다. 따라서 toodo 다음 항목을 선택 하는 hello를 확인 해야 합니다.
    
    1. Hello 시각화 탭에서 원형 차트에 대 한 hello 기호를 클릭 합니다.
       
        ![원형 차트 만들기](./media/data-lake-store-power-bi/create-pie-chart.png "원형 차트 만들기")
    2. toouse는 하겠습니다 hello 열 **열 4** (hello 도시 이름) 및 **열 7** (hello 국가 이름). 이러한 열을 끌어 **필드** 너무 탭**시각화** 아래와 같이 탭 합니다.
       
        ![시각화 만들기](./media/data-lake-store-power-bi/create-visualizations.png "시각화 만들기")
    3. hello 아래와 같은 hello 원형 차트 같아야 합니다.
       
        ![원형 차트](./media/data-lake-store-power-bi/pie-chart.png "시각화 만들기")
16. Hello 페이지 수준 필터에서 특정 국가 선택 하면 선택한 hello 국가의 각 도시에 있는 드라이버 hello 수 이제 볼 수 있습니다. 예를 들어 hello에서 **시각화** 탭의 **페이지 수준 필터**선택, **브라질**합니다.
    
    ![국가 선택](./media/data-lake-store-power-bi/select-country.png "국가 선택")
17. hello 원형 차트는 브라질의 hello 도시에 자동으로 업데이트 된 toodisplay hello 드라이버입니다.
    
    ![국가의 드라이버](./media/data-lake-store-power-bi/driver-per-country.png "국가별 드라이버")
18. Hello에서 **파일** 메뉴를 클릭 하 여 **저장** toosave hello 시각화를 Power BI Desktop 파일로 합니다.

## <a name="publish-report-toopower-bi-service"></a>보고서 tooPower BI 서비스를 게시 합니다.
Power BI Desktop에서 hello 시각화를 만든 후 toohello Power BI 서비스를 게시 하 여 다른 사용자와 공유할 수 있습니다. 방법에 대 한 참조는 toodo [Power BI Desktop에서 게시](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/)합니다.

## <a name="see-also"></a>참고 항목
* [Data Lake 분석을 사용하여 Data Lake 저장소의 데이터 분석](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

