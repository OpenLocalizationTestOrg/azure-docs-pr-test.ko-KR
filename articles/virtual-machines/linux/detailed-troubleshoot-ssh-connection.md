---
title: "Azure VM에 대 한 aaaDetailed SSH 문제 해결 | Microsoft Docs"
description: "더 자세한 문제 해결 단계 tooan Azure 가상 컴퓨터를 연결 하는 문제에 대 한 SSH"
keywords: "ssh 연결 거부,ssh 오류,azure ssh,SSH 연결 실패"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a><span data-ttu-id="3c56e-104">문제 해결 단계는 Azure에서 Linux VM tooa 연결 문제에 대 한 자세한 SSH</span><span class="sxs-lookup"><span data-stu-id="3c56e-104">Detailed SSH troubleshooting steps for issues connecting tooa Linux VM in Azure</span></span>
<span data-ttu-id="3c56e-105">여러 가지가 있습니다 가능한 hello SSH 클라이언트 hello VM에서 수 tooreach hello SSH 서비스 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-105">There are many possible reasons that hello SSH client might not be able tooreach hello SSH service on hello VM.</span></span> <span data-ttu-id="3c56e-106">더 hello를 통해 수행한 경우 [문제 해결 단계는 일반 SSH](troubleshoot-ssh-connection.md), toofurther 필요한 hello 연결 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-106">If you have followed through hello more [general SSH troubleshooting steps](troubleshoot-ssh-connection.md), you need toofurther troubleshoot hello connection issue.</span></span> <span data-ttu-id="3c56e-107">이 문서 과정을 안내해 자세한 문제 해결 단계 toodetermine hello SSH 연결 실패 하는 위치와 방법을 tooresolve 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-107">This article guides you through detailed troubleshooting steps toodetermine where hello SSH connection is failing and how tooresolve it.</span></span>

## <a name="take-preliminary-steps"></a><span data-ttu-id="3c56e-108">준비 단계 수행</span><span class="sxs-lookup"><span data-stu-id="3c56e-108">Take preliminary steps</span></span>
<span data-ttu-id="3c56e-109">hello 다음 그림에 사용 되는 hello 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-109">hello following diagram shows hello components that are involved.</span></span>

