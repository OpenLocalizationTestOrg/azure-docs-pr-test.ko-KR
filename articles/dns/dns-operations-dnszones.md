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
# <a name="how-toomanage-dns-zones-using-powershell"></a>어떻게 PowerShell을 사용 하 여 toomanage DNS 영역

> [!div class="op_single_selector"]
> * [포털](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

이 문서에서는 어떻게 toomanage DNS 영역을 Azure PowerShell을 사용 하 여 보여 줍니다. 플랫폼 간 hello를 사용 하 여 DNS 영역을 관리할 수 있습니다 [Azure CLI](dns-operations-dnszones-cli.md) 또는 Azure 포털을 환영 합니다.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>DNS 영역 만들기

Hello를 사용 하 여 DNS 영역이 만들어집니다 `New-AzureRmDnsZone` cmdlet.

hello 다음 예제에서는 호출 하는 DNS 영역 *contoso.com* 호출 hello 리소스 그룹에 *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

hello 다음 예제에서는 두 개의 toocreate DNS 영역 방법을 [Azure 리소스 관리자 태그](dns-zones-records.md#tags), *프로젝트 데모 =* 및 *env = 테스트*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a>DNS 영역 가져오기

tooretrieve DNS 영역을 사용 하 여 hello `Get-AzureRmDnsZone` cmdlet. 이 작업을 DNS 개체 해당 tooan 기존 영역에 Azure DNS 영역을 반환 합니다. hello 개체 (예: hello 레코드 집합 수), hello 영역에 대 한 데이터를 포함 하지만 포함 하지 않는 자체 hello 레코드 집합 (참조 `Get-AzureRmDnsRecordSet`).

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

## <a name="list-dns-zones"></a>DNS 영역 나열

Hello 영역 이름에서 생략 하 여 `Get-AzureRmDnsZone`, 리소스 그룹의 모든 영역을 열거할 수 있습니다. 이 작업은 영역 개체의 배열을 반환합니다.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

Hello 영역 이름 및 hello 리소스 그룹 이름을 모두 생략 하 여 `Get-AzureRmDnsZone`, hello Azure 구독에 있는 모든 영역을 열거할 수 있습니다.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>DNS 영역 업데이트

DNS 영역 리소스를 사용 하 여 만들어질 수 tooa 변경 `Set-AzureRmDnsZone`합니다. 이 cmdlet hello hello 영역 내에서 DNS 레코드 집합 중 하나를 업데이트 하지 않습니다 (참조 [어떻게 tooManage DNS 레코드](dns-operations-recordsets.md)). 것에 hello 영역 리소스 자체의 tooupdate 속성 사용 됩니다. hello 쓰기 가능한 영역 속성은 현재 제한 toohello [hello 영역의 리소스에 대 한 '태그' Azure 리소스 관리자](dns-zones-records.md#tags)합니다.

다음 두 가지 방법으로 tooupdate hello 중 DNS 영역을 사용 합니다.

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a>영역 이름 및 리소스 그룹 hello를 사용 하 여 hello 영역 지정

이 방법은 지정 된 hello 값으로 기존 영역 태그 hello를 대체 합니다.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a>$Zone 개체를 사용 하 여 hello 영역 지정

이 방법은 hello 기존 영역 개체를 검색 하 고 hello 태그를 수정 다음 hello 변경 내용을 커밋합니다. 이러한 방식으로 기존 태그를 보존할 수 있습니다.

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

사용 하는 경우 `Set-AzureRmDnsZone` $zone 개체와 [Etag 검사](dns-zones-records.md#etags) 사용 tooensure 동시 변경 내용을 덮어쓰지 않습니다. Hello 옵션을 사용할 수 있습니다 `-Overwrite` toosuppress 이러한 검사를 전환 합니다.

## <a name="delete-a-dns-zone"></a>DNS 영역 삭제

Hello를 사용 하 여 DNS 영역을 삭제할 수 있습니다 `Remove-AzureRmDnsZone` cmdlet.

> [!NOTE]
> DNS 영역을 삭제 하면 모든 DNS 레코드가 hello 영역 내에서 삭제 합니다. 이 작업은 취소할 수 없습니다. DNS 영역 hello를 사용 하는 경우 hello 영역이 삭제 되 면 hello 영역을 사용 하 여 서비스 실패 합니다.
>
>실수로 영역 삭제 tooprotect 참조 [tooprotect DNS 영역 및 기록 방법을](dns-protect-zones-recordsets.md)합니다.


다음 두 가지 방법으로 toodelete hello 중 DNS 영역을 사용 합니다.

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a>Hello 영역 이름 및 리소스 그룹 이름을 사용 하 여 hello 영역 지정

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a>$Zone 개체를 사용 하 여 hello 영역 지정

Hello 영역 toobe 사용 하 여 삭제를 지정할 수는 `$zone` 에서 반환 된 개체 `Get-AzureRmDnsZone`합니다.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

hello 영역 개체를 매개 변수로 전달 되는 대신도 파이프 될 수 있습니다.

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

와 마찬가지로 `Set-AzureRmDnsZone`, 영역을 사용 하 여 hello를 지정 하는 `$zone` 개체 Etag 검사 tooensure 동시 변경 내용을 삭제 되지 않습니다 수 있습니다. 사용 하 여 hello `-Overwrite` toosuppress 이러한 검사를 전환 합니다.

## <a name="confirmation-prompts"></a>확인 메시지 표시

hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, 및 `Remove-AzureRmDnsZone` cmdlet 모든 확인 메시지를 표시를 지원 합니다.

둘 다 `New-AzureRmDnsZone` 및 `Set-AzureRmDnsZone` 확인 메시지를 표시 하는 경우 hello `$ConfirmPreference` PowerShell 기본 설정 변수 값은 `Medium` 이하로 합니다. 삭제할 경우의 DNS 영역 hello toohello 잠재적으로 높은 영향 인해 `Remove-AzureRmDnsZone` cmdlet 확인 메시지를 표시 하는 경우 hello `$ConfirmPreference` PowerShell 변수 이외의 모든 값을 가지 `None`합니다.

Hello 기본값에 대 한 이후 `$ConfirmPreference` 은 `High`만 `Remove-AzureRmDnsZone` 확인 기본적으로 메시지를 표시 합니다.

Hello 현재 문자인 `$ConfirmPreference` hello를 사용 하 여 설정을 `-Confirm` 매개 변수입니다. 지정 하는 경우 `-Confirm` 또는 `-Confirm:$True` , hello cmdlet 확인 메시지가 표시 되기 전에 실행 합니다. 지정 하는 경우 `-Confirm:$False` , hello cmdlet 표시 하지 않습니다 확인 합니다.

`-Confirm` 및 `$ConfirmPreference`에 대한 자세한 내용은 [기본 설정 변수 정보](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables)를 참조하세요.

## <a name="next-steps"></a>다음 단계

너무 방법에 대해 알아봅니다[레코드 집합 및 레코드 관리](dns-operations-recordsets.md) DNS 영역에 있습니다.
<br>
너무 방법에 대해 알아봅니다[사용자 도메인 tooAzure DNS 위임](dns-domain-delegation.md)합니다.
<br>
검토 hello [Azure DNS PowerShell 참조 설명서](/powershell/module/azurerm.dns)합니다.

