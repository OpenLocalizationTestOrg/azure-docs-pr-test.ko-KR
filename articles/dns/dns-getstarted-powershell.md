---
title: "PowerShell을 사용하여 Azure DNS 시작 | Microsoft Docs"
description: "Azure DNS에 DNS 영역 및 레코드를 만드는 방법을 알아봅니다. PowerShell을 사용하여 첫 번째 DNS 영역 및 레코드를 만들고 관리하는 단계별 가이드입니다."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 48f7ba325f61b4a91c0208b4c99058da801bee19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="a4fe7-104">PowerShell을 사용하여 Azure DNS 시작</span><span class="sxs-lookup"><span data-stu-id="a4fe7-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4fe7-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="a4fe7-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="a4fe7-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4fe7-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="a4fe7-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a4fe7-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="a4fe7-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a4fe7-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="a4fe7-109">이 문서에서는 Azure PowerShell을 사용하여 DNS 영역 및 레코드를 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-109">This article walks you through the steps to create your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="a4fe7-110">Azure Portal 또는 플랫폼 간 Azure CLI를 사용하여 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-110">You can also perform these steps using the Azure portal or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="a4fe7-111">DNS 영역은 특정 도메인에 대한 DNS 레코드를 호스트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="a4fe7-112">Azure DNS에서 도메인 호스팅을 시작하려면 해당 도메인 이름의 DNS 영역을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="a4fe7-113">그러면 이 DNS 영역 안에 도메인의 각 DNS 레코드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="a4fe7-114">마지막으로 DNS 영역을 인터넷에 게시하려면 도메인에 대한 이름 서버를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="a4fe7-115">아래에서는 이러한 각 단계에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-115">Each of these steps is described below.</span></span>

<span data-ttu-id="a4fe7-116">이 지침에서는 이미 Azure PowerShell을 설치했고, 로그인했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-116">These instructions assume you have already installed and signed in to Azure PowerShell.</span></span> <span data-ttu-id="a4fe7-117">도움말은 [PowerShell을 사용하여 DNS 영역을 관리하는 방법](dns-operations-dnszones.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-117">For help, see [How to manage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="a4fe7-118">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="a4fe7-118">Create the resource group</span></span>

<span data-ttu-id="a4fe7-119">DNS 영역을 만들기 전에 DNS 영역을 포함할 리소스 그룹이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="a4fe7-120">다음은 명령을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-120">The following shows the command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="a4fe7-121">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="a4fe7-121">Create a DNS zone</span></span>

<span data-ttu-id="a4fe7-122">DNS 영역은 `New-AzureRmDnsZone` cmdlet을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-122">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="a4fe7-123">다음 예제에서는 *MyResourceGroup*이라는 리소스 그룹에 *contoso.com*이라는 DNS 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="a4fe7-124">예제를 사용하여 DNS 영역을 만들고 사용자 고유 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-124">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="a4fe7-125">DNS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="a4fe7-125">Create a DNS record</span></span>

<span data-ttu-id="a4fe7-126">`New-AzureRmDnsRecordSet` cmdlet을 사용하여 레코드 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-126">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="a4fe7-127">다음 예제에서는 리소스 그룹 "MyResourceGroup"에서 DNS 영역 "contoso.com"에 상대적 이름 "www"가 포함된 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-127">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="a4fe7-128">레코드의 정규화된 이름은 “www.contoso.com”입니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-128">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="a4fe7-129">레코드 형식은 "A"이고, IP 주소는 "1.2.3.4"이며, TTL은 3600초입니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-129">The record type is "A", with IP address "1.2.3.4", and the TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="a4fe7-130">두 개 이상의 레코드가 있는 레코드 집합 등 다른 레코드 유형을 알아보거나 기존 레코드를 수정하려면 [Azure PowerShell을 사용하여 DNS 레코드 및 레코드 집합 관리](dns-operations-recordsets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-130">For other record types, for record sets with more than one record, and to modify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="a4fe7-131">레코드 보기</span><span class="sxs-lookup"><span data-stu-id="a4fe7-131">View records</span></span>

<span data-ttu-id="a4fe7-132">사용자 영역에 DNS 레코드를 나열하려면 다음을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-132">To list the DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="a4fe7-133">이름 서버 업데이트</span><span class="sxs-lookup"><span data-stu-id="a4fe7-133">Update name servers</span></span>

<span data-ttu-id="a4fe7-134">DNS 영역 및 레코드가 적절히 설정되었다면 Azure DNS 이름 서버를 사용하도록 도메인 이름을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="a4fe7-135">이렇게 하면 인터넷에 있는 다른 사용자가 DNS 레코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-135">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="a4fe7-136">영역에 대한 이름 서버는 `Get-AzureRmDnsZone` cmdlet으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-136">The name servers for your zone are given by the `Get-AzureRmDnsZone` cmdlet:</span></span>

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

<span data-ttu-id="a4fe7-137">이러한 이름 서버는 사용자가 도메인 이름을 구입한 도메인 이름 등록 기관에서 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-137">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="a4fe7-138">등록 기관에서 도메인에 대한 이름 서버를 설정하는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-138">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="a4fe7-139">자세한 내용은 [Azure DNS에 도메인 위임](dns-domain-delegation.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-139">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="a4fe7-140">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="a4fe7-140">Delete all resources</span></span>

<span data-ttu-id="a4fe7-141">이 문서에서 만든 모든 리소스를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-141">To delete all resources created in this article, take the following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="a4fe7-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4fe7-142">Next steps</span></span>

<span data-ttu-id="a4fe7-143">Azure DNS에 대한 자세한 내용은 [Azure DNS 개요](dns-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-143">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="a4fe7-144">Azure DNS에서 DNS 영역 관리에 대한 자세한 내용은 [PowerShell을 사용하여 Azure DNS에서 DNS 영역 관리](dns-operations-dnszones.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-144">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="a4fe7-145">Azure DNS에서 DNS 레코드 관리에 대한 자세한 내용은 [PowerShell을 사용하여 Azure DNS에서 DNS 레코드 및 레코드 집합 관리](dns-operations-recordsets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4fe7-145">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

