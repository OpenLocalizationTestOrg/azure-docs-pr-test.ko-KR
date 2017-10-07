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
# <a name="high-performance-compute-linux-vm-sizes"></a>고성능 계산 Linux VM 크기

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>RDMA 지원 인스턴스
Hello 계산 집약적인 인스턴스 (H16r, H16mr, A8 및 A9)의 하위 집합에는 원격 직접 메모리 액세스 (RDMA) 연결에 대 한 네트워크 인터페이스를 기능입니다. 이 인터페이스는 또한 toohello 표준 Azure 네트워크 인터페이스 tooother 사용 가능한 VM 크기입니다. 
  
이 인터페이스는 H16r 및 H16mr 가상 컴퓨터에 대 한 FDR 속도 및 A8 및 A9 가상 컴퓨터에 대 한 QDR 속도에서 작동 하는 InfiniBand 네트워크를 통해 RDMA 가능 인스턴스 toocommunicate hello를 허용 합니다. 이러한 RDMA 기능 인터페이스 MPI (Message Passing) 응용 프로그램의 hello 확장성과 성능을 높일 수 있습니다.

다음은 Linux Vm의 경우 RDMA 가능 tooaccess hello Azure RDMA 네트워크에 대 한 요구 사항입니다.
 
* **분포** -Vm에서 RDMA 가능 SUSE Linux Enterprise Server (SLES)를 배포 해야 또는 불량 웨이브 소프트웨어 (이전의 OpenLogic) CentOS 기반 HPC 이미지에서 Azure 마켓플레이스를 환영 합니다. hello 다음 마켓플레이스 이미지 지원 RDMA 연결 합니다.
  
    * HPC용 SLES 12 SP1 또는 HPC용 SLES 12 SP1(Premium)
    
    * CentOS 기반 7.3 HPC, CentOS 기반 7.1 HPC, CentOS 기반 6.8 HPC 또는 CentOS 기반 6.5 HPC  
 
        > [!NOTE]
        > H 시리즈 VM의 경우 HPC용 SLES 12 SP1 이미지 또는 CentOS 기반 7.1 이상 HPC 이미지가 권장됩니다.
        >
        > Hello HPC CentOS 기반 이미지에서 커널 업데이트는 해제 되어 hello **yum** 구성 파일입니다. Hello Linux RDMA 드라이버 배포 되는 RPM 패키지 및 드라이버 업데이트에는 hello 커널 업데이트 되는 경우 작동 하지 않을 수 때문입니다.
        > 
        > 
* **MPI** - Intel MPI Library 5
  
    Hello 마켓플레이스 이미지에 따라을 선택 하면 별도 라이선스를 설치 또는 Intel MPI의 구성이 필요할 수 있습니다. 다음과 같습니다. 
  
  * **HPC 이미지에 대 한 SLES 12 SP1** -Intel MPI 패키지 hello VM에 배포 됩니다. Hello 다음 명령을 실행 하 여 설치 합니다.

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **CentOS 기반 HPC 이미지** - Intel MPI 5.1은 미리 설치되어 있습니다.  
    
    추가 시스템 구성은 클러스터 된 Vm에서 필요한 toorun MPI 작업을 합니다. 예를 들어 tooestablish 필요한 Vm의 클러스터에서 계산 노드 hello 간의 트러스트 합니다. 일반 설정에 대 한 참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="network-topology-considerations"></a>네트워크 토폴로지 고려 사항
* Azure의 RDMA 지원 Linux VM에서 Eth1은 RDMA 네트워크 트래픽용으로 예약됩니다. E t h 1 설정은 되거나 toothis 네트워크를 참조 하는 hello 구성 파일에 대 한 정보를 변경 하지 마십시오. Eth0은 일반 Azure 네트워크 트래픽용으로 예약됩니다.

* Azure에서 IP over IB(Infiniband)는 지원되지 않습니다. RDMA over IB만 지원됩니다.

## <a name="using-hpc-pack"></a>HPC Pack 사용
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft의 무료 HPC 클러스터 및 작업 관리 솔루션에서 Linux 사용 하 여 toouse hello 계산 집약적인 인스턴스를 하나의 옵션입니다. HPC 팩의 최신 릴리스에 hello toorun에 계산 노드 헤드 노드를 Windows Server에서 관리 되는 Azure Vm에 배포 된 여러 Linux 배포판을 지원 합니다. Intel MPI 실행 되는 RDMA 가능 Linux의 계산 노드, 사용 HPC Pack 예약 하 고 hello RDMA 네트워크를 액세스 Linux MPI 응용 프로그램을 실행할 수 있습니다. [Azure에서 HPC 팩 클러스터의 Linux 계산 노드 시작](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.

## <a name="other-sizes"></a>기타 크기
- [범용](sizes-general.md)
- [Compute에 최적화](sizes-compute.md)
- [메모리에 최적화](sizes-memory.md)
- [Storage에 최적화](sizes-storage.md)
- [GPU](../windows/sizes-gpu.md)


## <a name="next-steps"></a>다음 단계

- 배포 하 고 계산 집약적인 크기를 사용 하 여 linux에서 RDMA와 시작 tooget 참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

- [ACU(Azure Compute 단위)](acu.md)가 Azure SKU 간의 Compute 성능을 비교하는 데 어떻게 도움을 줄 수 있는지 알아봅니다.




