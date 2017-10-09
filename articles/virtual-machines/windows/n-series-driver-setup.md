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
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>Windows Server가 실행되는 N 시리즈 VM의 GPU 드라이버 설정
N 시리즈 Azure의 hello GPU 기능을 활용 tootake Windows Server 2016 또는 Windows Server 2012 r 2를 실행 하는 Vm 설치 NVIDIA 그래픽 드라이버를 지원 합니다. 이 문서에서는 N 시리즈 VM을 배포한 후의 드라이버 설치 단계를 제공합니다. [Linux VM](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에 대한 드라이버 설치 정보도 사용할 수 있습니다.

기본 사양, 저장소 용량 및 디스크 세부 정보는 [GPU Windows VM 크기](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요. 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>드라이버 설치

1. 원격 데스크톱 tooeach N 시리즈 VM으로 연결 합니다.

2. 다운로드, 추출 및 Windows 운영 체제에 대 한 지원 hello 드라이버를 설치 합니다.

Azure NV VM에서는 드라이버 설치 후 다시 시작해야 합니다. NC Vm에서는 다시 시작 필요하지 않습니다.

## <a name="verify-driver-installation"></a>드라이버 설치 확인

장치 관리자에서 드라이버 설치를 확인할 수 있습니다. hello 다음 예제에서는 성공적으로 hello 테슬라 K80 카드 구성 NC Azure VM에서

![GPU 드라이버 속성](./media/n-series-driver-setup/GPU_driver_properties.png)

hello 실행 tooquery hello GPU 장치 상태 [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) 명령줄 유틸리티 hello 드라이버와 함께 설치 됩니다.

1. 명령 프롬프트를 열고 toohello 변경 **C:\Program Files\NVIDIA Corporation\NVSMI** 디렉터리입니다.

2. **nvidia-smi**를 실행합니다. Hello 드라이버가 설치 되어 있으면 출력 유사한 toobelow 표시 됩니다. **GPU Util** 표시 **0%** hello VM에서 GPU 작업 부하를 현재 실행 중인 경우가 아니면 합니다.

![NVIDIA 장치 상태](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>NC24r VM에 대한 RDMA 네트워크

Hello에 배포 된 NC24r Vm에서 RDMA 네트워크 연결을 사용할 수 있습니다 동일한 가용성 집합입니다. hello HpcVmDrivers 확장은 RDMA 연결을 사용할 수 있는 tooinstall Windows 네트워크 장치 드라이버 추가 되어야 합니다. tooadd hello VM 확장 tooan NC24r VM을 사용 하 여 [Azure PowerShell](/powershell/azure/overview) Azure 리소스 관리자에 대 한 cmdlet입니다.

> [!NOTE]
> 현재, Windows Server 2012 R2만 NC24r Vm에서 hello RDMA 네트워크를 지원합니다.
> 

hello 미국 서 부 지역에서 myVM 이라는 tooinstall hello 최신 버전 1.1 HpcVMDrivers 확장 RDMA 가능 기존 VM에 입력 합니다.
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  자세한 내용은 [Windows용 가상 컴퓨터 확장 및 기능](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.

hello RDMA 네트워크와 실행 중인 응용 프로그램에 대 한 인터페이스 MPI (Message Passing) 트래픽을 지원 하므로 [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) 또는 Intel MPI 5.x 합니다. 


## <a name="next-steps"></a>다음 단계

* Hello N 시리즈 Vm에서 NVIDIA Gpu hello에 대 한 자세한 내용은 다음을 참조 합니다.
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html)(Azure NC VM용)
    * [NVIDIA 테슬라 M60](http://www.nvidia.com/object/tesla-m60.html) (Azure NV VM 용)

* Hello NVIDIA 테슬라 Gpu에 대 한 GPU accelerated 응용 프로그램 개발자도 다운로드 하 여 설치에 대 한 hello CUDA Toolkit 8 [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) 또는 [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe)합니다. 자세한 내용은 참조 hello [CUDA 설치 가이드](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi)합니다.


