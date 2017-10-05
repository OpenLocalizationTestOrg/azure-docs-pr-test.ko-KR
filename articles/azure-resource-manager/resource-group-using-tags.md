---
title: "논리적 조직을 위한 Azure 리소스에 태그 지정 | Microsoft Docs"
description: "태그를 적용하여 대금 청구 및 관리를 위해 Azure 리소스를 구성하는 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: 4f52c30614ad39da8a34ff6ecfb707b75400517f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-tags-to-organize-your-azure-resources"></a><span data-ttu-id="2d2d2-103">태그를 사용하여 Azure 리소스 구성</span><span class="sxs-lookup"><span data-stu-id="2d2d2-103">Use tags to organize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="2d2d2-104">Azure Resource Manager 작업을 지원하는 리소스에만 태그를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-104">You can apply tags only to resources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="2d2d2-105">클래식 배포 모델을 통해(예: Azure 클래식 포털을 통해) 가상 컴퓨터, 가상 네트워크 또는 저장소 계정을 만든 경우 해당 리소스에 태그를 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-105">If you created a virtual machine, virtual network, or storage account through the classic deployment model (such as through the Azure classic portal), you cannot apply a tag to that resource.</span></span> <span data-ttu-id="2d2d2-106">태그 지정을 지원하려면 Resource Manager를 통해 이러한 리소스를 다시 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-106">To support tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="2d2d2-107">다른 모든 리소스는 태그 지정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="2d2d2-108">태그 일관성을 위한 정책</span><span class="sxs-lookup"><span data-stu-id="2d2d2-108">Policies for tag consistency</span></span>

