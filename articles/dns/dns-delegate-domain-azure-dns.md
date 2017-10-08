---
title: "aaaDelegate 사용자 도메인 tooAzure DNS | Microsoft Docs"
description: "이름을 어떻게 지정 toochange 도메인 위임 및 Azure DNS를 사용 하 여 서버 tooprovide 도메인 호스팅 이해 합니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a><span data-ttu-id="68cac-103">도메인 tooAzure DNS 위임</span><span class="sxs-lookup"><span data-stu-id="68cac-103">Delegate a domain tooAzure DNS</span></span>

<span data-ttu-id="68cac-104">Azure DNS toohost DNS 영역을 허용 하 고 Azure에서 도메인에 대 한 hello DNS 레코드를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-104">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="68cac-105">도메인 tooreach Azure DNS에 대 한 DNS 쿼리에 대 한 순서로 hello 도메인에 toobe tooAzure DNS hello 부모 도메인에서 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-105">In order for DNS queries for a domain tooreach Azure DNS, hello domain has toobe delegated tooAzure DNS from hello parent domain.</span></span> <span data-ttu-id="68cac-106">Azure DNS에 유의 hello 도메인 등록 기관 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-106">Keep in mind Azure DNS is not hello domain registrar.</span></span> <span data-ttu-id="68cac-107">이 문서에서는 설명 방법을 toodelegate 사용자 도메인 tooAzure DNS 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-107">This article explains how toodelegate your domain tooAzure DNS.</span></span>

<span data-ttu-id="68cac-108">도메인 등록 기관에서 구매에 대 한 등록 자가 hello 옵션 tooset이 NS 레코드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-108">For domains purchased from a registrar, your registrar offers hello option tooset up these NS records.</span></span> <span data-ttu-id="68cac-109">않아도 tooown 도메인 toocreate 해당 도메인 이름 사용 하 여 DNS 영역을 Azure DNS에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-109">You do not have tooown a domain toocreate a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="68cac-110">그러나 hello 등록 기관과 함께 hello 위임 tooAzure DNS tooown hello 도메인 tooset이 필요지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-110">However, you do need tooown hello domain tooset up hello delegation tooAzure DNS with hello registrar.</span></span>

<span data-ttu-id="68cac-111">예를 들어 'contoso.net' hello 도메인을 구입 하 고 Azure DNS contoso.net' hello 이름'를 사용 하 여 영역을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-111">For example, suppose you purchase hello domain 'contoso.net' and create a zone with hello name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="68cac-112">Hello 도메인의 hello 소유자로 등록 자가 옵션 tooconfigure hello 이름 서버 주소 (즉, hello NS 레코드) 도메인에 대 한 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-112">As hello owner of hello domain, your registrar offers you hello option tooconfigure hello name server addresses (that is, hello NS records) for your domain.</span></span> <span data-ttu-id="68cac-113">hello 등록 자가이 경우 '.net' hello 부모 도메인의 이러한 NS 레코드를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-113">hello registrar stores these NS records in hello parent domain, in this case '.net'.</span></span> <span data-ttu-id="68cac-114">그런 다음 클라이언트 hello 전 세계는 'contoso.net'에서 DNS 레코드 tooresolve 하려고 할 때 Azure DNS 영역에서 tooyour 방향이 지정 된 도메인을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-114">Clients around hello world can then be directed tooyour domain in Azure DNS zone when trying tooresolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="68cac-115">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="68cac-115">Create a DNS zone</span></span>

