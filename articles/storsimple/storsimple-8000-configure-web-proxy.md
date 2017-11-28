---
title: "StorSimple 8000 시리즈 장치에 대한 웹 프록시 설정 | Microsoft Docs"
description: "StorSimple용 Windows PowerShell을 사용하여 StorSimple 장치에 대한 웹 프록시 설정을 구성하는 방법을 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: 
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: alkohli
ms.openlocfilehash: 1109e44ed9c6aa8a0f7305b8a50410316711589c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a><span data-ttu-id="fef26-103">StorSimple 장치에 대한 웹 프록시 구성</span><span class="sxs-lookup"><span data-stu-id="fef26-103">Configure web proxy for your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="fef26-104">개요</span><span class="sxs-lookup"><span data-stu-id="fef26-104">Overview</span></span>

<span data-ttu-id="fef26-105">이 자습서에서는 StorSimple용 Windows PowerShell을 사용하여 StorSimple 장치에 대한 웹 프록시 설정을 구성하고 보는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-105">This tutorial describes how to use Windows PowerShell for StorSimple to configure and view web proxy settings for your StorSimple device.</span></span> <span data-ttu-id="fef26-106">클라우드와 통신할 때 StorSimple 장치에서 웹 프록시 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-106">The web proxy settings are used by the StorSimple device when communicating with the cloud.</span></span> <span data-ttu-id="fef26-107">웹 프록시 서버를 사용하여 보안, 필터 콘텐츠, 캐시의 다른 계층을 추가함으로써 대역폭 요구 사항 또는 분석을 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-107">A web proxy server is used to add another layer of security, filter content, cache to ease bandwidth requirements or even help with analytics.</span></span>

<span data-ttu-id="fef26-108">이 자습서의 지침은 StorSimple 8000 시리즈 물리적 장치에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-108">The guidance in this tutorial applies only to StorSimple 8000 series physical devices.</span></span> <span data-ttu-id="fef26-109">웹 프록시 구성은 StorSimple Cloud Appliance(8010 및 8020)에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-109">Web proxy configuration is not supported on the StorSimple Cloud Appliance (8010 and 8020).</span></span>

<span data-ttu-id="fef26-110">웹 프록시는 StorSimple 장치에 대한 _선택적_ 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-110">Web proxy is an _optional_ configuration for your StorSimple device.</span></span> <span data-ttu-id="fef26-111">StorSimple용 Windows PowerShell을 통해서만 웹 프록시를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-111">You can configure web proxy only via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="fef26-112">구성은 다음과 같은 2단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-112">The configuration is a two-step process as follows:</span></span>

1. <span data-ttu-id="fef26-113">먼저 StorSimple cmdlet용 설치 마법사 또는 Windows PowerShell을 통해 웹 프록시 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-113">You first configure web proxy settings through the setup wizard or Windows PowerShell for StorSimple cmdlets.</span></span>
2. <span data-ttu-id="fef26-114">그런 다음 StorSimple cmdlet용 Windows PowerShell을 통해 구성된 웹 프록시 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-114">You then enable the configured web proxy settings via Windows PowerShell for StorSimple cmdlets.</span></span>

<span data-ttu-id="fef26-115">웹 프록시 구성을 완료한 후에 Microsoft Azure StorSimple 장치 관리자 서비스 및 StorSimple용 Windows PowerShell에서 구성된 웹 프록시 설정을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-115">After the web proxy configuration is complete, you can view the configured web proxy settings in both the Microsoft Azure StorSimple Device Manager service and the Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="fef26-116">이 자습서를 읽은 후에 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-116">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="fef26-117">설치 마법사 및 cmdlet을 사용하여 웹 프록시를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-117">Configure web proxy by using setup wizard and cmdlets.</span></span>
* <span data-ttu-id="fef26-118">Cmdlet을 사용하여 웹 프록시를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-118">Enable web proxy by using cmdlets.</span></span>
* <span data-ttu-id="fef26-119">Azure Portal에서 웹 프록시 설정을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-119">View web proxy settings in the Azure portal.</span></span>
* <span data-ttu-id="fef26-120">웹 프록시를 구성하는 동안 오류 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-120">Troubleshoot errors during web proxy configuration.</span></span>


## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a><span data-ttu-id="fef26-121">StorSimple용 Windows PowerShell을 통해 웹 프록시 구성</span><span class="sxs-lookup"><span data-stu-id="fef26-121">Configure web proxy via Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="fef26-122">웹 프록시 설정을 구성하려면 다음 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-122">You use either of the following to configure web proxy settings:</span></span>

* <span data-ttu-id="fef26-123">설치 마법사는 구성 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-123">Setup wizard to guide you through the configuration steps.</span></span>
* <span data-ttu-id="fef26-124">StorSimple용 Windows PowerShell에서 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="fef26-124">Cmdlets in Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="fef26-125">이러한 각 메서드는 다음 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-125">Each of these methods is discussed in the following sections.</span></span>

## <a name="configure-web-proxy-via-the-setup-wizard"></a><span data-ttu-id="fef26-126">설치 마법사를 통해 웹 프록시 구성</span><span class="sxs-lookup"><span data-stu-id="fef26-126">Configure web proxy via the setup wizard</span></span>

<span data-ttu-id="fef26-127">웹 프록시를 구성하기 위한 단계를 안내하는 설치 마법사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-127">Use the setup wizard to guide you through the steps for web proxy configuration.</span></span> <span data-ttu-id="fef26-128">다음 단계를 수행하여 장치에 웹 프록시를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-128">Perform the following steps to configure web proxy on your device.</span></span>

#### <a name="to-configure-web-proxy-via-the-setup-wizard"></a><span data-ttu-id="fef26-129">설치 마법사를 통해 웹 프록시를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="fef26-129">To configure web proxy via the setup wizard</span></span>

1. <span data-ttu-id="fef26-130">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택하고 **장치 관리자 암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-130">In the serial console menu, choose option 1, **Log in with full access** and provide the **device administrator password**.</span></span> <span data-ttu-id="fef26-131">설치 마법사 세션을 시작하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-131">Type the following command to start a setup wizard session:</span></span>
   
    `Invoke-HcsSetupWizard`
2. <span data-ttu-id="fef26-132">처음으로 장치 등록을 위해 설치 마법사를 사용하면 웹 프록시를 구성할 때까지 모든 필요한 네트워크 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-132">If this is the first time that you have used the setup wizard for device registration, you need to configure all the required network settings until you reach the web proxy configuration.</span></span> <span data-ttu-id="fef26-133">장치가 이미 등록되어 있다면 웹 프록시를 구성할 때까지 모든 구성된 네트워크 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-133">If your device is already registered, accept all the configured network settings until you reach the web proxy configuration.</span></span> <span data-ttu-id="fef26-134">설치 마법사에서 웹 프록시 설정을 구성하는 메시지가 표시되면 **예**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-134">In the setup wizard, when prompted to configure web proxy settings, type **Yes**.</span></span>
3. <span data-ttu-id="fef26-135">**웹 프록시 URL**에 대해 웹 프록시 서버의 IP 주소 또는 정규화된 도메인 이름(FQDN) 및 클라우드와 통신할 때 사용하려는 장치인 TCP 포트 번호 장치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-135">For the **Web Proxy URL**, specify the IP address or the fully qualified domain name (FQDN) of your web proxy server and the TCP port number that you would like your device to use when communicating with the cloud.</span></span> <span data-ttu-id="fef26-136">이때 다음 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-136">Use the following format:</span></span>
   
    `http://<IP address or FQDN of the web proxy server>:<TCP port number>`
   
    <span data-ttu-id="fef26-137">기본적으로 TCP 포트 번호 8080가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-137">By default, TCP port number 8080 is specified.</span></span>
