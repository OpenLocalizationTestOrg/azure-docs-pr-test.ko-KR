---
title: "aaaAzure 리소스 공급자 및 리소스 종류 | Microsoft Docs"
description: "리소스 관리자, 스키마 및 사용 가능한 API 버전을 지 원하는 hello 리소스 공급자 및 hello 리소스를 호스팅할 수 있는 hello 영역에 설명 합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="e1a14-103">리소스 공급자 및 형식</span><span class="sxs-lookup"><span data-stu-id="e1a14-103">Resource providers and types</span></span>

<span data-ttu-id="e1a14-104">리소스를 배포할 때는 hello 리소스 공급자 및 형식에 대 한 tooretrieve 정보가 자주 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-104">When deploying resources, you frequently need tooretrieve information about hello resource providers and types.</span></span> <span data-ttu-id="e1a14-105">이 문서에서는 다음을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-105">In this article, you learn to:</span></span>

* <span data-ttu-id="e1a14-106">Azure의 모든 리소스 공급자 보기</span><span class="sxs-lookup"><span data-stu-id="e1a14-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="e1a14-107">리소스 공급자의 등록 상태 확인</span><span class="sxs-lookup"><span data-stu-id="e1a14-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="e1a14-108">리소스 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="e1a14-108">Register a resource provider</span></span>
* <span data-ttu-id="e1a14-109">리소스 공급자에 대한 리소스 종류 보기</span><span class="sxs-lookup"><span data-stu-id="e1a14-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="e1a14-110">리소스 종류에 대한 유효한 위치 보기</span><span class="sxs-lookup"><span data-stu-id="e1a14-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="e1a14-111">리소스 종류에 대한 유효한 API 버전 보기</span><span class="sxs-lookup"><span data-stu-id="e1a14-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="e1a14-112">Hello 포털, PowerShell 또는 Azure CLI를 통해 이러한 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-112">You can perform these steps through hello portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="e1a14-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1a14-113">PowerShell</span></span>

<span data-ttu-id="e1a14-114">toosee Azure 및 구독에 대 한 hello 등록 상태에서 모든 리소스 공급자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-114">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="e1a14-115">반환 결과는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="e1a14-116">리소스 공급자 등록 중 hello 리소스 공급자에 구독 toowork을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-116">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="e1a14-117">등록에 대 한 hello 범위 항상 hello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-117">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="e1a14-118">기본적으로 대부분의 리소스 공급자는 자동으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="e1a14-119">할 수 있습니다 toomanually 일부 리소스 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-119">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="e1a14-120">리소스 공급자 tooregister 있어야 권한 tooperform hello `/register/action` hello 리소스 공급자에 대 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-120">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="e1a14-121">이 작업은 참가자 hello 및 소유자 역할에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-121">This operation is included in hello Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="e1a14-122">반환 결과는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="e1a14-123">구독에 리소스 공급자의 리소스 종류가 아직 포함되어 있으면 해당 리소스 공급자를 등록 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="e1a14-124">특정 리소스 공급자를 사용 하 여 toosee 정보:</span><span class="sxs-lookup"><span data-stu-id="e1a14-124">toosee information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="e1a14-125">반환 결과는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="e1a14-126">리소스 공급자에 대 한 toosee hello 리소스 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-126">toosee hello resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="e1a14-127">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="e1a14-128">hello API 버전 tooa 버전의 hello 리소스 공급자가 릴리스되는 REST API 작업은 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-128">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="e1a14-129">리소스 공급자를 통해 새로운 기능, 새 버전의 hello REST API를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-129">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="e1a14-130">리소스 유형에 대 한 tooget hello 사용 가능한 API 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-130">tooget hello available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="e1a14-131">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="e1a14-132">모든 지역에서 리소스 관리자가 지원 되지만 hello 리소스 배포한 모든 지역에서 지원 되지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="e1a14-132">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="e1a14-133">또한 hello 리소스를 지 원하는 일부 영역을 사용 하지 못하게 하는 구독에 제한 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="e1a14-134">리소스 종류에 대 한 tooget hello 지원 위치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-134">tooget hello supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="e1a14-135">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="e1a14-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e1a14-136">Azure CLI</span></span>
<span data-ttu-id="e1a14-137">toosee Azure 및 구독에 대 한 hello 등록 상태에서 모든 리소스 공급자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-137">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="e1a14-138">반환 결과는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="e1a14-139">리소스 공급자 등록 중 hello 리소스 공급자에 구독 toowork을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-139">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="e1a14-140">등록에 대 한 hello 범위 항상 hello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-140">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="e1a14-141">기본적으로 대부분의 리소스 공급자는 자동으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="e1a14-142">할 수 있습니다 toomanually 일부 리소스 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-142">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="e1a14-143">리소스 공급자 tooregister 있어야 권한 tooperform hello `/register/action` hello 리소스 공급자에 대 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-143">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="e1a14-144">이 작업은 참가자 hello 및 소유자 역할에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-144">This operation is included in hello Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="e1a14-145">등록이 진행 중인 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="e1a14-146">구독에 리소스 공급자의 리소스 종류가 아직 포함되어 있으면 해당 리소스 공급자를 등록 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="e1a14-147">특정 리소스 공급자를 사용 하 여 toosee 정보:</span><span class="sxs-lookup"><span data-stu-id="e1a14-147">toosee information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="e1a14-148">반환 결과는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-148">Which returns results similar to:</span></span>

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

