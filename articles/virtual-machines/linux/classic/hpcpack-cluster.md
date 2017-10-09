---
title: "HPC Pack 클러스터에서 계산 Vm aaaLinux | Microsoft Docs"
description: "어떻게 toocreate 사용 HPC 팩 클러스터 및 Azure에서 Linux 고성능 (HPC) 작업을 컴퓨팅에 대 한 자세한 내용은"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Azure에서 HPC Pack 클러스터의 Linux 계산 노드 시작
Windows Server를 실행하는 헤드 노드 및 지원되는 Linux 배포를 실행하는 여러 컴퓨터 노드를 포함하는 Azure의 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) 클러스터를 설정합니다. Hello Linux 노드와 hello Windows hello 클러스터의 헤드 노드 간에 옵션 toomove 데이터를 탐색 합니다. Linux HPC toosubmit toohello 클러스터 작업 하는 방법에 대해 알아봅니다.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

상위 수준 hello 다음 다이어그램에서는 hello HPC Pack 클러스터 만들기 및 작업

![Linux 노드가 포함된 HPC Pack 클러스터][scenario]

다른 옵션 toorun Linux HPC에 대 한 Azure에서 작업 참조 [일괄 처리 및 고성능 컴퓨팅에 대 한 기술 리소스](../../../batch/big-compute-resources.md)합니다.

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a>Linux 계산 노드가 포함된 HPC Pack 클러스터 배포
이 문서에서는 두 가지 옵션이 toodeploy HPC Pack 클러스터 Azure에서 Linux 계산 노드와 합니다. 두 가지 방법 toocreate hello 헤드 노드에 HPC Pack의 Windows Server 마켓플레이스 이미지를 사용 합니다. 

* **Azure 리소스 관리자 템플릿** -hello Azure Marketplace에서에서 템플릿을 또는 hello 커뮤니티, tooautomate hello 리소스 관리자 배포 모델에서 hello 클러스터 만들기 퀵 스타트 템플릿을 사용 합니다. 예를 들어 hello [Linux 워크 로드에 대 한 HPC 팩 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) hello Azure Marketplace에서에서 서식 파일을 만듭니다 전체 HPC 팩 클러스터 인프라 Linux HPC에 대 한 작업입니다.
* **PowerShell 스크립트** -사용 하 여 hello [Microsoft HPC Pack IaaS 배포 스크립트](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-hpciaascluster.ps1**) tooautomate hello 클래식 배포 모델에서 전체 클러스터 배포 합니다. 이 Azure PowerShell 스크립트는 hello Azure Marketplace의에서 HPC Pack VM 이미지를 사용 하 여 빠른 배포를 위한 하 고 다양 한 구성 매개 변수 toodeploy Linux 계산 노드를 제공 합니다.

