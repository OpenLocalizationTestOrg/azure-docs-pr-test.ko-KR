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
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="17df3-103">Azure 리소스 정책의 RequestDisallowedByPolicy 오류</span><span class="sxs-lookup"><span data-stu-id="17df3-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="17df3-104">이 문서에서는 hello RequestDisallowedByPolicy 오류의 hello 원인을 설명,이 오류에 대 한 솔루션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="17df3-104">This article describes hello cause of hello RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="17df3-105">증상</span><span class="sxs-lookup"><span data-stu-id="17df3-105">Symptom</span></span>

<span data-ttu-id="17df3-106">Toodo 배포 하는 동안 작업을 시도 하면 때 발생할 수 있습니다는 **RequestDisallowedByPolicy** hello 작업은 어떠한 오류 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17df3-106">When you try toodo an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents hello action be performed.</span></span> <span data-ttu-id="17df3-107">hello 아래에는 hello 오류의 샘플:</span><span class="sxs-lookup"><span data-stu-id="17df3-107">hello following is a sample of hello error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="17df3-108">문제 해결</span><span class="sxs-lookup"><span data-stu-id="17df3-108">Troubleshooting</span></span>

<span data-ttu-id="17df3-109">배포를 차단한 hello 정책에 대 한 세부 정보 tooretrieve hello 방법 중 하나를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="17df3-109">tooretrieve details about hello policy that blocked your deployment, use hello following one of hello methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="17df3-110">방법 1</span><span class="sxs-lookup"><span data-stu-id="17df3-110">Method 1</span></span>

<span data-ttu-id="17df3-111">PowerShell에서 해당 정책 식별자 hello로 제공 **Id** 배포를 차단한 hello 정책에 대 한 매개 변수 tooretrieve 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="17df3-111">In PowerShell, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="17df3-112">방법 2</span><span class="sxs-lookup"><span data-stu-id="17df3-112">Method 2</span></span> 

<span data-ttu-id="17df3-113">Azure CLI 2.0에서 hello 정책 정의의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="17df3-113">In Azure CLI 2.0, provide hello name of hello policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="17df3-114">해결 방법</span><span class="sxs-lookup"><span data-stu-id="17df3-114">Solution</span></span>

<span data-ttu-id="17df3-115">보안 또는 규정 준수를 위해 IT 부서는 공용 IP 주소, 네트워크 보안 그룹, 사용자 정의 경로 또는 경로 테이블 만들기를 금지하는 리소스 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17df3-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="17df3-116">Hello "증상" 섹션에에서 설명 된 hello 오류 메시지의 hello 샘플, hello 정책 이름은 **regionPolicyDefinition**, 있지만 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17df3-116">In hello sample of hello error message that is described in hello "Symptoms" section, hello policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="17df3-117">tooresolve이이 문제를 IT 부서 tooreview hello 리소스 정책에 사용 하 고 tooperform hello 정책 준수 작업을 요청 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17df3-117">tooresolve this problem, work with your IT department tooreview hello resource policies, and determine how tooperform hello requested action in compliance with those policies.</span></span>


<span data-ttu-id="17df3-118">자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="17df3-118">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="17df3-119">리소스 정책 개요</span><span class="sxs-lookup"><span data-stu-id="17df3-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="17df3-120">일반적인 배포 오류 - RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="17df3-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


