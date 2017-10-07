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
# <a name="how-tooprotect-dns-zones-and-records"></a>어떻게 tooprotect DNS 영역 및 기록

DNS 영역 및 레코드는 중요한 리소스입니다. DNS 영역 또는 단일 DNS 레코드만 삭제해도 전체 서비스 중단이 발생할 수 있습니다.  따라서 중요 DNS 영역 및 레코드가 무단 또는 실수로 변경되지 않도록 보호하는 것이 중요합니다.

이 문서에서는 DNS 영역과 레코드 이러한 변경에 대해 Azure DNS tooprotect 있습니다를 사용 하는 방법을 설명 합니다.  Azure Resource Manager에서 제공하는 두 가지 강력한 보안 기능, 즉, [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md)와 [리소스 잠금](../azure-resource-manager/resource-group-lock-resources.md)을 적용합니다.

## <a name="role-based-access-control"></a>역할 기반 액세스 제어

Azure RBAC(Role-Based Access Control)는 Azure 사용자, 그룹, 리소스에 대해 정확한 액세스 관리를 지원합니다. RBAC를 사용 하 여 정확 하 게 hello 제한 된 액세스를 부여할 구성할 수 사용자에 게 필요 업무 tooperform을 수 있습니다. RBAC를 사용하여 액세스를 관리하는 방법에 대한 자세한 내용은 [역할 기반 액세스 제어란](../active-directory/role-based-access-control-what-is.md)을 참조하세요.

### <a name="hello-dns-zone-contributor-role"></a>hello ' DNS 영역 참가자 ' 역할

hello ' DNS 영역 참가자 ' 역할은 DNS 리소스 관리를 위해 Azure에서 제공 하는 기본 제공 역할입니다.  DNS 영역 참가자 사용 권한 tooa 사용자 또는 그룹을 지정 해당 그룹 toomanage DNS 리소스 하지만 다른 형식의 리소스가 아닌 수 있습니다.

예를 들어, myzones' hello 리소스 그룹' Contoso Corporation에 대 한 다섯 가지 영역이 포함 됩니다. 부여 hello DNS 관리자 ' DNS 영역 참가자 ' 권한을 toothat 리소스 그룹을 해당 DNS 영역을 완전히 제어할 수 있습니다. 예를 들어 DNS 관리자에 게 가상 컴퓨터를 중지 또는 만들 수 없습니다 불필요 한 사용 권한을 부여 하지 않습니다.

hello 가장 간단한 방법은 tooassign RBAC 권한은 [hello Azure 포털을 통해](../active-directory/role-based-access-control-configure.md)합니다.  Hello 리소스 그룹에 대 한 hello '액세스 제어 (IAM)' 블레이드를 여세요 'Add'를 클릭 한 다음 hello ' DNS 영역 참가자 ' 역할 및 필요한 선택 hello 사용자 또는 그룹 toogrant 사용 권한을 선택 합니다.

![Hello Azure 포털을 통해 리소스 그룹 수준 RBAC](./media/dns-protect-zones-recordsets/rbac1.png)

권한은 [Azure PowerShell을 사용하여 부여](../active-directory/role-based-access-control-manage-access-powershell.md)할 수도 있습니다.

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