![SSH 서비스의 구성 요소를 보여주는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

<span data-ttu-id="3c56e-111">hello 다음 단계 수 hello 소스 hello 실패의 원인을 찾아내서 해결 방법 또는 솔루션을 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-111">hello following steps help you isolate hello source of hello failure and figure out solutions or workarounds.</span></span>

1. <span data-ttu-id="3c56e-112">Hello 포털에서 VM hello의 hello 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-112">Check hello status of hello VM in hello portal.</span></span>
   <span data-ttu-id="3c56e-113">Hello에 [Azure 포털](https://portal.azure.com)선택, **가상 컴퓨터** > *VM 이름*합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-113">In hello [Azure portal](https://portal.azure.com), select **Virtual machines** > *VM name*.</span></span>

   <span data-ttu-id="3c56e-114">hello hello VM에 대 한 상태 창 표시할지 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-114">hello status pane for hello VM should show **Running**.</span></span> <span data-ttu-id="3c56e-115">계산, 저장소 및 네트워크 리소스에 대 한 최근 활동 tooshow 아래로 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="3c56e-115">Scroll down tooshow recent activity for compute, storage, and network resources.</span></span>

2. <span data-ttu-id="3c56e-116">선택 **설정을** tooexamine 끝점, IP 주소, 네트워크 보안 그룹 및 기타 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-116">Select **Settings** tooexamine endpoints, IP addresses, network security groups, and other settings.</span></span>

   <span data-ttu-id="3c56e-117">hello VM에서 볼 수 있는 SSH 트래픽에 대해 정의 된 끝점과 있어야 **끝점** 또는  **[네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md)**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-117">hello VM should have an endpoint defined for SSH traffic that you can view in **Endpoints** or **[Network security group](../../virtual-network/virtual-networks-nsg.md)**.</span></span> <span data-ttu-id="3c56e-118">Resource Manager를 사용하여 만든 VM의 끝점은 네트워크 보안 그룹에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-118">Endpoints in VMs that were created by using Resource Manager are stored in a network security group.</span></span> <span data-ttu-id="3c56e-119">또한, 있는지 hello 규칙 적용된 toohello 네트워크 보안 그룹 추가 되었으며 hello 서브넷에서 참조 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-119">Also, verify that hello rules have been applied toohello network security group and that they're referenced in hello subnet.</span></span>

<span data-ttu-id="3c56e-120">tooverify 네트워크 연결은 hello 구성 된 끝점을 확인 하 고 참조 하는 경우 HTTP 또는 다른 서비스와 같은 다른 프로토콜을 통해 VM hello에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-120">tooverify network connectivity, check hello configured endpoints and see if you can reach hello VM through another protocol, such as HTTP or another service.</span></span>

<span data-ttu-id="3c56e-121">이러한 단계 이후 hello SSH 연결을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3c56e-121">After these steps, try hello SSH connection again.</span></span>

## <a name="find-hello-source-of-hello-issue"></a><span data-ttu-id="3c56e-122">Hello 문제의 hello 소스 찾기</span><span class="sxs-lookup"><span data-stu-id="3c56e-122">Find hello source of hello issue</span></span>
<span data-ttu-id="3c56e-123">컴퓨터에 SSH 클라이언트 hello tooreach hello SSH 서비스 hello Azure VM tooissues 또는 hello 다음 영역에서에서 구성 오류 때문에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-123">hello SSH client on your computer might fail tooreach hello SSH service on hello Azure VM due tooissues or misconfigurations in hello following areas:</span></span>

* [<span data-ttu-id="3c56e-124">SSH 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3c56e-124">SSH client computer</span></span>](#source-1-ssh-client-computer)
* [<span data-ttu-id="3c56e-125">조직 에지 장치</span><span class="sxs-lookup"><span data-stu-id="3c56e-125">Organization edge device</span></span>](#source-2-organization-edge-device)
* [<span data-ttu-id="3c56e-126">클라우드 서비스 끝점 및 액세스 제어 목록(ACL)</span><span class="sxs-lookup"><span data-stu-id="3c56e-126">Cloud service endpoint and access control list (ACL)</span></span>](#source-3-cloud-service-endpoint-and-acl)
* [<span data-ttu-id="3c56e-127">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="3c56e-127">Network security groups</span></span>](#source-4-network-security-groups)
* [<span data-ttu-id="3c56e-128">Linux 기반 Azure VM</span><span class="sxs-lookup"><span data-stu-id="3c56e-128">Linux-based Azure VM</span></span>](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a><span data-ttu-id="3c56e-129">발생지 1: SSH 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3c56e-129">Source 1: SSH client computer</span></span>
<span data-ttu-id="3c56e-130">tooeliminate hello 오류의 hello 소스로 컴퓨터 SSH 연결 tooanother 온-프레미스를 만들 수 있는지를 확인 Linux 기반 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-130">tooeliminate your computer as hello source of hello failure, verify that it can make SSH connections tooanother on-premises, Linux-based computer.</span></span>

![SSH 클라이언트 컴퓨터 구성 요소를 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

<span data-ttu-id="3c56e-132">Hello 연결에 실패 하면 hello에 나오는 문제에 따라 컴퓨터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-132">If hello connection fails, check for hello following issues on your computer:</span></span>

* <span data-ttu-id="3c56e-133">인바운드 또는 아웃 바운드 SSH 트래픽(TCP 22)을 차단하는 로컬 방화벽 설정</span><span class="sxs-lookup"><span data-stu-id="3c56e-133">A local firewall setting that is blocking inbound or outbound SSH traffic (TCP 22)</span></span>
* <span data-ttu-id="3c56e-134">SSH 연결을 방지하는 로컬에 설치된 클라이언트 프록시 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="3c56e-134">Locally installed client proxy software that is preventing SSH connections</span></span>
* <span data-ttu-id="3c56e-135">SSH 연결을 방지하는 로컬에 설치된 네트워크 모니터링 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="3c56e-135">Locally installed network monitoring software that is preventing SSH connections</span></span>
* <span data-ttu-id="3c56e-136">트래픽을 모니터링하거나 특정 유형의 트래픽을 허용하거나 허용하지 않는 다른 유형의 보안 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="3c56e-136">Other types of security software that either monitor traffic or allow/disallow specific types of traffic</span></span>

<span data-ttu-id="3c56e-137">다음이 조건 중 하나를 적용 하는 경우 일시적으로 hello 소프트웨어를 사용 하지 않도록 설정 하 고 컴퓨터에 hello 연결을 차단 하 고 hello 이유 아웃는 SSH 연결 tooan 온-프레미스 컴퓨터 toofind를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3c56e-137">If one of these conditions apply, temporarily disable hello software and try an SSH connection tooan on-premises computer toofind out hello reason hello connection is being blocked on your computer.</span></span> <span data-ttu-id="3c56e-138">그런 다음 네트워크 관리자 toocorrect hello 소프트웨어 설정 tooallow SSH 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-138">Then work with your network administrator toocorrect hello software settings tooallow SSH connections.</span></span>

<span data-ttu-id="3c56e-139">인증서 인증을 사용 하는 경우 홈 디렉터리에 이러한 사용 권한을 toohello.ssh 폴더 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-139">If you are using certificate authentication, verify that you have these permissions toohello .ssh folder in your home directory:</span></span>

* <span data-ttu-id="3c56e-140">Chmod 700 ~/.ssh</span><span class="sxs-lookup"><span data-stu-id="3c56e-140">Chmod 700 ~/.ssh</span></span>
* <span data-ttu-id="3c56e-141">Chmod 644 ~/.ssh/\*.pub</span><span class="sxs-lookup"><span data-stu-id="3c56e-141">Chmod 644 ~/.ssh/\*.pub</span></span>
* <span data-ttu-id="3c56e-142">Chmod 600 ~/.ssh/id_rsa(또는 개인 키가 저장되어 있는 기타 파일)</span><span class="sxs-lookup"><span data-stu-id="3c56e-142">Chmod 600 ~/.ssh/id_rsa (or any other files that have your private keys stored in them)</span></span>
* <span data-ttu-id="3c56e-143">Chmod 644 ~/.ssh/known_hosts (toovia SSH를 연결 하는 호스트 포함)</span><span class="sxs-lookup"><span data-stu-id="3c56e-143">Chmod 644 ~/.ssh/known_hosts (contains hosts that you’ve connected toovia SSH)</span></span>

## <a name="source-2-organization-edge-device"></a><span data-ttu-id="3c56e-144">발생지 2: 조직 에지 장치</span><span class="sxs-lookup"><span data-stu-id="3c56e-144">Source 2: Organization edge device</span></span>
<span data-ttu-id="3c56e-145">tooeliminate hello 오류의 hello 소스로 사용자 조직에 지 장치 toohello 인터넷에 직접 연결에 있는 컴퓨터에 SSH 연결 tooyour Azure VM을 만들 수 있음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-145">tooeliminate your organization edge device as hello source of hello failure, verify that a computer that's directly connected toohello Internet can make SSH connections tooyour Azure VM.</span></span> <span data-ttu-id="3c56e-146">Hello VM에 사이트 간 VPN 이나 Azure express 경로 연결을 통해 액세스 하는 경우 너무 건너뜁니다[소스 4: 네트워크 보안 그룹](#nsg)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-146">If you are accessing hello VM over a site-to-site VPN or an Azure ExpressRoute connection, skip too[Source 4: Network security groups](#nsg).</span></span>

![조직 에지 장치를 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

<span data-ttu-id="3c56e-148">직접 연결 된 toohello 인터넷 되는 컴퓨터에 없을 경우 자체 리소스 그룹 또는 클라우드 서비스에 새 Azure VM 만들고 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-148">If you don't have a computer that is directly connected toohello Internet, create a new Azure VM in its own resource group or cloud service and use it.</span></span> <span data-ttu-id="3c56e-149">자세한 내용은 [Azure에서 Linux를 실행하는 가상 컴퓨터 만들기](quick-create-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c56e-149">For more information, see [Create a virtual machine running Linux in Azure](quick-create-cli.md).</span></span> <span data-ttu-id="3c56e-150">테스트와 완료 되 면 hello 리소스 그룹이 나 VM 및 클라우드 서비스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-150">Delete hello resource group or VM and cloud service when you're done with your testing.</span></span>

<span data-ttu-id="3c56e-151">Toohello 인터넷에 직접 연결에 있는 컴퓨터와 SSH 연결을 만들 수 있습니다, 경우에 대 한 사용자 조직에 지 장치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-151">If you can create an SSH connection with a computer that's directly connected toohello Internet, check your organization edge device for:</span></span>

* <span data-ttu-id="3c56e-152">인터넷 hello 사용 하 여 SSH 트래픽을 차단 하는 내부 방화벽</span><span class="sxs-lookup"><span data-stu-id="3c56e-152">An internal firewall that's blocking SSH traffic with hello Internet</span></span>
* <span data-ttu-id="3c56e-153">SSH 연결을 방지하는 프록시 서버</span><span class="sxs-lookup"><span data-stu-id="3c56e-153">A proxy server that's preventing SSH connections</span></span>
* <span data-ttu-id="3c56e-154">경계 네트워크의 장치에서 실행되는, SSH 연결을 방지하는 침입 검색 또는 네트워크 모니터링 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="3c56e-154">Intrusion detection or network monitoring software running on devices in your edge network that's preventing SSH connections</span></span>

<span data-ttu-id="3c56e-155">인터넷 hello로 조직 가장자리 장치 tooallow SSH 트래픽 네트워크 관리자 toocorrect hello 설정과 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-155">Work with your network administrator toocorrect hello settings of your organization edge devices tooallow SSH traffic with hello Internet.</span></span>

## <a name="source-3-cloud-service-endpoint-and-acl"></a><span data-ttu-id="3c56e-156">발생지 3: 클라우드 서비스 끝점 및 ACL</span><span class="sxs-lookup"><span data-stu-id="3c56e-156">Source 3: Cloud service endpoint and ACL</span></span>
> [!NOTE]
> <span data-ttu-id="3c56e-157">이 소스 hello 클래식 배포 모델을 사용 하 여 만든 tooVMs만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-157">This source applies only tooVMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="3c56e-158">리소스 관리자를 사용 하 여 만든 Vm에 대 한 건너뛸 너무[원본 4: 네트워크 보안 그룹](#nsg)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-158">For VMs that were created by using Resource Manager, skip too[source 4: Network security groups](#nsg).</span></span>

<span data-ttu-id="3c56e-159">다른 Azure VM에 동일을 hello tooeliminate hello 클라우드 서비스 끝점 및 hello 오류의 hello 소스로 ACL 확인 가상 네트워크는 SSH 연결 tooyour VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-159">tooeliminate hello cloud service endpoint and ACL as hello source of hello failure, verify that another Azure VM in hello same virtual network can make SSH connections tooyour VM.</span></span>

![클라우드 서비스 끝점 및 ACL을 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

<span data-ttu-id="3c56e-161">다른 VM hello에 없는 경우 동일한 가상 네트워크를 쉽게 만들 수 있습니다 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-161">If you don't have another VM in hello same virtual network, you can easily create one.</span></span> <span data-ttu-id="3c56e-162">자세한 내용은 참조 [hello CLI를 사용 하 여 Azure에서 Linux VM을 만들](quick-create-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-162">For more information, see [Create a Linux VM on Azure using hello CLI](quick-create-cli.md).</span></span> <span data-ttu-id="3c56e-163">삭제 테스트와 완료 되 면 추가 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-163">Delete hello extra VM when you are done with your testing.</span></span>

<span data-ttu-id="3c56e-164">에 VM으로 SSH 연결을 만들 수 있으면 hello 동일한 가상 네트워크, 영역을 다음 hello 확인:</span><span class="sxs-lookup"><span data-stu-id="3c56e-164">If you can create an SSH connection with a VM in hello same virtual network, check hello following areas:</span></span>

* <span data-ttu-id="3c56e-165">**hello hello 대상 VM에서 SSH 트래픽에 대 한 끝점 구성입니다.**</span><span class="sxs-lookup"><span data-stu-id="3c56e-165">**hello endpoint configuration for SSH traffic on hello target VM.**</span></span> <span data-ttu-id="3c56e-166">hello hello 끝점의 개인 TCP 포트는 hello SSH hello VM에서 서비스 수신 hello TCP 포트를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-166">hello private TCP port of hello endpoint should match hello TCP port on which hello SSH service on hello VM is listening.</span></span> <span data-ttu-id="3c56e-167">(hello 기본 포트는 22).</span><span class="sxs-lookup"><span data-stu-id="3c56e-167">(hello default port is 22).</span></span> <span data-ttu-id="3c56e-168">선택 하 여 hello Azure 포털에에서 hello SSH TCP 포트 번호를 확인 **가상 컴퓨터** > *VM 이름* > **설정**  >  **끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-168">Verify hello SSH TCP port number in hello Azure portal by selecting **Virtual machines** > *VM name* > **Settings** > **Endpoints**.</span></span>
* <span data-ttu-id="3c56e-169">**hello hello 대상 가상 컴퓨터에 SSH 트래픽 끝점 hello에 대 한 ACL 선택 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3c56e-169">**hello ACL for hello SSH traffic endpoint on hello target virtual machine.**</span></span> <span data-ttu-id="3c56e-170">ACL 허용 또는 원본 IP 주소에 기반 하는 hello 인터넷에서에서 들어오는 트래픽을 거부 toospecify가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-170">An ACL enables you toospecify allowed or denied incoming traffic from hello Internet, based on its source IP address.</span></span> <span data-ttu-id="3c56e-171">잘못 구성 된 Acl 들어오는 SSH 트래픽 toohello 끝점을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-171">Misconfigured ACLs can prevent incoming SSH traffic toohello endpoint.</span></span> <span data-ttu-id="3c56e-172">Hello 공용 IP 주소에 프록시 또는 다른 지 서버에서 들어오는 트래픽을 허용 하 여 Acl tooensure를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-172">Check your ACLs tooensure that incoming traffic from hello public IP addresses of your proxy or other edge server is allowed.</span></span> <span data-ttu-id="3c56e-173">자세한 내용은 [네트워크 ACL(액세스 제어 목록) 정보](../../virtual-network/virtual-networks-acl.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c56e-173">For more information, see [About network access control lists (ACLs)](../../virtual-network/virtual-networks-acl.md).</span></span>

<span data-ttu-id="3c56e-174">tooeliminate hello 끝점 hello 문제의 원인으로 hello 현재 끝점을 제거 다른 끝점을 만들고 hello SSH 이름 (TCP 포트 22 hello 공용 및 개인 포트 번호에 대 한)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-174">tooeliminate hello endpoint as a source of hello problem, remove hello current endpoint, create another endpoint, and specify hello SSH name (TCP port 22 for hello public and private port number).</span></span> <span data-ttu-id="3c56e-175">자세한 내용은 [Azure의 가상 컴퓨터에 끝점 설정](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c56e-175">For more information, see [Set up endpoints on a virtual machine in Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a><span data-ttu-id="3c56e-176">발생지 4: 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="3c56e-176">Source 4: Network security groups</span></span>
<span data-ttu-id="3c56e-177">네트워크 보안 그룹 사용 toohave 허용 된 인바운드 및 아웃 바운드 트래픽 더 세부적으로 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-177">Network security groups enable you toohave more granular control of allowed inbound and outbound traffic.</span></span> <span data-ttu-id="3c56e-178">Azure 가상 네트워크의 서브넷 및 클라우드 서비스에 적용되는 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-178">You can create rules that span subnets and cloud services in an Azure virtual network.</span></span> <span data-ttu-id="3c56e-179">사용자 네트워크 보안 그룹 규칙 tooensure 해당 SSH 트래픽 tooand를 인터넷 ï ´ ù hello에서 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3c56e-179">Check your network security group rules tooensure that SSH traffic tooand from hello Internet is allowed.</span></span>
<span data-ttu-id="3c56e-180">자세한 내용은 [네트워크 보안 그룹 정보](../../virtual-network/virtual-networks-nsg.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c56e-180">For more information, see [About network security groups](../../virtual-network/virtual-networks-nsg.md).</span></span>

<span data-ttu-id="3c56e-181">또한 IP 확인 toovalidate hello NSG 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-181">You can also use IP Verify toovalidate hello NSG configuration.</span></span> <span data-ttu-id="3c56e-182">자세한 내용은 [Azure 네트워크 모니터링 개요](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c56e-182">For more information, see [Azure network monitoring overview](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview).</span></span> 

## <a name="source-5-linux-based-azure-virtual-machine"></a><span data-ttu-id="3c56e-183">발생지 5: Linux 기반 Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3c56e-183">Source 5: Linux-based Azure virtual machine</span></span>
<span data-ttu-id="3c56e-184">가능한 문제 hello 마지막 소스는 hello Azure 가상 컴퓨터 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-184">hello last source of possible problems is hello Azure virtual machine itself.</span></span>

![Linux 기반 Azure 가상 컴퓨터를 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

<span data-ttu-id="3c56e-186">아직 수행 하지 않은 경우 hello 지침에 따라 [tooreset 암호 또는 Linux 기반 가상 컴퓨터에 대 한 SSH](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-186">If you haven't done so already, follow hello instructions [tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="3c56e-187">컴퓨터에서 다시 연결을 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="3c56e-187">Try connecting from your computer again.</span></span> <span data-ttu-id="3c56e-188">문제가 계속 발생 hello 다음은 일부 hello 관련 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-188">If it still fails, hello following are some of hello possible issues:</span></span>

* <span data-ttu-id="3c56e-189">SSH 서비스 hello hello 대상 가상 컴퓨터에서 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-189">hello SSH service is not running on hello target virtual machine.</span></span>
* <span data-ttu-id="3c56e-190">hello SSH 서비스는 TCP 포트 22에서 수신 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-190">hello SSH service is not listening on TCP port 22.</span></span> <span data-ttu-id="3c56e-191">tootest, 로컬 컴퓨터의 텔넷 클라이언트를 설치 하 고 실행 "텔넷 *cloudServiceName*. cloudapp.net 22"입니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-191">tootest, install a telnet client on your local computer and run "telnet *cloudServiceName*.cloudapp.net 22".</span></span> <span data-ttu-id="3c56e-192">이 단계는 hello 가상 컴퓨터 인바운드 및 아웃 바운드 통신 toohello SSH 끝점을 허용 하는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-192">This step determines if hello virtual machine allows inbound and outbound communication toohello SSH endpoint.</span></span>
* <span data-ttu-id="3c56e-193">hello hello 대상 가상 컴퓨터에서 로컬 방화벽에 인바운드 또는 아웃 바운드 SSH 트래픽을 방지 하는 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-193">hello local firewall on hello target virtual machine has rules that are preventing inbound or outbound SSH traffic.</span></span>
* <span data-ttu-id="3c56e-194">침입 검색 또는 모니터링 소프트웨어 hello Azure 가상 컴퓨터에서 실행 되는 네트워크 SSH 연결을 차단 중인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c56e-194">Intrusion detection or network monitoring software that's running on hello Azure virtual machine is preventing SSH connections.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3c56e-195">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="3c56e-195">Additional resources</span></span>
<span data-ttu-id="3c56e-196">응용 프로그램 액세스 문제를 해결 하는 방법에 대 한 자세한 내용은 참조 [문제 해결 액세스 tooan 응용 프로그램이 Azure 가상 컴퓨터에서 실행 중인](troubleshoot-app-connection.md)</span><span class="sxs-lookup"><span data-stu-id="3c56e-196">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](troubleshoot-app-connection.md)</span></span>
