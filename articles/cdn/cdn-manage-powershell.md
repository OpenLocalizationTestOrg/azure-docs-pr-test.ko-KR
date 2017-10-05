---
title: "PowerShell을 사용하여 Azure CDN 관리 | Microsoft Docs"
description: "Azure PowerShell cmdlet을 사용하여 Azure CDN을 관리하는 방법에 대해 알아봅니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: fb6f57a5-6e26-4847-8fd9-b51fb05a79eb
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5bd2eed7b34cafa43e8f38279890405d4ae55568
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="b45d6-103">PowerShell을 사용하여 Azure CDN 관리</span><span class="sxs-lookup"><span data-stu-id="b45d6-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="b45d6-104">PowerShell은 Azure CDN 프로필 및 끝점을 관리하는 매우 유연한 방법 중 하나를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-104">PowerShell provides one of the most flexible methods to manage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="b45d6-105">PowerShell을 대화형으로 또는 관리 작업을 자동화하는 스크립트를 작성하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-105">You can use PowerShell interactively or by writing scripts to automate management tasks.</span></span>  <span data-ttu-id="b45d6-106">이 자습서에서는 PowerShell을 사용하여 Azure CDN 프로필 및 끝점의 관리를 달성할 수 있는 가장 일반적인 작업 몇 가지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-106">This tutorial demonstrates several of the most common tasks you can accomplish with PowerShell to manage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b45d6-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b45d6-107">Prerequisites</span></span>
<span data-ttu-id="b45d6-108">PowerShell을 사용하여 Azure CDN 프로필 및 끝점을 관리하려면 Azure PowerShell 모듈이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-108">To use PowerShell to manage your Azure CDN profiles and endpoints, you must have the Azure PowerShell module installed.</span></span>  <span data-ttu-id="b45d6-109">Azure PowerShell을 설치하고 `Login-AzureRmAccount` cmdlet을 사용하여 Azure에 연결하는 방법을 알아보려면 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b45d6-109">To learn how to install Azure PowerShell and connect to Azure using the `Login-AzureRmAccount` cmdlet, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b45d6-110">`Login-AzureRmAccount`에 로그인해야 Azure PowerShell cmdlet을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-the-azure-cdn-cmdlets"></a><span data-ttu-id="b45d6-111">Azure CDN cmdlet 목록화</span><span class="sxs-lookup"><span data-stu-id="b45d6-111">Listing the Azure CDN cmdlets</span></span>
<span data-ttu-id="b45d6-112">`Get-Command` cmdlet을 사용하여 모든 Azure CDN cmdlet을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-112">You can list all the Azure CDN cmdlets using the `Get-Command` cmdlet.</span></span>

```text
PS C:\> Get-Command -Module AzureRM.Cdn

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Get-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpointNameAvailability             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfileSsoUrl                        2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Publish-AzureRmCdnEndpointContent                  2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnCustomDomain                      2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnEndpoint                          2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnProfile                           2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Start-AzureRmCdnEndpoint                           2.0.0      AzureRm.Cdn
Cmdlet          Stop-AzureRmCdnEndpoint                            2.0.0      AzureRm.Cdn
Cmdlet          Test-AzureRmCdnCustomDomain                        2.0.0      AzureRm.Cdn
Cmdlet          Unpublish-AzureRmCdnEndpointContent                2.0.0      AzureRm.Cdn
```

## <a name="getting-help"></a><span data-ttu-id="b45d6-113">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="b45d6-113">Getting help</span></span>
<span data-ttu-id="b45d6-114">`Get-Help` cmdlet을 사용하여 이러한 cmdlet에 대한 도움말을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-114">You can get help with any of these cmdlets using the `Get-Help` cmdlet.</span></span>  <span data-ttu-id="b45d6-115">`Get-Help` 는 사용량 및 구문을 제공하며 선택적으로 예제를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

```text
PS C:\> Get-Help Get-AzureRmCdnProfile

NAME
    Get-AzureRmCdnProfile

SYNOPSIS
    Gets an Azure CDN profile.


SYNTAX
    Get-AzureRmCdnProfile [-ProfileName <String>] [-ResourceGroupName <String>] [-InformationAction
    <ActionPreference>] [-InformationVariable <String>] [<CommonParameters>]


DESCRIPTION
    Gets an Azure CDN profile and all related information.


RELATED LINKS

REMARKS
    To see the examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="b45d6-116">기존 Azure CDN 프로필 목록화</span><span class="sxs-lookup"><span data-stu-id="b45d6-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="b45d6-117">매개 변수 없는 `Get-AzureRmCdnProfile` cmdlet은 모든 기존 CDN 프로필을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-117">The `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="b45d6-118">이 출력은 열거형에 대한 cmdlet으로 파이프될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-118">This output can be piped to cmdlets for enumeration.</span></span>