1. <span data-ttu-id="68cac-116">Azure 포털 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="68cac-116">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="68cac-117">Hello 허브 메뉴에서를 클릭 하 고 클릭 **새로 만들기 > 네트워킹 >** 클릭 하 고 **DNS 영역** tooopen hello 만들 DNS 영역 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-117">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS 영역](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="68cac-119">Hello에 **만들 DNS 영역** 블레이드 hello 다음 값을 입력 한 다음 클릭 **만들기**:</span><span class="sxs-lookup"><span data-stu-id="68cac-119">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="68cac-120">**설정**</span><span class="sxs-lookup"><span data-stu-id="68cac-120">**Setting**</span></span> | <span data-ttu-id="68cac-121">**값**</span><span class="sxs-lookup"><span data-stu-id="68cac-121">**Value**</span></span> | <span data-ttu-id="68cac-122">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="68cac-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="68cac-123">**Name**</span><span class="sxs-lookup"><span data-stu-id="68cac-123">**Name**</span></span>|<span data-ttu-id="68cac-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="68cac-124">contoso.net</span></span>|<span data-ttu-id="68cac-125">hello hello DNS 영역 이름</span><span class="sxs-lookup"><span data-stu-id="68cac-125">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="68cac-126">**구독**</span><span class="sxs-lookup"><span data-stu-id="68cac-126">**Subscription**</span></span>|<span data-ttu-id="68cac-127">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="68cac-127">[Your subscription]</span></span>|<span data-ttu-id="68cac-128">구독 toocreate hello 응용 프로그램 게이트웨이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-128">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="68cac-129">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="68cac-129">**Resource group**</span></span>|<span data-ttu-id="68cac-130">**새로 만들기:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="68cac-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="68cac-131">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-131">Create a resource group.</span></span> <span data-ttu-id="68cac-132">hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-132">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="68cac-133">리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서.</span><span class="sxs-lookup"><span data-stu-id="68cac-133">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="68cac-134">**위치**:</span><span class="sxs-lookup"><span data-stu-id="68cac-134">**Location**</span></span>|<span data-ttu-id="68cac-135">미국 서부</span><span class="sxs-lookup"><span data-stu-id="68cac-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="68cac-136">hello 리소스 그룹 hello 리소스 그룹의 toohello 위치 참조 되었으며 hello DNS 영역에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-136">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="68cac-137">hello DNS 영역의 위치는 항상 "전역" 하 고 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-137">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="68cac-138">이름 서버 검색</span><span class="sxs-lookup"><span data-stu-id="68cac-138">Retrieve name servers</span></span>

<span data-ttu-id="68cac-139">DNS 영역 tooAzure DNS를 위임할 수 있습니다, 전에 먼저 해당 영역의 tooknow hello 이름 서버 이름을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-139">Before you can delegate your DNS zone tooAzure DNS, you first need tooknow hello name server names for your zone.</span></span> <span data-ttu-id="68cac-140">Azure DNS는 영역이 만들어질 때마다 풀에서 이름 서버를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="68cac-141">Hello Azure 포털에서에서 만든 hello DNS 영역과 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-141">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="68cac-142">Hello 클릭 **contoso.net** hello의 DNS 영역 **모든 리소스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-142">Click hello **contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="68cac-143">이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **contoso.net** 이름별 필터 hello에...</span><span class="sxs-lookup"><span data-stu-id="68cac-143">If hello subscription you selected already has several resources in it, you can enter **contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="68cac-144">상자 tooeasily 액세스 hello 응용 프로그램 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-144">box tooeasily access hello application gateway.</span></span> 

1. <span data-ttu-id="68cac-145">Hello DNS 영역 블레이드에서 hello 이름 서버를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-145">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="68cac-146">이 예제에서는 hello 영역 'contoso.net' 할당 된 이름 서버에 ' n s 1-01.azure-dns.com', 'ns2 01.azure dns.net', ' ns3-01.azure-dns.org', 및 ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="68cac-146">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="68cac-148">Azure DNS hello 지정 된 이름 서버를 포함 하 여 영역에 권한 있는 NS 레코드를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-148">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="68cac-149">Azure PowerShell 또는 Azure CLI를 통해 toosee hello 이름 서버 이름을 지정 하기만 하면 tooretrieve 이러한 레코드, 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-149">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

