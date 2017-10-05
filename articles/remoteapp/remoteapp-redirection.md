---
title: "Azure RemoteApp에서 리디렉션 사용 | Microsoft 문서"
description: "RemoteApp에서 리디렉션을 구성 및 사용하는 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: b5a65d129225fde46e3b090bc3cd9427989005ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="3a151-103">Azure RemoteApp에서 리디렉션 사용</span><span class="sxs-lookup"><span data-stu-id="3a151-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3a151-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3a151-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="3a151-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3a151-106">장치 리디렉션을 사용하면 사용자가 로컬 컴퓨터, 휴대폰 또는 태블릿에 연결된 장치를 통해 원격 앱을 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-106">Device redirection lets your users interact with remote apps using the devices attached to their local computer, phone, or tablet.</span></span> <span data-ttu-id="3a151-107">예를 들어 Azure RemoteApp을 통해 Skype를 제공하는 경우 사용자가 Skype를 사용하려면 PC에 카메라가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-107">For example, if you have provided Skype through Azure RemoteApp, your user needs the camera installed on their PC to work with Skype.</span></span> <span data-ttu-id="3a151-108">프린터, 스피커, 모니터 및 USB로 연결된 다양한 주변 장치의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="3a151-109">RemoteApp은 RDP(원격 데스크톱 프로토콜) 및 RemoteFX를 활용하여 리디렉션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-109">RemoteApp leverages the Remote Desktop Protocol (RDP) and RemoteFX to provide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="3a151-110">기본적으로 사용할 수 있는 리디렉션</span><span class="sxs-lookup"><span data-stu-id="3a151-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="3a151-111">RemoteApp을 사용하는 경우 기본적으로 다음과 같은 리디렉션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-111">When you use RemoteApp, the following redirections are enabled by default.</span></span> <span data-ttu-id="3a151-112">괄호 안의 정보는 RDP 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-112">The information in parentheses show the RDP setting.</span></span>

