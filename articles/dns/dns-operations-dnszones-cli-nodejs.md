---
title: "Azure DNS에서 DNS 영역 관리 - Azure CLI 1.0 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 DNS 영역을 관리할 수 있습니다. 이 문서에서는 Azure DNS에서 DNS 영역을 업데이트, 삭제 및 만드는 방법을 설명합니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 588c87749f049eff5b9e0729f6769c8367ba41e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="6e593-104">Azure CLI 1.0을 사용하여 Azure DNS에서 DNS 영역을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="6e593-104">How to manage DNS Zones in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e593-105">포털</span><span class="sxs-lookup"><span data-stu-id="6e593-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="6e593-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e593-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="6e593-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6e593-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="6e593-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6e593-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="6e593-109">이 가이드는 Windows, Mac 및 Linux에서 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용하여 DNS 영역을 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="6e593-110">[Azure PowerShell](dns-operations-dnszones.md) 또는 Azure Portal을 사용하여 DNS 영역을 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6e593-111">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="6e593-111">CLI versions to complete the task</span></span>

<span data-ttu-id="6e593-112">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="6e593-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - 클래식 및 리소스 관리 배포 모델용 CLI.</span><span class="sxs-lookup"><span data-stu-id="6e593-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="6e593-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - 리소스 관리 배포 모델용 차세대 CLI.</span><span class="sxs-lookup"><span data-stu-id="6e593-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="6e593-115">소개</span><span class="sxs-lookup"><span data-stu-id="6e593-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="6e593-116">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="6e593-116">Getting help</span></span>

<span data-ttu-id="6e593-117">Azure DNS에 관련된 모든 CLI 1.0 명령은 `azure network dns`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-117">All CLI 1.0 commands relating to Azure DNS start with `azure network dns`.</span></span> <span data-ttu-id="6e593-118">`--help` 옵션(약식 `-h`)을 사용하여 각 명령에 대한 도움말을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-118">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="6e593-119">예:</span><span class="sxs-lookup"><span data-stu-id="6e593-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="6e593-120">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="6e593-120">Create a DNS zone</span></span>

<span data-ttu-id="6e593-121">`azure network dns zone create` 명령을 사용하여 DNS 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-121">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="6e593-122">도움말을 보려면 `azure network dns zone create -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e593-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="6e593-123">다음 예제에서는 *MyResourceGroup*이라는 리소스 그룹에 *contoso.com*이라는 DNS 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="6e593-124">태그를 사용하여 DNS 영역을 만들려면</span><span class="sxs-lookup"><span data-stu-id="6e593-124">To create a DNS zone with tags</span></span>

<span data-ttu-id="6e593-125">다음 예제에서는 두 [Azure Resource Manager 태그](dns-zones-records.md#tags), *project = demo* 및 *env = test*와 함께 `--tags` 매개 변수(짧은 양식 `-t`)를 사용하여 DNS 영역을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-125">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="6e593-126">DNS 영역 가져오기</span><span class="sxs-lookup"><span data-stu-id="6e593-126">Get a DNS zone</span></span>

<span data-ttu-id="6e593-127">DNS 영역을 가져오려면 `azure network dns zone show`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-127">To retrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="6e593-128">도움말을 보려면 `azure network dns zone show -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e593-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="6e593-129">다음 예제에서는 DNS 영역 *contoso.com* 및 해당 관련 데이터를 리소스 그룹 *MyResourceGroup*에서 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-129">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="6e593-130">다음 예제는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-130">The following example is the response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
data:    Id                              : /subscriptions/.../contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 2
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            : project=demo;env=test
info:    network dns zone show command OK
```

<span data-ttu-id="6e593-131">DNS 레코드는 `azure network dns zone show`에서 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="6e593-132">DNS 레코드를 나열하려면 `azure network dns record-set list`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-132">To list DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="6e593-133">DNS 영역 나열</span><span class="sxs-lookup"><span data-stu-id="6e593-133">List DNS zones</span></span>

<span data-ttu-id="6e593-134">DNS 영역을 열거하려면 `azure network dns zone list`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-134">To enumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="6e593-135">도움말을 보려면 `azure network dns zone list -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e593-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="6e593-136">리소스 그룹을 지정하면 리소스 그룹 내의 해당 영역만 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-136">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="6e593-137">리소스 그룹을 생략하면 구독의 모든 영역이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-137">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="6e593-138">DNS 영역 업데이트</span><span class="sxs-lookup"><span data-stu-id="6e593-138">Update a DNS zone</span></span>

<span data-ttu-id="6e593-139">`azure network dns zone set`를 사용하여 DNS 영역 리소스를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-139">Changes to a DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="6e593-140">도움말을 보려면 `azure network dns zone set -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e593-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="6e593-141">이 명령은 영역 내의 DNS 레코드 집합을 업데이트하지 않습니다([DNS 레코드를 관리하는 방법](dns-operations-recordsets-cli-nodejs.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="6e593-141">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="6e593-142">영역 리소스 자체의 속성을 업데이트하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-142">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="6e593-143">이러한 속성은 현재 영역 리소스에 대한 [Azure Resource Manager '태그'](dns-zones-records.md#tags)로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-143">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="6e593-144">다음 예제에서는 DNS 영역에서 태그를 업데이트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-144">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="6e593-145">기존 태그는 지정된 값으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-145">The existing tags are replaced by the value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="6e593-146">DNS 영역 삭제</span><span class="sxs-lookup"><span data-stu-id="6e593-146">Delete a DNS Zone</span></span>

<span data-ttu-id="6e593-147">`azure network dns zone delete`를 사용하여 DNS 영역을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="6e593-148">도움말을 보려면 `azure network dns zone delete -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e593-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="6e593-149">DNS 영역을 삭제하면 영역 내의 모든 DNS 레코드도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-149">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="6e593-150">이 작업은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-150">This operation cannot be undone.</span></span> <span data-ttu-id="6e593-151">DNS 영역을 사용 중인 경우 영역이 삭제되면 영역을 사용하는 서비스가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-151">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="6e593-152">실수로 영역이 삭제되는 것을 방지하려면 [DNS 영역 및 레코드를 보호하는 방법](dns-protect-zones-recordsets.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6e593-152">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="6e593-153">이 명령은 확인 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-153">This command prompts for confirmation.</span></span> <span data-ttu-id="6e593-154">선택적 `--quiet` 스위치(약식 `-q`)는 이 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-154">The optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="6e593-155">다음 예제는 리소스 그룹 *MyResourceGroup*에서 *contoso.com* 영역을 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-155">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="6e593-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6e593-156">Next steps</span></span>

<span data-ttu-id="6e593-157">DNS 영역에서 [레코드 집합 및 레코드 관리](dns-getstarted-create-recordset-cli-nodejs.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-157">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="6e593-158">[Azure DNS에 도메인을 위임](dns-domain-delegation.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6e593-158">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