<span data-ttu-id="68cac-150">hello 다음 예에서는 단계도 설명 hello tooretrieve hello 이름 서버에서 PowerShell 및 Azure CLI Azure DNS 영역에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-150">hello following examples also provide hello steps tooretrieve hello name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="68cac-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68cac-151">PowerShell</span></span>

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="68cac-152">다음 예제는 hello hello 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-152">hello following example is hello response.</span></span>

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a><span data-ttu-id="68cac-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="68cac-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="68cac-154">다음 예제는 hello hello 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-154">hello following example is hello response.</span></span>

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a><span data-ttu-id="68cac-155">대리자 hello 도메인</span><span class="sxs-lookup"><span data-stu-id="68cac-155">Delegate hello domain</span></span>

<span data-ttu-id="68cac-156">Hello DNS 영역을 만들면이 고 hello 이름 서버에 hello 부모 도메인이 보았습니다 toobe를 hello Azure DNS 이름 서버를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-156">Now that hello DNS zone is created and you have hello name servers, hello parent domain needs toobe updated with hello Azure DNS name servers.</span></span> <span data-ttu-id="68cac-157">각 등록자는 자신의 DNS 관리 도구 toochange hello 이름 서버 레코드를 도메인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-157">Each registrar has their own DNS management tools toochange hello name server records for a domain.</span></span> <span data-ttu-id="68cac-158">Hello 등록자의 DNS 관리 페이지에서 hello NS 레코드를 편집 하 고 Azure DNS 만든 hello 것으로 hello NS 레코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-158">In hello registrar's DNS management page, edit hello NS records and replace hello NS records with hello ones Azure DNS created.</span></span>

<span data-ttu-id="68cac-159">도메인 tooAzure DNS를 위임할 때는 Azure DNS에서 제공 하는 hello 이름 서버 이름을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-159">When delegating a domain tooAzure DNS, you must use hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="68cac-160">Toouse 모든 것이 좋습니다 4 hello 도메인 이름에 관계 없이 서버 이름, 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-160">It is recommended toouse all four name server names, regardless of hello name of your domain.</span></span> <span data-ttu-id="68cac-161">도메인 위임 hello 이름 서버 이름 toouse 필요 하지 않습니다 hello 도메인와 같은 최상위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-161">Domain delegation does not require hello name server name toouse hello same top-level domain as your domain.</span></span>

<span data-ttu-id="68cac-162">이러한 IP 주소는 나중에 변경 될 수 있습니다 때문 '연결 레코드가' toopoint toohello Azure DNS 이름 서버 IP 주소를 사용 해야 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-162">You should not use 'glue records' toopoint toohello Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="68cac-163">고유한 영역에서 이름 서버 이름을 사용하는 위임('베니티 이름 서버'라고도 함)은 현재 Azure DNS에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="68cac-164">이름 확인이 작동하는지 확인</span><span class="sxs-lookup"><span data-stu-id="68cac-164">Verify name resolution is working</span></span>

<span data-ttu-id="68cac-165">Hello 위임을 완료 한 후 프로그램 5d; 영역 (자동으로 만들어집니다 hello 영역을 만들 때)에 대 한 'nslookup' tooquery hello SOA 레코드와 같은 도구를 사용 하 여 이름 확인이 작동 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-165">After completing hello delegation, you can verify that name resolution is working by using a tool such as 'nslookup' tooquery hello SOA record for your zone (which is also automatically created when hello zone is created).</span></span>

