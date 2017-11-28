---
title: "aaaGrant 권한 toomany 응용 프로그램 tooaccess는 Azure 키 자격 증명 모음 | Microsoft Docs"
description: "Toogrant 권한 toomany 응용 프로그램 tooaccess 키 자격 증명 모음에 대해 알아봅니다"
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
ms.openlocfilehash: 5258149f939856f91b3848fc50399e58e5894f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a><span data-ttu-id="8769f-103">주요 자격 증명 모음 toomany 응용 프로그램 tooaccess 권한 부여</span><span class="sxs-lookup"><span data-stu-id="8769f-103">Grant permission toomany applications tooaccess a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="8769f-104">Q: 저는 있을 tooaccess 주요 자격 증명 모음은 응용 프로그램 중 (16 개).</span><span class="sxs-lookup"><span data-stu-id="8769f-104">Q: I have several (over 16) applications that need tooaccess a key vault.</span></span> <span data-ttu-id="8769f-105">Key Vault는 16개의 액세스 제어 항목만 허용하는데 어떻게 해결할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="8769f-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="8769f-106">Key Vault 액세스 제어 정책은 16개 항목만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8769f-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="8769f-107">그러나 Azure Active Directory 보안 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8769f-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="8769f-108">모든 hello 연결 서비스 보안 주체 toothis 보안 그룹 및 다음 액세스 toothis 보안 그룹 tooKey 자격 증명 모음을 부여를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8769f-108">Add all hello associated service principals toothis security group and then grant access toothis security group tooKey Vault.</span></span>

<span data-ttu-id="8769f-109">다음은 hello에 대 한 필수 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="8769f-109">Here are hello pre-requisites:</span></span>
* <span data-ttu-id="8769f-110">[Azure Active Directory V2 PowerShell 모듈 설치](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30)</span><span class="sxs-lookup"><span data-stu-id="8769f-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="8769f-111">[Azure PowerShell 설치](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="8769f-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="8769f-112">hello Azure Active Directory 테 넌 트에 사용 권한을 toocreate/편집 그룹이 야 toorun hello 다음 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8769f-112">toorun hello following commands, you need permissions toocreate/edit groups in hello Azure Active Directory tenant.</span></span> <span data-ttu-id="8769f-113">권한이 없는 경우 Azure Active Directory 관리자 toocontact를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8769f-113">If you don't have permissions, you may need toocontact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="8769f-114">이제 hello 다음 powershell에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8769f-114">Now run hello following commands in PowerShell.</span></span>

```powershell
# Connect tooAzure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members toothis group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members toothis group, in this fashion. 
 
# Set hello Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust hello permissions as required 
```

<span data-ttu-id="8769f-115">Toogrant 다른 응용 프로그램의 tooa 그룹 사용 권한 집합이 필요한 경우 이러한 응용 프로그램에 대 한 별도 Azure Active Directory 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8769f-115">If you need toogrant a different set of permissions tooa group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8769f-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8769f-116">Next steps</span></span>

<span data-ttu-id="8769f-117">너무 방법에 대 한 자세한[주요 자격 증명 모음 보안](key-vault-secure-your-key-vault.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8769f-117">Learn more about how too[Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
