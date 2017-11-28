---
title: "Azure 서비스에 대 한 DNS aaaReverse | Microsoft Docs"
description: "Tooconfigure Azure에서 호스팅된 서비스에 대 한 DNS 조회를 반대로 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="0f2f0-103">Azure에서 호스트되는 서비스에 대해 역방향 DNS 구성</span><span class="sxs-lookup"><span data-stu-id="0f2f0-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="0f2f0-104">이 문서에서는 tooconfigure Azure에서 호스팅된 서비스에 대 한 DNS 조회를 반대로 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-104">This article explains how tooconfigure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="0f2f0-105">Azure의 서비스는 Azure에서 할당하고 Microsoft가 소유하는 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="0f2f0-106">영역에 있는 hello 해당 Microsoft 소유 역방향 DNS 조회 (PTR 레코드)이 역방향 DNS 레코드를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-106">These reverse DNS records (PTR records) must be created in hello corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="0f2f0-107">이 문서에서는 설명 어떻게 toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-107">This article explains how toodo this.</span></span>

<span data-ttu-id="0f2f0-108">이 시나리오 혼동 해서는 안 hello 기능과 함께 너무[Azure DNS에서 할당 된 IP 범위에 대 한 hello 역방향 DNS 조회 영역을 호스팅하려](dns-reverse-dns-hosting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-108">This scenario should not be confused with hello ability too[host hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="0f2f0-109">이 경우 hello 역방향 조회 영역을 나타내는 hello IP 범위 할당 해야 tooyour 조직 일반적으로 ISP가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-109">In this case, hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="0f2f0-110">이 문서를 읽기 전에 이 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md)에 익숙해지는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="0f2f0-111">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="0f2f0-112">Hello 리소스 관리자 배포 모델에서 계산 리소스 (예: 가상 컴퓨터, 가상 컴퓨터 크기 집합 또는 서비스 패브릭 클러스터) PublicIpAddress 리소스를 통해 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-112">In hello Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="0f2f0-113">DNS 역방향 조회는 hello 'ReverseFqdn' hello PublicIpAddress 속성을 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-113">Reverse DNS lookups are configured using hello 'ReverseFqdn' property of hello PublicIpAddress.</span></span>
* <span data-ttu-id="0f2f0-114">Hello 클래식 배포 모델에서는 계산 리소스는 클라우드 서비스를 사용 하 여 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-114">In hello Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="0f2f0-115">DNS 역방향 조회는 hello 클라우드 서비스의 hello 'ReverseDnsFqdn' 속성을 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-115">Reverse DNS lookups are configured using hello 'ReverseDnsFqdn' property of hello Cloud Service.</span></span>

<span data-ttu-id="0f2f0-116">역방향 DNS hello Azure 앱 서비스에 대 한 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-116">Reverse DNS is not currently supported for hello Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="0f2f0-117">역방향 DNS 레코드의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="0f2f0-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="0f2f0-118">제 3 자가 자신의 Azure 서비스 매핑 tooyour DNS 도메인에 대 한 역방향 DNS 레코드 수 toocreate 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-118">A third party should not be able toocreate reverse DNS records for their Azure service mapping tooyour DNS domains.</span></span> <span data-ttu-id="0f2f0-119">tooprevent이 Azure hello 여기서 hello 역방향 DNS 레코드에 지정 된 도메인 이름과 hello와 동일 또는 동일 hello에 DNS 이름 또는 IP 주소 PublicIpAddress 또는 클라우드 hello로 확인 되 면 서비스를 사용 하는 역방향 DNS 레코드 만들기가 하나만 허용 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-119">tooprevent this, Azure only allows hello creation of a reverse DNS record where domain name specified in hello reverse DNS record is hello same as, or resolves to, hello DNS name or IP address of a PublicIpAddress or Cloud Service in hello same Azure subscription.</span></span>

