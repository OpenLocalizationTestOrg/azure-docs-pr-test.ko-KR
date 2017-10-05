---
title: "Azure VM에 대한 자세한 SSH 문제 해결 | Microsoft Docs"
description: "Azure 가상 컴퓨터에 연결할 때의 문제에 대한 자세한 SSH 문제 해결 단계"
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
ms.openlocfilehash: 9ccdb3fbca21264065eeb1c4e46314c62af4c2e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-to-a-linux-vm-in-azure"></a><span data-ttu-id="eae38-104">Azure에서 Linux VM에 연결할 때의 문제에 대한 자세한 SSH 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="eae38-104">Detailed SSH troubleshooting steps for issues connecting to a Linux VM in Azure</span></span>
<span data-ttu-id="eae38-105">SSH 클라이언트가 VM의 SSH 서비스에 도달할 수 없는 데에는 여러 원인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-105">There are many possible reasons that the SSH client might not be able to reach the SSH service on the VM.</span></span> <span data-ttu-id="eae38-106">추가적인 [일반 SSH 문제 해결 단계](troubleshoot-ssh-connection.md)를 진행한 경우 연결 문제를 추가적으로 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-106">If you have followed through the more [general SSH troubleshooting steps](troubleshoot-ssh-connection.md), you need to further troubleshoot the connection issue.</span></span> <span data-ttu-id="eae38-107">이 문서에서는 SSH 연결에 문제가 있는지 확인하는 자세한 문제 해결 단계와 해결 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-107">This article guides you through detailed troubleshooting steps to determine where the SSH connection is failing and how to resolve it.</span></span>

## <a name="take-preliminary-steps"></a><span data-ttu-id="eae38-108">준비 단계 수행</span><span class="sxs-lookup"><span data-stu-id="eae38-108">Take preliminary steps</span></span>
<span data-ttu-id="eae38-109">다음 다이어그램은 관련된 구성 요소를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-109">The following diagram shows the components that are involved.</span></span>

