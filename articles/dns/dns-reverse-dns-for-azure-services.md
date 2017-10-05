---
title: "Azure 서비스에 대한 역방향 DNS | Microsoft Docs"
description: "Azure에서 호스트되는 서비스에 대해 역방향 DNS 조회를 구성하는 방법 알아보기"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 63701e1ce0c1c6dcf2ce02ebce272b8280395e7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="b8d34-103">Azure에서 호스트되는 서비스에 대해 역방향 DNS 구성</span><span class="sxs-lookup"><span data-stu-id="b8d34-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="b8d34-104">이 문서에서는 Azure에서 호스트되는 서비스에 대해 역방향 DNS 조회를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-104">This article explains how to configure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="b8d34-105">Azure의 서비스는 Azure에서 할당하고 Microsoft가 소유하는 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="b8d34-106">이러한 역방향 DNS 레코드(PTR 레코드)는 해당 Microsoft 소유의 역방향 DNS 조회 영역에서 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-106">These reverse DNS records (PTR records) must be created in the corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="b8d34-107">이 문서에서는 이 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-107">This article explains how to do this.</span></span>

<span data-ttu-id="b8d34-108">이 시나리오를 [Azure DNS의 할당된 IP 범위에 대한 역방향 DNS 조회 영역 호스트](dns-reverse-dns-hosting.md) 기능과 혼동하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-108">This scenario should not be confused with the ability to [host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="b8d34-109">이 경우 역방향 조회 영역으로 표시되는 IP 범위가 일반적으로 ISP에 의해 조직에 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-109">In this case, the IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="b8d34-110">이 문서를 읽기 전에 이 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md)에 익숙해지는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="b8d34-111">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="b8d34-112">Resource Manager 배포 모델에서 계산 리소스(예: 가상 컴퓨터, 가상 컴퓨터 크기 집합 또는 Service Fabric 클러스터)는 PublicIpAddress 리소스를 통해 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-112">In the Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="b8d34-113">역방향 DNS 조회는 PublicIpAddress의 'ReverseFqdn' 속성을 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-113">Reverse DNS lookups are configured using the 'ReverseFqdn' property of the PublicIpAddress.</span></span>
* <span data-ttu-id="b8d34-114">클래식 배포 모델에서 계산 리소스는 Cloud Services를 사용하여 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-114">In the Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="b8d34-115">역방향 DNS 조회는 클라우드 서비스의 'ReverseFqdn' 속성을 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-115">Reverse DNS lookups are configured using the 'ReverseDnsFqdn' property of the Cloud Service.</span></span>

<span data-ttu-id="b8d34-116">역방향 DNS는 현재 Azure App Service에 대해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-116">Reverse DNS is not currently supported for the Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="b8d34-117">역방향 DNS 레코드의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="b8d34-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="b8d34-118">타사에서는 DNS 도메인에 대한 Azure 서비스 매핑을 위해 역방향 DNS 레코드를 만들지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-118">A third party should not be able to create reverse DNS records for their Azure service mapping to your DNS domains.</span></span> <span data-ttu-id="b8d34-119">이를 방지하기 위해 Azure는 역방향 DNS 레코드에 지정된 도메인 이름이 동일한 Azure 구독의 PublicIpAddress 또는 클라우드 서비스에 대한 DNS 이름 또는 IP 주소와 같거나 이러한 항목으로 확인되는 경우에만 역방향 DNS 레코드 만들기를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-119">To prevent this, Azure only allows the creation of a reverse DNS record where domain name specified in the reverse DNS record is the same as, or resolves to, the DNS name or IP address of a PublicIpAddress or Cloud Service in the same Azure subscription.</span></span>

