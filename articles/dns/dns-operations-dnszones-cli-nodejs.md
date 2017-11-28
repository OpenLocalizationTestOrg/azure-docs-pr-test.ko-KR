---
title: "Azure DNS-Azure CLI 1.0에에서 aaaManage DNS 영역 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 DNS 영역을 관리할 수 있습니다. 이 문서에서는 tooupdate, 삭제 하 고 dns를 Azure DNS 영역을 만드는 방법을 보여 줍니다."
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
ms.openlocfilehash: cb9790cc46626ef7f38a43edb57511104fe6057e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="415f8-104">Azure DNS를 사용 하 여 DNS 영역 toomanage Azure CLI 1.0 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="415f8-104">How toomanage DNS Zones in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="415f8-105">포털</span><span class="sxs-lookup"><span data-stu-id="415f8-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="415f8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="415f8-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="415f8-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="415f8-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="415f8-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="415f8-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="415f8-109">이 가이드에서는 어떻게 toomanage DNS 영역을 Windows, Mac 및 Linux에 대 한 사용 하지 않는 플랫폼 간 Azure CLI 1.0 hello를 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-109">This guide shows how toomanage your DNS zones by using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="415f8-110">사용 하 여 DNS 영역을 관리할 수 있습니다 [Azure PowerShell](dns-operations-dnszones.md) 또는 Azure 포털을 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or hello Azure portal.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="415f8-111">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="415f8-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="415f8-112">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="415f8-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="415f8-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="415f8-115">소개</span><span class="sxs-lookup"><span data-stu-id="415f8-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-cli-setup](../../includes/dns-cli-setup-include.md)]

## <a name="getting-help"></a><span data-ttu-id="415f8-116">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="415f8-116">Getting help</span></span>

<span data-ttu-id="415f8-117">TooAzure DNS와 관련 된 모든 CLI 1.0 명령을 시작 `azure network dns`합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-117">All CLI 1.0 commands relating tooAzure DNS start with `azure network dns`.</span></span> <span data-ttu-id="415f8-118">Hello를 사용 하 여 각 명령에 대 한 도움말은 `--help` 옵션 (약식 `-h`).</span><span class="sxs-lookup"><span data-stu-id="415f8-118">Help is available for each command using hello `--help` option (short form `-h`).</span></span>  <span data-ttu-id="415f8-119">예:</span><span class="sxs-lookup"><span data-stu-id="415f8-119">For example:</span></span>

```azurecli
azure network dns -h
azure network dns zone -h
azure network dns zone create -h
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="415f8-120">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="415f8-120">Create a DNS zone</span></span>

<span data-ttu-id="415f8-121">DNS 영역 hello를 사용 하 여 만들어집니다. `azure network dns zone create` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-121">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="415f8-122">도움말을 보려면 `azure network dns zone create -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="415f8-122">For help, see `azure network dns zone create -h`.</span></span>

<span data-ttu-id="415f8-123">hello 다음 예제에서는 호출 하는 DNS 영역 *contoso.com* 호출 hello 리소스 그룹에 *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="415f8-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a><span data-ttu-id="415f8-124">toocreate 태그와 DNS 영역</span><span class="sxs-lookup"><span data-stu-id="415f8-124">toocreate a DNS zone with tags</span></span>

