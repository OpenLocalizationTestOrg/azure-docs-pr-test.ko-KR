---
title: "Azure DNS에 도메인 위임 | Microsoft Docs"
description: "도메인 위임을 변경하고 Azure DNS 이름 서버를 사용하여 도메인 호스팅을 제공하는 방법을 이해합니다."
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
ms.openlocfilehash: 33b3ec24432ff1268860b9a2e9d5098600a8dedc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-a-domain-to-azure-dns"></a><span data-ttu-id="b77ca-103">Azure DNS에 도메인 위임</span><span class="sxs-lookup"><span data-stu-id="b77ca-103">Delegate a domain to Azure DNS</span></span>

<span data-ttu-id="b77ca-104">Azure DNS를 사용하면 DNS 영역을 호스트하고 Azure에서 도메인에 대한 DNS 레코드를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-104">Azure DNS allows you to host a DNS zone and manage the DNS records for a domain in Azure.</span></span> <span data-ttu-id="b77ca-105">도메인에 대한 DNS 쿼리가 Azure DNS에 도달하려면 부모 도메인에서 Azure DNS로 도메인을 위임해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-105">In order for DNS queries for a domain to reach Azure DNS, the domain has to be delegated to Azure DNS from the parent domain.</span></span> <span data-ttu-id="b77ca-106">Azure DNS는 도메인 등록 기관이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-106">Keep in mind Azure DNS is not the domain registrar.</span></span> <span data-ttu-id="b77ca-107">이 문서에서는 Azure DNS에 도메인을 위임하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-107">This article explains how to delegate your domain to Azure DNS.</span></span>

<span data-ttu-id="b77ca-108">등록 기관에서 구입한 도메인의 경우 등록 기관에서는 이러한 NS 레코드를 설정하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-108">For domains purchased from a registrar, your registrar offers the option to set up these NS records.</span></span> <span data-ttu-id="b77ca-109">Azure DNS에서 해당 도메인 이름으로 DNS 영역을 만들기 위해 도메인을 소유할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-109">You do not have to own a domain to create a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="b77ca-110">그러나 등록 기관에서 Azure DNS로 위임을 설정하려면 도메인을 소유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-110">However, you do need to own the domain to set up the delegation to Azure DNS with the registrar.</span></span>

<span data-ttu-id="b77ca-111">예를 들어 'contoso.net' 도메인을 구입하고 Azure DNS에서 이름이 'contoso.net'인 영역을 만든다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-111">For example, suppose you purchase the domain 'contoso.net' and create a zone with the name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="b77ca-112">도메인 소유자로, 등록 기관에서 도메인에 대한 이름 서버 주소(즉, NS 레코드)를 구성하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-112">As the owner of the domain, your registrar offers you the option to configure the name server addresses (that is, the NS records) for your domain.</span></span> <span data-ttu-id="b77ca-113">등록 기관은 이러한 NS 레코드를 상위 도메인(이 예에서는 '.net')에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-113">The registrar stores these NS records in the parent domain, in this case '.net'.</span></span> <span data-ttu-id="b77ca-114">그러면 전 세계의 클라이언트가 'contoso.net'의 DNS 레코드를 확인하려고 할 때 Azure DNS 영역의 도메인으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-114">Clients around the world can then be directed to your domain in Azure DNS zone when trying to resolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="b77ca-115">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="b77ca-115">Create a DNS zone</span></span>

