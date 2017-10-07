---
title: "aaaHosting 역방향 DNS 조회 영역에 Azure DNS | Microsoft Docs"
description: "Toouse Azure DNS toohost hello IP 범위에 대 한 DNS 조회 영역을 반전 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="81598-103">Azure DNS에서 역방향 DNS 조회 영역 호스트</span><span class="sxs-lookup"><span data-stu-id="81598-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="81598-104">이 문서에서는 toohost hello Azure DNS에서 할당 된 IP 범위에 대 한 DNS 조회 영역을 반전 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-104">This article explains how toohost hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="81598-105">hello 역방향 조회 영역을 나타내는 hello IP 범위 할당 해야 tooyour 조직 일반적으로 ISP가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-105">hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="81598-106">tooconfigure Azure 소유 IP 주소가 할당 tooyour Azure 서비스에 대 한 DNS 역방향 참조 하십시오. [hello IP 주소가 할당 tooyour Azure 서비스에 대 한 역방향 조회 hello 구성](dns-reverse-dns-for-azure-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-106">tooconfigure reverse DNS for Azure-owned IP address assigned tooyour Azure service, see [configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="81598-107">이 문서를 읽기 전에 이 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md)에 익숙해지는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="81598-108">이 문서 안내 hello 단계 toocreate 첫 번째 역방향 조회 DNS 영역 및 Azure PowerShell, CLI 1.0 Azure 또는 Azure CLI 2.0 hello Azure 포털을 사용 하 여 레코드.</span><span class="sxs-lookup"><span data-stu-id="81598-108">This article walks you through hello steps toocreate your first reverse lookup DNS zone and record using hello Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="81598-109">역방향 조회 DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="81598-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="81598-110">Toohello 로그인 [Azure 포털](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="81598-110">Sign in toohello [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="81598-111">Hello 허브 메뉴에서를 클릭 하 고 클릭 **새로** > **네트워킹** >을 클릭 한 다음 **DNS 영역** tooopen hello **만들 DNS 영역**블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81598-111">On hello Hub menu, click and click **New** > **Networking** > and then click **DNS zone** tooopen hello **Create DNS zone** blade.</span></span>

   ![DNS 영역](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="81598-113">Hello에 **만들 DNS 영역** 블레이드에서 DNS 영역 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-113">On hello **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="81598-114">IPv4 및 IPv6 접두사에 대 한 hello 영역의 hello 이름은 다르게 트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81598-114">hello name of hello zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="81598-115">에 대 한 hello 지침 중 하나를 사용 하 여 [IPV4](#ipv4) 또는 [IPv6](#ipv6) tooname 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="81598-115">Use either hello instructions for [IPV4](#ipv4) or [IPv6](#ipv6) tooname your zone.</span></span> <span data-ttu-id="81598-116">클릭 하 여 완료 된 경우 **만들기** toocreate hello 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="81598-116">When complete click **Create** toocreate hello zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="81598-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="81598-117">IPv4</span></span>

<span data-ttu-id="81598-118">IPv4 역방향 조회 영역의 hello 이름은 나타내는 hello IP 범위를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-118">hello name of an IPv4 reverse lookup zone is based on hello IP range it represents.</span></span> <span data-ttu-id="81598-119">형식에 따라 hello 여야 합니다: `<IPv4 network prefix in reverse order>.in-addr.arpa`합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-119">It should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="81598-120">예제를 보려면 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md#ipv4)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81598-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="81598-121">Azure dns에서 classless 역방향 DNS 조회 영역을 만들 때에 하이픈을 사용 해야 합니다 (`-`) 대신 슬래시 ('/')을 hello 영역 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="81598-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in hello zone name.</span></span>
>
> <span data-ttu-id="81598-122">예를 들어 hello IP 범위 192.0.2.128/26 사용 해야 `128-26.2.0.192.in-addr.arpa` 대신 hello 영역 이름으로 `128/26.2.0.192.in-addr.arpa`합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-122">For example, for hello IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as hello zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="81598-123">DNS 영역 hello 슬래시를 포함 하는 이름은 둘 다가 hello DNS 표준에 의해 지원, 때문에 이것이 (`/`) Azure DNS에서 문자를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-123">This is because, while both are supported by hello DNS standards, DNS zone names containing hello forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="81598-124">hello 다음 예제에서는 어떻게 toocreate ' 클래스 C' 역방향 DNS 영역 명명 된 `2.0.192.in-addr.arpa` hello Azure 포털을 통해 Azure DNS에서:</span><span class="sxs-lookup"><span data-stu-id="81598-124">hello following example shows how toocreate a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![DNS 영역 만들기](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="81598-126">hello '리소스 그룹 위치' hello 리소스 그룹에 대 한 hello 위치를 정의 되었으며 hello DNS 영역에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-126">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="81598-127">hello DNS 영역 위치는 항상 'global' 및 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-127">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="81598-128">hello 다음 예제에서는 보여 어떻게 toocomplete이 작업을 Azure PowerShell 및 Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="81598-128">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="81598-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81598-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="81598-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="81598-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="81598-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="81598-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="81598-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="81598-132">IPv6</span></span>

<span data-ttu-id="81598-133">IPv6 역방향 조회 영역의 hello 이름 hello 양식 뒤에 있어야: `<IPv6 network prefix in reverse order>.ip6.arpa`합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-133">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="81598-134">예제를 보려면 [Azure의 역방향 DNS 및 지원 개요](dns-reverse-dns-overview.md#ipv6)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81598-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="81598-135">hello 다음 예제에서는 방법과 toocreate IPv6 역방향 DNS 조회 영역 이름 `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` hello Azure 포털을 통해 Azure DNS에서:</span><span class="sxs-lookup"><span data-stu-id="81598-135">hello following example shows how toocreate an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![DNS 영역 만들기](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="81598-137">hello '리소스 그룹 위치' hello 리소스 그룹에 대 한 hello 위치를 정의 되었으며 hello DNS 영역에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-137">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="81598-138">hello DNS 영역 위치는 항상 'global' 및 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-138">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="81598-139">hello 다음 예제에서는 보여 어떻게 toocomplete이 작업을 Azure PowerShell 및 Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="81598-139">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="81598-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81598-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="81598-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="81598-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="81598-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="81598-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="81598-143">역방향 DNS 조회 영역 위임</span><span class="sxs-lookup"><span data-stu-id="81598-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="81598-144">역방향 DNS 조회 영역이 만들었으면 확인 해야 hello 부모 영역에서 해당 hello 영역 위임 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81598-144">Having created your reverse DNS lookup zone, you must ensure that hello zone is delegated from hello parent zone.</span></span> <span data-ttu-id="81598-145">DNS 위임 hello DNS 이름 확인 프로세스 toofind hello 이름 서버를 호스팅 역방향 DNS 조회 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-145">DNS delegation enables hello DNS name resolution process toofind hello name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="81598-146">이렇게 하면 해당 이름 서버 tooanswer DNS 역방향 쿼리 hello IP 주소의 주소 범위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-146">This enables those name servers tooanswer DNS reverse queries for hello IP addresses in your address range.</span></span>

<span data-ttu-id="81598-147">정방향 조회 영역에 대 한 DNS 영역 위임 hello 프로세스에 설명 되어 [사용자 도메인 tooAzure DNS 위임](dns-delegate-domain-azure-dns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-147">For forward lookup zones, hello process of delegating a DNS zone is described in [Delegate your domain tooAzure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="81598-148">역방향 조회 영역에 대 한 위임을 hello 작동 하는 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-148">Delegation for reverse lookup zones works hello same way.</span></span> <span data-ttu-id="81598-149">hello 유일한 차이점은 tooconfigure hello 이름 서버 도메인 이름 등록자 보다는 IP 범위를 공급자에 게 ISP hello로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-149">hello only difference is that you need tooconfigure hello name servers with hello ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="81598-150">DNS PTR 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="81598-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="81598-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="81598-151">IPv4</span></span>

<span data-ttu-id="81598-152">hello 다음 예제에서는 단계별로 hello Azure dns에서 역방향 DNS 영역에는 PTR 레코드를 만드는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="81598-152">hello following example walks you through hello process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="81598-153">다른 레코드 종류 및 toomodify 기존 레코드에 대 한 참조 [관리 DNS 레코드 및 레코드 집합 사용 하 여 Azure 포털 hello](dns-operations-recordsets-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-153">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="81598-154">Hello의 hello 위쪽 **DNS 영역** 블레이드를 **집합을 기록해 +** tooopen hello **레코드 집합을 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81598-154">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

 ![DNS 영역](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="81598-156">Hello에 **레코드 집합을 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81598-156">On hello **Add record set** blade.</span></span> 
1. <span data-ttu-id="81598-157">선택 **PTR** hello 레코드에서 "**형식**" 메뉴.</span><span class="sxs-lookup"><span data-stu-id="81598-157">Select **PTR** from hello record "**Type**" menu.</span></span>  
1. <span data-ttu-id="81598-158">hello PTR 레코드에 대 한 hello 레코드 집합의 이름이 필요 toobe hello 나머지 hello IPv4 주소 반대 순서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-158">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv4 address in reverse order.</span></span> <span data-ttu-id="81598-159">이 예제에서는 hello 처음 세 옥텟 이미 채워져 hello 영역 이름 (.2.0.192)의 일부로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-159">In this example, hello first three octets are already populated as part of hello zone name (.2.0.192).</span></span> <span data-ttu-id="81598-160">따라서만 hello 마지막 8 진수 hello 이름 필드에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81598-160">Therefore, only hello last octet is supplied in hello name field.</span></span> <span data-ttu-id="81598-161">예를 들어 해당 IP 주소가 192.0.2.15인 리소스에 대해 레코드 집합 이름을 "**15**"로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="81598-162">Hello에 "**도메인 이름**" 필드에, hello hello IP를 사용 하 여 hello 리소스의 정규화 된 도메인 이름 (FQDN)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-162">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
1. <span data-ttu-id="81598-163">선택 **확인** hello hello 블레이드 toocreate hello DNS 레코드 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-163">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

 ![레코드 집합 추가](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="81598-165">hello 다음은 방법 보여 주는 예 toocomplete PowerShell 및 hello AzureCLI로이 작업:</span><span class="sxs-lookup"><span data-stu-id="81598-165">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="81598-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81598-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="81598-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="81598-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="81598-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="81598-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="81598-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="81598-169">IPv6</span></span>

<span data-ttu-id="81598-170">다음 예제는 hello hello 새 'PTR' 레코드를 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-170">hello following example walks you through hello process of creating new 'PTR' record.</span></span> <span data-ttu-id="81598-171">다른 레코드 종류 및 toomodify 기존 레코드에 대 한 참조 [관리 DNS 레코드 및 레코드 집합 사용 하 여 Azure 포털 hello](dns-operations-recordsets-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-171">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="81598-172">Hello의 hello 위쪽 **DNS 영역 블레이드**선택, **집합을 기록해 +** tooopen hello **레코드 집합을 추가** 블레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-172">At hello top of hello **DNS zone blade**, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

  ![dns 영역 블레이드](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="81598-174">Hello에 **레코드 집합을 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="81598-174">On hello **Add record set** blade.</span></span> 
3. <span data-ttu-id="81598-175">선택 **PTR** hello 레코드에서 "**형식**" 메뉴.</span><span class="sxs-lookup"><span data-stu-id="81598-175">Select **PTR** from hello record "**Type**" menu.</span></span>  
4. <span data-ttu-id="81598-176">hello PTR 레코드에 대 한 hello 레코드 집합의 이름이 필요 toobe hello 나머지 hello IPv6 주소 반대 순서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-176">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv6 address in reverse order.</span></span> <span data-ttu-id="81598-177">제로 압축은 포함하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81598-177">It must not include any zero compression.</span></span> <span data-ttu-id="81598-178">이 예제에서는 hello IPv6 hello 영역 이름 (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa)의 일부로 이미 채워져 hello의 첫 번째 64 비트입니다.</span><span class="sxs-lookup"><span data-stu-id="81598-178">In this example, hello first 64 bits of hello IPv6 are already populated as part of hello zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="81598-179">따라서 hello 마지막 64 비트 hello 이름 필드에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81598-179">Therefore, only hello last 64 bits are supplied in hello name field.</span></span> <span data-ttu-id="81598-180">각 16 진수 사이의 hello 구분 기호로 마침표를 사용 하 여 hello 마지막 64 비트 hello IP 주소의 반대 순서로 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81598-180">hello last 64 bits of hello IP address are entered in reverse order, using a period as hello delimiter between each hexadecimal number.</span></span> <span data-ttu-id="81598-181">예를 들어 해당 IP 주소가 2001:0db8:abdc:0000:f524:10bc:1af9:405e인 리소스에 대해 레코드 집합 이름을 "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**"로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="81598-182">Hello에 "**도메인 이름**" 필드에, hello hello IP를 사용 하 여 hello 리소스의 정규화 된 도메인 이름 (FQDN)을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-182">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
6. <span data-ttu-id="81598-183">선택 **확인** hello hello 블레이드 toocreate hello DNS 레코드 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-183">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

![레코드 집합 추가 블레이드](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="81598-185">hello 다음은 방법 보여 주는 예 toocomplete PowerShell 및 hello AzureCLI로이 작업:</span><span class="sxs-lookup"><span data-stu-id="81598-185">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="81598-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81598-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="81598-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="81598-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="81598-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="81598-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="81598-189">레코드 보기</span><span class="sxs-lookup"><span data-stu-id="81598-189">View Records</span></span>

<span data-ttu-id="81598-190">tooview hello 레코드를 만든 hello Azure 포털의에서 tooyour DNS 영역을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-190">tooview hello records you created, navigate tooyour DNS zone in hello Azure portal.</span></span> <span data-ttu-id="81598-191">Hello hello의 일부를 줄이려면 **DNS 영역** 블레이드에서 hello DNS 영역에 대 한 hello 레코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-191">In hello lower part of hello **DNS zone** blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="81598-192">Hello 기본 NS 및 SOA 레코드를 모든 영역에 만들어지는 플러스 만든 새 레코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-192">You should see hello default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="81598-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="81598-193">IPv4</span></span>

<span data-ttu-id="81598-194">IPv4 PTR 레코드를 보여 주는 DNS 영역 블레이드:</span><span class="sxs-lookup"><span data-stu-id="81598-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![dns 영역 블레이드](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="81598-196">hello 다음 예에서는 PowerShell을 사용 하 여 tooview hello PTR을 기록 하는 방법을 보여 줍니다. 또는 Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="81598-196">hello following examples show how tooview hello PTR records using PowerShell or hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="81598-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81598-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="81598-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="81598-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="81598-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="81598-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="81598-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="81598-200">IPv6</span></span>

<span data-ttu-id="81598-201">IPv6 PTR 레코드를 보여 주는 DNS 영역 블레이드:</span><span class="sxs-lookup"><span data-stu-id="81598-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![dns 영역 블레이드](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="81598-203">hello 다음은 PowerShell 및 hello AzureCLI tooview hello 기록 하는 방법을 보여 주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="81598-203">hello following are examples on how tooview hello records with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="81598-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81598-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="81598-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="81598-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="81598-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="81598-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="81598-207">FAQ</span><span class="sxs-lookup"><span data-stu-id="81598-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="81598-208">Azure DNS에서 내 ISP 할당 IP 블록에 대한 역방향 DNS 조회 영역을 호스트할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="81598-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="81598-209">예.</span><span class="sxs-lookup"><span data-stu-id="81598-209">Yes.</span></span> <span data-ttu-id="81598-210">Azure DNS에 해당 하는 IP 범위에 대 한 hello (ARPA) 역방향 조회 영역 호스팅 완전히 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81598-210">Hosting hello reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="81598-211">이 문서에서 설명한 것 처럼 Azure DNS에 hello 역방향 조회 영역을 만든 다음 너무 ISP 작업할[대리자 hello 영역](dns-domain-delegation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-211">Create hello reverse lookup zone in Azure DNS as explained in this article, then work with your ISP too[delegate hello zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="81598-212">Hello PTR 레코드를 관리할 수 있습니다 각 역방향 조회 hello에 대 한 다른 방식으로 동일한 레코드 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="81598-212">You can then manage hello PTR records for each reverse lookup in hello same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="81598-213">내 역방향 DNS 조회 영역 호스트 비용은 얼마나 되나요?</span><span class="sxs-lookup"><span data-stu-id="81598-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="81598-214">Azure DNS에 IP ISP에 할당 된 블록에 요금이 부과 됩니다에 대 한 DNS 역방향 조회 영역 hello 호스팅 [표준 Azure DNS 속도가](https://azure.microsoft.com/pricing/details/dns/)합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-214">Hosting hello reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="81598-215">Azure DNS에서 IPv4 및 IPv6 주소 모두에 대해 역방향 DNS 조회 영역을 호스트할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="81598-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="81598-216">예.</span><span class="sxs-lookup"><span data-stu-id="81598-216">Yes.</span></span> <span data-ttu-id="81598-217">이 문서에서는 설명 어떻게 toocreate IPv4 및 IPv6 모두 역방향 DNS 조회 영역에 Azure DNS 합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-217">This article explains how toocreate both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="81598-218">기존의 역방향 DNS 조회 영역을 가져올 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="81598-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="81598-219">예.</span><span class="sxs-lookup"><span data-stu-id="81598-219">Yes.</span></span> <span data-ttu-id="81598-220">Azure DNS로 hello Azure CLI tooimport 기존 DNS 영역을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81598-220">You can use hello Azure CLI tooimport existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="81598-221">이 방법은 정방향 조회 영역 및 역방향 조회 영역을 둘 다에 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="81598-222">자세한 내용은 참조 [가져오기와 내보내기를 사용 하 여 DNS 영역 파일 hello Azure CLI](dns-import-export.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-222">For more information, see [Import and export a DNS zone file using hello Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="81598-223">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81598-223">Next steps</span></span>

<span data-ttu-id="81598-224">역방향 DNS에 대한 자세한 내용은 [Wikipedia에서 역방향 DNS 조회](http://en.wikipedia.org/wiki/Reverse_DNS_lookup)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81598-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="81598-225">너무 방법에 대해 알아봅니다[Azure 서비스에 대 한 역방향 DNS 레코드 관리](dns-reverse-dns-for-azure-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81598-225">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