<span data-ttu-id="2d2d2-109">리소스 정책을 사용하여 조직의 표준 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-109">You can use resource policies to create standard rules for your organization.</span></span> <span data-ttu-id="2d2d2-110">적절한 값으로 리소스에 태그가 지정되도록 정책을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-110">You can create policies that ensure resources are tagged with the appropriate values.</span></span> <span data-ttu-id="2d2d2-111">자세한 내용은 [태그에 대한 리소스 정책 적용](resource-manager-policy-tags.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="2d2d2-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d2d2-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="2d2d2-113">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2d2d2-113">Azure CLI</span></span>

<span data-ttu-id="2d2d2-114">*리소스 그룹*에 대한 기존 태그를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-114">To see the existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="2d2d2-115">그러면 스크립트가 다음 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-115">That script returns the following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="2d2d2-116">*지정된 리소스 ID를 포함한 리소스*에 대한 기존 태그를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-116">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="2d2d2-117">또는 *지정된 이름, 형식 및 리소스 그룹을 포함한 리소스*에 대한 기존 태그를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-117">Or, to see the existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="2d2d2-118">특정 태그가 있는 리소스 그룹을 가져오려면 `az group list`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-118">To get resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="2d2d2-119">특정 태그 및 값이 있는 모든 리소스를 가져오려면 `az resource list`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-119">To get all the resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="2d2d2-120">리소스 또는 리소스 그룹에 태그를 적용할 때마다 해당 리소스 또는 리소스 그룹의 기존 태그가 덮어써집니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-120">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="2d2d2-121">따라서 리소스 또는 리소스 그룹에 기존 태그가 있는지에 따라 다른 방법을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-121">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="2d2d2-122">*기존 태그를 포함하지 않는 리소스 그룹*에 태그를 추가하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-122">To add tags to a *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="2d2d2-123">*기존 태그를 포함하지 않는 리소스*에 태그를 추가하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-123">To add tags to a *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="2d2d2-124">태그가 이미 있는 리소스에 태그를 추가하려면 기존 태그를 검색하고, 해당 값의 서식을 다시 지정한 후 기존 태그와 새 태그를 다시 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-124">To add tags to a resource that already has tags, retrieve the existing tags, reformat that value, and reapply the existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="2d2d2-125">*리소스의 기존 태그를 유지하지 않고* 리소스 그룹의 모든 태그를 리소스에 적용하려면 다음 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-125">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

<span data-ttu-id="2d2d2-126">리소스 그룹의 모든 태그를 리소스에 적용하고 *리소스의 기존 태그를 유지*하려면 다음 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-126">To apply all tags from a resource group to its resources, and *retain existing tags on resources*, use the following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a><span data-ttu-id="2d2d2-127">템플릿</span><span class="sxs-lookup"><span data-stu-id="2d2d2-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="2d2d2-128">포털</span><span class="sxs-lookup"><span data-stu-id="2d2d2-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="2d2d2-129">REST API</span><span class="sxs-lookup"><span data-stu-id="2d2d2-129">REST API</span></span>
<span data-ttu-id="2d2d2-130">Azure Portal 및 PowerShell 둘 다 백그라운드에서 [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-130">The Azure portal and PowerShell both use the [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind the scenes.</span></span> <span data-ttu-id="2d2d2-131">태그를 다른 환경으로 통합해야 하는 경우 리소스 ID에 대해 **GET**을 사용하여 태그를 가져온 다음 **PATCH** 호출을 사용하여 태그 집합을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-131">If you need to integrate tagging into another environment, you can get tags by using **GET** on the resource ID and update the set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="2d2d2-132">태그 및 청구</span><span class="sxs-lookup"><span data-stu-id="2d2d2-132">Tags and billing</span></span>
<span data-ttu-id="2d2d2-133">태그를 사용하여 청구 데이터를 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-133">You can use tags to group your billing data.</span></span> <span data-ttu-id="2d2d2-134">예를 들어 서로 다른 조직에 여러 VM을 실행하는 경우 태그를 사용하여 비용 센터별로 사용량을 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-134">For example, if you are running multiple VMs for different organizations, use the tags to group usage by cost center.</span></span> <span data-ttu-id="2d2d2-135">또한 프로덕션 환경에서 실행 중인 VM에 대한 청구 사용량과 같이 런타임 환경별로 비용을 분류하는 데 태그를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-135">You can also use tags to categorize costs by runtime environment, such as the billing usage for VMs running in the production environment.</span></span>


<span data-ttu-id="2d2d2-136">[Azure 리소스 사용 및 RateCard API](../billing/billing-usage-rate-card-overview.md) 또는 사용 CSV(쉼표로 구분된 값) 파일을 통해 태그에 대한 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-136">You can retrieve information about tags through the [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or the usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="2d2d2-137">[Azure 계정 포털](https://account.windowsazure.com/) 또는 [EA 포털](https://ea.azure.com)에서 사용 현황 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-137">You download the usage file from the [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="2d2d2-138">대금 청구 정보에 프로그래밍 방식으로 액세스하는 방법은 [Microsoft Azure 리소스 소비에 대한 통찰력 얻기](../billing/billing-usage-rate-card-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-138">For more information about programmatic access to billing information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="2d2d2-139">REST API 작업에 대한 내용은 [Azure 청구 REST API 참조](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="2d2d2-140">대금 청구에 태그를 지원하는 서비스용 사용 CSV를 다운로드하면 **태그** 열에 태그가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-140">When you download the usage CSV for services that support tags with billing, the tags appear in the **Tags** column.</span></span> <span data-ttu-id="2d2d2-141">자세한 내용은 [Microsoft Azure 청구서 이해](../billing/billing-understand-your-bill.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![요금 청구에 대한 태그를 참조하십시오.](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="2d2d2-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2d2d2-143">Next steps</span></span>
* <span data-ttu-id="2d2d2-144">사용자 지정된 정책을 사용하여 구독 전체에 제한 사항 및 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="2d2d2-145">정의한 정책을 사용하려면 모든 리소스에 특정 태그 값이 있어야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="2d2d2-146">자세한 내용은 [정책을 사용하여 리소스 관리 및 액세스 제어](resource-manager-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-146">For more information, see [Use policies to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="2d2d2-147">리소스 배포 시 Azure PowerShell 사용에 대한 소개는 [Azure Resource Manager에서 Azure PowerShell 사용](powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-147">For an introduction to using Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="2d2d2-148">리소스 배포 시 Azure CLI 사용에 대한 소개는 [Azure Resource Manager에서 Mac, Linux 및 Windows용 Azure CLI 사용](xplat-cli-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-148">For an introduction to using the Azure CLI when you're deploying resources, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="2d2d2-149">포털 사용에 대한 소개는 [Azure Portal을 사용하여 Azure 리소스 관리](resource-group-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-149">For an introduction to using the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="2d2d2-150">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d2d2-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

