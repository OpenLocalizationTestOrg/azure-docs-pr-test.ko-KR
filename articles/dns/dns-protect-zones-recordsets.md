---
title: "aaaProtecting DNS 영역과 레코드 | Microsoft Docs"
description: "어떻게 tooprotect DNS 영역과 레코드 Microsoft Azure DNS에서 설정 합니다."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a><span data-ttu-id="c530d-103">어떻게 tooprotect DNS 영역 및 기록</span><span class="sxs-lookup"><span data-stu-id="c530d-103">How tooprotect DNS zones and records</span></span>

<span data-ttu-id="c530d-104">DNS 영역 및 레코드는 중요한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="c530d-105">DNS 영역 또는 단일 DNS 레코드만 삭제해도 전체 서비스 중단이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="c530d-106">따라서 중요 DNS 영역 및 레코드가 무단 또는 실수로 변경되지 않도록 보호하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="c530d-107">이 문서에서는 DNS 영역과 레코드 이러한 변경에 대해 Azure DNS tooprotect 있습니다를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-107">This article explains how Azure DNS enables you tooprotect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="c530d-108">Azure Resource Manager에서 제공하는 두 가지 강력한 보안 기능, 즉, [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md)와 [리소스 잠금](../azure-resource-manager/resource-group-lock-resources.md)을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="c530d-109">역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="c530d-109">Role-based access control</span></span>

