---
title: "DNS 영역 및 레코드 보호 | Microsoft 문서"
description: "Microsoft Azure DNS에서 DNS 영역 및 레코드 집합을 보호하는 방법"
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
ms.openlocfilehash: 0b7040d6273b3a6b85cd55850d596807226b87fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-protect-dns-zones-and-records"></a><span data-ttu-id="10e8c-103">DNS 영역 및 레코드를 보호하는 방법</span><span class="sxs-lookup"><span data-stu-id="10e8c-103">How to protect DNS zones and records</span></span>

<span data-ttu-id="10e8c-104">DNS 영역 및 레코드는 중요한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="10e8c-105">DNS 영역 또는 단일 DNS 레코드만 삭제해도 전체 서비스 중단이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="10e8c-106">따라서 중요 DNS 영역 및 레코드가 무단 또는 실수로 변경되지 않도록 보호하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="10e8c-107">이 문서는 Azure DNS를 통해 DNS 영역 및 레코드를 이러한 변경으로부터 보호하는 방식에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-107">This article explains how Azure DNS enables you to protect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="10e8c-108">Azure Resource Manager에서 제공하는 두 가지 강력한 보안 기능, 즉, [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md)와 [리소스 잠금](../azure-resource-manager/resource-group-lock-resources.md)을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="10e8c-109">역할 기반 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="10e8c-109">Role-based access control</span></span>

