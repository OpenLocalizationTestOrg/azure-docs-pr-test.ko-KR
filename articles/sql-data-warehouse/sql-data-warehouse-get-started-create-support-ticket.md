---
title: "SQL 데이터 웨어하우스에 대 한 지원 티켓 aaaHow toocreate | Microsoft Docs"
description: "어떻게 Azure SQL 데이터 웨어하우스에 toocreate 지원 티켓 합니다."
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
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="28974-103">SQL 데이터 웨어하우스에 대 한 toocreate 지원 티켓 하는 방법</span><span class="sxs-lookup"><span data-stu-id="28974-103">How toocreate a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="28974-104">SQL Data Warehouse에 문제가 발생한 경우 엔지니어링 팀이 도움을 줄 수 있도록 지원 티켓을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="28974-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="28974-105">2016 년 12 월 20 일을 기준으로 hello Azure 포털에서에서 리소스 상태 검사 hello 정확 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28974-105">As of 12/20/2016, hello resource health check in hello Azure portal is not accurate.</span></span> <span data-ttu-id="28974-106">최선을 다 toofix이이 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="28974-106">We are actively working toofix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="28974-107">지원 티켓 만들기</span><span class="sxs-lookup"><span data-stu-id="28974-107">Create a support ticket</span></span>
1. <span data-ttu-id="28974-108">열기 hello [Azure 포털][Azure portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-108">Open hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="28974-109">Hello 홈 화면에서 클릭 hello **도움말 + 지원** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="28974-109">On hello Home screen, click hello **Help + support** tile.</span></span>
   
    ![도움말 + 지원](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="28974-111">Hello 도움말 + 지원 블레이드에서에서 클릭 **만들기 지원 요청**합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-111">On hello Help + Support blade, click **Create support request**.</span></span>
   
    ![새 지원 요청](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="28974-113">선택 hello **요청 유형**합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-113">Select hello **Request Type**.</span></span>
   
    ![요청 유형](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="28974-115">기본적으로 각 SQL server(예: myserver.database.windows.net)에는 **DTU 할당량** 인 45,000이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28974-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="28974-116">이 할당량은 안전을 위한 제한일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="28974-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="28974-117">지원 티켓을 만들고 선택 하 여 할당량을 늘릴 수 있습니다 *할당량* hello 요청 형식으로.</span><span class="sxs-lookup"><span data-stu-id="28974-117">You can increase your quota by creating a support ticket and selecting *Quota* as hello request type.</span></span> <span data-ttu-id="28974-118">프로그램 DTU, 곱하기 toocalculate hello 총 여 7.5 hello [DWU] [ DWU] 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-118">toocalculate your DTU needs, multiply hello 7.5 by hello total [DWU][DWU] needed.</span></span> <span data-ttu-id="28974-119">예를 들어 원하는 toohost 두 하면 하나의 SQL server에서 DW6000s 90000의 DTU 할당량을 요청 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-119">For example, you would like toohost two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="28974-120">SQL server 블레이드 hello에서에서 현재 DTU 사용에 hello 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28974-120">You can view your current DTU consumption from hello SQL server blade in hello portal.</span></span> <span data-ttu-id="28974-121">일시 중지 및 일시 중지 되지 않은 데이터베이스 hello DTU 할당량을 차지 합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-121">Both paused and un-paused databases count toward hello DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="28974-122">선택 hello **구독** hello hello 문제를 보고 하려는 데이터베이스를 호스트 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-122">Select hello **Subscription** that hosts hello database with hello problem you are reporting.</span></span>
   
    ![구독](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="28974-124">선택 **SQL 데이터 웨어하우스** 리소스 hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-124">Select **SQL Data Warehouse** as hello Resource.</span></span>
   
    ![리소스](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="28974-126">[Azure 지원 계획][Azure support plan]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="28974-127">**대금 청구, 할당량 및 구독 관리** 지원은 모든 지원 수준에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="28974-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="28974-128">**고장 수리** 지원은 [개발자][Developer], [표준][Standard], [전문가 지원][Professional Direct] 또는 [프리미어][Premier] 지원을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="28974-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="28974-129">나누기 수정 문제는 Azure를 사용 하는 동안 고객에 의해 발생 하는 문제 합리적인 기대 해당 발생 하는 Microsoft hello 문제가 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused hello problem.</span></span>
   * <span data-ttu-id="28974-130">**개발자 멘토링** 및 **자문 서비스** hello에 사용할 수 있는 [Professional 직접] [ Professional Direct] 및 [프리미어] [ Premier] 지원 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="28974-130">**Developer mentoring** and **advisory services** are available at hello [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="28974-131">또한 SQL 데이터 웨어하우스를 보고할 수 있습니다 계획을 지 원하는 프리미어를 설정한 경우 관련 hello에 문제 [Microsoft Premier online 포털][Microsoft Premier online portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on hello [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="28974-132">참조 [Azure 지원 계획이] [ Azure support plan] toolearn 다양 한 지원 계획, 범위, 응답 시간 가격 정보를 포함 하 여 hello에 대 한 자세한 등입니다.  Azure 지원에 대한 질문과 대답은 [Azure 지원 FAQ][Azure support FAQs]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28974-132">See [Azure support plans][Azure support plan] toolearn more about hello various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![지원 계획](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="28974-134">선택 hello **문제 유형** 및 **범주**합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-134">Select hello **Problem Type** and **Category**.</span></span> <span data-ttu-id="28974-135">이 예제에서는 hello 문제 유형으로 "도구" 및 "클라이언트 도구" hello 범주로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="28974-135">In this example, we have chosen "Tools" as hello Problem type and "Client tools" as hello category.</span></span> 
   
    ![문제 유형 범주](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="28974-137">Hello 문제를 설명 하 고의 비즈니스 영향 수준 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-137">Describe hello problem and choose hello level of business impact.</span></span>
   
    ![문제 설명](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="28974-139">이 지원 티켓에 대한 **연락처 정보** 는 미리 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="28974-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="28974-140">필요한 경우 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="28974-140">Update this if necessary.</span></span>
    
    ![연락처 정보](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="28974-142">클릭 **만들기** toosubmit hello 지원 요청.</span><span class="sxs-lookup"><span data-stu-id="28974-142">Click **Create** toosubmit hello support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="28974-143">지원 티켓 모니터링</span><span class="sxs-lookup"><span data-stu-id="28974-143">Monitor a support ticket</span></span>
<span data-ttu-id="28974-144">Hello 지원 요청을 제출 하 고 나면 hello Azure 지원 팀은 사용자에 게 연락 합니다.</span><span class="sxs-lookup"><span data-stu-id="28974-144">After you have submitted hello support request, hello Azure support team will contact you.</span></span> <span data-ttu-id="28974-145">toocheck 요청 상태 및 세부 정보를 클릭 하 여 **관리 지원 요청** hello 대시보드에서.</span><span class="sxs-lookup"><span data-stu-id="28974-145">toocheck your request status and details, click **Manage support requests** on hello dashboard.</span></span>

![상태 확인](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="28974-147">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="28974-147">Other Resources</span></span>
<span data-ttu-id="28974-148">또한에 연결할 수 있습니다 SQL 데이터 웨어하우스 커뮤니티 hello로 [스택 오버플로] [ Stack Overflow] 컴퓨터나 hello [Azure SQL 데이터 웨어하우스 MSDN 포럼] [ Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="28974-148">Additionally, you can connect with hello SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on hello [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

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

