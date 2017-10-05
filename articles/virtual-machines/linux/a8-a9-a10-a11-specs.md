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
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>Linux용 H 시리즈 및 계산 집약적인 A 시리즈 VM 정보
여기에는 *계산 집약적* 인스턴스로 알려진 최신 Azure H 시리즈 및 이전 A8, A9, A10 및 A11 크기 사용에 대한 일부 고려 사항과 배경 정보가 나와 있습니다. 이 문서는 Linux VM에 대해 이러한 크기를 사용하는 것에 중점을 둡니다. [Windows VM](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서도 사용할 수 있습니다. 

기본 사양의 저장소 용량 및 디스크 세부 정보는 [가상 컴퓨터 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-to-the-rdma-network"></a>RDMA 네트워크에 액세스
다음의 지원되는 Linux HPC 배포판 및 지원되는 MPI 구현 중 하나를 실행하는 RDMA 지원 Linux VM 클러스터를 만들어 Azure RDMA 네트워크를 활용할 수 있습니다. 배포 옵션 및 샘플 구성 단계는 [MPI 응용 프로그램을 실행하도록 Linux RDMA 클러스터 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.

* **배포판** - Azure 마켓플레이스의 RDMA 지원 SLES(SUSE Linux Enterprise Server) 또는 Rogue Wave Software(이전의 OpenLogic) CentOS 기반 HPC 이미지에서 VM을 배포해야 합니다. 다음 Marketplace 이미지는 RDMA 연결을 지원합니다.
  
    * HPC용 SLES 12 SP1, HPC용 SLES 12 SP1(Premium)
    
    * CentOS 기반 7.1 HPC, CentOS 기반 6.5 HPC  
 
        > [!NOTE]
        > H 시리즈 VM의 경우 HPC용 SLES 12 SP1 이미지 또는 CentOS 기반 7.1 HPC 이미지가 권장됩니다.
        >
        > CentOS 기반 HPC 이미지에서 커널 업데이트는 **yum** 구성 파일에서 사용할 수 없습니다. 즉 Linux RDMA 드라이버가 RPM 패키지로 배포되기 때문에 커널이 업데이트되는 경우 드라이버 업데이트가 작동하지 않을 수 있습니다.
        > 
        > 
* **MPI** - Intel MPI Library 5
  
    선택한 마켓플레이스 이미지에 따라 다음과 같이 Intel MPI의 별도 라이선스, 설치 또는 구성이 필요할 수 있습니다. 
  
  * **HPC 이미지의 SLES 12 SP1** - VM에 Intel MPI 패키지를 배포합니다. 다음 명령을 실행하여 설치합니다.

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **CentOS 기반 HPC 이미지** - Intel MPI 5.1은 미리 설치되어 있습니다.  
    
    클러스터된 VM에서 MPI 작업을 실행하기 위해 추가 시스템 구성이 필요합니다. 예를 들어 VM 클러스터에서 계산 노드 간에 트러스트를 설정해야 합니다. 일반적인 설정에 대해서는 [MPI 응용 프로그램을 실행하도록 Linux RDMA 클러스터 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.

## <a name="considerations-for-hpc-pack-and-linux"></a>HPC 팩 및 Linux에 대한 고려 사항
Microsoft의 무료 HPC 클러스터 및 작업 관리 솔루션인 [HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)은 Linux에서 계산 집약적 인스턴스를 사용하기 위한 한 가지 옵션을 제공합니다. HPC 팩의 최신 릴리스는 여러 Linux 배포를 지원하여 Windows Server 헤드 노드를 통해 관리되는 Azure VM에서 배포된 계산 노드에서 실행할 수 있습니다. RDMA 지원 Linux 계산 노드에서 Intel MPI가 실행되는 경우 HPC Pack은 RDMA 네트워크에 액세스하는 Linux MPI 응용 프로그램을 예약하고 실행할 수 있습니다. 시작하려면 [Azure에서 HPC Pack 클러스터의 Linux 계산 노드 시작](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.

## <a name="network-topology-considerations"></a>네트워크 토폴로지 고려 사항
* Azure의 RDMA 지원 Linux VM에서 Eth1은 RDMA 네트워크 트래픽용으로 예약됩니다. Eth1 설정 또는 이 네트워크를 참조하는 구성 파일의 정보를 변경하지 마세요. Eth0은 일반 Azure 네트워크 트래픽용으로 예약됩니다.
* Azure에서 IP over IB(Infiniband)는 지원되지 않습니다. RDMA over IB만 지원됩니다.



## <a name="next-steps"></a>다음 단계
* 계산 집약적 크기의 가용성 및 가격 책정에 대한 세부 정보는 [가상 컴퓨터 가격 책정](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux)을 참조하세요.
* 저장소 용량 및 디스크 세부 정보는 [가상 컴퓨터 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.
* Linux에서 RDMA를 사용하여 계산 집약적 크기를 배포하고 사용하려면 [MPI 응용 프로그램을 실행하기 위해 Linux RDMA 클러스터 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.

