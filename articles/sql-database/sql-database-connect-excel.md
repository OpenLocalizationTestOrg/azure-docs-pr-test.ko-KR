---
title: "aaaConnect Excel tooSQL 데이터베이스 | Microsoft Docs"
description: "Hello 클라우드에서 tooconnect Microsoft Excel tooAzure SQL 데이터베이스 하는 방법에 대해 알아봅니다. 보고 및 데이터 탐색을 위해 Excel로 데이터를 가져옵니다."
services: sql-database
keywords: "연결 toosql excel, 데이터 tooexcel 가져오기"
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a>Excel tooan Azure SQL 데이터베이스 연결 및 보고서 만들기

Hello 클라우드에서 Excel tooa SQL 데이터베이스를 연결 하 고 데이터를 가져올 테이블 및 hello 데이터베이스의 값에 따라 차트를 만듭니다. 데이터베이스 테이블, Excel에서는 hello 연결을 설정 하는이 자습서에서는 Excel 용 데이터 및 hello 연결 정보를 저장 하는 hello 파일을 저장 한 다음 hello에서 피벗 차트를을 데이터베이스 값 만듭니다.

시작하기 전에 Azure에서 SQL 데이터베이스가 필요합니다. 하나 없다면 참조 [첫 번째 SQL 데이터베이스를 만듭니다.](sql-database-get-started-portal.md) tooget 데이터베이스 샘플 데이터로 설정 하 고 잠시 후에 작동 합니다. 이 문서에서는 해당 문서에서 샘플 데이터를 Excel에 가져오지만 고유의 데이터에서 비슷한 단계를 따를 수 있습니다.

또한 Excel의 사본이 필요합니다. 이 문서는 [Microsoft Excel 2016](https://products.office.com/)를 사용합니다.

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a>Excel tooa SQL 데이터베이스를 연결 하 고 odc 파일을 만들
1. tooconnect Excel tooSQL 데이터베이스 Excel을 열고 새 통합 문서를 만들거나 기존 Excel 통합 문서를 엽니다.
2. Hello hello 페이지 위쪽에 hello 메뉴 모음에서 클릭 **데이터**, 클릭 **기타 원본**, 클릭 하 고 **SQL Server에서**합니다.
   
   ![데이터 원본 선택: Excel tooSQL 데이터베이스를 연결 합니다.](./media/sql-database-connect-excel/excel_data_source.png)
   
   hello 데이터 연결 마법사가 열립니다.
3. Hello에 **tooDatabase 서버 연결** 대화 상자에서 SQL 데이터베이스 유형 hello **서버 이름** tooconnect tooin hello 양식 표시할 <*servername* > **. database.windows.net**합니다. 예를 들어 **adworkserver.database.windows.net**입니다.
4. 아래 **로그온 자격 증명**, 클릭 **다음 사용자 이름 및 암호 사용 하 여 hello**, 형식 hello **사용자 이름** 및 **암호** 에 설정 SQL 데이터베이스 서버를 만들 때 hello 및 클릭 **다음**합니다.
   
   ![Hello 서버 이름 및 로그인 자격 증명을 입력 합니다.](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > 네트워크 환경에 따라 수 tooconnect 수 또는 hello SQL 데이터베이스 서버에 클라이언트 IP 주소의 트래픽을 허용 하지 않으면 hello 연결 손실 될 수 있습니다. Toohello 이동 [Azure 포털](https://portal.azure.com/)SQL 서버, 서버 클릭 하 여, 방화벽 설정에서 클릭을 클라이언트 IP 주소를 추가 합니다. 참조 [tooconfigure 방화벽 설정을 어떻게](sql-database-configure-firewall-settings.md) 대 한 자세한 내용은 합니다.
   > 
   > 
5. Hello에 **데이터베이스 및 테이블 선택** 대화 상자에서 선택 hello 데이터베이스 toowork와 hello 목록에서 선택 하 고 hello 테이블이 나 뷰를 toowork 원하는 클릭 합니다 (선택한 **vGetAllCategories**), 한 다음 클릭 **다음**합니다.
   
    ![데이터베이스 및 테이블 선택](./media/sql-database-connect-excel/select-database-and-table.png)
   
    hello **데이터 연결 파일 저장 및 마침** Excel에서 사용 하는 hello Office 데이터베이스 연결 (*.odc) 파일에 대 한 정보를 입력할 수 있는 대화 상자가 열립니다. Hello 기본값 그대로 두고 하거나 선택 항목을 사용자 지정할 수 있습니다.
6. 참고 hello 하지만 hello 기본값을 그대로 두면 **파일 이름** 특히 합니다. A **설명**, **이름**, 및 **검색 키워드** 도와주 고, 다른 사용자가 연결 하려는 기억 tooand hello 연결을 찾을 합니다. 클릭 **항상 시도 toouse이 파일 toorefresh 데이터** tooit를 연결 하 고 클릭 하는 경우 업데이트할 수 있습니다 hello odc 파일에 저장 된 연결 정보를 원하는 경우 **마침**합니다.
   
    ![odc 파일 저장](./media/sql-database-connect-excel/save-odc-file.png)
   
    hello **데이터를 가져올** 대화 상자가 나타납니다.

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a>Excel로 hello 데이터 가져오기 및 피벗 차트 만들기
Hello 연결 및 데이터 및 연결 정보로 만든된 hello 파일 설정 했으므로 tooimport hello 데이터를 보고 합니다.

1. Hello에 **데이터 가져오기** 대화 상자에서 hello 워크시트에서 데이터를 제공할 원하는 hello 옵션을 클릭 한 다음 클릭 **확인**합니다. **PivotChart**를 선택했습니다. Toocreate 선택할 수도 있습니다는 **새 워크시트** 또는 너무**이 데이터 tooa 데이터 모델 추가**합니다. 데이터 모델에 대한 자세한 내용은 [Excel에서 데이터 모델 만들기](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B)를 참조하세요. 클릭 **속성** hello 이전 단계와 toochoose 새로 고침 옵션을 hello 데이터에서 만든 hello odc 파일에 대 한 tooexplore 정보입니다.
   
    ![Excel에서 데이터에 대 한 hello 형식 선택](./media/sql-database-connect-excel/import-data.png)
   
    이제 hello 워크시트에 빈 피벗 테이블 및 차트입니다.
2. 아래 **피벗 테이블 필드**, tooview 원하는 필드를 hello 모든 hello에 대 한 확인란을 선택 합니다.
   
    ![데이터베이스 보고서를 구성합니다.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> 다른 Excel 통합 문서 및 워크시트 toohello 데이터베이스 tooconnect 원하는 클릭 **데이터**, 클릭 **연결**, 클릭 **추가**, 만든 hello 연결을 선택 hello 목록에서 **열려**합니다.
> ![다른 통합 문서에서 연결 열기](./media/sql-database-connect-excel/open-from-another-workbook.png)
> 
> 

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[tooSQL 데이터베이스 SQL Server Management Studio를 사용 하 여 연결](sql-database-connect-query-ssms.md) 고급 쿼리 및 분석 합니다.
* Hello 이점에 대 한 자세한 내용은 [탄력적 풀](sql-database-elastic-pool.md)합니다.
* 너무 방법에 대해 알아봅니다[tooSQL 데이터베이스 hello 백 엔드에 연결 하는 웹 응용 프로그램 만들기](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md)합니다.

