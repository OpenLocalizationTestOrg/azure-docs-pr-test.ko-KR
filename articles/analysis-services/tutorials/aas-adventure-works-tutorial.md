---
title: "aaa \"Azure Analysis Services Adventure Works 자습서 | \"Microsoft Docs"
description: "Azure Analysis Services에 대 한 hello Adventure Works 자습서 소개"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services - Adventure Works 자습서

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 자습서에서는 방법 단원을 제공 toocreate hello 1400 호환성 수준에서 테이블 형식 모델을 사용 하 여 배포 [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)합니다.  

새로운 tooAnalysis 서비스 및 테이블 형식 모델링을 하는 경우이 자습서를 완료 hello 가장 빠른 방법은 toolearn 어떻게는 toocreate 및 기본 테이블 형식 모델을 배포 합니다. Hello 필수 되 면 두 toothree 시간 toocomplete 간에 소요 될 위치에 있습니다.  
  
## <a name="what-you-learn"></a>학습 내용   
  
-   Hello에 toocreate 새 테이블 형식 모델 프로젝트 어떻게 **1400 호환성 수준이** SSDT에서 합니다.
  
-   어떻게 tooimport 데이터를 테이블 형식 모델 프로젝트에는 관계형 데이터베이스입니다.  
  
-   어떻게 toocreate 고 hello 모델의 테이블 간에 관계를 관리 합니다.  
  
-   어떻게 toocreate 계산 열, 측정값 및 핵심 성과 지표는 데 도움이 되는 중요 한 비즈니스 메트릭을 분석 합니다.  
  
-   어떻게 toocreate 비즈니스 사용자와 응용 프로그램별 뷰포인트를 제공 하 여 모델 데이터를 검색 하는 사용자가 보다 쉽게 수 있도록 하는 계층 및 큐브 뷰를 관리 합니다.  
  
-   어떻게 toocreate 파티션이 있는 테이블 데이터 더 작은 논리적 부분으로 분할 다른 파티션과 별개로 처리할 수 있는 합니다.  
  
-   어떻게 toosecure 사용자 멤버와 역할을 만들어 개체와 데이터를 모델링 합니다.  
  
-   어떻게 toodeploy 테이블 형식 모델 tooan **Azure Analysis Services** 서버 또는 온-프레미스 SQL Server 2017 Analysis Services 서버입니다.  
  
## <a name="prerequisites"></a>필수 조건  
toocomplete 해야이 자습서에서는:  
  