<span data-ttu-id="68cac-166">Toospecify hello Azure DNS 이름 서버에 없는, hello 위임 올바르게 hello 일반 DNS 확인 프로세스를 설정한 경우 hello 이름 서버를 자동으로 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-166">You do not have toospecify hello Azure DNS name servers, if hello delegation has been set up correctly, hello normal DNS resolution process finds hello name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="68cac-167">hello 다음은 hello 명령 앞의 예제 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-167">hello following is an example response from hello preceding command:</span></span>

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="68cac-168">Azure DNS에서 하위 도메인 위임</span><span class="sxs-lookup"><span data-stu-id="68cac-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="68cac-169">별도 자식 영역을 tooset 하려는 경우 Azure dns에서 하위 도메인을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-169">If you want tooset up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="68cac-170">예를 들어 있으면 설정 하 고 Azure dns에서 위임된 'contoso.net' tooset 별도 자식 영역을 선택 한다고 가정 'partners.contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="68cac-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like tooset up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="68cac-171">Azure DNS partners.contoso.net을' hello 자식 영역' 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-171">Create hello child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="68cac-172">Hello Azure DNS에 hello 자식 영역을 호스팅하는 hello 자식 영역 tooobtain hello 이름 서버에 권한 있는 NS 레코드를 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-172">Look up hello authoritative NS records in hello child zone tooobtain hello name servers hosting hello child zone in Azure DNS.</span></span>
3. <span data-ttu-id="68cac-173">Toohello 자식 영역을 가리키는 hello 부모 영역에서 NS 레코드를 구성 하 여 hello 자식 영역을 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-173">Delegate hello child zone by configuring NS records in hello parent zone pointing toohello child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="68cac-174">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="68cac-174">Create a DNS zone</span></span>

1. <span data-ttu-id="68cac-175">Azure 포털 toohello에 로그인</span><span class="sxs-lookup"><span data-stu-id="68cac-175">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="68cac-176">Hello 허브 메뉴에서를 클릭 하 고 클릭 **새로 만들기 > 네트워킹 >** 클릭 하 고 **DNS 영역** tooopen hello 만들 DNS 영역 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-176">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS 영역](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="68cac-178">Hello에 **만들 DNS 영역** 블레이드 hello 다음 값을 입력 한 다음 클릭 **만들기**:</span><span class="sxs-lookup"><span data-stu-id="68cac-178">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="68cac-179">**설정**</span><span class="sxs-lookup"><span data-stu-id="68cac-179">**Setting**</span></span> | <span data-ttu-id="68cac-180">**값**</span><span class="sxs-lookup"><span data-stu-id="68cac-180">**Value**</span></span> | <span data-ttu-id="68cac-181">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="68cac-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="68cac-182">**Name**</span><span class="sxs-lookup"><span data-stu-id="68cac-182">**Name**</span></span>|<span data-ttu-id="68cac-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="68cac-183">partners.contoso.net</span></span>|<span data-ttu-id="68cac-184">hello hello DNS 영역 이름</span><span class="sxs-lookup"><span data-stu-id="68cac-184">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="68cac-185">**구독**</span><span class="sxs-lookup"><span data-stu-id="68cac-185">**Subscription**</span></span>|<span data-ttu-id="68cac-186">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="68cac-186">[Your subscription]</span></span>|<span data-ttu-id="68cac-187">구독 toocreate hello 응용 프로그램 게이트웨이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-187">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="68cac-188">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="68cac-188">**Resource group**</span></span>|<span data-ttu-id="68cac-189">**기존 리소스 그룹 사용:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="68cac-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="68cac-190">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-190">Create a resource group.</span></span> <span data-ttu-id="68cac-191">hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-191">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="68cac-192">리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서.</span><span class="sxs-lookup"><span data-stu-id="68cac-192">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="68cac-193">**위치**:</span><span class="sxs-lookup"><span data-stu-id="68cac-193">**Location**</span></span>|<span data-ttu-id="68cac-194">미국 서부</span><span class="sxs-lookup"><span data-stu-id="68cac-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="68cac-195">hello 리소스 그룹 hello 리소스 그룹의 toohello 위치 참조 되었으며 hello DNS 영역에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-195">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="68cac-196">hello DNS 영역의 위치는 항상 "전역" 하 고 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-196">hello DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="68cac-197">이름 서버 검색</span><span class="sxs-lookup"><span data-stu-id="68cac-197">Retrieve name servers</span></span>

