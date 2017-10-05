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
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="4108d-103">SQL 데이터 웨어하우스에 대한 지원 티켓을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="4108d-103">How to create a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="4108d-104">SQL Data Warehouse에 문제가 발생한 경우 엔지니어링 팀이 도움을 줄 수 있도록 지원 티켓을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="4108d-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="4108d-105">2016/12/20을 기준으로 Azure Portal의 리소스 상태 검사는 정확하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-105">As of 12/20/2016, the resource health check in the Azure portal is not accurate.</span></span> <span data-ttu-id="4108d-106">이 문제를 해결하기 위한 작업이 활발히 진행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-106">We are actively working to fix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="4108d-107">지원 티켓 만들기</span><span class="sxs-lookup"><span data-stu-id="4108d-107">Create a support ticket</span></span>
1. <span data-ttu-id="4108d-108">[Azure Portal][Azure portal]을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-108">Open the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="4108d-109">홈 화면에서 **도움말 + 지원** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-109">On the Home screen, click the **Help + support** tile.</span></span>
   
    ![도움말 + 지원](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="4108d-111">도움말 + 지원 블레이드에서 **지원 요청 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-111">On the Help + Support blade, click **Create support request**.</span></span>
   
    ![새 지원 요청](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="4108d-113">**요청 유형**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-113">Select the **Request Type**.</span></span>
   
    ![요청 유형](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="4108d-115">기본적으로 각 SQL server(예: myserver.database.windows.net)에는 **DTU 할당량** 인 45,000이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="4108d-116">이 할당량은 안전을 위한 제한일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="4108d-117">지원 티켓을 만들고 *할당량* 을 요청 형식으로 선택하여 할당량을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-117">You can increase your quota by creating a support ticket and selecting *Quota* as the request type.</span></span> <span data-ttu-id="4108d-118">DTU 요구 사항을 계산하려면 7.5를 필요한 총 [DWU][DWU]로 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-118">To calculate your DTU needs, multiply the 7.5 by the total [DWU][DWU] needed.</span></span> <span data-ttu-id="4108d-119">예를 들어 하나의 SQL Server에서 두 개의 DW6000을 호스트하려면 DTU 할당량인 90,000을 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-119">For example, you would like to host two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="4108d-120">포털의 SQL Server 블레이드에서 현재 DTU 사용량을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-120">You can view your current DTU consumption from the SQL server blade in the portal.</span></span> <span data-ttu-id="4108d-121">일시 중지되거나 일시 중지되지 않은 데이터베이스는 모두 DTU 할당량에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-121">Both paused and un-paused databases count toward the DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="4108d-122">보고하려는 문제가 있는 데이터베이스를 호스팅하는 **구독** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-122">Select the **Subscription** that hosts the database with the problem you are reporting.</span></span>
   
    ![구독](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="4108d-124">리소스로 **SQL 데이터 웨어하우스** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-124">Select **SQL Data Warehouse** as the Resource.</span></span>
   
    ![리소스](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="4108d-126">[Azure 지원 계획][Azure support plan]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="4108d-127">**대금 청구, 할당량 및 구독 관리** 지원은 모든 지원 수준에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="4108d-128">**고장 수리** 지원은 [개발자][Developer], [표준][Standard], [전문가 지원][Professional Direct] 또는 [프리미어][Premier] 지원을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="4108d-129">고장 수리 문제는 고객이 Azure를 사용하는 동안 고객에게 발생한 문제 중 Microsoft로 인해 문제가 발생했다는 합리적인 이유가 존재하는 문제를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused the problem.</span></span>
   * <span data-ttu-id="4108d-130">**개발자 멘토링** 및 **자문 서비스**는 [전문가 지원][Professional Direct] 및 [프리미어][Premier] 지원 수준에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-130">**Developer mentoring** and **advisory services** are available at the [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="4108d-131">프리미어 지원 계획이 있는 경우 [Microsoft 프리미어 온라인 포털][Microsoft Premier online portal]에서 SQL Data Warehouse 관련 문제를 보고할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on the [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="4108d-132">범위, 응답 시간, 가격 책정 등을 포함한 다양한 지원 계획에 대한 자세한 정보는 [Azure 지원 계획][Azure support plan]을 참조하세요.  Azure 지원에 대한 질문과 대답은 [Azure 지원 FAQ][Azure support FAQs]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4108d-132">See [Azure support plans][Azure support plan] to learn more about the various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![지원 계획](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="4108d-134">**문제 유형** 및 **범주**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-134">Select the **Problem Type** and **Category**.</span></span> <span data-ttu-id="4108d-135">이 예제에서는 문제 유형으로 '도구'를, 범주로 '클라이언트 도구'를 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-135">In this example, we have chosen "Tools" as the Problem type and "Client tools" as the category.</span></span> 
   
    ![문제 유형 범주](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="4108d-137">문제를 설명하고 비즈니스에 미치는 영향 수준을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-137">Describe the problem and choose the level of business impact.</span></span>
   
    ![문제 설명](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="4108d-139">이 지원 티켓에 대한 **연락처 정보** 는 미리 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="4108d-140">필요한 경우 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="4108d-140">Update this if necessary.</span></span>
    
    ![연락처 정보](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="4108d-142">**만들기** 를 클릭하여 지원 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-142">Click **Create** to submit the support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="4108d-143">지원 티켓 모니터링</span><span class="sxs-lookup"><span data-stu-id="4108d-143">Monitor a support ticket</span></span>
<span data-ttu-id="4108d-144">지원 요청을 제출하면 Azure 지원팀이 연락합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-144">After you have submitted the support request, the Azure support team will contact you.</span></span> <span data-ttu-id="4108d-145">사용자 요청 상태 및 세부 정보를 확인하려면 대시보드에서 **지원 요청 관리** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-145">To check your request status and details, click **Manage support requests** on the dashboard.</span></span>

![상태 확인](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="4108d-147">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="4108d-147">Other Resources</span></span>
<span data-ttu-id="4108d-148">또한 [Stack Overflow][Stack Overflow] 또는 [Azure SQL Data Warehouse MSDN 포럼][Azure SQL Data Warehouse MSDN forum]에서 SQL Data Warehouse 커뮤니티에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4108d-148">Additionally, you can connect with the SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on the [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

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