1. <span data-ttu-id="b77ca-116">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-116">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="b77ca-117">허브 메뉴에서 **새로 만들기 > 네트워킹 >**을 클릭한 다음 **DNS 영역**을 클릭하여 DNS 영역 블레이드 만들기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-117">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS 영역](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="b77ca-119">**DNS 영역 만들기** 블레이드에서 다음 값을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-119">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="b77ca-120">**설정**</span><span class="sxs-lookup"><span data-stu-id="b77ca-120">**Setting**</span></span> | <span data-ttu-id="b77ca-121">**값**</span><span class="sxs-lookup"><span data-stu-id="b77ca-121">**Value**</span></span> | <span data-ttu-id="b77ca-122">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="b77ca-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="b77ca-123">**Name**</span><span class="sxs-lookup"><span data-stu-id="b77ca-123">**Name**</span></span>|<span data-ttu-id="b77ca-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="b77ca-124">contoso.net</span></span>|<span data-ttu-id="b77ca-125">DNS 영역의 이름</span><span class="sxs-lookup"><span data-stu-id="b77ca-125">The name of the DNS zone</span></span>|
   |<span data-ttu-id="b77ca-126">**구독**</span><span class="sxs-lookup"><span data-stu-id="b77ca-126">**Subscription**</span></span>|<span data-ttu-id="b77ca-127">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="b77ca-127">[Your subscription]</span></span>|<span data-ttu-id="b77ca-128">응용 프로그램 게이트웨이를 만들 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-128">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="b77ca-129">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="b77ca-129">**Resource group**</span></span>|<span data-ttu-id="b77ca-130">**새로 만들기:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="b77ca-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="b77ca-131">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-131">Create a resource group.</span></span> <span data-ttu-id="b77ca-132">리소스 그룹 이름은 선택한 구독 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-132">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="b77ca-133">리소스 그룹에 대해 자세히 알아보려면 [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b77ca-133">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="b77ca-134">**위치**:</span><span class="sxs-lookup"><span data-stu-id="b77ca-134">**Location**</span></span>|<span data-ttu-id="b77ca-135">미국 서부</span><span class="sxs-lookup"><span data-stu-id="b77ca-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="b77ca-136">리소스 그룹은 리소스 그룹의 위치를 나타내며 DNS 영역에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-136">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="b77ca-137">DNS 영역 위치는 항상 "전역"이며 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-137">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="b77ca-138">이름 서버 검색</span><span class="sxs-lookup"><span data-stu-id="b77ca-138">Retrieve name servers</span></span>

<span data-ttu-id="b77ca-139">DNS 영역을 Azure DNS에 위임하려면 먼저 해당 영역에 대한 이름 서버 이름을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-139">Before you can delegate your DNS zone to Azure DNS, you first need to know the name server names for your zone.</span></span> <span data-ttu-id="b77ca-140">Azure DNS는 영역이 만들어질 때마다 풀에서 이름 서버를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="b77ca-141">DNS 영역을 만든 후 Azure Portal의 **즐겨찾기** 창에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-141">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="b77ca-142">**모든 리소스** 블레이드에서 **contoso.net** DNS 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-142">Click the **contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="b77ca-143">선택한 구독에 이미 여러 개의 리소스가 있는 경우 [이름을 기준으로 필터링...]에 **contoso.net**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-143">If the subscription you selected already has several resources in it, you can enter **contoso.net** in the Filter by name…</span></span> <span data-ttu-id="b77ca-144">응용 프로그램 게이트웨이에 간편하게 액세스할 수 있는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-144">box to easily access the application gateway.</span></span> 

1. <span data-ttu-id="b77ca-145">DNS 영역 블레이드에서 이름 서버를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-145">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="b77ca-146">이 예제에서는 'contoso.com' 영역에 이름 서버 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', 'ns4-01.azure-dns.info'가 할당되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-146">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="b77ca-148">Azure DNS는 할당된 이름 서버를 포함하는 영역에 권한이 있는 NS 레코드를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-148">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="b77ca-149">Azure PowerShell 또는 Azure CLI를 통해 이름 서버 이름을 확인하려면 이러한 레코드만 검색하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-149">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

<span data-ttu-id="b77ca-150">또한 다음 예제에서는 PowerShell 및 Azure CLI를 사용하여 Azure DNS에서 영역의 이름 서버를 검색하는 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-150">The following examples also provide the steps to retrieve the name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="b77ca-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b77ca-151">PowerShell</span></span>

```powershell
# The record name "@" is used to refer to records at the top of the zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="b77ca-152">다음 예제는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-152">The following example is the response.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="b77ca-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b77ca-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="b77ca-154">다음 예제는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-154">The following example is the response.</span></span>

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

## <a name="delegate-the-domain"></a><span data-ttu-id="b77ca-155">도메인 위임</span><span class="sxs-lookup"><span data-stu-id="b77ca-155">Delegate the domain</span></span>

<span data-ttu-id="b77ca-156">DNS 영역을 만들었고 이름 서버를 확보했으니, 이제 Azure DNS 이름 서버를 사용하여 부모 도메인을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-156">Now that the DNS zone is created and you have the name servers, the parent domain needs to be updated with the Azure DNS name servers.</span></span> <span data-ttu-id="b77ca-157">각 등록 기관에는 도메인에 대한 이름 서버 레코드를 변경하는 자체 DNS 관리 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-157">Each registrar has their own DNS management tools to change the name server records for a domain.</span></span> <span data-ttu-id="b77ca-158">등록 기관의 DNS 관리 페이지에서 NS 레코드를 편집하고 NS 레코드를 Azure DNS에서 만든 레코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-158">In the registrar's DNS management page, edit the NS records and replace the NS records with the ones Azure DNS created.</span></span>

<span data-ttu-id="b77ca-159">Azure DNS에 도메인을 위임하는 경우 Azure DNS에서 제공하는 이름 서버 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-159">When delegating a domain to Azure DNS, you must use the name server names provided by Azure DNS.</span></span> <span data-ttu-id="b77ca-160">도메인 이름에 상관 없이 4개의 이름 서버 이름을 모두 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-160">It is recommended to use all four name server names, regardless of the name of your domain.</span></span> <span data-ttu-id="b77ca-161">도메인 위임에는 같은 최상위 도메인을 도메인으로 사용하는 이름 서버 이름이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-161">Domain delegation does not require the name server name to use the same top-level domain as your domain.</span></span>

<span data-ttu-id="b77ca-162">이러한 IP 주소는 나중에 변경될 수 있으므로 Azure DNS 이름 서버 IP 주소를 가리키는 데 '연결 레코드'를 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-162">You should not use 'glue records' to point to the Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="b77ca-163">고유한 영역에서 이름 서버 이름을 사용하는 위임('베니티 이름 서버'라고도 함)은 현재 Azure DNS에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="b77ca-164">이름 확인이 작동하는지 확인</span><span class="sxs-lookup"><span data-stu-id="b77ca-164">Verify name resolution is working</span></span>

<span data-ttu-id="b77ca-165">위임을 완료한 후 'nslookup'과 같은 도구로 영역에 대한 SOA 레코드(영역을 만들 때 자동으로 생성됨)를 쿼리하여 이름 확인이 작동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-165">After completing the delegation, you can verify that name resolution is working by using a tool such as 'nslookup' to query the SOA record for your zone (which is also automatically created when the zone is created).</span></span>

<span data-ttu-id="b77ca-166">위임이 올바르게 설정된 경우 Azure DNS 이름 서버를 지정할 필요가 없습니다. 일반적인 DNS 확인 프로세스는 자동으로 이름 서버를 자동으로 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-166">You do not have to specify the Azure DNS name servers, if the delegation has been set up correctly, the normal DNS resolution process finds the name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="b77ca-167">다음은 이전 명령의 응답 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-167">The following is an example response from the preceding command:</span></span>

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

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="b77ca-168">Azure DNS에서 하위 도메인 위임</span><span class="sxs-lookup"><span data-stu-id="b77ca-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="b77ca-169">별도의 자식 영역을 설정하려는 경우 Azure DNS에 하위 도메인을 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-169">If you want to set up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="b77ca-170">예를 들어 Azure DNS에서 'contoso.net'을 설정하고 위임한 후 별도의 자식 영역 'partners.contoso.net'을 설정하려 한다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like to set up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="b77ca-171">Azure DNS에서 자식 영역 'partners.contoso.net'을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-171">Create the child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="b77ca-172">Azure DNS에서 자식 영역을 호스팅하는 이름 서버를 가져오려면 자식 영역에서 신뢰할 수 있는 NS 레코드를 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-172">Look up the authoritative NS records in the child zone to obtain the name servers hosting the child zone in Azure DNS.</span></span>
3. <span data-ttu-id="b77ca-173">자식 영역을 가리키는 부모 영역에 NS 레코드를 구성하여 자식 영역을 위임합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-173">Delegate the child zone by configuring NS records in the parent zone pointing to the child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="b77ca-174">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="b77ca-174">Create a DNS zone</span></span>

1. <span data-ttu-id="b77ca-175">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-175">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="b77ca-176">허브 메뉴에서 **새로 만들기 > 네트워킹 >**을 클릭한 다음 **DNS 영역**을 클릭하여 DNS 영역 블레이드 만들기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-176">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS 영역](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="b77ca-178">**DNS 영역 만들기** 블레이드에서 다음 값을 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-178">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="b77ca-179">**설정**</span><span class="sxs-lookup"><span data-stu-id="b77ca-179">**Setting**</span></span> | <span data-ttu-id="b77ca-180">**값**</span><span class="sxs-lookup"><span data-stu-id="b77ca-180">**Value**</span></span> | <span data-ttu-id="b77ca-181">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="b77ca-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="b77ca-182">**Name**</span><span class="sxs-lookup"><span data-stu-id="b77ca-182">**Name**</span></span>|<span data-ttu-id="b77ca-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="b77ca-183">partners.contoso.net</span></span>|<span data-ttu-id="b77ca-184">DNS 영역의 이름</span><span class="sxs-lookup"><span data-stu-id="b77ca-184">The name of the DNS zone</span></span>|
   |<span data-ttu-id="b77ca-185">**구독**</span><span class="sxs-lookup"><span data-stu-id="b77ca-185">**Subscription**</span></span>|<span data-ttu-id="b77ca-186">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="b77ca-186">[Your subscription]</span></span>|<span data-ttu-id="b77ca-187">응용 프로그램 게이트웨이를 만들 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-187">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="b77ca-188">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="b77ca-188">**Resource group**</span></span>|<span data-ttu-id="b77ca-189">**기존 리소스 그룹 사용:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="b77ca-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="b77ca-190">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-190">Create a resource group.</span></span> <span data-ttu-id="b77ca-191">리소스 그룹 이름은 선택한 구독 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-191">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="b77ca-192">리소스 그룹에 대해 자세히 알아보려면 [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) 개요 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b77ca-192">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="b77ca-193">**위치**:</span><span class="sxs-lookup"><span data-stu-id="b77ca-193">**Location**</span></span>|<span data-ttu-id="b77ca-194">미국 서부</span><span class="sxs-lookup"><span data-stu-id="b77ca-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="b77ca-195">리소스 그룹은 리소스 그룹의 위치를 나타내며 DNS 영역에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-195">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="b77ca-196">DNS 영역 위치는 항상 "전역"이며 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-196">The DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="b77ca-197">이름 서버 검색</span><span class="sxs-lookup"><span data-stu-id="b77ca-197">Retrieve name servers</span></span>

1. <span data-ttu-id="b77ca-198">DNS 영역을 만든 후 Azure Portal의 **즐겨찾기** 창에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-198">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="b77ca-199">**모든 리소스** 블레이드에서 **partners.contoso.net** DNS 영역을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-199">Click the **partners.contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="b77ca-200">선택한 구독에 이미 여러 개의 리소스가 있는 경우 [이름을 기준으로 필터링...]에 **partners.contoso.net**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-200">If the subscription you selected already has several resources in it, you can enter **partners.contoso.net** in the Filter by name…</span></span> <span data-ttu-id="b77ca-201">DNS 영역에 간편하게 액세스할 수 있는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-201">box to easily access the DNS zone.</span></span>

1. <span data-ttu-id="b77ca-202">DNS 영역 블레이드에서 이름 서버를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-202">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="b77ca-203">이 예제에서는 'contoso.com' 영역에 이름 서버 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', 'ns4-01.azure-dns.info'가 할당되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-203">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="b77ca-205">Azure DNS는 할당된 이름 서버를 포함하는 영역에 권한이 있는 NS 레코드를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-205">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="b77ca-206">Azure PowerShell 또는 Azure CLI를 통해 이름 서버 이름을 확인하려면 이러한 레코드만 검색하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-206">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="b77ca-207">부모 영역에 이름 서버 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="b77ca-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="b77ca-208">Azure Portal에서 **contoso.net** DNS 영역으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-208">Navigate to the **contoso.net** DNS zone in the Azure portal.</span></span>
1. <span data-ttu-id="b77ca-209">**+ 레코드 집합**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="b77ca-210">**레코드 집합 추가** 블레이드에서 다음 값을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-210">On the **Add record set** blade, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="b77ca-211">**설정**</span><span class="sxs-lookup"><span data-stu-id="b77ca-211">**Setting**</span></span> | <span data-ttu-id="b77ca-212">**값**</span><span class="sxs-lookup"><span data-stu-id="b77ca-212">**Value**</span></span> | <span data-ttu-id="b77ca-213">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="b77ca-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="b77ca-214">**Name**</span><span class="sxs-lookup"><span data-stu-id="b77ca-214">**Name**</span></span>|<span data-ttu-id="b77ca-215">파트너</span><span class="sxs-lookup"><span data-stu-id="b77ca-215">partners</span></span>|<span data-ttu-id="b77ca-216">자식 DNS 영역의 이름</span><span class="sxs-lookup"><span data-stu-id="b77ca-216">The name of the child DNS zone</span></span>|
   |<span data-ttu-id="b77ca-217">**형식**</span><span class="sxs-lookup"><span data-stu-id="b77ca-217">**Type**</span></span>|<span data-ttu-id="b77ca-218">NS</span><span class="sxs-lookup"><span data-stu-id="b77ca-218">NS</span></span>|<span data-ttu-id="b77ca-219">이름 서버 레코드에 NS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="b77ca-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="b77ca-220">**TTL**</span></span>|<span data-ttu-id="b77ca-221">1</span><span class="sxs-lookup"><span data-stu-id="b77ca-221">1</span></span>|<span data-ttu-id="b77ca-222">Time to Live입니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-222">Time to live.</span></span>|
   |<span data-ttu-id="b77ca-223">**TTL 단위**</span><span class="sxs-lookup"><span data-stu-id="b77ca-223">**TTL unit**</span></span>|<span data-ttu-id="b77ca-224">시간</span><span class="sxs-lookup"><span data-stu-id="b77ca-224">Hours</span></span>|<span data-ttu-id="b77ca-225">Time to Live를 시간 단위로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-225">sets time to live unit to hours</span></span>|
   |<span data-ttu-id="b77ca-226">**이름 서버**</span><span class="sxs-lookup"><span data-stu-id="b77ca-226">**NAME SERVER**</span></span>|<span data-ttu-id="b77ca-227">{partners.contoso.net 영역의 이름 서버}</span><span class="sxs-lookup"><span data-stu-id="b77ca-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="b77ca-228">partners.contoso.net 영역의 이름 서버 4개를 모두 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-228">Enter all 4 of the name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="b77ca-230">다른 도구를 사용하여 Azure DNS에서 하위 도메인 위임</span><span class="sxs-lookup"><span data-stu-id="b77ca-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="b77ca-231">다음 예에서는 PowerShell 및 CLI를 사용하여 Azure DNS에서 하위 도메인을 위임하는 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-231">The following examples provide the steps to delegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="b77ca-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b77ca-232">PowerShell</span></span>

<span data-ttu-id="b77ca-233">다음 PowerShell 예는 작동 방식을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-233">The following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="b77ca-234">Azure Portal 또는 크로스 플랫폼 Azure CLI를 통해 동일한 단계를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-234">The same steps can be executed via the Azure portal, or via the cross-platform Azure CLI.</span></span>

```powershell
# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve the authoritative NS records from the child zone as shown in the next example. This contains the name servers assigned to the child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create the corresponding NS record set in the parent zone to complete the delegation. The record set name in the parent zone matches the child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="b77ca-235">`nslookup`을 통해 자식 영역의 SOA 레코드를 조회하여 모든 항목이 올바르게 설정되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-235">Use `nslookup` to verify that everything is set up correctly by looking up the SOA record of the child zone.</span></span>

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

#### <a name="azure-cli"></a><span data-ttu-id="b77ca-236">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b77ca-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="b77ca-237">출력에서 `partners.contoso.net` 영역의 이름 서버를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-237">Retrieve the name servers for the `partners.contoso.net` zone from the output.</span></span>

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

<span data-ttu-id="b77ca-238">각 이름 서버의 레코드 집합 및 NS 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-238">Create the record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create the record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="b77ca-239">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="b77ca-239">Delete all resources</span></span>

<span data-ttu-id="b77ca-240">이 문서에서 만든 모든 리소스를 삭제하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-240">To delete all resources created in this article, complete the following steps:</span></span>

1. <span data-ttu-id="b77ca-241">Azure Portal의 **즐겨찾기** 창에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-241">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="b77ca-242">[모든 리소스] 블레이드에서 **contosorg** 리소스 그룹을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-242">Click the **contosorg** resource group in the All resources blade.</span></span> <span data-ttu-id="b77ca-243">선택한 구독에 이미 여러 개의 리소스가 있는 경우 **이름을 기준으로 필터링...**에 **contosorg**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-243">If the subscription you selected already has several resources in it, you can enter **contosorg** in the **Filter by name…**</span></span> <span data-ttu-id="b77ca-244">리소스 그룹에 간편하게 액세스할 수 있는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-244">box to easily access the resource group.</span></span>
1. <span data-ttu-id="b77ca-245">**contosorg** 블레이드에서 **삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-245">In the **contosorg** blade, click the **Delete** button.</span></span>
1. <span data-ttu-id="b77ca-246">포털에서 삭제할 리소스 그룹의 이름을 입력하여 리소스 그룹 삭제를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-246">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span></span> <span data-ttu-id="b77ca-247">리소스 그룹 이름으로 *contosorg*를 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-247">Type *contosorg* for the resource group name, then click **Delete**.</span></span> <span data-ttu-id="b77ca-248">리소스 그룹을 삭제하면 리소스 그룹 내 모든 리소스가 삭제되므로 리소스 그룹을 삭제하기 전에 리소스 그룹의 콘텐츠를 항상 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-248">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span></span> <span data-ttu-id="b77ca-249">포털에서 리소스 그룹 내 포함된 모든 리소스가 삭제된 다음 리소스 그룹 자체가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-249">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span></span> <span data-ttu-id="b77ca-250">이 프로세스는 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b77ca-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b77ca-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b77ca-251">Next steps</span></span>

[<span data-ttu-id="b77ca-252">DNS 영역 관리</span><span class="sxs-lookup"><span data-stu-id="b77ca-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="b77ca-253">DNS 레코드 관리</span><span class="sxs-lookup"><span data-stu-id="b77ca-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