1. <span data-ttu-id="68cac-198">Hello Azure 포털에서에서 만든 hello DNS 영역과 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-198">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="68cac-199">Hello 클릭 **partners.contoso.net** hello의 DNS 영역 **모든 리소스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-199">Click hello **partners.contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="68cac-200">이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **partners.contoso.net** 이름별 필터 hello에...</span><span class="sxs-lookup"><span data-stu-id="68cac-200">If hello subscription you selected already has several resources in it, you can enter **partners.contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="68cac-201">상자 tooeasily 액세스 hello DNS 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-201">box tooeasily access hello DNS zone.</span></span>

1. <span data-ttu-id="68cac-202">Hello DNS 영역 블레이드에서 hello 이름 서버를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-202">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="68cac-203">이 예제에서는 hello 영역 'contoso.net' 할당 된 이름 서버에 ' n s 1-01.azure-dns.com', 'ns2 01.azure dns.net', ' ns3-01.azure-dns.org', 및 ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="68cac-203">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="68cac-205">Azure DNS hello 지정 된 이름 서버를 포함 하 여 영역에 권한 있는 NS 레코드를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-205">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="68cac-206">Azure PowerShell 또는 Azure CLI를 통해 toosee hello 이름 서버 이름을 지정 하기만 하면 tooretrieve 이러한 레코드, 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-206">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="68cac-207">부모 영역에 이름 서버 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="68cac-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="68cac-208">Toohello 이동 **contoso.net** hello Azure 포털에서에서 DNS 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-208">Navigate toohello **contoso.net** DNS zone in hello Azure portal.</span></span>
1. <span data-ttu-id="68cac-209">**+ 레코드 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="68cac-210">Hello에 **레코드 집합을 추가** 블레이드에서 hello 다음 값을 입력 한 다음 클릭 **확인**:</span><span class="sxs-lookup"><span data-stu-id="68cac-210">On hello **Add record set** blade, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="68cac-211">**설정**</span><span class="sxs-lookup"><span data-stu-id="68cac-211">**Setting**</span></span> | <span data-ttu-id="68cac-212">**값**</span><span class="sxs-lookup"><span data-stu-id="68cac-212">**Value**</span></span> | <span data-ttu-id="68cac-213">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="68cac-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="68cac-214">**Name**</span><span class="sxs-lookup"><span data-stu-id="68cac-214">**Name**</span></span>|<span data-ttu-id="68cac-215">파트너</span><span class="sxs-lookup"><span data-stu-id="68cac-215">partners</span></span>|<span data-ttu-id="68cac-216">hello hello 자식 DNS 영역 이름</span><span class="sxs-lookup"><span data-stu-id="68cac-216">hello name of hello child DNS zone</span></span>|
   |<span data-ttu-id="68cac-217">**형식**</span><span class="sxs-lookup"><span data-stu-id="68cac-217">**Type**</span></span>|<span data-ttu-id="68cac-218">NS</span><span class="sxs-lookup"><span data-stu-id="68cac-218">NS</span></span>|<span data-ttu-id="68cac-219">이름 서버 레코드에 NS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="68cac-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="68cac-220">**TTL**</span></span>|<span data-ttu-id="68cac-221">1</span><span class="sxs-lookup"><span data-stu-id="68cac-221">1</span></span>|<span data-ttu-id="68cac-222">Toolive 사용 되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-222">Time toolive.</span></span>|
   |<span data-ttu-id="68cac-223">**TTL 단위**</span><span class="sxs-lookup"><span data-stu-id="68cac-223">**TTL unit**</span></span>|<span data-ttu-id="68cac-224">시간</span><span class="sxs-lookup"><span data-stu-id="68cac-224">Hours</span></span>|<span data-ttu-id="68cac-225">시간 단위 toolive toohours 설정</span><span class="sxs-lookup"><span data-stu-id="68cac-225">sets time toolive unit toohours</span></span>|
   |<span data-ttu-id="68cac-226">**이름 서버**</span><span class="sxs-lookup"><span data-stu-id="68cac-226">**NAME SERVER**</span></span>|<span data-ttu-id="68cac-227">{partners.contoso.net 영역의 이름 서버}</span><span class="sxs-lookup"><span data-stu-id="68cac-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="68cac-228">Partners.contoso.net 영역에서 모든 4 hello 이름 서버를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-228">Enter all 4 of hello name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="68cac-230">다른 도구를 사용하여 Azure DNS에서 하위 도메인 위임</span><span class="sxs-lookup"><span data-stu-id="68cac-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="68cac-231">hello 다음 예제에서는 제공 hello 단계 toodelegate PowerShell 및 CLI Azure DNS에 하위 도메인:</span><span class="sxs-lookup"><span data-stu-id="68cac-231">hello following examples provide hello steps toodelegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="68cac-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68cac-232">PowerShell</span></span>