![SSH 서비스의 구성 요소를 보여주는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

<span data-ttu-id="eae38-111">다음 단계는 실패의 원인을 찾아내고 해결 방안을 알아내는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-111">The following steps help you isolate the source of the failure and figure out solutions or workarounds.</span></span>

1. <span data-ttu-id="eae38-112">포털에서 VM의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-112">Check the status of the VM in the portal.</span></span>
   <span data-ttu-id="eae38-113">[Azure Portal](https://portal.azure.com)에서 **가상 컴퓨터** > *VM 이름*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-113">In the [Azure portal](https://portal.azure.com), select **Virtual machines** > *VM name*.</span></span>

   <span data-ttu-id="eae38-114">VM에 대한 상태 창에 **실행 중**이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-114">The status pane for the VM should show **Running**.</span></span> <span data-ttu-id="eae38-115">아래로 스크롤하여 계산, 저장소 및 네트워크 리소스에 대한 최근 활동을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-115">Scroll down to show recent activity for compute, storage, and network resources.</span></span>

2. <span data-ttu-id="eae38-116">**설정** 을 선택하여 끝점, IP 주소, 네트워크 보안 그룹 및 기타 설정을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-116">Select **Settings** to examine endpoints, IP addresses, network security groups, and other settings.</span></span>

   <span data-ttu-id="eae38-117">VM에는 **끝점** 또는  **[네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md)**에서 볼 수 있는 SSH 트래픽에 대해 정의된 끝점이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-117">The VM should have an endpoint defined for SSH traffic that you can view in **Endpoints** or **[Network security group](../../virtual-network/virtual-networks-nsg.md)**.</span></span> <span data-ttu-id="eae38-118">Resource Manager를 사용하여 만든 VM의 끝점은 네트워크 보안 그룹에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-118">Endpoints in VMs that were created by using Resource Manager are stored in a network security group.</span></span> <span data-ttu-id="eae38-119">또한 규칙이 네트워크 보안 그룹에 적용되어 있고 서브넷에서 참조되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-119">Also, verify that the rules have been applied to the network security group and that they're referenced in the subnet.</span></span>

<span data-ttu-id="eae38-120">네트워크 연결 상태를 확인하려면 구성된 끝점을 점검하고 HTTP와 같은 다른 프로토콜 또는 다른 서비스를 통해 VM에 연결할 수 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-120">To verify network connectivity, check the configured endpoints and see if you can reach the VM through another protocol, such as HTTP or another service.</span></span>

<span data-ttu-id="eae38-121">이 단계 후 SSH 연결을 다시 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="eae38-121">After these steps, try the SSH connection again.</span></span>

## <a name="find-the-source-of-the-issue"></a><span data-ttu-id="eae38-122">문제의 발생지 찾기</span><span class="sxs-lookup"><span data-stu-id="eae38-122">Find the source of the issue</span></span>
<span data-ttu-id="eae38-123">다음 영역의 문제 또는 잘못된 구성으로 인해 컴퓨터의 SSH 클라이언트에서 Azure VM의 SSH 서비스에 연결하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-123">The SSH client on your computer might fail to reach the SSH service on the Azure VM due to issues or misconfigurations in the following areas:</span></span>

* [<span data-ttu-id="eae38-124">SSH 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="eae38-124">SSH client computer</span></span>](#source-1-ssh-client-computer)
* [<span data-ttu-id="eae38-125">조직 에지 장치</span><span class="sxs-lookup"><span data-stu-id="eae38-125">Organization edge device</span></span>](#source-2-organization-edge-device)
* [<span data-ttu-id="eae38-126">클라우드 서비스 끝점 및 액세스 제어 목록(ACL)</span><span class="sxs-lookup"><span data-stu-id="eae38-126">Cloud service endpoint and access control list (ACL)</span></span>](#source-3-cloud-service-endpoint-and-acl)
* [<span data-ttu-id="eae38-127">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="eae38-127">Network security groups</span></span>](#source-4-network-security-groups)
* [<span data-ttu-id="eae38-128">Linux 기반 Azure VM</span><span class="sxs-lookup"><span data-stu-id="eae38-128">Linux-based Azure VM</span></span>](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a><span data-ttu-id="eae38-129">발생지 1: SSH 클라이언트 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="eae38-129">Source 1: SSH client computer</span></span>
<span data-ttu-id="eae38-130">문제의 발생지인 사용자의 컴퓨터를 제거하려면 사용자의 컴퓨터가 다른 온-프레미스, Linux 기반 컴퓨터에 SSH 연결을 설정할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-130">To eliminate your computer as the source of the failure, verify that it can make SSH connections to another on-premises, Linux-based computer.</span></span>

![SSH 클라이언트 컴퓨터 구성 요소를 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

<span data-ttu-id="eae38-132">연결이 실패하면 컴퓨터에서 다음 문제를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-132">If the connection fails, check for the following issues on your computer:</span></span>

* <span data-ttu-id="eae38-133">인바운드 또는 아웃 바운드 SSH 트래픽(TCP 22)을 차단하는 로컬 방화벽 설정</span><span class="sxs-lookup"><span data-stu-id="eae38-133">A local firewall setting that is blocking inbound or outbound SSH traffic (TCP 22)</span></span>
* <span data-ttu-id="eae38-134">SSH 연결을 방지하는 로컬에 설치된 클라이언트 프록시 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="eae38-134">Locally installed client proxy software that is preventing SSH connections</span></span>
* <span data-ttu-id="eae38-135">SSH 연결을 방지하는 로컬에 설치된 네트워크 모니터링 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="eae38-135">Locally installed network monitoring software that is preventing SSH connections</span></span>
* <span data-ttu-id="eae38-136">트래픽을 모니터링하거나 특정 유형의 트래픽을 허용하거나 허용하지 않는 다른 유형의 보안 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="eae38-136">Other types of security software that either monitor traffic or allow/disallow specific types of traffic</span></span>

<span data-ttu-id="eae38-137">이러한 조건 중 하나가 적용되면 일시적으로 소프트웨어를 사용하지 않도록 설정하고 온-프레미스 컴퓨터에 SSH 연결을 시도하여 컴퓨터에서 연결을 차단하는 원인을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-137">If one of these conditions apply, temporarily disable the software and try an SSH connection to an on-premises computer to find out the reason the connection is being blocked on your computer.</span></span> <span data-ttu-id="eae38-138">그런 다음 네트워크 관리자와 협력하여 SSH 연결을 허용하도록 소프트웨어 설정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-138">Then work with your network administrator to correct the software settings to allow SSH connections.</span></span>

<span data-ttu-id="eae38-139">인증서 인증을 사용하는 경우 홈 디렉터리의 .ssh 폴더에 대해 다음 권한이 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="eae38-139">If you are using certificate authentication, verify that you have these permissions to the .ssh folder in your home directory:</span></span>

* <span data-ttu-id="eae38-140">Chmod 700 ~/.ssh</span><span class="sxs-lookup"><span data-stu-id="eae38-140">Chmod 700 ~/.ssh</span></span>
* <span data-ttu-id="eae38-141">Chmod 644 ~/.ssh/\*.pub</span><span class="sxs-lookup"><span data-stu-id="eae38-141">Chmod 644 ~/.ssh/\*.pub</span></span>
* <span data-ttu-id="eae38-142">Chmod 600 ~/.ssh/id_rsa(또는 개인 키가 저장되어 있는 기타 파일)</span><span class="sxs-lookup"><span data-stu-id="eae38-142">Chmod 600 ~/.ssh/id_rsa (or any other files that have your private keys stored in them)</span></span>
* <span data-ttu-id="eae38-143">Chmod 644 ~/.ssh/known_hosts(SSH를 통해 연결한 호스트 포함)</span><span class="sxs-lookup"><span data-stu-id="eae38-143">Chmod 644 ~/.ssh/known_hosts (contains hosts that you’ve connected to via SSH)</span></span>

## <a name="source-2-organization-edge-device"></a><span data-ttu-id="eae38-144">발생지 2: 조직 에지 장치</span><span class="sxs-lookup"><span data-stu-id="eae38-144">Source 2: Organization edge device</span></span>
<span data-ttu-id="eae38-145">문제의 발생지인 조직의 에지 장치를 제거하려면 인터넷에 직접 연결된 컴퓨터가 Azure 가상 컴퓨터에 SSH 연결을 설정할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-145">To eliminate your organization edge device as the source of the failure, verify that a computer that's directly connected to the Internet can make SSH connections to your Azure VM.</span></span> <span data-ttu-id="eae38-146">사이트 간 VPN 또는 Azure Express 경로 연결을 통해 VM에 액세스하는 경우 [발생지 4: 네트워크 보안 그룹](#nsg)으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-146">If you are accessing the VM over a site-to-site VPN or an Azure ExpressRoute connection, skip to [Source 4: Network security groups](#nsg).</span></span>

![조직 에지 장치를 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

<span data-ttu-id="eae38-148">인터넷에 직접 연결된 컴퓨터가 없는 경우 자체 리소스 그룹에 또는 클라우드 서비스에 새 Azure VM을 만든 후 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-148">If you don't have a computer that is directly connected to the Internet, create a new Azure VM in its own resource group or cloud service and use it.</span></span> <span data-ttu-id="eae38-149">자세한 내용은 [Azure에서 Linux를 실행하는 가상 컴퓨터 만들기](quick-create-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eae38-149">For more information, see [Create a virtual machine running Linux in Azure](quick-create-cli.md).</span></span> <span data-ttu-id="eae38-150">테스트가 완료되면 리소스 그룹 또는 VM 및 클라우드 서비스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-150">Delete the resource group or VM and cloud service when you're done with your testing.</span></span>

<span data-ttu-id="eae38-151">인터넷에 직접 연결된 컴퓨터에 대한 SSH 연결을 설정할 수 있는 경우 조직 에지 장치에서 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-151">If you can create an SSH connection with a computer that's directly connected to the Internet, check your organization edge device for:</span></span>

* <span data-ttu-id="eae38-152">인터넷을 사용하여 SSH 트래픽을 차단하는 내부 방화벽</span><span class="sxs-lookup"><span data-stu-id="eae38-152">An internal firewall that's blocking SSH traffic with the Internet</span></span>
* <span data-ttu-id="eae38-153">SSH 연결을 방지하는 프록시 서버</span><span class="sxs-lookup"><span data-stu-id="eae38-153">A proxy server that's preventing SSH connections</span></span>
* <span data-ttu-id="eae38-154">경계 네트워크의 장치에서 실행되는, SSH 연결을 방지하는 침입 검색 또는 네트워크 모니터링 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="eae38-154">Intrusion detection or network monitoring software running on devices in your edge network that's preventing SSH connections</span></span>

<span data-ttu-id="eae38-155">네트워크 관리자와 협력하여 인터넷에서 SSH 트래픽을 허용하도록 조직 에지 장치 설정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-155">Work with your network administrator to correct the settings of your organization edge devices to allow SSH traffic with the Internet.</span></span>

## <a name="source-3-cloud-service-endpoint-and-acl"></a><span data-ttu-id="eae38-156">발생지 3: 클라우드 서비스 끝점 및 ACL</span><span class="sxs-lookup"><span data-stu-id="eae38-156">Source 3: Cloud service endpoint and ACL</span></span>
> [!NOTE]
> <span data-ttu-id="eae38-157">이 발생지는 클래식 배포 모델을 사용하여 만든 VM에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-157">This source applies only to VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="eae38-158">Resource Manager를 사용하여 만든 VM의 경우 [발생지 4: 네트워크 보안 그룹](#nsg)으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-158">For VMs that were created by using Resource Manager, skip to [source 4: Network security groups](#nsg).</span></span>

<span data-ttu-id="eae38-159">문제의 발생지인 클라우드 서비스 끝점 및 ACL을 제거하려면 동일한 가상 네트워크의 다른 Azure VM이 사용자의 VM에 SSH 연결을 설정할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-159">To eliminate the cloud service endpoint and ACL as the source of the failure, verify that another Azure VM in the same virtual network can make SSH connections to your VM.</span></span>

![클라우드 서비스 끝점 및 ACL을 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

<span data-ttu-id="eae38-161">동일한 가상 네트워크에 다른 VM이 없는 경우 새 가상 컴퓨터를 손쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-161">If you don't have another VM in the same virtual network, you can easily create one.</span></span> <span data-ttu-id="eae38-162">자세한 내용은 [CLI를 사용하여 Azure에서 Linux VM 만들기](quick-create-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eae38-162">For more information, see [Create a Linux VM on Azure using the CLI](quick-create-cli.md).</span></span> <span data-ttu-id="eae38-163">테스트를 마치면 추가한 VM을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-163">Delete the extra VM when you are done with your testing.</span></span>

<span data-ttu-id="eae38-164">동일한 가상 네트워크에 있는 VM과 SSH의 연결을 만들 수 있는 경우 다음 영역을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-164">If you can create an SSH connection with a VM in the same virtual network, check the following areas:</span></span>

* <span data-ttu-id="eae38-165">**대상 VM의 SSH 트래픽에 대한 끝점 구성.**</span><span class="sxs-lookup"><span data-stu-id="eae38-165">**The endpoint configuration for SSH traffic on the target VM.**</span></span> <span data-ttu-id="eae38-166">끝점의 개인 TCP 포트는 VM에서 SSH 서비스가 수신 대기 중인 TCP 포트와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-166">The private TCP port of the endpoint should match the TCP port on which the SSH service on the VM is listening.</span></span> <span data-ttu-id="eae38-167">기본 포트는 22입니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-167">(The default port is 22).</span></span> <span data-ttu-id="eae38-168">**가상 컴퓨터** > *VM 이름* > **설정** > **끝점**을 선택하여 Azure Portal에서 SSH TCP 포트 번호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-168">Verify the SSH TCP port number in the Azure portal by selecting **Virtual machines** > *VM name* > **Settings** > **Endpoints**.</span></span>
* <span data-ttu-id="eae38-169">**대상 가상 컴퓨터의 SSH 트래픽 끝점에 대한 ACL.**</span><span class="sxs-lookup"><span data-stu-id="eae38-169">**The ACL for the SSH traffic endpoint on the target virtual machine.**</span></span> <span data-ttu-id="eae38-170">ACL을 통해 인터넷에서 들어오는 트래픽을 원본 IP 주소에 따라 허용 또는 거부하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-170">An ACL enables you to specify allowed or denied incoming traffic from the Internet, based on its source IP address.</span></span> <span data-ttu-id="eae38-171">ACL이 잘못 구성될 경우 끝점에 SSH 트래픽이 들어오지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-171">Misconfigured ACLs can prevent incoming SSH traffic to the endpoint.</span></span> <span data-ttu-id="eae38-172">ACL을 확인하고 프록시 또는 다른 에지 서버의 공용 IP 주소에서 들어오는 트래픽이 허용되어 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="eae38-172">Check your ACLs to ensure that incoming traffic from the public IP addresses of your proxy or other edge server is allowed.</span></span> <span data-ttu-id="eae38-173">자세한 내용은 [네트워크 ACL(액세스 제어 목록) 정보](../../virtual-network/virtual-networks-acl.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eae38-173">For more information, see [About network access control lists (ACLs)](../../virtual-network/virtual-networks-acl.md).</span></span>

<span data-ttu-id="eae38-174">문제의 발생지인 끝점을 제거하려면 현재 끝점을 제거하고 다른 끝점을 만든 다음 SSH 이름(공용 및 개인 포트 번호에 TCP 포트 22)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-174">To eliminate the endpoint as a source of the problem, remove the current endpoint, create another endpoint, and specify the SSH name (TCP port 22 for the public and private port number).</span></span> <span data-ttu-id="eae38-175">자세한 내용은 [Azure의 가상 컴퓨터에 끝점 설정](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eae38-175">For more information, see [Set up endpoints on a virtual machine in Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a><span data-ttu-id="eae38-176">발생지 4: 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="eae38-176">Source 4: Network security groups</span></span>
<span data-ttu-id="eae38-177">네트워크 보안 그룹을 사용하면 허용되는 인바운드 및 아웃바운드 트래픽을 더 세부적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-177">Network security groups enable you to have more granular control of allowed inbound and outbound traffic.</span></span> <span data-ttu-id="eae38-178">Azure 가상 네트워크의 서브넷 및 클라우드 서비스에 적용되는 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-178">You can create rules that span subnets and cloud services in an Azure virtual network.</span></span> <span data-ttu-id="eae38-179">네트워크 보안 그룹 규칙을 확인하고 인터넷으로 나가고 들어오는 SSH 트래픽이 허용되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-179">Check your network security group rules to ensure that SSH traffic to and from the Internet is allowed.</span></span>
<span data-ttu-id="eae38-180">자세한 내용은 [네트워크 보안 그룹 정보](../../virtual-network/virtual-networks-nsg.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eae38-180">For more information, see [About network security groups](../../virtual-network/virtual-networks-nsg.md).</span></span>

<span data-ttu-id="eae38-181">IP 확인을 사용하여 NSG 구성이 유효한지 검사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-181">You can also use IP Verify to validate the NSG configuration.</span></span> <span data-ttu-id="eae38-182">자세한 내용은 [Azure 네트워크 모니터링 개요](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eae38-182">For more information, see [Azure network monitoring overview](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview).</span></span> 

## <a name="source-5-linux-based-azure-virtual-machine"></a><span data-ttu-id="eae38-183">발생지 5: Linux 기반 Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="eae38-183">Source 5: Linux-based Azure virtual machine</span></span>
<span data-ttu-id="eae38-184">마지막 가능한 문제 발생지는 Azure 가상 컴퓨터 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-184">The last source of possible problems is the Azure virtual machine itself.</span></span>

![Linux 기반 Azure 가상 컴퓨터를 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

<span data-ttu-id="eae38-186">아직 수행하지 않은 경우 [지침에 따라 Linux 기반 가상 컴퓨터에 대한 암호 또는 SSH를 다시 설정](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-186">If you haven't done so already, follow the instructions [to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="eae38-187">컴퓨터에서 다시 연결을 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="eae38-187">Try connecting from your computer again.</span></span> <span data-ttu-id="eae38-188">문제가 계속 발생하면 다음과 같은 문제가 있는 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-188">If it still fails, the following are some of the possible issues:</span></span>

* <span data-ttu-id="eae38-189">SSH 서비스가 대상 가상 컴퓨터에서 실행되고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-189">The SSH service is not running on the target virtual machine.</span></span>
* <span data-ttu-id="eae38-190">SSH 서비스가 TCP 포트 22에서 수신 대기하고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-190">The SSH service is not listening on TCP port 22.</span></span> <span data-ttu-id="eae38-191">테스트하려면 로컬 컴퓨터에 텔넷 클라이언트를 설치하고 "telnet *cloudServiceName*.cloudapp.net 22"를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-191">To test, install a telnet client on your local computer and run "telnet *cloudServiceName*.cloudapp.net 22".</span></span> <span data-ttu-id="eae38-192">이 단계에서는 가상 컴퓨터에서 SSH 끝점에 대한 인바운드 및 아웃바운드 통신을 허용하는지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-192">This step determines if the virtual machine allows inbound and outbound communication to the SSH endpoint.</span></span>
* <span data-ttu-id="eae38-193">대상 가상 컴퓨터의 로컬 방화벽에 인바운드 또는 아웃바운드 SSH 트래픽을 방지하는 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-193">The local firewall on the target virtual machine has rules that are preventing inbound or outbound SSH traffic.</span></span>
* <span data-ttu-id="eae38-194">Azure 가상 컴퓨터에서 실행 중인 침입 검색 또는 네트워크 모니터링 소프트웨어가 SSH 연결을 방지하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eae38-194">Intrusion detection or network monitoring software that's running on the Azure virtual machine is preventing SSH connections.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eae38-195">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="eae38-195">Additional resources</span></span>
<span data-ttu-id="eae38-196">응용 프로그램 액세스 문제를 해결하는 방법에 대한 자세한 내용은 [Azure 가상 컴퓨터에서 실행 중인 응용 프로그램에 대한 액세스 문제 해결](troubleshoot-app-connection.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eae38-196">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](troubleshoot-app-connection.md)</span></span>
