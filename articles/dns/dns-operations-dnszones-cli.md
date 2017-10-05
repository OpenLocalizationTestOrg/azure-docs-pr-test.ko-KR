---
title: "Azure DNS에서 DNS 영역 관리 - Azure CLI 2.0 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 DNS 영역을 관리할 수 있습니다. 이 문서에서는 Azure DNS에서 DNS 영역을 업데이트, 삭제 및 만드는 방법을 설명합니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 1414baf9e51d648cc3a46c4f8635040b4d276910
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="d4487-104">Azure CLI 2.0을 사용하여 Azure DNS에서 DNS 영역을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="d4487-104">How to manage DNS Zones in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4487-105">포털</span><span class="sxs-lookup"><span data-stu-id="d4487-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="d4487-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4487-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="d4487-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d4487-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="d4487-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d4487-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)


<span data-ttu-id="d4487-109">이 가이드는 Windows, Mac 및 Linux에서 사용할 수 있는 플랫폼 간 Azure CLI를 사용하여 DNS 영역을 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-109">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="d4487-110">[Azure PowerShell](dns-operations-dnszones.md) 또는 Azure Portal을 사용하여 DNS 영역을 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-110">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="d4487-111">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="d4487-111">CLI versions to complete the task</span></span>

<span data-ttu-id="d4487-112">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="d4487-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - 클래식 및 리소스 관리 배포 모델용 CLI.</span><span class="sxs-lookup"><span data-stu-id="d4487-113">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="d4487-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - 리소스 관리 배포 모델용 차세대 CLI.</span><span class="sxs-lookup"><span data-stu-id="d4487-114">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="d4487-115">소개</span><span class="sxs-lookup"><span data-stu-id="d4487-115">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="d4487-116">Azure DNS용 Azure CLI 2.0 설정</span><span class="sxs-lookup"><span data-stu-id="d4487-116">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="d4487-117">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d4487-117">Before you begin</span></span>

