---
title: "aaaCreate 네트워킹이 Accelerated Azure 가상 컴퓨터 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 네트워킹이 가속화 됩니다. 가상 컴퓨터."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="37b15-103">가속화된 네트워킹을 사용하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="37b15-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="37b15-104">이 자습서에 설명 어떻게 toocreate 네트워킹이 Accelerated Azure 가상 컴퓨터 (VM).</span><span class="sxs-lookup"><span data-stu-id="37b15-104">In this tutorial, you learn how toocreate an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="37b15-105">가속화된 네트워킹은 Windows용 GA이고 특정 Linux 배포를 위한 공개 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="37b15-106">가속된 네트워킹 단일 루트 I/O 가상화 (SR-IOV) tooa 네트워킹 성능을 크게 향상 VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-106">Accelerated networking enables single root I/O virtualization (SR-IOV) tooa VM, greatly improving its networking performance.</span></span> <span data-ttu-id="37b15-107">이 성능 우선 경로 대기 시간, 지터, 및 지원 되는 VM 형식에 대 한 hello 가장 까다로운 네트워크 작업에 사용할 CPU 사용률 줄이기 hello 데이터 경로에서 호스트의 hello를 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-107">This high-performance path bypasses hello host from hello datapath reducing latency, jitter, and CPU utilization, for use with hello most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="37b15-108">hello와 가속된 네트워킹 없는 두 가상 컴퓨터 (VM) 간의 그림 표시 통신 다음:</span><span class="sxs-lookup"><span data-stu-id="37b15-108">hello following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![비교](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="37b15-110">가속된 네트워킹 없이 hello VM 내부 및 외부의 모든 네트워킹 트래픽 hello 호스트 및 가상 스위치 hello 트래버스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-110">Without accelerated networking, all networking traffic in and out of hello VM must traverse hello host and hello virtual switch.</span></span> <span data-ttu-id="37b15-111">예: 네트워크 보안 그룹으로 액세스 제어 목록, 격리 및 기타 가상화 된 네트워크 서비스 toonetwork 트래픽의 hello 가상 스위치 모든 정책 적용을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-111">hello virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services toonetwork traffic.</span></span> <span data-ttu-id="37b15-112">가상 스위치, hello 읽기에 대 한 자세한 toolearn [Hyper-v 네트워크 가상화 및 가상 스위치](https://technet.microsoft.com/library/jj945275.aspx) 문서.</span><span class="sxs-lookup"><span data-stu-id="37b15-112">toolearn more about virtual switches, read hello [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="37b15-113">가속 네트워킹 네트워크 트래픽을 hello VM의 네트워크 인터페이스 (NIC)에 도착 하 고 toohello VM 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-113">With accelerated networking, network traffic arrives at hello VM's network interface (NIC), and is then forwarded toohello VM.</span></span> <span data-ttu-id="37b15-114">가속된 네트워킹 오프 로드 되어 하드웨어에 적용 하지 않고 hello 가상 스위치는 모든 네트워크 정책에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-114">All network policies that hello virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="37b15-115">하드웨어 사용 hello NIC tooforward에 정책을 적용 네트워크 트래픽을 직접 toohello VM을 hello 호스트에 적용 되는 모든 hello 정책을 유지 하면서 hello 호스트 및 hello 가상 스위치를 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-115">Applying policy in hardware enables hello NIC tooforward network traffic directly toohello VM, bypassing hello host and hello virtual switch, while maintaining all hello policy it applied in hello host.</span></span>

