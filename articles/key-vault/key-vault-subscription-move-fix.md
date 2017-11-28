---
title: "구독 이동 후 aaaChange hello 주요 자격 증명 모음 테 넌 트 ID | Microsoft Docs"
description: "키 자격 증명 모음 구독 된 후에 대 한 tooswitch hello 테 넌 트 ID tooa 다른 테 넌 트를 이동 하는 방법에 대해 알아봅니다"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 4d0607208c61c57959439d2d0bd8feade4141fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="f312e-103">구독 이동 후에 주요 자격 증명 모음 테넌트 ID 변경</span><span class="sxs-lookup"><span data-stu-id="f312e-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="f312e-104">Q: 내 구독에서 테 넌 트 A tootenant B. 옮겨졌습니다. 어떻게 내 기존 키 자격 증명 모음에 대 한 hello 테 넌 트 ID를 변경 하 고 테 넌 트 B의에서 보안 주체에 대 한 올바른 Acl 설정?</span><span class="sxs-lookup"><span data-stu-id="f312e-104">Q: My subscription was moved from tenant A tootenant B. How do I change hello tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="f312e-105">구독에 새 키 자격 증명 모음을 만들 때 자동으로 동률된 toohello 해당 구독에 대 한 기본 Azure Active Directory 테 넌 트 ID 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f312e-105">When you create a new key vault in a subscription, it is automatically tied toohello default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="f312e-106">모든 액세스 정책 항목 제한은 toothis 테 넌 트 ID도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f312e-106">All access policy entries are also tied toothis tenant ID.</span></span> <span data-ttu-id="f312e-107">Azure 구독을 이동 하면 테 넌 트에서 tootenant B에서 기존 키 자격 증명 모음에 액세스할 수 없는 hello 보안 주체 (사용자 및 응용 프로그램)에서 테 넌 트 B. toofix이이 문제를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f312e-107">When you move your Azure subscription from tenant A tootenant B, your existing key vaults are inaccessible by hello principals (users and applications) in tenant B. toofix this issue, you need to:</span></span>

* <span data-ttu-id="f312e-108">연결 된 모든 기존 키 자격 증명 모음에서이 구독 tootenant B. hello 테 넌 트 ID를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f312e-108">Change hello tenant ID associated with all existing key vaults in this subscription tootenant B.</span></span>
* <span data-ttu-id="f312e-109">모든 기존 액세스 정책 항목을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f312e-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="f312e-110">테넌트 B와 연결된 새 액세스 정책 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f312e-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="f312e-111">예를 들어 있으면 주요 자격 증명 모음 'myvault' 테 넌 트 A tootenant B 여기의에서 이동 된 구독에서 어떻게 toochange hello이 주요 자격 증명 모음에 대 한 테 넌 트 ID와 이전 액세스 정책을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f312e-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A tootenant B, here's how toochange hello tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="f312e-112">테 넌 트 A hello 이동 하기 전에이 자격 증명이 모음 이어서 hello의 원래 값 **$vault 합니다. Properties.TenantId** 는 테 넌 트 A while **(Get AzureRmContext). Tenant.TenantId** B. 테 넌 트은</span><span class="sxs-lookup"><span data-stu-id="f312e-112">Because this vault was in tenant A before hello move, hello original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="f312e-113">이제 hello 올바른 테 넌 트 ID와 연결 된 자격 증명 모음 및 오래 된 액세스 정책 항목 삭제 되므로 설정 새로운 액세스 정책 항목을 [Set-azurermkeyvaultaccesspolicy](https://msdn.microsoft.com/library/mt603625.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f312e-113">Now that your vault is associated with hello correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f312e-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f312e-114">Next steps</span></span>
<span data-ttu-id="f312e-115">Azure 키 자격 증명 모음에 대 한 질문이 있으면 방문 hello [Azure 키 자격 증명 모음 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)합니다.</span><span class="sxs-lookup"><span data-stu-id="f312e-115">If you have questions about Azure Key Vault, visit hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