4. <span data-ttu-id="fef26-138">인증 유형으로 **NTLM**, **기본** 또는 **없음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-138">Choose the authentication type as **NTLM**, **Basic**, or **None**.</span></span> <span data-ttu-id="fef26-139">기본은 프록시 서버 구성에 대한 최소한의 보안 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-139">Basic is the least secure authentication for the proxy server configuration.</span></span> <span data-ttu-id="fef26-140">NT LAN 관리자(NTLM)는 3방향 메시징 시스템을 사용(추가 무결성이 필요하면 4방향)하여 사용자를 인증하는 안전하고 복잡한 인증 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-140">NT LAN Manager (NTLM) is a highly secure and complex authentication protocol that uses a three-way messaging system (sometimes four if additional integrity is required) to authenticate a user.</span></span> <span data-ttu-id="fef26-141">기본 인증은 NTLM입니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-141">The default authentication is NTLM.</span></span> <span data-ttu-id="fef26-142">자세한 내용은 [기본](http://hc.apache.org/httpclient-3.x/authentication.html) 및 [NTLM 인증](http://hc.apache.org/httpclient-3.x/authentication.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fef26-142">For more information, see [Basic](http://hc.apache.org/httpclient-3.x/authentication.html) and [NTLM authentication](http://hc.apache.org/httpclient-3.x/authentication.html).</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="fef26-143">**StorSimple 장치 관리자 서비스에서는 해당 장치에 대한 프록시 서버 구성에서 기본 또는 NTLM 인증이 사용되면 장치 모니터링 차트가 실행되지 않습니다. 작업할 모니터링 차트의 경우 인증이 NONE으로 설정되어 있는지 확인해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="fef26-143">**In the StorSimple Device Manager service, the device monitoring charts do not work when Basic or NTLM authentication is enabled in the proxy server configuration for the device. For the monitoring charts to work, you need to ensure that authentication is set to NONE.**</span></span>
  
5. <span data-ttu-id="fef26-144">인증을 사용하도록 설정한 경우 **웹 프록시 사용자 이름** 및 **웹 프록시 암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-144">If you enabled the authentication, supply a **Web Proxy Username** and a **Web Proxy Password**.</span></span> <span data-ttu-id="fef26-145">또한 암호를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-145">You also need to confirm the password.</span></span>
   
    ![StorSimple 장치1에서 웹 프록시 구성](./media/storsimple-configure-web-proxy/IC751830.png)

<span data-ttu-id="fef26-147">처음으로 장치를 등록하는 경우 등록을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-147">If you are registering your device for the first time, continue with the registration.</span></span> <span data-ttu-id="fef26-148">이미 장치가 등록된 경우 마법사가 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-148">If your device was already registered, the wizard exits.</span></span> <span data-ttu-id="fef26-149">구성된 설정은 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-149">The configured settings are saved.</span></span>

<span data-ttu-id="fef26-150">이제 웹 프록시를 사용하도록 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-150">Web proxy is now enabled.</span></span> <span data-ttu-id="fef26-151">[웹 프록시를 사용하도록 설정](#enable-web-proxy) 단계를 건너뛰고 [Azure Portal에서 웹 프록시 설정 보기](#view-web-proxy-settings-in-the-azure-portal)로 바로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-151">You can skip the [Enable web proxy](#enable-web-proxy) step and go directly to [View web proxy settings in the Azure portal](#view-web-proxy-settings-in-the-azure-portal).</span></span>

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a><span data-ttu-id="fef26-152">StorSimple cmdlet용 Windows PowerShell을 통해 웹 프록시 구성</span><span class="sxs-lookup"><span data-stu-id="fef26-152">Configure web proxy via Windows PowerShell for StorSimple cmdlets</span></span>

<span data-ttu-id="fef26-153">웹 프록시 설정을 구성하는 다른 방법은 StorSimple cmdlet용 Windows PowerShell을 통한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-153">An alternate way to configure web proxy settings is via the Windows PowerShell for StorSimple cmdlets.</span></span> <span data-ttu-id="fef26-154">다음 단계를 수행하여 웹 프록시를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-154">Perform the following steps to configure web proxy.</span></span>

#### <a name="to-configure-web-proxy-via-cmdlets"></a><span data-ttu-id="fef26-155">cmdlet를 통해 웹 프록시를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="fef26-155">To configure web proxy via cmdlets</span></span>
1. <span data-ttu-id="fef26-156">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-156">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="fef26-157">메시지가 표시되면 **장치 관리자 암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-157">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="fef26-158">기본 암호는 `Password1`입니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-158">The default password is `Password1`.</span></span>
2. <span data-ttu-id="fef26-159">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-159">At the command prompt, type:</span></span>
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    <span data-ttu-id="fef26-160">메시지가 표시되면 암호를 제공하고 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-160">Provide and confirm the password when prompted.</span></span>
   
    ![StorSimple 장치3에서 웹 프록시 구성](./media/storsimple-configure-web-proxy/IC751831.png)

<span data-ttu-id="fef26-162">웹 프록시를 구성하고 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-162">The web proxy is now configured and needs to be enabled.</span></span>

## <a name="enable-web-proxy"></a><span data-ttu-id="fef26-163">웹 프록시 활성화</span><span class="sxs-lookup"><span data-stu-id="fef26-163">Enable web proxy</span></span>

<span data-ttu-id="fef26-164">웹 프록시는 기본적으로 사용하지 않도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-164">Web proxy is disabled by default.</span></span> <span data-ttu-id="fef26-165">StorSimple 장치에서 웹 프록시 설정을 구성한 후에 StorSimple용 Windows PowerShell을 사용하여 웹 프록시 설정을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-165">After you configure the web proxy settings on your StorSimple device, use the Windows PowerShell for StorSimple to enable the web proxy settings.</span></span>

> [!NOTE]
> <span data-ttu-id="fef26-166">**설치 마법사를 사용하여 웹 프록시를 구성하는 경우 이 단계가 필요하지 않습니다. 웹 프록시는 설치 마법사 세션 후 기본적으로 자동으로 사용하도록 설정됩니다.**</span><span class="sxs-lookup"><span data-stu-id="fef26-166">**This step is not required if you used the setup wizard to configure web proxy. Web proxy is automatically enabled by default after a setup wizard session.**</span></span>


<span data-ttu-id="fef26-167">장치에서 웹 프록시를 사용하려면 StorSimple용 Windows PowerShell에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-167">Perform the following steps in Windows PowerShell for StorSimple to enable web proxy on your device:</span></span>

#### <a name="to-enable-web-proxy"></a><span data-ttu-id="fef26-168">웹 프록시를 활성화하려면</span><span class="sxs-lookup"><span data-stu-id="fef26-168">To enable web proxy</span></span>
1. <span data-ttu-id="fef26-169">직렬 콘솔 메뉴에서 옵션 1, **모든 권한으로 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-169">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="fef26-170">메시지가 표시되면 **장치 관리자 암호**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-170">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="fef26-171">기본 암호는 `Password1`입니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-171">The default password is `Password1`.</span></span>
2. <span data-ttu-id="fef26-172">명령 프롬프트에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-172">At the command prompt, type:</span></span>
   
    `Enable-HcsWebProxy`
   
    <span data-ttu-id="fef26-173">StorSimple 장치에서 웹 프록시 구성을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-173">You have now enabled the web proxy configuration on your StorSimple device.</span></span>
   
    ![StorSimple 장치4에서 웹 프록시 구성](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-the-azure-portal"></a><span data-ttu-id="fef26-175">Azure Portal에서 웹 프록시 설정 보기</span><span class="sxs-lookup"><span data-stu-id="fef26-175">View web proxy settings in the Azure portal</span></span>

<span data-ttu-id="fef26-176">웹 프록시 설정은 Windows PowerShell 인터페이스를 통해 구성하며 포털에서 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-176">The web proxy settings are configured through the Windows PowerShell interface and cannot be changed from within the portal.</span></span> <span data-ttu-id="fef26-177">하지만 포털에서 이러한 구성된 설정을 볼 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-177">You can, however, view these configured settings in the portal.</span></span> <span data-ttu-id="fef26-178">다음 단계를 수행하여 웹 프록시를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-178">Perform the following steps to view web proxy.</span></span>

#### <a name="to-view-web-proxy-settings"></a><span data-ttu-id="fef26-179">웹 프록시 설정을 보려면</span><span class="sxs-lookup"><span data-stu-id="fef26-179">To view web proxy settings</span></span>
1. <span data-ttu-id="fef26-180">**StorSimple 장치 관리자 서비스 > 장치**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-180">Navigate to **StorSimple Device Manager service > Devices**.</span></span> <span data-ttu-id="fef26-181">장치를 선택하여 클릭하고 **장치 설정 > 네트워크**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-181">Select and click a device and then go to **Device settings > Network**.</span></span>

    ![네트워크 클릭](./media/storsimple-8000-configure-web-proxy/view-web-proxy-1.png)

2. <span data-ttu-id="fef26-183">**네트워크 설정** 블레이드에서 **웹 프록시** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-183">In the **Network settings** blade, click the **Web proxy** tile.</span></span>

    ![웹 프록시 클릭](./media/storsimple-8000-configure-web-proxy/view-web-proxy-2.png)

3. <span data-ttu-id="fef26-185">**웹 프록시** 블레이드에서 StorSimple 장치에 구성된 웹 프록시 설정을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-185">In the **Web proxy** blade, review the configured web proxy settings on your StorSimple device.</span></span>
   
    ![웹 프록시 설정 보기](./media/storsimple-8000-configure-web-proxy/view-web-proxy-3.png)


## <a name="errors-during-web-proxy-configuration"></a><span data-ttu-id="fef26-187">웹 프록시 구성하는 동안 오류</span><span class="sxs-lookup"><span data-stu-id="fef26-187">Errors during web proxy configuration</span></span>

<span data-ttu-id="fef26-188">웹 프록시 설정이 제대로 구성되지 않으면 StorSimple용 Windows PowerShell에서 사용자에게 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-188">If the web proxy settings are configured incorrectly, error messages are displayed to the user in Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="fef26-189">다음 테이블에서 이러한 오류 메시지, 가능한 원인 및 권장되는 작업 중 일부를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-189">The following table explains some of these error messages, their probable causes, and recommended actions.</span></span>

| <span data-ttu-id="fef26-190">일련 번호</span><span class="sxs-lookup"><span data-stu-id="fef26-190">Serial no.</span></span> | <span data-ttu-id="fef26-191">HRESULT 오류 코드</span><span class="sxs-lookup"><span data-stu-id="fef26-191">HRESULT error Code</span></span> | <span data-ttu-id="fef26-192">가능한 근본 원인</span><span class="sxs-lookup"><span data-stu-id="fef26-192">Possible root cause</span></span> | <span data-ttu-id="fef26-193">권장 작업</span><span class="sxs-lookup"><span data-stu-id="fef26-193">Recommended action</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="fef26-194">1.</span><span class="sxs-lookup"><span data-stu-id="fef26-194">1.</span></span> |<span data-ttu-id="fef26-195">0x80070001</span><span class="sxs-lookup"><span data-stu-id="fef26-195">0x80070001</span></span> |<span data-ttu-id="fef26-196">명령은 수동 컨트롤러에서 실행되고 활성 컨트롤러와 통신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-196">Command is run from the passive controller and it is not able to communicate with the active controller.</span></span> |<span data-ttu-id="fef26-197">활성 컨트롤러에서 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-197">Run the command on the active controller.</span></span> <span data-ttu-id="fef26-198">수동 컨트롤러에서 명령을 실행하려면 수동에서 활성 컨트롤러로 연결을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-198">To run the command from the passive controller, you must fix the connectivity from passive to active controller.</span></span> <span data-ttu-id="fef26-199">이 연결이 끊어진 경우 Microsoft 지원과 연계해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-199">You must engage Microsoft Support if this connectivity is broken.</span></span> |
| <span data-ttu-id="fef26-200">2.</span><span class="sxs-lookup"><span data-stu-id="fef26-200">2.</span></span> |<span data-ttu-id="fef26-201">0x800710dd - 작업 식별자가 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-201">0x800710dd - The operation identifier is not valid</span></span> |<span data-ttu-id="fef26-202">프록시 설정은 StorSimple Cloud Appliance에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-202">Proxy settings are not supported on StorSimple Cloud Appliance.</span></span> |<span data-ttu-id="fef26-203">프록시 설정은 StorSimple Cloud Appliance에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-203">Proxy settings are not supported on StorSimple Cloud Appliance.</span></span> <span data-ttu-id="fef26-204">물리적 StorSimple 장치에만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-204">These can only be configured on a StorSimple physical device.</span></span> |
| <span data-ttu-id="fef26-205">3.</span><span class="sxs-lookup"><span data-stu-id="fef26-205">3.</span></span> |<span data-ttu-id="fef26-206">0x80070057 - 잘못된 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fef26-206">0x80070057 - Invalid parameter</span></span> |<span data-ttu-id="fef26-207">프록시 설정에 대해 제공된 매개 변수 중 하나가 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-207">One of the parameters provided for the proxy settings is not valid.</span></span> |<span data-ttu-id="fef26-208">URI는 올바른 형식으로 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-208">The URI is not provided in correct format.</span></span> <span data-ttu-id="fef26-209">다음 형식을 사용하세요. `http://<IP address or FQDN of the web proxy server>:<TCP port number>`</span><span class="sxs-lookup"><span data-stu-id="fef26-209">Use the following format: `http://<IP address or FQDN of the web proxy server>:<TCP port number>`</span></span> |
| <span data-ttu-id="fef26-210">4.</span><span class="sxs-lookup"><span data-stu-id="fef26-210">4.</span></span> |<span data-ttu-id="fef26-211">0x800706ba - RPC 서버를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="fef26-211">0x800706ba - RPC server not available</span></span> |<span data-ttu-id="fef26-212">근본 원인은 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-212">The root cause is one of the following:</span></span></br></br><span data-ttu-id="fef26-213">클러스터가 켜지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-213">Cluster is not up.</span></span> </br></br><span data-ttu-id="fef26-214">데이터 경로 서비스가 실행되고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-214">Datapath service is not running.</span></span></br></br><span data-ttu-id="fef26-215">명령은 수동 컨트롤러에서 실행되고 활성 컨트롤러와 통신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-215">The command is run from passive controller and it is not able to communicate with the active controller.</span></span> |<span data-ttu-id="fef26-216">Microsoft 지원과 연계하여 클러스터가 작동하고 데이터 경로 서비스가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-216">Engage Microsoft Support to ensure that the cluster is up and datapath service is running.</span></span></br></br><span data-ttu-id="fef26-217">활성 컨트롤러에서 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-217">Run the command from the active controller.</span></span> <span data-ttu-id="fef26-218">수동 컨트롤러에서 명령을 실행하려는 경우 수동 컨트롤러가 활성 컨트롤러와 통신할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-218">If you want to run the command from the passive controller, you must ensure that the passive controller can communicate with the active controller.</span></span> <span data-ttu-id="fef26-219">이 연결이 끊어진 경우 Microsoft 지원과 연계해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-219">You must engage Microsoft Support if this connectivity is broken.</span></span> |
| <span data-ttu-id="fef26-220">5.</span><span class="sxs-lookup"><span data-stu-id="fef26-220">5.</span></span> |<span data-ttu-id="fef26-221">0x800706be - RPC 호출 실패</span><span class="sxs-lookup"><span data-stu-id="fef26-221">0x800706be - RPC call failed</span></span> |<span data-ttu-id="fef26-222">클러스터의 작동이 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-222">Cluster is down.</span></span> |<span data-ttu-id="fef26-223">Microsoft 지원과 연계하여 클러스터가 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-223">Engage Microsoft Support to ensure that the cluster is up.</span></span> |
| <span data-ttu-id="fef26-224">6.</span><span class="sxs-lookup"><span data-stu-id="fef26-224">6.</span></span> |<span data-ttu-id="fef26-225">0x8007138f - 클러스터 리소스를 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="fef26-225">0x8007138f - Cluster resource not found</span></span> |<span data-ttu-id="fef26-226">플랫폼 서비스 클러스터 리소스를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-226">Platform service cluster resource is not found.</span></span> <span data-ttu-id="fef26-227">설치가 올바르지 않은 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-227">This can happen when the installation was not proper.</span></span> |<span data-ttu-id="fef26-228">장치에서 공장 재설정을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-228">You may need to perform a factory reset on your device.</span></span> <span data-ttu-id="fef26-229">플랫폼 리소스를 만들어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-229">You may need to create a platform resource.</span></span> <span data-ttu-id="fef26-230">Microsoft 지원에 다음 단계를 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-230">Contact Microsoft Support for next steps.</span></span> |
| <span data-ttu-id="fef26-231">7.</span><span class="sxs-lookup"><span data-stu-id="fef26-231">7.</span></span> |<span data-ttu-id="fef26-232">0x8007138c - 클러스터 리소스는 온라인 상태가 아님</span><span class="sxs-lookup"><span data-stu-id="fef26-232">0x8007138c - Cluster resource not online</span></span> |<span data-ttu-id="fef26-233">플랫폼 또는 데이터 경로 클러스터 리소스는 온라인 상태가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-233">Platform or datapath cluster resources are not online.</span></span> |<span data-ttu-id="fef26-234">Microsoft 지원에 문의하여 데이터 경로 및 플랫폼 서비스 리소스가 온라인 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-234">Contact Microsoft Support to help ensure that the datapath and platform service resource are online.</span></span> |

> [!NOTE]
> * <span data-ttu-id="fef26-235">위의 오류 메시지 목록은 전체 목록이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-235">The above list of error messages is not exhaustive.</span></span>
> * <span data-ttu-id="fef26-236">웹 프록시 설정에 관련된 오류는 StorSimple 장치 관리자 서비스의 Azure Portal에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fef26-236">Errors related to web proxy settings will not be displayed in the Azure portal in your StorSimple Device Manager service.</span></span> <span data-ttu-id="fef26-237">구성이 완료된 후에 웹 프록시에 문제가 있다면 클래식 포털에서 장치 상태가 **오프라인** 으로 변경됩니다. |</span><span class="sxs-lookup"><span data-stu-id="fef26-237">If there is an issue with web proxy after the configuration is completed, the device status will change to **Offline** in the classic portal.|</span></span>

## <a name="next-steps"></a><span data-ttu-id="fef26-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fef26-238">Next Steps</span></span>
* <span data-ttu-id="fef26-239">장치를 배포하거나 웹 프록시 설정을 구성하는 동안 문제가 발생하면 [StorSimple 장치 배포 문제 해결](storsimple-troubleshoot-deployment.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fef26-239">If you experience any issues while deploying your device or configuring web proxy settings, refer to [Troubleshoot your StorSimple device deployment](storsimple-troubleshoot-deployment.md).</span></span>
* <span data-ttu-id="fef26-240">StorSimple 장치 관리자 서비스를 사용하는 방법을 알아보려면 [StorSimple 장치 관리자 서비스를 사용하여 StorSimple 장치 관리](storsimple-8000-manager-service-administration.md)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="fef26-240">To learn how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

