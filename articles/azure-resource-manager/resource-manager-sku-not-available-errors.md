---
title: "Azure SKU 사용할 수 없음 오류 | Microsoft Docs"
description: "배포 시 발생하는 SKU를 사용할 수 없음 오류를 해결하는 방법을 설명합니다."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: support-article
ms.date: 09/13/2017
ms.author: tomfitz
ms.openlocfilehash: 25cea4ae23471d182105ca3f720aaf74f81bf8c4
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="resolve-errors-for-sku-not-available"></a>SKU 사용할 수 없음 오류 해결

이 문서에서는 **SkuNotAvailable** 오류를 해결하는 방법에 대해 설명합니다.

## <a name="symptom"></a>증상

리소스를 배포할 때(일반적으로 가상 컴퓨터) 다음 오류 코드 및 오류 메시지가 표시됩니다.

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

## <a name="cause"></a>원인

선택한 리소스 SKU(예: VM 크기)를 선택한 위치에 사용할 수 없는 경우 이 오류가 나타납니다.

## <a name="solution"></a>해결 방법

이 문제를 해결하려면 지역에서 사용할 수 있는 SKU가 무엇인지 알아내야 합니다. PowerShell, 포털 또는 REST 작업을 사용하여 사용 가능한 SKU를 찾을 수 있습니다.

### <a name="solution-1"></a>해결 방법 1

PowerShell에서 [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) 명령을 사용합니다. 결과를 위치별로 필터링합니다. 이 명령이 작동하려면 최신 버전의 PowerShell이 있어야 합니다.

```powershell
Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
```

결과에는 위치에 대한 SKU 목록과 해당 SKU에 대한 제한 사항이 포함됩니다.

```powershell
ResourceType                Name      Locations Restriction                      Capability Value
------------                ----      --------- -----------                      ---------- -----
availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
virtualMachines      Standard_A0 southcentralus
virtualMachines      Standard_A1 southcentralus
virtualMachines      Standard_A2 southcentralus
```

### <a name="solution-2"></a>해결 방법 2

Azure CLI에서 `az vm list-skus` 명령을 사용합니다. 그런 다음 `grep` 또는 유사한 유틸리티를 사용하여 출력을 필터링할 수 있습니다.

```bash
$ az vm list-skus --output table
ResourceType      Locations           Name                    Capabilities                       Tier      Size           Restrictions
----------------  ------------------  ----------------------  ---------------------------------  --------  -------------  ---------------------------
availabilitySets  eastus              Classic                 MaximumPlatformFaultDomainCount=3
avilabilitySets   eastus              Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  eastus2             Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  eastus2             Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  westus              Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  westus              Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  centralus           Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  centralus           Aligned                 MaximumPlatformFaultDomainCount=3
```

### <a name="solution-3"></a>해결 방법 3

[포털](https://portal.azure.com)을 사용합니다. 포털에 로그인하고 인터페이스를 통해 리소스를 추가합니다. 값을 설정하면 해당 리소스에 사용 가능한 SKU가 표시됩니다. 배포를 완료할 필요는 없습니다.

![사용 가능한 SKU](./media/resource-manager-sku-not-available-errors/view-sku.png)

### <a name="solution-4"></a>해결 방법 4

가상 컴퓨터에 대한 REST API를 사용합니다. 다음 요청을 보냅니다.

```HTTP 
GET
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
```

다음과 같은 형식으로 사용 가능한 SKU 및 지역을 반환합니다.

```json
{
  "value": [
    {
      "resourceType": "virtualMachines",
      "name": "Standard_A0",
      "tier": "Standard",
      "size": "A0",
      "locations": [
        "eastus"
      ],
      "restrictions": []
    },
    {
      "resourceType": "virtualMachines",
      "name": "Standard_A1",
      "tier": "Standard",
      "size": "A1",
      "locations": [
        "eastus"
      ],
      "restrictions": []
    },
    ...
  ]
}
```

해당 위치 또는 대체 위치에서 비즈니스 요구를 충족하는 적합한 SKU를 찾을 수 없는 경우 [SKU 요청](https://aka.ms/skurestriction)을 Azure 지원에 제출하세요.