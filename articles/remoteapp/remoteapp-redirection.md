---
title: "Azure RemoteApp에서 aaaUsing 리디렉션 | Microsoft Docs"
description: "자세한 내용은 방법 RemoteApp에서 사용 하 여 tooconfigure 리디렉션"
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
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="1a25b-103">Azure RemoteApp에서 리디렉션 사용</span><span class="sxs-lookup"><span data-stu-id="1a25b-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1a25b-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1a25b-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1a25b-106">장치 리디렉션 hello 장치 연결 된 tootheir 로컬 컴퓨터, 휴대폰 또는 태블릿을 사용 하 여 원격 응용 프로그램과 상호 작용할 사용자가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-106">Device redirection lets your users interact with remote apps using hello devices attached tootheir local computer, phone, or tablet.</span></span> <span data-ttu-id="1a25b-107">예를 들어 Azure RemoteApp을 통해 Skype를 제공한 경우 사용자 자신의 PC toowork Skype로에 설치 하는 hello 카메라가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-107">For example, if you have provided Skype through Azure RemoteApp, your user needs hello camera installed on their PC toowork with Skype.</span></span> <span data-ttu-id="1a25b-108">프린터, 스피커, 모니터 및 USB로 연결된 다양한 주변 장치의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="1a25b-109">RemoteApp은 hello 프로토콜 RDP (원격 데스크톱)과 RemoteFX tooprovide 리디렉션을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-109">RemoteApp leverages hello Remote Desktop Protocol (RDP) and RemoteFX tooprovide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="1a25b-110">기본적으로 사용할 수 있는 리디렉션</span><span class="sxs-lookup"><span data-stu-id="1a25b-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="1a25b-111">RemoteApp을 사용 하는 경우 리디렉션을 수행 하는 hello 기본적으로 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-111">When you use RemoteApp, hello following redirections are enabled by default.</span></span> <span data-ttu-id="1a25b-112">괄호 안에 hello 정보 hello RDP 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-112">hello information in parentheses show hello RDP setting.</span></span>

