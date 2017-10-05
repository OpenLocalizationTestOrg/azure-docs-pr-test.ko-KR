---
title: "Linux의 계산 집약적 VM 정보 | Microsoft Docs"
description: "Linux VM을 위한 H 시리즈 및 A8, A9, A10, A11 계산 집약적 크기 사용에 관한 배경 정보와 고려 사항을 얻습니다."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a2307f7055966ec7146b5da0b4daf1ad469abe2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="a0d5f-103">Linux용 H 시리즈 및 계산 집약적인 A 시리즈 VM 정보</span><span class="sxs-lookup"><span data-stu-id="a0d5f-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="a0d5f-104">여기에는 *계산 집약적* 인스턴스로 알려진 최신 Azure H 시리즈 및 이전 A8, A9, A10 및 A11 크기 사용에 대한 일부 고려 사항과 배경 정보가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-104">Here is background information and some considerations for using the newer Azure H-series and the earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="a0d5f-105">이 문서는 Linux VM에 대해 이러한 크기를 사용하는 것에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="a0d5f-106">[Windows VM](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="a0d5f-107">기본 사양의 저장소 용량 및 디스크 세부 정보는 [가상 컴퓨터 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-to-the-rdma-network"></a><span data-ttu-id="a0d5f-108">RDMA 네트워크에 액세스</span><span class="sxs-lookup"><span data-stu-id="a0d5f-108">Access to the RDMA network</span></span>
<span data-ttu-id="a0d5f-109">다음의 지원되는 Linux HPC 배포판 및 지원되는 MPI 구현 중 하나를 실행하는 RDMA 지원 Linux VM 클러스터를 만들어 Azure RDMA 네트워크를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-109">You can create clusters of RDMA-capable Linux VMs that run one of the following supported Linux HPC distributions and a supported MPI implementation to take advantage of the Azure RDMA network.</span></span> <span data-ttu-id="a0d5f-110">배포 옵션 및 샘플 구성 단계는 [MPI 응용 프로그램을 실행하도록 Linux RDMA 클러스터 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-110">See [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="a0d5f-111">**배포판** - Azure 마켓플레이스의 RDMA 지원 SLES(SUSE Linux Enterprise Server) 또는 Rogue Wave Software(이전의 OpenLogic) CentOS 기반 HPC 이미지에서 VM을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="a0d5f-112">다음 Marketplace 이미지는 RDMA 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-112">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="a0d5f-113">HPC용 SLES 12 SP1, HPC용 SLES 12 SP1(Premium)</span><span class="sxs-lookup"><span data-stu-id="a0d5f-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="a0d5f-114">CentOS 기반 7.1 HPC, CentOS 기반 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="a0d5f-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="a0d5f-115">H 시리즈 VM의 경우 HPC용 SLES 12 SP1 이미지 또는 CentOS 기반 7.1 HPC 이미지가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="a0d5f-116">CentOS 기반 HPC 이미지에서 커널 업데이트는 **yum** 구성 파일에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-116">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="a0d5f-117">즉 Linux RDMA 드라이버가 RPM 패키지로 배포되기 때문에 커널이 업데이트되는 경우 드라이버 업데이트가 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-117">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="a0d5f-118">**MPI** - Intel MPI Library 5</span><span class="sxs-lookup"><span data-stu-id="a0d5f-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="a0d5f-119">선택한 마켓플레이스 이미지에 따라 다음과 같이 Intel MPI의 별도 라이선스, 설치 또는 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-119">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="a0d5f-120">**HPC 이미지의 SLES 12 SP1** - VM에 Intel MPI 패키지를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="a0d5f-121">다음 명령을 실행하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-121">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="a0d5f-122">**CentOS 기반 HPC 이미지** - Intel MPI 5.1은 미리 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="a0d5f-123">클러스터된 VM에서 MPI 작업을 실행하기 위해 추가 시스템 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-123">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="a0d5f-124">예를 들어 VM 클러스터에서 계산 노드 간에 트러스트를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-124">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="a0d5f-125">일반적인 설정에 대해서는 [MPI 응용 프로그램을 실행하도록 Linux RDMA 클러스터 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-125">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="a0d5f-126">HPC 팩 및 Linux에 대한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="a0d5f-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="a0d5f-127">Microsoft의 무료 HPC 클러스터 및 작업 관리 솔루션인 [HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)은 Linux에서 계산 집약적 인스턴스를 사용하기 위한 한 가지 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="a0d5f-128">HPC 팩의 최신 릴리스는 여러 Linux 배포를 지원하여 Windows Server 헤드 노드를 통해 관리되는 Azure VM에서 배포된 계산 노드에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-128">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="a0d5f-129">RDMA 지원 Linux 계산 노드에서 Intel MPI가 실행되는 경우 HPC Pack은 RDMA 네트워크에 액세스하는 Linux MPI 응용 프로그램을 예약하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="a0d5f-130">시작하려면 [Azure에서 HPC Pack 클러스터의 Linux 계산 노드 시작](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-130">To get started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="a0d5f-131">네트워크 토폴로지 고려 사항</span><span class="sxs-lookup"><span data-stu-id="a0d5f-131">Network topology considerations</span></span>
* <span data-ttu-id="a0d5f-132">Azure의 RDMA 지원 Linux VM에서 Eth1은 RDMA 네트워크 트래픽용으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="a0d5f-133">Eth1 설정 또는 이 네트워크를 참조하는 구성 파일의 정보를 변경하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-133">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="a0d5f-134">Eth0은 일반 Azure 네트워크 트래픽용으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="a0d5f-135">Azure에서 IP over IB(Infiniband)는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="a0d5f-136">RDMA over IB만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a0d5f-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0d5f-137">Next steps</span></span>
* <span data-ttu-id="a0d5f-138">계산 집약적 크기의 가용성 및 가격 책정에 대한 세부 정보는 [가상 컴퓨터 가격 책정](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-138">For details about availability and pricing of the compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="a0d5f-139">저장소 용량 및 디스크 세부 정보는 [가상 컴퓨터 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="a0d5f-140">Linux에서 RDMA를 사용하여 계산 집약적 크기를 배포하고 사용하려면 [MPI 응용 프로그램을 실행하기 위해 Linux RDMA 클러스터 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0d5f-140">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