<span data-ttu-id="37b15-116">hello 가속화 된 네트워킹의 이점만 적용 toohello VM에서 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-116">hello benefits of accelerated networking only apply toohello VM that it is enabled on.</span></span> <span data-ttu-id="37b15-117">이상적인 tooenable hello 최상의 결과 두 개 이상의 Vm에서이 기능은 연결 toohello 동일한 Azure 가상 네트워크 (VNet).</span><span class="sxs-lookup"><span data-stu-id="37b15-117">For hello best results, it is ideal tooenable this feature on at least two VMs connected toohello same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="37b15-118">Vnet 또는 연결 온-프레미스에서 통신,이 기능에 영향을 최소화 toooverall 대기 시간에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-118">When communicating across VNets or connecting on-premises, this feature has minimal impact toooverall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="37b15-119">일반적 가용성 해제 된이 Linux 공개 미리 보기에는 동일한 수준의 가용성 및 안정성 기능으로 hello를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-119">This Linux Public Preview may not have hello same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="37b15-120">hello 기능은 지원 되지 않습니다, 기능, 제한 있을 수 있습니다 및 모든 Azure 위치에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-120">hello feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="37b15-121">가용성 및이 기능의 상태에 최신 알림 hello에 대 한 hello Azure 가상 네트워크 업데이트 페이지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-121">For hello most up-to-date notifications on availability and status of this feature, check hello Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="37b15-122">이점</span><span class="sxs-lookup"><span data-stu-id="37b15-122">Benefits</span></span>
* <span data-ttu-id="37b15-123">**대기 시간이 / 높은 패킷 / 초 (pps):** hello 데이터 경로에서 제거 하는 hello 가상 스위치 정책 처리에 대 한 hello 호스트에 패킷을 보내는 hello 시간과 제거 하 고 증가 hello hello VM 내에 처리할 수 있는 패킷 수입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-123">**Lower Latency / Higher packets per second (pps):** Removing hello virtual switch from hello datapath removes hello time packets spend in hello host for policy processing and increases hello number of packets that can be processed inside hello VM.</span></span>
* <span data-ttu-id="37b15-124">**지터 감소:** 가상 스위치 처리 toobe 적용 해야 하는 정책의 hello 양과 hello 처리를 수행 하는 hello CPU의 hello 작업량에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-124">**Reduced jitter:** Virtual switch processing depends on hello amount of policy that needs toobe applied and hello workload of hello CPU that is doing hello processing.</span></span> <span data-ttu-id="37b15-125">Hello 정책 적용 toohello 하드웨어 오프 로드 toohello VM을 제거 하는 hello tooVM 통신을 호스트 하 고 모든 소프트웨어 인터럽트 및 컨텍스트 전환 직접 패킷을 전달 하 여 해당 가변성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-125">Offloading hello policy enforcement toohello hardware removes that variability by delivering packets directly toohello VM, removing hello host tooVM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="37b15-126">**CPU 사용률 감소:** 무시 hello hello 호스트에서 가상 스위치에 네트워크 트래픽 처리에 대 한 CPU 사용률 tooless 잠재 고객 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-126">**Decreased CPU utilization:** Bypassing hello virtual switch in hello host leads tooless CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="37b15-127"><a name="Limitations"></a>제한 사항</span><span class="sxs-lookup"><span data-stu-id="37b15-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="37b15-128">다음과 같은 제한을 hello이이 기능을 사용 하는 경우 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-128">hello following limitations exist when using this capability:</span></span>

