---
title: "hello Azure Analysis Services 웹 디자이너를 사용 하 여 테이블 형식 모델 aaaCreate | Microsoft Docs"
description: "Toocreate Azure Analysis Services 테이블 형식 모델 사용 하 여 Azure 포털에서 웹 디자이너 hello 하는 방법에 대해 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a>Azure Portal에서 모델 만들기

Azure 포털의 hello Azure Analysis Services 웹 디자이너 (미리 보기) 기능 쉽고 빠르게 toocreate 제공 하 고 테이블 형식 모델 및 쿼리 모델 브라우저에서 직접 데이터를 편집 합니다. 

염두에서에 둬야, hello 웹 디자이너는 **미리 보기**합니다. 새로운 기능 미리 보기에서 모든 hello 시간을 추가 하는 기능이 제한 됩니다. 더 많은 고급 모델 개발 및 테스트에 대 한 최상의 toouse Visual Studio (SSDT) 및 SQL Server Management Studio (SSMS) 않습니다.

## <a name="prerequisites"></a>필수 조건

- Hello Standard 또는 Developer 계층에서 사용 되는 Azure Analysis Services 서버입니다. Hello 웹 디자이너를 사용 하 여 생성 하는 새 모델은 DirectQuery를 사용할 경우 이러한 계층 에서만 지원 됩니다.
- 데이터 원본으로 Azure SQL Database, Azure SQL Data Warehouse 또는 Power BI Desktop(.pbix) 파일. Power BI Desktop 파일로 만드는 새 모델은 Azure SQL Database, Azure SQL Data Warehouse, Oracle 및 Teradata 데이터 원본을 지원합니다.
- SQL Server 계정 및 tooAzure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 데이터 원본에 연결 하기 위한 암호입니다.

## <a name="toocreate-a-new-tabular-model"></a>toocreate 새 테이블 형식 모델

1. 서버의 **개요** 블레이드 > **웹 디자이너**에서 **열기**를 클릭합니다.

    ![Azure Portal에서 모델 만들기](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. **웹 디자이너** > **모델**에서 **+ 추가**를 클릭합니다.

    ![Azure Portal에서 모델 만들기](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. **새 모델**에서 모델 이름을 입력한 다음 데이터 원본을 선택합니다.

    ![Azure Portal의 새 모델 대화 상자](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. **연결**, hello 연결 속성을 입력 합니다. 사용자 이름 및 암호는 SQL Server 계정이어야 합니다.

     ![Azure Portal의 연결 대화 상자](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. **테이블 및 뷰**hello 테이블 tooinclude에서 모델을 선택한 다음 클릭 **만들기**합니다. 키 쌍을 사용하여 테이블 간의 관계가 자동으로 생성됩니다.

     ![테이블 및 보기 선택](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

새 모델이 브라우저에 나타납니다. 여기서 다음과 같은 일을 할 수 있습니다.   

- 필드 toohello 쿼리 디자이너를 끌어서 필터를 추가 하 여 모델 데이터를 쿼리 합니다.
- 테이블에 새 측정값을 만듭니다.
- Hello json 편집기를 사용 하 여 모델 메타 데이터를 편집 합니다.
- Visual Studio (SSDT), Power BI Desktop 또는 Excel에서 hello 모델을 엽니다.

![테이블 및 보기 선택](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> 모델 메타 데이터를 편집 하거나 브라우저에서 새 측정값을 만들 때 Azure에서 해당 변경 내용을 tooyour 모델을 저장 하 합니다. SSDT, Power BI Desktop 또는 Excel에서 모델을 작업하는 경우에도 모델이 동기화되지 않을 수 있습니다.


## <a name="next-steps"></a>다음 단계 
[데이터베이스 역할 및 사용자 관리](analysis-services-database-users.md)  
[Excel과 연결](analysis-services-connect-excel.md)  


