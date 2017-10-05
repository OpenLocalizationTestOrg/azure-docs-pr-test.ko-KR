---
title: "Azure에서 Windows 가상 컴퓨터 정품 인증 문제 해결 | Microsoft Docs"
description: "Azure에서 Windows 가상 컴퓨터 정품 인증 문제를 해결하기 위한 문제 해결 단계를 제공합니다."
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 77ef396e0bf75fab56bda2e76516b481d018c5b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="137d5-103">Windows Azure 가상 컴퓨터 정품 인증 문제 해결</span><span class="sxs-lookup"><span data-stu-id="137d5-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="137d5-104">사용자 지정 이미지에서 만든 Azure Windows VM(가상 컴퓨터)을 활성화하는 데 문제가 발생하는 경우 문제를 해결하려면 이 문서에 제공된 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use the information provided in this document to troubleshoot the issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="137d5-105">증상</span><span class="sxs-lookup"><span data-stu-id="137d5-105">Symptom</span></span>

<span data-ttu-id="137d5-106">Windows Azure VM을 활성화하려고 할 때 다음 샘플과 유사한 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-106">When you try to activate an Azure Windows VM, you receive an error message resembles the following sample:</span></span>

<span data-ttu-id="137d5-107">**오류: 0xC004F074 보고된 소프트웨어 라이센싱 서비스를 컴퓨터에서 활성화할 수 없습니다. KMS(Key Management Service)를 연결할 수 없습니다. 추가 정보는 응용 프로그램 이벤트 로그를 참조하세요.**</span><span class="sxs-lookup"><span data-stu-id="137d5-107">**Error: 0xC004F074 The Software LicensingService reported that the computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see the Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="137d5-108">원인</span><span class="sxs-lookup"><span data-stu-id="137d5-108">Cause</span></span>
<span data-ttu-id="137d5-109">일반적으로 Azure VM 정품 인증 문제는 Windows VM이 적절한 KMS 클라이언트 설정 키를 사용하여 구성되어 있지 않거나 Windows VM에 Azure KMS 서비스(kms.core.windows.net, 포트 1668)에 대한 연결 문제가 있는 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-109">Generally, Azure VM activation issues occur if the Windows VM is not configured by using the appropriate KMS client setup key, or the Windows VM has a connectivity problem to the Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="137d5-110">해결 방법</span><span class="sxs-lookup"><span data-stu-id="137d5-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="137d5-111">사이트 간 VPN 및 강제 터널링을 사용하는 경우 [강제 터널링을 사용하여 KMS 정품 인증을 활성화하도록 Azure 사용자 지정 경로 사용](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="137d5-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes to enable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="137d5-112">ExpressRoute를 사용하고 기본 경로가 게시된 경우 [Azure VM이 ExpressRoute를 통해 활성화되지 못했습니다.](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="137d5-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail to activate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-the-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="137d5-113">1단계 적절한 KMS 클라이언트 설정 키 구성(Windows Server 2016 및 Windows Server 2012 R2용)</span><span class="sxs-lookup"><span data-stu-id="137d5-113">Step 1 Configure the appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="137d5-114">Windows Server 2016 또는 Windows Server 2012 R2의 사용자 지정 이미지에서 만든 VM의 경우 VM에 적절한 KMS 클라이언트 설정 키를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-114">For the VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure the appropriate KMS client setup key for the VM.</span></span>

<span data-ttu-id="137d5-115">이 단계는 Windows 2012 또는 Windows 2008 R2에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-115">This step does not apply to Windows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="137d5-116">Windows Server 2016 및 Windows Server 2012 R2에서만 지원되는 AVMA(Automation Virtual Machine Activation) 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-116">It uses the Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="137d5-117">관리자 권한의 명령 프롬프트에서 **slmgr.vbs /dlv**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="137d5-118">출력에서 설명 값을 확인하고 소매(소매 채널) 또는 볼륨(VOLUME_KMSCLIENT) 라이선스 미디어에서 만들어졌는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-118">Check the Description value in the output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="137d5-119">**slmgr.vbs /dlv**가 소매 채널을 표시하는 경우 다음 명령을 실행하여 사용된 Windows Server의 버전에 [KMS 클라이언트 설정 키](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396)를 설정하고 활성화를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-119">If **slmgr.vbs /dlv** shows RETAIL channel, run the following commands to set the [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for the version of Windows Server being used, and force it to retry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="137d5-120">예를 들어 Windows Server 2016 데이터 센터에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-120">For example, for Windows Server 2016 Datacenter, you would run the following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-the-connectivity-between-the-vm-and-azure-kms-service"></a><span data-ttu-id="137d5-121">2단계 VM과 Azure KMS 서비스 간의 연결 확인</span><span class="sxs-lookup"><span data-stu-id="137d5-121">Step 2 Verify the connectivity between the VM and Azure KMS service</span></span>

1. <span data-ttu-id="137d5-122">[Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) 도구를 활성화하지 않는 VM의 로컬 폴더에 다운로드하고 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-122">Download and extract the [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool to a local folder in the VM that does not activate.</span></span> 

2. <span data-ttu-id="137d5-123">시작하고 Windows PowerShell에서 검색하고 Windows PowerShell을 마우스 오른쪽 단추로 클릭한 다음 관리자 권한으로 실행을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-123">Go to Start, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="137d5-124">VM이 올바른 Azure KMS 서버를 사용하도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-124">Make sure that the VM is configured to use the correct Azure KMS server.</span></span> <span data-ttu-id="137d5-125">이렇게 하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-125">To do this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="137d5-126">명령이 다음을 반환해야 합니다. 키 관리 서비스 컴퓨터 이름을 kms.core.windows.net:1688으로 성공적으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-126">The command should return: Key Management Service machine name set to kms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="137d5-127">KMS 서버에 연결한 Psping을 사용하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-127">Verify by using Psping that you have connectivity to the KMS server.</span></span> <span data-ttu-id="137d5-128">Pstools.zip 다운로드를 추출한 폴더로 전환하고 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-128">Switch to the folder where you extracted the Pstools.zip download, and then run the following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="137d5-129">출력의 마지막 두 번째 줄에서 전송 = 4, 수신 = 4, 손실 = 0 (0% 손실)이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-129">In the second-to-last line of the output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="137d5-130">손실이 0(영)보다 큰 경우 VM은 KMS 서버에 연결되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-130">If Lost is greater than 0 (zero), the VM does not have connectivity to the KMS server.</span></span> <span data-ttu-id="137d5-131">이 경우에 VM이 가상 네트워크에 있고 사용자 지정 DNS 서버를 지정하면 해당 DNS 서버가 kms.core.windows.net을 확인할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-131">In this situation, if the VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able to resolve kms.core.windows.net.</span></span> <span data-ttu-id="137d5-132">또는 DNS 서버가 kms.core.windows.net을 확인할 수 있도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-132">Or, change the DNS server to one that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="137d5-133">모든 DNS 서버를 가상 네트워크에서 제거하면 VM은 Azure의 내부 DNS 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="137d5-134">이 서비스는 kms.core.windows.net을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="137d5-135">또한 게스트 방화벽이 정품 인증 시도를 차단하는 방식으로 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-135">Also verify that the guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="137d5-136">kms.core.windows.net에 성공적으로 연결되었는지 확인한 후에 해당 관리자 권한 Windows PowerShell 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-136">After you verify successful connectivity to kms.core.windows.net, run the following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="137d5-137">이 명령은 여러 번 활성화되도록 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="137d5-138">성공적으로 활성화되면 다음과 같은 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-138">A successful activation returns information that resembles the following:</span></span>

<span data-ttu-id="137d5-139">**Windows(R), ServerDatacenter 버전 활성화(12345678-1234-1234-1234-12345678) … 제품을 성공적으로 활성화했습니다.**</span><span class="sxs-lookup"><span data-stu-id="137d5-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="137d5-140">FAQ</span><span class="sxs-lookup"><span data-stu-id="137d5-140">FAQ</span></span> 

### <a name="i-created-the-windows-server-2016-from-azure-marketplace-do-i-need-to-configure-kms-key-for-activating-the-windows-server-2016"></a><span data-ttu-id="137d5-141">Azure Marketplace에서 Windows Server 2016을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-141">I created the Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="137d5-142">Windows Server 2016을 활성화하기 위해 KMS 키를 구성해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="137d5-142">Do I need to configure KMS key for activating the Windows Server 2016?</span></span> 
 
<span data-ttu-id="137d5-143">아니요.</span><span class="sxs-lookup"><span data-stu-id="137d5-143">No.</span></span> <span data-ttu-id="137d5-144">Azure Marketplace의 이미지는 적절한 KMS 클라이언트 설정 키를 이미 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-144">The image in Azure Marketplace has the appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-the-same-way-regardless-if-the-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="137d5-145">VM이 Azure HUB(Hybrid Use Benefit)를 사용하는지 여부와 상관없이 동일하게 Windows 정품 인증이 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="137d5-145">Does Windows activation work the same way regardless if the VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="137d5-146">예.</span><span class="sxs-lookup"><span data-stu-id="137d5-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="137d5-147">Windows 정품 인증 기간이 만료된 경우 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="137d5-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="137d5-148">유예 기간이 만료되고 Windows가 여전히 활성화되지 않은 경우 Windows Server 2008 R2 및 Windows 이후 버전은 정품 인증에 대한 추가 알림을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-148">When the grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="137d5-149">바탕 화면 배경 화면을 검은색으로 유지하고 Windows 업데이트를 통해 보안 및 중요 업데이트만을 설치하고 선택 사항 업데이트를 설치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="137d5-149">The desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="137d5-150">[라이선스 조건](http://technet.microsoft.com/en-us/library/ff793403.aspx) 페이지의 맨 아래에 있는 알림 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="137d5-150">See  the Notifications section at the bottom of the [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="137d5-151">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="137d5-151">Need help?</span></span> <span data-ttu-id="137d5-152">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="137d5-152">Contact support.</span></span>
<span data-ttu-id="137d5-153">다른 도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="137d5-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>