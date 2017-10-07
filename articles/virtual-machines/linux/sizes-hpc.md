---
title: "Linux VM aaaAzure 크기-HPC | Microsoft Docs"
description: "Linux 고성능 컴퓨팅 Azure의 가상 컴퓨터에 사용할 수 있는 hello 다른 크기를 나열 합니다."
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
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="3c437-103">고성능 계산 Linux VM 크기</span><span class="sxs-lookup"><span data-stu-id="3c437-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="3c437-104">RDMA 지원 인스턴스</span><span class="sxs-lookup"><span data-stu-id="3c437-104">RDMA-capable instances</span></span>
<span data-ttu-id="3c437-105">Hello 계산 집약적인 인스턴스 (H16r, H16mr, A8 및 A9)의 하위 집합에는 원격 직접 메모리 액세스 (RDMA) 연결에 대 한 네트워크 인터페이스를 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="3c437-106">이 인터페이스는 또한 toohello 표준 Azure 네트워크 인터페이스 tooother 사용 가능한 VM 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="3c437-107">이 인터페이스는 H16r 및 H16mr 가상 컴퓨터에 대 한 FDR 속도 및 A8 및 A9 가상 컴퓨터에 대 한 QDR 속도에서 작동 하는 InfiniBand 네트워크를 통해 RDMA 가능 인스턴스 toocommunicate hello를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="3c437-108">이러한 RDMA 기능 인터페이스 MPI (Message Passing) 응용 프로그램의 hello 확장성과 성능을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="3c437-109">다음은 Linux Vm의 경우 RDMA 가능 tooaccess hello Azure RDMA 네트워크에 대 한 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-109">Following are requirements for RDMA-capable Linux VMs tooaccess hello Azure RDMA network:</span></span>
 
* <span data-ttu-id="3c437-110">**분포** -Vm에서 RDMA 가능 SUSE Linux Enterprise Server (SLES)를 배포 해야 또는 불량 웨이브 소프트웨어 (이전의 OpenLogic) CentOS 기반 HPC 이미지에서 Azure 마켓플레이스를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="3c437-111">hello 다음 마켓플레이스 이미지 지원 RDMA 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-111">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="3c437-112">HPC용 SLES 12 SP1 또는 HPC용 SLES 12 SP1(Premium)</span><span class="sxs-lookup"><span data-stu-id="3c437-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="3c437-113">CentOS 기반 7.3 HPC, CentOS 기반 7.1 HPC, CentOS 기반 6.8 HPC 또는 CentOS 기반 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="3c437-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="3c437-114">H 시리즈 VM의 경우 HPC용 SLES 12 SP1 이미지 또는 CentOS 기반 7.1 이상 HPC 이미지가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="3c437-115">Hello HPC CentOS 기반 이미지에서 커널 업데이트는 해제 되어 hello **yum** 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-115">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="3c437-116">Hello Linux RDMA 드라이버 배포 되는 RPM 패키지 및 드라이버 업데이트에는 hello 커널 업데이트 되는 경우 작동 하지 않을 수 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-116">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="3c437-117">**MPI** - Intel MPI Library 5</span><span class="sxs-lookup"><span data-stu-id="3c437-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="3c437-118">Hello 마켓플레이스 이미지에 따라을 선택 하면 별도 라이선스를 설치 또는 Intel MPI의 구성이 필요할 수 있습니다. 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-118">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="3c437-119">**HPC 이미지에 대 한 SLES 12 SP1** -Intel MPI 패키지 hello VM에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="3c437-120">Hello 다음 명령을 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-120">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="3c437-121">**CentOS 기반 HPC 이미지** - Intel MPI 5.1은 미리 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="3c437-122">추가 시스템 구성은 클러스터 된 Vm에서 필요한 toorun MPI 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-122">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="3c437-123">예를 들어 tooestablish 필요한 Vm의 클러스터에서 계산 노드 hello 간의 트러스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-123">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="3c437-124">일반 설정에 대 한 참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3c437-124">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="3c437-125">네트워크 토폴로지 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3c437-125">Network topology considerations</span></span>
* <span data-ttu-id="3c437-126">Azure의 RDMA 지원 Linux VM에서 Eth1은 RDMA 네트워크 트래픽용으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="3c437-127">E t h 1 설정은 되거나 toothis 네트워크를 참조 하는 hello 구성 파일에 대 한 정보를 변경 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="3c437-127">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="3c437-128">Eth0은 일반 Azure 네트워크 트래픽용으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="3c437-129">Azure에서 IP over IB(Infiniband)는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="3c437-130">RDMA over IB만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="3c437-131">HPC Pack 사용</span><span class="sxs-lookup"><span data-stu-id="3c437-131">Using HPC Pack</span></span>
<span data-ttu-id="3c437-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft의 무료 HPC 클러스터 및 작업 관리 솔루션에서 Linux 사용 하 여 toouse hello 계산 집약적인 인스턴스를 하나의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="3c437-133">HPC 팩의 최신 릴리스에 hello toorun에 계산 노드 헤드 노드를 Windows Server에서 관리 되는 Azure Vm에 배포 된 여러 Linux 배포판을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-133">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="3c437-134">Intel MPI 실행 되는 RDMA 가능 Linux의 계산 노드, 사용 HPC Pack 예약 하 고 hello RDMA 네트워크를 액세스 Linux MPI 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="3c437-135">[Azure에서 HPC 팩 클러스터의 Linux 계산 노드 시작](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c437-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="3c437-136">기타 크기</span><span class="sxs-lookup"><span data-stu-id="3c437-136">Other sizes</span></span>
- [<span data-ttu-id="3c437-137">범용</span><span class="sxs-lookup"><span data-stu-id="3c437-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="3c437-138">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="3c437-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="3c437-139">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="3c437-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="3c437-140">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="3c437-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="3c437-141">GPU</span><span class="sxs-lookup"><span data-stu-id="3c437-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="3c437-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c437-142">Next steps</span></span>

- <span data-ttu-id="3c437-143">배포 하 고 계산 집약적인 크기를 사용 하 여 linux에서 RDMA와 시작 tooget 참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-143">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="3c437-144">[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3c437-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




