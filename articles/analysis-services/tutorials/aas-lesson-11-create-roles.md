---
title: "Azure Analysis Services 자습서 단원 11: 역할 만들기 | Microsoft Docs"
description: "Azure Analysis Services 자습서 프로젝트에서 역할을 만드는 방법을 설명합니다."
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
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 085a36edd2a0e80123ac8754b438bceadfa6c0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="c7a32-103">단원 11: 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="c7a32-103">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="c7a32-104">이 단원에서는 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-104">In this lesson, you create roles.</span></span> <span data-ttu-id="c7a32-105">역할은 역할 멤버인 Sa 사용자로만 액세스를 제한하여 모델 데이터베이스 개체 및 데이터 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-105">Roles provide model database object and data security by limiting access to only those users that are role members.</span></span> <span data-ttu-id="c7a32-106">각 역할은 단일 사용 권한(없음, 읽기, 읽기 및 프로세스, 프로세스 또는 관리자)으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-106">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="c7a32-107">역할 관리자를 사용하여 모델 작성 중에 역할을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-107">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="c7a32-108">모델을 배포한 후에는 SSMS(SQL Server Management Studio)를 사용하여 역할을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-108">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="c7a32-109">자세한 내용은 [역할](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7a32-109">To learn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="c7a32-110">이 자습서를 완료하는 데 역할 만들기가 반드시 필요한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-110">Creating roles is not necessary to complete this tutorial.</span></span> <span data-ttu-id="c7a32-111">기본적으로 현재 로그인한 계정은 모델에 대해 관리자 권한을 포함하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-111">By default, the account you are currently logged in with has Administrator privileges on the model.</span></span> <span data-ttu-id="c7a32-112">그러나 조직의 다른 사용자가 보고 클라이언트를 사용하여 탐색하도록 하려면 읽기 권한을 가진 역할을 하나 이상 만들고 해당 사용자를 멤버로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-112">However, for other users in your organization to browse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="c7a32-113">세 가지 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-113">You create three roles:</span></span>  
  
-   <span data-ttu-id="c7a32-114">**Sales Manager** – 이 역할에는 모든 모델 개체 및 데이터에 대해 읽기 권한을 보유하도록 하려는 조직의 사용자가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-114">**Sales Manager** – This role can include users in your organization for which you want to have Read permission to all model objects and data.</span></span>  
  
-   <span data-ttu-id="c7a32-115">**Sales Analyst US** – 이 역할에는 미국 내 판매와 관련된 데이터를 찾아볼 수 있도록 하려는 조직의 사용자가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-115">**Sales Analyst US** – This role can include users in your organization for which you want only to be able to browse data related to sales in the United States.</span></span> <span data-ttu-id="c7a32-116">이 역할의 경우 DAX 수식을 사용하여 멤버가 미국에 대한 데이터만 찾아보도록 제한하는 *행 필터*를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-116">For this role, you use a DAX formula to define a *Row Filter*, which restricts members to browse data only for the United States.</span></span>  
  
-   <span data-ttu-id="c7a32-117">**Administrator** – 이 역할에는 모델 데이터베이스에 대해 관리 작업을 수행하도록 무제한 액세스 및 권한을 허용하는 관리자 권한을 가진 사용자가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-117">**Administrator** – This role can include users for which you want to have Administrator permission, which allows unlimited access and permissions to perform administrative tasks on the model database.</span></span>  
  
