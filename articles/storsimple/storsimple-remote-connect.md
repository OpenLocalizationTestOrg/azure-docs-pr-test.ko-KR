---
title: "StorSimple 장치에 원격으로 연결 | Microsoft Docs"
description: "원격 관리를 위해 장치를 구성하는 방법 및 HTTP 또는 HTTPS를 통해 StorSimple용 Windows PowerShell에 연결하는 방법을 설명합니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b916173e127394d3ea06eded36285bdbbf884b12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="07167-103">StorSimple 8000 시리즈 장치에 원격으로 연결</span><span class="sxs-lookup"><span data-stu-id="07167-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="07167-104">개요</span><span class="sxs-lookup"><span data-stu-id="07167-104">Overview</span></span>
<span data-ttu-id="07167-105">Windows PowerShell 원격을 사용하여 StorSimple 장치에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-105">You can use Windows PowerShell remoting to connect to your StorSimple device.</span></span> <span data-ttu-id="07167-106">이러한 방식으로 연결하면 메뉴가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="07167-107">장치의 직렬 콘솔을 사용하여 연결하는 경우에만 메뉴가 표시됩니다. Windows PowerShell 원격을 사용하여 특정 Runspace에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="07167-108">표시 언어를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-108">You can also specify the display language.</span></span> 

