---
title: "aaaRun 별-Linux Vm에서 HPC Pack을 사용한 CCM + | Microsoft Docs"
description: "Azure에서 Microsoft HPC Pack 클러스터를 배포하고 RDMA 네트워크 간의 여러 Linux 계산 노드에서 STAR-CCM+ 작업을 실행합니다."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Azure의 Linux RDMA 클러스터에서 Microsoft HPC 팩으로 STAR-CCM+ 실행
이 문서에서는 Azure와 실행에 toodeploy Microsoft HPC Pack 클러스터 어떻게는 [CD adapco 별-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) InfiniBand와 상호 연결 되는 여러 Linux 계산 노드에서 작업입니다.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Microsoft HPC Pack 기능 toorun 다양 한 대규모 HPC 및 Microsoft Azure 가상 컴퓨터의 클러스터에서 MPI 응용 프로그램을 포함 하 여 병렬 응용 프로그램을 제공 합니다. HPC 팩은 HPC 팩 클러스터에 배포된 Linux 계산 노드 VM에서 Linux HPC 응용 프로그램의 실행도 지원합니다. 소개 toousing Linux 계산 노드 HPC Pack을 사용한, 참조 [Azure에서 HPC Pack 클러스터에서 계산 노드 Linux 시작](hpcpack-cluster.md)합니다.