<span data-ttu-id="0f2f0-120">이 유효성 검사는 hello 역방향 DNS 레코드를 설정 하거나 수정할 때만 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-120">This validation is only performed when hello reverse DNS record is set or modified.</span></span> <span data-ttu-id="0f2f0-121">유효성 재검사는 정기적으로 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="0f2f0-122">예를 들어: hello PublicIpAddress 리소스 hello DNS 이름 contosoapp1.northus.cloudapp.azure.com 및 IP 주소 23.96.52.53 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-122">For example: suppose hello PublicIpAddress resource has hello DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="0f2f0-123">ReverseFqdn PublicIpAddress로 지정할 수 있으며 hello에 대 한 hello:</span><span class="sxs-lookup"><span data-stu-id="0f2f0-123">hello ReverseFqdn for hello PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="0f2f0-124">PublicIpAddress hello에 대 한 hello DNS 이름, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="0f2f0-124">hello DNS name for hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="0f2f0-125">hello DNS 이름에서 다른 PublicIpAddress hello에 대 한 동일한 contosoapp2.westus.cloudapp.azure.com 같은 구독을</span><span class="sxs-lookup"><span data-stu-id="0f2f0-125">hello DNS name for a different PublicIpAddress in hello same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="0f2f0-126">베 니 티 DNS 이름, app1.contoso.com, 등으로이 이름은 *첫 번째* CNAME toocontosoapp1.northus.cloudapp.azure.com 또는 구성 tooa 다른 PublicIpAddress hello에 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME toocontosoapp1.northus.cloudapp.azure.com, or tooa different PublicIpAddress in hello same subscription.</span></span>
* <span data-ttu-id="0f2f0-127">베 니 티 DNS 이름, app1.contoso.com, 등으로이 이름은 *첫 번째* hello에 A 레코드 toohello IP 주소로 23.96.52.53, 또는 다른 PublicIpAddress의 toohello IP 주소 구성 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record toohello IP address 23.96.52.53, or toohello IP address of a different PublicIpAddress in hello same subscription.</span></span>

<span data-ttu-id="0f2f0-128">hello 동일한 제약 조건을 적용 tooreverse DNS 클라우드 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-128">hello same constraints apply tooreverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="0f2f0-129">PublicIpAddress 리소스에 대한 역방향 DNS</span><span class="sxs-lookup"><span data-stu-id="0f2f0-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="0f2f0-130">이 섹션에서는 tooconfigure Azure PowerShell, Azure CLI 1.0 또는 Azure CLI 2.0을 사용 하 여 hello 리소스 관리자 배포 모델의 PublicIpAddress 리소스에 대 한 DNS를 반대로 하는 방법에 대 한 자세한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-130">This section provides detailed instructions for how tooconfigure reverse DNS for PublicIpAddress resources in hello Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="0f2f0-131">현재 hello Azure 포털을 통해 PublicIpAddress 리소스에 대 한 역방향 DNS 구성 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via hello Azure portal.</span></span>

<span data-ttu-id="0f2f0-132">Azure는 현재 IPv4 PublicIpAddress 리소스에 대해서만 역방향 DNS를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="0f2f0-133">IPv6에 대해서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a><span data-ttu-id="0f2f0-134">역방향 DNS tooan PublicIpAddresses 기존 추가</span><span class="sxs-lookup"><span data-stu-id="0f2f0-134">Add reverse DNS tooan existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="0f2f0-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f2f0-135">PowerShell</span></span>

<span data-ttu-id="0f2f0-136">tooadd 역방향 DNS tooan PublicIpAddress 기존:</span><span class="sxs-lookup"><span data-stu-id="0f2f0-136">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="0f2f0-137">tooadd 역방향 DNS 이름에 아직 PublicIpAddress 기존 DNS tooan, DNS 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-137">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="0f2f0-138">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0f2f0-138">Azure CLI 1.0</span></span>

<span data-ttu-id="0f2f0-139">tooadd 역방향 DNS tooan PublicIpAddress 기존:</span><span class="sxs-lookup"><span data-stu-id="0f2f0-139">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="0f2f0-140">tooadd 역방향 DNS 이름에 아직 PublicIpAddress 기존 DNS tooan, DNS 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-140">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="0f2f0-141">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0f2f0-141">Azure CLI 2.0</span></span>