<span data-ttu-id="e1a14-149">리소스 공급자에 대 한 toosee hello 리소스 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-149">toosee hello resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="e1a14-150">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="e1a14-151">hello API 버전 tooa 버전의 hello 리소스 공급자가 릴리스되는 REST API 작업은 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-151">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="e1a14-152">리소스 공급자를 통해 새로운 기능, 새 버전의 hello REST API를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-152">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="e1a14-153">리소스 유형에 대 한 tooget hello 사용 가능한 API 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-153">tooget hello available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="e1a14-154">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="e1a14-155">모든 지역에서 리소스 관리자가 지원 되지만 hello 리소스 배포한 모든 지역에서 지원 되지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="e1a14-155">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="e1a14-156">또한 hello 리소스를 지 원하는 일부 영역을 사용 하지 못하게 하는 구독에 제한 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="e1a14-157">리소스 종류에 대 한 tooget hello 지원 위치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-157">tooget hello supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="e1a14-158">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="e1a14-159">포털</span><span class="sxs-lookup"><span data-stu-id="e1a14-159">Portal</span></span>

<span data-ttu-id="e1a14-160">Azure 및 구독에 대 한 hello 등록 상태에서 모든 리소스 공급자 선택 toosee **구독**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-160">toosee all resource providers in Azure, and hello registration status for your subscription, select **Subscriptions**.</span></span>

![구독 선택](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="e1a14-162">Hello 구독 tooview를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-162">Choose hello subscription tooview.</span></span>

![구독 지정](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="e1a14-164">선택 **리소스 공급자** 및 사용 가능한 리소스 공급자의 뷰 hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-164">Select **Resource providers** and view hello list of available resource providers.</span></span>

![리소스 공급자 보기](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="e1a14-166">리소스 공급자 등록 중 hello 리소스 공급자에 구독 toowork을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-166">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="e1a14-167">등록에 대 한 hello 범위 항상 hello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-167">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="e1a14-168">기본적으로 대부분의 리소스 공급자는 자동으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="e1a14-169">할 수 있습니다 toomanually 일부 리소스 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-169">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="e1a14-170">리소스 공급자 tooregister 있어야 권한 tooperform hello `/register/action` hello 리소스 공급자에 대 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-170">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="e1a14-171">이 작업은 참가자 hello 및 소유자 역할에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-171">This operation is included in hello Contributor and Owner roles.</span></span> <span data-ttu-id="e1a14-172">리소스 공급자 tooregister 선택 **등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-172">tooregister a resource provider, select **Register**.</span></span>

![리소스 공급자 등록](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="e1a14-174">구독에 리소스 공급자의 리소스 종류가 아직 포함되어 있으면 해당 리소스 공급자를 등록 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="e1a14-175">특정 리소스 공급자에 대 한 정보 toosee 선택 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-175">toosee information for a particular resource provider, select **More services**.</span></span>

![추가 서비스 선택](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="e1a14-177">검색할 **리소스 탐색기** hello 사용 가능한 옵션에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-177">Search for **Resource Explorer** and select it from hello available options.</span></span>

![리소스 탐색기 선택](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="e1a14-179">**공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-179">Select **Providers**.</span></span>

![공급자 선택](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="e1a14-181">리소스 공급자 선택 hello 및 리소스 tooview 한다는 것을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-181">Select hello resource provider and resource type that you want tooview.</span></span>

![리소스 종류 선택](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="e1a14-183">모든 지역에서 리소스 관리자가 지원 되지만 hello 리소스 배포한 모든 지역에서 지원 되지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="e1a14-183">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="e1a14-184">또한 hello 리소스를 지 원하는 일부 영역을 사용 하지 못하게 하는 구독에 제한 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> <span data-ttu-id="e1a14-185">hello 리소스 탐색기 hello 리소스 유형에 대 한 유효한 위치가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-185">hello resource explorer displays valid locations for hello resource type.</span></span>

![위치 표시](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="e1a14-187">hello API 버전 tooa 버전의 hello 리소스 공급자가 릴리스되는 REST API 작업은 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-187">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="e1a14-188">리소스 공급자를 통해 새로운 기능, 새 버전의 hello REST API를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-188">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> <span data-ttu-id="e1a14-189">리소스 탐색기 hello hello 리소스 종류에 대해 유효한 API 버전을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-189">hello resource explorer displays valid API versions for hello resource type.</span></span>

![API 버전 표시](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="e1a14-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e1a14-191">Next steps</span></span>
* <span data-ttu-id="e1a14-192">리소스 관리자 템플릿을 만드는 방법에 대해 toolearn 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-192">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e1a14-193">리소스를 배포 하는 방법에 대 한 toolearn 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-193">toolearn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="e1a14-194">리소스 공급자에 대 한 tooview hello 작업 참조 [Azure REST API](/rest/api/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1a14-194">tooview hello operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

