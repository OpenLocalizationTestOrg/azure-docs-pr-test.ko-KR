---
title: "SQL Data Warehouse에 대한 지원 티켓을 만드는 방법 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스에서 지원 티켓을 만드는 방법"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 058ff1229acee5d03db7c0305c5565ae95a85758
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-create-a-support-ticket-for-sql-data-warehouse"></a>SQL 데이터 웨어하우스에 대한 지원 티켓을 만드는 방법
SQL Data Warehouse에 문제가 발생한 경우 엔지니어링 팀이 도움을 줄 수 있도록 지원 티켓을 만드세요.

> [!NOTE] 
> 2016/12/20을 기준으로 Azure Portal의 리소스 상태 검사는 정확하지 않습니다. 이 문제를 해결하기 위한 작업이 활발히 진행되고 있습니다. 


## <a name="create-a-support-ticket"></a>지원 티켓 만들기
1. [Azure Portal][Azure portal]을 엽니다.
2. 홈 화면에서 **도움말 + 지원** 타일을 클릭합니다.
   
    ![도움말 + 지원](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. 도움말 + 지원 블레이드에서 **지원 요청 만들기**를 클릭합니다.
   
    ![새 지원 요청](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. **요청 유형**을 선택합니다.
   
    ![요청 유형](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > 기본적으로 각 SQL server(예: myserver.database.windows.net)에는 **DTU 할당량** 인 45,000이 있습니다. 이 할당량은 안전을 위한 제한일 뿐입니다. 지원 티켓을 만들고 *할당량* 을 요청 형식으로 선택하여 할당량을 늘릴 수 있습니다. DTU 요구 사항을 계산하려면 7.5를 필요한 총 [DWU][DWU]로 곱합니다. 예를 들어 하나의 SQL Server에서 두 개의 DW6000을 호스트하려면 DTU 할당량인 90,000을 요청해야 합니다.  포털의 SQL Server 블레이드에서 현재 DTU 사용량을 볼 수 있습니다. 일시 중지되거나 일시 중지되지 않은 데이터베이스는 모두 DTU 할당량에 포함됩니다. 
   > 
   > 
5. 보고하려는 문제가 있는 데이터베이스를 호스팅하는 **구독** 을 선택합니다.
   
    ![구독](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. 리소스로 **SQL 데이터 웨어하우스** 를 선택합니다.
   
    ![리소스](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. [Azure 지원 계획][Azure support plan]을 선택합니다.
   
   * **대금 청구, 할당량 및 구독 관리** 지원은 모든 지원 수준에서 제공됩니다.
   * **고장 수리** 지원은 [개발자][Developer], [표준][Standard], [전문가 지원][Professional Direct] 또는 [프리미어][Premier] 지원을 통해 제공됩니다. 고장 수리 문제는 고객이 Azure를 사용하는 동안 고객에게 발생한 문제 중 Microsoft로 인해 문제가 발생했다는 합리적인 이유가 존재하는 문제를 의미합니다.
   * **개발자 멘토링** 및 **자문 서비스**는 [전문가 지원][Professional Direct] 및 [프리미어][Premier] 지원 수준에서 제공됩니다. 
     
     프리미어 지원 계획이 있는 경우 [Microsoft 프리미어 온라인 포털][Microsoft Premier online portal]에서 SQL Data Warehouse 관련 문제를 보고할 수도 있습니다.  범위, 응답 시간, 가격 책정 등을 포함한 다양한 지원 계획에 대한 자세한 정보는 [Azure 지원 계획][Azure support plan]을 참조하세요.  Azure 지원에 대한 질문과 대답은 [Azure 지원 FAQ][Azure support FAQs]를 참조하세요.  
     
     ![지원 계획](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. **문제 유형** 및 **범주**를 선택합니다. 이 예제에서는 문제 유형으로 '도구'를, 범주로 '클라이언트 도구'를 선택했습니다. 
   
    ![문제 유형 범주](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. 문제를 설명하고 비즈니스에 미치는 영향 수준을 선택합니다.
   
    ![문제 설명](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. 이 지원 티켓에 대한 **연락처 정보** 는 미리 채워집니다. 필요한 경우 업데이트하세요.
    
    ![연락처 정보](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. **만들기** 를 클릭하여 지원 요청을 제출합니다.

## <a name="monitor-a-support-ticket"></a>지원 티켓 모니터링
지원 요청을 제출하면 Azure 지원팀이 연락합니다. 사용자 요청 상태 및 세부 정보를 확인하려면 대시보드에서 **지원 요청 관리** 를 클릭합니다.

![상태 확인](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a>기타 리소스
또한 [Stack Overflow][Stack Overflow] 또는 [Azure SQL Data Warehouse MSDN 포럼][Azure SQL Data Warehouse MSDN forum]에서 SQL Data Warehouse 커뮤니티에 연결할 수 있습니다.

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

