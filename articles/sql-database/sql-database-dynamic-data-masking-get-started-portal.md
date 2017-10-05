---
title: "Azure Portal: SQL Database 동적 데이터 마스킹 | Microsoft Docs"
description: "Azure Portal에서 SQL Database 동적 데이터 마스킹을 시작하는 방법"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 15184e14d4e1e23b56126bbf9f972c1619dcba80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-the-azure-portal"></a><span data-ttu-id="b2996-103">Azure Portal에서 SQL Database 동적 데이터 마스킹 시작</span><span class="sxs-lookup"><span data-stu-id="b2996-103">Get started with SQL Database dynamic data masking with the Azure Portal</span></span>

<span data-ttu-id="b2996-104">이 항목에서는 Azure Portal을 사용하여 [동적 데이터 마스킹](sql-database-dynamic-data-masking-get-started.md)을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-104">This topic shows you how to implement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with the Azure portal.</span></span> <span data-ttu-id="b2996-105">[Azure SQL Database cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx) 또는 [REST API](https://msdn.microsoft.com/library/dn505719.aspx)를 사용하여 동적 데이터 마스킹을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-the-azure-portal"></a><span data-ttu-id="b2996-106">Azure 포털을 사용하여 데이터베이스에 대한 동적 데이터 마스킹 설정</span><span class="sxs-lookup"><span data-stu-id="b2996-106">Set up dynamic data masking for your database using the Azure Portal</span></span>
1. <span data-ttu-id="b2996-107">[https://portal.azure.com](https://portal.azure.com)에서 Azure 포털을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-107">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b2996-108">마스킹할 중요 데이터가 포함된 데이터베이스의 설정 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-108">Navigate to the settings blade of the database that includes the sensitive data you want to mask.</span></span>
3. <span data-ttu-id="b2996-109">**동적 데이터 마스킹** 타일을 클릭하여 **동적 데이터 마스킹** 구성 블레이드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-109">Click the **Dynamic Data Masking** tile which launches the **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="b2996-110">아래쪽의 **작업** 섹션으로 스크롤한 다음 **동적 데이터 마스킹**을 클릭해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-110">Alternatively, you can scroll down to the **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![탐색 창](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="b2996-112">**동적 데이터 마스킹** 구성 블레이드에 권장 엔진이 마스킹 대상으로 플래그한 몇 가지 데이터베이스 열이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-112">In the **Dynamic Data Masking** configuration blade you may see some database columns that the recommendations engine has flagged for masking.</span></span> <span data-ttu-id="b2996-113">권장을 적용하려면 하나 이상의 열에 대해 **마스크 추가**를 클릭합니다. 해당 열에 대해 기본 형식을 기초로 마스크가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-113">In order to accept the recommendations, just click **Add Mask** for one or more columns and a mask will be created based on the default type for this column.</span></span> <span data-ttu-id="b2996-114">마스킹 규칙을 클릭하고 마스킹 필드 형식을 원하는 다른 형식으로 편집하면 마스킹 기능을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-114">You can change the masking function by clicking on the masking rule and editing the masking field format to a different format of your choice.</span></span> <span data-ttu-id="b2996-115">반드시 **저장**을 클릭하여 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-115">Be sure to click **Save** to save your settings.</span></span>
   
    ![탐색 창](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="b2996-117">데이터베이스에서 열에 마스크를 추가하려면 **동적 데이터 마스킹** 구성 블레이드에서 **마스크 추가**를 클릭하여 **마스킹 규칙 추가** 구성 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-117">To add a mask for any column in your database, at the top of the **Dynamic Data Masking** configuration blade click **Add Mask** to open the **Add Masking Rule** configuration blade</span></span>
   
    ![탐색 창](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="b2996-119">**스키마**, **테이블** 및 **열**을 선택하여 마스킹하도록 지정되는 필드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-119">Select the **Schema**, **Table** and **Column** to define the designated field that will be masked.</span></span>
7. <span data-ttu-id="b2996-120">중요한 데이터 마스킹 범주 목록에서 **마스킹 필드 형식** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-120">Choose a **Masking Field Format** from the list of sensitive data masking categories.</span></span>
   
    ![탐색 창](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="b2996-122">데이터 마스킹 규칙 블레이드에서 **저장** 을 클릭하여 동적 데이터 마스킹 정책의 마스킹 규칙 집합을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-122">Click **Save** in the data masking rule blade to update the set of masking rules in the dynamic data masking policy.</span></span>
9. <span data-ttu-id="b2996-123">마스킹에서 제외되며 마스크되지 않은 중요 데이터에 액세스할 수 있는 SQL 사용자 또는 AAD ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-123">Type the SQL users or AAD identities that should be excluded from masking, and have access to the unmasked sensitive data.</span></span> <span data-ttu-id="b2996-124">세미콜론으로 구분된 사용자 목록이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="b2996-125">관리자 권한이 있는 사용자는 항상 원래의 마스킹되지 않은 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-125">Note that users with administrator privileges always have access to the original unmasked data.</span></span>
   
    ![탐색 창](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="b2996-127">응용 프로그램 계층에서 권한이 있는 응용 프로그램 사용자에 대해 중요한 데이터를 표시할 수 있도록 지정하려면 응용 프로그램이 데이터베이스 쿼리에 사용할 SQL 사용자나 AAD ID를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-127">To make it so the application layer can display sensitive data for application privileged users, add the SQL user or AAD identity the application uses to query the database.</span></span> <span data-ttu-id="b2996-128">중요한 데이터의 노출을 최소화하려면 권한이 있는 사용자 수를 최소한으로 이 목록에 포함하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-128">It is highly recommended that this list contain a minimal number of privileged users to minimize exposure of the sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="b2996-129">데이터 마스킹 구성 블레이드에서 **저장** 을 클릭하여 신규 또는 업데이트된 마스킹 정책을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-129">Click **Save** in the data masking configuration blade to save the new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b2996-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b2996-130">Next steps</span></span>

* <span data-ttu-id="b2996-131">동적 데이터 마스킹의 개요는 [동적 데이터 마스킹](sql-database-dynamic-data-masking-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2996-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="b2996-132">[Azure SQL Database cmdlet](https://msdn.microsoft.com/library/azure/mt574084.aspx) 또는 [REST API](https://msdn.microsoft.com/library/dn505719.aspx)를 사용하여 동적 데이터 마스킹을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2996-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>