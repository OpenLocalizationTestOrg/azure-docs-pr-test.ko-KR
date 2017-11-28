---
title: "Azure DNS-PowerShell에서에서 aaaManage DNS 영역 | Microsoft Docs"
description: "Azure Powershell을 사용하여 DNS 영역을 관리할 수 있습니다. 이 문서에서는 tooupdate, 삭제 하 고 dns를 Azure DNS 영역을 만드는 방법을 설명합니다"
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
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a><span data-ttu-id="4cc38-104">어떻게 PowerShell을 사용 하 여 toomanage DNS 영역</span><span class="sxs-lookup"><span data-stu-id="4cc38-104">How toomanage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4cc38-105">포털</span><span class="sxs-lookup"><span data-stu-id="4cc38-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="4cc38-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cc38-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="4cc38-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4cc38-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="4cc38-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4cc38-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="4cc38-109">이 문서에서는 어떻게 toomanage DNS 영역을 Azure PowerShell을 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-109">This article shows you how toomanage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="4cc38-110">플랫폼 간 hello를 사용 하 여 DNS 영역을 관리할 수 있습니다 [Azure CLI](dns-operations-dnszones-cli.md) 또는 Azure 포털을 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="4cc38-111">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="4cc38-111">Create a DNS zone</span></span>

