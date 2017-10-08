---
title: "Azure AD 앱 tooaccess aaaUse PowerShell toocreate hello Azure 미디어 서비스 API | Microsoft Docs"
description: "자세한 방법을 toouse PowerShell toocreate Azure Active Directory (Azure AD) 응용 프로그램 고 tooaccess hello Azure 미디어 서비스 API를 설정 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 1a8b4a53ad10b559f6ee4242b95c5bd15ee8e903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a>Azure AD 앱 toouse PowerShell toocreate hello Azure 미디어 서비스 API 사용

Azure Active Directory (Azure AD) 응용 프로그램 및 서비스 보안 주체 tooaccess Azure 미디어 서비스 리소스는 PowerShell toouse toocreate를 스크립팅 하는 방법에 대해 알아봅니다.  

## <a name="prerequisites"></a>필수 조건

- Azure 계정. 계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작하세요. 
- Media Services 계정. 자세한 내용은 참조 [hello Azure 포털에에서 있는 Azure 미디어 서비스 계정을 만드는](media-services-portal-create-account.md)합니다.
- Azure PowerShell 버전 0.8.8 이상. 자세한 내용은 참조 [어떻게 toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)합니다.
- Azure Resource Manager cmdlet.  

## <a name="create-an-azure-ad-app-by-using-powershell"></a>PowerShell을 사용하여 Azure AD 앱 만들기  

```powershell
Login-AzureRmAccount
Import-Module AzureRM.Resources
Set-AzureRmContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

자세한 내용은 다음 문서는 hello 참조:

- [Azure PowerShell toocreate 서비스 보안 주체 tooaccess 리소스 사용](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [Azure PowerShell을 사용하여 역할 기반 액세스 제어 관리](../active-directory/role-based-access-control-manage-access-powershell.md)
- [Toomanually는 인증서를 사용 하 여 디먼 응용 프로그램을 구성 하는 방법](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>다음 단계

시작 [tooyour 계정에 파일 업로드](media-services-portal-upload-files.md)합니다.
