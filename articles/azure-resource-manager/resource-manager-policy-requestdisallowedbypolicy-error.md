---
title: "Azure 리소스 정책에 aaaRequestDisallowedByPolicy 오류 | Microsoft Docs"
description: "Hello RequestDisallowedByPolicy 오류 hello 원인을 설명합니다."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Azure 리소스 정책의 RequestDisallowedByPolicy 오류

이 문서에서는 hello RequestDisallowedByPolicy 오류의 hello 원인을 설명,이 오류에 대 한 솔루션을 제공 합니다.

## <a name="symptom"></a>증상

Toodo 배포 하는 동안 작업을 시도 하면 때 발생할 수 있습니다는 **RequestDisallowedByPolicy** hello 작업은 어떠한 오류 수행할 수 있습니다. hello 아래에는 hello 오류의 샘플:

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>문제 해결

배포를 차단한 hello 정책에 대 한 세부 정보 tooretrieve hello 방법 중 하나를 수행 하는 hello를 사용 합니다.

### <a name="method-1"></a>방법 1

PowerShell에서 해당 정책 식별자 hello로 제공 **Id** 배포를 차단한 hello 정책에 대 한 매개 변수 tooretrieve 세부 정보입니다.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>방법 2 

Azure CLI 2.0에서 hello 정책 정의의 hello 이름을 제공 합니다. 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>해결 방법

보안 또는 규정 준수를 위해 IT 부서는 공용 IP 주소, 네트워크 보안 그룹, 사용자 정의 경로 또는 경로 테이블 만들기를 금지하는 리소스 정책을 적용할 수 있습니다. Hello "증상" 섹션에에서 설명 된 hello 오류 메시지의 hello 샘플, hello 정책 이름은 **regionPolicyDefinition**, 있지만 달라질 수 있습니다.
tooresolve이이 문제를 IT 부서 tooreview hello 리소스 정책에 사용 하 고 tooperform hello 정책 준수 작업을 요청 하는 방법을 확인 합니다.


자세한 내용은 다음 문서는 hello 참조:

- [리소스 정책 개요](resource-manager-policy.md)
- [일반적인 배포 오류 - RequestDisallowedByPolicy](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