hello 이와 동등한 명령을 이기도 [hello Azure CLI를 통해 사용할 수 있는](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a>영역 수준 RBAC

Azure RBAC 규칙이 적용 된 tooa 구독 수는 리소스 그룹 또는 tooan 개별 리소스입니다. Azure DNS의 hello 경우에서 해당 리소스는 개별 DNS 영역 또는 개별 레코드 집합도 가능 합니다.

예를 들어 myzones' hello 리소스 그룹' contoso.com' hello 영역' 및 각 고객 계정에 대해 CNAME 레코드 만들어집니다 하는 subzone 지 대 'customers.contoso.com'를 포함 합니다.  hello 사용 되는 계정 toomanage이 CNAME 레코드 할당할 hello 'customers.contoso.com' 영역에만 사용 권한을 toocreate 레코드, 없어야 액세스 toohello 다른 영역입니다.

Hello Azure 포털을 통해 영역 수준 RBAC 사용 권한은 부여할 수 있습니다.  Hello 영역에 대 한 hello '액세스 제어 (IAM)' 블레이드를 여세요 'Add'를 클릭 한 다음 hello ' DNS 영역 참가자 ' 역할 및 필요한 선택 hello 사용자 또는 그룹 toogrant 사용 권한을 선택 합니다.

![Hello Azure 포털을 통해 DNS 영역 수준 RBAC](./media/dns-protect-zones-recordsets/rbac2.png)

권한은 [Azure PowerShell을 사용하여 부여](../active-directory/role-based-access-control-manage-access-powershell.md)할 수도 있습니다.

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

hello 이와 동등한 명령을 이기도 [hello Azure CLI를 통해 사용할 수 있는](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a>레코드 집합 수준 RBAC

한 단계 더 나아갈 수 있습니다. 메일 관리자를 게 Contoso Corporation에 대 한 액세스 toohello MX 및 hello 구로 hello '만든 contoso.com' 영역에 TXT 레코드를 필요로 하는 것이 좋습니다.  그녀 다른 TXT 또는 MX 레코드 또는 다른 종류의 tooany 레코드 tooany 액세스할 필요 하지 않습니다.  Azure DNS에 액세스 해야 하면 hello 레코드 집합 수준 tooprecisely hello 레코드를 메일 관리자 hello에서 tooassign 사용 권한을 허용 합니다.  hello 메일 관리자가 권한이 정확 하 게 hello, 그녀가 고 toomake 수 없습니다 다른 변경 됩니다.

레코드 집합 수준 RBAC 사용 권한은 hello hello 레코드 집합 블레이드에서 hello '사용자' 단추를 사용 하 여 Azure 포털을 통해 구성할 수 있습니다.

![레코드는 hello Azure 포털을 통해 RBAC 수준 설정](./media/dns-protect-zones-recordsets/rbac3.png)

레코드 집합 수준 RBAC 권한은 [Azure PowerShell을 사용하여 부여](../active-directory/role-based-access-control-manage-access-powershell.md)할 수도 있습니다.

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

hello 이와 동등한 명령을 이기도 [hello Azure CLI를 통해 사용할 수 있는](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a>사용자 지정 역할

hello 기본 제공 ' DNS 영역 참가자 ' 역할에 DNS 리소스를 완전히 제어할 수 있습니다. 그는 또한 가능한 toobuild 고유한 고객 Azure 역할, tooprovide도 세부적인 제어 합니다.

다시 각 Contoso Corporation 고객 계정에 대해 customers.contoso.com' hello 영역'에서 CNAME 레코드를 작성 하는 hello 예제를 참조 하세요.  hello 사용 되는 계정 toomanage 이러한 CNAMEs 사용 권한 toomanage CNAME 레코드가 부여 됩니다.  되기 없습니다 toomodify 레코드의 다른 유형 (예: MX 레코드를 변경) 또는 영역 수준 작업 영역 삭제 등을 수행 합니다.

다음 예제는 hello만 CNAME 레코드를 관리 하기 위한 사용자 지정 역할 정을 보여 줍니다.

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

작업 속성 hello hello 다음 DNS 특정 권한을 정의 합니다.

* `Microsoft.Network/dnsZones/CNAME/*`은 CNAME 레코드에 대한 모든 권한을 부여합니다.
* `Microsoft.Network/dnsZones/read`사용 권한 tooread DNS 영역을 하지만 toosee 있습니다를 사용 하도록 설정 하는 hello CNAME 생성 되는 영역을 hello toomodify 하지 부여 합니다.

남은 동작이 hello에서 복사 되는 hello [DNS 영역 참가자 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor)합니다.

> [!NOTE]
> 레코드를 삭제 하는 사용자 지정 RBAC 역할 tooprevent를 사용 하 여 효과적인 컨트롤이 아닙니다 여전히 toobe 업데이트 허용 하는 동안 설정 합니다. 이 방식에서는 레코드 집합을 삭제할 수 없지만 수정은 방지할 수 없습니다.  허용 된 수정 추가 등 tooleave '빈' 레코드 집합 기록 모든 제거 포함 hello 레코드 집합에서 레코드를 제거 합니다. 이 hello DNS 확인 관점에서 설정 hello 레코드를 삭제 하는 것과 같습니다.

사용자 지정 역할 정의 현재 hello Azure 포털을 통해 정의할 수 없습니다. 이 역할 정의를 기준으로 하는 사용자 지정 역할은 Azure PowerShell을 사용하여 만들 수 있습니다.

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

Hello Azure CLI를 통해 만들 수도 있습니다.

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

hello 역할 그런 다음 할당할 수 있습니다 hello에서 동일한 방식으로 기본 제공 역할으로이 문서의 앞부분에 설명 된 대로 합니다.

Toocreate를 관리 하 고 사용자 지정 역할을 할당 하는 방법에 대 한 자세한 내용은 참조 [사용자 정의 역할에서 Azure RBAC](../active-directory/role-based-access-control-custom-roles.md)합니다.

## <a name="resource-locks"></a>리소스 잠금

또한 tooRBAC Azure 리소스 관리자 지원 다른 유형의 보안 제어, 즉 hello 기능 too'lock' 리소스입니다. RBAC 규칙을 사용 하면 특정 사용자 및 그룹의 toocontrol hello 동작, 여기서 리소스 잠금이 적용된 toohello 리소스 되며 모든 사용자 및 역할에서 적용 됩니다. 자세한 내용은 [Azure 리소스 관리자를 사용하여 리소스 잠그기](../azure-resource-manager/resource-group-lock-resources.md)를 참조하세요.

리소스 잠금은 **DoNotDelete** 및 **ReadOnly**의 두 가지 유형이 있습니다. 적용할 수 있습니다 이러한 tooa DNS 영역 또는 tooan 개별 레코드 집합 중 하나입니다.  hello 다음 섹션에서는 설명 몇 가지 일반적인 시나리오와 방법을 toosupport 리소스 잠금을 사용 합니다.

### <a name="protecting-against-all-changes"></a>모든 변경으로부터 보호

tooprevent 되 고 변경 ReadOnly 잠금 toohello 영역을 적용 합니다.  이 경우 새 레코드 집합을 만들 수 없으며 기존 레코드 집합이 수정 또는 삭제되지 않습니다.

영역 수준 리소스 잠금은 hello Azure 포털을 통해 만들 수 있습니다.  Hello DNS 영역 블레이드에서 'Locks'를 클릭 한 다음 'Add':

![영역 수준 리소스 잠금을 hello Azure 포털을 통해](./media/dns-protect-zones-recordsets/locks1.png)

또한 Azure PowerShell을 통해 영역 수준 리소스 잠금을 만들 수 있습니다.

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

현재 Azure CLI hello를 통해 Azure 리소스 잠금을 구성 지원 되지 않습니다.

### <a name="protecting-individual-records"></a>개별 레코드 보호

tooprevent 설정 수정에 대 한 기존 DNS 레코드 ReadOnly 잠금 toohello 레코드 집합을 적용 합니다.

> [!NOTE]
> DoNotDelete 잠금 tooa 적용 레코드 집합은 효과적인 컨트롤이 아닙니다. Hello 레코드 삭제 되지 않도록 설정 하는 것을 방지 하지만 중단 되지는 않습니다 것 수정 되지 않도록 합니다.  허용 된 수정 추가 등 tooleave '빈' 레코드 집합 기록 모든 제거 포함 hello 레코드 집합에서 레코드를 제거 합니다. 이 hello DNS 확인 관점에서 설정 hello 레코드를 삭제 하는 것과 같습니다.

레코드 집합 수준 리소스 잠금은 현재 Azure PowerShell을 사용해야 구성할 수 있으며  Hello Azure 포털 또는 Azure CLI에는 지원 되지 않습니다.

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a>영역 삭제로부터 보호

Azure dns에서 영역 삭제 되 면 hello 영역의 모든 레코드 집합 삭제 됩니다.  이 작업은 취소할 수 없습니다.  중요 한 영역을 실수로 삭제에 hello 잠재적인 toohave 중요 한 비즈니스 영향을 줍니다.  따라서 실수로 영역 삭제에 대 한 매우 중요 한 tooprotect 버전이 있습니다.

Hello 영역 삭제 되지 않도록 방지 DoNotDelete 잠금 tooa 영역을 적용 합니다.  그러나 잠금이 자식 리소스 상속, 이후 또한 hello 영역에서 삭제 되지 않도록 적절 하지 않을 모든 레코드 집합 방지 합니다.  또한 위의 hello 참고에 설명 된 때 하지도 효과적 hello 기존 레코드 집합에서 여전히 레코드를 제거할 수 있으므로 합니다.

대신, 예: hello SOA 레코드 집합 hello 시간대에서 설정 DoNotDelete 잠금 tooa 레코드를 적용 하는 것이 좋습니다.  Hello 영역도 hello 레코드 집합을 삭제 하지 않고 삭제할 수 있으므로이 방지 자유롭게 수정할 hello 영역 toobe 내의 레코드 집합 허용 하면서 영역 삭제 됩니다. Toodelete hello 영역, 하려고 시도 하는 경우 Azure 리소스 관리자 hello SOA 레코드 집합 삭제는이 및 SOA hello 잠겨 있기 때문에 블록 hello 호출을 검색 합니다.  삭제되는 레코드 집합이 없습니다.

다음 PowerShell 명령을 hello hello SOA 레코드의 영역을 제공 하는 hello에 대 한 DoNotDelete 잠금을 만듭니다.

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

또 다른 방법은 tooprevent 실수로 영역 삭제 하는 영역을 영역가 않는 사용자 지정 역할 tooensure hello 연산자 및 서비스 사용 되는 계정 toomanage 사용 하 여 사용 권한을 삭제 합니다. 2 단계 삭제, (hello 잘못 된 영역을 삭제 하는 tooprevent hello 영역 범위)에서 첫 번째 부여 영역 삭제 권한 toodelete 영역을 해야 하는 경우 적용할 수 있습니다 및 두 번째 toodelete hello 영역입니다.

이러한 두 번째 방법은 tooremember toocreate 잠금이 필요 없이 해당 계정에서 액세스할 모든 영역에 대해 작동 hello 이점이 있습니다. Hello 단점은 hello 구독 소유자와 같은 영역 삭제 권한으로 모든 계정에 중요 한 영역 삭제 실수로 여전히 수 있음

가능한 toouse는 hello에서 두 방법-리소스 잠금 및 사용자 정의 역할-이와 심층적인 방어 접근 방식 tooDNS 영역 보안 업데이트 합니다.

## <a name="next-steps"></a>다음 단계

* RBAC 사용에 대 한 자세한 내용은 참조 [hello Azure 포털에에서 대 한 액세스 관리 시작](../active-directory/role-based-access-control-what-is.md)합니다.
* 리소스 잠금에 대한 자세한 내용은[ Azure Resource Manager를 사용하여 리소스 잠그기](../azure-resource-manager/resource-group-lock-resources.md)를 참조하세요.

