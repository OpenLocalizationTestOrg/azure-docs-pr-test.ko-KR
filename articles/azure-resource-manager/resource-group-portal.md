---
title: "Azure 포털 toomanage aaaUse Azure 리소스 | Microsoft Docs"
description: "Azure 포털 및 Azure 리소스 관리 toomanage 리소스를 사용 합니다. 표시 방법을 toowork 대시보드 toomonitor 리소스입니다."
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
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="ceea8-104">포털을 통해 Azure 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="ceea8-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ceea8-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ceea8-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="ceea8-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ceea8-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="ceea8-107">포털</span><span class="sxs-lookup"><span data-stu-id="ceea8-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="ceea8-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ceea8-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="ceea8-109">이 항목에서는 방법을 toouse hello [Azure 포털](https://portal.azure.com) 와 [Azure 리소스 관리자](resource-group-overview.md) toomanage Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-109">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toomanage your Azure resources.</span></span> <span data-ttu-id="ceea8-110">toolearn hello 포털을 통해 리소스를 배포 하는 방법에 대 한 참조 [리소스 관리자 템플릿 및 Azure 포털을 사용 하 여 리소스를 배포](resource-group-template-deploy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-110">toolearn about deploying resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="ceea8-111">현재, 모든 서비스는 hello 포털 또는 리소스 관리자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-111">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="ceea8-112">이러한 서비스에 대해 필요한 toouse hello [클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-112">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="ceea8-113">각 서비스의 상태를 hello에 대 한 참조 [Azure 포털 가용성 차트](https://azure.microsoft.com/features/azure-portal/availability/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-113">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="ceea8-114">리소스 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="ceea8-114">Manage resource groups</span></span>

<span data-ttu-id="ceea8-115">리소스 그룹은 Azure 솔루션에 관련된 리소스를 보유하는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="ceea8-116">리소스 그룹 hello hello 솔루션에 대 한 모든 hello 리소스 또는 그룹으로 toomanage 되도록 하는 리소스에만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-116">hello resource group can include all hello resources for hello solution, or only those resources that you want toomanage as a group.</span></span> <span data-ttu-id="ceea8-117">원하는 tooallocate 리소스를 결정 하는 요소 hello 조직에 가장 적합 한 기반으로 tooresource 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-117">You decide how you want tooallocate resources tooresource groups based on what makes hello most sense for your organization.</span></span> <span data-ttu-id="ceea8-118">일반적으로 hello를 공유 하는 리소스를 추가 같은 수명 주기 toohello 동일한 리소스 그룹 수 있도록 쉽게 배포, 업데이트를 그룹으로 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-118">Generally, add resources that share hello same lifecycle toohello same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="ceea8-119">리소스 그룹 hello hello 리소스에 대 한 메타 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-119">hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="ceea8-120">따라서 hello 리소스 그룹에 대 한 위치를 지정 하면 지정 하는 메타 데이터가 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-120">Therefore, when you specify a location for hello resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="ceea8-121">규정 준수 상의 이유로 tooensure 할 수 있습니다는 데이터가 저장 되는 특정 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-121">For compliance reasons, you may need tooensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="ceea8-122">toosee 구독에서 모든 hello 리소스 그룹 선택 **리소스 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-122">toosee all hello resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![리소스 그룹 찾아보기](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="ceea8-124">toocreate 빈 리소스 그룹을 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-124">toocreate an empty resource group, select **Add**.</span></span>
   
    ![리소스 그룹 추가](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="ceea8-126">이름 및 hello 새 리소스 그룹에 대 한 위치를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-126">Provide a name and location for hello new resource group.</span></span> <span data-ttu-id="ceea8-127">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-127">Select **Create**.</span></span>
   
    ![리소스 그룹 만들기](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="ceea8-129">Tooselect 야 **새로 고침** toosee hello 최근에 만든 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-129">You may need tooselect **Refresh** toosee hello recently created resource group.</span></span>
   
    ![리소스 그룹 새로 고침](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="ceea8-131">리소스 그룹에 대해 표시 되는 toocustomize hello 정보 선택 **열**합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-131">toocustomize hello information displayed for your resource groups, select **Columns**.</span></span>
   
    ![열 사용자 지정](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="ceea8-133">Hello 열 tooadd를 선택한 다음 선택 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-133">Select hello columns tooadd, and then select **Update**.</span></span>
   
    ![열 추가](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="ceea8-135">toolearn 리소스 tooyour 새 리소스 그룹 배포에 대 한 참조 [리소스 관리자 템플릿 및 Azure 포털을 사용 하 여 리소스를 배포](resource-group-template-deploy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-135">toolearn about deploying resources tooyour new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="ceea8-136">빠른 액세스 tooa 리소스 그룹에 대 한 hello 블레이드 tooyour 대시보드에 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-136">For quick access tooa resource group, you can pin hello blade tooyour dashboard.</span></span>
   
    ![리소스 그룹 고정](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="ceea8-138">hello 대시보드 hello 리소스 그룹 및 해당 리소스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-138">hello dashboard displays hello resource group and its resources.</span></span> <span data-ttu-id="ceea8-139">Hello 리소스 그룹 또는 해당 리소스 toonavigate toohello 항목 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-139">You can select either hello resource groups or any of its resources toonavigate toohello item.</span></span>
   
    ![리소스 그룹 고정](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="ceea8-141">리소스 태그 지정</span><span class="sxs-lookup"><span data-stu-id="ceea8-141">Tag resources</span></span>
<span data-ttu-id="ceea8-142">태그 tooresource 그룹을 적용할 수 있으며 리소스 toologically 자산을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-142">You can apply tags tooresource groups and resources toologically organize your assets.</span></span> <span data-ttu-id="ceea8-143">작업 태그에 대 한 정보를 참조 하십시오. [를 사용 하 여 Azure 리소스를 tooorganize 태그](resource-group-using-tags.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-143">For information about working with tags, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="ceea8-144">리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="ceea8-144">Monitor resources</span></span>
<span data-ttu-id="ceea8-145">리소스를 선택 하는 경우 기본 그래프와 해당 리소스 유형의 모니터링에 대 한 테이블 hello 리소스 블레이드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-145">When you select a resource, hello resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="ceea8-146">리소스와 통지 hello 선택 **모니터링** 섹션.</span><span class="sxs-lookup"><span data-stu-id="ceea8-146">Select a resource and notice hello **Monitoring** section.</span></span> <span data-ttu-id="ceea8-147">관련 toohello 리소스 종류는 그래프를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-147">It includes graphs that are relevant toohello resource type.</span></span> <span data-ttu-id="ceea8-148">hello 다음 이미지 표시 hello 기본 저장소 계정에 대 한 데이터를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-148">hello following image shows hello default monitoring data for a storage account.</span></span>
   
    ![모니터링 표시](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="ceea8-150">Hello 섹션 위에 hello 줄임표 (...)를 선택 하 여 hello 블레이드 tooyour 대시보드의 섹션을 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-150">You can pin a section of hello blade tooyour dashboard by selecting hello ellipsis (...) above hello section.</span></span> <span data-ttu-id="ceea8-151">Hello 블레이드에서 hello 크기 hello 섹션을 사용자 지정 하거나 완전히 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-151">You can also customize hello size hello section in hello blade or remove it completely.</span></span> <span data-ttu-id="ceea8-152">hello 다음 이미지 또는 방법을 보여 줍니다 toopin, 사용자 지정 hello CPU 및 메모리 섹션을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-152">hello following image shows how toopin, customize, or remove hello CPU and Memory section.</span></span>
   
    ![선택 고정](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="ceea8-154">Hello 섹션 toohello 대시보드를 고정 한 후 요약 hello hello 대시보드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-154">After pinning hello section toohello dashboard, you will see hello summary on hello dashboard.</span></span> <span data-ttu-id="ceea8-155">및 hello 데이터에 대 한 세부 정보 toomore 즉시 선택 하면 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-155">And, selecting it immediately takes you toomore details about hello data.</span></span>
   
    ![대시보드 보기](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="ceea8-157">toocompletely hello 포털을 통해 모니터링, tooyour 기본 대시보드를 탐색 및 선택 hello 데이터를 사용자 지정 **새 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-157">toocompletely customize hello data you monitor through hello portal, navigate tooyour default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="ceea8-159">새 대시보드의 이름을 지정 하 고 hello 대시보드 타일 끌어다 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-159">Give your new dashboard a name and drag tiles onto hello dashboard.</span></span> <span data-ttu-id="ceea8-160">hello 타일은 다양 한 옵션으로 필터링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-160">hello tiles are filtered by different options.</span></span>
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="ceea8-162">대시보드를 사용 하는 방법에 대 한 toolearn 참조 [만들고 hello Azure 포털에서에서 대시보드 공유](../azure-portal/azure-portal-dashboards.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-162">toolearn about working with dashboards, see [Creating and sharing dashboards in hello Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="ceea8-163">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="ceea8-163">Manage resources</span></span>
<span data-ttu-id="ceea8-164">리소스에 대 한 hello 블레이드에서 hello 리소스를 관리 하기 위한 hello 옵션 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-164">In hello blade for a resource, you see hello options for managing hello resource.</span></span> <span data-ttu-id="ceea8-165">hello 포털 해당 특정 리소스 종류에 대 한 관리 옵션을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-165">hello portal presents management options for that particular resource type.</span></span> <span data-ttu-id="ceea8-166">Hello의 위쪽 hello 리소스 블레이드 및 hello 왼쪽에 걸쳐 hello 관리 명령을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-166">You see hello management commands across hello top of hello resource blade and on hello left side.</span></span>

![리소스 관리](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="ceea8-168">이러한 옵션 중에서 시작 하 고 가상 컴퓨터를 중지 하거나 hello 가상 컴퓨터의 hello 속성을 다시 구성 하는 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring hello properties of hello virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="ceea8-169">리소스 이동</span><span class="sxs-lookup"><span data-stu-id="ceea8-169">Move resources</span></span>
<span data-ttu-id="ceea8-170">Toomove 리소스 tooanother 리소스 그룹 또는 다른 구독, 필요한 경우 참조 [리소스 toonew 리소스 그룹이 나 구독 이동](resource-group-move-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-170">If you need toomove resources tooanother resource group or another subscription, see [Move resources toonew resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="ceea8-171">리소스 잠금</span><span class="sxs-lookup"><span data-stu-id="ceea8-171">Lock resources</span></span>
<span data-ttu-id="ceea8-172">잠글 수 있습니다 구독, 리소스 그룹 또는 리소스 tooprevent 다른 사용자가 조직의 실수로 삭제 하거나 중요 한 리소스를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-172">You can lock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="ceea8-173">자세한 내용은 [Azure 리소스 관리자를 사용하여 리소스 잠그기](resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ceea8-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="ceea8-174">구독 및 비용 보기</span><span class="sxs-lookup"><span data-stu-id="ceea8-174">View your subscription and costs</span></span>
<span data-ttu-id="ceea8-175">모든 리소스에 대 한 구독 및 hello 겹쳐서 비용에 대 한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-175">You can view information about your subscription and hello rolled-up costs for all your resources.</span></span> <span data-ttu-id="ceea8-176">선택 **구독** 및 toosee hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-176">Select **Subscriptions** and hello subscription you want toosee.</span></span> <span data-ttu-id="ceea8-177">하나의 구독 tooselect만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-177">You might only have one subscription tooselect.</span></span>

![subscription](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="ceea8-179">Hello 구독 블레이드에서 이내 진행 속도 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-179">Within hello subscription blade, you see a burn rate.</span></span>

![진행 속도](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="ceea8-181">그리고 리소스 유형별 비용 분석이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-181">And, a breakdown of costs by resource type.</span></span>

![리소스 비용](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="ceea8-183">템플릿 내보내기</span><span class="sxs-lookup"><span data-stu-id="ceea8-183">Export template</span></span>
<span data-ttu-id="ceea8-184">리소스 그룹을 설정한 후 hello 리소스 그룹에 대 한 tooview hello 리소스 관리자 템플릿을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-184">After setting up your resource group, you may want tooview hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="ceea8-185">내보내는 hello 서식 파일에는 두 가지 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-185">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="ceea8-186">Hello 템플릿에 모든 hello 전체 인프라를 포함 하기 때문에 hello 솔루션의 향후 배포를 쉽게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-186">You can easily automate future deployments of hello solution because hello template contains all hello complete infrastructure.</span></span>
2. <span data-ttu-id="ceea8-187">템플릿 구문에 잘 알고 hello 개체 JSON (JavaScript Notation) 솔루션을 나타내는 보고 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-187">You can become familiar with template syntax by looking at hello JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="ceea8-188">단계별 지침은 [기존 리소스에서 Azure Resource Manager 템플릿 내보내기](resource-manager-export-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ceea8-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="ceea8-189">리소스 그룹 또는 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="ceea8-189">Delete resource group or resources</span></span>
<span data-ttu-id="ceea8-190">리소스 그룹을 삭제 하면 그 안에 포함 된 hello 리소스를 모두 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-190">Deleting a resource group deletes all hello resources contained within it.</span></span> <span data-ttu-id="ceea8-191">리소스 그룹 내부의 개별 리소스를 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="ceea8-192">다른 리소스 그룹에 연결 된 tooit 있는 리소스 수 있으므로 리소스 그룹을 삭제 하면 원하는 tooexercise 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-192">You want tooexercise caution when you delete a resource group because there might be resources in other resource groups that are linked tooit.</span></span> <span data-ttu-id="ceea8-193">리소스 관리자는 연결 된 리소스를 삭제 하지 않습니다 하지만 올바르게 hello 예상 리소스 없이 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-193">Resource Manager does not delete linked resources, but they may not operate correctly without hello expected resources.</span></span>

![그룹 삭제](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="ceea8-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ceea8-195">Next steps</span></span>
* <span data-ttu-id="ceea8-196">tooview 활동 로그 참조 [리소스 관리자와 작업을 감사](resource-group-audit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-196">tooview activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="ceea8-197">tooview 세부 정보는 배포에 대 한 참조 [배포 작업을 보려면](resource-manager-deployment-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-197">tooview details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="ceea8-198">hello 포털을 통해 toodeploy 리소스 참조 [리소스 관리자 템플릿 및 Azure 포털을 사용 하 여 리소스를 배포](resource-group-template-deploy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-198">toodeploy resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="ceea8-199">toomanage 액세스 tooresources 참조 [역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](../active-directory/role-based-access-control-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-199">toomanage access tooresources, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="ceea8-200">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ceea8-200">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

