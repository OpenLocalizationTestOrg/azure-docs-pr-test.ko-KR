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
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>Linux용 H 시리즈 및 계산 집약적인 A 시리즈 VM 정보
배경 정보 및 사용에 대 한 몇 가지 고려 사항 최신 Azure H 시리즈 hello 및 이전 A8, A9, A10 및 A11 크기 라고도 hello *계산 집약적인* 인스턴스. 이 문서는 Linux VM에 대해 이러한 크기를 사용하는 것에 중점을 둡니다. [Windows VM](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서도 사용할 수 있습니다. 

기본 사양의 저장소 용량 및 디스크 세부 정보는 [가상 컴퓨터 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a>Toohello RDMA 네트워크 액세스
Hello 지원 되는 Linux HPC 분포와 hello Azure RDMA 네트워크의 지원 되는 MPI 구현 tootake 이점은 다음 중 하나를 실행 하는 RDMA 가능 Linux Vm의 클러스터를 만들 수 있습니다. 참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 배포 옵션 및 샘플 구성 단계에 대 한 합니다.

* **분포** -Vm에서 RDMA 가능 SUSE Linux Enterprise Server (SLES)를 배포 해야 또는 불량 웨이브 소프트웨어 (이전의 OpenLogic) CentOS 기반 HPC 이미지에서 Azure 마켓플레이스를 환영 합니다. hello 다음 마켓플레이스 이미지 지원 RDMA 연결 합니다.
  
    * HPC용 SLES 12 SP1, HPC용 SLES 12 SP1(Premium)
    
    * CentOS 기반 7.1 HPC, CentOS 기반 6.5 HPC  
 
        > [!NOTE]
        > H 시리즈 VM의 경우 HPC용 SLES 12 SP1 이미지 또는 CentOS 기반 7.1 HPC 이미지가 권장됩니다.
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
    
    추가 시스템 구성은 클러스터 된 Vm에서 필요한 toorun MPI 작업을 합니다. 예를 들어 tooestablish 필요한 Vm의 클러스터에서 계산 노드 hello 간의 트러스트 합니다. 일반 설정에 대 한 참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

## <a name="considerations-for-hpc-pack-and-linux"></a>HPC 팩 및 Linux에 대한 고려 사항
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft의 무료 HPC 클러스터 및 작업 관리 솔루션을와 Linux toouse hello 계산 집약적인 인스턴스를 하나의 옵션을 제공 합니다. HPC 팩의 최신 릴리스에 hello toorun에 계산 노드 헤드 노드를 Windows Server에서 관리 되는 Azure Vm에 배포 된 여러 Linux 배포판을 지원 합니다. Intel MPI 실행 되는 RDMA 가능 Linux의 계산 노드, 사용 HPC Pack 예약 하 고 hello RDMA 네트워크를 액세스 Linux MPI 응용 프로그램을 실행할 수 있습니다. 시작 tooget 참조 [Azure에서 HPC Pack 클러스터에서 계산 노드 Linux 시작](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

## <a name="network-topology-considerations"></a>네트워크 토폴로지 고려 사항
* Azure의 RDMA 지원 Linux VM에서 Eth1은 RDMA 네트워크 트래픽용으로 예약됩니다. E t h 1 설정은 되거나 toothis 네트워크를 참조 하는 hello 구성 파일에 대 한 정보를 변경 하지 마십시오. Eth0은 일반 Azure 네트워크 트래픽용으로 예약됩니다.
* Azure에서 IP over IB(Infiniband)는 지원되지 않습니다. RDMA over IB만 지원됩니다.



## <a name="next-steps"></a>다음 단계
* 가용성 및 hello 계산 집약적인 크기의 가격 책정에 대 한 세부 정보를 참조 하십시오. [가상 컴퓨터 가격](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux)합니다.
* 저장소 용량 및 디스크 세부 정보는 [가상 컴퓨터 크기](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.
* 배포 하 고 계산 집약적인 크기를 사용 하 여 linux에서 RDMA와 시작 tooget 참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

