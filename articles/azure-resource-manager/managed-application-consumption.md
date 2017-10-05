---
title: "Azure 관리되는 응용 프로그램 사용 | Microsoft Docs"
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
ms.openlocfilehash: ed8fbaf2a4546c8e31eeced11cd0b5627fd62c0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="d85bb-103">내부 관리되는 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="d85bb-103">Consume an internal managed application</span></span>

<span data-ttu-id="d85bb-104">조직의 구성원을 위한 Azure [관리 응용 프로그램](managed-application-overview.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="d85bb-105">예를 들어 조직 표준을 준수하도록 하는 IT 부서에서 관리되는 응용 프로그램을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="d85bb-106">이러한 관리되는 응용 프로그램은 Azure Marketplace가 아닌 서비스 카탈로그를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-106">These managed applications are available through the Service Catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="d85bb-107">이 문서를 계속하기 전에 구독을 위한 서비스 카탈로그에서 사용할 수 있는 관리되는 응용 프로그램이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-107">Before proceeding with this article, you must have a managed application available in the service catalog for your subscription.</span></span> <span data-ttu-id="d85bb-108">조직의 다른 사용자가 관리되는 응용 프로그램을 가지고 있지 않은 경우 [내부 사용을 위한 관리되는 응용 프로그램 게시](managed-application-publishing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d85bb-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="d85bb-109">현재 Azure CLI 또는 Azure Portal 중 하나를 사용하여 관리되는 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-109">Currently, you can use either Azure CLI or the Azure portal to consume a managed application.</span></span>

## <a name="create-the-managed-application-by-using-the-portal"></a><span data-ttu-id="d85bb-110">포털을 사용하여 관리되는 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d85bb-110">Create the managed application by using the portal</span></span>

<span data-ttu-id="d85bb-111">포털을 통해 관리되는 응용 프로그램을 배포하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-111">To deploy a managed application through the portal, follow these steps:</span></span>

1. <span data-ttu-id="d85bb-112">Azure Portal로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-112">Go to the Azure portal.</span></span> <span data-ttu-id="d85bb-113">**서비스 카탈로그 관리되는 응용 프로그램**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-113">Search for **Service Catalog Managed Application**.</span></span>

   ![서비스 카탈로그 관리되는 응용 프로그램](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="d85bb-115">사용 가능한 솔루션의 목록에서 만들려는 관리되는 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-115">Select the managed application you want to create from the list of available solutions.</span></span> <span data-ttu-id="d85bb-116">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-116">Select **Create**.</span></span>

   ![관리되는 응용 프로그램 선택](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="d85bb-118">리소스를 프로비전하는 데 필요한 매개 변수의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-118">Provide values for the parameters that are required to provision the resources.</span></span> <span data-ttu-id="d85bb-119">위치에 **미국 중서부**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-119">Select **West Central US** for location.</span></span> <span data-ttu-id="d85bb-120">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-120">Select **OK**.</span></span>

   ![관리되는 응용 프로그램 매개 변수](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="d85bb-122">템플릿에서 사용자가 제공한 값의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-122">The template validates the values you provided.</span></span> <span data-ttu-id="d85bb-123">유효성 검사에 성공하면 **확인**을 선택하여 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-123">If validation succeeds, select **OK** to start the deployment.</span></span>

   ![관리되는 응용 프로그램 유효성 검사](./media/managed-application-consumption/validation.png)

<span data-ttu-id="d85bb-125">배포가 완료되면 템플릿에 정의된 해당 리소스를 사용자가 제공한 관리되는 리소스 그룹에 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-125">After the deployment finishes, the appropriate resources defined in the template are provisioned in the managed resource group you provided.</span></span>

## <a name="create-the-managed-application-by-using-azure-cli"></a><span data-ttu-id="d85bb-126">Azure CLI를 사용하여 관리되는 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d85bb-126">Create the managed application by using Azure CLI</span></span>

<span data-ttu-id="d85bb-127">Azure CLI를 사용하여 관리되는 응용 프로그램을 만드는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-127">There are two ways to create a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="d85bb-128">관리되는 응용 프로그램을 만들기 위한 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-128">Use the command for creating managed applications.</span></span>
* <span data-ttu-id="d85bb-129">일반 템플릿 배포 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-129">Use the regular template deployment command.</span></span>

### <a name="use-the-template-deployment-command"></a><span data-ttu-id="d85bb-130">템플릿 배포 명령 사용</span><span class="sxs-lookup"><span data-stu-id="d85bb-130">Use the template deployment command</span></span>

<span data-ttu-id="d85bb-131">공급업체에서 만든 applianceMainTemplate.json 파일을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-131">Deploy the applianceMainTemplate.json file that the vendor created.</span></span>

<span data-ttu-id="d85bb-132">그런 다음 두 개의 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-132">Then create two resource groups.</span></span> <span data-ttu-id="d85bb-133">첫 번째 리소스 그룹은 관리되는 응용 프로그램 리소스가 생성되는 위치입니다(Microsoft.Solutions/appliances).</span><span class="sxs-lookup"><span data-stu-id="d85bb-133">The first resource group is where the managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="d85bb-134">두 번째 리소스 그룹은 mainTemplate.json에 정의된 모든 리소스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-134">The second resource group contains all the resources defined in mainTemplate.json.</span></span> <span data-ttu-id="d85bb-135">이 리소스 그룹은 ISV에서 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-135">This resource group is managed by the ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="d85bb-136">`westcentralus`를 리소스 그룹의 위치로 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="d85bb-136">Use `westcentralus` as the location of the resource group.</span></span>
>

<span data-ttu-id="d85bb-137">mainResourceGroup에 applianceMainTemplate.json을 배포하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-137">To deploy applianceMainTemplate.json in mainResourceGroup, use the following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="d85bb-138">위의 템플릿이 실행된 후 템플릿에 정의된 매개 변수 값을 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-138">After the preceding template runs, it prompts you for the values of the parameters that are defined in the template.</span></span> <span data-ttu-id="d85bb-139">템플릿의 리소스를 프로비전하는 데 필요한 매개 변수 외에도 다음의 두 가지 주요 매개 변수 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-139">In addition to the parameters that are needed to provision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="d85bb-140">**managedResourceGroupId**: applianceMainTemplate.json에 정의된 리소스를 구성하는 리소스 그룹의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-140">**managedResourceGroupId**: The ID of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="d85bb-141">ID의 형식은 `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`입니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-141">The ID is of the form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="d85bb-142">위의 예제에서는 `managedResourceGroup`의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-142">In the preceding example, it's the ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="d85bb-143">**applianceDefinitionId**: 관리되는 응용 프로그램 정의 리소스의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-143">**applianceDefinitionId**: The ID of the managed application definition resource.</span></span> <span data-ttu-id="d85bb-144">이 값은 ISV에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-144">This value is provided by the ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="d85bb-145">게시자는 관리되는 응용 프로그램 정의를 포함하는 리소스 그룹에 대한 액세스를 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-145">The publisher must grant access to the resource group that contains the managed application definition.</span></span> <span data-ttu-id="d85bb-146">정의 리소스는 게시자 구독에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-146">The definition resource is created in the publisher subscription.</span></span> <span data-ttu-id="d85bb-147">따라서 고객 테넌트의 사용자, 사용자 그룹 또는 응용 프로그램은 이 리소스에 대한 읽기 액세스 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-147">Therefore, a user, user group, or application in the customer tenant needs read access to this resource.</span></span>

<span data-ttu-id="d85bb-148">배포가 성공적으로 완료되면 mainResourceGroup에 관리되는 응용 프로그램이 만들어졌음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-148">After the deployment finishes successfully, you see the managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="d85bb-149">storageAccount 리소스는 managedResourceGroup에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-149">The storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-the-create-command"></a><span data-ttu-id="d85bb-150">만들기 명령 사용</span><span class="sxs-lookup"><span data-stu-id="d85bb-150">Use the create command</span></span>

<span data-ttu-id="d85bb-151">`az managedapp create` 명령을 사용하여 관리되는 응용 프로그램 정의에서 관리되는 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-151">You can use the `az managedapp create` command to create a managed application from the managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="d85bb-152">**appliance-definition-Id**: 이전 단계에서 만든 관리되는 응용 프로그램 정의의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-152">**appliance-definition-Id**: The resource ID of the managed application definition created in the preceding step.</span></span> <span data-ttu-id="d85bb-153">이 ID를 얻으려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-153">To obtain this ID, run the following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="d85bb-154">이 명령은 관리되는 응용 프로그램 정의를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-154">This command returns the managed application definition.</span></span> <span data-ttu-id="d85bb-155">ID 속성의 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-155">You need the value of the ID property.</span></span>

* <span data-ttu-id="d85bb-156">**managed-rg-id**: applianceMainTemplate.json에 정의된 리소스를 포함하는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-156">**managed-rg-id**: The name of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="d85bb-157">이 리소스 그룹은 관리되는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-157">This resource group is the managed resource group.</span></span> <span data-ttu-id="d85bb-158">게시자가 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-158">It's managed by the publisher.</span></span> <span data-ttu-id="d85bb-159">리소스 그룹이 없는 경우 현재 사용자에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="d85bb-160">**resource-group**: 관리되는 응용 프로그램 리소스가 생성되는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-160">**resource-group**: The resource group where the managed application resource is created.</span></span> <span data-ttu-id="d85bb-161">Microsoft.Solutions/appliance 리소스가 이 리소스 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-161">The Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="d85bb-162">**parameters**: applianceMainTemplate.json에 정의된 리소스에 필요한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-162">**parameters**: The parameters that are needed for the resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="d85bb-163">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="d85bb-163">Known issues</span></span>

<span data-ttu-id="d85bb-164">이 미리 보기 릴리스에는 다음과 같은 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-164">This preview release includes the following issues:</span></span>

* <span data-ttu-id="d85bb-165">관리되는 응용 프로그램을 만드는 동안 500 내부 서버 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-165">A 500 internal server error appears during the creation of the managed application.</span></span> <span data-ttu-id="d85bb-166">이 문제가 발생하는 경우 일시적일 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-166">If you run into this issue, it's likely to be intermittent.</span></span> <span data-ttu-id="d85bb-167">작업을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="d85bb-167">Retry the operation.</span></span>
* <span data-ttu-id="d85bb-168">관리되는 리소스 그룹으로 새 리소스 그룹이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-168">A new resource group is needed for the managed resource group.</span></span> <span data-ttu-id="d85bb-169">기존 리소스 그룹을 사용하는 경우 배포가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-169">If you use an existing resource group, the deployment fails.</span></span>
* <span data-ttu-id="d85bb-170">Microsoft.Solutions/appliances 리소스가 포함된 리소스 그룹은 **westcentralus** 위치에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85bb-170">The resource group that contains the Microsoft.Solutions/appliances resource must be created in the **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d85bb-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d85bb-171">Next steps</span></span>

* <span data-ttu-id="d85bb-172">관리되는 응용 프로그램에 대한 소개는 [관리되는 응용 프로그램 개요](managed-application-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d85bb-172">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d85bb-173">서비스 카탈로그 관리되는 응용 프로그램을 게시하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 만들기 및 게시](managed-application-publishing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d85bb-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="d85bb-174">Azure Marketplace에 관리되는 응용 프로그램을 게시하는 방법에 대한 자세한 내용은 [Marketplace의 Azure 관리되는 응용 프로그램](managed-application-author-marketplace.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d85bb-174">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="d85bb-175">Marketplace의 관리되는 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [Marketplace의 Azure 관리되는 응용 프로그램 사용](managed-application-consume-marketplace.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d85bb-175">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