<span data-ttu-id="c7a32-118">조직의 Windows 사용자 및 그룹 계정은 고유하므로 특정 조직에서 멤버로 계정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-118">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization to members.</span></span> <span data-ttu-id="c7a32-119">그러나 이 자습서에서는 멤버를 비워 둬도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-119">However, for this tutorial, you can also leave the members blank.</span></span> <span data-ttu-id="c7a32-120">나중에 단원 12: Excel에서 분석에서 각 역할의 효과를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-120">You test the effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="c7a32-121">이 단원을 완료하기 위한 예상 시간: **15분**</span><span class="sxs-lookup"><span data-stu-id="c7a32-121">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="c7a32-122">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c7a32-122">Prerequisites</span></span>  
<span data-ttu-id="c7a32-123">이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="c7a32-124">이 단원의 작업을 수행하기 전에 이전 단원인 [단원 10: 파티션 만들기](../tutorials/aas-lesson-10-create-partitions.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-124">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="c7a32-125">역할 만들기</span><span class="sxs-lookup"><span data-stu-id="c7a32-125">Create roles</span></span>  
  
#### <a name="to-create-a-sales-manager-user-role"></a><span data-ttu-id="c7a32-126">Sales Manager 사용자 역할을 만들려면</span><span class="sxs-lookup"><span data-stu-id="c7a32-126">To create a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="c7a32-127">테이블 형식 모델 탐색기에서 **역할** > **역할**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-127">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="c7a32-128">역할 관리자에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-128">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="c7a32-129">새 역할을 클릭한 후 **이름** 열에서 역할의 이름을 **Sales Manager**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-129">Click the new role, and then in the **Name** column, rename the role to **Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="c7a32-130">**사용 권한** 열에서 드롭다운 목록을 클릭한 후 **읽기** 권한을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-130">In the **Permissions** column, click the dropdown list, and then select the **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="c7a32-132">선택 사항: **멤버** 탭을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-132">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="c7a32-133">**사용자 또는 그룹 선택** 대화 상자에서 역할에 포함하려는 조직에서 Windows 사용자 또는 그룹을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-133">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a><span data-ttu-id="c7a32-134">Sales Analyst US 사용자 역할을 만들려면</span><span class="sxs-lookup"><span data-stu-id="c7a32-134">To create a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="c7a32-135">역할 관리자에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-135">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="c7a32-136">역할의 이름을 **Sales Analyst US**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-136">Rename the role to **Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="c7a32-137">이 역할에 **읽기** 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-137">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="c7a32-138">행 필터 탭을 클릭한 다음 **DimGeography** 테이블에 대한 DAX 필터 열에 다음 수식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-138">Click the Row Filters tab, and then for the **DimGeography** table only, in the DAX Filter column, type the following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="c7a32-139">행 필터 수식은 부울(TRUE/FALSE) 값으로 확인되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-139">A Row Filter formula must resolve to a Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="c7a32-140">이 수식을 사용하여 Country Region Code 값이 “US”인 행만 사용자에게 표시되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-140">With this formula, you are specifying that only rows with the Country Region Code value of “US” are visible to the user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="c7a32-142">선택 사항: **멤버** 탭을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-142">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="c7a32-143">**사용자 또는 그룹 선택** 대화 상자에서 역할에 포함하려는 조직에서 Windows 사용자 또는 그룹을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-143">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-an-administrator-user-role"></a><span data-ttu-id="c7a32-144">Administrator 사용자 역할을 만들려면</span><span class="sxs-lookup"><span data-stu-id="c7a32-144">To create an Administrator user role</span></span>  
  
1.  <span data-ttu-id="c7a32-145">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-145">Click **New**.</span></span>  
  
2.  <span data-ttu-id="c7a32-146">역할의 이름을 **Administrator**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-146">Rename the role to **Administrator**.</span></span>  
  
3.  <span data-ttu-id="c7a32-147">이 역할에 **관리자** 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-147">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="c7a32-148">선택 사항: **멤버** 탭을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-148">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="c7a32-149">**사용자 또는 그룹 선택** 대화 상자에서 역할에 포함하려는 조직에서 Windows 사용자 또는 그룹을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c7a32-149">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="c7a32-150">다음 작업</span><span class="sxs-lookup"><span data-stu-id="c7a32-150">What's next?</span></span>
<span data-ttu-id="c7a32-151">[단원 12: Excel에서 분석](../tutorials/aas-lesson-12-analyze-in-excel.md)</span><span class="sxs-lookup"><span data-stu-id="c7a32-151">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
