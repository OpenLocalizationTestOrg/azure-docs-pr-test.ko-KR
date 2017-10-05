---
title: "Azure Linux VM 크기 - HPC | Microsoft Docs"
description: "Azure의 Linux 고성능 컴퓨팅 가상 컴퓨터에 사용할 수 있는 다양한 크기를 나열합니다."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: b7a3844ce86b4efac8a4fc3c2540e7b6460873a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="a06d1-103">고성능 계산 Linux VM 크기</span><span class="sxs-lookup"><span data-stu-id="a06d1-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="a06d1-104">RDMA 지원 인스턴스</span><span class="sxs-lookup"><span data-stu-id="a06d1-104">RDMA-capable instances</span></span>
<span data-ttu-id="a06d1-105">계산 집약적 인스턴스(H16r, H16mr, A8 및 A9) 일부는 RDMA(원격 직접 메모리 액세스) 연결을 위한 네트워크 인터페이스로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="a06d1-106">이 인터페이스는 다른 VM 크기에서 사용할 수 있는 표준 Azure 네트워크 인터페이스 외에 추가로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="a06d1-107">이 인터페이스를 사용하면 RDMA 지원 인스턴스가 InfiniBand 네트워크를 통해 통신할 수 있으며 H16r 및 H16mr 가상 컴퓨터에서는 FDR 속도로, A8 및 A9 가상 컴퓨터에서는 QDR 속도로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="a06d1-108">이러한 RDMA 기능은 MPI(Message Passing Interface) 응용 프로그램의 확장성 및 성능을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="a06d1-109">다음은 RDMA 지원 Linux VM이 Azure RDMA 네트워크에 액세스하기 위한 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-109">Following are requirements for RDMA-capable Linux VMs to access the Azure RDMA network:</span></span>
 
* <span data-ttu-id="a06d1-110">**배포판** - Azure 마켓플레이스의 RDMA 지원 SLES(SUSE Linux Enterprise Server) 또는 Rogue Wave Software(이전의 OpenLogic) CentOS 기반 HPC 이미지에서 VM을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="a06d1-111">다음 Marketplace 이미지는 RDMA 연결을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-111">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="a06d1-112">HPC용 SLES 12 SP1 또는 HPC용 SLES 12 SP1(Premium)</span><span class="sxs-lookup"><span data-stu-id="a06d1-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="a06d1-113">CentOS 기반 7.3 HPC, CentOS 기반 7.1 HPC, CentOS 기반 6.8 HPC 또는 CentOS 기반 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="a06d1-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="a06d1-114">H 시리즈 VM의 경우 HPC용 SLES 12 SP1 이미지 또는 CentOS 기반 7.1 이상 HPC 이미지가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="a06d1-115">CentOS 기반 HPC 이미지에서 커널 업데이트는 **yum** 구성 파일에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-115">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="a06d1-116">즉 Linux RDMA 드라이버가 RPM 패키지로 배포되기 때문에 커널이 업데이트되는 경우 드라이버 업데이트가 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-116">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="a06d1-117">**MPI** - Intel MPI Library 5</span><span class="sxs-lookup"><span data-stu-id="a06d1-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="a06d1-118">선택한 마켓플레이스 이미지에 따라 다음과 같이 Intel MPI의 별도 라이선스, 설치 또는 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-118">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="a06d1-119">**HPC 이미지의 SLES 12 SP1** - VM에 Intel MPI 패키지를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="a06d1-120">다음 명령을 실행하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-120">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="a06d1-121">**CentOS 기반 HPC 이미지** - Intel MPI 5.1은 미리 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="a06d1-122">클러스터된 VM에서 MPI 작업을 실행하기 위해 추가 시스템 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-122">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="a06d1-123">예를 들어 VM 클러스터에서 계산 노드 간에 트러스트를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-123">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="a06d1-124">일반적인 설정에 대해서는 [MPI 응용 프로그램을 실행하도록 Linux RDMA 클러스터 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a06d1-124">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="a06d1-125">네트워크 토폴로지 고려 사항</span><span class="sxs-lookup"><span data-stu-id="a06d1-125">Network topology considerations</span></span>
* <span data-ttu-id="a06d1-126">Azure의 RDMA 지원 Linux VM에서 Eth1은 RDMA 네트워크 트래픽용으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="a06d1-127">Eth1 설정 또는 이 네트워크를 참조하는 구성 파일의 정보를 변경하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a06d1-127">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="a06d1-128">Eth0은 일반 Azure 네트워크 트래픽용으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="a06d1-129">Azure에서 IP over IB(Infiniband)는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="a06d1-130">RDMA over IB만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="a06d1-131">HPC Pack 사용</span><span class="sxs-lookup"><span data-stu-id="a06d1-131">Using HPC Pack</span></span>
<span data-ttu-id="a06d1-132">Microsoft의 무료 HPC 클러스터 및 작업 관리 솔루션인 [HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)은 Linux에서 계산 집약적 인스턴스를 사용하기 위한 한 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="a06d1-133">HPC 팩의 최신 릴리스는 여러 Linux 배포를 지원하여 Windows Server 헤드 노드를 통해 관리되는 Azure VM에서 배포된 계산 노드에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-133">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="a06d1-134">RDMA 지원 Linux 계산 노드에서 Intel MPI가 실행되는 경우 HPC Pack은 RDMA 네트워크에 액세스하는 Linux MPI 응용 프로그램을 예약하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="a06d1-135">[Azure에서 HPC 팩 클러스터의 Linux 계산 노드 시작](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a06d1-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="a06d1-136">기타 크기</span><span class="sxs-lookup"><span data-stu-id="a06d1-136">Other sizes</span></span>
- [<span data-ttu-id="a06d1-137">범용</span><span class="sxs-lookup"><span data-stu-id="a06d1-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="a06d1-138">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="a06d1-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="a06d1-139">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="a06d1-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="a06d1-140">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="a06d1-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="a06d1-141">GPU</span><span class="sxs-lookup"><span data-stu-id="a06d1-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="a06d1-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a06d1-142">Next steps</span></span>

- <span data-ttu-id="a06d1-143">Linux에서 RDMA를 사용하여 계산 집약적 크기를 배포하고 사용하려면 [MPI 응용 프로그램을 실행하기 위해 Linux RDMA 클러스터 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a06d1-143">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="a06d1-144">[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a06d1-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




