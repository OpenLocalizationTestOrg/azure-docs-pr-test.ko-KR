---
title: "계산 집약적 aaaAbout와 Linux Vm | Microsoft Docs"
description: "배경 정보 및 hello H 시리즈 및 A8, A9, A10 및 A11 계산 집약적 크기를 사용 하 여 Linux vm에 대 한 고려 사항"
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
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="ecc6c-103">Linux용 H 시리즈 및 계산 집약적인 A 시리즈 VM 정보</span><span class="sxs-lookup"><span data-stu-id="ecc6c-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="ecc6c-104">배경 정보 및 사용에 대 한 몇 가지 고려 사항 최신 Azure H 시리즈 hello 및 이전 A8, A9, A10 및 A11 크기 라고도 hello *계산 집약적인* 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-104">Here is background information and some considerations for using hello newer Azure H-series and hello earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="ecc6c-105">이 문서는 Linux VM에 대해 이러한 크기를 사용하는 것에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="ecc6c-106">[Windows VM](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="ecc6c-107">기본 사양의 저장소 용량 및 디스크 세부 정보는 [가상 컴퓨터 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a><span data-ttu-id="ecc6c-108">Toohello RDMA 네트워크 액세스</span><span class="sxs-lookup"><span data-stu-id="ecc6c-108">Access toohello RDMA network</span></span>
<span data-ttu-id="ecc6c-109">Hello 지원 되는 Linux HPC 분포와 hello Azure RDMA 네트워크의 지원 되는 MPI 구현 tootake 이점은 다음 중 하나를 실행 하는 RDMA 가능 Linux Vm의 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-109">You can create clusters of RDMA-capable Linux VMs that run one of hello following supported Linux HPC distributions and a supported MPI implementation tootake advantage of hello Azure RDMA network.</span></span> <span data-ttu-id="ecc6c-110">참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 배포 옵션 및 샘플 구성 단계에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-110">See [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="ecc6c-111">**분포** -Vm에서 RDMA 가능 SUSE Linux Enterprise Server (SLES)를 배포 해야 또는 불량 웨이브 소프트웨어 (이전의 OpenLogic) CentOS 기반 HPC 이미지에서 Azure 마켓플레이스를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="ecc6c-112">hello 다음 마켓플레이스 이미지 지원 RDMA 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-112">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="ecc6c-113">HPC용 SLES 12 SP1, HPC용 SLES 12 SP1(Premium)</span><span class="sxs-lookup"><span data-stu-id="ecc6c-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="ecc6c-114">CentOS 기반 7.1 HPC, CentOS 기반 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="ecc6c-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="ecc6c-115">H 시리즈 VM의 경우 HPC용 SLES 12 SP1 이미지 또는 CentOS 기반 7.1 HPC 이미지가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="ecc6c-116">Hello HPC CentOS 기반 이미지에서 커널 업데이트는 해제 되어 hello **yum** 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-116">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="ecc6c-117">Hello Linux RDMA 드라이버 배포 되는 RPM 패키지 및 드라이버 업데이트에는 hello 커널 업데이트 되는 경우 작동 하지 않을 수 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-117">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="ecc6c-118">**MPI** - Intel MPI Library 5</span><span class="sxs-lookup"><span data-stu-id="ecc6c-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="ecc6c-119">Hello 마켓플레이스 이미지에 따라을 선택 하면 별도 라이선스를 설치 또는 Intel MPI의 구성이 필요할 수 있습니다. 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-119">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="ecc6c-120">**HPC 이미지에 대 한 SLES 12 SP1** -Intel MPI 패키지 hello VM에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="ecc6c-121">Hello 다음 명령을 실행 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-121">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="ecc6c-122">**CentOS 기반 HPC 이미지** - Intel MPI 5.1은 미리 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="ecc6c-123">추가 시스템 구성은 클러스터 된 Vm에서 필요한 toorun MPI 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-123">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="ecc6c-124">예를 들어 tooestablish 필요한 Vm의 클러스터에서 계산 노드 hello 간의 트러스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-124">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="ecc6c-125">일반 설정에 대 한 참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-125">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="ecc6c-126">HPC 팩 및 Linux에 대한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="ecc6c-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="ecc6c-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft의 무료 HPC 클러스터 및 작업 관리 솔루션을와 Linux toouse hello 계산 집약적인 인스턴스를 하나의 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="ecc6c-128">HPC 팩의 최신 릴리스에 hello toorun에 계산 노드 헤드 노드를 Windows Server에서 관리 되는 Azure Vm에 배포 된 여러 Linux 배포판을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-128">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="ecc6c-129">Intel MPI 실행 되는 RDMA 가능 Linux의 계산 노드, 사용 HPC Pack 예약 하 고 hello RDMA 네트워크를 액세스 Linux MPI 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="ecc6c-130">시작 tooget 참조 [Azure에서 HPC Pack 클러스터에서 계산 노드 Linux 시작](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-130">tooget started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="ecc6c-131">네트워크 토폴로지 고려 사항</span><span class="sxs-lookup"><span data-stu-id="ecc6c-131">Network topology considerations</span></span>
* <span data-ttu-id="ecc6c-132">Azure의 RDMA 지원 Linux VM에서 Eth1은 RDMA 네트워크 트래픽용으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="ecc6c-133">E t h 1 설정은 되거나 toothis 네트워크를 참조 하는 hello 구성 파일에 대 한 정보를 변경 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-133">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="ecc6c-134">Eth0은 일반 Azure 네트워크 트래픽용으로 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="ecc6c-135">Azure에서 IP over IB(Infiniband)는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="ecc6c-136">RDMA over IB만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="ecc6c-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ecc6c-137">Next steps</span></span>
* <span data-ttu-id="ecc6c-138">가용성 및 hello 계산 집약적인 크기의 가격 책정에 대 한 세부 정보를 참조 하십시오. [가상 컴퓨터 가격](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-138">For details about availability and pricing of hello compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="ecc6c-139">저장소 용량 및 디스크 세부 정보는 [가상 컴퓨터 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="ecc6c-140">배포 하 고 계산 집약적인 크기를 사용 하 여 linux에서 RDMA와 시작 tooget 참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecc6c-140">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

