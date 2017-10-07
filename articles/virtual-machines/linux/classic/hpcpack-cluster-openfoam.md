---
title: "Linux Vm에서 HPC Pack을 사용한 OpenFOAM aaaRun | Microsoft Docs"
description: "Azure에서 Microsoft HPC Pack 클러스터를 배포하고 RDMA 네트워크 간의 여러 Linux 계산 노드에서 OpenFOAM 작업을 실행합니다."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Azure의 Linux RDMA 클러스터에서 Microsoft HPC 팩을 사용하여 OpenFoam 실행
이 문서에서는 Azure 가상 컴퓨터의 한 가지 방법은 toorun OpenFoam 합니다. 여기서는 Azure에서 Linux 계산 노드를 사용하여 Microsoft HPC Pack 클러스터를 배포하고 Intel MPI를 사용하여 [OpenFoam](http://openfoam.com/) 작업을 실행합니다. Hello 계산 노드 hello Azure RDMA 네트워크를 통해 통신할 수 있도록 hello 계산 노드를 위해 RDMA 가능 Azure Vm을 사용할 수 있습니다. Azure에서 OpenFoam 완벽 하 게 포함 하는 다른 옵션 toorun hello UberCloud의 같은 Marketplace에서에서 사용할 수 있는 상용 이미지 구성 [CentOS 6 OpenFoam 2.3](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), 및에서 실행 하 여 [Azure 배치](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/)합니다. 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

OpenFOAM(오픈 필드 작업 및 조작에 대한)은 상업용 및 연구용 조직의 공학 및 과학에서 널리 사용되는 오픈 소스 CFD(컴퓨팅 유체 역학) 소프트웨어 패키지입니다. Meshing, 특히 snappyHexMesh, 복잡한 CAD 기하학 및 전처리 및 후처리에 대한 병렬화된 메셔에 대한 도구를 포함합니다. 거의 모든 프로세스는 사용자가 tootake 활용에서 마음껏 컴퓨터 하드웨어를 사용 하도록 설정 병렬로 실행 합니다.  

Microsoft HPC Pack 기능 toorun 제공 대규모 HPC 및 Microsoft Azure 가상 컴퓨터의 클러스터에서 MPI 응용 프로그램을 포함 하 여 병렬 응용 프로그램입니다. HPC 팩은 HPC 팩 클러스터에 배포된 Linux 계산 노드 VM에서 Linux HPC 응용 프로그램의 실행도 지원합니다. 참조 [Azure에서 HPC Pack 클러스터에서 계산 노드 Linux 시작](hpcpack-cluster.md) Linux 소개 toousing에 대 한 HPC Pack을 사용한 노드를 계산 합니다.

> [!NOTE]
> 이 문서에서는 설명 방법을 toorun HPC Pack을 사용 하 여 Linux MPI 작업 합니다. 또한 여기서는 Linux 시스템 관리 및 Linux 클러스터에서 실행 중인 MPI 작업에 대해 잘 알고 있다고 가정합니다. MPI 및 OpenFOAM hello이이 문서에 표시 된 것과 다른 버전을 사용 하는 경우 일부 설치 및 구성 단계 toomodify를 할 수 있습니다. 
> 
> 

## <a name="prerequisites"></a>필수 조건
* **RDMA 지원 Linux 계산 노드가 포함된 HPC 팩 클러스터** - [Azure Resource Manager 템플릿](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) 또는 [Azure PowerShell 스크립트](hpcpack-cluster-powershell-script.md)를 사용하여 A8, A9, H16r 또는 H16rm 크기의 Linux 계산 노드가 포함된 HPC 팩 클러스터를 배포합니다. 참조 [Azure에서 HPC Pack 클러스터에서 계산 노드 Linux 시작](hpcpack-cluster.md) hello 필수 구성 요소와 두 옵션 중 하나에 대 한 단계입니다. Hello PowerShell에서 스크립트 배포 옵션을 선택 하면이 문서의 hello 끝 hello 예제 파일의 hello 샘플 구성 파일을 참조 하십시오. 2 크기 A8 SUSE Linux Enterprise Server 12는 계산 노드 및 헤드 노드 크기 A8 Windows Server 2012 r 2로 구성 된이 구성 toodeploy Azure 기반 HPC Pack 클러스터를 사용 합니다. 구독 및 서비스 이름을 적절한 값으로 대체합니다. 
  
  **추가 참고 사항 tooknow**
  
  * Azure의 Linux RDMA 네트워킹 필수 조건에 대한 자세한 내용은 [고성능 계산 VM 크기](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.
  * Hello Powershell에서 스크립트 배포 옵션을 사용 하면 한 클라우드 서비스 toouse hello RDMA 네트워크 연결 내에서 모든 hello Linux 계산 노드를 배포 합니다.
  * Hello Linux 노드를 배포한 후 추가 관리 작업을 모두 SSH tooperform 여 연결 합니다. Hello Azure 포털에서에서 각 Linux VM에 대 한 hello SSH에 대 한 연결 세부 정보를 찾습니다.  
* **Intel MPI** -toorun OpenFOAM SLES 12 HPC에서 Azure의 노드에서 계산, hello에서 tooinstall hello Intel MPI 라이브러리 5 런타임이 필요 [Intel.com 사이트](https://software.intel.com/en-us/intel-mpi-library/)합니다. (Intel MPI 5는 CentOS 기반 HPC 이미지에 미리 설치되어 있습니다.)  이후 단계에서 필요한 경우 Linux 계산 노트에 Intel MPI를 설치합니다. 이 단계에서는 tooprepare 인텔를 등록 한 후 hello에에서 링크 hello 확인 전자 메일 toohello 관련된 웹 페이지입니다. 그런 다음 복사 hello hello Intel MPI의 적절 한 버전에 대 한 hello.tgz 파일에 대 한 링크를 다운로드 합니다. 이 문서는 Intel MPI 5.0.3.048 버전을 기반으로 합니다.
* **OpenFOAM 소스 팩** -hello에서 Linux 용 hello OpenFOAM 소스 팩 소프트웨어를 다운로드 [OpenFOAM Foundation 사이트](http://openfoam.org/download/2-3-1-source/)합니다. 이 문서는 OpenFOAM-2.3.1.tgz로 다운로드할 수 있는 소스 팩 버전 2.3.1을 기반으로 합니다. 이 문서 toounpack의 뒷부분에 나오는 hello 지침에 따라 하 고 hello Linux 계산 노드에서 OpenFOAM를 컴파일하십시오.
* **EnSight** (선택 사항)-OpenFOAM 시뮬레이션의 toosee hello 결과 다운로드 및 설치 hello [EnSight](https://www.ceisoftware.com/download/) 시각화 및 분석 하는 프로그램입니다. 라이선스 및 다운로드 정보는 hello EnSight 사이트에 있습니다.

## <a name="set-up-mutual-trust-between-compute-nodes"></a>계산 노드 간 상호 트러스트 설정
Hello 노드 tootrust 서로 필요 하 여러 Linux 노드에 대해 노드 간 작업 실행 (여 **rsh** 또는 **ssh**). Microsoft HPC Pack IaaS 배포 스크립트 hello로 hello HPC Pack 클러스터를 만들 때 hello 스크립트는 자동으로 지정 하는 hello 관리자 계정에 대 한 영구 상호 트러스트를 설정 합니다. Hello 클러스터의 도메인에서 만들 사용자의 관리자가 아닌 경우 작업 toothem, 할당 된 hello 작업이 완료 된 후 hello 관계를 삭제 하는 경우 tooset hello 노드 간에 상호 트러스트 임시를 보유 합니다. 각 사용자에 대 한 트러스트 tooestablish hello 트러스트 관계에 대 한 HPC Pack을 사용 하는 RSA 키 쌍 toohello 클러스터를 제공 합니다.

### <a name="generate-an-rsa-key-pair"></a>RSA 키 쌍 생성
공개 키와 개인 키를 포함 하는 RSA 키 쌍을 쉽게 toogenerate를 실행 하 여 Linux hello **붙여넣으세요** 명령입니다.

1. Linux 컴퓨터 tooa에 로그온 합니다.
2. Hello 다음 명령을 실행 합니다.
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > 키를 눌러 **Enter** hello 명령이 완료 될 때까지 toouse hello 기본 설정 합니다. 여기에 암호를 입력하지 마십시오. 암호를 묻는 메시지가 표시되면 **Enter** 키만 누르십시오.
   > 
   > 
   
   ![RSA 키 쌍 생성][keygen]
3. 디렉터리 toohello ~/.ssh 디렉터리를 변경 합니다. 개인 키 hello id_rsa.pub id_rsa와 hello 공개 키에 저장 됩니다.
   
   ![개인 및 공용 키][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a>Hello 키 쌍 toohello HPC Pack 클러스터 추가
1. HPC Pack 관리자 계정 (hello 관리자 설정한 계정 hello 배포 스크립트를 실행 한 경우)으로 원격 데스크톱 연결 tooyour 헤드 노드를 확인 합니다.
2. Hello 클러스터의 Active Directory 도메인에 표준 Windows Server 절차 toocreate 도메인 사용자 계정을 사용 합니다. 예를 들어 hello 헤드 노드에서 hello Active Directory 사용자 및 컴퓨터 도구를 사용 합니다. 이 문서의 hello 예제 hpclab\hpcuser 이라는 도메인 사용자를 만들면 가정 합니다.
3. C:\cred.xml 및 복사 hello RSA 키 데이터를 라는 파일을 만듭니다. 이 문서의 끝 hello에 샘플 cred.xml 파일이.입니다.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. 명령 프롬프트를 열고 다음 명령을 tooset hello hello hpclab\hpcuser 계정에 대 한 데이터를 자격 증명 hello를 입력 합니다. Hello를 사용 하 여 **extendeddata** 매개 변수 toopass hello hello 키 데이터를 만든 C:\cred.xml 파일의 이름입니다.
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   이 명령은 출력 없이 성공적으로 완료됩니다. Toorun 작업 해야 하는 hello 사용자 계정에 대 한 hello 자격 증명을 설정한 후 hello cred.xml 파일을 안전한 위치에 저장 하거나 삭제 합니다.
5. Linux 노드 중 하나에서 hello RSA 키 쌍을 생성 한 경우 사용을 마친 후 toodelete hello 키를 기억 합니다. HPC Pack은 기존 id_rsa 파일 또는 id_rsa.pub 파일을 찾으면 상호 트러스트를 설정하지 않습니다.

> [!IMPORTANT]
> म hello Linux 노드에서 hello 루트 계정에서 관리자가 제출 하는 작업 실행 되기 때문에 공유 클러스터에서 클러스터 관리자를 사용 하는 Linux 작업 실행 하는 권장 되지 않습니다. 그러나 관리자가 아닌 사용자가 제출한 작업 이름과 같은 hello 작업 사용자로 이름을 hello로 로컬 Linux 사용자 계정에서 실행 됩니다. 이 경우 HPC Pack toohello 작업에 할당 된 hello 노드에서이 Linux 사용자에 대 한 상호 트러스트를 설정 합니다. Hello 작업을 실행 하기 전에 hello Linux 노드에서 수동으로 hello Linux 사용자를 설정할 수 있습니다 또는 HPC 팩 hello 사용자 자동으로 만듭니다 hello 작업이 제출 되는 경우. HPC Pack hello 사용자를 만드는 경우 hello 작업이 완료 된 후 HPC Pack 삭제 됩니다. tooreduce 보안 위협, HPC Pack 작업 완료 후 hello 키를 제거 합니다.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>사용자가 액세스할 파일 공유를 설정합니다.
이제 hello 헤드 노드에서 폴더에 표준 SMB 공유를 설정 합니다. tooallow hello Linux 노드 tooaccess 응용 프로그램 파일 일반적인 경로로 탑재 hello 공유 hello Linux 노드에 폴더. 원하는 경우 여러 시나리오에서 권장되는 Azure 파일 공유 또는 NFS 공유와 같은 다른 파일 공유 옵션을 사용할 수 있습니다. Hello 파일 내용 및 단계에 공유 참조 [Azure에서 HPC Pack 클러스터에서 계산 노드 Linux 시작](hpcpack-cluster.md)합니다.

1. Hello 헤드 노드에 대 한 폴더를 만들고 읽기/쓰기 권한을 설정 하 여 tooEveryone을 공유 합니다. 예를 들어 C:\OpenFOAM으로 hello 헤드 노드에서 공유 \\ \\SUSE12RDMA HN\OpenFOAM 합니다. 여기에서 *SUSE12RDMA HN* hello 헤드 노드 hello 호스트 이름입니다.
2. Windows PowerShell 창을 열고 다음 명령을 hello를 실행 합니다.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

첫 번째 명령은 hello hello LinuxNodes 그룹의 모든 노드에서 /openfoam 라는 폴더를 만듭니다. 두 번째 명령은 hello dir_mode 및 file_mode 비트 집합 too777 hello Linux 노드에 hello 공유 폴더 //SUSE12RDMA-HN/OpenFOAM을 탑재합니다. hello *username* 및 *암호* hello 명령 hello 헤드 노드에 대 한 사용자의 hello 자격 증명 이어야 합니다.

> [!NOTE]
> hello "\`" hello 두 번째 명령은의 기호는 PowerShell에 대 한 이스케이프 기호는 합니다. "\`,"hello 의미"," (쉼표 문자)는 hello 명령의 일부입니다.
> 
> 

## <a name="install-mpi-and-openfoam"></a>MPI 및 OpenFOAM 설치
hello RDMA 네트워크에서 MPI 작업으로 OpenFOAM toorun toocompile OpenFOAM hello Intel MPI 라이브러리와 함께 필요합니다. 

먼저, 실행 하 여 여러 **clusrun** 명령을 tooinstall Intel MPI 라이브러리 (아직 설치 되지 않은) 하는 경우 한 OpenFOAM Linux 노드에 있습니다. 사용 하 여 hello 헤드 노드 공유 구성 이전에 hello Linux 노드 간에 tooshare hello 설치 파일.

> [!IMPORTANT]
> 이러한 설치 및 컴파일 단계는 예제입니다. Linux 시스템 관리 tooensure 종속 컴파일러 및 라이브러리 제대로 설치 되어 있는지에 대 한 지식이 필요 합니다. Intel MPI 및 OpenFOAM 버전에 대 한 특정 환경 변수 또는 기타 설정을 toomodify를 할 수 있습니다. 자세한 내용은 사용 환경에 맞는 [Linux 설치 가이드용 Intel MPI 라이브러리](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) 및 [OpenFOAM 원본 팩 설치](http://openfoam.org/download/2-3-1-source/)를 참조하세요.
> 
> 

### <a name="install-intel-mpi"></a>Intel MPI 설치
Hello Linux 노드에 /openfoam에서이 파일에 액세스할 수 있도록 hello 헤드 노드에서 C:\OpenFoam에 Intel MPI (이 예제의 l_mpi_p_5.0.3.048.tgz)에 대 한 hello 다운로드 한 설치 패키지를 저장 합니다. 그러고 나 서 **clusrun** 모든 hello Linux 노드에 tooinstall Intel MPI 라이브러리입니다.

1. hello 다음 hello 설치 패키지 복사본 명령과 너무/옵트인/intel 각 노드에서 추출 합니다.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. 인텔 MPI 라이브러리 tooinstall silent.cfg 파일을 자동으로 사용 합니다. 예 hello에 hello이이 문서의 뒷부분에서 샘플 파일을 찾을 수 있습니다. 전체 hello에서이 파일 공유 폴더 /openfoam입니다. Hello silent.cfg 파일에 대 한 세부 정보를 참조 하십시오. [Linux Installation Guide-자동 설치에 대 한 Intel MPI 라이브러리](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall)합니다.
   
   > [!TIP]
   > silent.cfg 파일을 Linux 줄 끝(CR LF가 아닌 LF만)을 사용하여 텍스트 파일로 저장합니다. 이 단계를 수행 하면 hello Linux 노드에에서 제대로 실행 되도록 합니다.
   > 
   > 
3. 자동 모드에서 Intel MPI Library를 설치합니다.
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a>MPI 구성
테스트를 추가할지를 묻는 toohello /etc/security/limits.conf 줄의 각 hello Linux 노드에 따라 hello:

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


Hello limits.conf 파일을 업데이트 한 후 hello Linux 노드를 다시 시작 합니다. 예를 들어 hello 다음 이름을 사용해 서 **clusrun** 명령:

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

를 다시 시작한 후 /openfoam으로 탑재 되어 해당 hello 공유 폴더를 확인 합니다.

### <a name="compile-and-install-openfoam"></a>OpenFOAM 컴파일 및 설치
Hello Linux 노드에 /openfoam에서이 파일에 액세스할 수 있도록 hello 헤드 노드에서 OpenFOAM 소스 팩 (OpenFOAM 2.3.1.tgz이 예에서) tooC:\OpenFoam hello에 대 한 hello 다운로드 한 설치 패키지를 저장 합니다. 그러고 나 서 **clusrun** 모든 OpenFOAM toocompile hello Linux 노드에 명령입니다.

1. 각 Linux 노드에 복사 hello 소스 패키지 toothis 폴더 폴더 /opt/OpenFOAM을 만들고 있는 추출 합니다.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. toocompile OpenFOAM Intel MPI 및 OpenFOAM 모두에 대 한 몇 가지 환경 변수를 먼저 설정 Intel MPI 라이브러리 hello로 합니다. Settings.sh tooset hello 변수 호출 되는 bash 스크립트를 사용 합니다. 예 hello에 hello이이 문서의 뒷부분에서 샘플 파일을 찾을 수 있습니다. 전체 hello에서 (Linux 줄 끝으로 저장 됨)이이 파일 공유 폴더 /openfoam입니다. 이 파일에는 또한 hello MPI 및 OpenFOAM 런타임 이후 toorun OpenFOAM 작업을 사용 하는 설정을 포함 합니다.
3. 필요한 종속 패키지 toocompile OpenFOAM를 설치 합니다. Linux 배포판에 따라 tooadd 저장소를 먼저 할 수 있습니다. 실행 **clusrun** toohello 다음과 비슷한 명령을:
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    필요한 경우 SSH tooeach Linux 노드 toorun hello tooconfirm 제대로 실행 되는 명령입니다.
4. 다음 명령은 toocompile OpenFOAM hello를 실행 합니다. 따라서 hello를 사용 하 여 hello 컴파일 프로세스 일부 시간 toocomplete 걸리고 많은 로그 정보 toostandard 출력의 생성, **인터리브 /** 인터리브 toodisplay hello 출력 옵션입니다.
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > hello "\`" hello 명령에는 기호는 powershell에 이스케이프 기호입니다. "\`&" hello 의미 "&" hello 명령에 포함 합니다.
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a>Toorun OpenFOAM 작업 준비
이제 get 준비 toorun MPI 작업 두 개의 Linux 노드에서 hello OpenFoam 샘플 중 하나인 sloshingTank3D 호출 됩니다. 

### <a name="set-up-hello-runtime-environment"></a>Hello 런타임 환경 설정
tooset 업 hello hello 헤드 노드에서 다음 Windows PowerShell 창에서 명령을 실행 hello Linux 노드에서 MPI 및 OpenFOAM hello 런타임 환경입니다. (이 명령은 SUSE Linux에 대해서만 유효합니다.)

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a>샘플 데이터 준비
Hello 헤드 노드 공유를 사용 하 여 이전에 구성한 (/openfoam으로 탑재할) hello Linux 노드 간에 tooshare 파일입니다.

1. Linux에 SSH tooone 노드를 계산 합니다.
2. 이 아직 수행 하지 않은 경우 다음 명령 tooset hello OpenFOAM 런타임 환경을 hello를 실행 합니다.
   
   ```
   $ source /openfoam/settings.sh
   ```
3. Hello sloshingTank3D 샘플 toohello 공유 폴더를 복사한 tooit 이동 합니다.
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. 이 샘플의 hello 기본 매개 변수를 사용 하면 걸릴 수 있습니다 분 toorun 수만 하므로 toomodify 해도 일부 매개 변수 toomake 실행 속도입니다. 간단 하 게 하나의 선택할 toomodify hello 시간 단계 변수 deltaT 되며 writeInterval hello 시스템/controlDict 파일에 있습니다. 이 파일의 시간 및 데이터 읽기 및 쓰기 솔루션 toohello 제어와 관련 된 모든 입력된 데이터를 저장 합니다. 예를 들어 0.05 too0.5에서 writeInterval의 hello 값과 hello deltaT 0.05 too0.5에서 값을 변경할 수 있습니다.
   
   ![단계 변수 수정][step_variables]
5. Hello 시스템/decomposeParDict 파일에 hello 변수에 대 한 원하는 값을 지정 합니다. 이 예에서는 두 개의 numberOfSubdomains too16 및 n/hierarchicalCoeffs Linux 노드 각각 8 개 코어, 사용 설정 too(1 1 16), 즉 OpenFOAM를 16 프로세스와 병렬로 실행 합니다. 자세한 내용은 [OpenFOAM 사용자 가이드: 3.4 병렬로 응용 프로그램 실행](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4)을 참고하세요.
   
   ![프로세스 분해][decompose]
6. Hello 명령을 hello sloshingTank3D 디렉터리 tooprepare hello 샘플 데이터에서 다음을 실행 합니다.
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. Hello 헤드 노드에서 표시 되어야 C:\OpenFoam\sloshingTank3D에 hello 예제 데이터 파일이 복사 됩니다. (C:\OpenFoam hello 헤드 노드에서 hello 공유 폴더입니다.)
   
   ![헤드 노드 hello에 데이터 파일][data_files]

### <a name="host-file-for-mpirun"></a>mpirun에 대한 호스트 파일
이 단계에서는 파일을 만들면 호스트 (계산 노드 목록)는 hello **mpirun** 명령을 사용 합니다.

1. Hello Linux 노드 중 하나에서 모든 Linux 노드에 /openfoam/hostfile에서이 파일에 연결할 수 있도록 /openfoam, 아래 hostfile 라는 파일을 만듭니다.
2. Linux 노드 이름을 이 파일에 작성합니다. 이 예제에서는 hello 파일 이름 다음 hello를 포함 합니다.
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > 또한 hello 헤드 노드에서 C:\OpenFoam\hostfile에이 파일을 만들 수 있습니다. 이 옵션을 선택하는 경우 Linux 줄 끝(CR LF가 아닌 LF만)을 사용하여 텍스트 파일로 저장합니다. 이렇게 하면 hello Linux 노드에에서 제대로 실행 되도록 합니다.
   > 
   > 
   
   **Bash 스크립트 래퍼**
   
   많은 Linux 노드에 있는 경우 그 중 일부에 사용자 작업 toorun 않습니다 고정된 호스트 파일을 하는 것이 좋습니다 toouse 노드 tooyour 작업 할당 될 모르기 때문에. 이 경우에 대 한 bash 스크립트 래퍼 작성 **mpirun** toocreate 호스트 파일을 자동으로 hello 합니다. /Openfoam/hpcimpirun.sh로 저장와 hpcimpirun.sh이 문서의 hello 끝에서 호출 하는 예제 bash 스크립트 래퍼를 찾을 수 있습니다. 이 예제 스크립트는 다음 hello:
   
   1. 에 대 한 hello 환경 변수를 설정 하는 **mpirun**, 및 일부 추가 명령 매개 변수 toorun hello MPI 작업 hello RDMA 네트워크를 통해 합니다. 이 경우 변수를 다음 hello 설정 합니다.
      
      * I_MPI_FABRICS=shm:dapl
      * I_MPI_DAPL_PROVIDER=ofa-v2-ib0
      * I_MPI_DYNAMIC_CONNECTION=0
   2. Toohello 환경 변수 $에 따라 호스트 파일을 만듭니다. CCP_NODES_CORES hello 작업이 활성화 되 면 hello HPC 헤드 노드에로 설정 됩니다.
      
      $CCP_NODES_CORES의 hello 형식이이 패턴을 따릅니다.
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      여기서,
      
      * `<Number of nodes>`-hello 노드 수가 toothis 작업을 할당 합니다.  
      * `<Name of node_n_...>`-각 노드 이름을 hello toothis 작업을 할당 합니다.
      * `<Cores of node_n_...>`-hello hello 노드에 할당 된 toothis 작업의 코어 수입니다.
      
      예를 들어 hello 작업에서 두 노드 toorun를 필요한 경우 $CCP_NODES_CORES 것과 비슷합니다.
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. 호출 hello **mpirun** 명령 및 매개 변수 toohello 명령줄을 두 개의 추가 합니다.
      
      * `--hostfile <hostfilepath>: <hostfilepath>`-hello 호스트 파일 hello 스크립트의 hello 경로 만듭니다
      * `-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-hello HPC Pack 헤드 노드를 hello 총 코어 수를 저장 하 여 설정 하는 환경 변수 toothis 작업을 할당 합니다. 이 경우 hello에 대 한 프로세스 수가 지정 **mpirun**합니다.

## <a name="submit-an-openfoam-job"></a>OpenFOAM 작업 제출
이제 HPC 클러스터 관리자에서 작업을 제출할 수 있습니다. Hello 수행 하는 작업의 일부에 대 한 hello 명령줄에서 toopass hello 스크립트 hpcimpirun.sh를 해야합니다.

1. Tooyour 클러스터 헤드 노드를 연결 하 고 HPC 클러스터 관리자를 시작 합니다.
2. **리소스 관리에서**, hello Linux 계산 노드 hello에 있는지 확인 하세요 **온라인** 상태입니다. 온라인 상태가 아닌 경우 노드를 선택하고 **온라인 상태로 전환**을 클릭합니다.
3. **작업 관리**에서 **새 작업**을 클릭합니다.
4. 작업 이름(예: *sloshingTank3D*)을 입력합니다.
   
   ![작업 세부 정보][job_details]
5. **리소스 작업**, "노드"으로 리소스의 hello 형식을 선택 하 고 hello 최소 too2를 설정 합니다. 이 구성은이 예에서 8 개의 코어가 각각 두 개의 Linux 노드에서 hello 작업을 실행 합니다.
   
   ![작업 리소스][job_resources]
6. 클릭 **작업 편집** 왼쪽된 탐색 영역 hello와 클릭 **추가** tooadd 작업 toohello 작업 합니다. Hello로 4 개 작업 toohello 작업을 추가 명령줄 및 설정 합니다.
   
   > [!NOTE]
   > 실행 `source /openfoam/settings.sh` 되므로 hello OpenFOAM 명령 전에 호출 각각 작업을 수행 하는 hello hello OpenFOAM 및 MPI 런타임 환경에서 설정 합니다.
   > 
   > 
   
   * **작업 1**. 실행 **decomposePar** toogenerate 실행 하는 데이터 파일이 **interDyMFoam** 병렬로 합니다.
     
     * 하나의 노드 toohello 작업 할당
     * **명령 줄** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`
     * **작업 디렉터리** -/ openfoam/sloshingTank3D
     
     다음 그림 hello를 참조 하십시오. 마찬가지로 hello 나머지 작업을 구성 합니다.
     
     ![작업 1 세부 정보][task_details1]
   * **작업 2**. 실행 **interDyMFoam** 병렬 toocompute hello 샘플에서.
     
     * 두 개의 노드 toohello 작업 할당
     * **명령 줄** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`
     * **작업 디렉터리** -/ openfoam/sloshingTank3D
   * **작업 3**. 실행 **reconstructPar** toomerge hello 설정 시간 디렉터리의 각 processor_N_ 디렉터리에서 단일 집합으로 합니다.
     
     * 하나의 노드 toohello 작업 할당
     * **명령 줄** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`
     * **작업 디렉터리** -/ openfoam/sloshingTank3D
   * **작업 4**. 실행 **foamToEnsight** 병렬 tooconvert에 EnSight로 hello OpenFOAM 결과 파일 형식을 지정 하 고 hello EnSight 파일 Ensight hello 사례 디렉터리에 라는 디렉터리에 저장 합니다.
     
     * 두 개의 노드 toohello 작업 할당
     * **명령 줄** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`
     * **작업 디렉터리** -/ openfoam/sloshingTank3D
7. 작업 순서를 오름차순 종속성 toothese 작업을 추가 합니다.
   
   ![작업 종속성][task_dependencies]
8. 클릭 **전송** toorun이이 작업 합니다.
   
   HPC Pack 기본적으로 현재 로그온 한 사용자 계정으로 hello 작업을 제출합니다. 클릭 한 후 **전송**, tooenter hello 사용자 이름 및 암호 입력 하 라는 대화 상자가 나타날 수 있습니다.
   
   ![작업 자격 증명][creds]
   
   어떤 조건 HPC Pack 하기 전에 입력 하 고이 대화 상자를 표시 하지 않는 hello 사용자 정보를 기억 합니다. 다시 표시 하 고 hello 다음 명령 프롬프트에서 명령을 입력 한 다음 hello 작업을 제출 하는 HPC Pack toomake 합니다.
   
   ```
   hpccred delcreds
   ```
9. hello 작업 toohello 매개 변수 hello 샘플에 대 한 설정에 따라 분 tooseveral 시간 수만에서 작업을 수행 합니다. Hello 열 지도 hello Linux 노드에서 실행 되는 hello 작업을 볼 수 있습니다. 
   
   ![열 지도][heat_map]
   
   각 노드에서 8개의 프로세스가 시작됩니다.
   
   ![Linux 프로세스][linux_processes]
10. Hello 작업이 완료 되 면 hello 작업 결과를 C:\OpenFoam\sloshingTank3D, 및 hello 로그 파일에 C:\OpenFoam 아래의 폴더에서 찾습니다.

## <a name="view-results-in-ensight"></a>EnSight에서 결과 보기
필요에 따라 [EnSight](https://www.ceisoftware.com/) toovisualize hello OpenFOAM 작업의 hello 결과 및 분석 합니다. EnSight에서 시각화 및 애니메이션에 대한 자세한 내용은 이 [비디오 가이드](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html)를 참조하세요.

1. Hello 헤드 노드에서 EnSight를 설치한 후이 시작 합니다.
2. C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case를 엽니다.
   
   Hello 뷰어에서 탱크를 표시 됩니다.
   
   ![EnSight의 탱크][tank]
3. 만들기는 **Isosurface** 에서 **internalMesh**, hello 변수 선택 **alpha_water**합니다.
   
   ![isosurface 만들기][isosurface]
4. Hello 색을 설정 **Isosurface_part** hello 이전 단계에서 만든 합니다. 예를 들어 설정 toowater 파란색입니다.
   
   ![Isosurface 색상 편집][isosurface_color]
5. 만들기는 **Iso 볼륨** 에서 **벽** 선택 하 여 **벽** hello에 **부분** 패널로 끌어다 hello 클릭 **Isosurfaces**  hello 도구 모음 단추입니다.
6. Hello 대화 상자에서 선택 **형식** 으로 **Isovolume** 설정의 Min hello **Isovolume 범위** too0.5 합니다. toocreate isovolume hello, 클릭 **선택한 부분와 함께 만들기**합니다.
7. Hello 색을 설정 **Iso_volume_part** hello 이전 단계에서 만든 합니다. 예를 들어 설정 toodeep 물 파란색입니다.
8. Hello 색을 설정 **벽**합니다. 예를 들어 설정 tootransparent 흰색입니다.
9. 클릭 하 여 지금 **재생** hello 시뮬레이션의 toosee hello 결과입니다.
   
    ![탱크 결과][tank_result]

## <a name="sample-files"></a>샘플 파일
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>PowerShell 스크립트를 통한 클러스터 배포용 샘플 XML 구성 파일
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a>샘플 cred.xml 파일
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-tooinstall-mpi"></a>샘플 silent.cfg 파일 tooinstall MPI
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a>샘플 settings.sh 스크립트
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a>샘플 hpcimpirun.sh 스크립트
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
