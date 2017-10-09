---
title: "Windows 용 드라이버 설치 aaaAzure N 시리즈 | Microsoft Docs"
description: "어떻게 tooset NVIDIA GPU 드라이버를 Windows Azure에서 실행 되는 N 시리즈 Vm 구성"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="dc39f-103">Windows Server가 실행되는 N 시리즈 VM의 GPU 드라이버 설정</span><span class="sxs-lookup"><span data-stu-id="dc39f-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="dc39f-104">N 시리즈 Azure의 hello GPU 기능을 활용 tootake Windows Server 2016 또는 Windows Server 2012 r 2를 실행 하는 Vm 설치 NVIDIA 그래픽 드라이버를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="dc39f-105">이 문서에서는 N 시리즈 VM을 배포한 후의 드라이버 설치 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="dc39f-106">[Linux VM](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 대한 드라이버 설치 정보도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="dc39f-107">기본 사양, 저장소 용량 및 디스크 세부 정보는 [GPU Windows VM 크기](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc39f-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="dc39f-108">드라이버 설치</span><span class="sxs-lookup"><span data-stu-id="dc39f-108">Driver installation</span></span>

1. <span data-ttu-id="dc39f-109">원격 데스크톱 tooeach N 시리즈 VM으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-109">Connect by Remote Desktop tooeach N-series VM.</span></span>

2. <span data-ttu-id="dc39f-110">다운로드, 추출 및 Windows 운영 체제에 대 한 지원 hello 드라이버를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-110">Download, extract, and install hello supported driver for your Windows operating system.</span></span>

<span data-ttu-id="dc39f-111">Azure NV VM에서는 드라이버 설치 후 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="dc39f-112">NC Vm에서는 다시 시작 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="dc39f-113">드라이버 설치 확인</span><span class="sxs-lookup"><span data-stu-id="dc39f-113">Verify driver installation</span></span>

<span data-ttu-id="dc39f-114">장치 관리자에서 드라이버 설치를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="dc39f-115">hello 다음 예제에서는 성공적으로 hello 테슬라 K80 카드 구성 NC Azure VM에서</span><span class="sxs-lookup"><span data-stu-id="dc39f-115">hello following example shows successful configuration of hello Tesla K80 card on an Azure NC VM.</span></span>

![GPU 드라이버 속성](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="dc39f-117">hello 실행 tooquery hello GPU 장치 상태 [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) 명령줄 유틸리티 hello 드라이버와 함께 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-117">tooquery hello GPU device state, run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span>

1. <span data-ttu-id="dc39f-118">명령 프롬프트를 열고 toohello 변경 **C:\Program Files\NVIDIA Corporation\NVSMI** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-118">Open a command prompt and change toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="dc39f-119">**nvidia-smi**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="dc39f-120">Hello 드라이버가 설치 되어 있으면 출력 유사한 toobelow 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-120">If hello driver is installed you will see output similar toobelow.</span></span> <span data-ttu-id="dc39f-121">**GPU Util** 표시 **0%** hello VM에서 GPU 작업 부하를 현재 실행 중인 경우가 아니면 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on hello VM.</span></span>

![NVIDIA 장치 상태](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="dc39f-123">NC24r VM에 대한 RDMA 네트워크</span><span class="sxs-lookup"><span data-stu-id="dc39f-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="dc39f-124">Hello에 배포 된 NC24r Vm에서 RDMA 네트워크 연결을 사용할 수 있습니다 동일한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-124">RDMA network connectivity can be enabled on NC24r VMs deployed in hello same availability set.</span></span> <span data-ttu-id="dc39f-125">hello HpcVmDrivers 확장은 RDMA 연결을 사용할 수 있는 tooinstall Windows 네트워크 장치 드라이버 추가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-125">hello HpcVmDrivers extension must be added tooinstall Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="dc39f-126">tooadd hello VM 확장 tooan NC24r VM을 사용 하 여 [Azure PowerShell](/powershell/azure/overview) Azure 리소스 관리자에 대 한 cmdlet입니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-126">tooadd hello VM extension tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="dc39f-127">현재, Windows Server 2012 R2만 NC24r Vm에서 hello RDMA 네트워크를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-127">Currently, only Windows Server 2012 R2 supports hello RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="dc39f-128">hello 미국 서 부 지역에서 myVM 이라는 tooinstall hello 최신 버전 1.1 HpcVMDrivers 확장 RDMA 가능 기존 VM에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-128">tooinstall hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in hello West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="dc39f-129">자세한 내용은 [Windows용 가상 컴퓨터 확장 및 기능](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc39f-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="dc39f-130">hello RDMA 네트워크와 실행 중인 응용 프로그램에 대 한 인터페이스 MPI (Message Passing) 트래픽을 지원 하므로 [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) 또는 Intel MPI 5.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-130">hello RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="dc39f-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dc39f-131">Next steps</span></span>

* <span data-ttu-id="dc39f-132">Hello N 시리즈 Vm에서 NVIDIA Gpu hello에 대 한 자세한 내용은 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-132">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="dc39f-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html)(Azure NC VM용)</span><span class="sxs-lookup"><span data-stu-id="dc39f-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="dc39f-134">[NVIDIA 테슬라 M60](http://www.nvidia.com/object/tesla-m60.html) (Azure NV VM 용)</span><span class="sxs-lookup"><span data-stu-id="dc39f-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="dc39f-135">Hello NVIDIA 테슬라 Gpu에 대 한 GPU accelerated 응용 프로그램 개발자도 다운로드 하 여 설치에 대 한 hello CUDA Toolkit 8 [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) 또는 [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-135">Developers building GPU-accelerated applications for hello NVIDIA Tesla GPUs can also download and install hello CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="dc39f-136">자세한 내용은 참조 hello [CUDA 설치 가이드](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc39f-136">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


