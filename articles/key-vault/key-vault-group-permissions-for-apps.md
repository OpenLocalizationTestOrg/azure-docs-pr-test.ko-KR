---
title: "여러 응용 프로그램에 Azure Key Vault 액세스 권한 부여 | Microsoft Docs"
description: "여러 응용 프로그램에 Key Vault 액세스 권한을 부여하는 방법을 알아봅니다."
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 785d4e40-fb7b-485a-8cbc-d9c8c87708e6
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: ambapat
ms.openlocfilehash: f58b633de2e4b5702ff2df9b3722662b09510200
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permission-to-many-applications-to-access-a-key-vault"></a><span data-ttu-id="b28f4-103">여러 응용 프로그램에 Key Vault 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="b28f4-103">Grant permission to many applications to access a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-to-access-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="b28f4-104">Q: Key Vault에 액세스해야 하는 여러 개의 응용 프로그램(16개 초과)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f4-104">Q: I have several (over 16) applications that need to access a key vault.</span></span> <span data-ttu-id="b28f4-105">Key Vault는 16개의 액세스 제어 항목만 허용하는데 어떻게 해결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b28f4-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="b28f4-106">Key Vault 액세스 제어 정책은 16개 항목만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f4-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="b28f4-107">그러나 Azure Active Directory 보안 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b28f4-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="b28f4-108">관련된 모든 서비스 주체를 이 보안 그룹에 추가한 다음 Key Vault에 이 보안 그룹에 대한 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f4-108">Add all the associated service principals to this security group and then grant access to this security group to Key Vault.</span></span>

<span data-ttu-id="b28f4-109">다음은 필수 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="b28f4-109">Here are the pre-requisites:</span></span>
* <span data-ttu-id="b28f4-110">[Azure Active Directory V2 PowerShell 모듈 설치](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30)</span><span class="sxs-lookup"><span data-stu-id="b28f4-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="b28f4-111">[Azure PowerShell 설치](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="b28f4-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="b28f4-112">다음 명령을 실행하려면 Azure Active Directory 테넌트의 그룹 만들기/편집 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f4-112">To run the following commands, you need permissions to create/edit groups in the Azure Active Directory tenant.</span></span> <span data-ttu-id="b28f4-113">권한이 없는 경우 Azure Active Directory 관리자에게 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f4-113">If you don't have permissions, you may need to contact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="b28f4-114">이제 PowerShell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b28f4-114">Now run the following commands in PowerShell.</span></span>

```powershell
# Connect to Azure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members to this group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members to this group, in this fashion. 
 
# Set the Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust the permissions as required 
```

<span data-ttu-id="b28f4-115">응용 프로그램 그룹에 다른 권한 집합을 부여해야 할 경우 이러한 응용 프로그램에 대해 별도의 Azure Active Directory 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b28f4-115">If you need to grant a different set of permissions to a group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b28f4-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b28f4-116">Next steps</span></span>

<span data-ttu-id="b28f4-117">[Key Vault 보안 설정](key-vault-secure-your-key-vault.md)에 대해 좀 더 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b28f4-117">Learn more about how to [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
