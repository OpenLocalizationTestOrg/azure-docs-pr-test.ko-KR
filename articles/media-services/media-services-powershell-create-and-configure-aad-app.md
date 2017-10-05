---
title: "PowerShell을 사용하여 Azure AD 앱 만들기 및 Azure Media Services API 액세스 | Microsoft Docs"
description: "PowerShell을 사용하여 Azure AD(Azure Active Directory) 앱을 만들고 Azure Media Services API에 액세스하도록 설정하는 방법을 알아봅니다."
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
ms.openlocfilehash: eea0f3a03dd77ce56484f32b192299bd97c05300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-create-an-azure-ad-app-to-use-with-the-azure-media-services-api"></a><span data-ttu-id="8cf48-103">PowerShell을 사용하여 Azure Media Services API와 함께 사용할 Azure AD 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="8cf48-103">Use PowerShell to create an Azure AD app to use with the Azure Media Services API</span></span>

<span data-ttu-id="8cf48-104">PowerShell 스크립트를 사용하여 Azure Media Services 리소스에 액세스하기 위한 Azure AD(Azure Active Directory) 응용 프로그램 및 서비스 주체를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8cf48-104">Learn how to use a PowerShell script to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="8cf48-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8cf48-105">Prerequisites</span></span>

- <span data-ttu-id="8cf48-106">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="8cf48-106">An Azure account.</span></span> <span data-ttu-id="8cf48-107">계정이 없는 경우 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="8cf48-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="8cf48-108">미디어 서비스 계정.</span><span class="sxs-lookup"><span data-stu-id="8cf48-108">A Media Services account.</span></span> <span data-ttu-id="8cf48-109">자세한 내용은 [Azure Portal에서 Azure Media Services 계정 만들기](media-services-portal-create-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cf48-109">For more information, see [Create an Azure Media Services account in the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="8cf48-110">Azure PowerShell 버전 0.8.8 이상.</span><span class="sxs-lookup"><span data-stu-id="8cf48-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="8cf48-111">자세한 내용은 [Azure PowerShell 사용 방법](https://docs.microsoft.com/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cf48-111">For more information, see [How to use Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="8cf48-112">Azure Resource Manager cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8cf48-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="8cf48-113">PowerShell을 사용하여 Azure AD 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="8cf48-113">Create an Azure AD app by using PowerShell</span></span>  

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
    # Sleep here for a few seconds to allow the service principal application to become active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

<span data-ttu-id="8cf48-114">자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cf48-114">For more information, see the following articles:</span></span>

- [<span data-ttu-id="8cf48-115">Azure PowerShell을 사용하여 리소스에 액세스하는 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="8cf48-115">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="8cf48-116">Azure PowerShell을 사용하여 역할 기반 액세스 제어 관리</span><span class="sxs-lookup"><span data-stu-id="8cf48-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="8cf48-117">인증서를 사용하여 디먼 앱을 수동으로 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="8cf48-117">How to manually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="8cf48-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8cf48-118">Next steps</span></span>

<span data-ttu-id="8cf48-119">[계정에 파일 업로드](media-services-portal-upload-files.md) 시작</span><span class="sxs-lookup"><span data-stu-id="8cf48-119">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
