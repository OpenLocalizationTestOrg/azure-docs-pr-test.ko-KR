---
title: "Azure DNS에서 DNS 영역 관리 - PowerShell | Microsoft Docs"
description: "Azure Powershell을 사용하여 DNS 영역을 관리할 수 있습니다. 이 문서에서는 Azure DNS에서 DNS 영역을 업데이트, 삭제 및 만드는 방법을 설명합니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 92f1da660d875c76d5d826669d6c1d12018c3d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-using-powershell"></a><span data-ttu-id="4f7bb-104">PowerShell을 사용하여 DNS 영역을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="4f7bb-104">How to manage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f7bb-105">포털</span><span class="sxs-lookup"><span data-stu-id="4f7bb-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="4f7bb-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f7bb-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="4f7bb-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4f7bb-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="4f7bb-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4f7bb-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="4f7bb-109">이 문서는 Azure PowerShell을 사용하여 DNS 영역을 관리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-109">This article shows you how to manage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="4f7bb-110">플랫폼 간 [Azure CLI](dns-operations-dnszones-cli.md) 또는 Azure Portal을 사용하여 DNS 영역을 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="4f7bb-111">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="4f7bb-111">Create a DNS zone</span></span>

<span data-ttu-id="4f7bb-112">DNS 영역은 `New-AzureRmDnsZone` cmdlet을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-112">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="4f7bb-113">다음 예제에서는 *MyResourceGroup*이라는 리소스 그룹에 *contoso.com*이라는 DNS 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-113">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="4f7bb-114">다음 예제에서는 두 [Azure Resource Manager 태그](dns-zones-records.md#tags), *project = demo* 및 *env = test*를 사용하여 DNS 영역을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-114">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="4f7bb-115">DNS 영역 가져오기</span><span class="sxs-lookup"><span data-stu-id="4f7bb-115">Get a DNS zone</span></span>

<span data-ttu-id="4f7bb-116">DNS 영역을 가져오려면 `Get-AzureRmDnsZone` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-116">To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="4f7bb-117">이 작업은 Azure DNS의 기존 영역에 해당하는 DNS 영역 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-117">This operation returns a DNS zone object corresponding to an existing zone in Azure DNS.</span></span> <span data-ttu-id="4f7bb-118">이 개체는 영역에 대한 데이터(예: 레코드 집합 수)를 포함하지만 레코드 집합 자체는 포함하지 않습니다(`Get-AzureRmDnsRecordSet` 참조).</span><span class="sxs-lookup"><span data-stu-id="4f7bb-118">The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a><span data-ttu-id="4f7bb-119">DNS 영역 나열</span><span class="sxs-lookup"><span data-stu-id="4f7bb-119">List DNS zones</span></span>

<span data-ttu-id="4f7bb-120">`Get-AzureRmDnsZone`에서 영역 이름을 생략하면, 리소스 그룹의 모든 영역을 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-120">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="4f7bb-121">이 작업은 영역 개체의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="4f7bb-122">`Get-AzureRmDnsZone`에서 영역 이름 및 리소스 그룹 이름을 모두 생략하여 Azure 구독의 모든 영역을 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-122">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="4f7bb-123">DNS 영역 업데이트</span><span class="sxs-lookup"><span data-stu-id="4f7bb-123">Update a DNS zone</span></span>

<span data-ttu-id="4f7bb-124">`Set-AzureRmDnsZone`를 사용하여 DNS 영역 리소스를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-124">Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="4f7bb-125">이 cmdlet은 영역 내의 DNS 레코드 집합을 업데이트하지 않습니다([DNS 레코드를 관리하는 방법](dns-operations-recordsets.md)참조).</span><span class="sxs-lookup"><span data-stu-id="4f7bb-125">This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="4f7bb-126">영역 리소스 자체의 속성을 업데이트하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-126">It's only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="4f7bb-127">이러한 쓰기 가능 영역 속성은 현재 [영역 리소스에 대한 Azure Resource Manager '태그'](dns-zones-records.md#tags)로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-127">The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="4f7bb-128">다음 두 가지 방법 중 하나를 사용하여 DNS 영역을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-128">Use one of the following two ways to update a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a><span data-ttu-id="4f7bb-129">영역 이름 및 리소스 그룹을 사용하여 영역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-129">Specify the zone using the zone name and resource group</span></span>

<span data-ttu-id="4f7bb-130">이 접근 방법은 기존 영역 태그를 지정된 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-130">This approach replaces the existing zone tags with the values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="4f7bb-131">$zone 개체를 사용하여 영역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-131">Specify the zone using a $zone object</span></span>

<span data-ttu-id="4f7bb-132">이 방법은 기존 영역 개체를 검색하고, 태그를 수정한 다음, 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-132">This approach retrieves the existing zone object, modifies the tags, and then commits the changes.</span></span> <span data-ttu-id="4f7bb-133">이러한 방식으로 기존 태그를 보존할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="4f7bb-134">$zone 개체와 함께 `Set-AzureRmDnsZone`을 사용하는 경우 동시 변경 내용을 덮어쓰지 않도록 [Etag 검사](dns-zones-records.md#etags)가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="4f7bb-135">선택적 `-Overwrite` 스위치를 사용하여 이러한 검사를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-135">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="4f7bb-136">DNS 영역 삭제</span><span class="sxs-lookup"><span data-stu-id="4f7bb-136">Delete a DNS Zone</span></span>

<span data-ttu-id="4f7bb-137">`Remove-AzureRmDnsZone` cmdlet을 사용하여 DNS 영역을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-137">DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="4f7bb-138">DNS 영역을 삭제하면 영역 내의 모든 DNS 레코드도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-138">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="4f7bb-139">이 작업은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-139">This operation cannot be undone.</span></span> <span data-ttu-id="4f7bb-140">DNS 영역을 사용 중인 경우 영역이 삭제되면 영역을 사용하는 서비스가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-140">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="4f7bb-141">실수로 영역이 삭제되는 것을 방지하려면 [DNS 영역 및 레코드를 보호하는 방법](dns-protect-zones-recordsets.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-141">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="4f7bb-142">다음 두 가지 방법 중 하나를 사용하여 DNS 영역을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-142">Use one of the following two ways to delete a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a><span data-ttu-id="4f7bb-143">영역 이름 및 리소스 그룹 이름을 사용하여 영역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-143">Specify the zone using the zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="4f7bb-144">$zone 개체를 사용하여 영역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-144">Specify the zone using a $zone object</span></span>

<span data-ttu-id="4f7bb-145">`Get-AzureRmDnsZone`에서 반환된 `$zone` 개체를 사용하여 삭제될 영역을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-145">You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="4f7bb-146">영역 개체를 매개 변수로 전달하는 대신 파이프할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-146">The zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="4f7bb-147">`Set-AzureRmDnsZone`과 마찬가지로, `$zone` 개체를 사용하여 영역을 지정하면 동시 변경 내용을 삭제하지 않도록 Etag 검사가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-147">As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="4f7bb-148">이러한 검사를 무시하려면 `-Overwrite` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-148">Use the `-Overwrite` switch to suppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="4f7bb-149">확인 메시지 표시</span><span class="sxs-lookup"><span data-stu-id="4f7bb-149">Confirmation prompts</span></span>

<span data-ttu-id="4f7bb-150">`New-AzureRmDnsZone`, `Set-AzureRmDnsZone` 및 `Remove-AzureRmDnsZone` cmdlet은 모두 확인 메시지를 표시하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-150">The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="4f7bb-151">`$ConfirmPreference` PowerShell 기본 설정 변수 값에 `Medium` 이하의 값이 있는 경우 `New-AzureRmDnsZone` 및 `Set-AzureRmDnsZone`은 확인 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="4f7bb-152">DNS 영역을 삭제할 경우 미치는 영향이 클 수 있으므로 `Remove-AzureRmDnsZone` cmdlet은 `$ConfirmPreference` PowerShell 변수가 `None` 이외의 값을 갖는 경우 확인 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-152">Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="4f7bb-153">`$ConfirmPreference`의 기본값은 `High`이므로 `Remove-AzureRmDnsZone`는 기본적으로 확인 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-153">Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="4f7bb-154">`-Confirm` 매개 변수를 사용하여 현재 `$ConfirmPreference` 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-154">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="4f7bb-155">`-Confirm` 또는 `-Confirm:$True`를 지정하는 경우 cmdlet은 실행하기 전에 확인을 위한 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-155">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="4f7bb-156">`-Confirm:$False`을 지정하는 경우 cmdlet은 확인을 위한 메시지를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-156">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="4f7bb-157">`-Confirm` 및 `$ConfirmPreference`에 대한 자세한 내용은 [기본 설정 변수 정보](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f7bb-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f7bb-158">Next steps</span></span>

<span data-ttu-id="4f7bb-159">DNS 영역에서 [레코드 집합 및 레코드 관리](dns-operations-recordsets.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-159">Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="4f7bb-160">[Azure DNS에 도메인을 위임](dns-domain-delegation.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-160">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="4f7bb-161">[Azure DNS PowerShell 참조 설명서](/powershell/module/azurerm.dns)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="4f7bb-161">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

