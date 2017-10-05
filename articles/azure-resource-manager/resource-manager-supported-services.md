---
title: "Azure 리소스 공급자 및 리소스 종류 | Microsoft Docs"
description: "리소스 관리자, 스키마, 제공되는 API 버전 및 리소스를 호스팅할 수 있는 지역을 지원하는 리소스 공급자에 대해 설명합니다."
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
ms.openlocfilehash: 6a9128f45d4199404019cee594842d59c7f1aaf3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="c8dff-103">리소스 공급자 및 형식</span><span class="sxs-lookup"><span data-stu-id="c8dff-103">Resource providers and types</span></span>

<span data-ttu-id="c8dff-104">리소스를 배포할 때는 리소스 공급자 및 형식에 대한 정보를 자주 검색하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-104">When deploying resources, you frequently need to retrieve information about the resource providers and types.</span></span> <span data-ttu-id="c8dff-105">이 문서에서는 다음을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-105">In this article, you learn to:</span></span>

* <span data-ttu-id="c8dff-106">Azure의 모든 리소스 공급자 보기</span><span class="sxs-lookup"><span data-stu-id="c8dff-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="c8dff-107">리소스 공급자의 등록 상태 확인</span><span class="sxs-lookup"><span data-stu-id="c8dff-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="c8dff-108">리소스 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="c8dff-108">Register a resource provider</span></span>
* <span data-ttu-id="c8dff-109">리소스 공급자에 대한 리소스 종류 보기</span><span class="sxs-lookup"><span data-stu-id="c8dff-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="c8dff-110">리소스 종류에 대한 유효한 위치 보기</span><span class="sxs-lookup"><span data-stu-id="c8dff-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="c8dff-111">리소스 종류에 대한 유효한 API 버전 보기</span><span class="sxs-lookup"><span data-stu-id="c8dff-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="c8dff-112">이러한 단계는 포털, PowerShell 또는 Azure CLI를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-112">You can perform these steps through the portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="c8dff-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8dff-113">PowerShell</span></span>

<span data-ttu-id="c8dff-114">Azure의 모든 리소스 공급자와 구독에 대한 등록 상태를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-114">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="c8dff-115">반환 결과는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="c8dff-116">리소스 공급자를 등록하면 구독이 리소스 공급자에서 작동하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-116">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="c8dff-117">등록 범위는 항상 해당 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-117">The scope for registration is always the subscription.</span></span> <span data-ttu-id="c8dff-118">기본적으로 대부분의 리소스 공급자는 자동으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="c8dff-119">그러나 일부 리소스 공급자는 수동으로 등록해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-119">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="c8dff-120">리소스 공급자를 등록하려면 리소스 공급자에 대해 `/register/action` 작업을 수행할 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-120">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="c8dff-121">이 작업은 참가자 및 소유자 역할에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-121">This operation is included in the Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="c8dff-122">반환 결과는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="c8dff-123">구독에 리소스 공급자의 리소스 종류가 아직 포함되어 있으면 해당 리소스 공급자를 등록 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="c8dff-124">특정 리소스 공급자에 대한 정보를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-124">To see information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="c8dff-125">반환 결과는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="c8dff-126">리소스 공급자에 대한 리소스 종류를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-126">To see the resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="c8dff-127">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="c8dff-128">API 버전은 리소스 공급자가 릴리스하는 REST API 작업의 버전에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-128">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="c8dff-129">리소스 공급자는 새 기능을 사용하도록 설정할 때 새 버전의 REST API를 릴리스합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-129">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="c8dff-130">리소스 종류의 사용 가능한 API 버전을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-130">To get the available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="c8dff-131">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="c8dff-132">리소스 관리자는 모든 지역에서 지원되지만 배포한 리소스는 모든 지역에서 지원되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-132">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="c8dff-133">또한 해당 리소스를 지원하는 일부 지역을 사용하지 못하도록 구독에 대한 제한 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="c8dff-134">리소스 종류의 지원되는 위치를 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-134">To get the supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="c8dff-135">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="c8dff-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c8dff-136">Azure CLI</span></span>
<span data-ttu-id="c8dff-137">Azure의 모든 리소스 공급자와 구독에 대한 등록 상태를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-137">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="c8dff-138">반환 결과는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="c8dff-139">리소스 공급자를 등록하면 구독이 리소스 공급자에서 작동하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-139">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="c8dff-140">등록 범위는 항상 해당 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-140">The scope for registration is always the subscription.</span></span> <span data-ttu-id="c8dff-141">기본적으로 대부분의 리소스 공급자는 자동으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="c8dff-142">그러나 일부 리소스 공급자는 수동으로 등록해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-142">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="c8dff-143">리소스 공급자를 등록하려면 리소스 공급자에 대해 `/register/action` 작업을 수행할 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-143">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="c8dff-144">이 작업은 참가자 및 소유자 역할에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-144">This operation is included in the Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="c8dff-145">등록이 진행 중인 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="c8dff-146">구독에 리소스 공급자의 리소스 종류가 아직 포함되어 있으면 해당 리소스 공급자를 등록 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="c8dff-147">특정 리소스 공급자에 대한 정보를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-147">To see information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="c8dff-148">반환 결과는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-148">Which returns results similar to:</span></span>

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