<span data-ttu-id="10e8c-110">Azure RBAC(Role-Based Access Control)는 Azure 사용자, 그룹, 리소스에 대해 정확한 액세스 관리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="10e8c-111">RBAC를 사용하여 사용자가 해당 작업을 수행하는 데 필요한 만큼의 액세스 권한을 정확하게 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-111">Using RBAC, you can grant precisely the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="10e8c-112">RBAC를 사용하여 액세스를 관리하는 방법에 대한 자세한 내용은 [역할 기반 액세스 제어란](../active-directory/role-based-access-control-what-is.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10e8c-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="the-dns-zone-contributor-role"></a><span data-ttu-id="10e8c-113">'DNS 영역 참가자' 역할</span><span class="sxs-lookup"><span data-stu-id="10e8c-113">The 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="10e8c-114">'DNS 영역 참가자' 역할은 DNS 리소스 관리를 위해 Azure에서 제공하는 기본 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-114">The 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="10e8c-115">DNS 영역 참가자 권한을 사용자 또는 그룹에 할당할 경우 해당 그룹에서 DNS 리소스를 관리할 수 있지만 다른 유형의 리소스는 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-115">Assigning DNS Zone Contributor permissions to a user or group enables that group to manage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="10e8c-116">예를 들어 'myzones' 리소스 그룹에 Contoso Corporation의 영역 5개가 있다고 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-116">For example, suppose the resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="10e8c-117">해당 리소스 그룹에'DNS 영역 참가자' DNS 관리자 권한을 부여할 경우 해당 DNS 영역을 완전히 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-117">Granting the DNS administrator 'DNS Zone Contributor' permissions to that resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="10e8c-118">또한 불필요한 권한을 부여하지 않습니다. 예를 들어 DNS 관리자는 Virtual Machines를 만들거나 중지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-118">It also avoids granting unnecessary permissions, for example the DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="10e8c-119">RBAC 권한을 할당하는 가장 간단한 방법은 [Azure Portal을 사용](../active-directory/role-based-access-control-configure.md)하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-119">The simplest way to assign RBAC permissions is [via the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="10e8c-120">리소스 그룹의 [Access Control(IAM)] 블레이드를 열고 [추가]를 클릭한 다음 [DNS 영역 참가자] 역할을 선택하고 권한을 부여할 사용자 또는 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-120">Open the 'Access control (IAM)' blade for the resource group, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![Azure Portal을 통한 리소스 그룹 수준 RBAC](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="10e8c-122">권한은 [Azure PowerShell을 사용하여 부여](../active-directory/role-based-access-control-manage-access-powershell.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="10e8c-123">동일한 명령을 [Azure CLI를 통해 사용](../active-directory/role-based-access-control-manage-access-azure-cli.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-123">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="10e8c-124">영역 수준 RBAC</span><span class="sxs-lookup"><span data-stu-id="10e8c-124">Zone level RBAC</span></span>

<span data-ttu-id="10e8c-125">구독, 리소스 그룹 또는 개별 리소스에 Azure RBAC 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-125">Azure RBAC rules can be applied to a subscription, a resource group or to an individual resource.</span></span> <span data-ttu-id="10e8c-126">Azure DNS의 경우 해당 리소스는 개별 DNS 영역이 될 수 있으며 개별 레코드 집합도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-126">In the case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="10e8c-127">예를 들어 'myzones' 리소스 그룹에 'contoso.com' 영역과 각 고객 계정에 대해 CNAME 레코드가 만들어져 있는 'customers.contoso.com' 하위 영역이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-127">For example, suppose the resource group 'myzones' contains the zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="10e8c-128">이러한 CNAME 레코드를 관리하는 데 사용하는 계정은 'customers.contoso.com' 영역의 레코드만 만들 수 있는 권한을 부여받아야 하며 다른 영역에는 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-128">The account used to manage these CNAME records should be assigned permissions to create records in the 'customers.contoso.com' zone only, it should not have access to the other zones.</span></span>

<span data-ttu-id="10e8c-129">영역 수준 RBAC 권한은 Azure Portal을 통해 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-129">Zone-level RBAC permissions can be granted via the Azure portal.</span></span>  <span data-ttu-id="10e8c-130">영역의 [Access Control(IAM)] 블레이드를 열고 [추가]를 클릭한 다음 [DNS 영역 참가자] 역할을 선택하고 권한을 부여할 필요가 있는 사용자 또는 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-130">Open the 'Access control (IAM)' blade for the zone, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![Azure Portal을 통한 DNS 영역 수준 RBAC](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="10e8c-132">권한은 [Azure PowerShell을 사용하여 부여](../active-directory/role-based-access-control-manage-access-powershell.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to a specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="10e8c-133">동일한 명령을 [Azure CLI를 통해 사용](../active-directory/role-based-access-control-manage-access-azure-cli.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-133">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to a specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="10e8c-134">레코드 집합 수준 RBAC</span><span class="sxs-lookup"><span data-stu-id="10e8c-134">Record set level RBAC</span></span>

<span data-ttu-id="10e8c-135">한 단계 더 나아갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-135">We can go one step further.</span></span> <span data-ttu-id="10e8c-136">'contoso.com' 영역의 루트 수준에서 MX 및 TXT 레코드에 액세스해야 하는 Contoso Corporation의 메일 관리자를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="10e8c-136">Consider the mail administrator for Contoso Corporation, who needs access to the MX and TXT records at the apex of the 'contoso.com' zone.</span></span>  <span data-ttu-id="10e8c-137">이 메일 관리자는 다른 MX 레코드, TXT 레코드 또는 다른 유형의 레코드에 액세스 할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-137">She doesn't need access to any other MX or TXT records, or to any records of any other type.</span></span>  <span data-ttu-id="10e8c-138">Azure DNS에서는 레코드 집합 수준에서 메일 관리자가 액세스해야 하는 레코드에 정확하게 권한을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-138">Azure DNS allows you to assign permissions at the record set level, to precisely the records that the mail administrator needs access to.</span></span>  <span data-ttu-id="10e8c-139">메일 관리자는 자신에게 필요한 관리 권한만 정확하게 부여받으며 다른 사항을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-139">The mail administrator is granted precisely the control she needs, and is unable to make any other changes.</span></span>

<span data-ttu-id="10e8c-140">Azure Portal에서 레코드 집합 블레이드의 [사용자] 단추를 사용하여 레코드 집합 수준 RBAC 권한을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-140">Record-set level RBAC permissions can be configured via the Azure portal, using the 'Users' button in the record set blade:</span></span>

![Azure Portal을 통한 레코드 집합 수준 RBAC](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="10e8c-142">레코드 집합 수준 RBAC 권한은 [Azure PowerShell을 사용하여 부여](../active-directory/role-based-access-control-manage-access-powershell.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions to a specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="10e8c-143">동일한 명령을 [Azure CLI를 통해 사용](../active-directory/role-based-access-control-manage-access-azure-cli.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-143">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions to a specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="10e8c-144">사용자 지정 역할</span><span class="sxs-lookup"><span data-stu-id="10e8c-144">Custom roles</span></span>

<span data-ttu-id="10e8c-145">기본 제공 'DNS 영역 참가자' 역할을 사용하면 DNS 리소스를 완벽히 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-145">The built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="10e8c-146">또한 사용자 지정 Azure 역할을 구축하여 더욱 정밀한 관리를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-146">It is also possible to build your own customer Azure roles, to provide even finer-grained control.</span></span>

<span data-ttu-id="10e8c-147">'customers.contoso.com' 영역에서 Contoso Corporation 고객 계정마다 CNAME 레코드를 만드는 예를 다시 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="10e8c-147">Consider again the example in which a CNAME record in the zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="10e8c-148">이러한 CNAME을 관리하는 데 사용한 계정은 CNAME 레코드만 관리할 권한을 부여받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-148">The account used to manage these CNAMEs should be granted permission to manage CNAME records only.</span></span>  <span data-ttu-id="10e8c-149">그런 다음 다른 유형의 레코드(예: MX 레코드 변경)를 수정하거나 영역 삭제와 같은 영역 수준 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-149">It is then unable to modify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="10e8c-150">다음 예는 CNAME 레코드 관리에 대한 사용자 지정 역할 정의를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-150">The following example shows a custom role definition for managing CNAME records only:</span></span>

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

<span data-ttu-id="10e8c-151">작업 속성은 다음과 같은 DNS별 권한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-151">The Actions property defines the following DNS-specific permissions:</span></span>

* <span data-ttu-id="10e8c-152">`Microsoft.Network/dnsZones/CNAME/*`은 CNAME 레코드에 대한 모든 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="10e8c-153">`Microsoft.Network/dnsZones/read`는 DNS 영역을 읽을 권한을 부여하지만 수정 권한은 부여하지 않아 CNAME이 생성되는 영역을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-153">`Microsoft.Network/dnsZones/read` grants permission to read DNS zones, but not to modify them, enabling you to see the zone in which the CNAME is being created.</span></span>

<span data-ttu-id="10e8c-154">나머지 작업은 [DNS 영역 참가자의 기본 역할](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor)에서 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-154">The remaining Actions are copied from the [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="10e8c-155">레코드 집합 삭제를 방지하기 위해 사용자 지정 RBAC 역할을 사용하면서 업데이트를 허용하는 것은 효과적인 관리가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-155">Using a custom RBAC role to prevent deleting record sets while still allowing them to be updated is not an effective control.</span></span> <span data-ttu-id="10e8c-156">이 방식에서는 레코드 집합을 삭제할 수 없지만 수정은 방지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="10e8c-157">허용되는 수정 작업에는 레코드 집합을 '비우기' 위해 레코드를 모두 제거하는 작업을 포함하여 레코드 집합에서 레코드를 추가 및 제거하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-157">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="10e8c-158">이 경우 DNS 확인 관점에서 레코드 집합을 삭제하는 것과 같은 효과를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-158">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="10e8c-159">사용자 지정 역할 정의는 현재 Azure Portal을 통해 정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-159">Custom role definitions cannot currently be defined via the Azure portal.</span></span> <span data-ttu-id="10e8c-160">이 역할 정의를 기준으로 하는 사용자 지정 역할은 Azure PowerShell을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="10e8c-161">Azure CLI를 통해 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-161">It can also be created via the Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="10e8c-162">그런 다음 이 문서의 앞부분에서 설명한 대로 역할을 기본 역할과 동일한 방식으로 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-162">The role can then be assigned in the same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="10e8c-163">사용자 지정 역할을 만들고 관리하고 할당하는 방법은 [Azure RBAC에서 사용자 지정 역할](../active-directory/role-based-access-control-custom-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10e8c-163">For more information on how to create, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="10e8c-164">리소스 잠금</span><span class="sxs-lookup"><span data-stu-id="10e8c-164">Resource locks</span></span>

<span data-ttu-id="10e8c-165">RBAC 외에도 Azure Resource Manager는 리소스를 '잠그는' 기능과 같은 다른 유형의 보안 관리 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-165">In addition to RBAC, Azure Resource Manager supports another type of security control, namely the ability to 'lock' resources.</span></span> <span data-ttu-id="10e8c-166">특정 사용자와 그룹의 작업을 관리할 수 있는 RBAC 규칙의 경우 리소스 잠금이 리소스에 적용되며 모든 사용자와 역할에 대해 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-166">Where RBAC rules allow you to control the actions of specific users and groups, resource locks are applied to the resource, and are effective across all users and roles.</span></span> <span data-ttu-id="10e8c-167">자세한 내용은 [Azure 리소스 관리자를 사용하여 리소스 잠그기](../azure-resource-manager/resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10e8c-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="10e8c-168">리소스 잠금은 **DoNotDelete** 및 **ReadOnly**의 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="10e8c-169">이러한 잠금은 DNS 영역 또는 개별 레코드 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-169">These can be applied either to a DNS zone, or to an individual record set.</span></span>  <span data-ttu-id="10e8c-170">다음 섹션에서는 몇 가지 일반적인 시나리오와 리소스 잠금을 사용하여 지원하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-170">The following sections describe several common scenarios, and how to support them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="10e8c-171">모든 변경으로부터 보호</span><span class="sxs-lookup"><span data-stu-id="10e8c-171">Protecting against all changes</span></span>

<span data-ttu-id="10e8c-172">모든 변경을 방지하려면 영역에 ReadOnly 잠금을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-172">To prevent any changes being made, apply a ReadOnly lock to the zone.</span></span>  <span data-ttu-id="10e8c-173">이 경우 새 레코드 집합을 만들 수 없으며 기존 레코드 집합이 수정 또는 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="10e8c-174">Azure Portal을 통해 영역 수준의 리소스 잠금을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-174">Zone level resource locks can be created via the Azure portal.</span></span>  <span data-ttu-id="10e8c-175">DNS 영역 블레이드에서 [잠금]을 클릭한 다음 [추가]를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-175">From the DNS zone blade, click 'Locks', then 'Add':</span></span>

![Azure Portal을 통한 영역 수준 리소스 잠금](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="10e8c-177">또한 Azure PowerShell을 통해 영역 수준 리소스 잠금을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="10e8c-178">현재는 Azure CLI를 통해 Azure 리소스 잠금을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-178">Configuring Azure resource locks is not currently supported via the Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="10e8c-179">개별 레코드 보호</span><span class="sxs-lookup"><span data-stu-id="10e8c-179">Protecting individual records</span></span>

<span data-ttu-id="10e8c-180">기존 DNS 레코드 집합이 수정되지 않도록 하려면 레코드 집합에 ReadOnly 잠금을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-180">To prevent an existing DNS record set against modification, apply a ReadOnly lock to the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="10e8c-181">레코드 집합에 DoNotDelete 잠금을 적용하는 것은 효과적인 관리 방법이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-181">Applying a DoNotDelete lock to a record set is not an effective control.</span></span> <span data-ttu-id="10e8c-182">이 방식에서는 레코드 집합을 삭제할 수 없지만 수정은 방지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-182">It prevents the record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="10e8c-183">허용되는 수정 작업에는 레코드 집합을 '비우기' 위해 레코드를 모두 제거하는 작업을 포함하여 레코드 집합에서 레코드를 추가 및 제거하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-183">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="10e8c-184">이 경우 DNS 확인 관점에서 레코드 집합을 삭제하는 것과 같은 효과를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-184">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="10e8c-185">레코드 집합 수준 리소스 잠금은 현재 Azure PowerShell을 사용해야 구성할 수 있으며</span><span class="sxs-lookup"><span data-stu-id="10e8c-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="10e8c-186">Azure Portal 또는 Azure CLI에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-186">They are not supported in the Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="10e8c-187">영역 삭제로부터 보호</span><span class="sxs-lookup"><span data-stu-id="10e8c-187">Protecting against zone deletion</span></span>

<span data-ttu-id="10e8c-188">Azure DNS에서 영역이 삭제되면 해당 영역의 모든 레코드 집합도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-188">When a zone is deleted in Azure DNS, all record sets in the zone are also deleted.</span></span>  <span data-ttu-id="10e8c-189">이 작업은 취소할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-189">This operation cannot be undone.</span></span>  <span data-ttu-id="10e8c-190">중요 영역을 실수로 삭제할 경우 비즈니스에 심각한 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-190">Accidentally deleting a critical zone has the potential to have a significant business impact.</span></span>  <span data-ttu-id="10e8c-191">따라서 실수로 영역을 삭제하지 않도록 보호하는 것이 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-191">It is therefore very important to protect against accidental zone deletion.</span></span>

<span data-ttu-id="10e8c-192">영역에 DoNotDelete 잠금을 적용할 경우 영역이 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-192">Applying a DoNotDelete lock to a zone prevents the zone from being deleted.</span></span>  <span data-ttu-id="10e8c-193">하지만 하위 리소스에서 잠금을 상속하기 때문에 영역에 있는 레코드 집합을 삭제할 수 없게 되며 이러한 상황은 바람직하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-193">However, since locks are inherited by child resources, it also prevents any record sets in the zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="10e8c-194">또한 위 참고 사항에서 설명한 바와 같이 기존 레코드 집합에서 여전히 레코드를 제거할 수 있기 때문에 비효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-194">Furthermore, as described in the note above, it is also ineffective since records can still be removed from the existing record sets.</span></span>

<span data-ttu-id="10e8c-195">대신 영역의 레코드 집합(예: SOA 레코드 집합)에 DoNotDelete 잠금을 적용해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="10e8c-195">As an alternative, consider applying a DoNotDelete lock to a record set in the zone, such as the SOA record set.</span></span>  <span data-ttu-id="10e8c-196">영역을 삭제하면 레코드 집합도 삭제되기 때문에 이 잠금을 적용하면 영역이 삭제되지 않도록 보호하는 동시에 영역 내 레코드 집합을 자유롭게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-196">Since the zone cannot be deleted without also deleting the record sets, this protects against zone deletion, while still allowing record sets within the zone to be modified freely.</span></span> <span data-ttu-id="10e8c-197">영역을 삭제하려고 시도할 경우 Azure Resource Manager에서 SOA 레코드 집합도 삭제되는 것을 감지하고 SOA가 잠기므로 호출을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-197">If an attempt is made to delete the zone, Azure Resource Manager detects this would also delete the SOA record set, and blocks the call because the SOA is locked.</span></span>  <span data-ttu-id="10e8c-198">삭제되는 레코드 집합이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-198">No record sets are deleted.</span></span>

<span data-ttu-id="10e8c-199">다음 PowerShell 명령은 지정된 영역의 SOA 레코드에 대해 DoNotDelete 잠금을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-199">The following PowerShell command creates a DoNotDelete lock against the SOA record of the given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on the record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="10e8c-200">실수로 영역을 삭제하지 못하게 하는 또 다른 방법으로 사용자 지정 역할을 사용하여 영역 관리에 사용되는 운영자 및 서비스 계정에 영역 삭제 권한이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-200">Another way to prevent accidental zone deletion is by using a custom role to ensure the operator and service accounts used to manage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="10e8c-201">영역을 삭제해야 하는 경우 2단계 삭제 작업을 수행하는데, 먼저 영역 범위에서 잘못된 영역을 삭제하지 않도록 하는 영역 삭제 권한을 부여하고, 다음으로 영역을 삭제하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-201">When you do need to delete a zone, you can enforce a two-step delete, first granting zone delete permissions (at the zone scope, to prevent deleting the wrong zone) and second to delete the zone.</span></span>

<span data-ttu-id="10e8c-202">이 두 번째 방법은 잠금을 만들지 않고도 해당 계정에서 액세스하는 모든 영역에서 작동한다는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-202">This second approach has the advantage that it works for all zones accessed by those accounts, without having to remember to create any locks.</span></span> <span data-ttu-id="10e8c-203">구독 소유자와 같이 영역 삭제 권한이 있는 계정은 여전히 실수로 중요한 영역을 삭제할 수 있다는 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-203">It has the disadvantage that any accounts with zone delete permissions, such as the subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="10e8c-204">DNS 영역 보호에 대한 심층적 방어 접근 방식으로서 리소스 잠금과 사용자 지정 역할을 동시에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="10e8c-204">It is possible to use both approaches - resource locks and custom roles - at the same time, as a defense-in-depth approach to DNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10e8c-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="10e8c-205">Next steps</span></span>

* <span data-ttu-id="10e8c-206">RBAC를 사용하는 방법은 [Azure Portal에서 액세스 관리 시작](../active-directory/role-based-access-control-what-is.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10e8c-206">For more information about working with RBAC, see [Get started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="10e8c-207">리소스 잠금에 대한 자세한 내용은[ Azure Resource Manager를 사용하여 리소스 잠그기](../azure-resource-manager/resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="10e8c-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