```powershell
# Output the name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="b45d6-119">또한 프로필 이름 및 리소스 그룹을 지정하여 단일 프로필을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-119">You can also return a single profile by specifying the profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="b45d6-120">다른 리소스 그룹에 속하기만 하다면 같은 이름을 가진 여러 CDN 프로필이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-120">It is possible to have multiple CDN profiles with the same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="b45d6-121">`ResourceGroupName` 매개 변수를 생략함년 일치하는 이름을 가진 모든 프로필이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-121">Omitting the `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="b45d6-122">기존 CDN 끝점 목록화</span><span class="sxs-lookup"><span data-stu-id="b45d6-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="b45d6-123">`Get-AzureRmCdnEndpoint` 은 개별 끝점 또는 프로필의 모든 끝점을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all the endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of the endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of the endpoints on all of the profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of the endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="b45d6-124">CDN 프로필 및 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="b45d6-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="b45d6-125">`New-AzureRmCdnProfile` 및 `New-AzureRmCdnEndpoint`는 CDN 프로필 및 끝점을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used to create CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="b45d6-126">끝점 이름 가용성 확인</span><span class="sxs-lookup"><span data-stu-id="b45d6-126">Checking endpoint name availability</span></span>
<span data-ttu-id="b45d6-127">`Get-AzureRmCdnEndpointNameAvailability` 은 끝점 이름을 사용할 수 있는지 여부를 나타내는 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message to the console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="b45d6-128">사용자 지정 도메인 추가</span><span class="sxs-lookup"><span data-stu-id="b45d6-128">Adding a custom domain</span></span>
<span data-ttu-id="b45d6-129">`New-AzureRmCdnCustomDomain` 은 기존 끝점에 사용자 지정 도메인 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-129">`New-AzureRmCdnCustomDomain` adds a custom domain name to an existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b45d6-130">[사용자 지정 도메인을 콘텐츠 배달 네트워크(CDN) 끝점에 매핑하는 방법](cdn-map-content-to-custom-domain.md)에서 설명한 대로 DNS 공급자를 통해 CNAME을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-130">You must set up the CNAME with your DNS provider as described in [How to map Custom Domain to Content Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="b45d6-131">`Test-AzureRmCdnCustomDomain`를 사용하여 끝점을 수정하기 전에 매핑을 시험해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-131">You can test the mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check the mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create the custom domain on the endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="b45d6-132">끝점 수정</span><span class="sxs-lookup"><span data-stu-id="b45d6-132">Modifying an endpoint</span></span>
<span data-ttu-id="b45d6-133">`Set-AzureRmCdnEndpoint` 은 기존 끝점을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save the changed endpoint and apply the changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="b45d6-134">CDN 자산 제거/사전 로드</span><span class="sxs-lookup"><span data-stu-id="b45d6-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="b45d6-135">`Unpublish-AzureRmCdnEndpointContent`은 캐시된 자산을 제거하며, `Publish-AzureRmCdnEndpointContent`는 자산을 지원되는 끝점에 사전 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="b45d6-136">CDN 끝점 시작/중지</span><span class="sxs-lookup"><span data-stu-id="b45d6-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="b45d6-137">`Start-AzureRmCdnEndpoint` 및 `Stop-AzureRmCdnEndpoint`를 사용하여 개별 끝점 또는 끝점 그룹을 시작 및 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used to start and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop the cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="b45d6-138">CDN 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="b45d6-138">Deleting CDN resources</span></span>
<span data-ttu-id="b45d6-139">`Remove-AzureRmCdnProfile` 및 `Remove-AzureRmCdnEndpoint`를 사용하여 프로필 및 끝점을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used to remove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all the endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="b45d6-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b45d6-140">Next Steps</span></span>
<span data-ttu-id="b45d6-141">[.NET](cdn-app-dev-net.md) 또는 [Node.js](cdn-app-dev-node.md)를 사용하여 Azure CDN을 자동화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b45d6-141">Learn how to automate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="b45d6-142">CDN 기능에 대해 알아보려면 [CDN 개요](cdn-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b45d6-142">To learn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

