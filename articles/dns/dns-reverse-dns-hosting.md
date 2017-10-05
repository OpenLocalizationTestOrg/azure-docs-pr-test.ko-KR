---
title: "Azure DNS에서 역방향 DNS 조회 영역 호스트 | Microsoft Docs"
description: "Azure DNS를 사용하여 IP 범위에 대한 역방향 DNS 조회 영역을 호스트하는 방법을 알아봅니다."
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
ms.openlocfilehash: 3e10b25d2f9b91c96af2958fef6dc6a4fdbff301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="d4cf7-103">Azure DNS에서 역방향 DNS 조회 영역 호스트</span><span class="sxs-lookup"><span data-stu-id="d4cf7-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="d4cf7-104">이 문서에서는 Azure DNS에서 할당된 IP 범위에 대한 역방향 DNS 조회 영역을 호스트하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="d4cf7-105">역방향 조회 영역으로 표시되는 IP 범위가 일반적으로 ISP에 의해 조직에 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-105">The IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="d4cf7-106">Azure 서비스에 할당된 Azure 소유의 IP 주소에 대한 역방향 DNS를 구성하려면 [Azure 서비스에 할당된 IP 주소에 대한 역방향 조회 구성](dns-reverse-dns-for-azure-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-106">To configure reverse DNS for Azure-owned IP address assigned to your Azure service, see [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="d4cf7-107">이 문서를 읽기 전에 이 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md)에 익숙해지는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="d4cf7-108">이 문서에서는 Azure Portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0을 사용하여 역방향 조회 DNS 영역 및 레코드를 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-108">This article walks you through the steps to create your first reverse lookup DNS zone and record using the Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="d4cf7-109">역방향 조회 DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="d4cf7-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="d4cf7-110">[Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d4cf7-110">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="d4cf7-111">허브 메뉴에서 **새로 만들기** > **네트워킹**을 클릭한 다음 **DNS 영역**을 클릭하여 **DNS 영역 만들기** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-111">On the Hub menu, click and click **New** > **Networking** > and then click **DNS zone** to open the **Create DNS zone** blade.</span></span>

   ![DNS 영역](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="d4cf7-113">**DNS 영역 만들기** 블레이드에서 DNS 영역의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-113">On the **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="d4cf7-114">영역 이름은 IPv4 및 IPv6 접두사에 대해 다르게 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="d4cf7-115">영역 이름을 지정하려면 [IPV4](#ipv4) 또는 [IPv6](#ipv6)에 대한 지침을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-115">Use either the instructions for [IPV4](#ipv4) or [IPv6](#ipv6) to name your zone.</span></span> <span data-ttu-id="d4cf7-116">완료되면 **만들기**를 클릭하여 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-116">When complete click **Create** to create the zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="d4cf7-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="d4cf7-117">IPv4</span></span>

<span data-ttu-id="d4cf7-118">IPv4 역방향 조회 영역의 이름은 나타내는 IP 범위를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-118">The name of an IPv4 reverse lookup zone is based on the IP range it represents.</span></span> <span data-ttu-id="d4cf7-119">`<IPv4 network prefix in reverse order>.in-addr.arpa` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="d4cf7-120">예제를 보려면 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md#ipv4)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="d4cf7-121">Azure DNS에서 클래스 없는 역방향 DNS 조회 영역을 만들 경우 영역 이름에 슬래시('/') 대신 하이픈(`-`)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in the zone name.</span></span>
>
> <span data-ttu-id="d4cf7-122">예를 들어 IP 범위 192.0.2.128/26에 대해 `128/26.2.0.192.in-addr.arpa` 대신 `128-26.2.0.192.in-addr.arpa`를 영역 이름으로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="d4cf7-123">둘 다 DNS 표준에서 지원되지만 슬래시(`/`) 문자를 포함하는 DNS 영역 이름은 Azure DNS에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-123">This is because, while both are supported by the DNS standards, DNS zone names containing the forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="d4cf7-124">다음 예제에서는 Azure Portal을 통해 Azure DNS에 `2.0.192.in-addr.arpa`라는 '클래스 C' 역방향 DNS 영역을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-124">The following example shows how to create a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span></span>

 ![DNS 영역 만들기](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="d4cf7-126">‘리소스 그룹 위치’는 리소스 그룹의 위치를 정의하며 DNS 영역에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-126">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="d4cf7-127">DNS 영역 위치는 항상 ‘전역’이며 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-127">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="d4cf7-128">다음 예제에서는 Azure PowerShell 및 Azure CLI를 사용하여 이 작업을 완료하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-128">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d4cf7-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4cf7-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d4cf7-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d4cf7-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="d4cf7-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="d4cf7-132">IPv6</span></span>

<span data-ttu-id="d4cf7-133">IPv6 역방향 조회 영역의 이름은 `<IPv6 network prefix in reverse order>.ip6.arpa` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-133">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="d4cf7-134">예제를 보려면 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md#ipv6)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="d4cf7-135">다음 예제에서는 Azure Portal을 통해 Azure DNS에 `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa`라는 IPv6 역방향 DNS 조회 영역을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-135">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span></span>

 ![DNS 영역 만들기](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="d4cf7-137">‘리소스 그룹 위치’는 리소스 그룹의 위치를 정의하며 DNS 영역에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-137">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="d4cf7-138">DNS 영역 위치는 항상 ‘전역’이며 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-138">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="d4cf7-139">다음 예제에서는 Azure PowerShell 및 Azure CLI를 사용하여 이 작업을 완료하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-139">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d4cf7-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4cf7-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="d4cf7-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="d4cf7-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="d4cf7-143">역방향 DNS 조회 영역 위임</span><span class="sxs-lookup"><span data-stu-id="d4cf7-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="d4cf7-144">DNS 역방향 조회 영역을 만들었으므로 해당 영역이 부모 영역에서 위임되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-144">Having created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span></span> <span data-ttu-id="d4cf7-145">DNS 위임을 사용하면 DNS 이름 확인 프로세스를 통해 역방향 DNS 조회 영역을 호스트하는 이름 서버를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-145">DNS delegation enables the DNS name resolution process to find the name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="d4cf7-146">이를 통해 이러한 이름 서버는 주소 범위에 있는 IP 주소에 대한 DNS 역방향 쿼리에 응답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-146">This enables those name servers to answer DNS reverse queries for the IP addresses in your address range.</span></span>

<span data-ttu-id="d4cf7-147">정방향 조회 영역의 경우 DNS 영역을 위임하는 프로세스는 [Azure DNS에 도메인 위임](dns-delegate-domain-azure-dns.md)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-147">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="d4cf7-148">역방향 조회 영역에 대한 위임도 동일한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-148">Delegation for reverse lookup zones works the same way.</span></span> <span data-ttu-id="d4cf7-149">유일한 차이점은 도메인 이름 등록자가 아닌 IP 범위를 제공한 ISP로 이름 서버를 구성해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-149">The only difference is that you need to configure the name servers with the ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="d4cf7-150">DNS PTR 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="d4cf7-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="d4cf7-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="d4cf7-151">IPv4</span></span>

<span data-ttu-id="d4cf7-152">다음 예제에서는 Azure Portal의 역방향 DNS 영역에 PTR 레코드를 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-152">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="d4cf7-153">다른 레코드 유형을 알아보고 기존 레코드를 수정하려면 [Azure Portal을 사용하여 DNS 레코드 및 레코드 집합 관리](dns-operations-recordsets-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-153">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="d4cf7-154">**DNS 영역** 블레이드의 위쪽에서 **+레코드 집합**을 클릭하여 **레코드 집합 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-154">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

 ![DNS 영역](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="d4cf7-156">**레코드 집합 추가** 블레이드에서</span><span class="sxs-lookup"><span data-stu-id="d4cf7-156">On the **Add record set** blade.</span></span> 
1. <span data-ttu-id="d4cf7-157">레코드 "**형식**" 메뉴에서 **PTR**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-157">Select **PTR** from the record "**Type**" menu.</span></span>  
1. <span data-ttu-id="d4cf7-158">PTR 레코드에 대한 레코드 집합 이름은 반대 순서로 IPv4 주소의 나머지 부분이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span></span> <span data-ttu-id="d4cf7-159">이 예제에서 처음 3개 8진수는 이미 영역 이름(.2.0.192)의 일부로 채워져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span></span> <span data-ttu-id="d4cf7-160">따라서 마지막 8진수만 이름 필드에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-160">Therefore, only the last octet is supplied in the name field.</span></span> <span data-ttu-id="d4cf7-161">예를 들어 해당 IP 주소가 192.0.2.15인 리소스에 대해 레코드 집합 이름을 "**15**"로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="d4cf7-162">"**도메인 이름**" 필드에 IP를 사용하여 리소스의 FQDN(정규화된 도메인 이름)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-162">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
1. <span data-ttu-id="d4cf7-163">블레이드의 맨 아래에서 **확인**을 선택하여 DNS 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-163">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

 ![레코드 집합 추가](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="d4cf7-165">다음 예제에서는 PowerShell 및 Azure CLI를 사용하여 이 작업을 완료하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-165">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d4cf7-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4cf7-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="d4cf7-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="d4cf7-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="d4cf7-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="d4cf7-169">IPv6</span></span>

<span data-ttu-id="d4cf7-170">다음 예제에서는 새로운 'PTR' 레코드를 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-170">The following example walks you through the process of creating new 'PTR' record.</span></span> <span data-ttu-id="d4cf7-171">다른 레코드 유형을 알아보고 기존 레코드를 수정하려면 [Azure Portal을 사용하여 DNS 레코드 및 레코드 집합 관리](dns-operations-recordsets-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-171">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="d4cf7-172">**DNS 영역** 블레이드의 위쪽에서 **+레코드 집합**을 클릭하여 **레코드 집합 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-172">At the top of the **DNS zone blade**, select **+ Record set** to open the **Add record set** blade.</span></span>

  ![dns 영역 블레이드](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="d4cf7-174">**레코드 집합 추가** 블레이드에서</span><span class="sxs-lookup"><span data-stu-id="d4cf7-174">On the **Add record set** blade.</span></span> 
3. <span data-ttu-id="d4cf7-175">레코드 "**형식**" 메뉴에서 **PTR**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-175">Select **PTR** from the record "**Type**" menu.</span></span>  
4. <span data-ttu-id="d4cf7-176">PTR 레코드에 대한 레코드 집합 이름은 반대 순서로 IPv6 주소의 나머지 부분이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-176">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span></span> <span data-ttu-id="d4cf7-177">제로 압축은 포함하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-177">It must not include any zero compression.</span></span> <span data-ttu-id="d4cf7-178">이 예제에서 IPv6의 처음 64비트는 영역 이름의 일부로 이미 채워져 있습니다(0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="d4cf7-178">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="d4cf7-179">따라서 마지막 64비트만 이름 필드에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-179">Therefore, only the last 64 bits are supplied in the name field.</span></span> <span data-ttu-id="d4cf7-180">IP 주소의 마지막 64비트는 각 16진수 간에 구분 기호로 마침표를 사용하여 역순으로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-180">The last 64 bits of the IP address are entered in reverse order, using a period as the delimiter between each hexadecimal number.</span></span> <span data-ttu-id="d4cf7-181">예를 들어 해당 IP 주소가 2001:0db8:abdc:0000:f524:10bc:1af9:405e인 리소스에 대해 레코드 집합 이름을 "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**"로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="d4cf7-182">"**도메인 이름**" 필드에 IP를 사용하여 리소스의 FQDN(정규화된 도메인 이름)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-182">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
6. <span data-ttu-id="d4cf7-183">블레이드의 맨 아래에서 **확인**을 선택하여 DNS 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-183">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

![레코드 집합 추가 블레이드](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="d4cf7-185">다음 예제에서는 PowerShell 및 Azure CLI를 사용하여 이 작업을 완료하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-185">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d4cf7-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4cf7-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="d4cf7-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="d4cf7-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="d4cf7-189">레코드 보기</span><span class="sxs-lookup"><span data-stu-id="d4cf7-189">View Records</span></span>

<span data-ttu-id="d4cf7-190">만든 레코드를 보려면 Azure Portal에서 DNS 영역으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-190">To view the records you created, navigate to your DNS zone in the Azure portal.</span></span> <span data-ttu-id="d4cf7-191">**DNS 영역** 블레이드의 아래쪽에서 DNS 영역에 대한 레코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-191">In the lower part of the **DNS zone** blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="d4cf7-192">모든 영역에 생성된 기본 NS 및 SOA 레코드와 사용자가 생성한 모든 새 레코드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-192">You should see the default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="d4cf7-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="d4cf7-193">IPv4</span></span>

<span data-ttu-id="d4cf7-194">IPv4 PTR 레코드를 보여 주는 DNS 영역 블레이드:</span><span class="sxs-lookup"><span data-stu-id="d4cf7-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![dns 영역 블레이드](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="d4cf7-196">다음 예제에서는 PowerShell 또는 Azure CLI를 사용하여 PTR 레코드를 보는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-196">The following examples show how to view the PTR records using PowerShell or the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d4cf7-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4cf7-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d4cf7-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d4cf7-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="d4cf7-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="d4cf7-200">IPv6</span></span>

<span data-ttu-id="d4cf7-201">IPv6 PTR 레코드를 보여 주는 DNS 영역 블레이드:</span><span class="sxs-lookup"><span data-stu-id="d4cf7-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![dns 영역 블레이드](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="d4cf7-203">다음 예제에서는 PowerShell 또는 Azure CLI를 사용하여 레코드를 보는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-203">The following are examples on how to view the records with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d4cf7-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4cf7-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="d4cf7-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="d4cf7-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d4cf7-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="d4cf7-207">FAQ</span><span class="sxs-lookup"><span data-stu-id="d4cf7-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="d4cf7-208">Azure DNS에서 내 ISP 할당 IP 블록에 대한 역방향 DNS 조회 영역을 호스트할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d4cf7-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="d4cf7-209">예.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-209">Yes.</span></span> <span data-ttu-id="d4cf7-210">Azure DNS에서 고유한 IP 범위에 대해 역방향 조회(ARPA) 영역을 호스팅하는 것은 완전히 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-210">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="d4cf7-211">이 문서에 설명된 대로 Azure DNS에서 역방향 조회 영역을 만든 다음 ISP와 함께 [영역을 위임](dns-domain-delegation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-211">Create the reverse lookup zone in Azure DNS as explained in this article, then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="d4cf7-212">그런 다음 다른 레코드 유형과 동일한 방식으로 각 역방향 조회를 위해 PTR 레코드를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-212">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="d4cf7-213">내 역방향 DNS 조회 영역 호스트 비용은 얼마나 되나요?</span><span class="sxs-lookup"><span data-stu-id="d4cf7-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="d4cf7-214">Azure DNS에서 ISP 할당 IP 블록에 대해 역방향 DNS 조회 영역을 호스트하는 비용은 [표준 Azure DNS 요율](https://azure.microsoft.com/pricing/details/dns/)로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-214">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="d4cf7-215">Azure DNS에서 IPv4 및 IPv6 주소 모두에 대해 역방향 DNS 조회 영역을 호스트할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d4cf7-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="d4cf7-216">예.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-216">Yes.</span></span> <span data-ttu-id="d4cf7-217">이 문서에서는 Azure DNS에서 IPv4 및 IPv6 역방향 DNS 조회 영역을 둘 다 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-217">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="d4cf7-218">기존의 역방향 DNS 조회 영역을 가져올 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d4cf7-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="d4cf7-219">예.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-219">Yes.</span></span> <span data-ttu-id="d4cf7-220">Azure CLI를 사용하여 Azure DNS로 기존 DNS 영역을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-220">You can use the Azure CLI to import existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="d4cf7-221">이 방법은 정방향 조회 영역 및 역방향 조회 영역을 둘 다에 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="d4cf7-222">자세한 내용은 [Azure CLI를 사용하여 DNS 영역 파일 가져오기 및 내보내기](dns-import-export.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-222">For more information, see [Import and export a DNS zone file using the Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4cf7-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4cf7-223">Next steps</span></span>

<span data-ttu-id="d4cf7-224">역방향 DNS에 대한 자세한 내용은 [Wikipedia에서 역방향 DNS 조회](http://en.wikipedia.org/wiki/Reverse_DNS_lookup)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="d4cf7-225">[Azure 서비스에 대한 역방향 DNS 레코드를 관리](dns-reverse-dns-for-azure-services.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d4cf7-225">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
