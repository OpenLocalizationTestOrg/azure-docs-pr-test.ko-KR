---
title: "aaaAzure Windows VM 크기-HPC | Microsoft Docs"
description: "Windows 고성능 컴퓨팅 Azure의 가상 컴퓨터에 사용할 수 있는 hello 다른 크기를 나열 합니다."
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
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="cb348-103">고성능 계산 VM 크기</span><span class="sxs-lookup"><span data-stu-id="cb348-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="cb348-104">RDMA 지원 인스턴스</span><span class="sxs-lookup"><span data-stu-id="cb348-104">RDMA-capable instances</span></span>
<span data-ttu-id="cb348-105">Hello 계산 집약적인 인스턴스 (H16r, H16mr, A8 및 A9)의 하위 집합에는 원격 직접 메모리 액세스 (RDMA) 연결에 대 한 네트워크 인터페이스를 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="cb348-106">이 인터페이스는 또한 toohello 표준 Azure 네트워크 인터페이스 tooother 사용 가능한 VM 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="cb348-107">이 인터페이스는 H16r 및 H16mr 가상 컴퓨터에 대 한 FDR 속도 및 A8 및 A9 가상 컴퓨터에 대 한 QDR 속도에서 작동 하는 InfiniBand 네트워크를 통해 RDMA 가능 인스턴스 toocommunicate hello를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="cb348-108">이러한 RDMA 기능 인터페이스 MPI (Message Passing) 응용 프로그램의 hello 확장성과 성능을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="cb348-109">다음은 Windows Vm을 RDMA 가능 tooaccess hello Azure RDMA 네트워크에 대 한 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-109">Following are requirements for RDMA-capable Windows VMs tooaccess hello Azure RDMA network:</span></span> 

* <span data-ttu-id="cb348-110">**운영 체제**</span><span class="sxs-lookup"><span data-stu-id="cb348-110">**Operating system**</span></span>
  
  <span data-ttu-id="cb348-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="cb348-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cb348-112">현재 Windows Server 2016은 Azure에서 RDMA 연결을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="cb348-113">**가용성 설정 또는 클라우드 서비스** – 배포 hello RDMA 가능 Vm에 hello 동일한 가용성 집합 (hello Azure 리소스 관리자 배포 모델을 사용 하는 경우) 하는 경우 또는 (hello 클래식 배포 모델을 사용 하는 경우) 하는 경우 동일한 클라우드 서비스를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-113">**Availability set or cloud service** – Deploy hello RDMA-capable VMs in hello same availability set (when you use hello Azure Resource Manager deployment model) or hello same cloud service (when you use hello classic deployment model).</span></span> <span data-ttu-id="cb348-114">RDMA 가능 Vm hello hello에 있어야 Azure 일괄 처리를 사용 하는 경우 동일한 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-114">If you use Azure Batch, hello RDMA-capable VMs must be in hello same pool.</span></span>

* <span data-ttu-id="cb348-115">**MPI** - Microsoft MPI(MS-MPI) 2012 R2 이상, Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="cb348-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="cb348-116">지원 되는 MPI 구현 인스턴스 간에 Microsoft Network Direct 인터페이스 toocommunicate hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-116">Supported MPI implementations use hello Microsoft Network Direct interface toocommunicate between instances.</span></span> 

* <span data-ttu-id="cb348-117">**RDMA 네트워크 주소 공간** -Azure의 hello RDMA 네트워크 주소 공간 172.16.0.0/16 hello를 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-117">**RDMA network address space** - hello RDMA network in Azure reserves hello address space 172.16.0.0/16.</span></span> <span data-ttu-id="cb348-118">Azure 가상 네트워크에 배포 된 인스턴스에서 MPI 응용 프로그램 toorun hello 가상 네트워크 주소 공간 hello RDMA 네트워크에 겹치지 않는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-118">toorun MPI applications on instances deployed in an Azure virtual network, make sure that hello virtual network address space does not overlap hello RDMA network.</span></span>

* <span data-ttu-id="cb348-119">**HpcVmDrivers VM 확장** -RDMA 가능 Vm에서 hello HpcVmDrivers 확장 tooinstall Windows 네트워크 장치 드라이버 RDMA 연결에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add hello HpcVmDrivers extension tooinstall Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="cb348-120">(A8 및 A9 인스턴스의 특정 배포에서는 HpcVmDrivers 확장 hello 자동으로 추가 됩니다.) 사용할 수 있습니다 tooadd hello VM 확장 tooa VM [Azure PowerShell](/powershell/azure/overview) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cb348-120">(In certain deployments of A8 and A9 instances, hello HpcVmDrivers extension is added automatically.) tooadd hello VM extension tooa VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="cb348-121">다음 명령을 설치 hello 라는 기존 RDMA 가능 VM에 최신 버전 1.1 HpcVMDrivers 확장 hello *myVM* 이라는 hello 리소스 그룹에 배포 된 *myResourceGroup* hello 에서 *미국 서 부* 영역:</span><span class="sxs-lookup"><span data-stu-id="cb348-121">hello following command installs hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in hello resource group named *myResourceGroup* in hello *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="cb348-122">자세한 내용은 [가상 컴퓨터 확장 및 기능](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb348-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="cb348-123">Hello에 배포 된 Vm에 대 한 확장 작업할 수도 [클래식 배포 모델](classic/manage-extensions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-123">You can also work with extensions for VMs deployed in hello [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="cb348-124">HPC Pack 사용</span><span class="sxs-lookup"><span data-stu-id="cb348-124">Using HPC Pack</span></span>

<span data-ttu-id="cb348-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft의 무료 HPC 클러스터 및 작업 관리 솔루션을 toocreate Azure toorun MPI Windows 기반 응용 프로그램 및 기타 HPC 작업에서 계산 클러스터에 하나의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toocreate a compute cluster in Azure toorun Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="cb348-126">HPC Pack 2012 R2 및 이후 버전 MS-MPI RDMA 가능 Vm에 배포할 때 hello Azure RDMA 네트워크를 사용 하는 런타임 환경을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses hello Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="cb348-127">기타 크기</span><span class="sxs-lookup"><span data-stu-id="cb348-127">Other sizes</span></span>
- [<span data-ttu-id="cb348-128">범용</span><span class="sxs-lookup"><span data-stu-id="cb348-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="cb348-129">Compute에 최적화</span><span class="sxs-lookup"><span data-stu-id="cb348-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="cb348-130">메모리에 최적화</span><span class="sxs-lookup"><span data-stu-id="cb348-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="cb348-131">Storage에 최적화</span><span class="sxs-lookup"><span data-stu-id="cb348-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="cb348-132">GPU에 최적화</span><span class="sxs-lookup"><span data-stu-id="cb348-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="cb348-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb348-133">Next steps</span></span>

- <span data-ttu-id="cb348-134">검사 목록 toouse hello 계산 집약적인 인스턴스 Windows 서버에서 HPC Pack을 사용한 참조 [HPC Pack toorun MPI 응용 프로그램을 사용 하 여 Windows RDMA 클러스터를 설정](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-134">For checklists toouse hello compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack toorun MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="cb348-135">toouse 계산 집약적인 인스턴스에서 MPI 응용 프로그램에서 Azure 일괄 처리 실행 될 때 참조 [toorun 인터페이스 MPI (Message Passing) 응용 프로그램을 Azure 일괄 처리의 작업을 사용 하 여 다중 인스턴스](../../batch/batch-mpi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-135">toouse compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="cb348-136">[ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cb348-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