* <span data-ttu-id="37b15-129">**네트워크 인터페이스 만들기:** 가속화된 네트워킹은 새 NIC에서만 사용할 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="37b15-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="37b15-130">기존 NIC에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="37b15-131">**VM 만들기:** A 인 NIC와 가속된 네트워킹 사용 수만 때 hello 첨부 tooa VM 수 VM이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-131">**VM creation:** A NIC with accelerated networking enabled can only be attached tooa VM when hello VM is created.</span></span> <span data-ttu-id="37b15-132">hello NIC VM을 기존 연결 된 tooan 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-132">hello NIC cannot be attached tooan existing VM.</span></span>
* <span data-ttu-id="37b15-133">**지역:** 가속화된 네트워킹 기능을 갖춘 Windows VM은 대부분의 Azure 지역에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="37b15-134">가속화된 네트워킹 기능을 갖춘 Linux VM은 여러 지역에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="37b15-135">hello 지역에서 사용할 수 있는이 기능을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-135">hello regions this capability is available in is expanding.</span></span> <span data-ttu-id="37b15-136">Hello 최신 정보에 대 한 아래 hello Azure 가상 네트워킹 업데이트가 블로그를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="37b15-136">Please see hello Azure Virtual Networking Updates blog below for hello latest information.</span></span>   
* <span data-ttu-id="37b15-137">**지원되는 운영 체제:** Windows: Microsoft Windows Server 2012 R2 Datacenter 및 Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="37b15-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="37b15-138">Linux: Ubuntu Server 16.04 LTS(커널 4.4.0-77 이상), SLES 12 SP2, RHEL 7.3 및 CentOS 7.3(“Rogue Wave Software”에 의해 게시됨).</span><span class="sxs-lookup"><span data-stu-id="37b15-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="37b15-139">**VM 크기:** 8개 이상의 코어가 있는 범용 및 계산 용도로 최적화된 인스턴스 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="37b15-140">자세한 내용은 참조 hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 및 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM의 문서 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-140">For more information, see hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="37b15-141">hello 지원 되는 VM 인스턴스 크기 집합 확장 hello 앞에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-141">hello set of supported VM instance sizes will expand in hello future.</span></span>
* <span data-ttu-id="37b15-142">**ARM(Azure Resource Manager)을 통한 배포:** 가속화된 네트워킹은 ASM/RDFE를 통해 배포할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="37b15-143">Hello를 통해 변경 내용을 toothese 제한 사항에 발표 됩니다 [업데이트 Azure 가상 네트워킹이](https://azure.microsoft.com/updates/accelerated-networking-in-preview) 페이지.</span><span class="sxs-lookup"><span data-stu-id="37b15-143">Changes toothese limitations are announced through hello [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="37b15-144">Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="37b15-144">Create a Windows VM</span></span>
<span data-ttu-id="37b15-145">Hello Azure 포털 또는 Azure를 사용할 수 있습니다 [PowerShell](#windows-powershell) toocreate hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-145">You can use hello Azure portal or Azure [PowerShell](#windows-powershell) toocreate hello VM.</span></span>

### <span data-ttu-id="37b15-146"><a name="windows-portal"></a>포털</span><span class="sxs-lookup"><span data-stu-id="37b15-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="37b15-147">인터넷 브라우저를 열고 Azure hello [포털](https://portal.azure.com) 및 Azure 사용 하 여 로그인 [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-147">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="37b15-148">아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="37b15-149">Hello 포털에서 클릭 **+ 새로 만들기** > **계산** > **Windows Server 2016 Datacenter**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-149">In hello portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="37b15-150">Hello에 **Windows Server 2016 Datacenter** leave 나타나는 블레이드 *리소스 관리자* 아래에서 선택한 **배포 모델을 선택**를 클릭 하 고 **만들기** .</span><span class="sxs-lookup"><span data-stu-id="37b15-150">In hello **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="37b15-151">Hello에 **기본 사항** 나타나는 블레이드 hello 다음 값을 입력 hello 남아 있는 기본 옵션 또는 선택 하거나 사용자 고유의 값을 입력을 클릭 hello **확인** 단추:</span><span class="sxs-lookup"><span data-stu-id="37b15-151">In hello **Basics** blade that appears, enter hello following values, leave hello remaining default options or select or enter your own values, and click hello **OK** button:</span></span>

    |<span data-ttu-id="37b15-152">설정</span><span class="sxs-lookup"><span data-stu-id="37b15-152">Setting</span></span>|<span data-ttu-id="37b15-153">값</span><span class="sxs-lookup"><span data-stu-id="37b15-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="37b15-154">이름</span><span class="sxs-lookup"><span data-stu-id="37b15-154">Name</span></span>|<span data-ttu-id="37b15-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="37b15-155">MyVm</span></span>|
    |<span data-ttu-id="37b15-156">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="37b15-156">Resource group</span></span>|<span data-ttu-id="37b15-157">**새로 만들기**를 선택한 채로 두고 *MyResourceGroup*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="37b15-158">위치</span><span class="sxs-lookup"><span data-stu-id="37b15-158">Location</span></span>|<span data-ttu-id="37b15-159">미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="37b15-159">West US 2</span></span>|

    <span data-ttu-id="37b15-160">새 tooAzure 인 경우에 대해 자세히 알아보세요 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), 및 [위치](https://azure.microsoft.com/regions) (또한 않는 tooas 영역 함).</span><span class="sxs-lookup"><span data-stu-id="37b15-160">If you're new tooAzure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred tooas regions).</span></span>
5. <span data-ttu-id="37b15-161">Hello에 **크기를 선택** 나타나는 블레이드 입력 *8* hello에 **최소 코어** 클릭 한 다음 상자 **모든 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-161">In hello **Choose a size** blade that appears, enter *8* in hello **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="37b15-162">클릭 **DS4_V2 표준**, 또는 지원 되는 모든 VM, 클릭 hello **선택** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-162">Click **DS4_V2 Standard**, or any supported VM, then click hello **Select** button.</span></span>
7. <span data-ttu-id="37b15-163">Hello에 **설정** 나타나는 블레이드 유지 된 모든 설정-클릭 제외 하 고는 **Enabled** 아래 **네트워킹 Accelerated**, hello 클릭 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-163">In hello **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click hello **OK** button.</span></span> <span data-ttu-id="37b15-164">**참고:** , 이전 단계에서 선택 하는 경우 VM 크기, 운영 체제 또는 위치에 대 한 hello에는 없지만 값 [제한](#Limitations) 이 문서의 섹션 **가속 네트워킹**표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in hello [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="37b15-165">Hello에 **요약** 블레이드를 놓고 클릭 hello **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-165">In hello **Summary** blade that appears, click hello **OK** button.</span></span> <span data-ttu-id="37b15-166">Azure는 hello VM 만들기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-166">Azure starts creating hello VM.</span></span> <span data-ttu-id="37b15-167">VM을 만드는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="37b15-168">Windows 네트워킹 드라이버 가속 tooinstall hello, hello에서 단계를 완료 하는 hello [Windows 구성](#configure-windows) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="37b15-168">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="37b15-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="37b15-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="37b15-170">Hello 최신 버전의 hello Azure PowerShell 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-170">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="37b15-171">새 tooAzure PowerShell 인 경우 hello 읽을 [Azure PowerShell 개요](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서.</span><span class="sxs-lookup"><span data-stu-id="37b15-171">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="37b15-172">Hello Windows 시작 단추를 클릭 하 여 PowerShell 세션을 시작 합니다. 입력 **powershell**를 클릭 한 다음 **PowerShell** hello 검색 결과에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-172">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="37b15-173">PowerShell 창에 입력 hello `login-azurermaccount` Azure 사용 하 여 명령 toosign [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-173">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="37b15-174">아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="37b15-175">브라우저에서 다음 스크립트는 hello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-175">In your browser, copy hello following script:</span></span>
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="37b15-176">PowerShell 창에 toopaste hello 스크립트를 마우스 오른쪽 단추로 클릭 하 고 실행 되기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-176">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="37b15-177">사용자 이름과 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-177">You are prompted for a username and password.</span></span> <span data-ttu-id="37b15-178">Tooit hello 다음 단계에 연결할 때 이러한 자격 증명 toolog toohello VM에서에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-178">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="37b15-179">Hello 스크립트 실패 실행 되기 전에 hello 스크립트의 값을 변경 하는 경우 VM 크기, 운영 체제에 사용 된 hello 값을 확인 하 고 hello 위치 같습니다 [제한](#Limitations) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="37b15-179">If hello script fails, and you changed values in hello script before executing it, confirm hello values you used for VM size, operating system, and location are listed in hello [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="37b15-180">Windows 네트워킹 드라이버 가속 tooinstall hello, hello에서 단계를 완료 하는 hello [Windows 구성](#configure-windows) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="37b15-180">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="37b15-181"><a name="configure-windows"></a>Windows 구성</span><span class="sxs-lookup"><span data-stu-id="37b15-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="37b15-182">Azure의 hello VM을 만든 후에 Windows 용 hello 가속된 네트워킹 드라이버를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-182">Once you create hello VM in Azure, you must install hello accelerated networking driver for Windows.</span></span> <span data-ttu-id="37b15-183">Hello 다음 단계를 완료 하기 전에 만들었어야 Windows VM 중 하나가 hello를 사용 하 여 가속 네트워킹 [포털](#windows-portal) 또는 [PowerShell](#windows-powershell) 이 문서의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-183">Before completing hello following steps, you must have created a Windows VM with accelerated networking using either hello [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="37b15-184">인터넷 브라우저를 열고 Azure hello [포털](https://portal.azure.com) 및 Azure 사용 하 여 로그인 [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-184">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="37b15-185">아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="37b15-186">Hello 텍스트를 포함 하는 hello 상자에서 *리소스 검색* hello Azure 포털의 hello 위쪽 입력 *MyVm*합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-186">In hello box that contains hello text *Search resources* at hello top of hello Azure portal, type *MyVm*.</span></span> <span data-ttu-id="37b15-187">때 **MyVm** 나타납니다 hello 검색 결과에를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-187">When **MyVm** appears in hello search results, click it.</span></span>
3. <span data-ttu-id="37b15-188">Hello에 **MyVm** 블레이드를 놓고 클릭 hello **연결** hello 왼쪽된 위 모서리의 hello 블레이드의 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-188">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="37b15-189">**참고:** 경우 **만들기** hello 아래에 표시 되 **연결** 단추, Azure가 아직 완료 되지 hello VM 만들기.</span><span class="sxs-lookup"><span data-stu-id="37b15-189">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="37b15-190">클릭 **연결** 더 이상 참조 한 후에 **만들기** hello에서 **연결** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-190">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
4. <span data-ttu-id="37b15-191">브라우저 toodownload hello 허용 **MyVm.rdp** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-191">Allow your browser toodownload hello **MyVm.rdp** file.</span></span>  <span data-ttu-id="37b15-192">를 다운로드 한 후 클릭 hello 파일 tooopen 것입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-192">Once downloaded, click hello file tooopen it.</span></span> 
5. <span data-ttu-id="37b15-193">Hello 클릭 **연결** hello 단추 **원격 데스크톱 연결** 상자가 표시 되 면 사용자에 게 알리는 hello 해당의 hello 원격 연결 게시자를 식별할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-193">Click hello **Connect** button in hello **Remote Desktop Connection** box that appears, notifying you that hello publisher of hello remote connection can't be identified.</span></span>
6. <span data-ttu-id="37b15-194">Hello에 **Windows 보안** 상자가 표시 되 면 클릭 **추가 선택 사항을**, 클릭 **다른 계정을 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-194">In hello **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="37b15-195">Hello 사용자 이름 및 4 단계에서 입력 한 암호를 입력 한 다음 hello 클릭 **확인** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-195">Enter hello username and password you entered in step 4, then click hello **OK** button.</span></span>
7. <span data-ttu-id="37b15-196">Hello 클릭 **예** 단추 hello 원격 데스크톱 연결 나타나는 상자에서 사용자에 게 알리는 hello 원격 컴퓨터의 hello id를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-196">Click hello **Yes** button in hello Remote Desktop Connection box that appears, notifying you that hello identity of hello remote computer cannot be verified.</span></span>
8. <span data-ttu-id="37b15-197">Hello Windows 시작 단추를 마우스 오른쪽 단추로 클릭 하 고 클릭 **장치 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-197">Right-click hello Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="37b15-198">Hello 확장 **네트워크 어댑터가** 노드.</span><span class="sxs-lookup"><span data-stu-id="37b15-198">Expand hello **Network adapters** node.</span></span> <span data-ttu-id="37b15-199">해당 hello 확인 **함수 가상 이더넷 어댑터 Mellanox ConnectX 3** hello 다음 그림에에서 나와 있는 것 처럼 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-199">Confirm that hello **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in hello following picture:</span></span>
   
    ![장치 관리자](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="37b15-201">이제 가속화된 네트워킹을 VM에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="37b15-202">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="37b15-202">Create a Linux VM</span></span>
<span data-ttu-id="37b15-203">Hello Azure 포털 또는 Azure를 사용할 수 있습니다 [PowerShell](#linux-powershell) toocreate Ubuntu 또는 SLES VM입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-203">You can use hello Azure portal or Azure [PowerShell](#linux-powershell) toocreate an Ubuntu or SLES VM.</span></span> <span data-ttu-id="37b15-204">RHEL 및 CentOS VM의 경우 다른 워크플로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="37b15-205">아래의 hello 지침을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="37b15-205">Please see hello instructions below.</span></span>

### <span data-ttu-id="37b15-206"><a name="linux-portal"></a>포털</span><span class="sxs-lookup"><span data-stu-id="37b15-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="37b15-207">Hello의 1-5 단계를 완료 하 여 Linux 미리 보기에 대 한 네트워킹 accelerated hello에 대 한 레지스터 [PowerShell Linux VM-생성](#linux-powershell) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="37b15-207">Register for hello accelerated networking for Linux preview by completing steps 1-5 of hello [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="37b15-208">Hello 포털에서 hello 미리 보기에 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-208">You cannot register for hello preview in hello portal.</span></span>
2. <span data-ttu-id="37b15-209">에 hello 1-8 단계를 완료 [Windows VM-만듭니다 포털](#windows-portal) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="37b15-209">Complete steps 1-8 in hello [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="37b15-210">2단계에서 **Windows Server 2016 Datacenter** 대신 **Ubuntu Server 16.04 LTS**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="37b15-211">이 자습서에 대 한 선택 toouse SSH 키 대신 암호를 있지만 프로덕션 배포에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-211">For this tutorial, choose toouse a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="37b15-212">경우 **네트워킹 Accelerated** hello의 7 단계를 완료 하면 나타나지 않으면 [Windows VM-생성 포털](#windows-portal) 섹션이 문서의 될 hello 다음 이유 중 하나에 대해:</span><span class="sxs-lookup"><span data-stu-id="37b15-212">If **Accelerated networking** does not appear when you complete step 7 of hello [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of hello following reasons:</span></span>
    - <span data-ttu-id="37b15-213">사용자 등록 되지 않은 아직 hello 미리 보기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-213">You are not yet registered for hello preview.</span></span> <span data-ttu-id="37b15-214">등록 상태 인지 확인 **등록 된**hello의 4 단계에서 설명한 것 처럼, [Powershell Linux VM-생성](#linux-powershell) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="37b15-214">Confirm that your registration state is **Registered**, as explained in step 4 of hello [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="37b15-215">**참고:** 가속 hello에 참여 하는 경우 (해당 없음 긴 필요한 tooregister toouse Accelerated Windows Vm에 적합 한 네트워킹)를 Windows Vm 미리 보기에 대 한 네트워킹 하지 자동으로 등록 가속 hello에 대 한 네트워킹 Linux Vm의 경우 미리 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-215">**Note:** If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="37b15-216">Linux Vm에 tooparticipate 미리 보기에 대 한 hello 가속 네트워킹에 대 한 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-216">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
    - <span data-ttu-id="37b15-217">VM 크기, 운영 체제 또는 hello에 나열 된 위치를 선택 하지 않은 [제한](#limitations) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="37b15-217">You have not selected a VM size, operating system, or location listed in hello [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="37b15-218">tooinstall hello Linux에 대 한 네트워킹 드라이버 accelerated, hello에서 단계를 완료 하는 hello [구성 Linux](#configure-linux) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="37b15-218">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="37b15-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="37b15-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="37b15-220">가속 네트워킹 구독에서 Linux Vm을 만들고 다음 toocreate 가속화 된 네트워킹의 hello 사용 하 여 Windows VM을 시도 하는 경우 동일한 구독 hello Windows VM을 만들 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt toocreate a Windows VM with accelerated networking in hello same subscription, hello Windows VM creation may fail.</span></span> <span data-ttu-id="37b15-221">이 미리 보기에서는 가속화된 네트워킹을 사용하는 Linux VM과 Windows VM을 별도의 구독에서 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="37b15-222">Hello 최신 버전의 hello Azure PowerShell 설치 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-222">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="37b15-223">새 tooAzure PowerShell 인 경우 hello 읽을 [Azure PowerShell 개요](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서.</span><span class="sxs-lookup"><span data-stu-id="37b15-223">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="37b15-224">Hello Windows 시작 단추를 클릭 하 여 PowerShell 세션을 시작 합니다. 입력 **powershell**를 클릭 한 다음 **PowerShell** hello 검색 결과에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-224">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="37b15-225">PowerShell 창에 입력 hello `login-azurermaccount` Azure 사용 하 여 명령 toosign [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-225">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="37b15-226">아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="37b15-227">Azure에 대 한 네트워킹 accelerated hello에 대 한 레지스터 hello 다음 단계를 완료 하 여 미리 보기:</span><span class="sxs-lookup"><span data-stu-id="37b15-227">Register for hello accelerated networking for Azure preview by completing hello following steps:</span></span>
    - <span data-ttu-id="37b15-228">너무 전자 메일을 보내[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) 는 Azure 구독 ID로, 의도 된 용도입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-228">Send an email too[axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="37b15-229">Microsoft에서 보내는 구독 활성화에 대한 메일 확인을 기다려 주세요.</span><span class="sxs-lookup"><span data-stu-id="37b15-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="37b15-230">Hello 명령 tooconfirm hello 미리 보기에 등록 된 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-230">Enter hello following command tooconfirm you are registered for hello preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="37b15-231">5 단계까지 진행 하지 마십시오 **등록 된** hello hello 이전 명령을 입력 한 후 출력에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-231">Do not continue with step 5 until **Registered** appears in hello output after you enter hello previous command.</span></span> <span data-ttu-id="37b15-232">출력은 hello 다음 계속 하기 전에 출력 같이 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-232">Your output must look like hello following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="37b15-233">가속 hello에 참여 하는 경우 (해당 없음 긴 필요한 tooregister toouse Accelerated Windows Vm에 적합 한 네트워킹)를 Windows Vm 미리 보기에 대 한 네트워킹 하면 등록 되지 않은 자동으로 가속 hello에 대 한 Linux Vm의 경우 미리 보기에 대 한 네트워킹 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-233">If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="37b15-234">Linux Vm에 tooparticipate 미리 보기에 대 한 hello 가속 네트워킹에 대 한 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-234">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
      >
5. <span data-ttu-id="37b15-235">브라우저에서 hello 다음 원하는 대로 Ubuntu 또는 SLES 대체 하 여 스크립트를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-235">In your browser, copy hello following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="37b15-236">또한 Redhat 및 CentOS에는 아래에서 간략하게 설명되는 다른 워크플로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="37b15-237">PowerShell 창에 toopaste hello 스크립트를 마우스 오른쪽 단추로 클릭 하 고 실행 되기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-237">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="37b15-238">사용자 이름과 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-238">You are prompted for a username and password.</span></span> <span data-ttu-id="37b15-239">Tooit hello 다음 단계에 연결할 때 이러한 자격 증명 toolog toohello VM에서에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-239">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="37b15-240">Hello 스크립트에 실패 하면 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-240">If hello script fails, confirm that:</span></span>
    - <span data-ttu-id="37b15-241">4 단계에서 설명한 것 처럼 hello 미리 보기에 등록 된</span><span class="sxs-lookup"><span data-stu-id="37b15-241">You are registered for hello preview, as explained in step 4</span></span>
    - <span data-ttu-id="37b15-242">VM 크기, 운영 체제 유형 또는 위치 값 hello 스크립트에서 실행 되기 전에 변경 하는 경우, hello 값 hello에 나열 됩니다 [제한](#Limitations) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="37b15-242">If you changed VM size, operating system type, or location values in hello script before executing it, that hello values are listed in hello [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="37b15-243">tooinstall hello Linux에 대 한 네트워킹 드라이버 accelerated, hello에서 단계를 완료 하는 hello [구성 Linux](#configure-linux) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="37b15-243">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="37b15-244"><a name="configure-linux"></a>Linux 구성</span><span class="sxs-lookup"><span data-stu-id="37b15-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="37b15-245">Azure의 hello VM을 만든 후에 Linux 용 hello 가속된 네트워킹 드라이버를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-245">Once you create hello VM in Azure, you must install hello accelerated networking driver for Linux.</span></span> <span data-ttu-id="37b15-246">Hello 다음 단계를 완료 하기 전에 만들었어야 Linux VM 중 하나가 hello를 사용 하 여 가속 네트워킹 [포털](#linux-portal) 또는 [PowerShell](#linux-powershell) 이 문서의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-246">Before completing hello following steps, you must have created a Linux VM with accelerated networking using either hello [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="37b15-247">인터넷 브라우저를 열고 Azure hello [포털](https://portal.azure.com) 및 Azure 사용 하 여 로그인 [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-247">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="37b15-248">아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="37b15-249">Hello hello 포털 toohello 오른쪽의 hello 위쪽 *리소스 검색* 막대에서 클릭 hello **> _** 아이콘 toostart Bash 클라우드 셸 (미리 보기).</span><span class="sxs-lookup"><span data-stu-id="37b15-249">At hello top of hello portal, toohello right of hello *Search resources* bar, click hello **>_** icon toostart a Bash cloud shell (Preview).</span></span> <span data-ttu-id="37b15-250">hello Bash 클라우드 셸 창이 표시 하 고 몇 초 후 hello 포털의 hello 맨 아래에 표시 된  **username@Azure:~ $** 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-250">hello Bash cloud shell pane appears at hello bottom of hello portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="37b15-251">Hello 클라우드 셸 대신 컴퓨터에서 SSH toohello VM 수 있지만이 자습서에서는 hello 지침 hello 클라우드 셸을 사용 하는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-251">Though you can SSH toohello VM from your computer, rather than hello cloud shell, hello instructions in this tutorial assume you're using hello cloud shell.</span></span>
3. <span data-ttu-id="37b15-252">Hello 포털의 hello 위쪽 hello 상자에 텍스트가 포함 된 hello *리소스 검색*, 형식 *MyVm*합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-252">At hello top of hello portal, in hello box that contains hello text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="37b15-253">때 **MyVm** 나타납니다 hello 검색 결과에를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-253">When **MyVm** appears in hello search results, click it.</span></span>
4. <span data-ttu-id="37b15-254">Hello에 **MyVm** 블레이드를 놓고 클릭 hello **연결** hello 왼쪽된 위 모서리의 hello 블레이드의 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-254">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="37b15-255">**참고:** 경우 **만들기** hello 아래에 표시 되 **연결** 단추, Azure가 아직 완료 되지 hello VM 만들기.</span><span class="sxs-lookup"><span data-stu-id="37b15-255">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="37b15-256">클릭 **연결** 더 이상 참조 한 후에 **만들기** hello에서 **연결** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-256">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
5. <span data-ttu-id="37b15-257">Azure tooenter hello 알려 상자를 엽니다. `ssh adminuser@<ipaddress>`합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-257">Azure opens a box telling you tooenter hello `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="37b15-258">이 명령은 hello 클라우드 셸 (또는 복사에 4 단계에서 표시 된 hello 상자 고 toohello 클라우드 셸에서 붙여), Enter에는 다음 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-258">Enter this command in hello cloud shell (or copy it from hello box that appeared in step 4 and paste it in toohello cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="37b15-259">Enter **예** toocontinue 연결 하려는 경우 다음 Enter 키를 누르면 요청 toohello 질문 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-259">Enter **yes** toohello question asking you if you want toocontinue connecting, then press Enter.</span></span>
7. <span data-ttu-id="37b15-260">Hello VM을 만들 때 입력 한 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-260">Enter hello password you entered when creating hello VM.</span></span> <span data-ttu-id="37b15-261">Toohello VM에에서 로그온 했습니다. 한 번 표시는 adminuser@MyVm:~ $ 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-261">Once successfully logged in toohello VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="37b15-262">Hello 클라우드 셸 세션을 통해 VM toohello 이제 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-262">You are now logged in toohello VM through hello cloud shell session.</span></span> <span data-ttu-id="37b15-263">**참고:** 클라우드 셸 세션을 10분 동안 사용하지 않으면 시간이 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="37b15-264">이 시점에서 hello 명령을 사용 하는 hello 배포에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-264">At this point, hello instructions vary based on hello distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="37b15-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="37b15-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="37b15-266">Hello 프롬프트에서 입력 `uname -r` hello 버전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-266">At hello prompt, enter `uname -r` and confirm hello version for:</span></span>

    * <span data-ttu-id="37b15-267">Ubuntu는 "4.4.0-77-generic" 이상임</span><span class="sxs-lookup"><span data-stu-id="37b15-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="37b15-268">SLES는 "4.4.59-92.20-default" 이상임</span><span class="sxs-lookup"><span data-stu-id="37b15-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="37b15-269">다음에 나오는 실행 중인 hello 명령을 사용 하 여 hello 표준 네트워킹 vNIC 사이의 accelerated hello 네트워킹 vNIC 채권을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-269">Create a bond between hello standard networking vNIC and hello accelerated networking vNIC by running hello commands that follow.</span></span> <span data-ttu-id="37b15-270">네트워크 트래픽은 hello 채권 특정 구성 변경 내용은 간에 네트워킹 트래픽은 중단 되지 않도록 보장 하는 동안에 가속화 된 네트워킹 vNIC를 성능이 높은 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-270">Network traffic uses hello higher performing accelerated networking vNIC, while hello bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="37b15-271">Hello 스크립트를 실행 한 후 VM hello 60 초 일시 중지 한 후 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-271">After running hello script, hello VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="37b15-272">한 번 VM이 다시 시작 하는 hello tooit 다시 5-7 단계를 완료 하 여 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-272">Once hello VM is restarted, reconnect tooit by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="37b15-273">Hello 실행 `ifconfig` 명령 및 bond0가 들어온 고 hello 인터페이스 위쪽으로 표시 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-273">Run hello `ifconfig` command and confirm that bond0 has come up and hello interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="37b15-274">가속된 네트워킹을 사용 하 여 응용 프로그램 hello를 통해 통신 해야 *bond0* 되지 않은 인터페이스 *eth0*합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-274">Applications using accelerated networking must communicate over hello *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="37b15-275">가속된 네트워킹 일반 공급 전에 hello 인터페이스 이름이 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-275">hello interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="37b15-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="37b15-276">RHEL/CentOS</span></span>

<span data-ttu-id="37b15-277">Red Hat Enterprise Linux 또는 CentOS 7.3 VM 만드는 몇 가지 추가 단계를 hello VF (가상 함수) hello 네트워크 카드 드라이버 및 SR-IOV에 필요한 tooload hello 최신 드라이버 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps tooload hello latest drivers needed for SR-IOV and hello Virtual Function (VF) driver for hello network card.</span></span> <span data-ttu-id="37b15-278">hello hello 지침의 첫 번째 단계는 이미지 준비 toomake 사용된 될 수 있는 hello 드라이버가 미리 로드 되어 하나 이상의 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="37b15-278">hello first phase of hello instructions prepares an image that can be used toomake one or more virtual machines that have hello drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="37b15-279">1단계: Red Hat Enterprise Linux 또는 CentOS 7.3 기본 이미지를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="37b15-280">Azure에서 비SRIOV CentOS 7.3 VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="37b15-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="37b15-281">LIS 4.2.2를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="37b15-282">구성 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="37b15-283">이 VM의 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="37b15-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="37b15-284">Azure 포털에서이 VM; 중지 및 "디스크" tooVM의, hello os 디스크 VHD URI를 캡처하십시오.</span><span class="sxs-lookup"><span data-stu-id="37b15-284">From Azure portal, stop this VM; and go tooVM’s "Disks", capture hello OSDisk’s VHD URI.</span></span> <span data-ttu-id="37b15-285">이 URI는 hello 기본 이미지의 VHD 이름 및 해당 저장소 계정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-285">This URI contains hello base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="37b15-286">2단계: Azure에서 새 VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="37b15-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="37b15-287">새 Vm 기반 새로 AzureRMVMConfig을 프로 비전 기본 이미지 AcceleratedNetworking hello vNIC에서 사용 하도록 설정 된, 1 단계에서 캡처된 VHD hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="37b15-287">Provision new VMs based with New-AzureRMVMConfig using hello base image VHD captured in phase one, with AcceleratedNetworking enabled on hello vNIC:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="37b15-288">Vm 부팅 한 후 "lspci" 하 여 hello VF 장치를 확인 하 고 hello Mellanox 항목을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-288">After VMs boot up, check hello VF device by "lspci" and check hello Mellanox entry.</span></span> <span data-ttu-id="37b15-289">예를 들어 hello lspci 출력에서이 항목의 확인할:</span><span class="sxs-lookup"><span data-stu-id="37b15-289">For example, we should see this item in hello lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="37b15-290">Hello 결합 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-290">Run hello bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="37b15-291">다시 부팅 새 Vm hello:</span><span class="sxs-lookup"><span data-stu-id="37b15-291">Reboot hello new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="37b15-292">hello VM bond0 구성 및 사용 하도록 설정 하는 네트워킹 Accelerated 경로 hello로 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-292">hello VM should start with bond0 configured and hello Accelerated Networking path enabled.</span></span>  <span data-ttu-id="37b15-293">실행 `ifconfig` tooconfirm 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b15-293">Run `ifconfig` tooconfirm.</span></span>