<span data-ttu-id="c530d-110">Azure RBAC(Role-Based Access Control)는 Azure 사용자, 그룹, 리소스에 대해 정확한 액세스 관리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="c530d-111">RBAC를 사용 하 여 정확 하 게 hello 제한 된 액세스를 부여할 구성할 수 사용자에 게 필요 업무 tooperform을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-111">Using RBAC, you can grant precisely hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="c530d-112">RBAC를 사용하여 액세스를 관리하는 방법에 대한 자세한 내용은 [역할 기반 액세스 제어란](../active-directory/role-based-access-control-what-is.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c530d-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="hello-dns-zone-contributor-role"></a><span data-ttu-id="c530d-113">hello ' DNS 영역 참가자 ' 역할</span><span class="sxs-lookup"><span data-stu-id="c530d-113">hello 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="c530d-114">hello ' DNS 영역 참가자 ' 역할은 DNS 리소스 관리를 위해 Azure에서 제공 하는 기본 제공 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-114">hello 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="c530d-115">DNS 영역 참가자 사용 권한 tooa 사용자 또는 그룹을 지정 해당 그룹 toomanage DNS 리소스 하지만 다른 형식의 리소스가 아닌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-115">Assigning DNS Zone Contributor permissions tooa user or group enables that group toomanage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="c530d-116">예를 들어, myzones' hello 리소스 그룹' Contoso Corporation에 대 한 다섯 가지 영역이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-116">For example, suppose hello resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="c530d-117">부여 hello DNS 관리자 ' DNS 영역 참가자 ' 권한을 toothat 리소스 그룹을 해당 DNS 영역을 완전히 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-117">Granting hello DNS administrator 'DNS Zone Contributor' permissions toothat resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="c530d-118">예를 들어 DNS 관리자에 게 가상 컴퓨터를 중지 또는 만들 수 없습니다 불필요 한 사용 권한을 부여 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-118">It also avoids granting unnecessary permissions, for example hello DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="c530d-119">hello 가장 간단한 방법은 tooassign RBAC 권한은 [hello Azure 포털을 통해](../active-directory/role-based-access-control-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-119">hello simplest way tooassign RBAC permissions is [via hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="c530d-120">Hello 리소스 그룹에 대 한 hello '액세스 제어 (IAM)' 블레이드를 여세요 'Add'를 클릭 한 다음 hello ' DNS 영역 참가자 ' 역할 및 필요한 선택 hello 사용자 또는 그룹 toogrant 사용 권한을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-120">Open hello 'Access control (IAM)' blade for hello resource group, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Hello Azure 포털을 통해 리소스 그룹 수준 RBAC](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="c530d-122">권한은 [Azure PowerShell을 사용하여 부여](../active-directory/role-based-access-control-manage-access-powershell.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="c530d-123">hello 이와 동등한 명령을 이기도 [hello Azure CLI를 통해 사용할 수 있는](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="c530d-123">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="c530d-124">영역 수준 RBAC</span><span class="sxs-lookup"><span data-stu-id="c530d-124">Zone level RBAC</span></span>

<span data-ttu-id="c530d-125">Azure RBAC 규칙이 적용 된 tooa 구독 수는 리소스 그룹 또는 tooan 개별 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-125">Azure RBAC rules can be applied tooa subscription, a resource group or tooan individual resource.</span></span> <span data-ttu-id="c530d-126">Azure DNS의 hello 경우에서 해당 리소스는 개별 DNS 영역 또는 개별 레코드 집합도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-126">In hello case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="c530d-127">예를 들어 myzones' hello 리소스 그룹' contoso.com' hello 영역' 및 각 고객 계정에 대해 CNAME 레코드 만들어집니다 하는 subzone 지 대 'customers.contoso.com'를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-127">For example, suppose hello resource group 'myzones' contains hello zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="c530d-128">hello 사용 되는 계정 toomanage이 CNAME 레코드 할당할 hello 'customers.contoso.com' 영역에만 사용 권한을 toocreate 레코드, 없어야 액세스 toohello 다른 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-128">hello account used toomanage these CNAME records should be assigned permissions toocreate records in hello 'customers.contoso.com' zone only, it should not have access toohello other zones.</span></span>

<span data-ttu-id="c530d-129">Hello Azure 포털을 통해 영역 수준 RBAC 사용 권한은 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-129">Zone-level RBAC permissions can be granted via hello Azure portal.</span></span>  <span data-ttu-id="c530d-130">Hello 영역에 대 한 hello '액세스 제어 (IAM)' 블레이드를 여세요 'Add'를 클릭 한 다음 hello ' DNS 영역 참가자 ' 역할 및 필요한 선택 hello 사용자 또는 그룹 toogrant 사용 권한을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-130">Open hello 'Access control (IAM)' blade for hello zone, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Hello Azure 포털을 통해 DNS 영역 수준 RBAC](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="c530d-132">권한은 [Azure PowerShell을 사용하여 부여](../active-directory/role-based-access-control-manage-access-powershell.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="c530d-133">hello 이와 동등한 명령을 이기도 [hello Azure CLI를 통해 사용할 수 있는](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="c530d-133">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="c530d-134">레코드 집합 수준 RBAC</span><span class="sxs-lookup"><span data-stu-id="c530d-134">Record set level RBAC</span></span>

<span data-ttu-id="c530d-135">한 단계 더 나아갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-135">We can go one step further.</span></span> <span data-ttu-id="c530d-136">메일 관리자를 게 Contoso Corporation에 대 한 액세스 toohello MX 및 hello 구로 hello '만든 contoso.com' 영역에 TXT 레코드를 필요로 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-136">Consider hello mail administrator for Contoso Corporation, who needs access toohello MX and TXT records at hello apex of hello 'contoso.com' zone.</span></span>  <span data-ttu-id="c530d-137">그녀 다른 TXT 또는 MX 레코드 또는 다른 종류의 tooany 레코드 tooany 액세스할 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-137">She doesn't need access tooany other MX or TXT records, or tooany records of any other type.</span></span>  <span data-ttu-id="c530d-138">Azure DNS에 액세스 해야 하면 hello 레코드 집합 수준 tooprecisely hello 레코드를 메일 관리자 hello에서 tooassign 사용 권한을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-138">Azure DNS allows you tooassign permissions at hello record set level, tooprecisely hello records that hello mail administrator needs access to.</span></span>  <span data-ttu-id="c530d-139">hello 메일 관리자가 권한이 정확 하 게 hello, 그녀가 고 toomake 수 없습니다 다른 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-139">hello mail administrator is granted precisely hello control she needs, and is unable toomake any other changes.</span></span>

<span data-ttu-id="c530d-140">레코드 집합 수준 RBAC 사용 권한은 hello hello 레코드 집합 블레이드에서 hello '사용자' 단추를 사용 하 여 Azure 포털을 통해 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-140">Record-set level RBAC permissions can be configured via hello Azure portal, using hello 'Users' button in hello record set blade:</span></span>

![레코드는 hello Azure 포털을 통해 RBAC 수준 설정](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="c530d-142">레코드 집합 수준 RBAC 권한은 [Azure PowerShell을 사용하여 부여](../active-directory/role-based-access-control-manage-access-powershell.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="c530d-143">hello 이와 동등한 명령을 이기도 [hello Azure CLI를 통해 사용할 수 있는](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="c530d-143">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="c530d-144">사용자 지정 역할</span><span class="sxs-lookup"><span data-stu-id="c530d-144">Custom roles</span></span>

<span data-ttu-id="c530d-145">hello 기본 제공 ' DNS 영역 참가자 ' 역할에 DNS 리소스를 완전히 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-145">hello built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="c530d-146">그는 또한 가능한 toobuild 고유한 고객 Azure 역할, tooprovide도 세부적인 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-146">It is also possible toobuild your own customer Azure roles, tooprovide even finer-grained control.</span></span>

<span data-ttu-id="c530d-147">다시 각 Contoso Corporation 고객 계정에 대해 customers.contoso.com' hello 영역'에서 CNAME 레코드를 작성 하는 hello 예제를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c530d-147">Consider again hello example in which a CNAME record in hello zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="c530d-148">hello 사용 되는 계정 toomanage 이러한 CNAMEs 사용 권한 toomanage CNAME 레코드가 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-148">hello account used toomanage these CNAMEs should be granted permission toomanage CNAME records only.</span></span>  <span data-ttu-id="c530d-149">되기 없습니다 toomodify 레코드의 다른 유형 (예: MX 레코드를 변경) 또는 영역 수준 작업 영역 삭제 등을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-149">It is then unable toomodify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="c530d-150">다음 예제는 hello만 CNAME 레코드를 관리 하기 위한 사용자 지정 역할 정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-150">hello following example shows a custom role definition for managing CNAME records only:</span></span>

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

<span data-ttu-id="c530d-151">작업 속성 hello hello 다음 DNS 특정 권한을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-151">hello Actions property defines hello following DNS-specific permissions:</span></span>

* <span data-ttu-id="c530d-152">`Microsoft.Network/dnsZones/CNAME/*`은 CNAME 레코드에 대한 모든 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="c530d-153">`Microsoft.Network/dnsZones/read`사용 권한 tooread DNS 영역을 하지만 toosee 있습니다를 사용 하도록 설정 하는 hello CNAME 생성 되는 영역을 hello toomodify 하지 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-153">`Microsoft.Network/dnsZones/read` grants permission tooread DNS zones, but not toomodify them, enabling you toosee hello zone in which hello CNAME is being created.</span></span>

<span data-ttu-id="c530d-154">남은 동작이 hello에서 복사 되는 hello [DNS 영역 참가자 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor)합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-154">hello remaining Actions are copied from hello [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="c530d-155">레코드를 삭제 하는 사용자 지정 RBAC 역할 tooprevent를 사용 하 여 효과적인 컨트롤이 아닙니다 여전히 toobe 업데이트 허용 하는 동안 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-155">Using a custom RBAC role tooprevent deleting record sets while still allowing them toobe updated is not an effective control.</span></span> <span data-ttu-id="c530d-156">이 방식에서는 레코드 집합을 삭제할 수 없지만 수정은 방지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="c530d-157">허용 된 수정 추가 등 tooleave '빈' 레코드 집합 기록 모든 제거 포함 hello 레코드 집합에서 레코드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-157">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="c530d-158">이 hello DNS 확인 관점에서 설정 hello 레코드를 삭제 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-158">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="c530d-159">사용자 지정 역할 정의 현재 hello Azure 포털을 통해 정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-159">Custom role definitions cannot currently be defined via hello Azure portal.</span></span> <span data-ttu-id="c530d-160">이 역할 정의를 기준으로 하는 사용자 지정 역할은 Azure PowerShell을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="c530d-161">Hello Azure CLI를 통해 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-161">It can also be created via hello Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="c530d-162">hello 역할 그런 다음 할당할 수 있습니다 hello에서 동일한 방식으로 기본 제공 역할으로이 문서의 앞부분에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-162">hello role can then be assigned in hello same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="c530d-163">Toocreate를 관리 하 고 사용자 지정 역할을 할당 하는 방법에 대 한 자세한 내용은 참조 [사용자 정의 역할에서 Azure RBAC](../active-directory/role-based-access-control-custom-roles.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-163">For more information on how toocreate, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="c530d-164">리소스 잠금</span><span class="sxs-lookup"><span data-stu-id="c530d-164">Resource locks</span></span>

<span data-ttu-id="c530d-165">또한 tooRBAC Azure 리소스 관리자 지원 다른 유형의 보안 제어, 즉 hello 기능 too'lock' 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-165">In addition tooRBAC, Azure Resource Manager supports another type of security control, namely hello ability too'lock' resources.</span></span> <span data-ttu-id="c530d-166">RBAC 규칙을 사용 하면 특정 사용자 및 그룹의 toocontrol hello 동작, 여기서 리소스 잠금이 적용된 toohello 리소스 되며 모든 사용자 및 역할에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-166">Where RBAC rules allow you toocontrol hello actions of specific users and groups, resource locks are applied toohello resource, and are effective across all users and roles.</span></span> <span data-ttu-id="c530d-167">자세한 내용은 [Azure 리소스 관리자를 사용하여 리소스 잠그기](../azure-resource-manager/resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c530d-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="c530d-168">리소스 잠금은 **DoNotDelete** 및 **ReadOnly**의 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="c530d-169">적용할 수 있습니다 이러한 tooa DNS 영역 또는 tooan 개별 레코드 집합 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-169">These can be applied either tooa DNS zone, or tooan individual record set.</span></span>  <span data-ttu-id="c530d-170">hello 다음 섹션에서는 설명 몇 가지 일반적인 시나리오와 방법을 toosupport 리소스 잠금을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-170">hello following sections describe several common scenarios, and how toosupport them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="c530d-171">모든 변경으로부터 보호</span><span class="sxs-lookup"><span data-stu-id="c530d-171">Protecting against all changes</span></span>

<span data-ttu-id="c530d-172">tooprevent 되 고 변경 ReadOnly 잠금 toohello 영역을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-172">tooprevent any changes being made, apply a ReadOnly lock toohello zone.</span></span>  <span data-ttu-id="c530d-173">이 경우 새 레코드 집합을 만들 수 없으며 기존 레코드 집합이 수정 또는 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="c530d-174">영역 수준 리소스 잠금은 hello Azure 포털을 통해 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-174">Zone level resource locks can be created via hello Azure portal.</span></span>  <span data-ttu-id="c530d-175">Hello DNS 영역 블레이드에서 'Locks'를 클릭 한 다음 'Add':</span><span class="sxs-lookup"><span data-stu-id="c530d-175">From hello DNS zone blade, click 'Locks', then 'Add':</span></span>

![영역 수준 리소스 잠금을 hello Azure 포털을 통해](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="c530d-177">또한 Azure PowerShell을 통해 영역 수준 리소스 잠금을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="c530d-178">현재 Azure CLI hello를 통해 Azure 리소스 잠금을 구성 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-178">Configuring Azure resource locks is not currently supported via hello Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="c530d-179">개별 레코드 보호</span><span class="sxs-lookup"><span data-stu-id="c530d-179">Protecting individual records</span></span>

<span data-ttu-id="c530d-180">tooprevent 설정 수정에 대 한 기존 DNS 레코드 ReadOnly 잠금 toohello 레코드 집합을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-180">tooprevent an existing DNS record set against modification, apply a ReadOnly lock toohello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="c530d-181">DoNotDelete 잠금 tooa 적용 레코드 집합은 효과적인 컨트롤이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-181">Applying a DoNotDelete lock tooa record set is not an effective control.</span></span> <span data-ttu-id="c530d-182">Hello 레코드 삭제 되지 않도록 설정 하는 것을 방지 하지만 중단 되지는 않습니다 것 수정 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-182">It prevents hello record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="c530d-183">허용 된 수정 추가 등 tooleave '빈' 레코드 집합 기록 모든 제거 포함 hello 레코드 집합에서 레코드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-183">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="c530d-184">이 hello DNS 확인 관점에서 설정 hello 레코드를 삭제 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-184">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="c530d-185">레코드 집합 수준 리소스 잠금은 현재 Azure PowerShell을 사용해야 구성할 수 있으며</span><span class="sxs-lookup"><span data-stu-id="c530d-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="c530d-186">Hello Azure 포털 또는 Azure CLI에는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-186">They are not supported in hello Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="c530d-187">영역 삭제로부터 보호</span><span class="sxs-lookup"><span data-stu-id="c530d-187">Protecting against zone deletion</span></span>

<span data-ttu-id="c530d-188">Azure dns에서 영역 삭제 되 면 hello 영역의 모든 레코드 집합 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-188">When a zone is deleted in Azure DNS, all record sets in hello zone are also deleted.</span></span>  <span data-ttu-id="c530d-189">이 작업은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-189">This operation cannot be undone.</span></span>  <span data-ttu-id="c530d-190">중요 한 영역을 실수로 삭제에 hello 잠재적인 toohave 중요 한 비즈니스 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-190">Accidentally deleting a critical zone has hello potential toohave a significant business impact.</span></span>  <span data-ttu-id="c530d-191">따라서 실수로 영역 삭제에 대 한 매우 중요 한 tooprotect 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-191">It is therefore very important tooprotect against accidental zone deletion.</span></span>

<span data-ttu-id="c530d-192">Hello 영역 삭제 되지 않도록 방지 DoNotDelete 잠금 tooa 영역을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-192">Applying a DoNotDelete lock tooa zone prevents hello zone from being deleted.</span></span>  <span data-ttu-id="c530d-193">그러나 잠금이 자식 리소스 상속, 이후 또한 hello 영역에서 삭제 되지 않도록 적절 하지 않을 모든 레코드 집합 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-193">However, since locks are inherited by child resources, it also prevents any record sets in hello zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="c530d-194">또한 위의 hello 참고에 설명 된 때 하지도 효과적 hello 기존 레코드 집합에서 여전히 레코드를 제거할 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-194">Furthermore, as described in hello note above, it is also ineffective since records can still be removed from hello existing record sets.</span></span>

<span data-ttu-id="c530d-195">대신, 예: hello SOA 레코드 집합 hello 시간대에서 설정 DoNotDelete 잠금 tooa 레코드를 적용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-195">As an alternative, consider applying a DoNotDelete lock tooa record set in hello zone, such as hello SOA record set.</span></span>  <span data-ttu-id="c530d-196">Hello 영역도 hello 레코드 집합을 삭제 하지 않고 삭제할 수 있으므로이 방지 자유롭게 수정할 hello 영역 toobe 내의 레코드 집합 허용 하면서 영역 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-196">Since hello zone cannot be deleted without also deleting hello record sets, this protects against zone deletion, while still allowing record sets within hello zone toobe modified freely.</span></span> <span data-ttu-id="c530d-197">Toodelete hello 영역, 하려고 시도 하는 경우 Azure 리소스 관리자 hello SOA 레코드 집합 삭제는이 및 SOA hello 잠겨 있기 때문에 블록 hello 호출을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-197">If an attempt is made toodelete hello zone, Azure Resource Manager detects this would also delete hello SOA record set, and blocks hello call because hello SOA is locked.</span></span>  <span data-ttu-id="c530d-198">삭제되는 레코드 집합이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-198">No record sets are deleted.</span></span>

<span data-ttu-id="c530d-199">다음 PowerShell 명령을 hello hello SOA 레코드의 영역을 제공 하는 hello에 대 한 DoNotDelete 잠금을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-199">hello following PowerShell command creates a DoNotDelete lock against hello SOA record of hello given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="c530d-200">또 다른 방법은 tooprevent 실수로 영역 삭제 하는 영역을 영역가 않는 사용자 지정 역할 tooensure hello 연산자 및 서비스 사용 되는 계정 toomanage 사용 하 여 사용 권한을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-200">Another way tooprevent accidental zone deletion is by using a custom role tooensure hello operator and service accounts used toomanage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="c530d-201">2 단계 삭제, (hello 잘못 된 영역을 삭제 하는 tooprevent hello 영역 범위)에서 첫 번째 부여 영역 삭제 권한 toodelete 영역을 해야 하는 경우 적용할 수 있습니다 및 두 번째 toodelete hello 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-201">When you do need toodelete a zone, you can enforce a two-step delete, first granting zone delete permissions (at hello zone scope, tooprevent deleting hello wrong zone) and second toodelete hello zone.</span></span>

<span data-ttu-id="c530d-202">이러한 두 번째 방법은 tooremember toocreate 잠금이 필요 없이 해당 계정에서 액세스할 모든 영역에 대해 작동 hello 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-202">This second approach has hello advantage that it works for all zones accessed by those accounts, without having tooremember toocreate any locks.</span></span> <span data-ttu-id="c530d-203">Hello 단점은 hello 구독 소유자와 같은 영역 삭제 권한으로 모든 계정에 중요 한 영역 삭제 실수로 여전히 수 있음</span><span class="sxs-lookup"><span data-stu-id="c530d-203">It has hello disadvantage that any accounts with zone delete permissions, such as hello subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="c530d-204">가능한 toouse는 hello에서 두 방법-리소스 잠금 및 사용자 정의 역할-이와 심층적인 방어 접근 방식 tooDNS 영역 보안 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-204">It is possible toouse both approaches - resource locks and custom roles - at hello same time, as a defense-in-depth approach tooDNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c530d-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c530d-205">Next steps</span></span>

* <span data-ttu-id="c530d-206">RBAC 사용에 대 한 자세한 내용은 참조 [hello Azure 포털에에서 대 한 액세스 관리 시작](../active-directory/role-based-access-control-what-is.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c530d-206">For more information about working with RBAC, see [Get started with access management in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="c530d-207">리소스 잠금에 대한 자세한 내용은[ Azure Resource Manager를 사용하여 리소스 잠그기](../azure-resource-manager/resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c530d-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