## <a name="set-up-an-hpc-pack-cluster"></a>HPC 팩 클러스터 설정
Hello에서 hello HPC Pack IaaS 배포 스크립트를 다운로드 [다운로드 센터](https://www.microsoft.com/en-us/download/details.aspx?id=44949) 로컬로 압축을 풉니다.

Azure PowerShell은 필수 요소입니다. 로컬 컴퓨터에서 PowerShell 구성 되지 않은 경우 hello 문서를 참조 하세요 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

이 문서 작성 hello 시 hello Azure 마켓플레이스 (을 Azure에 대 한 hello InfiniBand 드라이버 포함)에서 hello Linux 이미지 SLES 12, CentOS 6.5 및 CentOS 7.1 됩니다. 이 문서는 SLES 12 hello 사용을 기반으로 합니다. 모든 Linux 이미지에서 지 원하는 HPC hello 마켓플레이스 tooretrieve hello 이름 hello 다음 PowerShell 명령을 실행할 수 있습니다.

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

이러한 이미지 사용할 수 있는 및 이미지 이름 hello hello 위치를 나열 하는 hello 출력 (**ImageName**) toobe hello 배포 템플릿에 나중에 사용 합니다.

Hello 클러스터를 배포 하기 전에 해야 toobuild HPC Pack 배포 템플릿 파일. 작은 클러스터를 대상으로 하는 hello 헤드 노드 hello 도메인 컨트롤러일 되며 로컬 SQL 데이터베이스를 호스트 합니다.

hello 다음 서식 파일은 헤드 노드를 배포, 라는 XML 파일을 만들고 **MyCluster.xml**, 및의 hello 값 바꾸기 **SubscriptionId**, **StorageAccount**,  **위치**, **VMName**, 및 **ServiceName** 기업과 합니다.

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

관리자 권한 명령 프롬프트에서 hello PowerShell 명령을 실행 하 여 hello 헤드 노드 만들기를 시작 합니다.

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

20 too30 분 hello 헤드 노드를 준비 해야 합니다. Hello를 클릭 하 여 tooit hello Azure 포털에서에서 연결할 수 있습니다 **연결** hello 가상 컴퓨터의 아이콘입니다.

결국 toofix hello DNS 전달자를 할 수 있습니다. 따라서 toodo DNS 관리자를 시작 합니다.

1. 마우스 오른쪽 단추로 클릭 hello 서버 이름에 DNS 관리자를 선택 **속성**, hello를 클릭 한 다음 **전달자** 탭 합니다.
2. Hello 클릭 **편집** tooremove 모든 전달자 단추를 선택한 다음 클릭 **확인**합니다.
3. 해당 hello 있는지 확인 **없는 전달자를 사용할 수 있는 경우에 루트 힌트를 사용 하 여** 확인란을 선택한 다음 클릭 **확인**합니다.

## <a name="set-up-linux-compute-nodes"></a>Linux 계산 노드 설정
Hello를 사용 하 여 hello Linux 계산 노드를 배포할 toocreate hello 헤드 노드를 사용 하 여 동일한 배포 템플릿.

Hello 파일 복사 **MyCluster.xml** 로컬 컴퓨터 toohello 헤드 노드 및 업데이트 hello **NodeCount** toodeploy 원하는 노드의 hello 번호로 태그 (< = 20). 때문일 신중 하 게 toohave Azure 할당량을 사용할 수 있는 충분 한 코어가 A9 인스턴스 각 구독에 코어 16 개를 사용 합니다. Toouse hello에 더 많은 Vm을 원하는 경우 A9 대신 A8 인스턴스 (8 코어)를 사용할 수 있습니다 동일한 예산 합니다.

Hello 헤드 노드에서 hello HPC Pack IaaS 배포 스크립트를 복사 합니다.

Hello Azure PowerShell 명령을 관리자 권한 명령 프롬프트에서 다음을 실행 합니다.

1. 실행 **Add-azureaccount** tooconnect tooyour Azure 구독.
2. 여러 구독이 있는 경우 실행 **Get-azuresubscription** toolist 해당 합니다.
3. Hello를 실행 하 여 기본 구독 설정 **선택-SubscriptionName xxxx-기본** 명령입니다.
4. 실행 **.\New-HPCIaaSCluster.ps1-ConfigFile MyCluster.xml** toostart Linux 계산 노드를 배포 합니다.
   
   ![헤드 노드 배포 작업][hndeploy]

Hello HPC 팩 클러스터 관리자 도구를 엽니다. 몇 분 후에 클러스터 계산 노드 목록에 Linux 계산 노드가 정기적으로 나타납니다. Hello 클래식 배포 모드에서 IaaS Vm 순차적으로 생성 됩니다. 따라서 노드 수가 hello 중요 한 경우 배포 된 모든 가져오기 상당한 시간이 걸릴 수 있습니다.

![HPC 팩 클러스터 관리자의 Linux 노드][clustermanager]

이제 모든 노드가 실행 중에 hello 클러스터, 추가 인프라 설정 toomake가 있습니다.

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a>Windows 및 Linux 노드에 대한 Azure 파일 공유 설정
Hello Azure 파일 서비스 toostore 스크립트, 응용 프로그램 패키지 및 데이터 파일을 사용할 수 있습니다. Azure 파일은 Azure Blob 저장소를 영구 저장소로 사용하면서 CIFS 기능을 제공합니다. 이 hello 가장 확장성이 뛰어난 솔루션을 아니라 hello 가장 간단한 하나 되 고 전용된 Vm 하지 않아도 됩니다.

Hello hello 문서의 지침에 따라 Azure 파일 공유 만들기 [Windows에서 Azure 파일 저장소 시작](../../../storage/files/storage-dotnet-how-to-use-files.md)합니다.

사용자의 저장소 계정으로 hello 이름을 유지 **saname**, hello 파일 공유 이름으로 **sharename**, 및 hello 저장소 계정 키로 **sakey**합니다.

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a>Hello Azure 파일 공유 hello 헤드 노드에 탑재 하십시오.
관리자 권한 명령 프롬프트를 열고 hello 명령 toostore hello 자격 증명 hello 로컬 컴퓨터 자격 증명 모음에 다음을 실행 합니다.

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

그런 다음 toomount hello Azure 파일 공유를 실행 합니다.

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a>Hello Azure 파일 공유 Linux 계산 노드에 탑재 하십시오.
HPC Pack과 함께 제공 되는 유용한 도구는 hello clusrun 도구입니다. 계산 노드 집합에 동일 명령이 명령줄 도구 toorun hello를 동시에 사용할 수 있습니다. 이 경우에이 클래스는 toomount hello Azure 파일 공유를 사용 하는 고 toosurvive 재부팅을 유지 합니다.
Hello 헤드 노드에서 관리자 권한 명령 프롬프트에서 다음 명령을 hello를 실행 합니다.

toocreate hello 탑재 디렉터리:

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

toomount hello Azure 파일 공유:

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

toopersist hello 탑재 공유:

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a>STAR-CCM+ 설치
Azure VM 인스턴스 A8 및 A9는 InfiniBand 지원 및 RDMA 기능을 제공합니다. 이러한 기능을 사용 하는 hello 커널 드라이버는 Windows Server 2012 R2, SUSE 12, CentOS 6.5 및 CentOS 7.1 이미지 hello Azure 마켓플레이스를에서 사용할 수 있습니다. Microsoft MPI 및 Intel MPI (5.x 릴리스)는 Azure에서 해당 드라이버를 지 hello 두 하는 MPI 라이브러리입니다.

CD-adapco STAR-CCM+ 릴리스 11.x 이상은 Intel MPI 버전 5.x와 함께 제공되므로 Azure에 대한 InfiniBand 지원이 포함됩니다.

Hello Linux64 가져오기 별-hello에서 CCM + 패키지 [CD adapco 포털](https://steve.cd-adapco.com)합니다. 이 경우에는 혼합 정밀도의 버전 11.02.010을 사용했습니다.

Hello에서 hello 헤드 노드 **/hpcdata** Azure 파일 공유, 라는 셸 스크립트를 만들고 **setupstarccm.sh** 콘텐츠를 다음 hello로 합니다. 각 계산 노드 tooset 별 구성에이 스크립트가 실행 될-CCM + 로컬로 합니다.

#### <a name="sample-setupstarcmsh-script"></a>샘플 setupstarcm.sh 스크립트
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
이제 tooset 별을-CCM + 프로그램 모든 Linux에서 계산 노드, 관리자 권한 명령 프롬프트를 열고 및 hello 다음 명령을 실행 합니다.

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

Hello 명령을 실행 하는 동안에 클러스터 관리자의 hello 열 지도 사용 하 여 hello CPU 사용량을 모니터링할 수 있습니다. 몇 분 후 모든 노드가 올바르게 설정됩니다.

## <a name="run-star-ccm-jobs"></a>STAR-CCM+ 작업 실행
HPC Pack 순서 toorun 별에에서 그 작업 스케줄러 기능에 사용 되-CCM + 작업 합니다. toodo, 사용 되는 toostart hello 작업 되 고 별표를 실행 하는 몇 가지 스크립트의 지원 hello 필요 म-CCM + 합니다. 입력된 데이터 hello 편의 위해 첫 번째 hello Azure 파일 공유에 보관 됩니다.

PowerShell 스크립트 뒤 hello가 사용 되는 tooqueue 별-CCM + 작업 합니다. 3가지 인수를 사용합니다.

* hello 모델 이름
* 사용 되는 노드 toobe hello 수
* hello 사용 되는 각 노드 toobe의 코어 수

때문에 별-CCM + hello 메모리 대역폭을 채울 수 있는의 일반적으로 더 나은 toouse 당 코어 적은 계산 노드 및 새 노드를 추가 합니다. 노드당 코어 수를 정확 하 게 hello hello 프로세서 제품군 및 hello 상호 연결 속도에 따라 달라 집니다.

hello 노드 hello 작업에 대 한 단독으로 할당 되 고 다른 작업와 공유할 수 없습니다. hello 작업 직접 MPI 작업으로 시작 되지 않았습니다. hello **runstarccm.sh** 셸 스크립트 hello MPI 시작 관리자를 시작 합니다.

hello 입력 모델 및 hello **runstarccm.sh** hello에 스크립트 저장 **/hpcdata** 이전에 탑재 된 공유 합니다.

로그 파일 hello 작업 ID를 가진 명명 되 고 hello에 저장 된 **/hpcdata 공유**, 스타 hello 함께-CCM + 출력 파일입니다.

#### <a name="sample-submitstarccmjobps1-script"></a>샘플 SubmitStarccmJob.ps1 스크립트
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
**runner.java** 를 원하는 STAR-CCM+ java 모델 시작 관리자와 로깅 코드로 바꿉니다.

#### <a name="sample-runstarccmsh-script"></a>샘플 runstarccm.sh 스크립트
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

이 테스트에서는 Power-On-Demand 라이선스 토큰을 사용했습니다. 이 토큰에 대 한 tooset hello 있는 **$CDLMD_LICENSE_FILE** 환경 변수 너무 **1999@flex.cd-adapco.com**  hello에 대 한 hello 키를 **-podkey** hello 명령줄 옵션 .

일부 초기화 된 후 hello 스크립트-에서 추출 hello **$CCP_NODES_CORES** HPC Pack 설정-환경 변수를 사용 하 여 MPI launcher hello는 hostfile 노드 toobuild 목록이 hello 합니다. 이 hostfile hello hello 작업을 한 줄에 하나의 이름에 사용 되는 계산 노드 이름 목록이 포함 됩니다.

hello 형식의 **$CCP_NODES_CORES** 이 패턴을 따릅니다.

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

여기서,

* `<Number of nodes>`hello toothis 작업에 할당 된 노드 수가입니다.
* `<Name of node_n_...>`hello toothis 작업에 할당 된 각 노드 이름이입니다.
* `<Cores of node_n_...>`hello hello 노드의 toothis 작업에 할당 된 코어 수가입니다.

그러나 코어 수가 hello (**$NBCORES**) 노드 수에 따라 계산 된 hello 이기도 (**$NBNODES**) hello 노드당 코어 수 및 (매개 변수로 제공 **$NBCORESPERNODE**).

Hello MPI 옵션 hello Azure에서 MPI Intel 함께 사용 되는 것과 다음과 같습니다.

* `-mpi intel`Intel MPI toospecify 합니다.
* `-fabric UDAPL`Azure의 InfiniBand 동사를 toouse 합니다.
* `-cpubind bandwidth,v`별이 있는 MPI에 대 한 toooptimize 대역폭-CCM + 합니다.
* `-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`Azure의 InfiniBand toomake Intel MPI 작업 및 tooset hello 필요한 노드당 코어 수입니다.
* `-batch`toostart 별-CCM + 일괄 처리 모드에서 ui 없는 합니다.

마지막으로, toostart 작업을 된 노드가 실행 중 이며 클러스터 관리자에서 온라인 상태 인지 확인 합니다. 그런 다음 PowerShell 명령 창에서 다음을 실행합니다.

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a>노드 중지
나중에 테스트를 마친 후 HPC 팩 PowerShell 명령을 toostop 다음 hello를 사용 하 고 노드를 시작할 수 있습니다.

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a>다음 단계
다른 Linux 워크로드를 실행해 봅니다. 예를 들어 다음을 참조하세요.

* [Azure의 Linux 계산 노드에서 Microsoft HPC 팩을 사용하여 NAMD 실행](hpcpack-cluster-namd.md)
* [Azure의 Linux RDMA 클러스터에서 Microsoft HPC 팩을 사용하여 OpenFOAM 실행](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