* <span data-ttu-id="3a151-113">로컬 컴퓨터에서 소리 재생(**이 컴퓨터에서 재생**)</span><span class="sxs-lookup"><span data-stu-id="3a151-113">Play sounds on the local computer (**Play on this computer**).</span></span> <span data-ttu-id="3a151-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="3a151-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="3a151-115">로컬 컴퓨터에서 오디오를 캡처하고 원격 컴퓨터로 보내기(**이 컴퓨터에서 녹음**)</span><span class="sxs-lookup"><span data-stu-id="3a151-115">Capture audio from the local computer and send to the remote computer (**Record from this computer**).</span></span> <span data-ttu-id="3a151-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="3a151-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="3a151-117">로컬 프린터로 인쇄(redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="3a151-117">Print to local printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="3a151-118">COM 포트(redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="3a151-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="3a151-119">스마트 카드 장치(redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="3a151-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="3a151-120">클립보드(복사 및 붙여넣기 기능)(redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="3a151-120">Clipboard (ability to copy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="3a151-121">암호화되지 않은 형식 글꼴 다듬기(allow font smoothing:i:1)</span><span class="sxs-lookup"><span data-stu-id="3a151-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="3a151-122">지원되는 모든 플러그 앤 플레이 장치 리디렉션</span><span class="sxs-lookup"><span data-stu-id="3a151-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="3a151-123">(devicestoredirect:s:*)</span><span class="sxs-lookup"><span data-stu-id="3a151-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="3a151-124">사용할 수 있는 기타 리디렉션</span><span class="sxs-lookup"><span data-stu-id="3a151-124">What other redirection is available?</span></span>
<span data-ttu-id="3a151-125">기본적으로 다음 두 가지 리디렉션 옵션은 사용하지 않도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="3a151-126">드라이브 리디렉션(드라이브 매핑): 로컬 컴퓨터의 드라이브가 원격 세션에서 매핑된 드라이브가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in the remote session.</span></span> <span data-ttu-id="3a151-127">이 경우 원격 세션에서 작업하는 동안 로컬 드라이브에서 파일을 저장하거나 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-127">This lets you save or open files from your local drives while you work in the remote session.</span></span>
* <span data-ttu-id="3a151-128">USB 리디렉션: 원격 세션 내에서 로컬 컴퓨터에 연결된 USB 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-128">USB redirection: You can use the USB devices attached to your local computer within the remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="3a151-129">RemoteApp에서 리디렉션 설정 변경</span><span class="sxs-lookup"><span data-stu-id="3a151-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="3a151-130">SDK와 함께 Microsoft Azure PowerShell을 사용하여 컬렉션에 대한 장치 리디렉션 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-130">You can change the device redirection settings for a collection by using the Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="3a151-131">새 PowerShell과 SDK를 설치한 후 먼저 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview)에 설명된 대로 구독을 관리하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-131">After you install the new PowerShell and SDK, first configure it to manage your subscription as described in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="3a151-132">그런 후에 다음과 비슷한 명령을 사용하여 사용자 지정 RDP 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-132">Then use a command similar to the following to set the custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="3a151-133">(유의  *\`n*  개별 속성 사이의 구분 기호로 사용 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="3a151-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="3a151-134">구성된 사용자 지정 RDP 속성 목록을 가져오려면 다음 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-134">To get a list of what custom RDP properties are configured, run the following cmdlet.</span></span> <span data-ttu-id="3a151-135">사용자 지정 속성만 출력 결과로 표시되고 기본 속성은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-135">Note that only custom properties are shown as output results and not the default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="3a151-136">사용자 지정 속성을 설정하는 경우 매번 모든 사용자 지정 속성을 지정해야 합니다. 그렇지 않으면 설정이 사용 안 함으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-136">When you set custom properties you must specify all custom properties each time; otherwise the setting reverts to disabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="3a151-137">일반적인 예</span><span class="sxs-lookup"><span data-stu-id="3a151-137">Common examples</span></span>
<span data-ttu-id="3a151-138">드라이브 리디렉션을 사용하도록 설정하려면 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-138">Use the following cmdlet to enable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="3a151-139">USB 및 드라이브 리디렉션을 둘 다 사용하도록 설정하려면 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-139">Use this cmdlet to enable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="3a151-140">클립보드 공유를 사용하지 않도록 설정하려면 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-140">Use this cmdlet to disable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="3a151-141">변경 내용을 테스트하기 전에 단순히 연결을 끊는 것이 아니라 컬렉션의 모든 사용자를 완전히 로그오프해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-141">Be sure to completely log off all users in the collection (and not just disconnect them) before you test the change.</span></span> <span data-ttu-id="3a151-142">사용자가 완전히 로그오프되었는지 확인하려면 Azure 포털에서 컬렉션의 **세션** 탭으로 이동한 다음 연결이 끊어졌거나 로그인된 모든 사용자를 로그오프합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-142">To ensure users are completely logged off, go to the **Sessions** tab in the collection in the Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="3a151-143">경우에 따라 세션 내의 탐색기에 로컬 드라이브가 표시될 때까지 몇 초 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-143">Sometimes it can take several seconds for the local drives to show in Explorer within the session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="3a151-144">Windows 클라이언트에서 USB 리디렉션 설정 변경</span><span class="sxs-lookup"><span data-stu-id="3a151-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="3a151-145">RemoteApp에 연결하는 컴퓨터에서 USB 리디렉션을 사용하려는 경우 다음 두 작업이 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-145">If you want to use USB redirection on a computer that connects to RemoteApp, there are 2 actions that need to happen.</span></span> <span data-ttu-id="3a151-146">1 - 관리자가 Azure PowerShell을 사용하여 컬렉션 수준에서 USB 리디렉션을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-146">1 - Your administrator needs to enable USB redirection at the collection level by using Azure PowerShell.</span></span> <span data-ttu-id="3a151-147">2 - USB 리디렉션을 사용하려는 각 장치에서 허용하는 그룹 정책을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-147">2 - On each device where you want to use USB redirection, you need to enable a group policy that permits it.</span></span> <span data-ttu-id="3a151-148">이 단계는 USB 리디렉션을 사용하려는 각 사용자에 대해 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-148">This step will need to be done for each user that wants to use USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="3a151-149">Azure RemoteApp을 사용한 USB 리디렉션은 Windows 컴퓨터에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-the-remoteapp-collection"></a><span data-ttu-id="3a151-150">RemoteApp 컬렉션에 대해 USB 리디렉션 사용</span><span class="sxs-lookup"><span data-stu-id="3a151-150">Enable USB redirection for the RemoteApp collection</span></span>
<span data-ttu-id="3a151-151">컬렉션 수준에서 USB 리디렉션을 사용하도록 설정하려면 다음 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-151">Use the following cmdlet to enable USB redirection at the collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-the-client-computer"></a><span data-ttu-id="3a151-152">클라이언트 컴퓨터에 대해 USB 리디렉션 사용</span><span class="sxs-lookup"><span data-stu-id="3a151-152">Enable USB redirection for the client computer</span></span>
<span data-ttu-id="3a151-153">컴퓨터에서 USB 리디렉션 설정을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="3a151-153">To configure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="3a151-154">로컬 그룹 정책 편집기(GPEDIT.MSC)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-154">Open the Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="3a151-155">명령 프롬프트에서 gpedit.msc를 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="3a151-156">**Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="3a151-157">**이 컴퓨터에서 지원되는 기타 RemoteFX USB 장치의 RDP 리디렉션 허용**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="3a151-158">**사용**을 선택한 다음 **RemoteFX USB 리디렉션 액세스 권한의 관리자 및 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-158">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="3a151-159">관리자 권한으로는 명령 프롬프트를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-159">Open a command prompt with administrative permissions, and run the following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="3a151-160">컴퓨터를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-160">Restart the computer.</span></span>

<span data-ttu-id="3a151-161">그룹 정책 관리 도구를 사용하여 도메인의 모든 컴퓨터에 대한 USB 리디렉션 정책을 만들고 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-161">You can also use the Group Policy Management tool to create and apply the USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="3a151-162">도메인 관리자로 도메인 컨트롤러에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-162">Log into the domain controller as the domain administrator.</span></span>
2. <span data-ttu-id="3a151-163">그룹 정책 관리 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-163">Open the Group Policy Management Console.</span></span> <span data-ttu-id="3a151-164">**시작 > 관리 도구 > 그룹 정책 관리**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="3a151-165">정책을 만들려는 도메인 또는 조직 구성 단위로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-165">Navigate to the domain or organizational unit for which you want to create the policy.</span></span>
4. <span data-ttu-id="3a151-166">**기본 도메인 정책**을 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="3a151-167">**Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="3a151-168">**이 컴퓨터에서 지원되는 기타 RemoteFX USB 장치의 RDP 리디렉션 허용**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="3a151-169">**사용**을 선택한 다음 **RemoteFX USB 리디렉션 액세스 권한의 관리자 및 사용자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-169">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="3a151-170">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a151-170">Click **OK**.</span></span>  