<span data-ttu-id="4cc38-112">Hello를 사용 하 여 DNS 영역이 만들어집니다 `New-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cc38-112">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="4cc38-113">hello 다음 예제에서는 호출 하는 DNS 영역 *contoso.com* 호출 hello 리소스 그룹에 *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="4cc38-113">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="4cc38-114">hello 다음 예제에서는 두 개의 toocreate DNS 영역 방법을 [Azure 리소스 관리자 태그](dns-zones-records.md#tags), *프로젝트 데모 =* 및 *env = 테스트*:</span><span class="sxs-lookup"><span data-stu-id="4cc38-114">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="4cc38-115">DNS 영역 가져오기</span><span class="sxs-lookup"><span data-stu-id="4cc38-115">Get a DNS zone</span></span>

<span data-ttu-id="4cc38-116">tooretrieve DNS 영역을 사용 하 여 hello `Get-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cc38-116">tooretrieve a DNS zone, use hello `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="4cc38-117">이 작업을 DNS 개체 해당 tooan 기존 영역에 Azure DNS 영역을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-117">This operation returns a DNS zone object corresponding tooan existing zone in Azure DNS.</span></span> <span data-ttu-id="4cc38-118">hello 개체 (예: hello 레코드 집합 수), hello 영역에 대 한 데이터를 포함 하지만 포함 하지 않는 자체 hello 레코드 집합 (참조 `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="4cc38-118">hello object contains data about hello zone (such as hello number of record sets), but does not contain hello record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

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

## <a name="list-dns-zones"></a><span data-ttu-id="4cc38-119">DNS 영역 나열</span><span class="sxs-lookup"><span data-stu-id="4cc38-119">List DNS zones</span></span>

<span data-ttu-id="4cc38-120">Hello 영역 이름에서 생략 하 여 `Get-AzureRmDnsZone`, 리소스 그룹의 모든 영역을 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-120">By omitting hello zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="4cc38-121">이 작업은 영역 개체의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="4cc38-122">Hello 영역 이름 및 hello 리소스 그룹 이름을 모두 생략 하 여 `Get-AzureRmDnsZone`, hello Azure 구독에 있는 모든 영역을 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-122">By omitting both hello zone name and hello resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in hello Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="4cc38-123">DNS 영역 업데이트</span><span class="sxs-lookup"><span data-stu-id="4cc38-123">Update a DNS zone</span></span>

<span data-ttu-id="4cc38-124">DNS 영역 리소스를 사용 하 여 만들어질 수 tooa 변경 `Set-AzureRmDnsZone`합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-124">Changes tooa DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="4cc38-125">이 cmdlet hello hello 영역 내에서 DNS 레코드 집합 중 하나를 업데이트 하지 않습니다 (참조 [어떻게 tooManage DNS 레코드](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="4cc38-125">This cmdlet does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="4cc38-126">것에 hello 영역 리소스 자체의 tooupdate 속성 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-126">It's only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="4cc38-127">hello 쓰기 가능한 영역 속성은 현재 제한 toohello [hello 영역의 리소스에 대 한 '태그' Azure 리소스 관리자](dns-zones-records.md#tags)합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-127">hello writable zone properties are currently limited toohello [Azure Resource Manager ‘tags’ for hello zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="4cc38-128">다음 두 가지 방법으로 tooupdate hello 중 DNS 영역을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-128">Use one of hello following two ways tooupdate a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a><span data-ttu-id="4cc38-129">영역 이름 및 리소스 그룹 hello를 사용 하 여 hello 영역 지정</span><span class="sxs-lookup"><span data-stu-id="4cc38-129">Specify hello zone using hello zone name and resource group</span></span>

<span data-ttu-id="4cc38-130">이 방법은 지정 된 hello 값으로 기존 영역 태그 hello를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-130">This approach replaces hello existing zone tags with hello values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="4cc38-131">$Zone 개체를 사용 하 여 hello 영역 지정</span><span class="sxs-lookup"><span data-stu-id="4cc38-131">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="4cc38-132">이 방법은 hello 기존 영역 개체를 검색 하 고 hello 태그를 수정 다음 hello 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-132">This approach retrieves hello existing zone object, modifies hello tags, and then commits hello changes.</span></span> <span data-ttu-id="4cc38-133">이러한 방식으로 기존 태그를 보존할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="4cc38-134">사용 하는 경우 `Set-AzureRmDnsZone` $zone 개체와 [Etag 검사](dns-zones-records.md#etags) 사용 tooensure 동시 변경 내용을 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="4cc38-135">Hello 옵션을 사용할 수 있습니다 `-Overwrite` toosuppress 이러한 검사를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-135">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="4cc38-136">DNS 영역 삭제</span><span class="sxs-lookup"><span data-stu-id="4cc38-136">Delete a DNS Zone</span></span>

<span data-ttu-id="4cc38-137">Hello를 사용 하 여 DNS 영역을 삭제할 수 있습니다 `Remove-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4cc38-137">DNS zones can be deleted using hello `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="4cc38-138">DNS 영역을 삭제 하면 모든 DNS 레코드가 hello 영역 내에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-138">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="4cc38-139">이 작업은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-139">This operation cannot be undone.</span></span> <span data-ttu-id="4cc38-140">DNS 영역 hello를 사용 하는 경우 hello 영역이 삭제 되 면 hello 영역을 사용 하 여 서비스 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-140">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="4cc38-141">실수로 영역 삭제 tooprotect 참조 [tooprotect DNS 영역 및 기록 방법을](dns-protect-zones-recordsets.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-141">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="4cc38-142">다음 두 가지 방법으로 toodelete hello 중 DNS 영역을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-142">Use one of hello following two ways toodelete a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a><span data-ttu-id="4cc38-143">Hello 영역 이름 및 리소스 그룹 이름을 사용 하 여 hello 영역 지정</span><span class="sxs-lookup"><span data-stu-id="4cc38-143">Specify hello zone using hello zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="4cc38-144">$Zone 개체를 사용 하 여 hello 영역 지정</span><span class="sxs-lookup"><span data-stu-id="4cc38-144">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="4cc38-145">Hello 영역 toobe 사용 하 여 삭제를 지정할 수는 `$zone` 에서 반환 된 개체 `Get-AzureRmDnsZone`합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-145">You can specify hello zone toobe deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="4cc38-146">hello 영역 개체를 매개 변수로 전달 되는 대신도 파이프 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-146">hello zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="4cc38-147">와 마찬가지로 `Set-AzureRmDnsZone`, 영역을 사용 하 여 hello를 지정 하는 `$zone` 개체 Etag 검사 tooensure 동시 변경 내용을 삭제 되지 않습니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-147">As with `Set-AzureRmDnsZone`, specifying hello zone using a `$zone` object enables Etag checks tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="4cc38-148">사용 하 여 hello `-Overwrite` toosuppress 이러한 검사를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-148">Use hello `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="4cc38-149">확인 메시지 표시</span><span class="sxs-lookup"><span data-stu-id="4cc38-149">Confirmation prompts</span></span>

<span data-ttu-id="4cc38-150">hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, 및 `Remove-AzureRmDnsZone` cmdlet 모든 확인 메시지를 표시를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-150">hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="4cc38-151">둘 다 `New-AzureRmDnsZone` 및 `Set-AzureRmDnsZone` 확인 메시지를 표시 하는 경우 hello `$ConfirmPreference` PowerShell 기본 설정 변수 값은 `Medium` 이하로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="4cc38-152">삭제할 경우의 DNS 영역 hello toohello 잠재적으로 높은 영향 인해 `Remove-AzureRmDnsZone` cmdlet 확인 메시지를 표시 하는 경우 hello `$ConfirmPreference` PowerShell 변수 이외의 모든 값을 가지 `None`합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-152">Due toohello potentially high impact of deleting a DNS zone, hello `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="4cc38-153">Hello 기본값에 대 한 이후 `$ConfirmPreference` 은 `High`만 `Remove-AzureRmDnsZone` 확인 기본적으로 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-153">Since hello default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="4cc38-154">Hello 현재 문자인 `$ConfirmPreference` hello를 사용 하 여 설정을 `-Confirm` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-154">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="4cc38-155">지정 하는 경우 `-Confirm` 또는 `-Confirm:$True` , hello cmdlet 확인 메시지가 표시 되기 전에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-155">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="4cc38-156">지정 하는 경우 `-Confirm:$False` , hello cmdlet 표시 하지 않습니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-156">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="4cc38-157">`-Confirm` 및 `$ConfirmPreference`에 대한 자세한 내용은 [기본 설정 변수 정보](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4cc38-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cc38-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4cc38-158">Next steps</span></span>

<span data-ttu-id="4cc38-159">너무 방법에 대해 알아봅니다[레코드 집합 및 레코드 관리](dns-operations-recordsets.md) DNS 영역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-159">Learn how too[manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="4cc38-160">너무 방법에 대해 알아봅니다[사용자 도메인 tooAzure DNS 위임](dns-domain-delegation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-160">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="4cc38-161">검토 hello [Azure DNS PowerShell 참조 설명서](/powershell/module/azurerm.dns)합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc38-161">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

