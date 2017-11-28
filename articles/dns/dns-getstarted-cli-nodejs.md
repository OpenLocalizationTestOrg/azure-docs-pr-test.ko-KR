---
title: "Azure CLI 1.0을 사용 하 여 Azure DNS aaaGet 시작 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate DNS 영역 및 Azure DNS에 레코드입니다. 단계별 가이드 toocreate 이며 첫 번째 DNS 영역 및 Azure CLI 1.0 hello를 사용 하 여 레코드를 관리 합니다."
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
ms.openlocfilehash: e200c848ad261160e593306dbb8a1d92bf26880b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="9c227-104">Azure CLI 1.0을 사용하여 Azure DNS 시작</span><span class="sxs-lookup"><span data-stu-id="9c227-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c227-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9c227-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="9c227-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c227-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="9c227-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9c227-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="9c227-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9c227-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="9c227-109">이 문서 안내 하 hello 단계 toocreate 첫 번째 DNS 영역이 고은 Windows, Mac 및 Linux 가능한 플랫폼 간 Azure CLI 1.0 hello 사용 하 여 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="9c227-110">Hello Azure 포털 또는 Azure PowerShell을 사용 하 여 이러한 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="9c227-111">DNS 영역에는 특정 도메인에 대 한 사용 되는 toohost hello DNS 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="9c227-112">Azure DNS에서 도메인 호스팅 toostart toocreate DNS 영역 해당 도메인 이름을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="9c227-113">그러면 이 DNS 영역 안에 도메인의 각 DNS 레코드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="9c227-114">마지막으로, toopublish DNS 영역 toohello 인터넷 tooconfigure hello 이름 서버 hello 도메인에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="9c227-115">아래에서는 이러한 각 단계에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-115">Each of these steps is described below.</span></span>

<span data-ttu-id="9c227-116">이러한 지침에는 이미 설치 및 CLI 1.0 tooAzure 로그인 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-116">These instructions assume you have already installed and signed in tooAzure CLI 1.0.</span></span> <span data-ttu-id="9c227-117">에 대 한 도움말을 참조 하세요. [어떻게 toomanage DNS 영역을 Azure CLI 1.0을 사용 하 여](dns-operations-dnszones-cli-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-117">For help, see [How toomanage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="9c227-118">Hello 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="9c227-118">Create hello resource group</span></span>

<span data-ttu-id="9c227-119">Hello DNS 영역을 만들기 전에 리소스 그룹 toocontain hello DNS 영역이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="9c227-120">hello 다음 hello 명령을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-120">hello following shows hello command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="9c227-121">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="9c227-121">Create a DNS zone</span></span>

<span data-ttu-id="9c227-122">DNS 영역 hello를 사용 하 여 만들어집니다. `azure network dns zone create` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-122">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="9c227-123">이 명령에 대 한 도움말 toosee 입력 `azure network dns zone create -h`합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-123">toosee help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="9c227-124">hello 다음 예제에서는 호출 하는 DNS 영역 *contoso.com* 호출 hello 리소스 그룹에 *MyResourceGroup*합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-124">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="9c227-125">사용자 고유의 대 한 hello 값으로 대체 hello 예제 toocreate DNS 영역을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="9c227-126">DNS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="9c227-126">Create a DNS record</span></span>

<span data-ttu-id="9c227-127">toocreate DNS 레코드를 사용 하 여 hello `azure network dns record-set add-record` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-127">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="9c227-128">도움말을 보려면 `azure network dns record-set add-record -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c227-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="9c227-129">hello 다음 예제에서는 레코드 hello 상대 이름이 "www" hello "MyResourceGroup" 리소스 그룹에 "contoso.com", DNS 영역에서</span><span class="sxs-lookup"><span data-stu-id="9c227-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="9c227-130">hello 정규화 hello 레코드 집합의 이름이 "www.contoso.com" 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="9c227-131">hello 레코드 종류는 "A", "1.2.3.4" IP 주소로 하 고 기본 TTL 3600 초 (1 시간)을 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="9c227-132">다른 레코드 종류에 대 한 대체 TTL 값 및 toomodify 기존 레코드에 대 한 둘 이상의 레코드와 레코드 집합에 대 한 참조 [관리 DNS 레코드 및 레코드 집합을 사용 하 여 hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="9c227-133">레코드 보기</span><span class="sxs-lookup"><span data-stu-id="9c227-133">View records</span></span>

<span data-ttu-id="9c227-134">영역에서 toolist hello DNS 레코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="9c227-135">이름 서버 업데이트</span><span class="sxs-lookup"><span data-stu-id="9c227-135">Update name servers</span></span>

<span data-ttu-id="9c227-136">일단 시작 되 면 DNS 영역과 레코드는 올바르게 설정 되었는지, tooconfigure 필요한 충족 도메인 이름 toouse hello Azure DNS 이름 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="9c227-137">이렇게 하면 다른 사용자 hello 인터넷 toofind에 DNS 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="9c227-138">영역에 대 한 hello 이름 서버 hello에 의해 제공 됩니다 `azure network dns zone show` 명령:</span><span class="sxs-lookup"><span data-stu-id="9c227-138">hello name servers for your zone are given by hello `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

<span data-ttu-id="9c227-139">이러한 이름 서버 hello 도메인 이름 등록 기관 (여기서 구입한 hello 도메인 이름)으로 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-139">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="9c227-140">등록자는 hello 옵션 tooset hello 도메인에 대 한 hello 이름 서버를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-140">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="9c227-141">자세한 내용은 참조 [사용자 도메인 tooAzure DNS 위임](dns-domain-delegation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-141">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="9c227-142">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="9c227-142">Delete all resources</span></span>
 
<span data-ttu-id="9c227-143">take hello 단계 다음에이 문서에서 만든 모든 리소스를 toodelete:</span><span class="sxs-lookup"><span data-stu-id="9c227-143">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="9c227-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c227-144">Next steps</span></span>

<span data-ttu-id="9c227-145">Azure DNS에 대해 자세히 toolearn 참조 [Azure DNS 개요](dns-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-145">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="9c227-146">Azure DNS에 DNS 영역 관리에 대 한 더 toolearn 참조 [Azure CLI 1.0을 사용 하 여 Azure DNS에서 관리 하는 DNS 영역](dns-operations-dnszones-cli-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-146">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="9c227-147">Azure DNS에 DNS 레코드를 관리에 대해 자세히 toolearn 참조 [Azure CLI 1.0을 사용 하 여 Azure DNS에 관리 DNS 레코드와 레코드 집합](dns-operations-recordsets-cli-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c227-147">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

