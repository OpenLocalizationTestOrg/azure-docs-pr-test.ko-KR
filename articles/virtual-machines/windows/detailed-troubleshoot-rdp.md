---
title: "Azure에서 원격 데스크톱 상세 문제 해결 | Microsoft Docs"
description: "Azure에서 Windows 가상 컴퓨터에 연결할 수 없는 원격 데스크톱 오류에 대한 자세한 문제 해결 단계 검토"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "원격 데스크탑에 연결할 수 없습니다, 원격 데스크톱 문제 해결, 원격 데스크톱을 연결할 수 없습니다, 원격 데스크톱 오류, 원격 데스크톱 문제 해결, 원격 데스크톱 문제"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: 22080b9402b13fd8162024db10aef5475880e4a7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-to-windows-vms-in-azure"></a><span data-ttu-id="5c6f9-104">Azure의 Windows VM에 대한 원격 데스크톱 연결 문제의 자세한 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="5c6f9-104">Detailed troubleshooting steps for remote desktop connection issues to Windows VMs in Azure</span></span>
<span data-ttu-id="5c6f9-105">이 문서에서는 Windows 기반 Azure 가상 컴퓨터에 대한 복잡한 원격 데스크톱 오류를 진단 및 해결하는 자세한 문제 해결 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-105">This article provides detailed troubleshooting steps to diagnose and fix complex Remote Desktop errors for Windows-based Azure virtual machines.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c6f9-106">일반적인 원격 데스크톱 오류를 제거하려면 계속하기 전에 [원격 데스크톱에 대한 기본적인 문제 해결 문서](troubleshoot-rdp-connection.md)를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-106">To eliminate the more common Remote Desktop errors, make sure to read [the basic troubleshooting article for Remote Desktop](troubleshoot-rdp-connection.md) before proceeding.</span></span>