<span data-ttu-id="c8dff-149">리소스 공급자에 대한 리소스 종류를 보려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-149">To see the resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="c8dff-150">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="c8dff-151">API 버전은 리소스 공급자가 릴리스하는 REST API 작업의 버전에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-151">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="c8dff-152">리소스 공급자는 새 기능을 사용하도록 설정할 때 새 버전의 REST API를 릴리스합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-152">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="c8dff-153">리소스 종류의 사용 가능한 API 버전을 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-153">To get the available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="c8dff-154">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="c8dff-155">리소스 관리자는 모든 지역에서 지원되지만 배포한 리소스는 모든 지역에서 지원되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-155">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="c8dff-156">또한 해당 리소스를 지원하는 일부 지역을 사용하지 못하도록 구독에 대한 제한 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="c8dff-157">리소스 종류의 지원되는 위치를 가져오려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-157">To get the supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="c8dff-158">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="c8dff-159">포털</span><span class="sxs-lookup"><span data-stu-id="c8dff-159">Portal</span></span>

<span data-ttu-id="c8dff-160">Azure의 모든 리소스 공급자 및 구독에 대한 등록 상태를 보려면 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-160">To see all resource providers in Azure, and the registration status for your subscription, select **Subscriptions**.</span></span>

![구독 선택](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="c8dff-162">보려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-162">Choose the subscription to view.</span></span>

![구독 지정](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="c8dff-164">**리소스 공급자**를 선택하고 사용 가능한 리소스 공급자의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-164">Select **Resource providers** and view the list of available resource providers.</span></span>

![리소스 공급자 보기](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="c8dff-166">리소스 공급자를 등록하면 구독이 리소스 공급자에서 작동하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-166">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="c8dff-167">등록 범위는 항상 해당 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-167">The scope for registration is always the subscription.</span></span> <span data-ttu-id="c8dff-168">기본적으로 대부분의 리소스 공급자는 자동으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="c8dff-169">그러나 일부 리소스 공급자는 수동으로 등록해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-169">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="c8dff-170">리소스 공급자를 등록하려면 리소스 공급자에 대해 `/register/action` 작업을 수행할 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-170">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="c8dff-171">이 작업은 참가자 및 소유자 역할에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-171">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="c8dff-172">리소스 공급자를 등록하려면 **등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-172">To register a resource provider, select **Register**.</span></span>

![리소스 공급자 등록](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="c8dff-174">구독에 리소스 공급자의 리소스 종류가 아직 포함되어 있으면 해당 리소스 공급자를 등록 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="c8dff-175">특정 리소스 공급자에 대한 정보를 보려면 **추가 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-175">To see information for a particular resource provider, select **More services**.</span></span>

![추가 서비스 선택](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="c8dff-177">**리소스 탐색기**를 검색하고 사용 가능한 옵션 중에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-177">Search for **Resource Explorer** and select it from the available options.</span></span>

![리소스 탐색기 선택](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="c8dff-179">**공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-179">Select **Providers**.</span></span>

![공급자 선택](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="c8dff-181">보려는 리소스 공급자 및 리소스 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-181">Select the resource provider and resource type that you want to view.</span></span>

![리소스 종류 선택](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="c8dff-183">리소스 관리자는 모든 지역에서 지원되지만 배포한 리소스는 모든 지역에서 지원되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-183">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="c8dff-184">또한 해당 리소스를 지원하는 일부 지역을 사용하지 못하도록 구독에 대한 제한 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> <span data-ttu-id="c8dff-185">리소스 탐색기에는 리소스 종류에 대한 유효한 위치가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-185">The resource explorer displays valid locations for the resource type.</span></span>

![위치 표시](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="c8dff-187">API 버전은 리소스 공급자가 릴리스하는 REST API 작업의 버전에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-187">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="c8dff-188">리소스 공급자는 새 기능을 사용하도록 설정할 때 새 버전의 REST API를 릴리스합니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-188">As a resource provider enables new features, it releases a new version of the REST API.</span></span> <span data-ttu-id="c8dff-189">리소스 탐색기에는 리소스 종류에 대한 유효한 API 버전이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8dff-189">The resource explorer displays valid API versions for the resource type.</span></span>

![API 버전 표시](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="c8dff-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c8dff-191">Next steps</span></span>
* <span data-ttu-id="c8dff-192">리소스 관리자 템플릿을 만드는 방법에 대한 자세한 내용은 [Azure 리소스 관리자 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8dff-192">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c8dff-193">리소스 배포에 대한 자세한 내용은 [Azure 리소스 관리자 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8dff-193">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="c8dff-194">리소스 공급자에 대한 작업을 보려면 [Azure REST API](/rest/api/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8dff-194">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

