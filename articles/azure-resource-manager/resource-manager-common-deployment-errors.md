---
title: "일반적인 Azure 배포 오류 해결 | Microsoft Docs"
description: "Azure Resource Manager를 사용하여 Azure에 리소스를 배포할 때 발생하는 일반적인 오류를 해결하는 방법을 설명합니다."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "배포 오류 Azure 배포, Azure에 배포"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 30adc10d01290f14a3e116813b19916fa36ab0bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="31dae-104">Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결</span><span class="sxs-lookup"><span data-stu-id="31dae-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="31dae-105">이 항목에서는 발생할 수 있는 일반적인 Azure 배포 오류 중 일부를 해결할 수 있는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="31dae-106">다음 오류 코드는 이 항목에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-106">The following error codes are described in this topic:</span></span>

* [<span data-ttu-id="31dae-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="31dae-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="31dae-108">권한 부여 실패</span><span class="sxs-lookup"><span data-stu-id="31dae-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="31dae-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="31dae-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="31dae-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="31dae-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="31dae-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="31dae-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="31dae-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="31dae-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="31dae-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="31dae-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="31dae-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="31dae-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="31dae-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="31dae-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="31dae-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="31dae-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="31dae-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="31dae-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="31dae-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="31dae-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="31dae-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="31dae-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="31dae-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="31dae-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="31dae-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="31dae-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="31dae-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="31dae-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="31dae-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="31dae-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="31dae-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="31dae-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="31dae-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="31dae-125">DeploymentFailed</span></span>

<span data-ttu-id="31dae-126">이 오류 코드는 일반 배포 오류를 나타내지만 문제 해결을 시작해야 하는 오류 코드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-126">This error code indicates a general deployment error, but it is not the error code you need to start troubleshooting.</span></span> <span data-ttu-id="31dae-127">문제 해결에 실제로 도움이 되는 오류 코드는 보통 해당 오류 한 수준 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-127">The error code that actually helps you resolve the issue is usually one level below this error.</span></span> <span data-ttu-id="31dae-128">예를 들어 다음 이미지는 배포 오류에 속하는 **RequestDisallowedByPolicy** 오류 코드를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-128">For example, the following image shows the **RequestDisallowedByPolicy** error code that is under the deployment error.</span></span>

![오류 코드 표시](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="31dae-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="31dae-130">SkuNotAvailable</span></span>

<span data-ttu-id="31dae-131">리소스를 배포할 때(일반적으로 가상 컴퓨터) 다음 오류 코드 및 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-131">When deploying a resource (typically a virtual machine), you may receive the following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

<span data-ttu-id="31dae-132">선택한 리소스 SKU(예: VM 크기)를 선택한 위치에 사용할 수 없는 경우 이 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-132">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span></span> <span data-ttu-id="31dae-133">이 문제를 해결하려면 지역에서 사용할 수 있는 SKU가 무엇인지 알아내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-133">To resolve this issue, you need to determine which SKUs are available in a region.</span></span> <span data-ttu-id="31dae-134">PowerShell, 포털 또는 REST 작업을 사용하여 사용 가능한 SKU를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-134">You can use PowerShell, the portal, or a REST operation to find available SKUs.</span></span>

- <span data-ttu-id="31dae-135">PowerShell에서는 [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) 및 위치별 필터링을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="31dae-136">이 명령이 작동하려면 최신 버전의 PowerShell이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-136">You must have the latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="31dae-137">결과에는 위치에 대한 SKU 목록과 해당 SKU에 대한 제한 사항이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-137">The results include a list of SKUs for the location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="31dae-138">[포털](https://portal.azure.com)을 사용하려면 포털에 로그인하고 인터페이스를 통해 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-138">To use the [portal](https://portal.azure.com), log in to the portal and add a resource through the interface.</span></span> <span data-ttu-id="31dae-139">값을 설정하면 해당 리소스에 사용 가능한 SKU가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-139">As you set the values, you see the available SKUs for that resource.</span></span> <span data-ttu-id="31dae-140">배포를 완료할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-140">You do not need to complete the deployment.</span></span>

    ![사용 가능한 SKU](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="31dae-142">가상 컴퓨터에 대해 REST API를 사용하려면 다음 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-142">To use the REST API for virtual machines, send the following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="31dae-143">다음과 같은 형식으로 사용 가능한 SKU 및 지역을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-143">It returns available SKUs and regions in the following format:</span></span>

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

<span data-ttu-id="31dae-144">해당 위치 또는 대체 위치에서 비즈니스 요구를 충족하는 적합한 SKU를 찾을 수 없는 경우 [SKU 요청](https://aka.ms/skurestriction)을 Azure 지원에 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="31dae-144">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) to Azure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="31dae-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="31dae-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: The current subscription type is not permitted to perform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="31dae-146">이 오류가 발생하는 경우 Azure Active Directory 이외의 모든 Azure 서비스에 대한 액세스가 허용되지 않은 구독을 사용하고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-146">If you receive this error, you are using a subscription that is not permitted to access any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="31dae-147">클래식 포털에 액세스해야 하지만 리소스를 배포하도록 허용되지 않는 경우 이러한 유형의 구독을 보유하고 있는 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-147">You might have this type of subscription when you need to access the classic portal but are not permitted to deploy resources.</span></span> <span data-ttu-id="31dae-148">이 문제를 해결하려면 리소스를 배포할 수 있는 권한이 있는 구독을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-148">To resolve this issue, you must use a subscription that has permission to deploy resources.</span></span>  

<span data-ttu-id="31dae-149">PowerShell을 통해 사용할 수 있는 구독을 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-149">To view your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="31dae-150">또한 현재 구독 설정을 설정하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-150">And, to set the current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="31dae-151">Azure CLI 2.0을 통해 사용할 수 있는 구독을 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-151">To view your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="31dae-152">또한 현재 구독 설정을 설정하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-152">And, to set the current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="31dae-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="31dae-153">InvalidTemplate</span></span>
<span data-ttu-id="31dae-154">이 오류로 인해 별도의 몇 가지 유형의 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="31dae-155">구문 오류</span><span class="sxs-lookup"><span data-stu-id="31dae-155">Syntax error</span></span>

   <span data-ttu-id="31dae-156">템플릿 유효성 검사 실패를 나타내는 오류 메시지가 표시되면 템플릿 구문에 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-156">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="31dae-157">이 오류는 템플릿 식이 복잡할 수 있기 때문에 쉽게 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-157">This error is easy to make because template expressions can be intricate.</span></span> <span data-ttu-id="31dae-158">예를 들어 저장소 계정에 대한 다음 이름 할당에는 대괄호 집합 1개, 함수 3개, 괄호 집합 3개, 작은 따옴표 집합 1개, 속성 1개가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-158">For example, the following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="31dae-159">일치하는 구문을 제공하지 않으면 템플릿에서 의도와는 다른 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-159">If you do not provide the matching syntax, the template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="31dae-160">이러한 오류 유형을 수신하면 식 구문을 주의 깊게 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-160">When you receive this type of error, carefully review the expression syntax.</span></span> <span data-ttu-id="31dae-161">[Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) 또는 [Visual Studio Code](resource-manager-vs-code.md)와 같이 구문 오류에 대해 경고할 수 있는 JSON 편집기를 사용하는 것을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="31dae-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="31dae-162">잘못된 세그먼트 길이</span><span class="sxs-lookup"><span data-stu-id="31dae-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="31dae-163">리소스 이름이 올바른 형식이 아닐 경우 다른 잘못된 템플릿 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-163">Another invalid template error occurs when the resource name is not in the correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'The template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="31dae-164">루트 수준 리소스에는 리소스 형식에 포함된 세그먼트보다 이름에 포함된 세그먼트가 1개 더 적어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-164">A root level resource must have one less segment in the name than in the resource type.</span></span> <span data-ttu-id="31dae-165">각 세그먼트는 슬래시로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="31dae-166">다음 예제에서는 2개 세그먼트가 형식에 있고 1개 세그먼트가 이름에 있으므로 **유효한 이름**입니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-166">In the following example, the type has two segments and the name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="31dae-167">하지만 그 다음 예제의 경우 형식과 이름의 세그먼트 수가 같으므로 **유효한 이름이 아닙니다** .</span><span class="sxs-lookup"><span data-stu-id="31dae-167">But the next example is **not a valid name** because it has the same number of segments as the type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="31dae-168">자식 리소스의 경우 형식과 이름의 세그먼트 수는 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-168">For child resources, the type and name have the same number of segments.</span></span> <span data-ttu-id="31dae-169">자식 리소스의 이름과 형식 전체에 부모 리소의 이름과 형식이 포함되기 때문에 이 세그먼트 수는 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-169">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span></span> <span data-ttu-id="31dae-170">이에 따라 전체 이름에는 여전히 전체 형식보다 하나가 적은 세그먼트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-170">Therefore, the full name still has one less segment than the full type.</span></span>

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   <span data-ttu-id="31dae-171">리소스 공급자 간에 적용되는 Resource Manager 형식에서 세그먼트를 제대로 갖추는 것이 까다로울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-171">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="31dae-172">예를 들어 웹 사이트에 리소스 잠금을 적용하려면 4개 세그먼트가 있는 형식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-172">For example, applying a resource lock to a web site requires a type with four segments.</span></span> <span data-ttu-id="31dae-173">따라서 이름에는 다음과 같이 3개 세그먼트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-173">Therefore, the name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="31dae-174">인덱스 복사는 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="31dae-174">Copy index is not expected</span></span>

   <span data-ttu-id="31dae-175">**copy** 요소를 지원하지 않는 템플릿의 일부에 이 요소를 적용한 경우에 이러한 **InvalidTemplate** 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-175">You encounter this **InvalidTemplate** error when you have applied the **copy** element to a part of the template that does not support this element.</span></span> <span data-ttu-id="31dae-176">copy 요소는 리소스 종류에만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-176">You can only apply the copy element to a resource type.</span></span> <span data-ttu-id="31dae-177">리소스 형식 내에서 속성에 복사를 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-177">You cannot apply copy to a property within a resource type.</span></span> <span data-ttu-id="31dae-178">예를 들어 가상 컴퓨터에 복사를 적용하지만 가상 컴퓨터에 대한 OS 디스크에는 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-178">For example, you apply copy to a virtual machine, but you cannot apply it to the OS disks for a virtual machine.</span></span> <span data-ttu-id="31dae-179">경우에 따라 자식 리소스를 부모 리소스로 변환하여 복사 루프를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-179">In some cases, you can convert a child resource to a parent resource to create a copy loop.</span></span> <span data-ttu-id="31dae-180">복사 사용에 대한 자세한 내용은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31dae-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="31dae-181">잘못된 매개 변수</span><span class="sxs-lookup"><span data-stu-id="31dae-181">Parameter is not valid</span></span>

   <span data-ttu-id="31dae-182">템플릿에서 매개 변수에 허용되는 값을 지정했지만 이러한 값 중 하나가 아닌 값을 제공하는 경우 다음과 비슷한 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-182">If the template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar to the following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'The provided value {parameter value}
  for the template parameter {parameter name} is not valid. The parameter value is not
  part of the allowed values
  ``` 

   <span data-ttu-id="31dae-183">템플릿에 허용되는 값을 다시 한 번 확인하고 배포 시 값 하나를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-183">Double check the allowed values in the template, and provide one during deployment.</span></span>

- <span data-ttu-id="31dae-184">순환 종속성이 감지됨</span><span class="sxs-lookup"><span data-stu-id="31dae-184">Circular dependency detected</span></span>

   <span data-ttu-id="31dae-185">이 오류 메시지는 배포가 시작될 수 없도록 리소스가 서로 종속되어 있는 경우에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-185">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span></span> <span data-ttu-id="31dae-186">상호 종속성의 조합은 둘 이상의 리소스가 이미 대기 중인 다른 리소스를 기다리게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="31dae-187">예를 들어 리소스1은 리소스3에 종속되고, 리소스2는 리소스1에 종속되고, 리소스3은 리소스2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="31dae-188">일반적으로 이런 문제는 불필요한 종속성을 제거하여 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="31dae-189">NotFound 및 ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="31dae-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="31dae-190">해석할 수 없는 리소스 이름이 포함된 템플릿인 경우 다음과 비슷한 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-190">When your template includes the name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="31dae-191">템플릿에서 누락된 리소스를 배포하려는 경우 종속성을 추가해야 하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-191">If you are attempting to deploy the missing resource in the template, check whether you need to add a dependency.</span></span> <span data-ttu-id="31dae-192">리소스 관리자는 가능한 경우 리소스를 병렬로 만들어 배포를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="31dae-193">한 리소스가 다른 리소스 뒤에 배포되어야 하는 경우 템플릿에서 **dependsOn** 요소를 사용하여 다른 리소스에 대한 종속성을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-193">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template to create a dependency on the other resource.</span></span> <span data-ttu-id="31dae-194">예를 들어 웹앱을 배포할 때는 앱 서비스 계획이 반드시 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-194">For example, when deploying a web app, the App Service plan must exist.</span></span> <span data-ttu-id="31dae-195">웹앱이 App Service 계획에 종속된다고 지정하지 않으면 Resource Manager에서 두 리소스를 모두 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-195">If you have not specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span></span> <span data-ttu-id="31dae-196">웹앱에 속성을 설정하려고 할 때 App Service 계획 리소스가 아직 없기 때문에 이 리소스를 찾을 수 없다는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-196">You receive an error stating that the App Service plan resource cannot be found, because it does not exist yet when attempting to set a property on the web app.</span></span> <span data-ttu-id="31dae-197">웹앱에서 종속성을 설정하면 이러한 오류를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-197">You prevent this error by setting the dependency in the web app.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

<span data-ttu-id="31dae-198">종속성 오류 문제 해결을 위한 제안 사항은 [배포 시퀀스 확인](#check-deployment-sequence)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31dae-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="31dae-199">또한 배포되는 그룹이 아닌 다른 리소스 그룹에 리소스가 있는 경우에도 이러한 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-199">You also see this error when the resource exists in a different resource group than the one being deployed to.</span></span> <span data-ttu-id="31dae-200">이 경우 리소스의 정규화 된 이름을 가져오는 [resourceId 함수](resource-group-template-functions-resource.md#resourceid)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-200">In that case, use the [resourceId function](resource-group-template-functions-resource.md#resourceid) to get the fully qualified name of the resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="31dae-201">해석할 수 없는 리소스에 [reference](resource-group-template-functions-resource.md#reference) 또는 [listKeys](resource-group-template-functions-resource.md#listkeys) 함수를 사용하려는 경우에는 다음과 같은 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-201">If you attempt to use the [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive the following error:</span></span>

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="31dae-202">**reference** 함수를 포함하는 식을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-202">Look for an expression that includes the **reference** function.</span></span> <span data-ttu-id="31dae-203">매개 변수 값이 올바른지 다시 한 번 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-203">Double check that the parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="31dae-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="31dae-204">ParentResourceNotFound</span></span>

<span data-ttu-id="31dae-205">한 리소스가 다른 리소스의 부모이면 부모 리소스는 자식 리소스를 만들기 전에 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-205">When one resource is a parent to another resource, the parent resource must exist before creating the child resource.</span></span> <span data-ttu-id="31dae-206">아직 존재하지 않을 경우 다음과 같은 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-206">If it does not yet exist, you receive the following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="31dae-207">자식 리소스의 이름에 부모 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-207">The name of the child resource includes the parent name.</span></span> <span data-ttu-id="31dae-208">예를 들어 SQL Database는 다음과 같이 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="31dae-209">그러나 부모 리소스에 대한 종속성을 지정하지 않으면 자식 리소스는 부모보다 먼저 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-209">But, if you do not specify a dependency on the parent resource, the child resource may get deployed before the parent.</span></span> <span data-ttu-id="31dae-210">이 오류를 해결하려면 종속성을 포함하세요.</span><span class="sxs-lookup"><span data-stu-id="31dae-210">To resolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="31dae-211">torageAccountAlreadyExists 및 StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="31dae-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="31dae-212">저장소 계정에 대해서는 Azure에서 고유한 리소스 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-212">For storage accounts, you must provide a name for the resource that is unique across Azure.</span></span> <span data-ttu-id="31dae-213">고유한 이름을 제공하지 않으면 다음과 같은 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

<span data-ttu-id="31dae-214">명명 규칙과 [uniqueString](resource-group-template-functions-string.md#uniquestring) 함수 결과를 연결하여 고유한 이름을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-214">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="31dae-215">구독에서 기존 저장소 계정과 동일한 이름의 저장소 계정을 배포하지만 다른 위치를 제공하는 경우 해당 저장소 계정이 이미 다른 위치에 이미 있다고 나타내는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-215">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span></span> <span data-ttu-id="31dae-216">이 경우 기존 저장소 계정을 삭제하거나 기존 저장소 계정과 동일한 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-216">Either delete the existing storage account, or provide the same location as the existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="31dae-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="31dae-217">AccountNameInvalid</span></span>
<span data-ttu-id="31dae-218">저장소 계정에 사용이 금지된 문자를 포함하는 이름을 제공하려는 경우 **AccountNameInvalid** 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-218">You see the **AccountNameInvalid** error when attempting to give a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="31dae-219">저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="31dae-220">[uniqueString](resource-group-template-functions-string.md#uniquestring) 함수는 13자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-220">The [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="31dae-221">**uniqueString** 결과에 접두어를 연결하는 경우 11자 미만의 접두어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-221">If you concatenate a prefix to the **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="31dae-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="31dae-222">BadRequest</span></span>

<span data-ttu-id="31dae-223">속성에 대해 잘못된 값을 제공하면 BadRequest 상태가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="31dae-224">예를 들어 저장소 계정에 대해 잘못된 SKU 값을 제공하는 경우 배포가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-224">For example, if you provide an incorrect SKU value for a storage account, the deployment fails.</span></span> <span data-ttu-id="31dae-225">속성에 대해 유효한 값을 확인하려면 [REST API](/rest/api)에서 배포 중인 리소스 유형을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-225">To determine valid values for property, look at the [REST API](/rest/api) for the resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="31dae-226">NoRegisteredProviderFound 및 MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="31dae-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="31dae-227">리소스를 배포할 때 다음 오류 코드 및 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-227">When deploying resource, you may receive the following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="31dae-228">또는 다음과 유사한 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

<span data-ttu-id="31dae-229">세 가지 이유 중 하나로 이러한 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="31dae-230">리소스 공급자가 구독에 대해 등록되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-230">The resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="31dae-231">해당 리소스 종류에 대해 API 버전이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-231">API version not supported for the resource type</span></span>
3. <span data-ttu-id="31dae-232">해당 리소스 종류에 대해 위치가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-232">Location not supported for the resource type</span></span>

<span data-ttu-id="31dae-233">오류 메시지는 지원되는 위치 및 API 버전에 대해 제안을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-233">The error message should give you suggestions for the supported locations and API versions.</span></span> <span data-ttu-id="31dae-234">템플릿을 제안된 값 중 하나로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-234">You can change your template to one of the suggested values.</span></span> <span data-ttu-id="31dae-235">대부분의 공급자는 Azure 포털이나 사용 중인 명령줄 인터페이스에 의해 자동으로 등록되지만, 그렇지 않은 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-235">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span></span> <span data-ttu-id="31dae-236">특정 리소스 공급자를 전에 사용하지 않은 경우 해당 공급자를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-236">If you have not used a particular resource provider before, you may need to register that provider.</span></span> <span data-ttu-id="31dae-237">PowerShell 또는 Azure CLI를 통해 리소스 공급자에 대해 자세히 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="31dae-238">**포털**</span><span class="sxs-lookup"><span data-stu-id="31dae-238">**Portal**</span></span>

<span data-ttu-id="31dae-239">등록 상태를 볼 수 있으며 포털을 통해 리소스 공급자 네임스페이스를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-239">You can see the registration status and register a resource provider namespace through the portal.</span></span>

1. <span data-ttu-id="31dae-240">구독의 경우 **리소스 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-240">For your subscription, select **Resource providers**.</span></span>

   ![리소스 공급자 선택](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="31dae-242">리소스 공급자의 목록을 확인하고 필요한 경우 **등록** 링크를 선택하여 배포하려는 유형의 리소스 공급자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-242">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span></span>

   ![리소스 공급자 나열](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="31dae-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="31dae-244">**PowerShell**</span></span>

<span data-ttu-id="31dae-245">등록 상태를 보려면 **Get-AzureRmResourceProvider**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-245">To see your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="31dae-246">공급자를 등록하려면 **Register-AzureRmResourceProvider** 를 사용하여 등록할 리소스 공급자의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-246">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="31dae-247">특정 종류의 리소스에 대해 지원되는 위치를 확인하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-247">To get the supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="31dae-248">특정 종류의 리소스에 대해 지원되는 API 버전을 확인하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-248">To get the supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="31dae-249">**Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="31dae-249">**Azure CLI**</span></span>

<span data-ttu-id="31dae-250">공급자가 등록되어 있는지 확인하려면 `azure provider list` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-250">To see whether the provider is registered, use the `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="31dae-251">리소스 공급자를 등록하려면 `azure provider register` 명령을 사용하고 등록할 *네임스페이스* 를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-251">To register a resource provider, use the `azure provider register` command, and specify the *namespace* to register.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="31dae-252">리소스 유형에 대해 지원되는 위치 및 API 버전을 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-252">To see the supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="31dae-253">QuotaExceeded 및 OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="31dae-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="31dae-254">또한 배포가 리소스 그룹, 구독, 계정 및 기타 범위당 할당량을 초과할 경우 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="31dae-255">예를 들어 지역에 대한 코어 수를 제한하도록 구독을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-255">For example, your subscription may be configured to limit the number of cores for a region.</span></span> <span data-ttu-id="31dae-256">허용량보다 많은 코어가 있는 가상 컴퓨터를 배포하려는 경우 할당량을 초과했다는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-256">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span></span>
<span data-ttu-id="31dae-257">전체 할당량 정보는 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31dae-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="31dae-258">코어에 대한 구독 할당량을 검사하려면 Azure CLI의 `azure vm list-usage` 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-258">To examine your subscription's quotas for cores, you can use the `azure vm list-usage` command in the Azure CLI.</span></span> <span data-ttu-id="31dae-259">다음 예제에서는 무료 평가판 계정에 대한 코어 할당량이 4개임을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-259">The following example illustrates that the core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="31dae-260">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-260">Which returns:</span></span>

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

<span data-ttu-id="31dae-261">미국 서부 지역의 코어를 5개 이상 만드는 템플릿을 배포하는 경우에 다음과 같은 배포 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-261">If you deploy a template that creates more than four cores in the West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="31dae-262">또는 PowerShell에서 **Get-AzureRmVMUsage** Cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-262">Or in PowerShell, you can use the **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="31dae-263">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-263">Which returns:</span></span>

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

<span data-ttu-id="31dae-264">이러한 경우 포털로 이동하여 사용자가 배포하고 싶은 지역의 할당량을 올려서 지원 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-264">In these cases, you should go to the portal and file a support issue to raise your quota for the region into which you want to deploy.</span></span>

> [!NOTE]
> <span data-ttu-id="31dae-265">리소스 그룹에 대한 할당량은 구독 전체가 아니라 각 개별 지역에 대한 할당량입니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-265">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span></span> <span data-ttu-id="31dae-266">사용자가 미국 서부에 30개의 코어를 배포해야 하면 미국 서부에 30개의 리소스 관리자 코어를 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-266">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="31dae-267">사용자가 액세스하는 임의의 지역에서 30개 코어를 배포해야 하는 경우 모든 지역에 대해 30개 Resource Manager 코어를 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-267">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="31dae-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="31dae-268">InvalidContentLink</span></span>
<span data-ttu-id="31dae-269">다음과 같은 오류 메시지가 표시되는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-269">When you receive the error message:</span></span>

```
Code=InvalidContentLink
Message=Unable to download deployment content from ...
```

<span data-ttu-id="31dae-270">아마 사용할 수 없는 중첩된 템플릿에 연결하려고 했을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-270">You have most likely attempted to link to a nested template that is not available.</span></span> <span data-ttu-id="31dae-271">중첩된 템플릿에 제공된 URI를 다시 한 번 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-271">Double check the URI you provided for the nested template.</span></span> <span data-ttu-id="31dae-272">저장소 계정에 해당 템플릿이 있는 경우 액세스 가능한 URI인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-272">If the template exists in a storage account, make sure the URI is accessible.</span></span> <span data-ttu-id="31dae-273">SAS 토큰을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-273">You may need to pass a SAS token.</span></span> <span data-ttu-id="31dae-274">자세한 내용은 [Azure 리소스 관리자에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31dae-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="31dae-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="31dae-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="31dae-276">구독에 배포 중에 수행을 시도하는 작업을 방해하는 리소스 정책이 포함된 경우 이 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying to perform during deployment.</span></span> <span data-ttu-id="31dae-277">오류 메시지에서 정책 식별자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-277">In the error message, look for the policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="31dae-278">**PowerShell**에서 해당 정책 식별자를 **Id** 매개 변수로 제공하여 배포를 차단한 정책에 대한 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-278">In **PowerShell**, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="31dae-279">**Azure CLI**에서 정책 정의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-279">In **Azure CLI**, provide the name of the policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="31dae-280">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31dae-280">For more information, see the following articles:</span></span>

- [<span data-ttu-id="31dae-281">RequestDisallowedByPolicy 오류</span><span class="sxs-lookup"><span data-stu-id="31dae-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="31dae-282">[정책을 사용하여 리소스 및 컨트롤 액세스 관리](resource-manager-policy.md)</span><span class="sxs-lookup"><span data-stu-id="31dae-282">[Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="31dae-283">권한 부여 실패</span><span class="sxs-lookup"><span data-stu-id="31dae-283">Authorization failed</span></span>
<span data-ttu-id="31dae-284">리소스를 배포하려고 하는 계정 또는 서비스 주체에게 작업 수행을 위한 액세스 권한이 없으므로 배포 중에 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-284">You may receive an error during deployment because the account or service principal attempting to deploy the resources does not have access to perform those actions.</span></span> <span data-ttu-id="31dae-285">개발자 또는 관리자는 Azure Active Directory를 사용하여 ID와 해당 ID가 액세스할 수 있는 리소스를 자세히 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-285">Azure Active Directory enables you or your administrator to control which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="31dae-286">예를 들어 계정이 읽기 역할에 할당되면 새 리소스를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-286">For example, if your account is assigned to the Reader role, you are not able to create resources.</span></span> <span data-ttu-id="31dae-287">이 경우 권한 부여에 실패했다는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dae-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="31dae-288">역할 기반 액세스 제어에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31dae-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="31dae-289">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31dae-289">Next steps</span></span>
* <span data-ttu-id="31dae-290">감사 작업에 대해 알아보려면 [리소스 관리자로 작업 감사](resource-group-audit.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31dae-290">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="31dae-291">배포 중 오류를 확인하는 작업에 대해 알아보려면 [배포 작업 보기](resource-manager-deployment-operations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31dae-291">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