<span data-ttu-id="5c6f9-107">[기본 원격 데스크톱 문제 해결 가이드](troubleshoot-rdp-connection.md)에 나오는 특정 오류 메시지와 유사하지 않는 원격 데스크톱 오류 메시지가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-107">You may encounter a Remote Desktop error message that does not resemble any of the specific error messages covered in [the basic Remote Desktop troubleshooting guide](troubleshoot-rdp-connection.md).</span></span> <span data-ttu-id="5c6f9-108">RDP(원격 데스크톱) 클라이언트에서 Azure VM의 RDP 서비스에 연결할 수 없는 이유를 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-108">Follow these steps to determine why the Remote Desktop (RDP) client is unable to connect to the RDP service on the Azure VM.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="5c6f9-109">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-109">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="5c6f9-110">또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-110">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="5c6f9-111">[Azure 지원 사이트](https://azure.microsoft.com/support/options/) 로 이동하여 **지원 받기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-111">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span> <span data-ttu-id="5c6f9-112">Azure 지원을 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/support/faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-112">For information about using Azure Support, read the [Microsoft Azure Support FAQ](https://azure.microsoft.com/support/faq/).</span></span>

## <a name="components-of-a-remote-desktop-connection"></a><span data-ttu-id="5c6f9-113">원격 데스크톱 연결을 위한 구성 요소</span><span class="sxs-lookup"><span data-stu-id="5c6f9-113">Components of a Remote Desktop connection</span></span>
<span data-ttu-id="5c6f9-114">다음은 RDP 연결과 관련된 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-114">The following components are involved in an RDP connection:</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

<span data-ttu-id="5c6f9-115">진행하기 전에 마지막으로 VM에 대한 원격 데스크톱 연결을 성공한 이후로 변경된 사항을 마음속으로 생각해보는 것이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-115">Before proceeding, it might help to mentally review what has changed since the last successful Remote Desktop connection to the VM.</span></span> <span data-ttu-id="5c6f9-116">예:</span><span class="sxs-lookup"><span data-stu-id="5c6f9-116">For example:</span></span>

* <span data-ttu-id="5c6f9-117">VM 또는 VM을 포함하는 클라우드 서비스의 공용 IP 주소(가상 IP 주소 [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)라고도 함)가 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-117">The public IP address of the VM or the cloud service containing the VM (also called the virtual IP address [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) has changed.</span></span> <span data-ttu-id="5c6f9-118">DNS 클라이언트 캐시에 DNS 이름에 대해 등록된 *이전 IP 주소* 가 있으므로 RDP 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-118">The RDP failure could be because your DNS client cache still has the *old IP address* registered for the DNS name.</span></span> <span data-ttu-id="5c6f9-119">DNS 클라이언트 캐시를 플러시하고 VM 연결을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-119">Flush your DNS client cache and try connecting the VM again.</span></span> <span data-ttu-id="5c6f9-120">또는 새 VIP와 직접 연결을 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-120">Or try connecting directly with the new VIP.</span></span>
* <span data-ttu-id="5c6f9-121">Azure Portal에서 생성된 연결을 사용하는 대신, 타사 응용 프로그램을 사용하여 원격 데스크톱 연결을 관리하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-121">You are using a third-party application to manage your Remote Desktop connections instead of using the connection generated by the Azure portal.</span></span> <span data-ttu-id="5c6f9-122">응용 프로그램 구성에 원격 데스크톱 트래픽에 대한 올바른 TCP 포트가 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-122">Verify that the application configuration includes the correct TCP port for the Remote Desktop traffic.</span></span> <span data-ttu-id="5c6f9-123">[Azure Portal](https://portal.azure.com)에서 VM의 설정 > 끝점을 클릭하여 클래식 가상 컴퓨터에 대한 이 포트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-123">You can check this port for a classic virtual machine in the [Azure portal](https://portal.azure.com), by clicking the VM's Settings > Endpoints.</span></span>

## <a name="preliminary-steps"></a><span data-ttu-id="5c6f9-124">준비 단계</span><span class="sxs-lookup"><span data-stu-id="5c6f9-124">Preliminary steps</span></span>
<span data-ttu-id="5c6f9-125">자세한 문제 해결을 계속하기 전에 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-125">Before proceeding to the detailed troubleshooting,</span></span>

* <span data-ttu-id="5c6f9-126">Azure Portal에서 확실한 문제가 있는지 가상 컴퓨터의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-126">Check the status of the virtual machine in the Azure portal for any obvious issues.</span></span>
* <span data-ttu-id="5c6f9-127">[기본적인 문제 해결 가이드의 일반적인 RDP 오류에 대한 빠른 해결 단계](troubleshoot-rdp-connection.md#quick-troubleshooting-steps)를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-127">Follow the [quick fix steps for common RDP errors in the basic troubleshooting guide](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).</span></span>

<span data-ttu-id="5c6f9-128">이 단계를 거친 후 원격 데스크톱을 통해 VM에 다시 연결하세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-128">Try reconnecting to the VM via Remote Desktop after these steps.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="5c6f9-129">자세한 문제 해결</span><span class="sxs-lookup"><span data-stu-id="5c6f9-129">Detailed troubleshooting steps</span></span>
<span data-ttu-id="5c6f9-130">다음과 같은 원본에서 발생한 문제 때문에 원격 데스크톱 클라이언트가 Azure VM의 원격 데스크톱 서비스에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-130">The Remote Desktop client may not be able to reach the Remote Desktop service on the Azure VM due to issues at the following sources:</span></span>

* [<span data-ttu-id="5c6f9-131">원격 데스크톱 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="5c6f9-131">Remote Desktop client computer</span></span>](#source-1-remote-desktop-client-computer)
* [<span data-ttu-id="5c6f9-132">조직 인트라넷 에지 장치</span><span class="sxs-lookup"><span data-stu-id="5c6f9-132">Organization intranet edge device</span></span>](#source-2-organization-intranet-edge-device)
* [<span data-ttu-id="5c6f9-133">클라우드 서비스 끝점 및 액세스 제어 목록(ACL)</span><span class="sxs-lookup"><span data-stu-id="5c6f9-133">Cloud service endpoint and access control list (ACL)</span></span>](#source-3-cloud-service-endpoint-and-acl)
* [<span data-ttu-id="5c6f9-134">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="5c6f9-134">Network security groups</span></span>](#source-4-network-security-groups)
* [<span data-ttu-id="5c6f9-135">Windows 기반 Azure VM</span><span class="sxs-lookup"><span data-stu-id="5c6f9-135">Windows-based Azure VM</span></span>](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a><span data-ttu-id="5c6f9-136">발생지 1: 원격 데스크톱 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="5c6f9-136">Source 1: Remote Desktop client computer</span></span>
<span data-ttu-id="5c6f9-137">컴퓨터가 다른 온-프레미스, Windows 기반 컴퓨터에 대한 원격 데스크톱 연결을 설정할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-137">Verify that your computer can make Remote Desktop connections to another on-premises, Windows-based computer.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

<span data-ttu-id="5c6f9-138">연결할 수 없는 경우 컴퓨터에서 다음 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-138">If you cannot, check for the following settings on your computer:</span></span>

* <span data-ttu-id="5c6f9-139">원격 데스크톱 트래픽을 차단하는 로컬 방화벽 설정</span><span class="sxs-lookup"><span data-stu-id="5c6f9-139">A local firewall setting that is blocking Remote Desktop traffic.</span></span>
* <span data-ttu-id="5c6f9-140">원격 데스크톱 연결을 방지하는 로컬에 설치된 클라이언트 프록시 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="5c6f9-140">Locally installed client proxy software that is preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="5c6f9-141">원격 데스크톱 연결을 방지하는 로컬에 설치된 네트워크 모니터링 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="5c6f9-141">Locally installed network monitoring software that is preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="5c6f9-142">트래픽을 모니터링하거나 특정 유형의 트래픽을 허용/비허용하며 원격 데스크톱 연결을 방지하는 다른 유형의 보안 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="5c6f9-142">Other types of security software that either monitor traffic or allow/disallow specific types of traffic that is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="5c6f9-143">이러한 모든 경우에 일시적으로 소프트웨어를 사용하지 않도록 설정하고 원격 데스크톱을 통해 온-프레미스 컴퓨터에 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-143">In all these cases, temporarily disable the software and try to connect to an on-premises computer via Remote Desktop.</span></span> <span data-ttu-id="5c6f9-144">이러한 방식으로 실제 원인을 찾을 수 있는 경우 네트워크 관리자와 협력하여 원격 데스크톱 연결을 허용하도록 소프트웨어 설정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-144">If you can find out the actual cause this way, work with your network administrator to correct the software settings to allow Remote Desktop connections.</span></span>

## <a name="source-2-organization-intranet-edge-device"></a><span data-ttu-id="5c6f9-145">발생지 2: 조직 인트라넷 에지 장치</span><span class="sxs-lookup"><span data-stu-id="5c6f9-145">Source 2: Organization intranet edge device</span></span>
<span data-ttu-id="5c6f9-146">인터넷에 직접 연결된 컴퓨터가 Azure 가상 컴퓨터에 대한 원격 데스크톱 연결을 설정할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-146">Verify that a computer directly connected to the Internet can make Remote Desktop connections to your Azure virtual machine.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

<span data-ttu-id="5c6f9-147">인터넷에 직접 연결된 컴퓨터가 없는 경우 리소스 그룹 또는 클라우드 서비스에서 새 Azure 가상 컴퓨터로 만들고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-147">If you do not have a computer that is directly connected to the Internet, create and test with a new Azure virtual machine in a resource group or cloud service.</span></span> <span data-ttu-id="5c6f9-148">자세한 내용은 [Azure에서 Windows를 실행하는 가상 컴퓨터 만들기](../virtual-machines-windows-hero-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-148">For more information, see [Create a virtual machine running Windows in Azure](../virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="5c6f9-149">테스트가 완료되면 가상 컴퓨터와 리소스 그룹 또는 클라우드 서비스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-149">You can delete the virtual machine and the resource group or the cloud service, after the test.</span></span>

<span data-ttu-id="5c6f9-150">인터넷에 직접 연결된 컴퓨터로 원격 데스크톱에 연결할 수 있는 경우 조직 인트라넷 에지 장치에서 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-150">If you can create a Remote Desktop connection with a computer directly attached to the Internet, check your organization intranet edge device for:</span></span>

* <span data-ttu-id="5c6f9-151">인터넷에 대한 HTTPS 연결을 차단하는 내부 방화벽</span><span class="sxs-lookup"><span data-stu-id="5c6f9-151">An internal firewall blocking HTTPS connections to the Internet.</span></span>
* <span data-ttu-id="5c6f9-152">원격 데스크톱 연결을 방지하는 프록시 서버</span><span class="sxs-lookup"><span data-stu-id="5c6f9-152">A proxy server preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="5c6f9-153">경계 네트워크의 장치에서 실행되는, 원격 데스크톱 연결을 방지하는 침입 탐지 또는 네트워크 모니터링 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="5c6f9-153">Intrusion detection or network monitoring software running on devices in your edge network that is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="5c6f9-154">네트워크 관리자와 협력하여 인터넷과 HTTPS 기반 원격 데스크톱의 연결을 허용하도록 조직 인트라넷 에지 장치 설정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-154">Work with your network administrator to correct the settings of your organization intranet edge device to allow HTTPS-based Remote Desktop connections to the Internet.</span></span>

## <a name="source-3-cloud-service-endpoint-and-acl"></a><span data-ttu-id="5c6f9-155">발생지 3: 클라우드 서비스 끝점 및 ACL</span><span class="sxs-lookup"><span data-stu-id="5c6f9-155">Source 3: Cloud service endpoint and ACL</span></span>
<span data-ttu-id="5c6f9-156">클래식 배포 모델을 사용하여 만든 VM의 경우 동일한 클라우드 서비스 또는 가상 네트워크에 있는 다른 Azure VM이 사용자의 Azure VM으로 원격 데스크톱 연결을 설정할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-156">For VMs created using the Classic deployment model, verify that another Azure VM that is in the same cloud service or virtual network can make Remote Desktop connections to your Azure VM.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> <span data-ttu-id="5c6f9-157">리소스 관리자에서 만든 가상 컴퓨터의 경우, [소스 4: 네트워크 보안 그룹](#source-4-network-security-groups)으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-157">For virtual machines created in Resource Manager, skip to [Source 4: Network Security Groups](#source-4-network-security-groups).</span></span>

<span data-ttu-id="5c6f9-158">동일한 클라우드 서비스 또는 가상 네트워크에 다른 가상 컴퓨터가 없는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-158">If you do not have another virtual machine in the same cloud service or virtual network, create one.</span></span> <span data-ttu-id="5c6f9-159">[Azure에서 Windows를 실행하는 가상 컴퓨터 만들기](../virtual-machines-windows-hero-tutorial.md)의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-159">Follow the steps in [Create a virtual machine running Windows in Azure](../virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="5c6f9-160">테스트가 완료된 후에 테스트 가상 컴퓨터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-160">Delete the test virtual machine after the test is completed.</span></span>

<span data-ttu-id="5c6f9-161">원격 데스크톱을 통해 동일한 클라우드 서비스 또는 가상 네트워크의 가상 컴퓨터에 연결할 수 있는 경우 다음 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-161">If you can connect via Remote Desktop to a virtual machine in the same cloud service or virtual network, check for these settings:</span></span>

* <span data-ttu-id="5c6f9-162">대상 VM에서 원격 데스크톱 트래픽에 대한 끝점 구성: 끝점의 개인 TCP 포트는 VM의 원격 데스크톱 서비스가 수신 대기하는 TCP 포트와 일치해야 합니다(기본값 3389).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-162">The endpoint configuration for Remote Desktop traffic on the target VM: The private TCP port of the endpoint must match the TCP port on which the VM's Remote Desktop service is listening (default is 3389).</span></span>
* <span data-ttu-id="5c6f9-163">대상 VM에서 원격 데스크톱 트래픽 끝점에 대한 ACL: ACL은 인터넷에서 들어오는 트래픽을 원본 IP 주소에 따라 허용 또는 거부하도록 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-163">The ACL for the Remote Desktop traffic endpoint on the target VM: ACLs allow you to specify allowed or denied incoming traffic from the Internet based on its source IP address.</span></span> <span data-ttu-id="5c6f9-164">ACL이 잘못 구성될 경우 끝점에 원격 데스크톱 트래픽이 들어오지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-164">Misconfigured ACLs can prevent incoming Remote Desktop traffic to the endpoint.</span></span> <span data-ttu-id="5c6f9-165">ACL을 확인하고 프록시 또는 다른 에지 서버의 공용 IP 주소에서 들어오는 트래픽이 허용되어 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-165">Check your ACLs to ensure that incoming traffic from your public IP addresses of your proxy or other edge server is allowed.</span></span> <span data-ttu-id="5c6f9-166">자세한 내용은 [네트워크 ACL(액세스 제어 목록)이란?](../../virtual-network/virtual-networks-acl.md)</span><span class="sxs-lookup"><span data-stu-id="5c6f9-166">For more information, see [What is a Network Access Control List (ACL)?](../../virtual-network/virtual-networks-acl.md)</span></span>

<span data-ttu-id="5c6f9-167">끝점이 문제의 발생지인지 확인하려면 현재 끝점을 제거하고 새 끝점을 만든 후 외부 포트 번호에 49152-65535 범위의 임의 포트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-167">To check if the endpoint is the source of the problem, remove the current endpoint and create a new one, choosing a random port in the range 49152–65535 for the external port number.</span></span> <span data-ttu-id="5c6f9-168">자세한 내용은 [가상 컴퓨터로 끝점을 설정하는 방법](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-168">For more information, see [How to set up endpoints to a virtual machine](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="source-4-network-security-groups"></a><span data-ttu-id="5c6f9-169">소스 4: 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="5c6f9-169">Source 4: Network Security Groups</span></span>
<span data-ttu-id="5c6f9-170">네트워크 보안 그룹은 허용되는 인바운드 및 아웃바운드 트래픽을 더 세부적으로 제어하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-170">Network Security Groups allow more granular control of allowed inbound and outbound traffic.</span></span> <span data-ttu-id="5c6f9-171">Azure 가상 네트워크의 서브넷 및 클라우드 서비스에 적용되는 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-171">You can create rules spanning subnets and cloud services in an Azure virtual network.</span></span>

<span data-ttu-id="5c6f9-172">[IP 흐름 확인](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md)을 사용하여 네트워크 보안 그룹의 규칙이 가상 컴퓨터 간에 트래픽을 차단하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-172">Use [IP flow verify](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) to confirm if a rule in a Network Security Group is blocking traffic to or from a virtual machine.</span></span> <span data-ttu-id="5c6f9-173">효과적인 보안 그룹 규칙을 검토하여 인바운드 "허용" NSG 규칙이 있는지와 해당 규칙이 RDP 포트(기본값: 3389)에 우선적으로 사용되도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-173">You can also review effective security group rules to ensure inbound "Allow" NSG rule exists and is prioritized for RDP port(default 3389).</span></span> <span data-ttu-id="5c6f9-174">자세한 내용은 [효과적인 보안 규칙을 사용하여 VM 트래픽 흐름 문제 해결](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-174">For more information, see [Using Effective Security Rules to troubleshoot VM traffic flow](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).</span></span>

## <a name="source-5-windows-based-azure-vm"></a><span data-ttu-id="5c6f9-175">발생지 5: Windows 기반 Azure VM</span><span class="sxs-lookup"><span data-stu-id="5c6f9-175">Source 5: Windows-based Azure VM</span></span>
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

<span data-ttu-id="5c6f9-176">[이 문서](reset-rdp.md)의 지침에 따르세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-176">Follow the instructions in [this article](reset-rdp.md).</span></span> <span data-ttu-id="5c6f9-177">이 문서는 가상 컴퓨터에서 원격 데스크톱 서비스를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-177">This article resets the Remote Desktop service on the virtual machine:</span></span>

* <span data-ttu-id="5c6f9-178">"원격 데스크톱" Windows 방화벽 기본 규칙(TCP 포트 3389)이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-178">Enable the "Remote Desktop" Windows Firewall default rule (TCP port 3389).</span></span>
* <span data-ttu-id="5c6f9-179">HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections 레지스트리 값이 0으로 설정되어 원격 데스크톱 연결이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-179">Enable Remote Desktop connections by setting the HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections registry value to 0.</span></span>

<span data-ttu-id="5c6f9-180">컴퓨터에서 연결을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-180">Try the connection from your computer again.</span></span> <span data-ttu-id="5c6f9-181">여전히 원격 데스크톱을 통해 연결할 수 없다면 다음과 같은 가능한 문제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-181">If you are still not able to connect via Remote Desktop, check for the following possible problems:</span></span>

* <span data-ttu-id="5c6f9-182">원격 데스크톱 서비스가 대상 VM에서 실행되고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-182">The Remote Desktop service is not running on the target VM.</span></span>
* <span data-ttu-id="5c6f9-183">원격 데스크톱 서비스가 TCP 포트 3389에서 수신 대기하고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-183">The Remote Desktop service is not listening on TCP port 3389.</span></span>
* <span data-ttu-id="5c6f9-184">Windows 방화벽 또는 다른 로컬 방화벽에 원격 데스크톱 트래픽을 방지하는 아웃바운드 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-184">Windows Firewall or another local firewall has an outbound rule that is preventing Remote Desktop traffic.</span></span>
* <span data-ttu-id="5c6f9-185">Azure 가상 컴퓨터에서 실행 중인 침입 탐지 또는 네트워크 모니터링 소프트웨어가 원격 데스크톱 연결을 방지하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-185">Intrusion detection or network monitoring software running on the Azure virtual machine is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="5c6f9-186">클래식 배포 모델을 사용하여 만든 VM의 경우 Azure 가상 컴퓨터에 대해 원격 Azure PowerShell 세션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-186">For VMs created using the classic deployment model, you can use a remote Azure PowerShell session to the Azure virtual machine.</span></span> <span data-ttu-id="5c6f9-187">먼저 가상 컴퓨터의 호스팅 클라우드 서비스에 대 인증서를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-187">First, you need to install a certificate for the virtual machine's hosting cloud service.</span></span> <span data-ttu-id="5c6f9-188">[Azure 가상 컴퓨터에 대한 보안 원격 PowerShell 액세스 구성](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) 으로 이동하고 **InstallWinRMCertAzureVM.ps1** 스크립트 파일을 로컬 컴퓨터에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-188">Go to [Configure Secure Remote PowerShell Access to Azure Virtual Machines](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) and download the **InstallWinRMCertAzureVM.ps1** script file to your local computer.</span></span>

<span data-ttu-id="5c6f9-189">다음으로, 아직 없는 경우 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-189">Next, install Azure PowerShell if you haven't already.</span></span> <span data-ttu-id="5c6f9-190">[Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-190">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="5c6f9-191">다음으로, Azure PowerShell 명령 프롬프트를 열고 현재 폴더를 **InstallWinRMCertAzureVM.ps1** 스크립트 파일 위치로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-191">Next, open an Azure PowerShell command prompt and change the current folder to the location of the **InstallWinRMCertAzureVM.ps1** script file.</span></span> <span data-ttu-id="5c6f9-192">Azure PowerShell 스크립트를 실행하려면 올바른 실행 정책을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-192">To run an Azure PowerShell script, you must set the correct execution policy.</span></span> <span data-ttu-id="5c6f9-193">현재 정책 수준을 지정하려면 **Get-ExecutionPolicy** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-193">Run the **Get-ExecutionPolicy** command to determine your current policy level.</span></span> <span data-ttu-id="5c6f9-194">적절한 수준을 설정하는 방법에 대한 자세한 내용은 [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-194">For information about setting the appropriate level, see [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).</span></span>

<span data-ttu-id="5c6f9-195">Azure 구독 이름, 클라우드 서비스 이름 및 해당 가상 컴퓨터 이름(< and > 문자 제거)을 입력하고 이러한 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-195">Next, fill in your Azure subscription name, the cloud service name, and your virtual machine name (removing the < and > characters), and then run these commands.</span></span>

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of the cloud service that contains the target virtual machine>"
$vmName="<Name of the target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

<span data-ttu-id="5c6f9-196">*Get-AzureSubscription* 명령 표시의 **SubscriptionName** 속성에서 올바른 구독 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-196">You can get the correct subscription name from the *SubscriptionName* property of the display of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="5c6f9-197">**Get-AzureVM** 명령 표시의 *ServiceName* 열에서 가상 컴퓨터의 클라우드 서비스 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-197">You can get the cloud service name for the virtual machine from the *ServiceName* column in the display of the **Get-AzureVM** command.</span></span>

<span data-ttu-id="5c6f9-198">새 인증서가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-198">Check if you have the new certificate.</span></span> <span data-ttu-id="5c6f9-199">현재 사용자에 대한 인증서 스냅인을 열고 **Trusted Root Certification Authorities\Certificates** 폴더를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-199">Open a Certificates snap-in for the current user and look in the **Trusted Root Certification Authorities\Certificates** folder.</span></span> <span data-ttu-id="5c6f9-200">인증서 발급 대상 열에 클라우드 서비스의 DNS 이름을 가진 인증서가 표시되어야 합니다(예: cloudservice4testing.cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="5c6f9-200">You should see a certificate with the DNS name of your cloud service in the Issued To column (example: cloudservice4testing.cloudapp.net).</span></span>

<span data-ttu-id="5c6f9-201">다음으로, 이러한 명령을 사용하여 원격 Azure PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-201">Next, initiate a remote Azure PowerShell session by using these commands.</span></span>

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

<span data-ttu-id="5c6f9-202">유효한 관리자 자격 증명을 입력한 후 다음 Azure PowerShell 프롬프트와 비슷한 내용이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-202">After entering valid administrator credentials, you should see something similar to the following Azure PowerShell prompt:</span></span>

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

<span data-ttu-id="5c6f9-203">이 프롬프트의 첫 번째 부분은 대상 VM을 포함하는 클라우드 서비스 이름으로, "cloudservice4testing.cloudapp.net"과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-203">The first part of this prompt is your cloud service name that contains the target VM, which could be different from "cloudservice4testing.cloudapp.net".</span></span> <span data-ttu-id="5c6f9-204">이제 이 클라우드 서비스에 대해 Azure PowerShell 명령을 실행하여 언급된 문제를 조사하고 구성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-204">You can now issue Azure PowerShell commands for this cloud service to investigate the problems mentioned and correct the configuration.</span></span>

### <a name="to-manually-correct-the-remote-desktop-services-listening-tcp-port"></a><span data-ttu-id="5c6f9-205">TCP 포트에서 수신 대기하는 원격 데스크톱 서비스를 수동으로 수정하려면</span><span class="sxs-lookup"><span data-stu-id="5c6f9-205">To manually correct the Remote Desktop Services listening TCP port</span></span>
<span data-ttu-id="5c6f9-206">원격 Azure PowerShell 세션 프롬프트에서 이 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-206">At the remote Azure PowerShell session prompt, run this command.</span></span>

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

<span data-ttu-id="5c6f9-207">PortNumber 속성은 현재 포트 번호를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-207">The PortNumber property shows the current port number.</span></span> <span data-ttu-id="5c6f9-208">필요한 경우 이 명령을 사용하여 원격 데스크톱 포트 번호를 다시 기본값(3389)으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-208">If needed, change the Remote Desktop port number back to its default value (3389) by using this command.</span></span>

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

<span data-ttu-id="5c6f9-209">이 명령을 사용하여 포트가 3389로 변경되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-209">Verify that the port has been changed to 3389 by using this command.</span></span>

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

<span data-ttu-id="5c6f9-210">이 명령을 사용하여 원격 Azure PowerShell 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-210">Exit the remote Azure PowerShell session by using this command.</span></span>

```powershell
Exit-PSSession
```

<span data-ttu-id="5c6f9-211">Azure VM에 대한 원격 데스크톱 끝점도 TCP 포트 3398을 내부 포트로 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-211">Verify that the Remote Desktop endpoint for the Azure VM is also using TCP port 3398 as its internal port.</span></span> <span data-ttu-id="5c6f9-212">Azure VM을 다시 시작한 후 원격 데스크톱 연결을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="5c6f9-212">Restart the Azure VM and try the Remote Desktop connection again.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c6f9-213">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5c6f9-213">Additional resources</span></span>
[<span data-ttu-id="5c6f9-214">Windows 가상 컴퓨터에 대한 원격 데스크톱 서비스 또는 암호를 다시 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="5c6f9-214">How to reset a password or the Remote Desktop service for Windows virtual machines</span></span>](reset-rdp.md)

[<span data-ttu-id="5c6f9-215">Azure PowerShell 설치 및 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="5c6f9-215">How to install and configure Azure PowerShell</span></span>](/powershell/azure/overview)

[<span data-ttu-id="5c6f9-216">Linux 기반 Azure 가상 컴퓨터에 SSH(보안 셸) 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="5c6f9-216">Troubleshoot Secure Shell (SSH) connections to a Linux-based Azure virtual machine</span></span>](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="5c6f9-217">Azure 가상 컴퓨터에서 실행 중인 응용 프로그램에 대한 액세스 문제 해결</span><span class="sxs-lookup"><span data-stu-id="5c6f9-217">Troubleshoot access to an application running on an Azure virtual machine</span></span>](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

