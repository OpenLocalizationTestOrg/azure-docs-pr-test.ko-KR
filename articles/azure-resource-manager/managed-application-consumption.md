---
title: "Azure aaaConsume 관리 응용 프로그램 | Microsoft Docs"
description: "고객이 게시된 파일에서 Azure 관리되는 응용 프로그램을 만드는 방법에 대해 설명합니다."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="6291a-103">내부 관리되는 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="6291a-103">Consume an internal managed application</span></span>

<span data-ttu-id="6291a-104">조직의 구성원을 위한 Azure [관리 응용 프로그램](managed-application-overview.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="6291a-105">예를 들어 조직 표준을 준수하도록 하는 IT 부서에서 관리되는 응용 프로그램을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="6291a-106">이러한 관리 되는 응용 프로그램은 hello 하지 hello Azure 마켓플레이스 서비스 카탈로그를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-106">These managed applications are available through hello Service Catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="6291a-107">이 문서의 계속 하기 전에 구독에 대 한 관리 되는 응용 프로그램 hello 서비스 카탈로그에서 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-107">Before proceeding with this article, you must have a managed application available in hello service catalog for your subscription.</span></span> <span data-ttu-id="6291a-108">조직의 다른 사용자가 관리되는 응용 프로그램을 가지고 있지 않은 경우 [내부 사용을 위한 관리되는 응용 프로그램 게시](managed-application-publishing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6291a-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="6291a-109">현재 Azure CLI 또는 hello Azure 포털 tooconsume 관리 되는 응용 프로그램 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-109">Currently, you can use either Azure CLI or hello Azure portal tooconsume a managed application.</span></span>

## <a name="create-hello-managed-application-by-using-hello-portal"></a><span data-ttu-id="6291a-110">Hello 포털을 사용 하 여 hello 관리 되는 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6291a-110">Create hello managed application by using hello portal</span></span>

<span data-ttu-id="6291a-111">다음이 단계를 수행 하는 toodeploy hello 포털을 통해 관리 되는 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="6291a-111">toodeploy a managed application through hello portal, follow these steps:</span></span>

1. <span data-ttu-id="6291a-112">Azure 포털 toohello를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-112">Go toohello Azure portal.</span></span> <span data-ttu-id="6291a-113">**서비스 카탈로그 관리되는 응용 프로그램**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-113">Search for **Service Catalog Managed Application**.</span></span>

   ![서비스 카탈로그 관리되는 응용 프로그램](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="6291a-115">Select hello toocreate 사용 가능한 솔루션 hello 목록에서 원하는 응용 프로그램을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-115">Select hello managed application you want toocreate from hello list of available solutions.</span></span> <span data-ttu-id="6291a-116">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-116">Select **Create**.</span></span>

   ![관리되는 응용 프로그램 선택](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="6291a-118">Hello 매개 변수를 필요한 tooprovision hello 리소스에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-118">Provide values for hello parameters that are required tooprovision hello resources.</span></span> <span data-ttu-id="6291a-119">위치에 **미국 중서부**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-119">Select **West Central US** for location.</span></span> <span data-ttu-id="6291a-120">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-120">Select **OK**.</span></span>

   ![관리되는 응용 프로그램 매개 변수](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="6291a-122">hello 템플릿 제공한 hello 값의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-122">hello template validates hello values you provided.</span></span> <span data-ttu-id="6291a-123">유효성 검사는 성공 하는 경우 선택 **확인** toostart hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-123">If validation succeeds, select **OK** toostart hello deployment.</span></span>

   ![관리되는 응용 프로그램 유효성 검사](./media/managed-application-consumption/validation.png)

<span data-ttu-id="6291a-125">Hello 배포 완료 되 면 hello 서식 파일에 정의 된 hello 적절 한 리소스는 사용자가 제공한 hello 관리 되는 리소스 그룹에 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-125">After hello deployment finishes, hello appropriate resources defined in hello template are provisioned in hello managed resource group you provided.</span></span>

## <a name="create-hello-managed-application-by-using-azure-cli"></a><span data-ttu-id="6291a-126">Azure CLI를 사용 하 여 hello 관리 되는 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6291a-126">Create hello managed application by using Azure CLI</span></span>

<span data-ttu-id="6291a-127">두 가지 방법으로 toocreate 관리 되는 응용 프로그램을 Azure CLI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6291a-127">There are two ways toocreate a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="6291a-128">관리 되는 응용 프로그램을 만들기 위한 hello 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-128">Use hello command for creating managed applications.</span></span>
* <span data-ttu-id="6291a-129">Hello 일반 템플릿 배포 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-129">Use hello regular template deployment command.</span></span>

### <a name="use-hello-template-deployment-command"></a><span data-ttu-id="6291a-130">Hello 템플릿 배포 명령을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6291a-130">Use hello template deployment command</span></span>

<span data-ttu-id="6291a-131">만든 공급 업체 hello hello applianceMainTemplate.json 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-131">Deploy hello applianceMainTemplate.json file that hello vendor created.</span></span>

<span data-ttu-id="6291a-132">그런 다음 두 개의 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-132">Then create two resource groups.</span></span> <span data-ttu-id="6291a-133">hello 첫 번째 리소스 그룹은 hello 관리 되는 응용 프로그램 리소스를 만들 위치: Microsoft.Solutions/appliances 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-133">hello first resource group is where hello managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="6291a-134">두 번째 리소스 그룹 hello mainTemplate.json에 정의 된 hello 리소스를 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-134">hello second resource group contains all hello resources defined in mainTemplate.json.</span></span> <span data-ttu-id="6291a-135">이 리소스 그룹은 hello ISV에 의해 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-135">This resource group is managed by hello ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="6291a-136">사용 하 여 `westcentralus` hello 리소스 그룹의 hello 위치로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-136">Use `westcentralus` as hello location of hello resource group.</span></span>
>

<span data-ttu-id="6291a-137">mainResourceGroup, 다음 명령을 사용 하 여 hello에에서 toodeploy applianceMainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="6291a-137">toodeploy applianceMainTemplate.json in mainResourceGroup, use hello following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="6291a-138">Hello 템플릿 실행 앞, 뒤 묻는 hello hello 서식 파일에 정의 된 hello 매개 변수 값에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-138">After hello preceding template runs, it prompts you for hello values of hello parameters that are defined in hello template.</span></span> <span data-ttu-id="6291a-139">또한 toohello 매개 변수를 필요한 tooprovision 리소스 서식 파일에, 두 가지 주요 매개 변수 값이 필요 하면:</span><span class="sxs-lookup"><span data-stu-id="6291a-139">In addition toohello parameters that are needed tooprovision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="6291a-140">**managedResourceGroupId**: hello hello 리소스 그룹 포함 hello에에서 정의 된 리소스 applianceMainTemplate.json의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-140">**managedResourceGroupId**: hello ID of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="6291a-141">hello 폼의 hello ID가 `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-141">hello ID is of hello form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="6291a-142">hello ID의 예에서는 앞에 오는 hello에서 `managedResourceGroup`합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-142">In hello preceding example, it's hello ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="6291a-143">**applianceDefinitionId**: 관리 되는 응용 프로그램 정의 리소스의 hello hello ID입니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-143">**applianceDefinitionId**: hello ID of hello managed application definition resource.</span></span> <span data-ttu-id="6291a-144">이 값은 hello ISV가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-144">This value is provided by hello ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="6291a-145">hello 게시자 hello 관리 되는 응용 프로그램 정의 포함 하는 액세스 toohello 리소스 그룹에 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-145">hello publisher must grant access toohello resource group that contains hello managed application definition.</span></span> <span data-ttu-id="6291a-146">hello 정의 리소스가 hello 게시자 구독에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-146">hello definition resource is created in hello publisher subscription.</span></span> <span data-ttu-id="6291a-147">따라서, 사용자, 사용자 그룹 또는 응용 프로그램 hello 고객 테 넌 트에 대 한 읽기 액세스 toothis 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-147">Therefore, a user, user group, or application in hello customer tenant needs read access toothis resource.</span></span>

<span data-ttu-id="6291a-148">관리 되는 hello 참조 hello 배포 성공적으로 완료 되 면 mainResourceGroup 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-148">After hello deployment finishes successfully, you see hello managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="6291a-149">hello storageAccount 리소스 managedResourceGroup에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-149">hello storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-hello-create-command"></a><span data-ttu-id="6291a-150">사용 하 여 hello 명령 만들기</span><span class="sxs-lookup"><span data-stu-id="6291a-150">Use hello create command</span></span>

<span data-ttu-id="6291a-151">Hello를 사용할 수 있습니다 `az managedapp create` 명령 toocreate hello에서 관리 되는 응용 프로그램 관리 응용 프로그램 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-151">You can use hello `az managedapp create` command toocreate a managed application from hello managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="6291a-152">**어플라이언스 정의 Id**: hello의 리소스 ID hello hello 앞 단계에서에서 만든 응용 프로그램 정의 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-152">**appliance-definition-Id**: hello resource ID of hello managed application definition created in hello preceding step.</span></span> <span data-ttu-id="6291a-153">tooobtain hello 다음 명령을 실행 하는이 ID에:</span><span class="sxs-lookup"><span data-stu-id="6291a-153">tooobtain this ID, run hello following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="6291a-154">이 명령은 관리 되는 hello 응용 프로그램 정의 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-154">This command returns hello managed application definition.</span></span> <span data-ttu-id="6291a-155">Hello hello ID 속성 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-155">You need hello value of hello ID property.</span></span>

* <span data-ttu-id="6291a-156">**관리-rg-id**: hello 리소스 그룹 포함 hello에에서 정의 된 리소스 applianceMainTemplate.json의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-156">**managed-rg-id**: hello name of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="6291a-157">이 리소스 그룹은 hello 관리 되는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-157">This resource group is hello managed resource group.</span></span> <span data-ttu-id="6291a-158">Hello 게시자가이 기능을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-158">It's managed by hello publisher.</span></span> <span data-ttu-id="6291a-159">리소스 그룹이 없는 경우 현재 사용자에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="6291a-160">**리소스 그룹**: hello 응용 프로그램 리소스 관리는 hello 리소스 그룹이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-160">**resource-group**: hello resource group where hello managed application resource is created.</span></span> <span data-ttu-id="6291a-161">hello Microsoft.Solutions/appliance 리소스가이 리소스 그룹에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-161">hello Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="6291a-162">**매개 변수**: hello applianceMainTemplate.json에 정의 된 hello 리소스에 필요한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-162">**parameters**: hello parameters that are needed for hello resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="6291a-163">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="6291a-163">Known issues</span></span>

<span data-ttu-id="6291a-164">이 미리 보기 릴리스에서 될 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-164">This preview release includes hello following issues:</span></span>

* <span data-ttu-id="6291a-165">500 내부 서버 오류 hello 관리 되는 응용 프로그램의 hello 생성 중에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-165">A 500 internal server error appears during hello creation of hello managed application.</span></span> <span data-ttu-id="6291a-166">이 문제를 실행 하면 가능성이 toobe 간헐적으로 발생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-166">If you run into this issue, it's likely toobe intermittent.</span></span> <span data-ttu-id="6291a-167">Hello 작업을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-167">Retry hello operation.</span></span>
* <span data-ttu-id="6291a-168">Hello 관리 되는 리소스 그룹에 대 한 새 리소스 그룹이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-168">A new resource group is needed for hello managed resource group.</span></span> <span data-ttu-id="6291a-169">기존 리소스 그룹을 사용 하 여 hello 배포가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-169">If you use an existing resource group, hello deployment fails.</span></span>
* <span data-ttu-id="6291a-170">hello hello Microsoft.Solutions/appliances 리소스가 포함 된 리소스 그룹에에서 만들어야 hello **westcentralus** 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-170">hello resource group that contains hello Microsoft.Solutions/appliances resource must be created in hello **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6291a-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6291a-171">Next steps</span></span>

* <span data-ttu-id="6291a-172">소개 toomanaged 응용 프로그램에 대 한 참조 [관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-172">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6291a-173">서비스 카탈로그 관리되는 응용 프로그램을 게시하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 만들기 및 게시](managed-application-publishing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6291a-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="6291a-174">게시는 관리 되는 응용 프로그램 toohello Azure Marketplace에 대 한 정보를 참조 하십시오. [Azure 마켓플레이스 hello에 대 한 응용 프로그램 관리](managed-application-author-marketplace.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-174">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="6291a-175">Hello 시장에서에서 관리 되는 응용 프로그램을 사용 하는 방법에 대 한 정보를 참조 하십시오. [사용할 Azure 관리 응용 프로그램 마켓플레이스 hello에](managed-application-consume-marketplace.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6291a-175">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
