---
title: "aaaConnect tooyour StorSimple 장치에 원격으로 | Microsoft Docs"
description: "에 대해 설명 어떻게 tooconfigure 원격 관리를 위한 장치 방법과 tooconnect tooWindows HTTP 또는 HTTPS를 통해 StorSimple 용 PowerShell 합니다."
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
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="6198d-103">Tooyour StorSimple 8000 시리즈 장치에 원격으로 연결</span><span class="sxs-lookup"><span data-stu-id="6198d-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="6198d-104">개요</span><span class="sxs-lookup"><span data-stu-id="6198d-104">Overview</span></span>
<span data-ttu-id="6198d-105">Windows PowerShell remoting tooconnect tooyour StorSimple 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-105">You can use Windows PowerShell remoting tooconnect tooyour StorSimple device.</span></span> <span data-ttu-id="6198d-106">이러한 방식으로 연결하면 메뉴가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="6198d-107">(표시 메뉴 hello 장치 tooconnect에 hello 직렬 콘솔을 사용 하는 경우에.) Windows PowerShell 원격 기능에서는 특정 runspace tooa 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="6198d-108">Hello 표시 언어를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-108">You can also specify hello display language.</span></span> 

<span data-ttu-id="6198d-109">Windows PowerShell remoting toomanage 장치를 사용 하는 방법에 대 한 자세한 내용은 이동 너무[tooadminister StorSimple에 대 한 Windows PowerShell을 사용 하 여 StorSimple 장치](storsimple-windows-powershell-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="6198d-110">이 자습서에 설명 방법을 tooconfigure 다음 방법과 원격 관리에 대 한 장치 tooconnect tooWindows StorSimple 용 PowerShell 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="6198d-111">Windows PowerShell 원격을 통해 tooconnect HTTP 또는 HTTPS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-111">You can use HTTP or HTTPS tooconnect via Windows PowerShell remoting.</span></span> <span data-ttu-id="6198d-112">그러나 결정할 때 tooconnect tooWindows StorSimple에 대 한 PowerShell hello 다음을 고려 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="6198d-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following:</span></span> 

* <span data-ttu-id="6198d-113">Toohello 직접 연결 하는 장치 직렬 콘솔은 안전 하지만 네트워크 스위치를 통해 연결 toohello 직렬 콘솔을 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="6198d-114">네트워크 스위치를 통해 toohello 장치 직렬 콘솔을 연결할 때에 hello 보안 위험에 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span> 
* <span data-ttu-id="6198d-115">HTTP 세션을 통해 연결 hello 네트워크를 통해 hello 직렬 콘솔을 통한 연결 보다 더 강화 된 보안을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="6198d-116">가장 안전한 방법은 hello 하지 않더라도 신뢰할 수 있는 네트워크는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="6198d-117">가장 안전한 hello 및 hello 권장 옵션은 자체 서명 된 인증서와 HTTPS 세션을 통해 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="6198d-118">Windows PowerShell 인터페이스 toohello 원격으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="6198d-119">그러나, hello Windows PowerShell 인터페이스를 통해 원격 액세스 tooyour StorSimple 장치는 기본적으로 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="6198d-120">다음에 hello tooaccess 사용된 되는 클라이언트 장치 및 tooenable hello 장치에서 원격 관리를 먼저 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-120">You need tooenable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="6198d-121">이 문서에 설명 된 hello 단계는 Windows Server 2012 r 2를 실행 하는 호스트 시스템에서 수행 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="6198d-122">HTTP를 통해 연결</span><span class="sxs-lookup"><span data-stu-id="6198d-122">Connect through HTTP</span></span>
<span data-ttu-id="6198d-123">TooWindows PowerShell StorSimple에 대 한 HTTP 세션을 통해 연결 하는 hello StorSimple 장치의 직렬 콘솔을 통한 연결 보다 더 강화 된 보안을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="6198d-124">가장 안전한 방법은 hello 하지 않더라도 신뢰할 수 있는 네트워크는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="6198d-125">Azure 클래식 포털 hello 또는 hello 직렬 콘솔 tooconfigure 원격 관리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-125">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="6198d-126">다음 절차를 수행 하는 hello에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="6198d-127">Hello Azure 클래식 포털 tooenable 원격 관리를 사용 하 여 HTTP를 통해</span><span class="sxs-lookup"><span data-stu-id="6198d-127">Use hello Azure classic portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="6198d-128">Hello 직렬 콘솔 tooenable 원격 관리를 사용 하 여 HTTP를 통해</span><span class="sxs-lookup"><span data-stu-id="6198d-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="6198d-129">원격 관리를 활성화 한 후 다음 원격 연결에 대 한 프로시저 tooprepare hello 클라이언트 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="6198d-130">원격 연결에 대 한 hello 클라이언트 준비</span><span class="sxs-lookup"><span data-stu-id="6198d-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="6198d-131">Hello Azure 클래식 포털 tooenable 원격 관리를 사용 하 여 HTTP를 통해</span><span class="sxs-lookup"><span data-stu-id="6198d-131">Use hello Azure classic portal tooenable remote management over HTTP</span></span>
<span data-ttu-id="6198d-132">HTTP를 통해 hello Azure 클래식 포털 tooenable 원격 관리의 단계를 실행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-132">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a><span data-ttu-id="6198d-133">tooenable hello Azure 클래식 포털을 통해 원격 관리</span><span class="sxs-lookup"><span data-stu-id="6198d-133">tooenable remote management through hello Azure classic portal</span></span>
1. <span data-ttu-id="6198d-134">장치에 대한 **장치** > **구성**에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="6198d-135">Toohello 아래로 스크롤하여 **원격 관리** 섹션.</span><span class="sxs-lookup"><span data-stu-id="6198d-135">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="6198d-136">설정 **원격 관리를 사용 하도록 설정** 너무**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-136">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="6198d-137">이제 HTTP를 사용 하 여 tooconnect를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-137">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="6198d-138">(hello 기본값은 tooconnect HTTPS를 통한.) HTTP가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-138">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6198d-139">HTTP를 통한 연결은 신뢰할 수 있는 네트워크에서만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="6198d-140">클릭 **저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-140">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="6198d-141">Hello 직렬 콘솔 tooenable 원격 관리를 사용 하 여 HTTP를 통해</span><span class="sxs-lookup"><span data-stu-id="6198d-141">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="6198d-142">Hello hello 장치 직렬 콘솔 tooenable 원격 관리에 대 한 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-142">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="6198d-143">tooenable hello 장치 직렬 콘솔을 통해 원격 관리</span><span class="sxs-lookup"><span data-stu-id="6198d-143">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="6198d-144">Hello 직렬 콘솔 메뉴에서 옵션 1을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-144">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="6198d-145">너무 hello 장치 hello 직렬 콘솔을 사용 하는 방법에 대 한 자세한 내용을 보려면 이동[장치 직렬 콘솔을 통해 tooWindows PowerShell StorSimple에 대 한 연결](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-145">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="6198d-146">Hello 프롬프트에서 다음을 입력 합니다.`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="6198d-146">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="6198d-147">HTTP tooconnect toohello 장치를 사용 하 여 hello 보안 취약점에 대 한 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-147">You will be notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="6198d-148">메시지가 표시되면 **Y**를 입력하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="6198d-149">다음을 입력하여 HTTP를 사용할 수 있는지 확인합니다. `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="6198d-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="6198d-150">해당 hello 확인 **RemoteManagementMode** 필드 **HttpsAndHttpEnabled**.hello 그림 다음 PuTTY에서 이러한 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-150">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![직렬 HTTPS 및 HTTP 사용](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="6198d-152">원격 연결에 대 한 hello 클라이언트 준비</span><span class="sxs-lookup"><span data-stu-id="6198d-152">Prepare hello client for remote connection</span></span>
<span data-ttu-id="6198d-153">Hello hello 클라이언트 tooenable 원격 관리에 대 한 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-153">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="6198d-154">원격 연결에 대 한 tooprepare hello 클라이언트</span><span class="sxs-lookup"><span data-stu-id="6198d-154">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="6198d-155">관리자 권한으로 Windows PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="6198d-156">Hello 다음 hello StorSimple 장치 toohello 클라이언트의 신뢰할 수 있는 호스트 목록의 명령 tooadd hello IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-156">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="6198d-157">대체 <*device_ip*> 장치; hello IP 주소로 예:</span><span class="sxs-lookup"><span data-stu-id="6198d-157">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="6198d-158">다음 명령은 toosave hello 장치 자격 증명을 변수에 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-158">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="6198d-159">Hello 대화 상자가 나타나면:</span><span class="sxs-lookup"><span data-stu-id="6198d-159">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="6198d-160">이 형식으로 hello 사용자 이름을 입력: *device_ip\SSAdmin*합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-160">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="6198d-161">Hello hello 설치 마법사를 사용 hello 장치를 구성할 때 설정한 장치 관리자 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-161">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="6198d-162">hello 기본 암호는 *Password1*합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-162">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="6198d-163">이 명령을 입력 하 여 hello 장치에서 Windows PowerShell 세션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-163">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="6198d-164">hello를 추가 하는 hello StorSimple 가상 장치에 사용 하기 위해 Windows PowerShell 세션 toocreate `–Port` 매개 변수 hello StorSimple 가상 어플라이언스 Remoting에서 구성한 공용 포트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-164">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="6198d-165">이 시점에서 활성 원격 Windows PowerShell 세션 toohello 장치가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-165">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
    ![HTTP를 사용한 PowerShell 원격](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="6198d-167">HTTPS를 통해 연결</span><span class="sxs-lookup"><span data-stu-id="6198d-167">Connect through HTTPS</span></span>
<span data-ttu-id="6198d-168">TooWindows PowerShell StorSimple에 대 한 HTTPS 세션을 통해 연결 하는 가장 안전한 hello 및 권장 되는 방법의 tooyour Microsoft Azure StorSimple 장치를 원격으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-168">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="6198d-169">다음 절차를 수행 하는 hello StorSimple에 대 한 HTTPS tooconnect tooWindows PowerShell을 사용할 수 있도록 직렬 콘솔과 클라이언트 컴퓨터를 tooset hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-169">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="6198d-170">Azure 클래식 포털 hello 또는 hello 직렬 콘솔 tooconfigure 원격 관리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-170">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="6198d-171">다음 절차를 수행 하는 hello에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-171">Select from hello following procedures:</span></span>

* [<span data-ttu-id="6198d-172">Hello Azure 클래식 포털 tooenable 원격 관리를 사용 하 여 HTTPS를 통해</span><span class="sxs-lookup"><span data-stu-id="6198d-172">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="6198d-173">Hello 직렬 콘솔 tooenable 원격 관리를 사용 하 여 HTTPS를 통해</span><span class="sxs-lookup"><span data-stu-id="6198d-173">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="6198d-174">원격 관리를 활성화 한 후 다음 원격 관리에 대 한 프로시저 tooprepare hello 호스트 hello를 사용 하 고 hello 원격 호스트에서 toohello 장치를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-174">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="6198d-175">원격 관리를 위해 hello 호스트 준비</span><span class="sxs-lookup"><span data-stu-id="6198d-175">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="6198d-176">Hello 원격 호스트에서 toohello 장치 연결</span><span class="sxs-lookup"><span data-stu-id="6198d-176">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="6198d-177">Hello Azure 클래식 포털 tooenable 원격 관리를 사용 하 여 HTTPS를 통해</span><span class="sxs-lookup"><span data-stu-id="6198d-177">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>
<span data-ttu-id="6198d-178">HTTPS를 통해 hello Azure 클래식 포털 tooenable 원격 관리의 단계를 실행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-178">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a><span data-ttu-id="6198d-179">hello Azure 클래식 포털에서에서 HTTPS 통한 tooenable 원격 관리</span><span class="sxs-lookup"><span data-stu-id="6198d-179">tooenable remote management over HTTPS from hello Azure classic portal</span></span>
1. <span data-ttu-id="6198d-180">장치에 대한 **장치** > **구성**에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="6198d-181">Toohello 아래로 스크롤하여 **원격 관리** 섹션.</span><span class="sxs-lookup"><span data-stu-id="6198d-181">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="6198d-182">설정 **원격 관리를 사용 하도록 설정** 너무**예**합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-182">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="6198d-183">이제 HTTPS를 사용 하 여 tooconnect를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-183">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="6198d-184">(hello 기본값은 tooconnect HTTPS를 통한.) HTTPS가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-184">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="6198d-185">**원격 관리 인증서 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="6198d-186">위치 toosave이이 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-186">Specify a location toosave this file.</span></span> <span data-ttu-id="6198d-187">Tooinstall tooconnect toohello 장치를 사용 합니다 hello 클라이언트 또는 호스트 컴퓨터에이 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-187">You will need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="6198d-188">클릭 **저장** hello hello 페이지 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-188">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="6198d-189">Hello 직렬 콘솔 tooenable 원격 관리를 사용 하 여 HTTPS를 통해</span><span class="sxs-lookup"><span data-stu-id="6198d-189">Use hello serial console tooenable remote management over HTTPS</span></span>
<span data-ttu-id="6198d-190">Hello hello 장치 직렬 콘솔 tooenable 원격 관리에 대 한 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-190">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="6198d-191">tooenable hello 장치 직렬 콘솔을 통해 원격 관리</span><span class="sxs-lookup"><span data-stu-id="6198d-191">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="6198d-192">Hello 직렬 콘솔 메뉴에서 옵션 1을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-192">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="6198d-193">너무 hello 장치 hello 직렬 콘솔을 사용 하는 방법에 대 한 자세한 내용을 보려면 이동[장치 직렬 콘솔을 통해 tooWindows PowerShell StorSimple에 대 한 연결](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-193">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="6198d-194">Hello 프롬프트에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-194">At hello prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="6198d-195">이제 장치에서 HTTPS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="6198d-196">다음을 입력하여 HTTPS를 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="6198d-197">해당 hello 있는지 확인 **RemoteManagementMode** 필드 **HttpsEnabled**.hello 그림 다음 PuTTY에서 이러한 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-197">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![직렬 HTTPS 사용](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="6198d-199">hello 출력에서 `Get-HcsSystem`, hello hello 장치 일련 번호를 복사 하 고 나중에 사용할 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-199">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6198d-200">hello 일련 번호 hello 인증서에 CN 이름을 toohello 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-200">hello serial number maps toohello CN name in hello certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="6198d-201">다음을 입력하여 원격 관리 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="6198d-202">인증서 비슷한 toohello 다음 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-202">A certificate similar toohello following will appear.</span></span>
   
    ![원격 관리 인증서 가져오기](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="6198d-204">hello 인증서의 hello 정보 복사 **---BEGIN 인증서---** 너무**---END 인증서---** .cer 파일로 저장 하 고 메모장과 같은 텍스트 편집기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-204">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="6198d-205">(복사할 파일 tooyour 원격 호스트가 hello 호스트를 준비할 때.)</span><span class="sxs-lookup"><span data-stu-id="6198d-205">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6198d-206">toogenerate 새 인증서를 사용 하 여 hello `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6198d-206">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="6198d-207">원격 관리를 위해 hello 호스트 준비</span><span class="sxs-lookup"><span data-stu-id="6198d-207">Prepare hello host for remote management</span></span>
<span data-ttu-id="6198d-208">다음 절차를 수행 하는 hello를 수행 하는 HTTPS 세션을 사용 하는 원격 연결에 대 한 tooprepare hello 호스트 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="6198d-208">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="6198d-209">[클라이언트 hello 또는 원격 호스트의 루트 저장소 hello hello.cer 파일 가져오기](#to-import-the-certificate-on-the-remote-host)합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-209">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="6198d-210">[원격 호스트 hello 장치 일련 번호 toohello 호스트 파일을 추가](#to-add-device-serial-numbers-to-the-remote-host)합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-210">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="6198d-211">아래에서는 이러한 각 절차에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-211">Each of these procedures is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="6198d-212">hello 원격 호스트에서 tooimport hello 인증서</span><span class="sxs-lookup"><span data-stu-id="6198d-212">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="6198d-213">Hello.cer 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **인증서 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-213">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="6198d-214">Hello 인증서 가져오기 마법사가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-214">This will start hello Certificate Import Wizard.</span></span>
   
    ![인증서 가져오기 마법사 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="6198d-216">**저장소 위치**에 대해 **로컬 컴퓨터**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="6198d-217">선택 **모든 인증서 저장소를 다음 hello에 저장**, 클릭 하 고 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-217">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="6198d-218">원격 호스트의 루트 저장소 toohello 탐색 한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-218">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![인증서 가져오기 마법사 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="6198d-220">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-220">Click **Finish**.</span></span> <span data-ttu-id="6198d-221">Hello 가져오기가 완료 되었는지 여부를 알려 주는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-221">A message that tells you that hello import was successful appears.</span></span>
   
    ![인증서 가져오기 마법사 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="6198d-223">tooadd 장치 일련 번호 toohello 원격 호스트</span><span class="sxs-lookup"><span data-stu-id="6198d-223">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="6198d-224">관리자 권한으로 메모장을 시작 하 고 \Windows\System32\Drivers\etc에 위치한 hello 호스트 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-224">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="6198d-225">다음 세 가지 항목 tooyour 호스트 파일 hello 추가: **DATA 0 IP 주소**, **컨트롤러 0 고정 IP 주소**, 및 **컨트롤러 1 고정 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-225">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="6198d-226">이전에 저장 하는 hello 장치 일련 번호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-226">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="6198d-227">다음 이미지는 hello와 같이이 toohello IP 주소를 매핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="6198d-227">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="6198d-228">컨트롤러 0과 컨트롤러 1에 대 한 추가 **Controller0** 및 **Controller1** hello 일련 번호 (CN 이름)의 hello 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![CN 이름 toohosts 파일 추가](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="6198d-230">Hello 호스트 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-230">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="6198d-231">Hello 원격 호스트에서 toohello 장치 연결</span><span class="sxs-lookup"><span data-stu-id="6198d-231">Connect toohello device from hello remote host</span></span>
<span data-ttu-id="6198d-232">Windows PowerShell 및 SSL을 사용 하 여 원격 호스트 또는 클라이언트 장치에서 SSAdmin 세션 tooenter 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-232">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="6198d-233">hello SSAdmin 세션 매핑합니다 hello에 1 toooption [직렬 콘솔](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) 장치의 메뉴.</span><span class="sxs-lookup"><span data-stu-id="6198d-233">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="6198d-234">Hello 절차 toomake hello 원격 Windows PowerShell 연결 하려는 hello 컴퓨터에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-234">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="6198d-235">Windows PowerShell 및 SSL을 사용 하 여 hello 장치에서 SSAdmin 세션 tooenter</span><span class="sxs-lookup"><span data-stu-id="6198d-235">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="6198d-236">관리자 권한으로 Windows PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="6198d-237">입력 하 여 hello 장치 IP 주소 toohello 클라이언트의 신뢰할 수 있는 호스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-237">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="6198d-238">여기서 <*device_ip*> 장치의 hello IP 주소입니다; 예:</span><span class="sxs-lookup"><span data-stu-id="6198d-238">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="6198d-239">다음을 입력하여 새 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="6198d-240">여기서 <*대상 장치의 IP*>는 해당 장치용; DATA 0의 hello IP 주소 예를 들어 **10.126.173.90** hello hello 호스트 파일의 이미지를 앞에 표시 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-240">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="6198d-241">또한 장치에 대 한 hello 관리자 암호를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-241">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="6198d-242">다음을 입력하여 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="6198d-243">Hello cmdlet의 hello-ComputerName 매개 변수에 대해 제공 hello <*대상 장치의 일련 번호*> 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-243">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="6198d-244">이 일련 번호 매핑된 toohello 원격 호스트; hello hosts 파일에서 DATA 0 IP 주소 예를 들어 **SHX0991003G44MT** hello 다음 이미지와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-244">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="6198d-245">형식:</span><span class="sxs-lookup"><span data-stu-id="6198d-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="6198d-246">Toowait 몇 분 필요 하며 SSL을 통한 HTTPS 통해 연결 된 tooyour 장치 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-246">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="6198d-247">연결 된 tooyour 장치는 나타내는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-247">You will see a message that indicates you are connected tooyour device.</span></span>
   
    ![HTTPS 및 SSL을 사용한 PowerShell 원격](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="6198d-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6198d-249">Next steps</span></span>
* <span data-ttu-id="6198d-250">에 대 한 자세한 내용은 [StorSimple 장치의 Windows PowerShell tooadminister를 사용 하 여](storsimple-windows-powershell-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-250">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="6198d-251">에 대 한 자세한 내용은 [StorSimple 장치의 StorSimple Manager 서비스 tooadminister를 hello를 사용 하 여](storsimple-manager-service-administration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6198d-251">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