* <span data-ttu-id="1a25b-113">Hello 로컬 컴퓨터에서 소리 재생 (**이 컴퓨터에서 재생**).</span><span class="sxs-lookup"><span data-stu-id="1a25b-113">Play sounds on hello local computer (**Play on this computer**).</span></span> <span data-ttu-id="1a25b-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="1a25b-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="1a25b-115">Hello 로컬 컴퓨터와 송신 toohello 원격 컴퓨터에서 오디오 캡처 (**이 컴퓨터에서 레코드**).</span><span class="sxs-lookup"><span data-stu-id="1a25b-115">Capture audio from hello local computer and send toohello remote computer (**Record from this computer**).</span></span> <span data-ttu-id="1a25b-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="1a25b-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="1a25b-117">인쇄 toolocal 프린터 (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="1a25b-117">Print toolocal printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="1a25b-118">COM 포트(redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="1a25b-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="1a25b-119">스마트 카드 장치(redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="1a25b-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="1a25b-120">(기능 toocopy 및 붙여넣기) 클립보드 (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="1a25b-120">Clipboard (ability toocopy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="1a25b-121">암호화되지 않은 형식 글꼴 다듬기(allow font smoothing:i:1)</span><span class="sxs-lookup"><span data-stu-id="1a25b-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="1a25b-122">지원되는 모든 플러그 앤 플레이 장치 리디렉션</span><span class="sxs-lookup"><span data-stu-id="1a25b-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="1a25b-123">(devicestoredirect:s:*)</span><span class="sxs-lookup"><span data-stu-id="1a25b-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="1a25b-124">사용할 수 있는 기타 리디렉션</span><span class="sxs-lookup"><span data-stu-id="1a25b-124">What other redirection is available?</span></span>
<span data-ttu-id="1a25b-125">기본적으로 다음 두 가지 리디렉션 옵션은 사용하지 않도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="1a25b-126">드라이브의 리디렉션을 (드라이브 매핑): 로컬 컴퓨터의 드라이브 될 hello 원격 세션에서 매핑된 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in hello remote session.</span></span> <span data-ttu-id="1a25b-127">Hello 원격 세션에서 작업 하는 동안 저장 하면 또는 로컬 드라이브에서 열려 있는 파일 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-127">This lets you save or open files from your local drives while you work in hello remote session.</span></span>
* <span data-ttu-id="1a25b-128">USB 리디렉션을: hello 원격 세션 내에서 hello USB 장치 연결 된 tooyour 로컬 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-128">USB redirection: You can use hello USB devices attached tooyour local computer within hello remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="1a25b-129">RemoteApp에서 리디렉션 설정 변경</span><span class="sxs-lookup"><span data-stu-id="1a25b-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="1a25b-130">SDK와 Microsoft Azure PowerShell hello를 사용 하 여 컬렉션에 대 한 hello 장치 리디렉션 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-130">You can change hello device redirection settings for a collection by using hello Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="1a25b-131">설치한 후 새 PowerShell 및 SDK hello, 먼저에 설명 된 구독 toomanage 구성 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-131">After you install hello new PowerShell and SDK, first configure it toomanage your subscription as described in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="1a25b-132">그런 다음 다음 RDP 속성이 사용자 지정 tooset hello 명령 비슷한 toohello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-132">Then use a command similar toohello following tooset hello custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="1a25b-133">(유의  *\`n*  개별 속성 사이의 구분 기호로 사용 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="1a25b-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="1a25b-134">tooget RDP 속성 사용자 지정 구성 된 목록을 hello 다음 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-134">tooget a list of what custom RDP properties are configured, run hello following cmdlet.</span></span> <span data-ttu-id="1a25b-135">만 사용자 지정 속성 출력 결과 표시 되 고 기본 속성을 hello 하지 note:</span><span class="sxs-lookup"><span data-stu-id="1a25b-135">Note that only custom properties are shown as output results and not hello default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="1a25b-136">사용자 지정 속성을 설정 하는 경우 모든 사용자 지정 속성을 지정 해야 때마다; 그렇지 않으면 hello 설정을 toodisabled가 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-136">When you set custom properties you must specify all custom properties each time; otherwise hello setting reverts toodisabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="1a25b-137">일반적인 예</span><span class="sxs-lookup"><span data-stu-id="1a25b-137">Common examples</span></span>
<span data-ttu-id="1a25b-138">다음 cmdlet tooenable 드라이브 리디렉션 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-138">Use hello following cmdlet tooenable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="1a25b-139">이 cmdlet tooenable를 사용 하 여 USB 및 드라이브 모두 리디렉션:</span><span class="sxs-lookup"><span data-stu-id="1a25b-139">Use this cmdlet tooenable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="1a25b-140">이 cmdlet toodisable 클립보드 공유를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-140">Use this cmdlet toodisable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="1a25b-141">있는지 toocompletely 로그 오프 hello 컬렉션의 모든 사용자 수 (및 뿐 아니라 연결 끊기) hello 변경을 테스트 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="1a25b-141">Be sure toocompletely log off all users in hello collection (and not just disconnect them) before you test hello change.</span></span> <span data-ttu-id="1a25b-142">tooensure 사용자가 로그 오프, 이동 toohello 완전히 **세션** hello Azure 포털의에서 hello 컬렉션에 탭을 분리 하거나 로그인 모든 사용자를 로그 오프 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-142">tooensure users are completely logged off, go toohello **Sessions** tab in hello collection in hello Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="1a25b-143">경우에 따라이 지나야 hello 로컬 드라이브 tooshow 몇 초 정도 탐색기에서 hello 세션 내에서.</span><span class="sxs-lookup"><span data-stu-id="1a25b-143">Sometimes it can take several seconds for hello local drives tooshow in Explorer within hello session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="1a25b-144">Windows 클라이언트에서 USB 리디렉션 설정 변경</span><span class="sxs-lookup"><span data-stu-id="1a25b-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="1a25b-145">TooRemoteApp 연결 하는 컴퓨터에서 USB 리디렉션을 toouse를 원하는 경우 toohappen 해야 하는 두 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-145">If you want toouse USB redirection on a computer that connects tooRemoteApp, there are 2 actions that need toohappen.</span></span> <span data-ttu-id="1a25b-146">1-관리자는 Azure PowerShell을 사용 하 여 tooenable USB 리디렉션을 hello 컬렉션 수준에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-146">1 - Your administrator needs tooenable USB redirection at hello collection level by using Azure PowerShell.</span></span> <span data-ttu-id="1a25b-147">2-toouse USB 리디렉션을 원하는 각 장치에서 tooenable에서 허용 하는 그룹 정책이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-147">2 - On each device where you want toouse USB redirection, you need tooenable a group policy that permits it.</span></span> <span data-ttu-id="1a25b-148">이 단계는 toobe toouse USB 리디렉션을가 하는 각 사용자에 대해 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-148">This step will need toobe done for each user that wants toouse USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="1a25b-149">Azure RemoteApp을 사용한 USB 리디렉션은 Windows 컴퓨터에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a><span data-ttu-id="1a25b-150">Hello RemoteApp 컬렉션에 대 한 USB 리디렉션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1a25b-150">Enable USB redirection for hello RemoteApp collection</span></span>
<span data-ttu-id="1a25b-151">Hello cmdlet tooenable USB 리디렉션을 hello 모음 수준에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-151">Use hello following cmdlet tooenable USB redirection at hello collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a><span data-ttu-id="1a25b-152">Hello 클라이언트 컴퓨터에 대 한 USB 리디렉션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1a25b-152">Enable USB redirection for hello client computer</span></span>
<span data-ttu-id="1a25b-153">컴퓨터에 tooconfigure USB 리디렉션 설정:</span><span class="sxs-lookup"><span data-stu-id="1a25b-153">tooconfigure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="1a25b-154">열기 hello 로컬 그룹 정책 편집기 (GPEDIT 합니다. MSC)입니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-154">Open hello Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="1a25b-155">명령 프롬프트에서 gpedit.msc를 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="1a25b-156">**Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="1a25b-157">**이 컴퓨터에서 지원되는 기타 RemoteFX USB 장치의 RDP 리디렉션 허용**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="1a25b-158">선택 **Enabled**를 선택한 후 **hello RemoteFX USB 리디렉션을 액세스 권한에서에서 관리자와 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-158">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="1a25b-159">관리자 권한으로 명령 프롬프트를 열고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-159">Open a command prompt with administrative permissions, and run hello following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="1a25b-160">Hello 컴퓨터를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-160">Restart hello computer.</span></span>

<span data-ttu-id="1a25b-161">그룹 정책 관리 도구 toocreate hello를 사용 하 여 하 고 도메인의 모든 컴퓨터에 대 한 hello USB 리디렉션 정책을 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-161">You can also use hello Group Policy Management tool toocreate and apply hello USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="1a25b-162">도메인 관리자에 게도 hello 도메인 컨트롤러에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-162">Log into hello domain controller as hello domain administrator.</span></span>
2. <span data-ttu-id="1a25b-163">Hello 그룹 정책 관리 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-163">Open hello Group Policy Management Console.</span></span> <span data-ttu-id="1a25b-164">**시작 > 관리 도구 > 그룹 정책 관리**를 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="1a25b-165">Toohello 도메인 또는 조직 구성 단위 toocreate hello 정책 원하는 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-165">Navigate toohello domain or organizational unit for which you want toocreate hello policy.</span></span>
4. <span data-ttu-id="1a25b-166">**기본 도메인 정책**을 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="1a25b-167">**Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="1a25b-168">**이 컴퓨터에서 지원되는 기타 RemoteFX USB 장치의 RDP 리디렉션 허용**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="1a25b-169">선택 **Enabled**를 선택한 후 **hello RemoteFX USB 리디렉션을 액세스 권한에서에서 관리자와 사용자**합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-169">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="1a25b-170">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1a25b-170">Click **OK**.</span></span>  