<span data-ttu-id="b8d34-120">이 유효성 검사는 역방향 DNS 레코드를 설정하거나 수정하는 경우에만 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-120">This validation is only performed when the reverse DNS record is set or modified.</span></span> <span data-ttu-id="b8d34-121">유효성 재검사는 정기적으로 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="b8d34-122">예를 들어 PublicIpAddress 리소스의 DNS 이름이 contosoapp1.northus.cloudapp.azure.com이고 IP 주소가 23.96.52.53이라고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-122">For example: suppose the PublicIpAddress resource has the DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="b8d34-123">PublicIpAddress에 대한 ReverseFqdn을 다음과 같이 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-123">The ReverseFqdn for the PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="b8d34-124">PublicIpAddress, contosoapp1.northus.cloudapp.azure.com의 DNS 이름</span><span class="sxs-lookup"><span data-stu-id="b8d34-124">The DNS name for the PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="b8d34-125">같은 구독의 다른 PublicIpAddress에 대한 DNS 이름(예: Contosoapp2.westus.cloudapp.azure.com)</span><span class="sxs-lookup"><span data-stu-id="b8d34-125">The DNS name for a different PublicIpAddress in the same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="b8d34-126">베니티 DNS 이름(예: app1.contoso.com). 이 이름은 contosoapp1.northus.cloudapp.azure.com 또는 동일한 구독의 다른 PublicIpAddress에 대한 CNAME으로 구성된 *최초* 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME to contosoapp1.northus.cloudapp.azure.com, or to a different PublicIpAddress in the same subscription.</span></span>
* <span data-ttu-id="b8d34-127">베니티 DNS 이름(예: app1.contoso.com). 이 이름은 IP 주소 23.96.52.53 또는 동일한 구독의 다른 PublicIpAddress에 대한 IP 주소의 A 레코드로 구성된 *최초* 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record to the IP address 23.96.52.53, or to the IP address of a different PublicIpAddress in the same subscription.</span></span>

<span data-ttu-id="b8d34-128">동일한 제약 조건이 Cloud Services에 대한 역방향 DNS에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-128">The same constraints apply to reverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="b8d34-129">PublicIpAddress 리소스에 대한 역방향 DNS</span><span class="sxs-lookup"><span data-stu-id="b8d34-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="b8d34-130">이 섹션에서는 Azure PowerShell, Azure CLI 1.0 또는 Azure CLI 2.0을 사용하여 Resource Manager 배포 모델에서 PublicIpAddress 리소스에 대한 역방향 DNS를 구성하는 방법에 대한 자세한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-130">This section provides detailed instructions for how to configure reverse DNS for PublicIpAddress resources in the Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="b8d34-131">현재 Azure Portal에서는 PublicIpAddress 리소스에 대한 역방향 DNS를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via the Azure portal.</span></span>

<span data-ttu-id="b8d34-132">Azure는 현재 IPv4 PublicIpAddress 리소스에 대해서만 역방향 DNS를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="b8d34-133">IPv6에 대해서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-to-an-existing-publicipaddresses"></a><span data-ttu-id="b8d34-134">기존 PublicIpAddresses에 역방향 DNS 추가</span><span class="sxs-lookup"><span data-stu-id="b8d34-134">Add reverse DNS to an existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="b8d34-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8d34-135">PowerShell</span></span>

<span data-ttu-id="b8d34-136">기존 PublicIpAddresses에 역방향 DNS를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="b8d34-136">To add reverse DNS to an existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="b8d34-137">DNS 이름이 아직 없는 기존 PublicIpAddress에 역방향 DNS를 추가하려면 DNS 이름도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-137">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="b8d34-138">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b8d34-138">Azure CLI 1.0</span></span>

<span data-ttu-id="b8d34-139">기존 PublicIpAddresses에 역방향 DNS를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="b8d34-139">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="b8d34-140">DNS 이름이 아직 없는 기존 PublicIpAddress에 역방향 DNS를 추가하려면 DNS 이름도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-140">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="b8d34-141">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b8d34-141">Azure CLI 2.0</span></span>

