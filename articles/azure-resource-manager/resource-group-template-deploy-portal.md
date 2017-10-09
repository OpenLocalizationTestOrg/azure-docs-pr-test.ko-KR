---
title: "Azure 포털 toodeploy aaaUse Azure 리소스 | Microsoft Docs"
description: "Azure 포털 및 Azure 리소스 관리 toodeploy 리소스를 사용 합니다."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="f5753-103">리소스 관리자 템플릿과 Azure 포털로 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="f5753-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5753-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5753-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="f5753-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f5753-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="f5753-106">포털</span><span class="sxs-lookup"><span data-stu-id="f5753-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="f5753-107">REST API</span><span class="sxs-lookup"><span data-stu-id="f5753-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="f5753-108">이 항목에서는 방법을 toouse hello [Azure 포털](https://portal.azure.com) 와 [Azure 리소스 관리자](resource-group-overview.md) toodeploy Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-108">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toodeploy your Azure resources.</span></span> <span data-ttu-id="f5753-109">리소스를 관리 하는 방법에 대 한 toolearn 참조 [포털을 통해 관리 하는 Azure 리소스](resource-group-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-109">toolearn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="f5753-110">현재, 모든 서비스는 hello 포털 또는 리소스 관리자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-110">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="f5753-111">이러한 서비스에 대해 필요한 toouse hello [클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-111">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="f5753-112">각 서비스의 상태를 hello에 대 한 참조 [Azure 포털 가용성 차트](https://azure.microsoft.com/features/azure-portal/availability/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-112">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="f5753-113">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="f5753-113">Create resource group</span></span>
1. <span data-ttu-id="f5753-114">toocreate 빈 리소스 그룹을 선택 **새로** > **관리** > **리소스 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-114">toocreate an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![빈 소스 그룹 만들기](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="f5753-116">이름과 위치를 지정하고 필요한 경우 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="f5753-117">리소스 그룹 hello hello 리소스에 대 한 메타 데이터를 저장 하기 때문에 hello 리소스 그룹 위치 tooprovide가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-117">You need tooprovide a location for hello resource group because hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="f5753-118">규정 준수 상의 이유로 toospecify 메타 데이터를 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-118">For compliance reasons, you may want toospecify where that metadata is stored.</span></span> <span data-ttu-id="f5753-119">일반적으로 대부분의 리소스가 상주할 위치를 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="f5753-120">동일한 hello를 사용 하 여 위치 서식 파일을 단순화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-120">Using hello same location can simplify your template.</span></span>
   
    ![그룹 값 설정](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="f5753-122">마켓플레이스에서 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="f5753-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="f5753-123">리소스 그룹을 만든 후에 리소스 tooit hello Marketplace에서에서 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-123">After you create a resource group, you can deploy resources tooit from hello Marketplace.</span></span> <span data-ttu-id="f5753-124">hello 마켓플레이스는 일반적인 시나리오에 대 한 미리 정의 된 솔루션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-124">hello Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="f5753-125">toostart 해당 배포를 선택 **새로** hello 유형 및 리소스의 toodeploy 원할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-125">toostart a deployment, select **New** and hello type of resource you would like toodeploy.</span></span> <span data-ttu-id="f5753-126">그런 다음 hello hello 리소스의 특정 버전에 대 한 toodeploy 원할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-126">Then, look for hello particular version of hello resource you would like toodeploy.</span></span>
   
    ![리소스 배포](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="f5753-128">Toodeploy 원하는 hello 특정 솔루션, 표시 되지 않으면 마켓플레이스 hello에 대 한 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-128">If you do not see hello particular solution you would like toodeploy, you can search hello Marketplace for it.</span></span>
   
    ![마켓플레이스 검색](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="f5753-130">선택한 리소스의 hello 형식에 따라 컬렉션을 배포 하기 전에 관련 속성 tooset 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-130">Depending on hello type of selected resource, you have a collection of relevant properties tooset before deployment.</span></span> <span data-ttu-id="f5753-131">리소스 유형에 따라 달라지므로 해당 옵션은 여기에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="f5753-132">모든 유형에 대해 대상 리소스 그룹을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="f5753-133">hello 다음 그림에서는 어떻게 toocreate 웹 앱 및 만든 toohello 리소스 그룹을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-133">hello following image shows how toocreate a web app and deploy it toohello resource group you created.</span></span>
   
    ![리소스 그룹 만들기](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="f5753-135">또는 리소스를 배포할 때 toocreate 리소스 그룹을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-135">Alternatively, you can decide toocreate a resource group when deploying your resources.</span></span> <span data-ttu-id="f5753-136">선택 **새로 만들기** hello 리소스 그룹 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-136">Select **Create new** and give hello resource group a name.</span></span>
   
    ![새 리소스 그룹 만들기](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="f5753-138">배포가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-138">Your deployment begins.</span></span> <span data-ttu-id="f5753-139">hello 배포는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-139">hello deployment could take a few minutes.</span></span> <span data-ttu-id="f5753-140">Hello 배포 완료 되 면 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-140">When hello deployment has finished, you see a notification.</span></span>
   
    ![알림 보기](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="f5753-142">리소스를 배포한 후 hello를 사용 하 여 더 많은 리소스 toohello 리소스 그룹을 추가할 수 있습니다 **추가** hello 리소스 그룹 블레이드 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-142">After deploying your resources, you can add more resources toohello resource group by using hello **Add** command on hello resource group blade.</span></span>
   
    ![리소스 추가](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="f5753-144">사용자 지정 템플릿에서 배포</span><span class="sxs-lookup"><span data-stu-id="f5753-144">Deploy resources from custom template</span></span>
<span data-ttu-id="f5753-145">Tooexecute 배포 하지만 hello Marketplace에에서 hello 템플릿 중 하나를 사용 하지, 솔루션에 대 한 hello 인프라를 정의 하는 사용자 지정된 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-145">If you want tooexecute a deployment but not use any of hello templates in hello Marketplace, you can create a customized template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="f5753-146">서식 파일 만들기에 대 한 toolearn 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-146">toolearn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="f5753-147">toodeploy hello 포털을 통해 사용자 지정된 된 템플릿을 선택 **새로**, 검색을 시작 하 고 **템플릿 배포** hello 옵션 중에서 선택할 수 있을 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-147">toodeploy a customized template through hello portal, select **New**, and start searching for **Template Deployment** until you can select it from hello options.</span></span>
   
    ![템플릿 배포 찾기](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="f5753-149">선택 **템플릿 배포** hello 사용 가능한 리소스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-149">Select **Template Deployment** from hello available resources.</span></span>
   
    ![템플릿 배포 선택](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="f5753-151">Hello 템플릿 배포를 시작한 후 사용자 지정에 사용할 수 있는 hello 빈 서식 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-151">After launching hello template deployment, open hello blank template that is available for customizing.</span></span>
   
    ![템플릿 만들기](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="f5753-153">Hello 편집기에서 원하는 toodeploy hello 리소스를 정의 하는 hello JSON 구문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-153">In hello editor, add hello JSON syntax that defines hello resources you want toodeploy.</span></span> <span data-ttu-id="f5753-154">완료되면 **저장** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-154">Select **Save** when done.</span></span> <span data-ttu-id="f5753-155">Hello JSON 구문을 작성에 대 한 지침을 참조 하십시오. [리소스 관리자 템플릿 연습](resource-manager-template-walkthrough.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-155">For guidance on writing hello JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![템플릿 편집](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="f5753-157">Hello에서 기존 서식 파일을 선택할 수 있습니다 또는 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-157">Or, you can select a pre-existing template from hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="f5753-158">이러한 템플릿은 hello 커뮤니티 기여 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-158">These templates are contributed by hello community.</span></span> <span data-ttu-id="f5753-159">여러 가지 일반적인 시나리오를 처리 하 고 누군가가 템플릿에 비슷한 toowhat toodeploy를 시도 하는 추가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-159">They cover many common scenarios, and someone may have added a template that is similar toowhat you are trying toodeploy.</span></span> <span data-ttu-id="f5753-160">Hello 템플릿 toofind에 시나리오와 일치 하는 내용을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-160">You can search hello templates toofind something that matches your scenario.</span></span>
   
    ![빠른 시작 템플릿 선택](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="f5753-162">선택한 템플릿을 hello hello 편집기에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-162">You can view hello selected template in hello editor.</span></span>
5. <span data-ttu-id="f5753-163">입력 한 후 모든 hello 다른 값, 선택 **만들기** toodeploy hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="f5753-163">After providing all hello other values, select **Create** toodeploy hello template.</span></span> 
   
    ![템플릿 배포](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a><span data-ttu-id="f5753-165">Tooyour 계정을 서식 파일에서 리소스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-165">Deploy resources from a template saved tooyour account</span></span>
<span data-ttu-id="f5753-166">hello 포털 toosave 템플릿 tooyour Azure 계정이 있으며 나중에 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-166">hello portal enables you toosave a template tooyour Azure account, and redeploy it later.</span></span> <span data-ttu-id="f5753-167">다음 템플릿, 저장 된 사용에 대 한 자세한 내용은 [hello Azure 포털에서 개인 템플릿을 시작](../marketplace-consumer/mytemplates-getstarted.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-167">For more information about working with these saved templates, [Get started with private templates on hello Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="f5753-168">저장 된 템플릿을 선택 toofind **찾아보기** > **템플릿**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-168">toofind your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![템플릿 찾아보기](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="f5753-170">Hello tooyour 계정을 저장 하는 템플릿 목록에서 하나의 원하는 toowork에 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-170">From hello list of templates saved tooyour account, select hello one you wish toowork on.</span></span>
   
    ![저장된 템플릿](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="f5753-172">선택 **배포** tooredeploy이 템플릿을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-172">Select **Deploy** tooredeploy this saved template.</span></span>
   
    ![저장된 템플릿 배포](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="f5753-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5753-174">Next steps</span></span>
* <span data-ttu-id="f5753-175">tooview 감사 로그 참조 [리소스 관리자와 작업을 감사](resource-group-audit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-175">tooview audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="f5753-176">tootroubleshoot 배포 오류 참조 [배포 작업을 보려면](resource-manager-deployment-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-176">tootroubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="f5753-177">배포 또는 리소스 그룹에서 템플릿을 tooretrieve 참조 [기존 리소스에서 내보내기 Azure 리소스 관리자 템플릿을](resource-manager-export-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-177">tooretrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="f5753-178">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5753-178">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

