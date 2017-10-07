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
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a>주요 자격 증명 모음 toomany 응용 프로그램 tooaccess 권한 부여

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a>Q: 저는 있을 tooaccess 주요 자격 증명 모음은 응용 프로그램 중 (16 개). Key Vault는 16개의 액세스 제어 항목만 허용하는데 어떻게 해결할 수 있나요?

Key Vault 액세스 제어 정책은 16개 항목만 지원합니다. 그러나 Azure Active Directory 보안 그룹을 만들 수 있습니다. 모든 hello 연결 서비스 보안 주체 toothis 보안 그룹 및 다음 액세스 toothis 보안 그룹 tooKey 자격 증명 모음을 부여를 추가 합니다.

다음은 hello에 대 한 필수 정보입니다.
* [Azure Active Directory V2 PowerShell 모듈 설치](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30)
* [Azure PowerShell 설치](/powershell/azure/overview)
* hello Azure Active Directory 테 넌 트에 사용 권한을 toocreate/편집 그룹이 야 toorun hello 다음 명령입니다. 권한이 없는 경우 Azure Active Directory 관리자 toocontact를 할 수 있습니다.

이제 hello 다음 powershell에서 명령을 실행 합니다.

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

Toogrant 다른 응용 프로그램의 tooa 그룹 사용 권한 집합이 필요한 경우 이러한 응용 프로그램에 대 한 별도 Azure Active Directory 보안 그룹을 만듭니다.

## <a name="next-steps"></a>다음 단계

너무 방법에 대 한 자세한[주요 자격 증명 모음 보안](key-vault-secure-your-key-vault.md)합니다.