Azure에서 HPC Pack 클러스터 배포 옵션에 대 한 자세한 내용은 참조 [toocreate 옵션 및 Microsoft HPC Pack을 사용 하 여 Azure에 있는 고성능 HPC (컴퓨팅) 클러스터 관리](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

### <a name="prerequisites"></a>필수 조건
* **Azure 구독** -어느 hello Azure Global 또는 Azure China 서비스에서에서 구독을 사용할 수 있습니다. 계정이 없는 경우 몇 분 안에 [무료 계정](https://azure.microsoft.com/pricing/free-trial/) 을 만들 수 있습니다.
* **코어 할당량** -toodeploy 멀티 코어 VM 크기에 따라 여러 개의 클러스터 노드를 선택 하는 경우에 특히 tooincrease hello 할당량의 코어를 할 수 있습니다. 할당량 tooincrease 비용 없이 온라인 고객 지원 요청을 엽니다.
* **Linux 배포판** -HPC Pack 현재 계산 노드에 대 한 Linux 배포를 수행 하는 hello를 지원 합니다. 이러한 사용 가능한 배포판의 마켓플레이스 버전을 사용하거나 사용자 자체 버전을 제공할 수 있습니다.
  
  * **CentOS 기반**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC
  * **Red Hat Enterprise Linux** 6.7, 6.8, 7.2
  * **SUSE Linux Enterprise Server**: SLES 12, SLES 12(Premium), SLES 12 SP1, SLES 12 SP1(Premium), SLES 12 for HPC, SLES 12 for HPC(Premium)
  * **Ubuntu Server**: 14.04 LTS, 16.04 LTS
    
    > [!TIP]
    > RDMA 가능 hello VM 크기 중 하나를 사용 하 여 toouse hello Azure RDMA 네트워크 hello Azure Marketplace에서에서 SUSE Linux Enterprise Server 12 HPC 또는 HPC CentOS 기반 이미지를 지정 합니다. 자세한 내용은 [고성능 계산 VM 크기](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.
    > 
    > 

추가 필수 구성 요소 toodeploy hello hello HPC Pack IaaS 배포 스크립트를 사용 하 여 클러스터:

* **클라이언트 컴퓨터** -Windows 기반 클라이언트 컴퓨터 toorun hello 클러스터 배포 스크립트를 필요 합니다.
* **Azure PowerShell** - [Azure PowerShell(버전 0.8.10 이상)을 설치 및 구성](/powershell/azure/overview) 합니다.
* **HPC Pack IaaS 배포 스크립트** -다운로드 하 고 hello hello에서 hello 스크립트의 최신 버전을 푸는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=44949)합니다. 실행 하 여 hello 스크립트의 hello 버전을 확인 하면 `.\New-HPCIaaSCluster.ps1 –Version`합니다. 이 문서는 4.4.1 버전 또는 hello 스크립트의 나중에 기반으로 합니다.

### <a name="deployment-option-1-use-a-resource-manager-template"></a>배포 옵션 1. Resource Manager 템플릿 사용
1. Toohello 이동 [Linux 워크 로드에 대 한 HPC 팩 클러스터](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) 에서 Azure 마켓플레이스 hello 템플릿과 클릭 **배포**합니다.
2. 에 Azure 포털 hello hello 정보를 검토 하 고 클릭 **만들기**합니다.
   
    ![포털 만들기][portal]
3. Hello에 **기본 사항** 블레이드에서 hello 헤드 노드 VM의 이름도 지정 hello 클러스터에 대 한 이름을 입력 합니다. 기존 리소스 그룹을 선택 하거나 tooyou 사용할 수 있는 위치에 hello 배포에 대 한 그룹을 만들 수 있습니다. hello 위치에 영향을 특정 VM 크기 및 기타 Azure 서비스의 가용성을 hello (참조 [지역에 따라 사용할 수 있는 제품](https://azure.microsoft.com/regions/services/)).
4. Hello에 **헤드 노드 설정을** 블레이드에서 hello 기본 설정을 수락 일반적으로 첫 번째 배포에 대 한 합니다. 
   
   > [!NOTE]
   > hello **후 구성 스크립트 URL** 는 선택적 설정 하 고 toospecify 공개적으로 사용할 수 있는 Windows PowerShell 스크립트 실행 된 후 hello 헤드 노드 VM에 toorun 되도록 합니다. 
   > 
   > 
5. Hello에 **계산 노드 설정을** 블레이드에서 hello 노드, hello 번호 및 hello 노드의 크기에 대 한 명명 패턴을 선택 하 고 Linux 배포 toodeploy hello 합니다.
6. Hello에 **인프라 설정** 블레이드에서 hello 가상 네트워크 및 Active Directory에 대 한 이름을 입력 합니다. 도메인, 도메인 및 VM 관리자 자격 증명 및 hello 저장소 계정에 대 한 명명 패턴입니다.
   
   > [!NOTE]
   > HPC 팩 hello Active Directory 도메인 tooauthenticate 클러스터 사용자를 사용합니다. 
   > 
   > 
7. Hello 유효성 검사 테스트를 실행 하 고 hello 사용 약관을 검토 한 후 클릭 **구매**합니다.

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a>배포 옵션 2. Hello IaaS 배포 스크립트를 사용 하 여
다음은 hello HPC Pack IaaS 배포 스크립트를 사용 하 여 추가 필수 구성 요소 toodeploy hello 클러스터입니다.

* **클라이언트 컴퓨터** -Windows 기반 클라이언트 컴퓨터 toorun hello 클러스터 배포 스크립트를 필요 합니다.
* **Azure PowerShell** - [Azure PowerShell(버전 0.8.10 이상)을 설치 및 구성](/powershell/azure/overview) 합니다.
* **HPC Pack IaaS 배포 스크립트** -다운로드 하 고 hello hello에서 hello 스크립트의 최신 버전을 푸는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=44949)합니다. 실행 하 여 hello 스크립트의 hello 버전을 확인 하면 `.\New-HPCIaaSCluster.ps1 –Version`합니다. 이 문서는 4.4.1 버전 또는 hello 스크립트의 나중에 기반으로 합니다.

**XML 구성 파일**

HPC Pack IaaS 배포 스크립트 hello 입력된 toodescribe hello HPC 클러스터도 XML 구성 파일을 사용합니다. hello 다음 샘플 구성 파일을 지정 두 크기 A7 CentOS 7.0 Linux 계산 노드 및 HPC Pack 헤드 노드 구성 된 작은 클러스터 합니다. 

사용자 환경 및 원하는 클러스터 구성에 대 한 필요에 따라 hello 파일을 수정 하 고 HPCDemoConfig.xml 같은 이름으로 저장 합니다. 예를 들어 구독 이름 및 고유 저장소 계정 이름 및 클라우드 서비스 이름 toosupply 필요. 또한 다른 toochoose hello 계산 노드에 대 한 Linux 이미지를 지원 하는 것이 좋습니다. Hello 요소 hello 구성 파일에 대 한 자세한 내용은 참조 하십시오. hello 스크립트 폴더에 있는 Manual.rtf 파일 hello 및 [hello HPC Pack IaaS 배포 스크립트는 HPC 클러스터 만들기](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

**toorun hello HPC Pack IaaS 배포 스크립트**

1. Hello 클라이언트 컴퓨터에서 관리자 권한으로 Windows PowerShell을 엽니다.
2. 변경 스크립트 hello가 디렉터리 toohello 폴더 (이 예제의 E:\IaaSClusterScript)를 설치 합니다.
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. 다음 명령 toodeploy hello HPC Pack 클러스터 hello를 실행 합니다. 이 예에서는 해당 hello 구성 파일은 E:\HPCDemoConfig.xml 가정
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    a. 때문에 hello **AdminPassword** 지정 하지 않으면 사용자에 대 한 증명된 tooenter hello 암호 중인 hello 명령 앞, *MyAdminName*합니다.
   
    b. hello 스크립트 toovalidate hello 구성 파일을 시작합니다. Hello 네트워크 연결에 따라 tooseveral 분까지 걸릴 수 있으므로 합니다.
   
    ![유효성 검사][validate]
   
    c. 유효성 검사를 통과 hello 클러스터 리소스 toocreate hello 스크립트에 나열 됩니다. 입력 *Y* toocontinue 합니다.
   
    ![리소스][resources]
   
    d. toodeploy hello HPC Pack 클러스터를 시작 하 고 추가 수동 단계 없이 hello 구성을 완료 하는 hello 스크립트입니다. 몇 분 동안 hello 스크립트를 실행할 수 있습니다.
   
    ![배포][deploy]
   
   > [!NOTE]
   > 이 예제에서는 hello 스크립트 로그 파일을 자동으로 생성 hello 이후 **-로그 파일** 매개 변수가 지정 되지 않았습니다. hello 로그 실시간으로 기록 되지 않으며 hello 유효성 검사 및 hello 배포의 hello 끝에 수집 됩니다. Hello 스크립트가 실행 중인 PowerShell 프로세스 hello 중지 되 면 일부 로그 손실 됩니다.
   > 
   > 

## <a name="connect-toohello-head-node"></a>Toohello 헤드 노드를 연결 합니다.
Azure의 hello HPC Pack 클러스터를 배포한 후 [여 원격 데스크톱 연결](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello 클러스터를 배포할 때 지정한 도메인 자격 증명을 hello toohello 헤드 노드 VM를 사용 하 여 (예를 들어 *hpc\\ clusteradmin*). Hello 헤드 노드에서 hello 클러스터를 관리 합니다.

Hello 헤드 노드에서 HPC 클러스터 관리자 toocheck hello 상태의 hello HPC Pack 클러스터를 시작 합니다. 관리 및 모니터링 Linux 계산 노드 수 hello 동일한 방식으로 Windows를 사용 하는 계산 노드. 에 나열 된 hello Linux 노드를 참조 하는 예를 들어 **리소스 관리** (이러한 노드가 hello로 배포 **LinuxNode** 템플릿).

![노드 관리][management]

Hello에 hello Linux 노드에 표시 **열 지도** 보기.

![열 지도][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a>어떻게 Linux 노드에 있는 클러스터의 toomove 데이터
Linux 노드 및 hello Windows hello 클러스터의 헤드 노드 간에 여러 선택 항목 toomove 데이터 해야합니다. Hello 다음 섹션에서에서 자세히 설명 하는 세 가지 일반적인 방법 다음과 같습니다.

* **Azure 파일** -Azure 저장소에 관리 되는 SMB 파일 공유 toostore 데이터 파일을 노출 합니다. Windows 노드 및 Linux 노드 드라이브 또는 폴더에 hello Azure 파일 공유를 탑재할 수 서로 다른 가상 네트워크에 배포 되는 경우에 이와 합니다.
* **헤드 노드 SMB 공유** -Linux 노드에 hello 헤드 노드의 표준 Windows 공유 폴더를 탑재 합니다.
* **헤드 노드 NFS 서버** - Windows 및 Linux 혼합 환경에 대한 파일 공유 솔루션을 제공합니다.

### <a name="azure-file-storage"></a>Azure 파일 저장소
hello [Azure 파일](https://azure.microsoft.com/services/storage/files/) 서비스는 hello 표준 SMB 2.1 프로토콜을 사용 하 여 파일 공유를 노출 합니다. Azure Vm 및 클라우드 서비스를 통해 탑재 된 공유 응용 프로그램 구성 요소에서 파일 데이터를 공유할 수 및 온-프레미스 응용 프로그램이 hello 파일 저장소 API 통해 공유에 파일 데이터를 액세스할 수 있습니다. 

자세한 단계 toocreate Azure 파일 공유 하 고 hello 헤드 노드에서 탑재에 대 한 참조 [Windows에서 Azure 파일 저장소 시작](../../../storage/files/storage-how-to-use-files-windows.md)합니다. hello Linux 노드에 toomount hello Azure 파일 공유 참조 [어떻게 toouse Azure 파일 저장소와 Linux](../../../storage/files/storage-how-to-use-files-linux.md)합니다. 영구 연결을 tooset 참조 [Persisting 연결 tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)합니다.

다음 예제는 hello, 저장소 계정에서 Azure 파일 공유를 만듭니다. toomount hello hello 헤드 노드를 열고 명령 프롬프트를 공유 하 고 hello 명령 다음을 입력 합니다.

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

이 예제에서는 allvhdsje 저장소 계정 이름 storageaccountkey 저장소 계정 키가 있고, rdma는 hello Azure 파일 공유 이름입니다. hello Azure 파일 공유는 hello 헤드 노드에서 z:로 탑재 됩니다.

실행 되는 Linux 노드 toomount hello Azure 파일 공유는 **clusrun** hello 헤드 노드에서 명령을 합니다. **[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  여러 노드에서 관리 작업 유용한 HPC Pack 도구 toocarry 됩니다. 이 문서의 [Linux 노드에 대한 Clusrun](#Clusrun-for-Linux-nodes) 도 참조하세요.

Windows PowerShell 창을 열고 다음 명령을 hello를 입력 합니다.

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

첫 번째 명령은 hello hello LinuxNodes 그룹의 모든 노드에서 /rdma 라는 폴더를 만듭니다. 두 번째 명령은 hello hello Azure 파일 공유 allvhdsjw.file.core.windows.net/rdma dir 및 파일 모드 비트 집합 too777 hello /rdma 폴더에 탑재합니다. Hello 두 번째 명령에서 allvhdsje은 저장소 계정 이름 및 storageaccountkey 저장소 계정 키입니다.

> [!NOTE]
> hello "\`" hello 두 번째 명령은의 기호는 PowerShell에 대 한 이스케이프 기호는 합니다. "\`,"의미 해당 hello"," (쉼표 문자)는 hello 명령의 일부입니다.
> 
> 

### <a name="head-node-share"></a>헤드 노드 공유
Linux 노드에 헤드 노드 hello의 공유 폴더를 탑재 또는 합니다. 공유 hello 가장 간단한 방법은 tooshare 파일을 제공 하지만 hello에 hello 헤드 노드 및 모든 Linux 노드를 배포 해야 동일한 가상 네트워크입니다. Hello 단계는 다음과 같습니다.

1. Hello 헤드 노드에 폴더를 만들고 읽기/쓰기 권한을 가진 tooEveryone을 공유 합니다. 예를 들어 hello 헤드 노드의 D:\OpenFOAM 공유 \\CentOS7RDMA HN\OpenFOAM 합니다. 다음 CentOS7RDMA HN은 hello 헤드 노드의 hello 호스트 이름입니다.
   
    ![파일 공유 권한][fileshareperms]
   
    ![파일 공유][filesharing]
2. Windows PowerShell 창을 열고 다음 명령을 hello를 실행 합니다.
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

첫 번째 명령은 hello hello LinuxNodes 그룹의 모든 노드에서 /openfoam 라는 폴더를 만듭니다. 두 번째 명령은 hello hello 공유 폴더 //CentOS7RDMA-HN/OpenFOAM dir 및 파일 모드 비트 집합 too777 hello 폴더에 탑재합니다. hello 사용자 이름 및 암호 hello 명령에 해야 hello 사용자 이름 및 hello 헤드 노드에서 클러스터 사용자의 암호입니다. ( [클러스터 사용자 추가 또는 제거](https://technet.microsoft.com/library/ff919330.aspx)참조)

> [!NOTE]
> hello "\`" hello 두 번째 명령은의 기호는 PowerShell에 대 한 이스케이프 기호는 합니다. "\`,"의미 해당 hello"," (쉼표 문자)는 hello 명령의 일부입니다.
> 
> 

### <a name="nfs-server"></a>NFS 서버
hello NFS 서비스 tooshare 있으며 hello SMB 프로토콜을 사용 하 여 hello Windows Server 2012 운영 체제를 실행 하는 컴퓨터와 hello NFS 프로토콜을 사용 하 여 Linux 기반 컴퓨터 간의 파일 마이그레이션할 합니다. hello NFS 서버와 다른 모든 노드에 있는 toobe hello에 배포 된 동일한 가상 네트워크입니다. SMB 공유에 비해 Linux 노드와의 호환성이 향상됩니다. 예를 들어 파일 링크를 지원합니다.

1. NFS 서버를 설치한 집합과 tooinstall hello 단계에 따라 [네트워크 파일 시스템에 대 한 첫 번째 공유 종단에 대 한 서버](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx)합니다.
   
    예를 들어 다음과 같은 속성 hello로 nfs 라는 NFS 공유를 만듭니다.
   
    ![NFS 권한 부여][nfsauth]
   
    ![NFS 공유 권한][nfsshare]
   
    ![NFS NTFS 사용 권한][nfsperm]
   
    ![NFS 관리 속성][nfsmanage]
2. Windows PowerShell 창을 열고 다음 명령을 hello를 실행 합니다.
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   첫 번째 명령은 hello hello LinuxNodes 그룹의 모든 노드에서 /nfsshared 라는 폴더를 만듭니다. hello 두 번째 명령은 마운트 hello NFS 공유 CentOS7RDMA HN:에 nfs hello 폴더 / 합니다. 여기 CentOS7RDMA HN: / nfs는 NFS 공유의 hello 원격 경로입니다.

## <a name="how-toosubmit-jobs"></a>어떻게 toosubmit 작업
여러 가지 방법으로 toosubmit 작업 toohello HPC Pack 클러스터 가지가 있습니다.

* HPC 클러스터 관리자 또는 HPC 작업 관리자 GUI
* HPC 웹 포털
* REST API

Azure의 HPC 팩 GUI 도구 및 hello HPC 웹 포털을 통해 toohello 클러스터는 동일한 Windows 계산 노드: hello 작업 제출 합니다. 참조 [HPC 팩 작업 관리자](https://technet.microsoft.com/library/ff919691.aspx) 및 [toosubmit 온-프레미스 클라이언트 컴퓨터에서 작업 하는 방법을](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

hello REST API를 통해 toosubmit 작업 너무 참조[만들기 및 사용 하 여 작업을 제출 hello Microsoft HPC Pack에서 REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx)합니다. Linux 클라이언트에서 toosubmit 작업은 또한 toohello Python 샘플 hello에 참조할 [HPC 팩 SDK](https://www.microsoft.com/download/details.aspx?id=47756)합니다.

## <a name="clusrun-for-linux-nodes"></a>Linux 노드에 대한 Clusrun
HPC Pack hello [clusrun](https://technet.microsoft.com/library/cc947685.aspx) 도구 명령 프롬프트 또는 HPC 클러스터 관리자를 통해 Linux 노드에 사용 되는 tooexecute 명령 일 수 있습니다. 다음은 몇 가지 기본적인 예입니다.

* Hello 클러스터의 모든 노드에서 현재 사용자 이름을 표시 합니다.
  
    ```command
    clusrun whoami
    ```
* Hello 설치 **gdb** 사용 하는 디버거 도구 **yum** hello linuxnodes 그룹화 하 고 다음 10 분 후 hello 노드를 다시 시작의 모든 노드에 있습니다.
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* Hello 클러스터의 각 숫자 1부터 각 Linux 노드 상의 1 초 동안 10 표시 하는 셸 스크립트를 만들고, 실행 hello 노드에서 출력을 즉시 표시 합니다.
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> Toouse 해야 특정 문자를 이스케이프 **clusrun** 명령입니다. 이 예에서 볼 수 있듯이 사용 하 여 ^ 명령 프롬프트 tooescape hello에 ">" 기호입니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* Hello 클러스터 tooa 많은 노드를 확장 하거나 hello 클러스터에서 Linux 워크 로드를 실행 하십시오. 예제는 [Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행](hpcpack-cluster-namd.md)을 참조하세요.
* 사용 하 여 클러스터 시도 [RDMA 가능, 계산 집약적인 Vm](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI 작업 합니다. 그에 대한 예는 [Azure의 Linux RDMA 클러스터에서 Microsoft HPC Pack을 사용하여 OpenFOAM 실행](hpcpack-cluster-openfoam.md)을 참조하세요.
* Linux 노드 온-프레미스 HPC Pack 클러스터에서 작업에 관심이 있는 경우 참조 hello [TechNet 설명서](https://technet.microsoft.com/library/mt595803.aspx)합니다.

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