<span data-ttu-id="07167-109">Windows PowerShell 원격을 사용하여 장치를 관리하는 방법에 대한 자세한 내용은 [StorSimple용 Windows PowerShell을 사용하여 StorSimple 장치 관리](storsimple-windows-powershell-administration.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07167-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="07167-110">이 자습서에서는 원격 관리를 위해 장치를 구성하는 방법 및 StorSimple용 Windows PowerShell에 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="07167-111">HTTP 또는 HTTPS를 사용하여 Windows PowerShell 원격을 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-111">You can use HTTP or HTTPS to connect via Windows PowerShell remoting.</span></span> <span data-ttu-id="07167-112">그러나 StorSimple용 Windows PowerShell에 연결하는 방법을 결정하는 경우 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="07167-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following:</span></span> 

* <span data-ttu-id="07167-113">장치 직렬 콘솔에 직접 연결하는 것은 안전하지만 네트워크 스위치를 통해 직렬 콘솔에 연결하는 것은 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="07167-114">네트워크 스위치를 통해 장치 직렬 콘솔에 연결할 때는 보안 위험에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="07167-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span> 
* <span data-ttu-id="07167-115">HTTP 세션을 통해 연결하는 경우 네트워크에서 직렬 콘솔을 통해 연결하는 것보다 보안이 강화될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="07167-116">가장 안전한 방법은 아니지만 신뢰할 수 있는 네트워크에서는 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="07167-117">가장 안전하고 권장되는 옵션은 자체 서명된 인증서를 사용하여 HTTPS 세션을 통해 연결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="07167-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="07167-118">Windows PowerShell 인터페이스에 원격으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="07167-119">그러나 Windows PowerShell 인터페이스를 통한 StorSimple 장치에 대한 원격 액세스는 기본적으로 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="07167-120">먼저, 장치에서 원격 관리를 사용하도록 설정한 다음 장치에 액세스하는 데 사용되는 클라이언트에서 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-120">You need to enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="07167-121">이 문서에 설명된 단계는 Windows Server 2012 R2를 실행하는 호스트 시스템에서 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="07167-122">HTTP를 통해 연결</span><span class="sxs-lookup"><span data-stu-id="07167-122">Connect through HTTP</span></span>
<span data-ttu-id="07167-123">HTTP 세션을 통해 StorSimple용 Windows PowerShell에 연결하는 경우 StorSimple 장치의 직렬 콘솔을 통해 연결하는 것보다 보안이 강화됩니다.</span><span class="sxs-lookup"><span data-stu-id="07167-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="07167-124">가장 안전한 방법은 아니지만 신뢰할 수 있는 네트워크에서는 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="07167-125">Azure 클래식 포털 또는 직렬 콘솔을 사용하여 원격 관리를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-125">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="07167-126">다음 절차에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="07167-127">Azure 클래식 포털을 사용하여 HTTP를 통한 원격 관리 사용</span><span class="sxs-lookup"><span data-stu-id="07167-127">Use the Azure classic portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="07167-128">직렬 콘솔을 사용하여 HTTP를 통한 원격 관리 사용</span><span class="sxs-lookup"><span data-stu-id="07167-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="07167-129">원격 관리를 사용하도록 설정한 후 다음 절차에 따라 원격 연결을 위해 클라이언트를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="07167-130">원격 연결을 위해 클라이언트 준비</span><span class="sxs-lookup"><span data-stu-id="07167-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="07167-131">Azure 클래식 포털을 사용하여 HTTP를 통한 원격 관리 사용</span><span class="sxs-lookup"><span data-stu-id="07167-131">Use the Azure classic portal to enable remote management over HTTP</span></span>
<span data-ttu-id="07167-132">Azure 클래식 포털에서 다음 단계를 수행하여 HTTP를 통한 원격 관리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-132">Perform the following steps in the Azure classic portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-classic-portal"></a><span data-ttu-id="07167-133">Azure 클래식 포털을 통해 원격 관리를 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="07167-133">To enable remote management through the Azure classic portal</span></span>
1. <span data-ttu-id="07167-134">장치에 대한 **장치** > **구성**에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="07167-135">**원격 관리** 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-135">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="07167-136">**원격 관리 사용**을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-136">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="07167-137">이제 HTTP를 사용하여 연결하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-137">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="07167-138">기본값은 HTTPS를 통한 연결입니다. HTTP가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-138">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="07167-139">HTTP를 통한 연결은 신뢰할 수 있는 네트워크에서만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="07167-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="07167-140">페이지 맨 아래에서 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-140">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="07167-141">직렬 콘솔을 사용하여 HTTP를 통한 원격 관리 사용</span><span class="sxs-lookup"><span data-stu-id="07167-141">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="07167-142">원격 관리를 사용하도록 설정하려면 장치 직렬 콘솔에서 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="07167-142">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="07167-143">장치 직렬 콘솔을 통해 원격 관리를 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="07167-143">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="07167-144">직렬 콘솔 메뉴에서 옵션 1을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-144">On the serial console menu, select option 1.</span></span> <span data-ttu-id="07167-145">장치의 직렬 콘솔을 사용하는 방법에 대한 자세한 내용은 [장치 직렬 콘솔을 통해 StorSimple용 Windows PowerShell에 연결](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07167-145">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="07167-146">프롬프트에 다음을 입력합니다. `Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="07167-146">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="07167-147">HTTP를 사용하여 장치에 연결하는 경우의 보안 취약점에 대한 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07167-147">You will be notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="07167-148">메시지가 표시되면 **Y**를 입력하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="07167-149">다음을 입력하여 HTTP를 사용할 수 있는지 확인합니다. `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="07167-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="07167-150">**RemoteManagementMode** 필드에 **HttpsAndHttpEnabled**가 표시되는지 확인합니다. 다음 그림은 PuTTY에서 이러한 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07167-150">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![직렬 HTTPS 및 HTTP 사용](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="07167-152">원격 연결을 위해 클라이언트 준비</span><span class="sxs-lookup"><span data-stu-id="07167-152">Prepare the client for remote connection</span></span>
<span data-ttu-id="07167-153">원격 관리를 사용하도록 설정하려면 클라이언트에서 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="07167-153">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="07167-154">원격 연결을 위해 클라이언트를 준비하려면</span><span class="sxs-lookup"><span data-stu-id="07167-154">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="07167-155">관리자 권한으로 Windows PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="07167-156">다음 명령을 입력하여 클라이언트의 신뢰할 수 있는 호스트 목록에 StorSimple 장치의 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-156">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="07167-157"><*device_ip*>를 장치의 IP 주소로 대체합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-157">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="07167-158">다음 명령을 입력하여 변수에 장치 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-158">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="07167-159">나타나는 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-159">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="07167-160">*device_ip\SSAdmin* 형식으로 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-160">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="07167-161">설정 마법사를 사용하여 장치를 구성할 때 설정한 장치 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-161">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="07167-162">기본 암호는 *Password1*입니다.</span><span class="sxs-lookup"><span data-stu-id="07167-162">The default password is *Password1*.</span></span>
5. <span data-ttu-id="07167-163">다음 명령을 입력하여 장치에서 Windows PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-163">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="07167-164">StorSimple 가상 장치에 사용할 Windows PowerShell 세션을 만들려면 `–Port` 매개 변수를 추가하고 Remoting for StorSimple Virtual Appliance에서 구성한 공용 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-164">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="07167-165">이제 장치에 대한 활성 원격 Windows PowerShell 세션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-165">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
    ![HTTP를 사용한 PowerShell 원격](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="07167-167">HTTPS를 통해 연결</span><span class="sxs-lookup"><span data-stu-id="07167-167">Connect through HTTPS</span></span>
<span data-ttu-id="07167-168">HTTPS 세션을 통해 StorSimple용 Windows PowerShell에 연결하는 것은 Microsoft Azure StorSimple 장치에 원격으로 연결하는 가장 안전하고 권장되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="07167-168">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="07167-169">다음 절차에서는 HTTPS를 사용 여 StorSimple용 Windows PowerShell에 연결할 수 있도록 직렬 콘솔과 클라이언트 컴퓨터를 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-169">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="07167-170">Azure 클래식 포털 또는 직렬 콘솔을 사용하여 원격 관리를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-170">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="07167-171">다음 절차에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-171">Select from the following procedures:</span></span>

* [<span data-ttu-id="07167-172">Azure 클래식 포털을 사용하여 HTTPS를 통한 원격 관리 사용</span><span class="sxs-lookup"><span data-stu-id="07167-172">Use the Azure classic portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="07167-173">직렬 콘솔을 사용하여 HTTPS를 통한 원격 관리 사용</span><span class="sxs-lookup"><span data-stu-id="07167-173">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="07167-174">원격 관리를 사용하도록 설정한 후 다음 절차에 따라 원격 관리를 위해 호스트를 준비하고 원격 호스트에서 장치에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-174">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="07167-175">원격 관리를 위해 호스트 준비</span><span class="sxs-lookup"><span data-stu-id="07167-175">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="07167-176">원격 호스트에서 장치에 연결</span><span class="sxs-lookup"><span data-stu-id="07167-176">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="07167-177">Azure 클래식 포털을 사용하여 HTTPS를 통한 원격 관리 사용</span><span class="sxs-lookup"><span data-stu-id="07167-177">Use the Azure classic portal to enable remote management over HTTPS</span></span>
<span data-ttu-id="07167-178">Azure 클래식 포털에서 다음 단계를 수행하여 HTTPS를 통한 원격 관리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-178">Perform the following steps in the Azure classic portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-classic-portal"></a><span data-ttu-id="07167-179">Azure 클래식 포털에서 HTTPS를 통한 원격 관리를 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="07167-179">To enable remote management over HTTPS from the Azure classic portal</span></span>
1. <span data-ttu-id="07167-180">장치에 대한 **장치** > **구성**에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="07167-181">**원격 관리** 섹션으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-181">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="07167-182">**원격 관리 사용**을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-182">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="07167-183">이제 HTTPS를 사용하여 연결하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-183">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="07167-184">기본값은 HTTPS를 통한 연결입니다. HTTPS가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-184">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="07167-185">**원격 관리 인증서 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="07167-186">이 파일을 저장할 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-186">Specify a location to save this file.</span></span> <span data-ttu-id="07167-187">장치에 연결하는 데 사용할 클라이언트 또는 호스트 컴퓨터에 이 인증서를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-187">You will need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="07167-188">페이지 맨 아래에서 **저장** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-188">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="07167-189">직렬 콘솔을 사용하여 HTTPS를 통한 원격 관리 사용</span><span class="sxs-lookup"><span data-stu-id="07167-189">Use the serial console to enable remote management over HTTPS</span></span>
<span data-ttu-id="07167-190">원격 관리를 사용하도록 설정하려면 장치 직렬 콘솔에서 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="07167-190">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="07167-191">장치 직렬 콘솔을 통해 원격 관리를 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="07167-191">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="07167-192">직렬 콘솔 메뉴에서 옵션 1을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-192">On the serial console menu, select option 1.</span></span> <span data-ttu-id="07167-193">장치의 직렬 콘솔을 사용하는 방법에 대한 자세한 내용은 [장치 직렬 콘솔을 통해 StorSimple용 Windows PowerShell에 연결](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07167-193">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="07167-194">프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-194">At the prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="07167-195">이제 장치에서 HTTPS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="07167-196">다음을 입력하여 HTTPS를 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="07167-197">**RemoteManagementMode** 필드에 **HttpsEnabled**가 표시되는지 확인합니다. 다음 그림은 PuTTY에서 이러한 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07167-197">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![직렬 HTTPS 사용](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="07167-199">`Get-HcsSystem`의 출력에서 장치의 일련 번호를 복사하고 나중에 사용하기 위해 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-199">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="07167-200">일련 번호는 인증서의 CN 이름에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="07167-200">The serial number maps to the CN name in the certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="07167-201">다음을 입력하여 원격 관리 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="07167-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="07167-202">다음과 유사한 인증서가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="07167-202">A certificate similar to the following will appear.</span></span>
   
    ![원격 관리 인증서 가져오기](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="07167-204">**-----BEGIN CERTIFICATE-----**에서 **-----END CERTIFICATE-----**까지 인증서 정보를 메모장 등의 텍스트 편집기에 복사하고 .cer 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-204">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="07167-205">호스트를 준비할 때 이 파일을 원격 호스트에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-205">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="07167-206">새 인증서를 생성하려면 `Set-HcsRemoteManagementCert` cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-206">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="07167-207">원격 관리를 위해 호스트 준비</span><span class="sxs-lookup"><span data-stu-id="07167-207">Prepare the host for remote management</span></span>
<span data-ttu-id="07167-208">HTTPS 세션을 사용하는 원격 연결을 위해 호스트 컴퓨터를 준비하려면 다음 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="07167-208">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="07167-209">[클라이언트 또는 원격 호스트의 루트 저장소로 .cer 파일을 가져옵니다](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="07167-209">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="07167-210">[원격 호스트의 호스트 파일에 장치 일련 번호를 추가합니다](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="07167-210">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="07167-211">아래에서는 이러한 각 절차에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-211">Each of these procedures is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="07167-212">원격 호스트에서 인증서를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="07167-212">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="07167-213">.cer 파일을 마우스 오른쪽 단추로 클릭하고 **인증서 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-213">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="07167-214">인증서 가져오기 마법사가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="07167-214">This will start the Certificate Import Wizard.</span></span>
   
    ![인증서 가져오기 마법사 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="07167-216">**저장소 위치**에 대해 **로컬 컴퓨터**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="07167-217">**모든 인증서를 다음 저장소에 저장**을 선택하고 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-217">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="07167-218">원격 호스트의 루트 저장소로 이동한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-218">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![인증서 가져오기 마법사 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="07167-220">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-220">Click **Finish**.</span></span> <span data-ttu-id="07167-221">가져오기에 성공했음을 알리는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="07167-221">A message that tells you that the import was successful appears.</span></span>
   
    ![인증서 가져오기 마법사 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="07167-223">원격 호스트에 장치 일련 번호를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="07167-223">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="07167-224">관리자 권한으로 메모장을 시작하고 \Windows\System32\Drivers\etc에 있는 호스트 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07167-224">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="07167-225">호스트 파일에 **DATA 0 IP 주소**, **컨트롤러 0 고정 IP 주소** 및 **컨트롤러 1 고정 IP 주소**의 3개 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-225">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="07167-226">이전에 저장한 장치 일련 번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-226">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="07167-227">다음 그림과 같이 이 일련 번호를 IP 주소에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-227">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="07167-228">컨트롤러 0과 컨트롤러 1의 경우 일련 번호(CN 이름)의 끝에 **Controller0** 및 **Controller1**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![hosts 파일에 CN 이름 추가](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="07167-230">호스트 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-230">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="07167-231">원격 호스트에서 장치에 연결</span><span class="sxs-lookup"><span data-stu-id="07167-231">Connect to the device from the remote host</span></span>
<span data-ttu-id="07167-232">Windows PowerShell 및 SSL을 사용하여 원격 호스트 또는 클라이언트에서 장치의 SSAdmin 세션에 들어갑니다.</span><span class="sxs-lookup"><span data-stu-id="07167-232">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="07167-233">SSAdmin 세션은 장치의 [직렬 콘솔](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) 메뉴에 있는 옵션 1에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="07167-233">The SSAdmin session maps to option 1 in the [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="07167-234">원격 Windows PowerShell 연결을 설정하려는 컴퓨터에서 다음 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="07167-234">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="07167-235">Windows PowerShell 및 SSL을 사용하여 장치의 SSAdmin 세션에 들어가려면</span><span class="sxs-lookup"><span data-stu-id="07167-235">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="07167-236">관리자 권한으로 Windows PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="07167-237">다음을 입력하여 클라이언트의 신뢰할 수 있는 호스트에 장치 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-237">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="07167-238">여기서 <*device_ip*>는 장치의 IP 주소입니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-238">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="07167-239">다음을 입력하여 새 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07167-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="07167-240">여기서 <*대상 장치의 IP*>는 장치에 대한 DATA 0의 IP 주소(예: hosts 파일의 이전 그림에 표시된 **10.126.173.90**)입니다.</span><span class="sxs-lookup"><span data-stu-id="07167-240">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="07167-241">또한 장치에 대한 관리자 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-241">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="07167-242">다음을 입력하여 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07167-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="07167-243">cmdlet의 ComputerName 매개 변수의 경우 <*대상 장치의 일련 번호*>를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="07167-243">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="07167-244">이 일련 번호는 원격 호스트에서 hosts 파일에 있는 DATA 0의 IP 주소(예: 다음 그림에 표시된 **SHX0991003G44MT** )에 매핑되었습니다.</span><span class="sxs-lookup"><span data-stu-id="07167-244">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="07167-245">형식:</span><span class="sxs-lookup"><span data-stu-id="07167-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="07167-246">몇 분 정도 기다리면 HTTPS over SSL을 통해 장치에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="07167-246">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="07167-247">장치에 연결되었음을 나타내는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="07167-247">You will see a message that indicates you are connected to your device.</span></span>
   
    ![HTTPS 및 SSL을 사용한 PowerShell 원격](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="07167-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07167-249">Next steps</span></span>
* <span data-ttu-id="07167-250">[Windows PowerShell을 사용하여 StorSimple 장치를 관리하는 방법](storsimple-windows-powershell-administration.md)을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="07167-250">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="07167-251">[StorSimple Manager 서비스를 사용하여 StorSimple 장치를 관리](storsimple-manager-service-administration.md)하는 방법을 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="07167-251">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