<span data-ttu-id="b8d34-142">기존 PublicIpAddresses에 역방향 DNS를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="b8d34-142">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="b8d34-143">DNS 이름이 아직 없는 기존 PublicIpAddress에 역방향 DNS를 추가하려면 DNS 이름도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-143">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="b8d34-144">역방향 DNS를 사용하여 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="b8d34-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="b8d34-145">역방향 DNS 속성이 이미 지정된 새 PublicIpAddress를 만들려면</span><span class="sxs-lookup"><span data-stu-id="b8d34-145">To create a new PublicIpAddress with the reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="b8d34-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8d34-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="b8d34-147">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b8d34-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="b8d34-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b8d34-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="b8d34-149">기존 PublicIpAddresses의 역방향 DNS 보기</span><span class="sxs-lookup"><span data-stu-id="b8d34-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="b8d34-150">기존 PublicIpAddress에 대해 구성된 값을 보려면</span><span class="sxs-lookup"><span data-stu-id="b8d34-150">To view the configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="b8d34-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8d34-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="b8d34-152">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b8d34-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="b8d34-153">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b8d34-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="b8d34-154">기존 공용 IP 주소에서 역방향 DNS 제거</span><span class="sxs-lookup"><span data-stu-id="b8d34-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="b8d34-155">기존 PublicIpAddress에서 역방향 DNS 속성을 제거하려면</span><span class="sxs-lookup"><span data-stu-id="b8d34-155">To remove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="b8d34-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8d34-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="b8d34-157">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b8d34-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="b8d34-158">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b8d34-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="b8d34-159">Cloud Services에 대한 역방향 DNS 구성</span><span class="sxs-lookup"><span data-stu-id="b8d34-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="b8d34-160">이 섹션에서는 Azure PowerShell을 사용하여 클래식 배포 모델에서 Cloud Services에 대한 역방향 DNS를 구성하는 방법에 대한 자세한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-160">This section provides detailed instructions for how to configure reverse DNS for Cloud Services in the Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="b8d34-161">Azure Portal, Azure CLI 1.0 또는 Azure CLI 2.0을 통한 Cloud Services에 대한 역방향 DNS 구성은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-161">Configuring reverse DNS for Cloud Services is not supported via the Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-to-existing-cloud-services"></a><span data-ttu-id="b8d34-162">기존 클라우드 서비스에 역방향 DNS 추가</span><span class="sxs-lookup"><span data-stu-id="b8d34-162">Add reverse DNS to existing Cloud Services</span></span>

<span data-ttu-id="b8d34-163">기존 클라우드 서비스에 역방향 DNS 레코드를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="b8d34-163">To add a reverse DNS record to an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="b8d34-164">역방향 DNS를 사용하여 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="b8d34-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="b8d34-165">역방향 DNS 속성이 이미 지정된 새 클라우드 서비스를 만들려면</span><span class="sxs-lookup"><span data-stu-id="b8d34-165">To create a new Cloud Service with the reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="b8d34-166">기존 클라우드 서비스에 대한 역방향 DNS 보기</span><span class="sxs-lookup"><span data-stu-id="b8d34-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="b8d34-167">기존 클라우드 서비스에 대한 역방향 DNS 속성을 보려면</span><span class="sxs-lookup"><span data-stu-id="b8d34-167">To view the reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="b8d34-168">기존 클라우드 서비스에서 역방향 DNS 제거</span><span class="sxs-lookup"><span data-stu-id="b8d34-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="b8d34-169">기존 클라우드 서비스에서 역방향 DNS 속성을 제거하려면</span><span class="sxs-lookup"><span data-stu-id="b8d34-169">To remove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="b8d34-170">FAQ</span><span class="sxs-lookup"><span data-stu-id="b8d34-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="b8d34-171">역방향 DNS 레코드의 비용은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="b8d34-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="b8d34-172">무료입니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-172">They're free!</span></span>  <span data-ttu-id="b8d34-173">역방향 DNS 레코드 또는 쿼리에 대한 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-the-internet"></a><span data-ttu-id="b8d34-174">인터넷에서 내 역방향 DNS 레코드가 확인되나요?</span><span class="sxs-lookup"><span data-stu-id="b8d34-174">Will my reverse DNS records resolve from the internet?</span></span>

