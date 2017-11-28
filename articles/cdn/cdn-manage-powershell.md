---
title: "PowerShell과 함께 Azure CDN aaaManage | Microsoft Docs"
description: "Toouse Azure PowerShell cmdlet toomanage Azure CDN hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 269373136d4ef018e4d31f147456b4be2253b463
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="31166-103">PowerShell을 사용하여 Azure CDN 관리</span><span class="sxs-lookup"><span data-stu-id="31166-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="31166-104">PowerShell은 Azure CDN 프로필 및 끝점 hello 가장 유연한 방법 toomanage 중 하나를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-104">PowerShell provides one of hello most flexible methods toomanage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="31166-105">대화형으로 또는 tooautomate 관리 작업 스크립트를 작성 하 여 PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31166-105">You can use PowerShell interactively or by writing scripts tooautomate management tasks.</span></span>  <span data-ttu-id="31166-106">이 자습서에서는 여러 설명 hello 가장 일반적인 작업을 수행할 수 있는 PowerShell toomanage Azure CDN 프로필 및 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="31166-106">This tutorial demonstrates several of hello most common tasks you can accomplish with PowerShell toomanage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31166-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31166-107">Prerequisites</span></span>
<span data-ttu-id="31166-108">toouse PowerShell toomanage 사용자 프로필 Azure CDN과 끝점을 hello Azure PowerShell 모듈이 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-108">toouse PowerShell toomanage your Azure CDN profiles and endpoints, you must have hello Azure PowerShell module installed.</span></span>  <span data-ttu-id="31166-109">toolearn 어떻게 tooinstall Azure PowerShell tooAzure hello를 사용 하 여 연결 `Login-AzureRmAccount` cmdlet 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-109">toolearn how tooinstall Azure PowerShell and connect tooAzure using hello `Login-AzureRmAccount` cmdlet, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31166-110">`Login-AzureRmAccount`에 로그인해야 Azure PowerShell cmdlet을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31166-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a><span data-ttu-id="31166-111">Hello Azure CDN cmdlet 목록</span><span class="sxs-lookup"><span data-stu-id="31166-111">Listing hello Azure CDN cmdlets</span></span>
<span data-ttu-id="31166-112">Hello를 사용 하 여 모든 hello Azure CDN cmdlet을 나열할 수 있습니다 `Get-Command` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31166-112">You can list all hello Azure CDN cmdlets using hello `Get-Command` cmdlet.</span></span>

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

## <a name="getting-help"></a><span data-ttu-id="31166-113">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="31166-113">Getting help</span></span>
<span data-ttu-id="31166-114">Hello를 사용 하 여 이러한 cmdlet를 사용 하 여 도움말을 가져와서 `Get-Help` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31166-114">You can get help with any of these cmdlets using hello `Get-Help` cmdlet.</span></span>  <span data-ttu-id="31166-115">`Get-Help` 는 사용량 및 구문을 제공하며 선택적으로 예제를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

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
    toosee hello examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="31166-116">기존 Azure CDN 프로필 목록화</span><span class="sxs-lookup"><span data-stu-id="31166-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="31166-117">hello `Get-AzureRmCdnProfile` cmdlet 매개 변수 없이 모든 기존 CDN 프로필을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-117">hello `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="31166-118">이 출력에는 열거형에 대 한 파이프 된 toocmdlets 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31166-118">This output can be piped toocmdlets for enumeration.</span></span>

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="31166-119">Hello 프로필 이름 및 리소스 그룹을 지정 하 여 단일 프로필을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31166-119">You can also return a single profile by specifying hello profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="31166-120">가능한 toohave로 서로 다른 리소스 그룹에 이름과 같은 이름을 hello로 여러 CDN 프로필은</span><span class="sxs-lookup"><span data-stu-id="31166-120">It is possible toohave multiple CDN profiles with hello same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="31166-121">Hello 생략 `ResourceGroupName` 매개 변수 이름이 일치 하는 모든 프로필을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-121">Omitting hello `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="31166-122">기존 CDN 끝점 목록화</span><span class="sxs-lookup"><span data-stu-id="31166-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="31166-123">`Get-AzureRmCdnEndpoint`개별 끝점 또는 프로필에서 모든 hello 끝점을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31166-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all hello endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of hello endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of hello endpoints on all of hello profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of hello endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="31166-124">CDN 프로필 및 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="31166-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="31166-125">`New-AzureRmCdnProfile`및 `New-AzureRmCdnEndpoint` 은 사용 되는 toocreate CDN 프로필 및 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="31166-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used toocreate CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="31166-126">끝점 이름 가용성 확인</span><span class="sxs-lookup"><span data-stu-id="31166-126">Checking endpoint name availability</span></span>
<span data-ttu-id="31166-127">`Get-AzureRmCdnEndpointNameAvailability` 은 끝점 이름을 사용할 수 있는지 여부를 나타내는 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="31166-128">사용자 지정 도메인 추가</span><span class="sxs-lookup"><span data-stu-id="31166-128">Adding a custom domain</span></span>
<span data-ttu-id="31166-129">`New-AzureRmCdnCustomDomain`사용자 지정 도메인 이름을 tooan 기존 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-129">`New-AzureRmCdnCustomDomain` adds a custom domain name tooan existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31166-130">에 설명 된 대로 DNS 공급자로 CNAME hello를 설정 해야 [어떻게 toomap 사용자 지정 도메인 tooContent CDN (배달 네트워크) 끝점](cdn-map-content-to-custom-domain.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-130">You must set up hello CNAME with your DNS provider as described in [How toomap Custom Domain tooContent Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="31166-131">Hello 매핑을 사용 하 여 끝점을 수정 하기 전에 테스트할 수 있습니다 `Test-AzureRmCdnCustomDomain`합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-131">You can test hello mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check hello mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create hello custom domain on hello endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="31166-132">끝점 수정</span><span class="sxs-lookup"><span data-stu-id="31166-132">Modifying an endpoint</span></span>
<span data-ttu-id="31166-133">`Set-AzureRmCdnEndpoint` 은 기존 끝점을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="31166-134">CDN 자산 제거/사전 로드</span><span class="sxs-lookup"><span data-stu-id="31166-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="31166-135">`Unpublish-AzureRmCdnEndpointContent`은 캐시된 자산을 제거하며, `Publish-AzureRmCdnEndpointContent`는 자산을 지원되는 끝점에 사전 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="31166-136">CDN 끝점 시작/중지</span><span class="sxs-lookup"><span data-stu-id="31166-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="31166-137">`Start-AzureRmCdnEndpoint`및 `Stop-AzureRmCdnEndpoint` 사용된 toostart 수 있고 개별 끝점 또는 끝점 그룹을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used toostart and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="31166-138">CDN 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="31166-138">Deleting CDN resources</span></span>
<span data-ttu-id="31166-139">`Remove-AzureRmCdnProfile`및 `Remove-AzureRmCdnEndpoint` 사용된 tooremove 프로필 및 끝점 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31166-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used tooremove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="31166-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31166-140">Next Steps</span></span>
<span data-ttu-id="31166-141">자세한 내용은 방법 tooautomate Azure CDN와 [.NET](cdn-app-dev-net.md) 또는 [Node.js](cdn-app-dev-node.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-141">Learn how tooautomate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="31166-142">toolearn CDN 기능에 대 한 참조 [CDN 개요](cdn-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="31166-142">toolearn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

