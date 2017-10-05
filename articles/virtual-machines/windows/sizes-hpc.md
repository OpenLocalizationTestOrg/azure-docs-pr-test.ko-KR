---
title: "Azure Windows VM 크기 - HPC | Microsoft Docs"
description: "Azure의 Windows 고성능 컴퓨팅 가상 컴퓨터에 사용할 수 있는 다양한 크기를 나열합니다."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: a0596d134e9c26877848f93d72f35bfd2c957570
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="30520-103">고성능 계산 VM 크기</span><span class="sxs-lookup"><span data-stu-id="30520-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="30520-104">RDMA 지원 인스턴스</span><span class="sxs-lookup"><span data-stu-id="30520-104">RDMA-capable instances</span></span>
<span data-ttu-id="30520-105">계산 집약적 인스턴스(H16r, H16mr, A8 및 A9) 일부는 RDMA(원격 직접 메모리 액세스) 연결을 위한 네트워크 인터페이스로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="30520-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="30520-106">이 인터페이스는 다른 VM 크기에서 사용할 수 있는 표준 Azure 네트워크 인터페이스 외에 추가로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="30520-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="30520-107">이 인터페이스를 사용하면 RDMA 지원 인스턴스가 InfiniBand 네트워크를 통해 통신할 수 있으며 H16r 및 H16mr 가상 컴퓨터에서는 FDR 속도로, A8 및 A9 가상 컴퓨터에서는 QDR 속도로 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30520-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="30520-108">이러한 RDMA 기능은 MPI(Message Passing Interface) 응용 프로그램의 확장성 및 성능을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30520-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="30520-109">다음은 RDMA 지원 Windows VM이 Azure RDMA 네트워크에 액세스하기 위한 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="30520-109">Following are requirements for RDMA-capable Windows VMs to access the Azure RDMA network:</span></span> 

* <span data-ttu-id="30520-110">**운영 체제**</span><span class="sxs-lookup"><span data-stu-id="30520-110">**Operating system**</span></span>
  
  <span data-ttu-id="30520-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="30520-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="30520-112">현재 Windows Server 2016은 Azure에서 RDMA 연결을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30520-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="30520-113">**가용성 집합 또는 클라우드 서비스** – RDMA 지원 VM을 동일한 가용성 집합(Azure Resource Manager 배포 모델을 사용하는 경우) 또는 동일한 클라우드 서비스(클래식 배포 모델을 사용하는 경우)에서 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="30520-113">**Availability set or cloud service** – Deploy the RDMA-capable VMs in the same availability set (when you use the Azure Resource Manager deployment model) or the same cloud service (when you use the classic deployment model).</span></span> <span data-ttu-id="30520-114">Azure 배치를 사용하는 경우 RDMA 지원 VM이 동일한 풀에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30520-114">If you use Azure Batch, the RDMA-capable VMs must be in the same pool.</span></span>

* <span data-ttu-id="30520-115">**MPI** - Microsoft MPI(MS-MPI) 2012 R2 이상, Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="30520-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="30520-116">지원되는 MPI 구현은 Microsoft Network Direct 인터페이스를 사용하여 인스턴스 간에 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="30520-116">Supported MPI implementations use the Microsoft Network Direct interface to communicate between instances.</span></span> 

* <span data-ttu-id="30520-117">**RDMA 네트워크 주소 공간** - Azure의 RDMA 네트워크는 주소 공간 172.16.0.0/16을 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="30520-117">**RDMA network address space** - The RDMA network in Azure reserves the address space 172.16.0.0/16.</span></span> <span data-ttu-id="30520-118">Azure 가상 네트워크에 배포된 인스턴스에서 MPI 응용 프로그램을 실행하려면 가상 네트워크 주소 공간이 RDMA 네트워크와 겹치지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30520-118">To run MPI applications on instances deployed in an Azure virtual network, make sure that the virtual network address space does not overlap the RDMA network.</span></span>

* <span data-ttu-id="30520-119">**HpcVmDrivers VM 확장** - RDMA 지원 VM에서는 RDMA 연결용 Windows 네트워크 장치 드라이버를 설치하는 HpcVmDrivers 확장을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30520-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add the HpcVmDrivers extension to install Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="30520-120">(특정 A8 및 A9 인스턴스 배포에서는 HpcVmDrivers 확장이 자동으로 추가됩니다.) VM에 VM 확장을 추가해야 하는 경우 [Azure PowerShell](/powershell/azure/overview) cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30520-120">(In certain deployments of A8 and A9 instances, the HpcVmDrivers extension is added automatically.) To add the VM extension to a VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="30520-121">다음 명령은 *미국 서부* 영역의 *myResourceGroup* 리소스 그룹에 배포된 *myVM*이라는 기존 RDMA 지원 VM에 최신 버전의 1.1 HpcVMDrivers 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="30520-121">The following command installs the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in the resource group named *myResourceGroup* in the *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="30520-122">자세한 내용은 [가상 컴퓨터 확장 및 기능](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30520-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="30520-123">또한 [클래식 배포 모델](classic/manage-extensions.md)에서 배포된 VM의 확장으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30520-123">You can also work with extensions for VMs deployed in the [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="30520-124">HPC Pack 사용</span><span class="sxs-lookup"><span data-stu-id="30520-124">Using HPC Pack</span></span>

<span data-ttu-id="30520-125">Microsoft의 무료 HPC 클러스터 및 작업 관리 솔루션인 [Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)은 Windows 기반 MPI 응용 프로그램 및 기타 HPC 워크로드를 실행하기 위해 Azure에서 계산 클러스터를 만들기 위한 한 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="30520-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to create a compute cluster in Azure to run Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="30520-126">HPC Pack 2012 R2 이상 버전에는 RDMA 지원 VM에 배포할 경우 Azure RDMA 네트워크를 사용하는 MS-MPI에 대한 런타임 환경이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30520-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses the Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="30520-127">기타 크기</span><span class="sxs-lookup"><span data-stu-id="30520-127">Other sizes</span></span>
- [<span data-ttu-id="30520-128">범용</span><span class="sxs-lookup"><span data-stu-id="30520-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="30520-129">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="30520-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="30520-130">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="30520-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="30520-131">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="30520-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="30520-132">GPU에 최적화</span><span class="sxs-lookup"><span data-stu-id="30520-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="30520-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30520-133">Next steps</span></span>

- <span data-ttu-id="30520-134">Windows Server에서 HPC 팩을 통해 계산 집약적 인스턴스를 사용할 때의 검사 목록은 [MPI 응용 프로그램을 실행하기 위해 HPC 팩을 사용하여 Windows RDMA 클러스터 설정](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30520-134">For checklists to use the compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack to run MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="30520-135">Azure Batch에서 MPI 응용 프로그램 실행할 때 계산 집약적 인스턴스를 사용하려면 [다중 인스턴스 작업을 사용하여 Azure Batch에서 MPI(메시지 전달 인터페이스) 응용 프로그램 실행](../../batch/batch-mpi.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30520-135">To use compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks to run Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="30520-136">[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="30520-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