<span data-ttu-id="b8d34-175">예.</span><span class="sxs-lookup"><span data-stu-id="b8d34-175">Yes.</span></span> <span data-ttu-id="b8d34-176">Azure 서비스에 대해 역방향 DNS 속성을 설정하면 역방향 DNS 레코드를 모든 인터넷 사용자에 대해 확인하는 데 필요한 DNS 영역 및 DNS 위임을 Azure에서 모두 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-176">Once you set the reverse DNS property for your Azure service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="b8d34-177">내 Azure 서비스에 대해 기본 역방향 DNS 레코드가 생성되나요?</span><span class="sxs-lookup"><span data-stu-id="b8d34-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="b8d34-178">안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-178">No.</span></span> <span data-ttu-id="b8d34-179">역방향 DNS는 옵트인(opt in) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="b8d34-180">역방향 레코드를 구성하지 않으면 기본 역방향 DNS 레코드가 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-180">No default reverse DNS records are created if you choose not to configure them.</span></span>

### <a name="what-is-the-format-for-the-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="b8d34-181">FQDN(정규화된 도메인 이름)의 형식은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="b8d34-181">What is the format for the fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="b8d34-182">FQDN은 정방향 순서로 지정되고 점으로 끝나야 합니다(예: "app1.contoso.com.").</span><span class="sxs-lookup"><span data-stu-id="b8d34-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-the-validation-check-for-the-reverse-dns-ive-specified-fails"></a><span data-ttu-id="b8d34-183">내가 지정한 역방향 DNS의 유효성 검사가 실패하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="b8d34-183">What happens if the validation check for the reverse DNS I've specified fails?</span></span>

<span data-ttu-id="b8d34-184">역방향 DNS 유효성 검사가 실패하는 경우 역방향 DNS 레코드를 구성하는 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-184">Where the reverse DNS validation check fails, the operation to configure the reverse DNS record fails.</span></span> <span data-ttu-id="b8d34-185">필요에 따라 역방향 DNS 값을 수정하고 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="b8d34-185">Correct the reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="b8d34-186">Azure App Service에 대한 역방향 DNS를 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b8d34-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="b8d34-187">안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-187">No.</span></span> <span data-ttu-id="b8d34-188">역방향 DNS는 Azure App Service에 대해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-188">Reverse DNS is not supported for the Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="b8d34-189">내 Azure 대해 다중 역방향 DNS 레코드를 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b8d34-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="b8d34-190">안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-190">No.</span></span> <span data-ttu-id="b8d34-191">Azure는 각 Azure Cloud Service 또는 PublicIpAddress에 대해 단일 역방향 DNS 레코드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="b8d34-192">IPv6 PublicIpAddress 리소스에 대한 역방향 DNS를 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b8d34-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="b8d34-193">안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-193">No.</span></span> <span data-ttu-id="b8d34-194">Azure는 현재 IPv4 PublicIpAddress 리소스 및 Cloud Services에 대해서만 역방향 DNS를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-to-external-domains-from-my-azure-compute-services"></a><span data-ttu-id="b8d34-195">Azure 계산 서비스에서 외부 도메인으로 전자 메일을 보낼 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b8d34-195">Can I send emails to external domains from my Azure Compute services?</span></span>

<span data-ttu-id="b8d34-196">안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-196">No.</span></span> <span data-ttu-id="b8d34-197">[Azure Compute Services는 외부 도메인으로의 전자 메일 전송을 지원하지 않습니다](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/).</span><span class="sxs-lookup"><span data-stu-id="b8d34-197">[Azure Compute services do not support sending emails to external domains](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8d34-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8d34-198">Next steps</span></span>

<span data-ttu-id="b8d34-199">역방향 DNS에 대한 자세한 내용은 [Wikipedia에서 역방향 DNS 조회](http://en.wikipedia.org/wiki/Reverse_DNS_lookup)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8d34-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="b8d34-200">[Azure DNS에서 ISP 할당 IP 범위에 대한 역방향 조회 영역 호스트](dns-reverse-dns-for-azure-services.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b8d34-200">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