<span data-ttu-id="0f2f0-142">tooadd 역방향 DNS tooan PublicIpAddress 기존:</span><span class="sxs-lookup"><span data-stu-id="0f2f0-142">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="0f2f0-143">tooadd 역방향 DNS 이름에 아직 PublicIpAddress 기존 DNS tooan, DNS 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-143">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="0f2f0-144">역방향 DNS를 사용하여 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="0f2f0-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="0f2f0-145">hello 역방향 DNS 속성이 이미 지정 된 새 PublicIpAddress toocreate:</span><span class="sxs-lookup"><span data-stu-id="0f2f0-145">toocreate a new PublicIpAddress with hello reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0f2f0-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f2f0-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="0f2f0-147">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0f2f0-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="0f2f0-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0f2f0-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="0f2f0-149">기존 PublicIpAddresses의 역방향 DNS 보기</span><span class="sxs-lookup"><span data-stu-id="0f2f0-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="0f2f0-150">tooview hello 기존 PublicIpAddress에 대 한 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-150">tooview hello configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0f2f0-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f2f0-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="0f2f0-152">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0f2f0-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="0f2f0-153">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0f2f0-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="0f2f0-154">기존 공용 IP 주소에서 역방향 DNS 제거</span><span class="sxs-lookup"><span data-stu-id="0f2f0-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="0f2f0-155">tooremove 기존 PublicIpAddress에서 역방향 DNS 속성:</span><span class="sxs-lookup"><span data-stu-id="0f2f0-155">tooremove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0f2f0-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f2f0-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="0f2f0-157">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0f2f0-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="0f2f0-158">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0f2f0-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="0f2f0-159">Cloud Services에 대한 역방향 DNS 구성</span><span class="sxs-lookup"><span data-stu-id="0f2f0-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="0f2f0-160">이 섹션에서는 어떻게 tooconfigure 역방향 DNS 클라우드 서비스에 대 한 Azure PowerShell을 사용 하 여 hello 클래식 배포 모델에 대 한 자세한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-160">This section provides detailed instructions for how tooconfigure reverse DNS for Cloud Services in hello Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="0f2f0-161">클라우드 서비스에 대 한 역방향 DNS 구성 Azure CLI 1.0 또는 Azure CLI 2.0 hello Azure 포털을 통해 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-161">Configuring reverse DNS for Cloud Services is not supported via hello Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-tooexisting-cloud-services"></a><span data-ttu-id="0f2f0-162">역방향 DNS tooexisting 클라우드 서비스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-162">Add reverse DNS tooexisting Cloud Services</span></span>

<span data-ttu-id="0f2f0-163">기존 클라우드 서비스는 역방향 DNS 레코드 tooan tooadd:</span><span class="sxs-lookup"><span data-stu-id="0f2f0-163">tooadd a reverse DNS record tooan existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="0f2f0-164">역방향 DNS를 사용하여 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="0f2f0-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="0f2f0-165">toocreate hello 역방향 DNS 속성이 이미 지정 된 새 클라우드 서비스:</span><span class="sxs-lookup"><span data-stu-id="0f2f0-165">toocreate a new Cloud Service with hello reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="0f2f0-166">기존 클라우드 서비스에 대한 역방향 DNS 보기</span><span class="sxs-lookup"><span data-stu-id="0f2f0-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="0f2f0-167">tooview hello 기존 클라우드 서비스에 대 한 DNS 속성 역방향:</span><span class="sxs-lookup"><span data-stu-id="0f2f0-167">tooview hello reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="0f2f0-168">기존 클라우드 서비스에서 역방향 DNS 제거</span><span class="sxs-lookup"><span data-stu-id="0f2f0-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="0f2f0-169">기존 클라우드 서비스에서 역방향 DNS 속성 tooremove:</span><span class="sxs-lookup"><span data-stu-id="0f2f0-169">tooremove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="0f2f0-170">FAQ</span><span class="sxs-lookup"><span data-stu-id="0f2f0-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="0f2f0-171">역방향 DNS 레코드의 비용은 얼마인가요?</span><span class="sxs-lookup"><span data-stu-id="0f2f0-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="0f2f0-172">무료입니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-172">They're free!</span></span>  <span data-ttu-id="0f2f0-173">역방향 DNS 레코드 또는 쿼리에 대한 추가 비용은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a><span data-ttu-id="0f2f0-174">내 역방향 DNS 레코드 확인은 인터넷을 hello?</span><span class="sxs-lookup"><span data-stu-id="0f2f0-174">Will my reverse DNS records resolve from hello internet?</span></span>