<span data-ttu-id="415f8-125">hello 다음 예제에서는 두 개의 toocreate DNS 영역 방법을 [Azure 리소스 관리자 태그](dns-zones-records.md#tags), *프로젝트 데모 =* 및 *env = 테스트*, hello를 사용 하 여 `--tags` 매개 변수 (약식 `-t`):</span><span class="sxs-lookup"><span data-stu-id="415f8-125">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using hello `--tags` parameter (short form `-t`):</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com -t "project=demo";"env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="415f8-126">DNS 영역 가져오기</span><span class="sxs-lookup"><span data-stu-id="415f8-126">Get a DNS zone</span></span>

<span data-ttu-id="415f8-127">tooretrieve DNS 영역을 사용 하 여 `azure network dns zone show`합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-127">tooretrieve a DNS zone, use `azure network dns zone show`.</span></span> <span data-ttu-id="415f8-128">도움말을 보려면 `azure network dns zone show -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="415f8-128">For help, see `azure network dns zone show -h`.</span></span>

<span data-ttu-id="415f8-129">hello 다음 예제에서는 반환 hello DNS 영역 *contoso.com* 및 리소스 그룹에서 관련된 데이터 *MyResourceGroup*합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-129">hello following example returns hello DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
azure network dns zone show MyResourceGroup contoso.com
```

<span data-ttu-id="415f8-130">다음 예제는 hello hello 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-130">hello following example is hello response.</span></span>

```
info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
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

<span data-ttu-id="415f8-131">DNS 레코드는 `azure network dns zone show`에서 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-131">Note that DNS records are not returned by `azure network dns zone show`.</span></span> <span data-ttu-id="415f8-132">toolist DNS 레코드를 사용 하 여 `azure network dns record-set list`합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-132">toolist DNS records, use `azure network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="415f8-133">DNS 영역 나열</span><span class="sxs-lookup"><span data-stu-id="415f8-133">List DNS zones</span></span>

<span data-ttu-id="415f8-134">tooenumerate DNS 영역을 사용 하 여 `azure network dns zone list`합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-134">tooenumerate DNS zones, use `azure network dns zone list`.</span></span> <span data-ttu-id="415f8-135">도움말을 보려면 `azure network dns zone list -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="415f8-135">For help, see `azure network dns zone list -h`.</span></span>

<span data-ttu-id="415f8-136">Hello 리소스 그룹을 지정 하 여 hello 리소스 그룹 내에서 해당 영역에만 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-136">Specifying hello resource group lists only those zones within hello resource group:</span></span>

```azurecli
azure network dns zone list MyResourceGroup
```

<span data-ttu-id="415f8-137">Hello 리소스 그룹을 생략 hello 구독의 모든 영역을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-137">Omitting hello resource group lists all zones in hello subscription:</span></span>

```azurecli
azure network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="415f8-138">DNS 영역 업데이트</span><span class="sxs-lookup"><span data-stu-id="415f8-138">Update a DNS zone</span></span>

<span data-ttu-id="415f8-139">사용 하 여 DNS 영역 리소스를 제공할 수는 변경 내용 tooa `azure network dns zone set`합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-139">Changes tooa DNS zone resource can be made using `azure network dns zone set`.</span></span> <span data-ttu-id="415f8-140">도움말을 보려면 `azure network dns zone set -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="415f8-140">For help, see `azure network dns zone set -h`.</span></span>

<span data-ttu-id="415f8-141">이 명령은 hello hello 영역 내에서 DNS 레코드 집합의 업데이트 되지 않는 (참조 [어떻게 tooManage DNS 레코드](dns-operations-recordsets-cli-nodejs.md)).</span><span class="sxs-lookup"><span data-stu-id="415f8-141">This command does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets-cli-nodejs.md)).</span></span> <span data-ttu-id="415f8-142">Hello 영역 리소스 자체의 속성을 사용 하는 유일한 tooupdate 것합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-142">It is only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="415f8-143">이러한 속성은 현재 제한 toohello [Azure 리소스 관리자 '태그'](dns-zones-records.md#tags) hello 영역의 리소스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-143">These properties are currently limited toohello [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for hello zone resource.</span></span>

<span data-ttu-id="415f8-144">hello 다음 예제에서는 tooupdate hello DNS 영역에 태그를 삽입 방법</span><span class="sxs-lookup"><span data-stu-id="415f8-144">hello following example shows how tooupdate hello tags on a DNS zone.</span></span> <span data-ttu-id="415f8-145">hello 기존 태그는 지정 된 hello 값으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-145">hello existing tags are replaced by hello value specified.</span></span>

```azurecli
azure network dns zone set MyResourceGroup contoso.com -t "team=support"
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="415f8-146">DNS 영역 삭제</span><span class="sxs-lookup"><span data-stu-id="415f8-146">Delete a DNS Zone</span></span>

<span data-ttu-id="415f8-147">`azure network dns zone delete`를 사용하여 DNS 영역을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-147">DNS zones can be deleted using `azure network dns zone delete`.</span></span> <span data-ttu-id="415f8-148">도움말을 보려면 `azure network dns zone delete -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="415f8-148">For help, see `azure network dns zone delete -h`.</span></span>

> [!NOTE]
> <span data-ttu-id="415f8-149">DNS 영역을 삭제 하면 모든 DNS 레코드가 hello 영역 내에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-149">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="415f8-150">이 작업은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-150">This operation cannot be undone.</span></span> <span data-ttu-id="415f8-151">DNS 영역 hello를 사용 하는 경우 hello 영역이 삭제 되 면 hello 영역을 사용 하 여 서비스 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-151">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="415f8-152">실수로 영역 삭제 tooprotect 참조 [tooprotect DNS 영역 및 기록 방법을](dns-protect-zones-recordsets.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-152">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="415f8-153">이 명령은 확인 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-153">This command prompts for confirmation.</span></span> <span data-ttu-id="415f8-154">선택적 hello `--quiet` 스위치 (약식 `-q`)이이 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-154">hello optional `--quiet` switch (short form `-q`) suppresses this prompt.</span></span>

<span data-ttu-id="415f8-155">hello 다음 예제에서는 어떻게 toodelete hello 영역 *contoso.com* 리소스 그룹에서 *MyResourceGroup*합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-155">hello following example shows how toodelete hello zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
azure network dns zone delete MyResourceGroup contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="415f8-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="415f8-156">Next steps</span></span>

<span data-ttu-id="415f8-157">너무 방법에 대해 알아봅니다[레코드 집합 및 레코드 관리](dns-getstarted-create-recordset-cli-nodejs.md) DNS 영역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-157">Learn how too[manage record sets and records](dns-getstarted-create-recordset-cli-nodejs.md) in your DNS zone.</span></span>

<span data-ttu-id="415f8-158">너무 방법에 대해 알아봅니다[사용자 도메인 tooAzure DNS 위임](dns-domain-delegation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="415f8-158">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