<span data-ttu-id="68cac-233">다음 PowerShell 예에서는 hello이 작동 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-233">hello following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="68cac-234">hello hello Azure 포털을 통해 실행할 수 있습니다 또는 hello 플랫폼 간 Azure CLI를 통해 동일한 단계를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-234">hello same steps can be executed via hello Azure portal, or via hello cross-platform Azure CLI.</span></span>

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="68cac-235">사용 하 여 `nslookup` 모든 항목이 올바르게 설정 되어 hello hello 자식 영역 SOA 레코드를 조회 하 여 tooverify 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-235">Use `nslookup` tooverify that everything is set up correctly by looking up hello SOA record of hello child zone.</span></span>

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a><span data-ttu-id="68cac-236">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="68cac-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="68cac-237">Hello 이름 서버 hello에 대 한 검색 `partners.contoso.net` hello 출력에서 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-237">Retrieve hello name servers for hello `partners.contoso.net` zone from hello output.</span></span>

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="68cac-238">레코드 집합 hello와 각 이름 서버에 대 한 NS 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-238">Create hello record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="68cac-239">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="68cac-239">Delete all resources</span></span>

<span data-ttu-id="68cac-240">이 문서에서는 다음 단계 완료 hello에서에서 만든 모든 리소스를 toodelete:</span><span class="sxs-lookup"><span data-stu-id="68cac-240">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="68cac-241">Hello Azure 포털에서에서 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-241">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="68cac-242">Hello 클릭 **contosorg** 리소스 그룹 hello에서 모든 리소스 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-242">Click hello **contosorg** resource group in hello All resources blade.</span></span> <span data-ttu-id="68cac-243">이미 선택한 hello 구독에 여러 자원이 인 경우 입력 하면 **contosorg** hello에 **이름별으로 필터링...**</span><span class="sxs-lookup"><span data-stu-id="68cac-243">If hello subscription you selected already has several resources in it, you can enter **contosorg** in hello **Filter by name…**</span></span> <span data-ttu-id="68cac-244">상자 tooeasily 액세스 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-244">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="68cac-245">Hello에 **contosorg** 블레이드에서 hello 클릭 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-245">In hello **contosorg** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="68cac-246">hello 포털 해야 tootype hello 이름의 hello 리소스 그룹 tooconfirm toodelete 원하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-246">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="68cac-247">형식 *contosorg* hello 리소스 그룹 이름에 대 한 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-247">Type *contosorg* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="68cac-248">리소스 그룹을 삭제 hello 리소스 그룹 내에서 모든 리소스에 있으므로 항상 있는지 tooconfirm 리소스 그룹의 hello 내용을 삭제 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-248">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="68cac-249">hello 포털 hello 리소스 그룹 내에 포함 된 모든 리소스를 삭제 한 다음 자체 hello 리소스 그룹을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-249">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="68cac-250">이 프로세스는 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="68cac-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68cac-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68cac-251">Next steps</span></span>

[<span data-ttu-id="68cac-252">DNS 영역 관리</span><span class="sxs-lookup"><span data-stu-id="68cac-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="68cac-253">DNS 레코드 관리</span><span class="sxs-lookup"><span data-stu-id="68cac-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