<span data-ttu-id="0f2f0-175">예.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-175">Yes.</span></span> <span data-ttu-id="0f2f0-176">Azure 서비스에 대 한 hello 역방향 DNS 속성을 설정 하면 모든 hello DNS 위임이 Azure가 관리 하 고 DNS 영역 모든 인터넷 사용자가 확인 하는 역방향 DNS 레코드 tooensure 필요한.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-176">Once you set hello reverse DNS property for your Azure service, Azure manages all hello DNS delegations and DNS zones required tooensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="0f2f0-177">내 Azure 서비스에 대해 기본 역방향 DNS 레코드가 생성되나요?</span><span class="sxs-lookup"><span data-stu-id="0f2f0-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="0f2f0-178">안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-178">No.</span></span> <span data-ttu-id="0f2f0-179">역방향 DNS는 옵트인(opt in) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="0f2f0-180">기본값은 없습니다 tooconfigure 하지 않으려는 경우 역방향 DNS 레코드가 만들어집니다. 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-180">No default reverse DNS records are created if you choose not tooconfigure them.</span></span>

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="0f2f0-181">Hello 정규화 된 도메인 이름 (FQDN)에 대 한 hello 형식은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0f2f0-181">What is hello format for hello fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="0f2f0-182">FQDN은 정방향 순서로 지정되고 점으로 끝나야 합니다(예: "app1.contoso.com.").</span><span class="sxs-lookup"><span data-stu-id="0f2f0-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a><span data-ttu-id="0f2f0-183">Hello에 대 한 유효성 검사 hello 역방향 DNS 필자가 지정한 경우 실패 하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="0f2f0-183">What happens if hello validation check for hello reverse DNS I've specified fails?</span></span>

<span data-ttu-id="0f2f0-184">Hello 역방향 DNS 유효성 검사에 실패 하는 경우 hello 작업 tooconfigure hello 역방향 DNS 레코드는 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-184">Where hello reverse DNS validation check fails, hello operation tooconfigure hello reverse DNS record fails.</span></span> <span data-ttu-id="0f2f0-185">필요에 따라 hello 역방향 DNS 값을 수정 하 고 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-185">Correct hello reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="0f2f0-186">Azure App Service에 대한 역방향 DNS를 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0f2f0-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="0f2f0-187">아니요.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-187">No.</span></span> <span data-ttu-id="0f2f0-188">역방향 DNS hello Azure 앱 서비스에 대 한 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-188">Reverse DNS is not supported for hello Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="0f2f0-189">내 Azure 대해 다중 역방향 DNS 레코드를 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0f2f0-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="0f2f0-190">안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-190">No.</span></span> <span data-ttu-id="0f2f0-191">Azure는 각 Azure Cloud Service 또는 PublicIpAddress에 대해 단일 역방향 DNS 레코드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="0f2f0-192">IPv6 PublicIpAddress 리소스에 대한 역방향 DNS를 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0f2f0-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="0f2f0-193">안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-193">No.</span></span> <span data-ttu-id="0f2f0-194">Azure는 현재 IPv4 PublicIpAddress 리소스 및 Cloud Services에 대해서만 역방향 DNS를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a><span data-ttu-id="0f2f0-195">보내기 메일 tooexternal 도메인 내 Azure 계산 서비스에서</span><span class="sxs-lookup"><span data-stu-id="0f2f0-195">Can I send emails tooexternal domains from my Azure Compute services?</span></span>

<span data-ttu-id="0f2f0-196">아니요.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-196">No.</span></span> [<span data-ttu-id="0f2f0-197">Azure 계산 서비스 보내는 전자 메일 tooexternal 도메인을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-197">Azure Compute services do not support sending emails tooexternal domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="0f2f0-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f2f0-198">Next steps</span></span>

<span data-ttu-id="0f2f0-199">역방향 DNS에 대한 자세한 내용은 [Wikipedia에서 역방향 DNS 조회](http://en.wikipedia.org/wiki/Reverse_DNS_lookup)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="0f2f0-200">너무 방법에 대해 알아봅니다[Azure dns에서 ISP에 할당 된 IP 범위에 대 한 호스트 hello 역방향 조회 영역](dns-reverse-dns-for-azure-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f2f0-200">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

