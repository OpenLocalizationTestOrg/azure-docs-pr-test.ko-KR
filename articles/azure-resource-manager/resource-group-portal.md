---
title: "Azure 포털을 사용하여 Azure 리소스 관리 | Microsoft Docs"
description: "Azure 포털 및 Azure 리소스 관리자를 사용하여 리소스를 관리합니다. 대시보드를 사용하여 리소스를 모니터링하는 방법을 보여줍니다."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 7a94fd5065de93384460e851627a9813d439956b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="b294d-104">포털을 통해 Azure 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="b294d-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b294d-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b294d-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="b294d-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b294d-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="b294d-107">포털</span><span class="sxs-lookup"><span data-stu-id="b294d-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="b294d-108">REST API</span><span class="sxs-lookup"><span data-stu-id="b294d-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="b294d-109">이 항목에서는 [Azure Resource Manager](resource-group-overview.md)를 포함한 [Azure Portal](https://portal.azure.com)을 사용하여 Azure 리소스를 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-109">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to manage your Azure resources.</span></span> <span data-ttu-id="b294d-110">포털을 통해 리소스를 배포하는 방법을 알아보려면 [Resource Manager 템플릿 및 Azure 포털을 사용하여 리소스 배포](resource-group-template-deploy-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-110">To learn about deploying resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="b294d-111">현재 일부 서비스에서만 포털이나 리소스 관리자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-111">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="b294d-112">이러한 서비스의 경우 [클래식 포털](https://manage.windowsazure.com)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-112">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="b294d-113">각 서비스의 상태는 [Azure 포털 가용성 차트](https://azure.microsoft.com/features/azure-portal/availability/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-113">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="b294d-114">리소스 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="b294d-114">Manage resource groups</span></span>

<span data-ttu-id="b294d-115">리소스 그룹은 Azure 솔루션에 관련된 리소스를 보유하는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="b294d-116">리소스 그룹에는 솔루션에 대한 모든 리소스 또는 그룹으로 관리하려는 해당 리소스만 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-116">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span></span> <span data-ttu-id="b294d-117">사용자의 조직에 가장 적합한 내용에 따라 리소스 그룹에 리소스를 어떻게 할당할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-117">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span></span> <span data-ttu-id="b294d-118">일반적으로 쉽게 배포, 업데이트하고 그룹으로 삭제할 수 있도록 동일한 리소스 그룹에 대해 동일한 수명 주기를 공유하는 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-118">Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="b294d-119">리소스 그룹은 리소스에 대한 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-119">The resource group stores metadata about the resources.</span></span> <span data-ttu-id="b294d-120">따라서 리소스 그룹의 위치를 지정하면 메타데이터가 저장된 위치를 지정하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-120">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="b294d-121">규정 준수 때문에 특정 지역에 데이터가 저장되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-121">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="b294d-122">구독에서 모든 리소스 그룹을 보려면 **리소스 그룹**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-122">To see all the resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![리소스 그룹 찾아보기](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="b294d-124">빈 리소스 그룹을 만들려면 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-124">To create an empty resource group, select **Add**.</span></span>
   
    ![리소스 그룹 추가](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="b294d-126">새 리소스 그룹에 대한 이름 및 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-126">Provide a name and location for the new resource group.</span></span> <span data-ttu-id="b294d-127">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-127">Select **Create**.</span></span>
   
    ![리소스 그룹 만들기](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="b294d-129">최근에 만든 리소스 그룹을 보려면 **새로 고침** 을 선택해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-129">You may need to select **Refresh** to see the recently created resource group.</span></span>
   
    ![리소스 그룹 새로 고침](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="b294d-131">리소스 그룹에 대해 표시된 정보를 사용자 지정하려면 **열**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-131">To customize the information displayed for your resource groups, select **Columns**.</span></span>
   
    ![열 사용자 지정](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="b294d-133">추가할 열을 선택한 후 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-133">Select the columns to add, and then select **Update**.</span></span>
   
    ![열 추가](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="b294d-135">리소스를 새 리소스 그룹에 배포하는 방법을 알아보려면 [Resource Manager 템플릿 및 Azure 포털을 사용하여 리소스 배포](resource-group-template-deploy-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-135">To learn about deploying resources to your new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="b294d-136">리소스 그룹에 대한 빠른 액세스의 경우 대시보드에 블레이드를 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-136">For quick access to a resource group, you can pin the blade to your dashboard.</span></span>
   
    ![리소스 그룹 고정](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="b294d-138">대시보드에 리소스 그룹과 해당 리소스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-138">The dashboard displays the resource group and its resources.</span></span> <span data-ttu-id="b294d-139">리소스 그룹 또는 해당 리소스를 선택하여 항목을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-139">You can select either the resource groups or any of its resources to navigate to the item.</span></span>
   
    ![리소스 그룹 고정](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="b294d-141">리소스 태그 지정</span><span class="sxs-lookup"><span data-stu-id="b294d-141">Tag resources</span></span>
<span data-ttu-id="b294d-142">리소스 그룹 및 리소스에 태그를 적용하여 논리적으로 자산을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-142">You can apply tags to resource groups and resources to logically organize your assets.</span></span> <span data-ttu-id="b294d-143">태그 사용에 대한 자세한 내용은 [태그를 사용하여 Azure 리소스 구성](resource-group-using-tags.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-143">For information about working with tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="b294d-144">리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="b294d-144">Monitor resources</span></span>
<span data-ttu-id="b294d-145">리소스를 선택하면 리소스 종류를 모니터링하기 위한 기본 그래프 및 표가 리소스 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-145">When you select a resource, the resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="b294d-146">리소스를 선택하고 **모니터링** 섹션을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-146">Select a resource and notice the **Monitoring** section.</span></span> <span data-ttu-id="b294d-147">이 섹션에는 리소스 유형과 관련된 그래프가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-147">It includes graphs that are relevant to the resource type.</span></span> <span data-ttu-id="b294d-148">다음은 저장소 계정의 기본 모니터링 데이터를 보여주는 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-148">The following image shows the default monitoring data for a storage account.</span></span>
   
    ![모니터링 표시](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="b294d-150">섹션 위에 줄임표(...)를 선택하여 대시보드에 블레이드의 한 섹션을 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-150">You can pin a section of the blade to your dashboard by selecting the ellipsis (...) above the section.</span></span> <span data-ttu-id="b294d-151">블레이드의 섹션 크기를 사용자 지정하거나 완전히 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-151">You can also customize the size the section in the blade or remove it completely.</span></span> <span data-ttu-id="b294d-152">다음 이미지는 CPU 및 메모리 섹션을 고정, 사용자 지정 또는 제거하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-152">The following image shows how to pin, customize, or remove the CPU and Memory section.</span></span>
   
    ![선택 고정](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="b294d-154">대시보드에 섹션을 고정하면 대시보드에 요약이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-154">After pinning the section to the dashboard, you will see the summary on the dashboard.</span></span> <span data-ttu-id="b294d-155">그리고 즉시 선택하면 데이터에 대한 세부 정보로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-155">And, selecting it immediately takes you to more details about the data.</span></span>
   
    ![대시보드 보기](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="b294d-157">포털을 통해 모니터링하는 데이터를 완전히 사용자 지정하려면 기본 대시보드로 이동한 후 **새 대시보드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-157">To completely customize the data you monitor through the portal, navigate to your default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="b294d-159">새 대시보드의 이름을 지정하고 타일을 대시보드로 끌어 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-159">Give your new dashboard a name and drag tiles onto the dashboard.</span></span> <span data-ttu-id="b294d-160">타일은 다양한 옵션을 통해 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-160">The tiles are filtered by different options.</span></span>
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="b294d-162">대시보드를 사용하는 방법을 알아보려면 [Azure 포털에서 대시보드 만들기 및 공유](../azure-portal/azure-portal-dashboards.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-162">To learn about working with dashboards, see [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="b294d-163">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="b294d-163">Manage resources</span></span>
<span data-ttu-id="b294d-164">리소스에 대한 블레이드에는 리소스 관리 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-164">In the blade for a resource, you see the options for managing the resource.</span></span> <span data-ttu-id="b294d-165">포털에는 해당 리소스 유형의 관리 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-165">The portal presents management options for that particular resource type.</span></span> <span data-ttu-id="b294d-166">리소스 블레이드 상단과 왼쪽에는 관리 명령이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-166">You see the management commands across the top of the resource blade and on the left side.</span></span>

![리소스 관리](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="b294d-168">이러한 옵션에서 가상 컴퓨터를 시작 및 중지하거나 가상 컴퓨터의 속성을 다시 구성하는 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring the properties of the virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="b294d-169">리소스 이동</span><span class="sxs-lookup"><span data-stu-id="b294d-169">Move resources</span></span>
<span data-ttu-id="b294d-170">다른 리소스 그룹 또는 다른 구독으로 리소스를 이동해야 하는 경우에는 [새 리소스 그룹 또는 구독으로 리소스 이동](resource-group-move-resources.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-170">If you need to move resources to another resource group or another subscription, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="b294d-171">리소스 잠금</span><span class="sxs-lookup"><span data-stu-id="b294d-171">Lock resources</span></span>
<span data-ttu-id="b294d-172">구독, 리소스 그룹 또는 리소스에 잠금을 설정하여 조직의 다른 사용자가 실수로 중요한 리소스를 삭제 또는 수정하지 못하게 할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-172">You can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="b294d-173">자세한 내용은 [Azure 리소스 관리자를 사용하여 리소스 잠그기](resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="b294d-174">구독 및 비용 보기</span><span class="sxs-lookup"><span data-stu-id="b294d-174">View your subscription and costs</span></span>
<span data-ttu-id="b294d-175">모든 리소스에 대한 롤업 비용 및 구독에 대한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-175">You can view information about your subscription and the rolled-up costs for all your resources.</span></span> <span data-ttu-id="b294d-176">**구독** 을 선택한 다음 보고 싶은 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-176">Select **Subscriptions** and the subscription you want to see.</span></span> <span data-ttu-id="b294d-177">선택할 구독이 하나만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-177">You might only have one subscription to select.</span></span>

![subscription](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="b294d-179">구독 블레이드 내에 진행 속도가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-179">Within the subscription blade, you see a burn rate.</span></span>

![진행 속도](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="b294d-181">그리고 리소스 유형별 비용 분석이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-181">And, a breakdown of costs by resource type.</span></span>

![리소스 비용](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="b294d-183">템플릿 내보내기</span><span class="sxs-lookup"><span data-stu-id="b294d-183">Export template</span></span>
<span data-ttu-id="b294d-184">리소스 그룹을 설정한 후에는 리소스 그룹에 대한 Resource Manager 템플릿을 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-184">After setting up your resource group, you may want to view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="b294d-185">템플릿을 내보내면 다음과 같은 두 가지 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-185">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="b294d-186">템플릿에 모든 인프라가 포함되어 있기 때문에 향후 솔루션 배포를 간단하게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-186">You can easily automate future deployments of the solution because the template contains all the complete infrastructure.</span></span>
2. <span data-ttu-id="b294d-187">솔루션을 나타내는 JSON(JavaScript Object Notation)을 살펴보면서 템플릿 구문에 익숙해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-187">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="b294d-188">단계별 지침은 [기존 리소스에서 Azure Resource Manager 템플릿 내보내기](resource-manager-export-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="b294d-189">리소스 그룹 또는 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="b294d-189">Delete resource group or resources</span></span>
<span data-ttu-id="b294d-190">리소스 그룹을 삭제하면 그 안에 포함된 모든 리소스가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-190">Deleting a resource group deletes all the resources contained within it.</span></span> <span data-ttu-id="b294d-191">리소스 그룹 내부의 개별 리소스를 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="b294d-192">삭제하려는 리소스 그룹에 다른 리소스 그룹의 리소스가 링크되었을 수 있으므로 리소스 그룹을 삭제할 때는 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-192">You want to exercise caution when you delete a resource group because there might be resources in other resource groups that are linked to it.</span></span> <span data-ttu-id="b294d-193">Resource Manager는 링크된 리소스를 삭제하지 않지만 예상된 리소스가 없는 경우 올바르게 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b294d-193">Resource Manager does not delete linked resources, but they may not operate correctly without the expected resources.</span></span>

![그룹 삭제](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="b294d-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b294d-195">Next steps</span></span>
* <span data-ttu-id="b294d-196">활동 로그를 보려면 [리소스 관리자로 작업 감사](resource-group-audit.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-196">To view activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="b294d-197">배포에 대한 세부 정보를 보려면 [배포 작업 보기](resource-manager-deployment-operations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-197">To view details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="b294d-198">포털을 통해 리소스를 배포하려면 [Resource Manager 템플릿 및 Azure 포털을 사용하여 리소스 배포](resource-group-template-deploy-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-198">To deploy resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="b294d-199">리소스에 대한 액세스를 관리하려면 [역할 할당을 사용하여 Azure 구독 리소스에 대한 액세스 관리](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-199">To manage access to resources, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="b294d-200">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b294d-200">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

