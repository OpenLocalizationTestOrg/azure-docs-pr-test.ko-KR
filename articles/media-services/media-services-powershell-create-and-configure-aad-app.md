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
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a><span data-ttu-id="25d4b-103">Azure AD 앱 toouse PowerShell toocreate hello Azure 미디어 서비스 API 사용</span><span class="sxs-lookup"><span data-stu-id="25d4b-103">Use PowerShell toocreate an Azure AD app toouse with hello Azure Media Services API</span></span>

<span data-ttu-id="25d4b-104">Azure Active Directory (Azure AD) 응용 프로그램 및 서비스 보안 주체 tooaccess Azure 미디어 서비스 리소스는 PowerShell toouse toocreate를 스크립팅 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="25d4b-104">Learn how toouse a PowerShell script toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="25d4b-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="25d4b-105">Prerequisites</span></span>

- <span data-ttu-id="25d4b-106">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="25d4b-106">An Azure account.</span></span> <span data-ttu-id="25d4b-107">계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="25d4b-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="25d4b-108">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="25d4b-108">A Media Services account.</span></span> <span data-ttu-id="25d4b-109">자세한 내용은 참조 [hello Azure 포털에에서 있는 Azure 미디어 서비스 계정을 만드는](media-services-portal-create-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="25d4b-109">For more information, see [Create an Azure Media Services account in hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="25d4b-110">Azure PowerShell 버전 0.8.8 이상.</span><span class="sxs-lookup"><span data-stu-id="25d4b-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="25d4b-111">자세한 내용은 참조 [어떻게 toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="25d4b-111">For more information, see [How toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="25d4b-112">Azure Resource Manager cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25d4b-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="25d4b-113">PowerShell을 사용하여 Azure AD 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="25d4b-113">Create an Azure AD app by using PowerShell</span></span>  

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

<span data-ttu-id="25d4b-114">자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="25d4b-114">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="25d4b-115">Azure PowerShell toocreate 서비스 보안 주체 tooaccess 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="25d4b-115">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="25d4b-116">Azure PowerShell을 사용하여 역할 기반 액세스 제어 관리</span><span class="sxs-lookup"><span data-stu-id="25d4b-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="25d4b-117">Toomanually는 인증서를 사용 하 여 디먼 응용 프로그램을 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="25d4b-117">How toomanually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="25d4b-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25d4b-118">Next steps</span></span>

<span data-ttu-id="25d4b-119">시작 [tooyour 계정에 파일 업로드](media-services-portal-upload-files.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="25d4b-119">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
