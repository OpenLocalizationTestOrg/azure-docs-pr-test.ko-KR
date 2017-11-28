---
title: "일반적인 Azure 배포 오류 aaaTroubleshoot | Microsoft Docs"
description: "설명 방법을 tooresolve 리소스 tooAzure Azure 리소스 관리자를 사용 하 여 배포할 때 일반적인 오류입니다."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "배포 오류를 azure 배포 tooazure 배포"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="4e45a-104">Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결</span><span class="sxs-lookup"><span data-stu-id="4e45a-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="4e45a-105">이 항목에서는 발생할 수 있는 일반적인 Azure 배포 오류 중 일부를 해결할 수 있는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="4e45a-106">hello 다음 오류 코드는이 항목에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-106">hello following error codes are described in this topic:</span></span>

* [<span data-ttu-id="4e45a-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="4e45a-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="4e45a-108">권한 부여 실패</span><span class="sxs-lookup"><span data-stu-id="4e45a-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="4e45a-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="4e45a-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="4e45a-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="4e45a-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="4e45a-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="4e45a-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="4e45a-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="4e45a-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="4e45a-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="4e45a-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="4e45a-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="4e45a-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="4e45a-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="4e45a-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="4e45a-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="4e45a-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="4e45a-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="4e45a-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="4e45a-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="4e45a-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="4e45a-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="4e45a-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="4e45a-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="4e45a-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="4e45a-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="4e45a-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="4e45a-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="4e45a-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="4e45a-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="4e45a-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="4e45a-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="4e45a-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="4e45a-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="4e45a-125">DeploymentFailed</span></span>

<span data-ttu-id="4e45a-126">Hello 오류 코드 toostart 문제 해결이 필요한 것만이 오류 코드는 일반적인 배포 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-126">This error code indicates a general deployment error, but it is not hello error code you need toostart troubleshooting.</span></span> <span data-ttu-id="4e45a-127">실제로 hello 문제를 해결 하는 데 도움이 되는 hello 오류 코드는 일반적으로이 오류 보다 한 수준.</span><span class="sxs-lookup"><span data-stu-id="4e45a-127">hello error code that actually helps you resolve hello issue is usually one level below this error.</span></span> <span data-ttu-id="4e45a-128">예를 들어 hello 다음 이미지에서는 hello **RequestDisallowedByPolicy** hello 배포 오류 아래에 있는 오류 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-128">For example, hello following image shows hello **RequestDisallowedByPolicy** error code that is under hello deployment error.</span></span>

![오류 코드 표시](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="4e45a-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="4e45a-130">SkuNotAvailable</span></span>

<span data-ttu-id="4e45a-131">리소스 (일반적으로 가상 컴퓨터)을 배포할 때는 hello 다음과 같은 오류 코드 및 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-131">When deploying a resource (typically a virtual machine), you may receive hello following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

<span data-ttu-id="4e45a-132">Hello 리소스 (예: VM 크기) 선택한 SKU 선택한 hello 위치에 대해 사용할 수 없는 경우이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-132">You receive this error when hello resource SKU you have selected (such as VM size) is not available for hello location you have selected.</span></span> <span data-ttu-id="4e45a-133">tooresolve이이 문제를 toodetermine Sku 사용할 수 있는 지역에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-133">tooresolve this issue, you need toodetermine which SKUs are available in a region.</span></span> <span data-ttu-id="4e45a-134">PowerShell, hello 포털 또는 REST 작업 toofind에서는 사용 가능한 Sku입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-134">You can use PowerShell, hello portal, or a REST operation toofind available SKUs.</span></span>

- <span data-ttu-id="4e45a-135">PowerShell에서는 [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) 및 위치별 필터링을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="4e45a-136">Hello 최신 버전의 PowerShell이이 명령에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-136">You must have hello latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="4e45a-137">hello 결과 hello 위치에 대 한 Sku 목록 및 해당 SKU에 대 한 제한이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-137">hello results include a list of SKUs for hello location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="4e45a-138">toouse hello [포털](https://portal.azure.com)toohello 포털에 로그인 하 고 hello 인터페이스를 통해 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-138">toouse hello [portal](https://portal.azure.com), log in toohello portal and add a resource through hello interface.</span></span> <span data-ttu-id="4e45a-139">Hello 참조 hello 값을 설정 하는 대로 해당 리소스에 대 한 사용 가능한 Sku입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-139">As you set hello values, you see hello available SKUs for that resource.</span></span> <span data-ttu-id="4e45a-140">Toocomplete hello 배포가 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-140">You do not need toocomplete hello deployment.</span></span>

    ![사용 가능한 SKU](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="4e45a-142">가상 컴퓨터에 대 한 toouse hello REST API 요청을 수행 하는 hello 보내기:</span><span class="sxs-lookup"><span data-stu-id="4e45a-142">toouse hello REST API for virtual machines, send hello following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="4e45a-143">형식에 따라 hello에서 사용 가능한 Sku 및 지역 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-143">It returns available SKUs and regions in hello following format:</span></span>

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

<span data-ttu-id="4e45a-144">전송할 수 없습니다 해당 지역 또는 비즈니스 요구를 충족 하는 대체 지역에 적합 한 SKU toofind 인 경우는 [SKU 요청](https://aka.ms/skurestriction) tooAzure 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-144">If you are unable toofind a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) tooAzure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="4e45a-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="4e45a-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="4e45a-146">사용 중인 경우이 오류가 표시 되지 않는 구독 tooaccess Azure Active Directory 이외의 모든 Azure 서비스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-146">If you receive this error, you are using a subscription that is not permitted tooaccess any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="4e45a-147">Tooaccess hello 클래식 포털 필요 하지만 toodeploy 리소스 허용 되지 않는 경우 이러한 유형의 구독을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-147">You might have this type of subscription when you need tooaccess hello classic portal but are not permitted toodeploy resources.</span></span> <span data-ttu-id="4e45a-148">tooresolve이이 문제를 toodeploy 리소스 권한 있는 구독을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-148">tooresolve this issue, you must use a subscription that has permission toodeploy resources.</span></span>  

<span data-ttu-id="4e45a-149">tooview powershell을 사용할 수 있는 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-149">tooview your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="4e45a-150">고 tooset hello 현재 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-150">And, tooset hello current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="4e45a-151">tooview Azure CLI 2.0을 사용할 수 있는 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-151">tooview your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="4e45a-152">고 tooset hello 현재 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-152">And, tooset hello current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="4e45a-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="4e45a-153">InvalidTemplate</span></span>
<span data-ttu-id="4e45a-154">이 오류로 인해 별도의 몇 가지 유형의 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="4e45a-155">구문 오류</span><span class="sxs-lookup"><span data-stu-id="4e45a-155">Syntax error</span></span>

   <span data-ttu-id="4e45a-156">Hello 실패 템플릿 유효성 검사를 나타내는 오류 메시지가 표시 되 면 서식 파일에서 구문 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-156">If you receive an error message that indicates hello template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="4e45a-157">이 오류 쉽게 toomake 않으므로 템플릿 식은 복잡 한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-157">This error is easy toomake because template expressions can be intricate.</span></span> <span data-ttu-id="4e45a-158">예를 들어 hello 저장소 계정에 대 한 다음 이름을 할당 대괄호로, 세 개의 함수, 세 가지 괄호, 작은따옴표, 집합이 하나 및 포함 한 속성:</span><span class="sxs-lookup"><span data-stu-id="4e45a-158">For example, hello following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="4e45a-159">일치 하는 구문 hello를 제공 하지 않는 경우 hello 템플릿 의도 보다 다른 값을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-159">If you do not provide hello matching syntax, hello template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="4e45a-160">이러한 종류의 오류를 받으면 hello 식 구문을 자세히 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-160">When you receive this type of error, carefully review hello expression syntax.</span></span> <span data-ttu-id="4e45a-161">[Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) 또는 [Visual Studio Code](resource-manager-vs-code.md)와 같이 구문 오류에 대해 경고할 수 있는 JSON 편집기를 사용하는 것을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4e45a-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="4e45a-162">잘못된 세그먼트 길이</span><span class="sxs-lookup"><span data-stu-id="4e45a-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="4e45a-163">Hello 리소스 이름이 hello 형식이 잘못 되었습니다. 다른 잘못 된 템플릿 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-163">Another invalid template error occurs when hello resource name is not in hello correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="4e45a-164">루트 수준 리소스 hello 리소스 종류에서 보다 hello 이름에 덜 하나의 세그먼트가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-164">A root level resource must have one less segment in hello name than in hello resource type.</span></span> <span data-ttu-id="4e45a-165">각 세그먼트는 슬래시로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="4e45a-166">다음 예제는 hello, hello 형식에 두 세그먼트와 hello 이름에 하나의 세그먼트가 있으므로 **유효한 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-166">In hello following example, hello type has two segments and hello name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="4e45a-167">Hello 다음 예제는 하지만 **유효한 이름이 아닌** hello 있기 때문에 hello 종류로 동일한 세그먼트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-167">But hello next example is **not a valid name** because it has hello same number of segments as hello type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="4e45a-168">Hello 형식과 이름을 hello 자식 리소스에 대 한 동일한 세그먼트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-168">For child resources, hello type and name have hello same number of segments.</span></span> <span data-ttu-id="4e45a-169">이 세그먼트의이 수 때문에 합리적 hello 전체 이름 및 형식을 hello 자식에 대 한 hello 부모 이름 및 형식이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-169">This number of segments makes sense because hello full name and type for hello child includes hello parent name and type.</span></span> <span data-ttu-id="4e45a-170">따라서 hello 전체 이름을 아직 hello 전체 형식 보다 적은 하나의 세그먼트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-170">Therefore, hello full name still has one less segment than hello full type.</span></span>

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

   <span data-ttu-id="4e45a-171">오른쪽 가져오는 hello 세그먼트는 리소스 공급자에서 적용 되는 리소스 관리자 유형의 번거로울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-171">Getting hello segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="4e45a-172">예를 들어 적용 리소스 잠금 tooa 웹 사이트는 4 개의 세그먼트를 포함 한 형식이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-172">For example, applying a resource lock tooa web site requires a type with four segments.</span></span> <span data-ttu-id="4e45a-173">따라서 hello 이름은 세 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-173">Therefore, hello name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="4e45a-174">인덱스 복사는 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="4e45a-174">Copy index is not expected</span></span>

   <span data-ttu-id="4e45a-175">문제가 발생 하면 **InvalidTemplate** hello를 적용 하는 동안 오류가 발생 했습니다. **복사** 이 요소를 지원 하지 않는 hello 서식 파일의 요소 tooa 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-175">You encounter this **InvalidTemplate** error when you have applied hello **copy** element tooa part of hello template that does not support this element.</span></span> <span data-ttu-id="4e45a-176">Hello 복사 요소 tooa 리소스 종류만 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-176">You can only apply hello copy element tooa resource type.</span></span> <span data-ttu-id="4e45a-177">리소스 형식 내에서 복사 tooa 속성을 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-177">You cannot apply copy tooa property within a resource type.</span></span> <span data-ttu-id="4e45a-178">예를 들어 복사 tooa 가상 컴퓨터를 적용 하지만 toohello OS 디스크는 가상 컴퓨터에 대해 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-178">For example, you apply copy tooa virtual machine, but you cannot apply it toohello OS disks for a virtual machine.</span></span> <span data-ttu-id="4e45a-179">경우에 따라 자식 리소스 tooa 부모 리소스 toocreate 복사본 루프를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-179">In some cases, you can convert a child resource tooa parent resource toocreate a copy loop.</span></span> <span data-ttu-id="4e45a-180">복사 사용에 대한 자세한 내용은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e45a-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="4e45a-181">잘못된 매개 변수</span><span class="sxs-lookup"><span data-stu-id="4e45a-181">Parameter is not valid</span></span>

   <span data-ttu-id="4e45a-182">Hello 템플릿 매개 변수에 허용 되는 값을 지정 하는 경우 이러한 값 중 하나 하지 않은 값을 제공 하는 메시지와 비슷한 toohello를 다음 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-182">If hello template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar toohello following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   <span data-ttu-id="4e45a-183">다시 확인 hello hello 서식 파일에 허용 되는 값 및 배포 하는 동안 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-183">Double check hello allowed values in hello template, and provide one during deployment.</span></span>

- <span data-ttu-id="4e45a-184">순환 종속성이 감지됨</span><span class="sxs-lookup"><span data-stu-id="4e45a-184">Circular dependency detected</span></span>

   <span data-ttu-id="4e45a-185">리소스의 종속 관계 hello 배포를 시작 하지 못하게 하는 방식으로 하는 경우이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-185">You receive this error when resources depend on each other in a way that prevents hello deployment from starting.</span></span> <span data-ttu-id="4e45a-186">상호 종속성의 조합은 둘 이상의 리소스가 이미 대기 중인 다른 리소스를 기다리게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="4e45a-187">예를 들어 리소스1은 리소스3에 종속되고, 리소스2는 리소스1에 종속되고, 리소스3은 리소스2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="4e45a-188">일반적으로 이런 문제는 불필요한 종속성을 제거하여 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="4e45a-189">NotFound 및 ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="4e45a-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="4e45a-190">확인할 수 없는 리소스의 hello 이름을 포함 하는 서식 파일에, 다음과 같은 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-190">When your template includes hello name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="4e45a-191">Hello 서식 파일에는 리소스가 없습니다 toodeploy hello를 시도 하는 경우 종속성 tooadd 해야 할지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-191">If you are attempting toodeploy hello missing resource in hello template, check whether you need tooadd a dependency.</span></span> <span data-ttu-id="4e45a-192">리소스 관리자는 가능한 경우 리소스를 병렬로 만들어 배포를 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="4e45a-193">하나의 리소스를 다른 리소스 후 배포 해야 toouse hello **dependsOn** 요소에 대 한 종속성 a 템플릿 toocreate 프로그램에 다른 리소스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-193">If one resource must be deployed after another resource, you need toouse hello **dependsOn** element in your template toocreate a dependency on hello other resource.</span></span> <span data-ttu-id="4e45a-194">예를 들어 웹 응용 프로그램을 배포할 때는 hello 앱 서비스 계획 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-194">For example, when deploying a web app, hello App Service plan must exist.</span></span> <span data-ttu-id="4e45a-195">리소스 관리자 hello에 리소스가 모두 만듭니다 hello 앱 서비스 계획에 따라 달라 집니다 해당 hello 웹 앱을 지정 하지 않은 경우 동일한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-195">If you have not specified that hello web app depends on hello App Service plan, Resource Manager creates both resources at hello same time.</span></span> <span data-ttu-id="4e45a-196">Tooset hello 웹 앱에 대 한 속성을 시도할 때 아직 존재 하지 않으므로 앱 서비스 계획의 리소스를 찾을 수 없으면 해당 hello 라는 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-196">You receive an error stating that hello App Service plan resource cannot be found, because it does not exist yet when attempting tooset a property on hello web app.</span></span> <span data-ttu-id="4e45a-197">Hello 종속성 hello 웹 응용 프로그램에서 설정 하 여이 오류를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-197">You prevent this error by setting hello dependency in hello web app.</span></span>

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

<span data-ttu-id="4e45a-198">종속성 오류 문제 해결을 위한 제안 사항은 [배포 시퀀스 확인](#check-deployment-sequence)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e45a-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="4e45a-199">Hello 리소스 하나에 배포 되 고 hello 보다 다른 리소스 그룹에 있는 경우이 오류를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-199">You also see this error when hello resource exists in a different resource group than hello one being deployed to.</span></span> <span data-ttu-id="4e45a-200">이 경우 hello를 사용 하 여 [resourceId 함수](resource-group-template-functions-resource.md#resourceid) tooget hello hello 리소스의 정규화 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-200">In that case, use hello [resourceId function](resource-group-template-functions-resource.md#resourceid) tooget hello fully qualified name of hello resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="4e45a-201">Toouse hello를 시도 하면 [참조](resource-group-template-functions-resource.md#reference) 또는 [Listkey](resource-group-template-functions-resource.md#listkeys) hello 다음 오류가 수신 해결할 수 없는 리소스를 사용 하는 함수:</span><span class="sxs-lookup"><span data-stu-id="4e45a-201">If you attempt toouse hello [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive hello following error:</span></span>

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="4e45a-202">Hello를 포함 하는 식에 대 한 확인 **참조** 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-202">Look for an expression that includes hello **reference** function.</span></span> <span data-ttu-id="4e45a-203">Hello 매개 변수 값이 정확한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-203">Double check that hello parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="4e45a-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="4e45a-204">ParentResourceNotFound</span></span>

<span data-ttu-id="4e45a-205">하나의 리소스 부모 tooanother 리소스인 경우 hello 부모 리소스 hello 자식 리소스를 만들기 전에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-205">When one resource is a parent tooanother resource, hello parent resource must exist before creating hello child resource.</span></span> <span data-ttu-id="4e45a-206">아직 존재 하지 않는 경우 hello 다음 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-206">If it does not yet exist, you receive hello following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="4e45a-207">hello 자식 리소스의 hello 이름을 hello 부모 이름이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-207">hello name of hello child resource includes hello parent name.</span></span> <span data-ttu-id="4e45a-208">예를 들어 SQL Database는 다음과 같이 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="4e45a-209">그러나 hello 부모 리소스에 대 한 종속성을 지정 하지 않으면 hello 자식 리소스 hello 부모 하기 전에 배포 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-209">But, if you do not specify a dependency on hello parent resource, hello child resource may get deployed before hello parent.</span></span> <span data-ttu-id="4e45a-210">tooresolve이이 오류는 종속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-210">tooresolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="4e45a-211">torageAccountAlreadyExists 및 StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="4e45a-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="4e45a-212">저장소 계정에는 Azure에서 고유 hello 리소스에 대 한 이름을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-212">For storage accounts, you must provide a name for hello resource that is unique across Azure.</span></span> <span data-ttu-id="4e45a-213">고유한 이름을 제공하지 않으면 다음과 같은 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

<span data-ttu-id="4e45a-214">명명 규칙에 따라 hello의 hello 결과 함께 연결 하 여 고유한 이름을 만들 수 있습니다 [uniqueString](resource-group-template-functions-string.md#uniquestring) 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-214">You can create a unique name by concatenating your naming convention with hello result of hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="4e45a-215">Hello로 저장소 계정을 배포 하는 경우 구독에서 기존 저장소 계정으로 이름을 동일 하지만 다른 위치를 제공, 나타내는 hello 저장소 계정이 다른 위치에 이미 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-215">If you deploy a storage account with hello same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating hello storage account already exists in a different location.</span></span> <span data-ttu-id="4e45a-216">Hello 기존 저장소 계정을 삭제 하거나 제공 hello 기존 저장소 계정으로 같은 위치 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-216">Either delete hello existing storage account, or provide hello same location as hello existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="4e45a-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="4e45a-217">AccountNameInvalid</span></span>
<span data-ttu-id="4e45a-218">Hello 참조 **AccountNameInvalid** 금지 된 문자는 저장소 계정을 포함 하는 이름을 toogive를 시도 하는 동안 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-218">You see hello **AccountNameInvalid** error when attempting toogive a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="4e45a-219">저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="4e45a-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring) 13 문자가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="4e45a-221">접두사 toohello을 연결 하는 경우 **uniqueString** 결과 11 자 접두사를 입력이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-221">If you concatenate a prefix toohello **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="4e45a-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="4e45a-222">BadRequest</span></span>

<span data-ttu-id="4e45a-223">속성에 대해 잘못된 값을 제공하면 BadRequest 상태가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="4e45a-224">예를 들어 저장소 계정에 대 한 잘못 된 SKU 값을 제공 하는 경우 hello 배포가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-224">For example, if you provide an incorrect SKU value for a storage account, hello deployment fails.</span></span> <span data-ttu-id="4e45a-225">속성에 대 한 유효한 값 toodetermine hello를 살펴보고 [REST API](/rest/api) 배포 하는 hello 리소스 유형에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-225">toodetermine valid values for property, look at hello [REST API](/rest/api) for hello resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="4e45a-226">NoRegisteredProviderFound 및 MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="4e45a-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="4e45a-227">리소스를 배포할 때는 hello 오류 코드 다음 수신 및 메시지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-227">When deploying resource, you may receive hello following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="4e45a-228">또는 다음과 유사한 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

<span data-ttu-id="4e45a-229">세 가지 이유 중 하나로 이러한 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="4e45a-230">구독에 대 한 hello 리소스 공급자 등록 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-230">hello resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="4e45a-231">Hello 리소스 종류에 대해 지원 되지 않는 API 버전</span><span class="sxs-lookup"><span data-stu-id="4e45a-231">API version not supported for hello resource type</span></span>
3. <span data-ttu-id="4e45a-232">위치 hello 리소스 종류에 대해 지원 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="4e45a-232">Location not supported for hello resource type</span></span>

<span data-ttu-id="4e45a-233">hello 지원 위치 및 API 버전에 대 한 제안을 hello 오류 메시지를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-233">hello error message should give you suggestions for hello supported locations and API versions.</span></span> <span data-ttu-id="4e45a-234">사용자 템플릿 tooone hello의 변경할 수 있습니다 제안 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-234">You can change your template tooone of hello suggested values.</span></span> <span data-ttu-id="4e45a-235">대부분의 공급자는 전체 열이 아니라 hello를 사용 하는 Azure 포털 또는 hello 명령줄 인터페이스에 의해 자동으로 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-235">Most providers are registered automatically by hello Azure portal or hello command-line interface you are using, but not all.</span></span> <span data-ttu-id="4e45a-236">하기 전에 특정 리소스 공급자를 사용 하지 않은 경우 해당 공급자 tooregister를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-236">If you have not used a particular resource provider before, you may need tooregister that provider.</span></span> <span data-ttu-id="4e45a-237">PowerShell 또는 Azure CLI를 통해 리소스 공급자에 대해 자세히 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="4e45a-238">**포털**</span><span class="sxs-lookup"><span data-stu-id="4e45a-238">**Portal**</span></span>

<span data-ttu-id="4e45a-239">Hello 등록 상태를 확인 하 고 hello 포털을 통해 리소스 공급자 네임 스페이스를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-239">You can see hello registration status and register a resource provider namespace through hello portal.</span></span>

1. <span data-ttu-id="4e45a-240">구독의 경우 **리소스 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-240">For your subscription, select **Resource providers**.</span></span>

   ![리소스 공급자 선택](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="4e45a-242">리소스 공급자의 hello 목록을 확인 하 고 필요한 경우 선택 hello **등록** 링크 tooregister hello 리소스 공급자 toodeploy hello 유형의 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-242">Look at hello list of resource providers, and if necessary, select hello **Register** link tooregister hello resource provider of hello type you are trying toodeploy.</span></span>

   ![리소스 공급자 나열](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="4e45a-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="4e45a-244">**PowerShell**</span></span>

<span data-ttu-id="4e45a-245">toosee 등록 상태를 사용 하 여 **Get AzureRmResourceProvider**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-245">toosee your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="4e45a-246">tooregister 공급자를 사용 하 여 **레지스터 AzureRmResourceProvider** hello 이름을 제공 하 고 원하는 tooregister hello 리소스 공급자의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-246">tooregister a provider, use **Register-AzureRmResourceProvider** and provide hello name of hello resource provider you wish tooregister.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="4e45a-247">특정 유형의 리소스에 대 한 tooget hello 지원 위치 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-247">tooget hello supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="4e45a-248">tooget hello에 대 한 특정 유형의 리소스를 사용 하 여 지원 되는 API 버전:</span><span class="sxs-lookup"><span data-stu-id="4e45a-248">tooget hello supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="4e45a-249">**Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="4e45a-249">**Azure CLI**</span></span>

<span data-ttu-id="4e45a-250">toosee hello 공급자가 등록 되어 있는지 여부를 사용 하 여 hello `azure provider list` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-250">toosee whether hello provider is registered, use hello `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="4e45a-251">tooregister 리소스 공급자를 사용 하 여 hello `azure provider register` 명령을 실행 하 고 hello 지정 *네임 스페이스* tooregister 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-251">tooregister a resource provider, use hello `azure provider register` command, and specify hello *namespace* tooregister.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="4e45a-252">toosee hello 지원 위치 및 리소스 유형에 대 한 API 버전 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-252">toosee hello supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="4e45a-253">QuotaExceeded 및 OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="4e45a-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="4e45a-254">또한 배포가 리소스 그룹, 구독, 계정 및 기타 범위당 할당량을 초과할 경우 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="4e45a-255">구독이 수 있지만 예를 들어 지역에 대 한 코어 toolimit hello 수를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-255">For example, your subscription may be configured toolimit hello number of cores for a region.</span></span> <span data-ttu-id="4e45a-256">가상 컴퓨터 크기를 허용 하는 hello 보다 더 많은 코어와 toodeploy을 시도 하면 오류가 발생 상자가 hello 할당량을 초과 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-256">If you attempt toodeploy a virtual machine with more cores than hello permitted amount, you receive an error stating hello quota has been exceeded.</span></span>
<span data-ttu-id="4e45a-257">전체 할당량 정보는 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e45a-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="4e45a-258">tooexamine 구독 할당량 코어에 대 한 hello를 사용할 수 있습니다 `azure vm list-usage` hello Azure CLI 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-258">tooexamine your subscription's quotas for cores, you can use hello `azure vm list-usage` command in hello Azure CLI.</span></span> <span data-ttu-id="4e45a-259">다음 예제는 hello 무료 평가판 계정을 4에 대 한 해당 hello 코어 할당량을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-259">hello following example illustrates that hello core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="4e45a-260">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-260">Which returns:</span></span>

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

<span data-ttu-id="4e45a-261">미국 서 부 지역 hello에에서 5 개 이상의 코어를 만드는 템플릿을 배포 하는 경우 다음과 같은 배포 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-261">If you deploy a template that creates more than four cores in hello West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="4e45a-262">PowerShell에서 hello를 사용할 수 있습니다 또는 **Get AzureRmVMUsage** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4e45a-262">Or in PowerShell, you can use hello **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="4e45a-263">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-263">Which returns:</span></span>

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

<span data-ttu-id="4e45a-264">이러한 경우 toohello 포털 이동 하 고 파일 지원 문제 tooraise toodeploy 넣을 hello 영역에 대 한 할당량 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-264">In these cases, you should go toohello portal and file a support issue tooraise your quota for hello region into which you want toodeploy.</span></span>

> [!NOTE]
> <span data-ttu-id="4e45a-265">리소스 그룹에 대 한 hello 할당량은 주의 하지 hello 전체 구독에 대 한 각 개별 지역에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-265">Remember that for resource groups, hello quota is for each individual region, not for hello entire subscription.</span></span> <span data-ttu-id="4e45a-266">Toodeploy 30 코어 West US에 필요한 경우 West US에 30 리소스 관리자 코어 tooask을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-266">If you need toodeploy 30 cores in West US, you have tooask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="4e45a-267">Toodeploy 30 코어 hello 영역 toowhich 중 하나에서 필요한 경우 액세스를 권한이 모든 지역에서 30 리소스 관리자 코어를 요청 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-267">If you need toodeploy 30 cores in any of hello regions toowhich you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="4e45a-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="4e45a-268">InvalidContentLink</span></span>
<span data-ttu-id="4e45a-269">때 hello 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-269">When you receive hello error message:</span></span>

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

<span data-ttu-id="4e45a-270">대개 toolink tooa 중첩 된 서식 파일을 사용할 수 없으면 시도 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-270">You have most likely attempted toolink tooa nested template that is not available.</span></span> <span data-ttu-id="4e45a-271">중첩 된 템플릿 hello에 대 한 제공 된 URI hello를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-271">Double check hello URI you provided for hello nested template.</span></span> <span data-ttu-id="4e45a-272">Hello 서식 파일에는 저장소 계정에 없는 경우 hello URI에 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-272">If hello template exists in a storage account, make sure hello URI is accessible.</span></span> <span data-ttu-id="4e45a-273">Toopass SAS 토큰을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-273">You may need toopass a SAS token.</span></span> <span data-ttu-id="4e45a-274">자세한 내용은 [Azure 리소스 관리자에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e45a-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="4e45a-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="4e45a-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="4e45a-276">구독에 배포 하는 동안 tooperform를 시도 하는 동작을 방지 하는 리소스 정책을 포함 하는 경우이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying tooperform during deployment.</span></span> <span data-ttu-id="4e45a-277">Hello 오류 메시지에서 hello 정책 식별자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-277">In hello error message, look for hello policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="4e45a-278">**PowerShell**, 해당 정책 식별자 hello로 제공 **Id** 배포를 차단한 hello 정책에 대 한 매개 변수 tooretrieve 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-278">In **PowerShell**, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="4e45a-279">**Azure CLI**, hello 정책 정의의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-279">In **Azure CLI**, provide hello name of hello policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="4e45a-280">자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="4e45a-280">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="4e45a-281">RequestDisallowedByPolicy 오류</span><span class="sxs-lookup"><span data-stu-id="4e45a-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="4e45a-282">[정책 toomanage 리소스를 사용 하 고 액세스 제어](resource-manager-policy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-282">[Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="4e45a-283">권한 부여 실패</span><span class="sxs-lookup"><span data-stu-id="4e45a-283">Authorization failed</span></span>
<span data-ttu-id="4e45a-284">없기 때문에 hello 계정 또는 서비스 toodeploy hello 리소스를 시도 하 고 사용자 액세스 tooperform 해당 작업을 배포 하는 동안 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-284">You may receive an error during deployment because hello account or service principal attempting toodeploy hello resources does not have access tooperform those actions.</span></span> <span data-ttu-id="4e45a-285">Azure Active Directory 또는 사용자 관리자 toocontrol 있는 id 고도로 정밀도 사용 하 여 어떤 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-285">Azure Active Directory enables you or your administrator toocontrol which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="4e45a-286">예를 들어 계정은 toohello 읽기 역할에 할당 된 없는 경우 수 toocreate 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-286">For example, if your account is assigned toohello Reader role, you are not able toocreate resources.</span></span> <span data-ttu-id="4e45a-287">이 경우 권한 부여에 실패했다는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="4e45a-288">역할 기반 액세스 제어에 대한 자세한 내용은 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e45a-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="4e45a-289">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e45a-289">Next steps</span></span>
* <span data-ttu-id="4e45a-290">작업을 감사 하는 방법에 대 한 toolearn 참조 [리소스 관리자와 작업을 감사](resource-group-audit.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-290">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="4e45a-291">배포 하는 동안 작업 toodetermine hello 오류에 대 한 toolearn 참조 [배포 작업을 보려면](resource-manager-deployment-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e45a-291">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