<span data-ttu-id="d4487-118">구성을 시작하기 전에 다음 항목이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-118">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="d4487-119">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="d4487-119">An Azure subscription.</span></span> <span data-ttu-id="d4487-120">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-120">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="d4487-121">Windows, Linux 또는 MAC용 최신 버전의 Azure CLI 2.0을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-121">Install the latest version of the Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="d4487-122">자세한 내용은 [Azure CLI 2.0 설정](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4487-122">More information is available at [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="d4487-123">Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="d4487-123">Sign in to your Azure account</span></span>

<span data-ttu-id="d4487-124">콘솔 창을 열고 자격 증명을 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-124">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="d4487-125">자세한 내용은 Azure CLI에서 Azure에 로그인을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4487-125">For more information, see Log in to Azure from the Azure CLI</span></span>

```
az login
```

### <a name="select-the-subscription"></a><span data-ttu-id="d4487-126">구독 선택</span><span class="sxs-lookup"><span data-stu-id="d4487-126">Select the subscription</span></span>

<span data-ttu-id="d4487-127">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-127">Check the subscriptions for the account.</span></span>

```
az account list
```

<span data-ttu-id="d4487-128">사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-128">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="d4487-129">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d4487-129">Create a resource group</span></span>

<span data-ttu-id="d4487-130">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d4487-131">이 위치는 해당 리소스 그룹에서 리소스의 기본 위치로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="d4487-132">그러나 모든 DNS 리소스는 국가별이 아니라 전역이므로 리소스 그룹의 위치 선택이 Azure DNS에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-132">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="d4487-133">기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-133">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="d4487-134">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="d4487-134">Getting help</span></span>

<span data-ttu-id="d4487-135">Azure DNS에 관련된 모든 CLI 2.0 명령은 `az network dns`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-135">All CLI 2.0 commands relating to Azure DNS start with `az network dns`.</span></span> <span data-ttu-id="d4487-136">`--help` 옵션(약식 `-h`)을 사용하여 각 명령에 대한 도움말을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-136">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="d4487-137">예:</span><span class="sxs-lookup"><span data-stu-id="d4487-137">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="d4487-138">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="d4487-138">Create a DNS zone</span></span>

<span data-ttu-id="d4487-139">`az network dns zone create` 명령을 사용하여 DNS 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-139">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="d4487-140">도움말을 보려면 `az network dns zone create -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4487-140">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="d4487-141">다음 예제에서는 *MyResourceGroup*이라는 리소스 그룹에 *contoso.com*이라는 DNS 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-141">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="d4487-142">태그를 사용하여 DNS 영역을 만들려면</span><span class="sxs-lookup"><span data-stu-id="d4487-142">To create a DNS zone with tags</span></span>

<span data-ttu-id="d4487-143">다음 예제에서는 두 [Azure Resource Manager 태그](dns-zones-records.md#tags), *project = demo* 및 *env = test*와 함께 `--tags` 매개 변수(짧은 양식 `-t`)를 사용하여 DNS 영역을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-143">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="d4487-144">DNS 영역 가져오기</span><span class="sxs-lookup"><span data-stu-id="d4487-144">Get a DNS zone</span></span>

<span data-ttu-id="d4487-145">DNS 영역을 가져오려면 `az network dns zone show`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-145">To retrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="d4487-146">도움말을 보려면 `az network dns zone show --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4487-146">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="d4487-147">다음 예제에서는 DNS 영역 *contoso.com* 및 해당 관련 데이터를 리소스 그룹 *MyResourceGroup*에서 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-147">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="d4487-148">다음 예제는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-148">The following example is the response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="d4487-149">DNS 레코드는 `az network dns zone show`에서 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-149">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="d4487-150">DNS 레코드를 나열하려면 `az network dns record-set list`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-150">To list DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="d4487-151">DNS 영역 나열</span><span class="sxs-lookup"><span data-stu-id="d4487-151">List DNS zones</span></span>

<span data-ttu-id="d4487-152">DNS 영역을 열거하려면 `az network dns zone list`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-152">To enumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="d4487-153">도움말을 보려면 `az network dns zone list --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4487-153">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="d4487-154">리소스 그룹을 지정하면 리소스 그룹 내의 해당 영역만 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-154">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="d4487-155">리소스 그룹을 생략하면 구독의 모든 영역이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-155">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="d4487-156">DNS 영역 업데이트</span><span class="sxs-lookup"><span data-stu-id="d4487-156">Update a DNS zone</span></span>

<span data-ttu-id="d4487-157">`az network dns zone update`를 사용하여 DNS 영역 리소스를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-157">Changes to a DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="d4487-158">도움말을 보려면 `az network dns zone update --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4487-158">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="d4487-159">이 명령은 영역 내의 DNS 레코드 집합을 업데이트하지 않습니다([DNS 레코드를 관리하는 방법](dns-operations-recordsets-cli.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="d4487-159">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="d4487-160">영역 리소스 자체의 속성을 업데이트하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-160">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="d4487-161">이러한 속성은 현재 영역 리소스에 대한 [Azure Resource Manager '태그'](dns-zones-records.md#tags)로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-161">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="d4487-162">다음 예제에서는 DNS 영역에서 태그를 업데이트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-162">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="d4487-163">기존 태그는 지정된 값으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-163">The existing tags are replaced by the value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="d4487-164">DNS 영역 삭제</span><span class="sxs-lookup"><span data-stu-id="d4487-164">Delete a DNS zone</span></span>

<span data-ttu-id="d4487-165">`az network dns zone delete`를 사용하여 DNS 영역을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-165">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="d4487-166">도움말을 보려면 `az network dns zone delete --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4487-166">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> <span data-ttu-id="d4487-167">DNS 영역을 삭제하면 영역 내의 모든 DNS 레코드도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-167">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="d4487-168">이 작업은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-168">This operation cannot be undone.</span></span> <span data-ttu-id="d4487-169">DNS 영역을 사용 중인 경우 영역이 삭제되면 영역을 사용하는 서비스가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-169">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="d4487-170">실수로 영역이 삭제되는 것을 방지하려면 [DNS 영역 및 레코드를 보호하는 방법](dns-protect-zones-recordsets.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d4487-170">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>

<span data-ttu-id="d4487-171">이 명령은 확인 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-171">This command prompts for confirmation.</span></span> <span data-ttu-id="d4487-172">선택적 `--yes` 스위치는 이 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-172">The optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="d4487-173">다음 예제는 리소스 그룹 *MyResourceGroup*에서 *contoso.com* 영역을 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-173">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="d4487-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4487-174">Next steps</span></span>

<span data-ttu-id="d4487-175">DNS 영역에서 [레코드 집합 및 레코드 관리](dns-getstarted-create-recordset-cli.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-175">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="d4487-176">[Azure DNS에 도메인을 위임](dns-domain-delegation.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d4487-176">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

