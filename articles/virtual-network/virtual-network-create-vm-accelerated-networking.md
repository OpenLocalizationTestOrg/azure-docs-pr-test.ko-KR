---
title: "가속화된 네트워킹을 사용하는 Azure 가상 컴퓨터 만들기 | Microsoft Docs"
description: "가속화된 네트워킹을 사용하는 가상 컴퓨터를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 449425189a3b42dcb2c31316c1c8e38fac69d761
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="57999-103">가속화된 네트워킹을 사용하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="57999-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="57999-104">이 자습서에서는 가속화된 네트워킹을 사용하는 Azure VM(가상 컴퓨터)을 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="57999-104">In this tutorial, you learn how to create an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="57999-105">가속화된 네트워킹은 Windows용 GA이고 특정 Linux 배포를 위한 공개 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="57999-106">가속화된 네트워킹을 사용하면 VM에 대한 단일 루트 I/O 가상화(SR-IOV)를 구현할 수 있어 네트워킹 성능이 크게 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-106">Accelerated networking enables single root I/O virtualization (SR-IOV) to a VM, greatly improving its networking performance.</span></span> <span data-ttu-id="57999-107">이 고성능 경로는 데이터 경로에서 호스트를 우회함으로써 대기 시간, 지터 및 CPU 사용률을 줄이므로 지원되는 VM 유형에서 가장 까다로운 네트워크 워크로드에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-107">This high-performance path bypasses the host from the datapath reducing latency, jitter, and CPU utilization, for use with the most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="57999-108">다음 그림에서는 가속화된 네트워킹을 사용하거나 사용하지 않는 경우의 두 VM(가상 컴퓨터) 간 통신을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57999-108">The following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![비교](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="57999-110">가속화된 네트워킹을 사용하지 않는 경우 VM에서 들어오고 나가는 모든 네트워킹 트래픽이 호스트와 가상 스위치를 통과해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-110">Without accelerated networking, all networking traffic in and out of the VM must traverse the host and the virtual switch.</span></span> <span data-ttu-id="57999-111">가상 스위치는 네트워크 보안 그룹, 액세스 제어 목록, 격리 및 네트워크 트래픽에 대한 다른 네트워크 가상화 서비스 등, 모든 정책 적용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-111">The virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services to network traffic.</span></span> <span data-ttu-id="57999-112">가상 스위치에 대한 자세한 내용은 [Hyper-V 네트워크 가상화 및 가상 스위치](https://technet.microsoft.com/library/jj945275.aspx) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57999-112">To learn more about virtual switches, read the [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="57999-113">가속화된 네트워킹을 사용하는 경우 네트워크 트래픽이 VM의 NIC(네트워크 인터페이스)에 도착한 다음 VM으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-113">With accelerated networking, network traffic arrives at the VM's network interface (NIC), and is then forwarded to the VM.</span></span> <span data-ttu-id="57999-114">가상 스위치가 가속화된 네트워킹 없이 적용되는 모든 네트워크 정책은 오프로드되어 하드웨어에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-114">All network policies that the virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="57999-115">하드웨어에서 정책을 적용하면 NIC는 호스트에 적용된 모든 정책을 유지하면서 VM에 직접 네트워크 트래픽을 전달할 수 있으므로 호스트 및 가상 스위치를 우회할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-115">Applying policy in hardware enables the NIC to forward network traffic directly to the VM, bypassing the host and the virtual switch, while maintaining all the policy it applied in the host.</span></span>

<span data-ttu-id="57999-116">가속화된 네트워킹의 이점은 사용하도록 설정된 VM에만 적용된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="57999-116">The benefits of accelerated networking only apply to the VM that it is enabled on.</span></span> <span data-ttu-id="57999-117">최상의 결과를 얻으려면 동일한 Azure VNet(가상 네트워크)에 연결된 둘 이상의 VM에서 이 기능을 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-117">For the best results, it is ideal to enable this feature on at least two VMs connected to the same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="57999-118">VNet에서 통신하거나 온-프레미스에 연결할 때 이 기능을 사용하면 전체 대기 시간에 미치는 영향을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-118">When communicating across VNets or connecting on-premises, this feature has minimal impact to overall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="57999-119">이 Linux Public Preview는 현재 미리 보기로 있으며 일반 공급 릴리스에 있는 기능과 동일한 수준의 가용성 및 안정성을 제공하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-119">This Linux Public Preview may not have the same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="57999-120">이 기능은 지원되지 않으며, 기능이 제한될 수 있으며 모든 Azure 위치에서 사용하지는 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-120">The feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="57999-121">이 기능의 가용성 및 상태에 대한 최신 알림을 보려면 Azure Virtual Network 업데이트 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57999-121">For the most up-to-date notifications on availability and status of this feature, check the Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="57999-122">이점</span><span class="sxs-lookup"><span data-stu-id="57999-122">Benefits</span></span>
* <span data-ttu-id="57999-123">**더 낮은 대기 시간/더 높은 초당 패킷 수(pps):** 데이터 경로에서 가상 스위치를 제거하면 패킷이 정채 처리를 위해 호스트에서 소요하는 시간이 제거되고 VM 내에서 처리될 수 있는 패킷 수가 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="57999-123">**Lower Latency / Higher packets per second (pps):** Removing the virtual switch from the datapath removes the time packets spend in the host for policy processing and increases the number of packets that can be processed inside the VM.</span></span>
* <span data-ttu-id="57999-124">**감소된 지터:** 가상 스위치 처리는 적용해야 하는 정책의 양과 처리를 수행하는 CPU의 워크로드에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="57999-124">**Reduced jitter:** Virtual switch processing depends on the amount of policy that needs to be applied and the workload of the CPU that is doing the processing.</span></span> <span data-ttu-id="57999-125">정책 적용을 하드웨어로 오프로드하면 패킷이 VM으로 직접 전달되고, 호스트-VM 통신과 모든 소프트웨어 인터럽트 및 컨텍스트 전환이 제거되어 이러한 가변성이 해소됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-125">Offloading the policy enforcement to the hardware removes that variability by delivering packets directly to the VM, removing the host to VM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="57999-126">**CPU 사용률 감소:** 호스트의 가상 스위치를 무시하면 네트워크 트래픽 처리에 사용되는 CPU가 감소됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-126">**Decreased CPU utilization:** Bypassing the virtual switch in the host leads to less CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="57999-127"><a name="Limitations"></a>제한 사항</span><span class="sxs-lookup"><span data-stu-id="57999-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="57999-128">이 기능을 사용하는 경우 다음과 같은 제한이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-128">The following limitations exist when using this capability:</span></span>

* <span data-ttu-id="57999-129">**네트워크 인터페이스 만들기:** 가속화된 네트워킹은 새 NIC에서만 사용할 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="57999-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="57999-130">기존 NIC에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="57999-131">**VM 만들기:** VM을 만들 때 가속화된 네트워킹을 사용하도록 설정된 NIC만 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-131">**VM creation:** A NIC with accelerated networking enabled can only be attached to a VM when the VM is created.</span></span> <span data-ttu-id="57999-132">기존 VM에는 이 NIC를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-132">The NIC cannot be attached to an existing VM.</span></span>
* <span data-ttu-id="57999-133">**지역:** 가속화된 네트워킹 기능을 갖춘 Windows VM은 대부분의 Azure 지역에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="57999-134">가속화된 네트워킹 기능을 갖춘 Linux VM은 여러 지역에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="57999-135">이 기능을 사용할 수 있는 지역은 확장되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-135">The regions this capability is available in is expanding.</span></span> <span data-ttu-id="57999-136">최신 정보는 Azure 가상 네트워킹 업데이트 블로그를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57999-136">Please see the Azure Virtual Networking Updates blog below for the latest information.</span></span>   
* <span data-ttu-id="57999-137">**지원되는 운영 체제:** Windows: Microsoft Windows Server 2012 R2 Datacenter 및 Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="57999-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="57999-138">Linux: Ubuntu Server 16.04 LTS(커널 4.4.0-77 이상), SLES 12 SP2, RHEL 7.3 및 CentOS 7.3(“Rogue Wave Software”에 의해 게시됨).</span><span class="sxs-lookup"><span data-stu-id="57999-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="57999-139">**VM 크기:** 8개 이상의 코어가 있는 범용 및 계산 용도로 최적화된 인스턴스 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="57999-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="57999-140">자세한 내용은 [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 및 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM 크기 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57999-140">For more information, see the [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="57999-141">지원되는 VM 인스턴스 확장 집합은 앞으로 확장될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="57999-141">The set of supported VM instance sizes will expand in the future.</span></span>
* <span data-ttu-id="57999-142">**ARM(Azure Resource Manager)을 통한 배포:** 가속화된 네트워킹은 ASM/RDFE를 통해 배포할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="57999-143">이러한 제한 사항이 변경되면 [Azure 가상 네트워킹 업데이트](https://azure.microsoft.com/updates/accelerated-networking-in-preview) 페이지를 통해 발표됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-143">Changes to these limitations are announced through the [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="57999-144">Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="57999-144">Create a Windows VM</span></span>
<span data-ttu-id="57999-145">Azure Portal 또는 Azure [PowerShell](#windows-powershell)을 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-145">You can use the Azure portal or Azure [PowerShell](#windows-powershell) to create the VM.</span></span>

### <span data-ttu-id="57999-146"><a name="windows-portal"></a>포털</span><span class="sxs-lookup"><span data-stu-id="57999-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="57999-147">인터넷 브라우저에서 Azure [Portal](https://portal.azure.com)을 열고 Azure [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-147">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="57999-148">아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="57999-149">포털에서 시작하여 **+ 새로 만들기** > **계산** > **Windows Server 2016 Datacenter**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-149">In the portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="57999-150">표시되는 **Windows Server 2016 Datacenter** 블레이드의 **배포 모델 선택** 아래에서 *Resource Manager*를 선택한 채로 두고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-150">In the **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="57999-151">표시되는 **기본 사항** 블레이드에서 다음 값을 입력하고, 나머지 기본 옵션을 그대로 두거나 사용자 고유의 값을 선택하거나 입력한 다음, **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-151">In the **Basics** blade that appears, enter the following values, leave the remaining default options or select or enter your own values, and click the **OK** button:</span></span>

    |<span data-ttu-id="57999-152">설정</span><span class="sxs-lookup"><span data-stu-id="57999-152">Setting</span></span>|<span data-ttu-id="57999-153">값</span><span class="sxs-lookup"><span data-stu-id="57999-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="57999-154">이름</span><span class="sxs-lookup"><span data-stu-id="57999-154">Name</span></span>|<span data-ttu-id="57999-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="57999-155">MyVm</span></span>|
    |<span data-ttu-id="57999-156">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="57999-156">Resource group</span></span>|<span data-ttu-id="57999-157">**새로 만들기**를 선택한 채로 두고 *MyResourceGroup*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="57999-158">위치</span><span class="sxs-lookup"><span data-stu-id="57999-158">Location</span></span>|<span data-ttu-id="57999-159">미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="57999-159">West US 2</span></span>|

    <span data-ttu-id="57999-160">Azure를 처음 사용하는 경우 [리소스 그룹](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [구독](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) 및 [위치](https://azure.microsoft.com/regions)(지역이라고도 함)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="57999-160">If you're new to Azure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred to as regions).</span></span>
5. <span data-ttu-id="57999-161">표시되는 **크기 선택** 블레이드의 **최소 코어 수** 상자에서 *8*을 입력한 다음 **모두 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-161">In the **Choose a size** blade that appears, enter *8* in the **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="57999-162">**DS4_V2 표준** 또는 지원되는 VM을 클릭한 다음 **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-162">Click **DS4_V2 Standard**, or any supported VM, then click the **Select** button.</span></span>
7. <span data-ttu-id="57999-163">표시되는 **설정** 블레이드에서 모든 설정은 그대로 두는 한편, **가속화된 네트워킹** 아래에서 **사용**을 클릭한 다음 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-163">In the **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click the **OK** button.</span></span> <span data-ttu-id="57999-164">**참고:** 이 문서의 [제한 사항](#Limitations) 섹션에서 설명하지 않은 VM 크기, 운영 체제 또는 위치에 대한 값을 이전 단계에서 선택한 경우 **가속화된 네트워킹**은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in the [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="57999-165">표시되는 **요약** 블레이드에서 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-165">In the **Summary** blade that appears, click the **OK** button.</span></span> <span data-ttu-id="57999-166">Azure VM을 만들기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-166">Azure starts creating the VM.</span></span> <span data-ttu-id="57999-167">VM을 만드는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="57999-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="57999-168">Windows용 가속화된 네트워킹 드라이버를 설치하려면 이 문서의 [Windows 구성](#configure-windows)섹션에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-168">To install the accelerated networking driver for Windows, complete the steps in the [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="57999-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="57999-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="57999-170">최신 버전의 Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-170">Install the latest version of the Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="57999-171">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell 개요](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57999-171">If you're new to Azure PowerShell, read the [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="57999-172">[Windows 시작] 단추를 클릭하고 **powershell**을 입력한 다음 검색 결과에서 **PowerShell**을 클릭하여 PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-172">Start a PowerShell session by clicking the Windows Start button, typing **powershell**, then clicking **PowerShell** from the search results.</span></span>
3. <span data-ttu-id="57999-173">PowerShell 창에서 `login-azurermaccount` 명령을 입력하여 Azure [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-173">In your PowerShell window, enter the `login-azurermaccount` command to sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="57999-174">아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="57999-175">브라우저에서 다음 스크립트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-175">In your browser, copy the following script:</span></span>
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

    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
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

    # Create the virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="57999-176">PowerShell 창에서 마우스 오른쪽 단추를 클릭하여 스크립트를 붙여넣고 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-176">In your PowerShell window, right-click to paste the script and start executing it.</span></span> <span data-ttu-id="57999-177">사용자 이름과 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="57999-177">You are prompted for a username and password.</span></span> <span data-ttu-id="57999-178">다음 단계에서 VM에 연결할 때 이 자격 증명을 사용하여 해당 VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-178">Use these credentials to log in to the VM when connecting to it in the next step.</span></span> <span data-ttu-id="57999-179">스크립트가 실패하고 스크립트를 실행하기 전에 스크립트의 값을 변경한 경우 VM 크기, 운영 체제 및 위치에 사용한 값이 이 문서의 [제한 사항](#Limitations) 섹션에서 설명하는 값인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-179">If the script fails, and you changed values in the script before executing it, confirm the values you used for VM size, operating system, and location are listed in the [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="57999-180">Windows용 가속화된 네트워킹 드라이버를 설치하려면 이 문서의 [Windows 구성](#configure-windows)섹션에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-180">To install the accelerated networking driver for Windows, complete the steps in the [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="57999-181"><a name="configure-windows"></a>Windows 구성</span><span class="sxs-lookup"><span data-stu-id="57999-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="57999-182">Azure에서 VM을 만든 후에는 Windows용 가속화된 네트워킹 드라이버를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-182">Once you create the VM in Azure, you must install the accelerated networking driver for Windows.</span></span> <span data-ttu-id="57999-183">다음 단계를 수행하기 전에 이 문서의 [포털](#windows-portal) 또는 [PowerShell](#windows-powershell) 단계를 사용하여 가속화된 네트워킹을 사용하는 Windows VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-183">Before completing the following steps, you must have created a Windows VM with accelerated networking using either the [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="57999-184">인터넷 브라우저에서 Azure [Portal](https://portal.azure.com)을 열고 Azure [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-184">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="57999-185">아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="57999-186">*리소스 검색* 텍스트가 있는 Azure Portal 위쪽의 상자에서 *MyVm*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-186">In the box that contains the text *Search resources* at the top of the Azure portal, type *MyVm*.</span></span> <span data-ttu-id="57999-187">검색 결과에서 표시되는 **MyVm**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-187">When **MyVm** appears in the search results, click it.</span></span>
3. <span data-ttu-id="57999-188">표시되는 **MyVm** 블레이드에서 왼쪽 위 모서리에 있는 **연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-188">In the **MyVm** blade that appears, click the **Connect** button in the top left corner of the blade.</span></span> <span data-ttu-id="57999-189">**참고:** **연결** 단추 아래에서 **만들기**가 표시되는 경우 Azure에서 VM 만들기를 아직 완료하지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="57999-189">**Note:** If **Creating** is visible under the **Connect** button, Azure has not yet finished creating the VM.</span></span> <span data-ttu-id="57999-190">따라서 **연결** 단추 아래에서 **만들기**가 더 이상 표시되지 않는 경우에만 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-190">Click **Connect** only after you no longer see **Creating** under the **Connect** button.</span></span>
4. <span data-ttu-id="57999-191">브라우저에서 **MyVm.rdp** 파일을 다운로드하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-191">Allow your browser to download the **MyVm.rdp** file.</span></span>  <span data-ttu-id="57999-192">다운로드한 후에 해당 파일을 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="57999-192">Once downloaded, click the file to open it.</span></span> 
5. <span data-ttu-id="57999-193">원격 연결의 게시자를 식별할 수 없다고 알리는 메시지와 함께 표시되는 **원격 데스크톱 연결** 상자에서 **연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-193">Click the **Connect** button in the **Remote Desktop Connection** box that appears, notifying you that the publisher of the remote connection can't be identified.</span></span>
6. <span data-ttu-id="57999-194">표시되는 **Windows 보안** 상자에서 **추가 선택 항목**을 클릭한 다음 **다른 계정 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-194">In the **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="57999-195">4단계에서 입력한 사용자 이름과 암호를 입력한 다음 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-195">Enter the username and password you entered in step 4, then click the **OK** button.</span></span>
7. <span data-ttu-id="57999-196">원격 컴퓨터의 ID를 확인할 수 없다고 알리는 메시지와 함께 표시되는 [원격 데스크톱 연결] 상자에서 **예** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-196">Click the **Yes** button in the Remote Desktop Connection box that appears, notifying you that the identity of the remote computer cannot be verified.</span></span>
8. <span data-ttu-id="57999-197">[Windows 시작] 단추를 마우스 오른쪽 단추로 클릭한 다음 **장치 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-197">Right-click the Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="57999-198">**네트워크 어댑터** 노드를 펼칩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-198">Expand the **Network adapters** node.</span></span> <span data-ttu-id="57999-199">다음 그림과 같이 **Mellanox ConnectX-3 Virtual Function Ethernet Adapter**가 나타나는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-199">Confirm that the **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in the following picture:</span></span>
   
    ![장치 관리자](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="57999-201">이제 가속화된 네트워킹을 VM에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="57999-202">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="57999-202">Create a Linux VM</span></span>
<span data-ttu-id="57999-203">Azure Portal 또는 Azure [PowerShell](#linux-powershell)을 사용하여 Ubuntu 또는 SLES VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-203">You can use the Azure portal or Azure [PowerShell](#linux-powershell) to create an Ubuntu or SLES VM.</span></span> <span data-ttu-id="57999-204">RHEL 및 CentOS VM의 경우 다른 워크플로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="57999-205">아래의 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57999-205">Please see the instructions below.</span></span>

### <span data-ttu-id="57999-206"><a name="linux-portal"></a>포털</span><span class="sxs-lookup"><span data-stu-id="57999-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="57999-207">이 문서의 [Linux VM 만들기 - PowerShell](#linux-powershell) 섹션에 나오는 1-5단계를 수행하여 Linux 가속화된 네트워킹 미리 보기에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-207">Register for the accelerated networking for Linux preview by completing steps 1-5 of the [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="57999-208">포털에서는 미리 보기에 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-208">You cannot register for the preview in the portal.</span></span>
2. <span data-ttu-id="57999-209">이 문서의 [Windows VM 만들기 - 포털](#windows-portal) 섹션에 나오는 1-8단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-209">Complete steps 1-8 in the [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="57999-210">2단계에서 **Windows Server 2016 Datacenter** 대신 **Ubuntu Server 16.04 LTS**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="57999-211">이 자습서에서는 SSH 키 대신 암호를 사용하도록 선택하지만, 프로덕션 배포에서는 둘 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-211">For this tutorial, choose to use a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="57999-212">이 문서의 [Windows VM 만들기 - 포털](#windows-portal) 섹션의 7단계를 수행할 때 **가속화된 네트워킹**이 나타나지 않으면 다음과 같은 이유 중 하나로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-212">If **Accelerated networking** does not appear when you complete step 7 of the [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of the following reasons:</span></span>
    - <span data-ttu-id="57999-213">아직 미리 보기에 등록되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-213">You are not yet registered for the preview.</span></span> <span data-ttu-id="57999-214">이 문서의 [Linux VM 만들기 - Powershell](#linux-powershell) 섹션의 4단계에서 설명한 대로 등록 상태가 **등록됨**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-214">Confirm that your registration state is **Registered**, as explained in step 4 of the [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="57999-215">**참고:** Windows VM용 가속화된 네트워킹 미리 보기에 참여한 경우 Windows VM용 가속화된 네트워킹을 사용하기 위해 더 이상 등록할 필요가 없지만, Linux VM용 가속화된 네트워킹 미리 보기에서는 자동으로 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-215">**Note:** If you participated in the Accelerated networking for Windows VMs preview (it's no longer necessary to register to use Accelerated networking for Windows VMs), you are not automatically registered for the Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="57999-216">따라서 참여할 Linux VM 가속화된 네트워킹 미리 보기에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-216">You must register for the Accelerated networking for Linux VMs preview to participate in it.</span></span>
    - <span data-ttu-id="57999-217">이 문서의 [제한 사항](#limitations) 섹션에서 설명하는 VM 크기, 운영 체제 또는 위치를 선택하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-217">You have not selected a VM size, operating system, or location listed in the [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="57999-218">Linux용 가속화된 네트워킹 드라이버를 설치하려면 이 문서의 [Linux 구성](#configure-linux)섹션에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-218">To install the accelerated networking driver for Linux, complete the steps in the [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="57999-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="57999-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="57999-220">구독에서 가속화된 네트워킹을 사용하는 Linux VM을 만든 다음 동일한 구독에서 가속화된 네트워킹을 사용하는 Windows VM을 만들려고 하면 Windows VM 만들기가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt to create a Windows VM with accelerated networking in the same subscription, the Windows VM creation may fail.</span></span> <span data-ttu-id="57999-221">이 미리 보기에서는 가속화된 네트워킹을 사용하는 Linux VM과 Windows VM을 별도의 구독에서 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="57999-222">최신 버전의 Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-222">Install the latest version of the Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="57999-223">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell 개요](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57999-223">If you're new to Azure PowerShell, read the [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="57999-224">[Windows 시작] 단추를 클릭하고 **powershell**을 입력한 다음 검색 결과에서 **PowerShell**을 클릭하여 PowerShell 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-224">Start a PowerShell session by clicking the Windows Start button, typing **powershell**, then clicking **PowerShell** from the search results.</span></span>
3. <span data-ttu-id="57999-225">PowerShell 창에서 `login-azurermaccount` 명령을 입력하여 Azure [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-225">In your PowerShell window, enter the `login-azurermaccount` command to sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="57999-226">아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="57999-227">다음 단계를 완료하여 Azure 가속화된 네트워킹 미리 보기에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-227">Register for the accelerated networking for Azure preview by completing the following steps:</span></span>
    - <span data-ttu-id="57999-228">Azure 구독 ID 및 의도된 용도가 포함된 전자 메일을 [axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e)에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="57999-228">Send an email to [axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="57999-229">Microsoft에서 보내는 구독 활성화에 대한 메일 확인을 기다려 주세요.</span><span class="sxs-lookup"><span data-stu-id="57999-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="57999-230">다음 명령을 입력하여 미리 보기에 등록되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-230">Enter the following command to confirm you are registered for the preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="57999-231">이전 명령을 입력한 후 출력에 **등록됨**이 나타날 때까지 5단계로 진행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="57999-231">Do not continue with step 5 until **Registered** appears in the output after you enter the previous command.</span></span> <span data-ttu-id="57999-232">계속 진행하기 전에 출력은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-232">Your output must look like the following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="57999-233">Windows VM용 가속화된 네트워킹 미리 보기에 참여한 경우 Windows VM용 가속화된 네트워킹을 사용하기 위해 더 이상 등록할 필요가 없지만, Linux VM용 가속화된 네트워킹 미리 보기에서는 자동으로 등록되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-233">If you participated in the Accelerated networking for Windows VMs preview (it's no longer necessary to register to use Accelerated networking for Windows VMs), you are not automatically registered for the Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="57999-234">따라서 참여할 Linux VM 가속화된 네트워킹 미리 보기에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-234">You must register for the Accelerated networking for Linux VMs preview to participate in it.</span></span>
      >
5. <span data-ttu-id="57999-235">브라우저에서 Ubuntu 또는 SLES를 원하는 대로 대체하는 다음 스크립트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-235">In your browser, copy the following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="57999-236">또한 Redhat 및 CentOS에는 아래에서 간략하게 설명되는 다른 워크플로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

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

    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define the new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
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

    # Create the virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="57999-237">PowerShell 창에서 마우스 오른쪽 단추를 클릭하여 스크립트를 붙여넣고 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-237">In your PowerShell window, right-click to paste the script and start executing it.</span></span> <span data-ttu-id="57999-238">사용자 이름과 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="57999-238">You are prompted for a username and password.</span></span> <span data-ttu-id="57999-239">다음 단계에서 VM에 연결할 때 이 자격 증명을 사용하여 해당 VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-239">Use these credentials to log in to the VM when connecting to it in the next step.</span></span> <span data-ttu-id="57999-240">스크립트가 실패하면 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-240">If the script fails, confirm that:</span></span>
    - <span data-ttu-id="57999-241">4단계에서 설명한 대로 미리 보기에 등록되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-241">You are registered for the preview, as explained in step 4</span></span>
    - <span data-ttu-id="57999-242">스크립트를 실행하기 전에 스크립트에서 VM 크기, 운영 체제 유형 및 위치의 값을 변경한 경우 해당 값이 이 문서의 [제한 사항](#Limitations) 섹션에서 설명하는 값인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-242">If you changed VM size, operating system type, or location values in the script before executing it, that the values are listed in the [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="57999-243">Linux용 가속화된 네트워킹 드라이버를 설치하려면 이 문서의 [Linux 구성](#configure-linux)섹션에서 설명하는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-243">To install the accelerated networking driver for Linux, complete the steps in the [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="57999-244"><a name="configure-linux"></a>Linux 구성</span><span class="sxs-lookup"><span data-stu-id="57999-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="57999-245">Azure에서 VM을 만든 후에는 Linux용 가속화된 네트워킹 드라이버를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-245">Once you create the VM in Azure, you must install the accelerated networking driver for Linux.</span></span> <span data-ttu-id="57999-246">다음 단계를 수행하기 전에 이 문서의 [포털](#linux-portal) 또는 [PowerShell](#linux-powershell) 단계를 사용하여 가속화된 네트워킹을 사용하는 Linux VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-246">Before completing the following steps, you must have created a Linux VM with accelerated networking using either the [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="57999-247">인터넷 브라우저에서 Azure [Portal](https://portal.azure.com)을 열고 Azure [계정](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-247">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="57999-248">아직 계정이 없는 경우 [평가판](https://azure.microsoft.com/offers/ms-azr-0044p)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="57999-249">포털 위쪽의 *리소스 검색* 상자 오른쪽에 있는 **>_** 아이콘을 클릭하여 Bash 클라우드 셸(미리 보기)을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-249">At the top of the portal, to the right of the *Search resources* bar, click the **>_** icon to start a Bash cloud shell (Preview).</span></span> <span data-ttu-id="57999-250">Bash 클라우드 셸 창이 포털의 아래쪽에 나타나고, 몇 초 후에 **username@Azure:~$** 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-250">The Bash cloud shell pane appears at the bottom of the portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="57999-251">컴퓨터에서 VM으로 클라우드 셸 대신 SSH를 수행할 수 있지만, 이 자습서의 지침에서는 클라우드 셸을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-251">Though you can SSH to the VM from your computer, rather than the cloud shell, the instructions in this tutorial assume you're using the cloud shell.</span></span>
3. <span data-ttu-id="57999-252">*리소스 검색* 텍스트가 있는 포털 위쪽의 상자에서 *MyVm*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-252">At the top of the portal, in the box that contains the text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="57999-253">검색 결과에서 표시되는 **MyVm**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-253">When **MyVm** appears in the search results, click it.</span></span>
4. <span data-ttu-id="57999-254">표시되는 **MyVm** 블레이드에서 왼쪽 위 모서리에 있는 **연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-254">In the **MyVm** blade that appears, click the **Connect** button in the top left corner of the blade.</span></span> <span data-ttu-id="57999-255">**참고:** **연결** 단추 아래에서 **만들기**가 표시되는 경우 Azure에서 VM 만들기를 아직 완료하지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="57999-255">**Note:** If **Creating** is visible under the **Connect** button, Azure has not yet finished creating the VM.</span></span> <span data-ttu-id="57999-256">따라서 **연결** 단추 아래에서 **만들기**가 더 이상 표시되지 않는 경우에만 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-256">Click **Connect** only after you no longer see **Creating** under the **Connect** button.</span></span>
5. <span data-ttu-id="57999-257">Azure에서 `ssh adminuser@<ipaddress>`를 입력하라는 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="57999-257">Azure opens a box telling you to enter the `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="57999-258">이 명령을 클라우드 셸에서 입력하거나 4단계에서 표시되는 상자에서 복사하여 클라우드 셸에 붙여넣은 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="57999-258">Enter this command in the cloud shell (or copy it from the box that appeared in step 4 and paste it in to the cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="57999-259">연결을 계속할 것인지 묻는 질문에 **예**를 입력한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="57999-259">Enter **yes** to the question asking you if you want to continue connecting, then press Enter.</span></span>
7. <span data-ttu-id="57999-260">VM을 만들 때 입력한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-260">Enter the password you entered when creating the VM.</span></span> <span data-ttu-id="57999-261">VM에 성공적으로 로그인하면 adminuser@MyVm:~$ 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-261">Once successfully logged in to the VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="57999-262">이제 클라우드 셸 세션을 통해 VM에 로그인했습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-262">You are now logged in to the VM through the cloud shell session.</span></span> <span data-ttu-id="57999-263">**참고:** 클라우드 셸 세션을 10분 동안 사용하지 않으면 시간이 초과됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="57999-264">이때 지침은 사용 중인 배포에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="57999-264">At this point, the instructions vary based on the distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="57999-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="57999-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="57999-266">프롬프트에 `uname -r`을 입력하고 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-266">At the prompt, enter `uname -r` and confirm the version for:</span></span>

    * <span data-ttu-id="57999-267">Ubuntu는 "4.4.0-77-generic" 이상임</span><span class="sxs-lookup"><span data-stu-id="57999-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="57999-268">SLES는 "4.4.59-92.20-default" 이상임</span><span class="sxs-lookup"><span data-stu-id="57999-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="57999-269">다음 명령을 실행하여 표준 네트워킹 vNIC와 가속화된 네트워킹 vNIC 간에 본드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57999-269">Create a bond between the standard networking vNIC and the accelerated networking vNIC by running the commands that follow.</span></span> <span data-ttu-id="57999-270">네트워크 트래픽은 고성능 가속화된 네트워킹 vNIC를 사용하는 반면, 본드는 특정 구성 변경에서 네트워킹 트래픽이 중단되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-270">Network traffic uses the higher performing accelerated networking vNIC, while the bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="57999-271">스크립트를 실행한 후 VM은 60초 일시 정지된 후 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-271">After running the script, the VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="57999-272">VM이 다시 시작되면 5-7단계를 다시 수행하여 VM에 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-272">Once the VM is restarted, reconnect to it by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="57999-273">`ifconfig` 명령을 실행하고 bond0이 나타나고 인터페이스가 UP으로 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-273">Run the `ifconfig` command and confirm that bond0 has come up and the interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="57999-274">가속화된 네트워킹을 사용하는 응용 프로그램은 *eth0*이 아닌 *bond0* 인터페이스를 통해 통신해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-274">Applications using accelerated networking must communicate over the *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="57999-275">가속화된 네트워킹이 일반적으로 공급되기 전에 인터페이스 이름이 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57999-275">The interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="57999-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="57999-276">RHEL/CentOS</span></span>

<span data-ttu-id="57999-277">Red Hat Enterprise Linux 또는 CentOS 7.3 VM을 만들려면 SR-IOV에 필요한 드라이버와 네트워크 카드용 VF(Virtual Function) 드라이버를 로드하는 추가적인 몇 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps to load the latest drivers needed for SR-IOV and the Virtual Function (VF) driver for the network card.</span></span> <span data-ttu-id="57999-278">지침의 첫 번째 단계에서는 드라이버가 미리 로드된 하나 이상의 가상 컴퓨터를 만드는 데 사용할 수 있는 이미지를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-278">The first phase of the instructions prepares an image that can be used to make one or more virtual machines that have the drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="57999-279">1단계: Red Hat Enterprise Linux 또는 CentOS 7.3 기본 이미지를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="57999-280">Azure에서 비SRIOV CentOS 7.3 VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="57999-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="57999-281">LIS 4.2.2를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="57999-282">구성 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="57999-283">이 VM의 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="57999-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="57999-284">Azure Portal에서 이 VM을 중지하고 VM의 "디스크"로 이동하여 OSDisk의 VHD URI를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-284">From Azure portal, stop this VM; and go to VM’s "Disks", capture the OSDisk’s VHD URI.</span></span> <span data-ttu-id="57999-285">이 URI에는 기본 이미지의 VHD 이름 및 저장소 계정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="57999-285">This URI contains the base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="57999-286">2단계: Azure에서 새 VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="57999-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="57999-287">vNIC에서 AcceleratedNetworking을 사용하도록 설정하고 1단계에서 캡처된 기본 이미지 VHD를 사용하는 New-AzureRMVMConfig를 기반으로 새 VM을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-287">Provision new VMs based with New-AzureRMVMConfig using the base image VHD captured in phase one, with AcceleratedNetworking enabled on the vNIC:</span></span>

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
    
    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify the base image's VHD URI (from phase one step 5). 
    # Note: The storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need to replace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for the location from which the new image binary large object (BLOB) is copied to start the virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
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
    
    # Create the virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="57999-288">VM이 부팅된 후 "lspci"를 사용하여 VF 장치를 확인하고 Mellanox 항목을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-288">After VMs boot up, check the VF device by "lspci" and check the Mellanox entry.</span></span> <span data-ttu-id="57999-289">예를 들어 lspci 출력에 다음 항목이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-289">For example, we should see this item in the lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="57999-290">다음을 사용하여 본딩 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-290">Run the bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="57999-291">새 VM을 다시 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-291">Reboot the new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="57999-292">VM은 bond0이 구성되고 가속화된 네트워킹 경로가 사용하도록 설정된 상태로 시작되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-292">The VM should start with bond0 configured and the Accelerated Networking path enabled.</span></span>  <span data-ttu-id="57999-293">`ifconfig`를 실행하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57999-293">Run `ifconfig` to confirm.</span></span>
