---
title: "aaaUse Azure RemoteApp과 함께 PowerShell cmdlet | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure RemoteApp에서 Windows PowerShell cmdlet."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a><span data-ttu-id="884a9-103">Azure RemoteApp에서 Windows PowerShell cmdlet 사용</span><span class="sxs-lookup"><span data-stu-id="884a9-103">Use Windows PowerShell cmdlets with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="884a9-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="884a9-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

 <span data-ttu-id="884a9-106">Azure RemoteApp PowerShell cmdlet tooadminister hello를 사용 하 여 수 있으며 사용자 컬렉션을 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-106">You can use hello Azure RemoteApp PowerShell cmdlets tooadminister and maintain your collections.</span></span> <span data-ttu-id="884a9-107">다음 시작 정보 tooget hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-107">Use hello following information tooget started.</span></span>

## <a name="get-hello-cmdlets"></a><span data-ttu-id="884a9-108">Hello cmdlet 가져오기</span><span class="sxs-lookup"><span data-stu-id="884a9-108">Get hello cmdlets</span></span>
- - -
<span data-ttu-id="884a9-109">먼저 hello Azure Powershell cmdlet 다운로드 [여기](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlet에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-109">First download hello Azure Powershell cmdlets [here](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlets are included in it.</span></span> 

<span data-ttu-id="884a9-110">체크 아웃 hello [Azure RemoteApp cmdlet 도움말](/powershell/module/azure?view=azuresmps-3.7.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-110">Check out hello [Azure RemoteApp cmdlet help](/powershell/module/azure?view=azuresmps-3.7.0).</span></span>

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a><span data-ttu-id="884a9-111">Azure cmdlet toouse 구독 구성</span><span class="sxs-lookup"><span data-stu-id="884a9-111">Configure Azure cmdlets toouse your subscription</span></span>
- - -
<span data-ttu-id="884a9-112">에 따라 [이 가이드](/powershell/azure/overview) Azure 구독에 대해 hello cmdlet을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-112">Follow [this guide](/powershell/azure/overview) so you can use hello cmdlets against your Azure subscription.</span></span>

<span data-ttu-id="884a9-113">이러한 단계 tooget 신속 하 게 시작을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-113">You can use these steps tooget started quickly:</span></span>

1. <span data-ttu-id="884a9-114">다운로드 및 설치 hello [Azure PowerShell cmdlet](http://go.microsoft.com/?linkid=9811175)합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-114">Download and install hello [Azure PowerShell cmdlets](http://go.microsoft.com/?linkid=9811175).</span></span>
2. <span data-ttu-id="884a9-115">Microsoft Azure PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-115">Launch Microsoft Azure PowerShell.</span></span>
3. <span data-ttu-id="884a9-116">실행 **Add-azureaccount** tooauthenticate tooyour Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="884a9-116">Run **Add-AzureAccount** tooauthenticate tooyour Azure subscription.</span></span> <span data-ttu-id="884a9-117">입력 메시지가 표시 되 면 동일한 사용자 이름 및 암호 toosign tooAzure 포털에서 사용 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-117">When prompted, enter hello same user name and password that you use toosign in tooAzure portal.</span></span>  
4. <span data-ttu-id="884a9-118">실행 **Get-azuresubscription** 사용자 계정과 연결 된 toolist hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-118">Run **Get-AzureSubscription** toolist hello subscriptions associated with your user account.</span></span> 
5. <span data-ttu-id="884a9-119">실행 **선택-SubscriptionName &lt;구독 이름&gt;**  또는 **Select-azuresubscription SubscriptionId &lt;구독 ID&gt;**  toospecify hello 구독 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-119">Run **Select-AzureSubscription -SubscriptionName &lt;subscription name&gt;** or **Select-AzureSubscription -SubscriptionId &lt;subscription ID&gt;** toospecify hello subscription toouse.</span></span>

<span data-ttu-id="884a9-120">축, Azure PowerShell 콘솔은 구성 및 준비 toouse.</span><span class="sxs-lookup"><span data-stu-id="884a9-120">Congratulations, your Azure PowerShell console is configured and ready toouse.</span></span> <span data-ttu-id="884a9-121">필요가 있다는 것 toorepeate 2 ~ 5 단계 hello hello Azure PowerShell 콘솔을 시작할 때마다 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-121">Be aware that you'll need toorepeate steps 2 through 5 each time you start hello hello Azure PowerShell console.</span></span>  


## <a name="list-all-collections"></a><span data-ttu-id="884a9-122">모든 컬렉션 나열</span><span class="sxs-lookup"><span data-stu-id="884a9-122">List all collections</span></span>
- - -
     <span data-ttu-id="884a9-123">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="884a9-123">Get-AzureRemoteAppCollection</span></span>

## <a name="delete-a-collection"></a><span data-ttu-id="884a9-124">컬렉션 삭제</span><span class="sxs-lookup"><span data-stu-id="884a9-124">Delete a collection</span></span>
- - -
    <span data-ttu-id="884a9-125">Remove-AzureRemoteAppCollection <enter collection name></span><span class="sxs-lookup"><span data-stu-id="884a9-125">Remove-AzureRemoteAppCollection <enter collection name></span></span>

<span data-ttu-id="884a9-126">예제: `Remove-AzureRemoteAppCollection ContosoProduction`.</span><span class="sxs-lookup"><span data-stu-id="884a9-126">Example:  `Remove-AzureRemoteAppCollection ContosoProduction`.</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="884a9-127">클라우드 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="884a9-127">Create a cloud collection</span></span>
- - -
<span data-ttu-id="884a9-128">아주 간단, hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-128">It's simple, run hello following command:</span></span>

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

<span data-ttu-id="884a9-129">명령 위에 hello (Excel, OneNote, Outlook, PowerPoint, Visio 및 Word)의 Microsoft Office 365 응용 프로그램에서 자동으로 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-129">hello above command automatically publishes Microsoft Office 365 applications (Excel, OneNote, Outlook, PowerPoint, Visio and Word).</span></span>

<span data-ttu-id="884a9-130">컬렉션 만들기가 30 분 또는 toocomplete 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-130">Collection creation can take 30 minutes or longer toocomplete.</span></span> <span data-ttu-id="884a9-131">따라서 이 명령은 다음과 같이 사용할 수 있는 추적 ID를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-131">Therefore, this command returns a tracking ID that you can use as follows:</span></span>

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

<span data-ttu-id="884a9-132">Hello 컬렉션을 완료 한 후 다음 명령을 hello로 사용자 toohello 컬렉션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-132">After hello collection is done, you can add users toohello collection with hello following command:</span></span>

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

<span data-ttu-id="884a9-133">완료되었습니다!</span><span class="sxs-lookup"><span data-stu-id="884a9-133">And you're done!</span></span> <span data-ttu-id="884a9-134">해당 사용자 수 tooconnect toohello hello Azure RemoteApp 클라이언트를 찾을 수를 사용 하 여 응용 프로그램 해야 [여기](https://www.remoteapp.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="884a9-134">That user should be able tooconnect toohello application using hello Azure RemoteApp client found [here](https://www.remoteapp.windowsazure.com/).</span></span>

## <a name="available-cmdlets"></a><span data-ttu-id="884a9-135">사용할 수 있는 cmdlet</span><span class="sxs-lookup"><span data-stu-id="884a9-135">Available cmdlets</span></span>
<span data-ttu-id="884a9-136">다양 한 다른 명령을, hello 설명서에 곧 제공 될 예정:</span><span class="sxs-lookup"><span data-stu-id="884a9-136">There are lots of other commands that we have, hello documentation for them will be coming shortly:</span></span>

<span data-ttu-id="884a9-137">기본 RemoteApp 컬렉션 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="884a9-137">Basic RemoteApp Collection cmdlets:</span></span> 

* <span data-ttu-id="884a9-138">New-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="884a9-138">New-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="884a9-139">Get-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="884a9-139">Get-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="884a9-140">Set-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="884a9-140">Set-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="884a9-141">Update-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="884a9-141">Update-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="884a9-142">Remove-AzureRemoteAppCollection</span><span class="sxs-lookup"><span data-stu-id="884a9-142">Remove-AzureRemoteAppCollection</span></span>
* <span data-ttu-id="884a9-143">Add-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="884a9-143">Add-AzureRemoteAppUser</span></span>
* <span data-ttu-id="884a9-144">Get-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="884a9-144">Get-AzureRemoteAppUser</span></span>
* <span data-ttu-id="884a9-145">Remove-AzureRemoteAppUser</span><span class="sxs-lookup"><span data-stu-id="884a9-145">Remove-AzureRemoteAppUser</span></span>
* <span data-ttu-id="884a9-146">Get-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="884a9-146">Get-AzureRemoteAppSession</span></span>
* <span data-ttu-id="884a9-147">Disconnect-AzureRemoteAppSession</span><span class="sxs-lookup"><span data-stu-id="884a9-147">Disconnect-AzureRemoteAppSession</span></span>
* <span data-ttu-id="884a9-148">Invoke-AzureRemoteAppSessionLogoff</span><span class="sxs-lookup"><span data-stu-id="884a9-148">Invoke-AzureRemoteAppSessionLogoff</span></span>
* <span data-ttu-id="884a9-149">Send-AzureRemoteAppSessionMessage</span><span class="sxs-lookup"><span data-stu-id="884a9-149">Send-AzureRemoteAppSessionMessage</span></span>
* <span data-ttu-id="884a9-150">Get-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="884a9-150">Get-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="884a9-151">Get-AzureRemoteAppStartMenuProgram</span><span class="sxs-lookup"><span data-stu-id="884a9-151">Get-AzureRemoteAppStartMenuProgram</span></span>
* <span data-ttu-id="884a9-152">Publish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="884a9-152">Publish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="884a9-153">Unpublish-AzureRemoteAppProgram</span><span class="sxs-lookup"><span data-stu-id="884a9-153">Unpublish-AzureRemoteAppProgram</span></span>
* <span data-ttu-id="884a9-154">Get-AzureRemoteAppCollectionUsageDetails</span><span class="sxs-lookup"><span data-stu-id="884a9-154">Get-AzureRemoteAppCollectionUsageDetails</span></span>
* <span data-ttu-id="884a9-155">Get-AzureRemoteAppCollectionUsageSummary</span><span class="sxs-lookup"><span data-stu-id="884a9-155">Get-AzureRemoteAppCollectionUsageSummary</span></span>
* <span data-ttu-id="884a9-156">Get-AzureRemoteAppPlan</span><span class="sxs-lookup"><span data-stu-id="884a9-156">Get-AzureRemoteAppPlan</span></span>

<span data-ttu-id="884a9-157">RemoteApp 가상 네트워크 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="884a9-157">RemoteApp virtual network cmdlets:</span></span>

* <span data-ttu-id="884a9-158">New-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="884a9-158">New-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="884a9-159">Get-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="884a9-159">Get-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="884a9-160">Set-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="884a9-160">Set-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="884a9-161">Remove-AzureRemoteAppVNet</span><span class="sxs-lookup"><span data-stu-id="884a9-161">Remove-AzureRemoteAppVNet</span></span>
* <span data-ttu-id="884a9-162">Get-AzureRemoteAppVpnDevice</span><span class="sxs-lookup"><span data-stu-id="884a9-162">Get-AzureRemoteAppVpnDevice</span></span>
* <span data-ttu-id="884a9-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span><span class="sxs-lookup"><span data-stu-id="884a9-163">Get-- AzureRemoteAppVpnDeviceConfigScript</span></span>
* <span data-ttu-id="884a9-164">Reset-AzureRemoteAppVpnSharedKey</span><span class="sxs-lookup"><span data-stu-id="884a9-164">Reset-AzureRemoteAppVpnSharedKey</span></span>

<span data-ttu-id="884a9-165">RemoteApp 템플릿 이미지 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="884a9-165">RemoteApp template image cmdlets:</span></span>

* <span data-ttu-id="884a9-166">New-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="884a9-166">New-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="884a9-167">Get-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="884a9-167">Get-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="884a9-168">Rename-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="884a9-168">Rename-AzureRemoteAppTemplateImage</span></span>
* <span data-ttu-id="884a9-169">Remove-AzureRemoteAppTemplateImage</span><span class="sxs-lookup"><span data-stu-id="884a9-169">Remove-AzureRemoteAppTemplateImage</span></span>

<span data-ttu-id="884a9-170">기타 RemoteApp cmdlet:</span><span class="sxs-lookup"><span data-stu-id="884a9-170">Other RemoteApp cmdlets:</span></span>

* <span data-ttu-id="884a9-171">Get-AzureRemoteAppLocation</span><span class="sxs-lookup"><span data-stu-id="884a9-171">Get-AzureRemoteAppLocation</span></span>
* <span data-ttu-id="884a9-172">Get-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="884a9-172">Get-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="884a9-173">Set-AzureRemoteAppWorkspace</span><span class="sxs-lookup"><span data-stu-id="884a9-173">Set-AzureRemoteAppWorkspace</span></span>
* <span data-ttu-id="884a9-174">Get-AzureRemoteAppOperationResult</span><span class="sxs-lookup"><span data-stu-id="884a9-174">Get-AzureRemoteAppOperationResult</span></span>

