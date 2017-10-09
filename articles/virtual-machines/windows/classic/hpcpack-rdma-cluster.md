---
title: "Windows RDMA 클러스터 toorun MPI 응용 프로그램을 aaaSet | Microsoft Docs"
description: "어떻게 toocreate H16r, H16mr, A8 또는 A9 Vm toouse 크기를 사용 하 여 Windows HPC 팩 클러스터 hello Azure RDMA 네트워크 toorun MPI 응용 프로그램에 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 7d9f5bc8-012f-48dd-b290-db81c7592215
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 23bc8740dbd05a7c7ab3f998489a41d0df4520a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-rdma-cluster-with-hpc-pack-toorun-mpi-applications"></a>HPC Pack toorun MPI 응용 프로그램을 사용 하 여 Windows RDMA 클러스터 설정
사용 하 여 Azure에서 Windows RDMA 클러스터 설정 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) 및 [VM 크기를 계산 하는 고성능](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun 병렬 인터페이스 MPI (Message Passing) 응용 프로그램입니다. HPC 팩 클러스터에서 RDMA 지원, Windows Server 기반 노드를 설정하는 경우 MPI 응용 프로그램은 Azure에서 RDMA(원격 직접 메모리 액세스) 기술을 기반으로 하는 낮은 대기 시간 및 높은 처리량의 네트워크에서 효율적으로 통신합니다.

Linux Vm의 경우 해당 액세스 hello Azure RDMA 네트워크에 toorun MPI 작업 참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](../../linux/classic/rdma-cluster.md)합니다.

## <a name="hpc-pack-cluster-deployment-options"></a>HPC 팩 클러스터 배포 옵션
Microsoft HPC Pack는 없는 추가 비용 toocreate에 HPC 클러스터 온-프레미스 제공 되거나 Azure toorun Windows 또는 Linux HPC 응용 프로그램에는 도구입니다. HPC Pack hello 메시지 전달 인터페이스 Windows 용 MS-MPI ()의 hello Microsoft 구현 위한 런타임 환경이 포함 되어 있습니다. 지원 되는 Windows Server 운영 체제를 실행 하는 RDMA 가능 인스턴스에서만 사용 되므로, HPC 팩 hello Azure RDMA 네트워크를 액세스 효율적인 옵션 toorun Windows MPI 응용 프로그램 제공 합니다. 

이 문서는 두 가지 시나리오를 소개 하 고 toodetailed 지침 tooset Microsoft HPC Pack을 사용한 Windows RDMA 클러스터를 연결 합니다. 

* 시나리오 1. 계산 집약적 작업자 역할 인스턴스 배포(PaaS)
* 시나리오 2. 계산 집약적 VM에 계산 노드 배포(IaaS)