-   Azure Analysis Services 또는 SQL Server 2017 Analysis Services 모델에 toodeploy 인스턴스. [Azure Analysis Services 평가판](https://azure.microsoft.com/services/analysis-services/)을 등록하고 [서버를 만듭니다](../analysis-services-create-server.md). 또는 [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp)를 등록하여 다운로드합니다. 

-   SQL Server 데이터 웨어하우스 또는 hello로 Azure SQL 데이터 웨어하우스 [AdventureWorksDW2014 예제 데이터베이스](http://go.microsoft.com/fwlink/?LinkID=335807)합니다. 이 예제 데이터베이스 hello 데이터 필요한 toocomplete이이 자습서에 포함 됩니다. [SQL Server 평가판](https://www.microsoft.com/sql-server/sql-server-downloads)을 다운로드합니다. 또는 [Azure SQL Database 평가판](https://azure.microsoft.com/services/sql-database/)을 등록합니다. 

    **중요:** hello 예제 데이터베이스는 온-프레미스 SQL Server에 설치 하 고 모델 tooan Azure Analysis Services 서버를 배포 하는 [온-프레미스 데이터 게이트웨이](../analysis-services-gateway.md) 가 필요 합니다.

-   최신 버전의 hello [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)합니다.

-   최신 버전의 hello [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.    

-   [Power BI Desktop](https://powerbi.microsoft.com/desktop/) 또는 Excel과 같은 클라이언트 응용 프로그램. 

## <a name="scenario"></a>시나리오  
이 자습서는 가상의 회사인 Adventure Works Cycles를 기반으로 합니다. Adventure Works를 생성 하 고 자전거, 파트 및 액세서리 toocommercial 시장 북미, 유럽 및 아시아에서 배포 하는 대규모의 다국적 제조 회사입니다. hello 있으며 직원 수는 500 명입니다. 또한 Adventure Works는 시장 기반 전체에 대한 여러 지역별 영업 팀을 고용하고 있습니다. 프로젝트 toocreate 판매 및 마케팅 사용자 tooanalyze hello AdventureWorksDW 데이터베이스의 인터넷 매출 데이터에 대 한 테이블 형식 모델입니다.  
  
toocomplete hello 자습서에서는 다양 한 단원을 완료 해야 합니다. 각 단원에는 작업이 있습니다. 순서로 각 태스크를 완료 하는 것은 hello 단원을 완료 해야 합니다. 특정 단원에서 유사한 결과를 얻는 몇 가지 작업이 있을 수 있지만 각 작업을 완료하는 방법은 약간 다릅니다. 이 종종는 방법 보여 줍니다 두 개 이상의 한 가지 방법은 toocomplete 작업, 및 toochallenge 이전 단원 및 작업에서 배운 기술을 사용 하 여 있습니다.  
  
hello hello 단원의 목적은 tooguide SSDT에 포함 된 hello 기능을 많이 사용 하 여 기본 테이블 형식 모델 제작 하는 과정입니다. 각 단원 hello 이전 단원에는 빌드, 때문에 hello 단원을 순서 대로 완료 해야 합니다.
  
이 자습서 단원 SSMS를 사용 하거나 클라이언트를 사용 하 여 서버 또는 데이터베이스를 관리 하는 Azure 포털의 서버를 관리 하는 방법에 대 한 응용 프로그램 toobrowse 모델 데이터 제공 하지 않습니다. 


## <a name="lessons"></a>단원  
이 자습서는 다음 단원 hello를 포함 되어 있습니다.  
  
|단원|예상된 시간 toocomplete|  
|----------|------------------------------|  
|[1 - 새 테이블 형식 모델 프로젝트 만들기](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|10분|  
|[2 - 데이터 가져오기](../tutorials/aas-lesson-2-get-data.md)|10분|  
|[3 - 날짜 테이블로 표시](../tutorials/aas-lesson-3-mark-as-date-table.md)|3분|  
|[4 - 관계 만들기](../tutorials/aas-lesson-4-create-relationships.md)|10분|  
|[5 - 계산된 열 만들기](../tutorials/aas-lesson-5-create-calculated-columns.md)|15분|
|[6 - 측정값 만들기](../tutorials/aas-lesson-6-create-measures.md)|30분|  
|[7 - KPI(핵심 성과 지표) 만들기](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|15분|  
|[8 - 큐브 뷰 만들기](../tutorials/aas-lesson-8-create-perspectives.md)|5분|  
|[9 - 계층 구조 만들기](../tutorials/aas-lesson-9-create-hierarchies.md)|20분|  
|[10 - 파티션 만들기](../tutorials/aas-lesson-10-create-partitions.md)|15분|  
|[11 - 역할 만들기](../tutorials/aas-lesson-11-create-roles.md)|15분|  
|[12 - Excel에서 분석](../tutorials/aas-lesson-12-analyze-in-excel.md)|5분| 
|[13 - 배포](../tutorials/aas-lesson-13-deploy.md)|5분|  
  
## <a name="supplemental-lessons"></a>추가 단원  
이러한 단원 필요한 toocomplete hello 자습서 없는 하지만 더 나은 이해 고급 테이블 형식 모델 제작 기능에에서 도움이 될 수 있습니다.  
  
|단원|예상된 시간 toocomplete|  
|----------|------------------------------|  
|[세부 정보 행](../tutorials/aas-supplemental-lesson-detail-rows.md)|10분|
|[동적 보안](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30분|
|[불규칙한 계층 구조](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20분| 

  
## <a name="next-steps"></a>다음 단계  
시작 tooget 참조 [1 단원: 새 테이블 형식 모델 프로젝트](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)합니다.  
  
  
  