Windows 일반 전제 조건 toouse 계산 집약적인 인스턴스를 참조 하십시오. [VM 크기를 계산 하는 고성능](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

## <a name="scenario-1-deploy-compute-intensive-worker-role-instances-paas"></a>시나리오 1: 계산 집약적 작업자 역할 인스턴스 배포(PaaS)
기존 HPC 팩 클러스터에서 클라우드 서비스(PaaS)에서 실행 중인 Azure 작업자 역할 인스턴스(Azure 노드)에 추가 계산 리소스를 추가합니다. HPC Pack에서 "버스트 tooAzure"이 라고도 하는이 기능을 hello 작업자 역할 인스턴스에 대 한 크기의 범위를 지원 합니다. Azure 노드를 hello 추가 때 hello RDMA 가능 크기 중 하나를 지정 합니다.

다음은 단계 및 고려 사항은 tooburst tooRDMA 가능 Azure 인스턴스를 기존 (일반적으로 온-프레미스) 클러스터입니다. 유사한 프로시저 tooadd 작업자 역할 인스턴스 tooan HPC Pack 헤드 노드는 Azure VM에 배포 된를 사용 합니다.

> [!NOTE]
> HPC Pack을 사용한 자습서 tooburst tooAzure를 참조 하십시오. [HPC Pack을 사용한 하이브리드 클러스터 설정](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)합니다. Note 특히 tooRDMA 가능 Azure 노드를 적용 하는 단계를 수행 하는 hello hello 고려해 야 합니다.
> 
> 

![버스트 tooAzure][burst]

### <a name="steps"></a>단계
1. **HPC 팩 2012 R2 헤드 노드 배포 및 구성**
   
    Hello에서 hello 최신 HPC Pack 설치 패키지를 다운로드 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=49922)합니다. 참조 된 Azure 버스트 배포에 대 한 요구 사항 및 지침은 tooprepare [Microsoft HPC Pack을 사용한 tooAzure 작업자 인스턴스 버스트](https://technet.microsoft.com/library/gg481749.aspx)합니다.
2. **Hello Azure 구독에에서 관리 인증서를 구성 합니다.**
   
    Hello 헤드 노드와 Azure 간의 인증서 toosecure hello 연결을 구성 합니다. 옵션 및 절차에 대 한 참조 [시나리오 tooConfigure hello HPC Pack 용 Azure 관리 인증서](http://technet.microsoft.com/library/gg481759.aspx)합니다. 테스트 배포에 대 한 HPC Pack 설치 기본 Microsoft HPC Azure 관리 인증서 tooyour Azure 구독을 신속 하 게 업로드할 수 있습니다.
3. **새 클라우드 서비스 및 저장소 계정 만들기**
   
    RDMA 가능 hello 인스턴스를 사용할 수 있는 지역에 배포 hello에 대 한 클라우드 서비스 및 저장소 계정을 Azure 포털 toocreate hello를 사용 합니다.
4. **Azure 노드 템플릿 만들기**
   
    HPC 클러스터 관리자에서 hello 노드 템플릿 만들기 마법사를 사용 합니다. 단계를 참조 하십시오. [Azure 노드 템플릿 만들기](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Templ) "단계 tooDeploy Microsoft HPC Pack 사용한 Azure 노드"에 있습니다.
   
    초기 테스트에 대 한 hello 템플릿에서 수동 가용성 정책을 구성 하는 것이 좋습니다.
5. **Toohello 클러스터 노드 추가**
   
    HPC 클러스터 관리자에서 노드 추가 마법사 hello를 사용 합니다. 자세한 내용은 참조 [Azure 노드 추가 toohello Windows HPC 클러스터](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Add)합니다.
   
    Hello 노드의 hello 크기를 지정할 때는 hello RDMA 가능 인스턴스 크기 중 하나를 선택 합니다.
   
   > [!NOTE]
   > 각 버스트 tooAzure hello 계산 집약적인 인스턴스 배포에서 HPC Pack을 자동으로 최소 두 개의 RDMA 가능 인스턴스 (예: A8) 프록시 노드로 배포 또한 toohello Azure 작업자 역할 인스턴스를 지정 합니다. hello 프록시 노드 toohello 구독 할당 되 고 hello Azure 작업자 역할 인스턴스와 함께 요금이 코어를 사용 합니다.
   > 
   > 
6. **(프로 비전) hello 노드를 시작 하 고 직접 온라인 toorun 작업**
   
    Hello 노드를 선택 하 고 hello를 사용 하 여 **시작** HPC 클러스터 관리자에서 작업 합니다. 프로 비전 완료 되 면 hello 노드를 선택 하 고 hello를 사용 하 여 **온라인 상태로 만들기** HPC 클러스터 관리자에서 작업 합니다. hello 노드는 준비 toorun 작업입니다.
7. **Toohello 클러스터 작업 제출**
   
   HPC Pack 작업 제출 도구 toorun 클러스터 작업을 사용 합니다. [Microsoft HPC 팩: 작업 관리](http://technet.microsoft.com/library/jj899585.aspx)를 참조하세요.
8. **중지 (프로 비전 해제) hello 노드**
   
   작업 실행이 완료 되 면 hello 노드를 오프 라인 및 hello를 사용 하 여 **중지** HPC 클러스터 관리자에서 작업 합니다.

## <a name="scenario-2-deploy-compute-nodes-in-compute-intensive-vms-iaas"></a>시나리오 2: 계산 집약적 VM에 계산 노드 배포(IaaS)
이 시나리오에서는 hello HPC Pack 헤드 노드 및 클러스터 계산 노드 Vm에 Azure 가상 네트워크에 배포 합니다. HPC Pack은 자동 배포 스크립트 및 Azure 빠른 시작 템플릿을 포함하여 다양한 [Azure VM의 배포 옵션](../../linux/hpcpack-cluster-options.md)을 제공합니다. 예를 들어 hello 다음 고려 사항 및 단계를 안내해 toouse hello [HPC Pack IaaS 배포 스크립트](hpcpack-cluster-powershell-script.md) Azure의 HPC Pack 2012 R2 클러스터의 hello 배포를 자동화 하 합니다.

![Azure VM의 클러스터][iaas]

### <a name="steps"></a>단계
1. **클러스터 헤드 노드를 만들고 클라이언트 컴퓨터에서 hello HPC Pack IaaS 배포 스크립트를 실행 하 여 계산 노드 Vm**
   
    Hello에서 hello HPC Pack IaaS 배포 스크립트 패키지를 다운로드 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=49922)합니다.
   
    tooprepare hello 클라이언트 컴퓨터 hello 스크립트 구성 파일을 만들고 실행된 hello 스크립트, 참조 [hello HPC Pack IaaS 배포 스크립트는 HPC 클러스터 만들기](hpcpack-cluster-powershell-script.md)합니다. 
   
    추가 고려 사항에 따라 참고 hello toodeploy RDMA 가능 계산 노드:
   
   * **가상 네트워크**: toouse ´ ï ´ 원하는 어떤 hello RDMA 가능 인스턴스 크기의에서 지역에 새 가상 네트워크를 지정 합니다.
   * **Windows Server 운영 체제**: toosupport RDMA 연결은 hello 계산 노드 Vm에 대 한 Windows Server 2012 R2 또는 Windows Server 2012 운영 체제를 지정 합니다.
   * **클라우드 서비스**: 헤드 노드를 한 클라우드 서비스에 배포하고 계산 노드를 다른 클라우드 서비스에 배포하는 것이 좋습니다.
   * **헤드 노드 크기**:이 시나리오를 고려해 야의 크기 이상 A4 (매우 큼) hello 헤드 노드에 대 한 합니다.
   * **HpcVmDrivers 확장**: hello 배포 스크립트 hello Azure VM 에이전트 및 HpcVmDrivers 확장 hello 자동으로 설치 Windows Server 운영 체제와 크기 A8 또는 A9 계산 노드를 배포 합니다. HpcVmDrivers는 toohello RDMA 네트워크에 연결할 수 있도록 hello 계산 노드 Vm에 드라이버를 설치 합니다. RDMA 가능 H 시리즈 Vm에 HpcVmDrivers 확장 hello를 수동으로 설치 해야 합니다. [고성능 계산 VM 크기](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.
   * **클러스터 네트워크 구성**: hello 배포 스크립트를 자동으로 hello HPC Pack 클러스터 토폴로지 5 (hello 엔터프라이즈 네트워크의 모든 노드)를 설정 합니다. 이 토폴로지는 VM에서의 모든 HPC Pack 클러스터 배포에 필요합니다. 나중에 hello 클러스터 네트워크 토폴로지를 변경 하지 마십시오.
2. **Hello 계산 노드 온라인 toorun 작업 가져오기**
   
    Hello 노드를 선택 하 고 hello를 사용 하 여 **온라인 상태로 만들기** HPC 클러스터 관리자에서 작업 합니다. hello 노드는 준비 toorun 작업입니다.
3. **Toohello 클러스터 작업 제출**
   
    Toohello 헤드 노드 toosubmit 작업을 연결 하거나이 온-프레미스 컴퓨터 toodo를 설정 합니다. 자세한 내용은 참조 [Azure에서 HPC 작업 제출 tooan 클러스터](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
4. **Take hello 노드가 오프 라인 및 중지 (할당 취소)에**
   
    작업 실행이 완료 되 면 HPC 클러스터 관리자에서 hello 노드를 오프 라인으로 수행 합니다. 그런 다음 Azure 관리 도구 tooshut를 사용 하 여 다운 합니다.

## <a name="run-mpi-applications-on-hello-cluster"></a>Hello 클러스터에서 MPI 응용 프로그램을 실행 합니다.
### <a name="example-run-mpipingpong-on-an-hpc-pack-cluster"></a>예: HPC 팩 클러스터에서 mpipingpong 실행
RDMA 가능 hello 인스턴스를 실행 하는 HPC Pack 배포 tooverify HPC 팩 hello **mpipingpong** hello 클러스터에서 명령을 합니다. **mpipingpong** 쌍을 이루는 노드 간에 데이터 패킷을 반복적으로 보내는 toocalculate 대기 시간 및 처리량을 측정 하 고 hello RDMA 사용 응용 프로그램 네트워크에 대 한 통계입니다. 이 예제에서는 MPI 작업을 실행 하기 위한 일반적인 패턴을 보여 줍니다 (이 경우 **mpipingpong**) hello 클러스터를 사용 하 여 **mpiexec** 명령입니다.

이 예제에서는 "tooAzure 전환" 구성에 Azure 노드를 추가 가정 ([시나리오 1](#scenario-1.-deploy-compute-intensive-worker-role-instances-\(PaaS\) in this article)합니다. Azure Vm의 클러스터에 HPC Pack을 배포 하는 경우 toomodify hello 명령 구문을 toospecify 다른 노드 그룹 필요 하 고 추가 환경 변수 toodirect 네트워크 트래픽 toohello RDMA 네트워크를 설정 합니다.

hello 클러스터에서 mpipingpong toorun:

1. Hello 헤드 노드 또는 올바르게 구성 된 클라이언트 컴퓨터에서 명령 프롬프트를 엽니다.
2. 다음 명령은 toosubmit 작은 패킷 크기와 많은 반복 작업이 toorun mpipingpong 형식 hello 4 개 노드 중 Azure 전환 배포에서 노드 쌍 간의 tooestimate 대기 시간:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 1:100000 -op -s nul
    ```
   
    hello 명령은 제출 된 hello 작업의 hello ID를 반환 합니다.
   
    Azure Vm에 배포 된 hello HPC Pack 클러스터를 배포한 경우 포함 하는 노드 그룹 계산 노드 Vm에는 단일 클라우드 서비스 배포를 지정 하 고 hello 수정 **mpiexec** 명령은 다음과 같습니다.
   
    ```Command
    job submit /nodegroup:vmcomputenodes /numnodes:4 mpiexec -c 1 -affinity -env MSMPI_DISABLE_SOCK 1 -env MSMPI_PRECONNECT all -env MPICH_NETMASK 172.16.0.0/255.255.0.0 mpipingpong -p 1:100000 -op -s nul
    ```
3. Hello 작업이 완료 되 면 tooview hello 출력에 (이 경우 hello 작업의 작업 1의 hello 출력)를 따르는 형식 hello
   
    ```Command
    task view <JobID>.1
    ```
   
    여기서 &lt; *JobID* &gt; hello 제출 된 hello 작업 ID입니다.
   
    hello 출력 toohello 다음과 유사한 대기 시간 결과 포함합니다.
   
    ![핑퐁 대기 시간][pingpong1]
4. Azure의 쌍 간의 처리량 tooestimate 버스트 노드, 형식 hello 다음 명령은 toosubmit 작업 toorun **mpipingpong** 큰 패킷 크기와를 몇 차례 반복:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 4000000:1000 -op -s nul
    ```
   
    hello 명령은 제출 된 hello 작업의 hello ID를 반환 합니다.
   
    Azure Vm에 배포 된 HPC Pack 클러스터에서 2 단계에서 설명 된 대로 hello 명령을 수정 합니다.
5. Hello 작업이 완료 되 면 tooview hello 형식 hello 뒤에 (이 경우 hello 작업의 작업 1의 hello 출력)를 출력 합니다.
   
    ```Command
    task view <JobID>.1
    ```
   
   hello 출력 toohello 다음과를 유사한 처리량 결과가 포함 됩니다.
   
   ![핑퐁 처리량][pingpong2]

### <a name="mpi-application-considerations"></a>MPI 응용 프로그램 고려 사항
다음은 Azure에서 HPC Pack을 사용하여 MPI 응용 프로그램을 실행하기 위한 고려 사항입니다. 일부 Azure 노드 ("버스트 tooAzure" 구성에 추가 된 작업자 역할 인스턴스)의 toodeployments만 적용 됩니다.

* 클라우드 서비스의 작업자 역할 인스턴스는 Azure에서 미리 알리지 않고 정기적으로 다시 프로비전됩니다(예: 시스템 유지 관리에서 또는 인스턴스가 실패할 경우). MPI 작업을 실행 하는 동안에 인스턴스는 다시 프로 비전, 경우 hello 인스턴스 데이터를 잃고 처음 배포한, hello MPI 작업 toofail을 일으킬 수 있는 경우 toohello 상태를 반환 합니다. hello 노드 hello 및 단일 MPI 작업에 대 한 사용 하는 더 이상 hello 작업을 실행 하면 hello는 hello 인스턴스 중 하나는 다시 프로 비전 작업이 실행 되는 동안 가능성이 높습니다. 이러한 사실도 고려해 hello 배포에서 단일 노드를 파일 서버로 지정 하면 됩니다.
* Azure에서 MPI 작업 toorun toouse hello RDMA 가능 인스턴스가 없는 합니다. HPC 팩에서 지원되는 모든 인스턴스 크기를 사용할 수 있습니다. 그러나 RDMA 가능 인스턴스 hello 상대적으로 대규모의 MPI 작업은 중요 한 toohello 대기 시간 및 hello hello 노드를 연결 하는 hello 네트워크 대역폭을 실행 하는 데 권장 됩니다. 다른 크기 toorun 대기 시간 및 대역폭에 민감한 MPI 작업을 사용 하는 경우에 단일 태스크만 몇 가지 노드에서 실행 되는 소형 작업을 실행 하는 것이 좋습니다.
* 배포 된 응용 프로그램 tooAzure 인스턴스는 hello 응용 프로그램과 관련 된 약관 제목 toohello입니다. 라이선스에 대 한 상용 응용 프로그램 또는 hello 클라우드에서 실행 하기 위한 기타 제한의 hello 공급 업체와 함께 확인 하십시오. 일부 공급 업체는 종량제 라이선스를 제공합니다.
* Azure 인스턴스 tooaccess 온-프레미스 노드, 공유 및 라이선스 서버 설치 추가로 필요 합니다. 예를 들어, tooenable hello Azure 노드 tooaccess 온-프레미스 라이선스 서버를 사용 하는 사이트 간 Azure 가상 네트워크를 구성할 수 있습니다.
* Azure 인스턴스에서 MPI 응용 프로그램 toorun 각 MPI 응용 프로그램 등록 with Windows Firewall hello 인스턴스에서 hello를 실행 하 여 **hpcfwutil** 명령입니다. 따라서 hello 방화벽에 의해 동적으로 할당 된 포트에서 MPI 통신 tootake 위치를 수 있습니다.
  
  > [!NOTE]
  > 버스트 tooAzure 배포용 구성할 수도 있습니다 방화벽 예외 명령을 toorun 자동으로 tooyour 클러스터에 추가 된 모든 새 Azure 노드의 합니다. Hello를 실행 한 후 **hpcfwutil** 명령로 스크롤한 다음 응용 프로그램의 작동을 Azure 노드 용 hello 명령 tooa 시작 스크립트를 추가 합니다. 자세한 내용은 [Azure 노드에 시작 스크립트 사용](https://technet.microsoft.com/library/jj899632.aspx)을 참조하세요.
  > 
  > 
* HPC 팩 hello CCP_MPI_NETMASK 클러스터 환경 변수 toospecify 허용 되는 주소의 범위를 사용 하 여 MPI 통신에 대 한 합니다. HPC Pack 2012 r 2 부터는 hello CCP_MPI_NETMASK 클러스터 환경 변수만 영향을 도메인에 가입 된 클러스터 계산 노드 간 MPI 통신 (온-프레미스 또는 Azure Vm에서). 전환 tooAzure 구성에 추가 된 노드에서 hello 변수는 무시 됩니다.
* 다른 클라우드 서비스 (예를 들어 여러 클라우드 서비스에 배포 된 Azure VM 계산 노드 또는 서로 다른 노드 템플릿으로 버스트 tooAzure 배포의 경우)에 배포 되는 Azure 인스턴스에서 MPI 작업을 실행할 수 없습니다. 서로 다른 노드 템플릿으로 시작 하는 여러 Azure 노드 배포가 있는 경우 hello MPI 작업은 하나의 Azure 노드 집합에서 실행 해야 합니다.
* Azure 노드 tooyour 클러스터를 추가 하 고 가져오고으로 온라인 hello HPC 작업 스케줄러 서비스 즉시 hello 노드에서 toostart 작업을 시도 합니다. 경우에 작업의 일부가 Azure에서 실행 수를 업데이트 하거나 작업 템플릿 toodefine 형식을 Azure에서 실행할 수 있는 작업 만들기를 확인 합니다. 예를 들어 Azure 노드에서만 실행만 작업 템플릿을 사용 하 여 제출 된 작업이 hello 노드 그룹 속성 toohello 작업 서식 파일을 추가 하 고 hello로 AzureNodes 선택 tooensure 값이 필요 합니다. Azure 노드 용 사용자 지정 그룹 toocreate hello Add-hpcgroup HPC PowerShell cmdlet을 사용 합니다.

## <a name="next-steps"></a>다음 단계
* 대체 toousing HPC Pack으로 Azure의 계산 노드 관리 되는 풀에서 MPI 응용 프로그램 hello Azure 배치 서비스 toorun 사용 하 여 개발 합니다. 참조 [toorun 인터페이스 MPI (Message Passing) 응용 프로그램을 Azure 일괄 처리의 작업을 사용 하 여 다중 인스턴스](../../../batch/batch-mpi.md)합니다.
* Linux MPI toorun 하려는 경우 hello Azure RDMA 네트워크에 액세스 하는 응용 프로그램 참조 [Linux RDMA 클러스터 toorun MPI 응용 프로그램 설정](../../linux/classic/rdma-cluster.md)합니다.

<!--Image references-->
[burst]:media/hpcpack-rdma-cluster/burst.png
[iaas]:media/hpcpack-rdma-cluster/iaas.png
[pingpong1]:media/hpcpack-rdma-cluster/pingpong1.png
[pingpong2]:media/hpcpack-rdma-cluster/pingpong2.png
