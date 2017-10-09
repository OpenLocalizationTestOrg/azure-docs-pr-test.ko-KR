---
title: "aaaUse 계산 집약적 배치와 함께 Azure Vm | Microsoft Docs"
description: "Azure 배치 풀에서 tootake 활용 RDMA 가능 또는 GPU 사용이 가능한 VM 크기 방법"
services: batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: danlep
ms.openlocfilehash: 6a462a5f2a44ddcec8bf4e5c200d444cac8fafe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-rdma-capable-or-gpu-enabled-instances-in-batch-pools"></a>Batch 풀에서 RDMA 가능 또는 GPU 가능 인스턴스 사용

toorun 특정 일괄 처리 작업이 tootake 활용 대규모 계산을 위해 설계 된 Azure VM 크기를 할 수 있습니다. 예를 들어 toorun 다중 인스턴스 [MPI 작업](batch-mpi.md), A8, A9, 선택할 수 있습니다 또는 H 시리즈 크기를 보유 한 네트워크 인터페이스에 대 한 직접 메모리 RDMA (원격 액세스). 이러한 크기 MPI 응용 프로그램을 가속화할 수 있는 노드 간 통신에 대 한 tooan InfiniBand 네트워크에 연결 합니다. 또는 CUDA 응용 프로그램의 경우 NVIDIA Tesla GPU(그래픽 처리 장치) 카드를 포함하는 N 시리즈 크기를 선택할 수 있습니다.

이 문서에서는 지침과 예제 toouse 일괄 처리 풀에 있는 Azure의 특별 한 크기의 일부입니다. 사양 및 백그라운드는 다음을 참조하세요.

* 고성능 계산 VM 크기([Linux](../virtual-machines/linux/sizes-hpc.md), [Windows](../virtual-machines/windows/sizes-hpc.md)) 

* GPU 가능 VM 크기([Linux](../virtual-machines/linux/sizes-gpu.md), [Windows](../virtual-machines/windows/sizes-gpu.md)) 


## <a name="subscription-and-account-limits"></a>구독 및 계정 제한

* **할당량** -하나 이상의 Azure 할당량 제한 hello 개수나 유형에 노드의 tooa 배치 풀을 추가할 수 있습니다. 사용자는 RDMA 가능, GPU 사용을 선택 하면 제한 된 가능성이 toobe 또는 다른 멀티 코어 VM 크기입니다. 만든 일괄 처리 계정 hello 유형에 따라 hello 할당량 toohello 계정 자체 또는 tooyour 구독을 적용할 수 있습니다.

    * Hello에 일괄 처리 계정을 만든 경우 **서비스 일괄** 구성 hello에 따라 제한 됩니다 [전용된 코어 할당량 일괄 처리 계정 별로](batch-quota-limit.md#resource-quotas)합니다. 기본적으로 이 할당량은 20개의 코어입니다. 별도 할당량이 적용 너무[Vm 낮은 우선 순위](batch-low-pri-vms.md)사용 하는 경우, 합니다. 

    * Hello에 hello 계정을 만든 경우 **사용자 구독** hello / 지역당 VM 코어 수를 제한 하는 구성에서 구독 합니다. [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요. 구독에는 HPC 및 GPU 인스턴스를 포함 하는 지역 할당량 toocertain VM 크기도 적용 됩니다. Hello 사용자 구독 구성에서 추가 할당량이 없습니다 toohello 일괄 처리 계정을 적용 합니다. 

  일괄 처리에서 특수화 된 VM 크기를 사용 하는 경우 하나 이상의 할당량 tooincrease 할 수 있습니다. 할당량 증가 열기 toorequest는 [온라인 고객 지원 요청](../azure-supportability/how-to-create-azure-support-request.md) 비용 없이 합니다.

* **지역 가용성** -계산 집약적인 Vm 하지 못할 수도 있습니다 일괄 처리 계정을 만들면 hello 지역에 있습니다. 크기는 사용할 수 있는, toocheck 참조 [지역에 따라 사용할 수 있는 제품](https://azure.microsoft.com/regions/services/)합니다.


## <a name="dependencies"></a>종속성

계산 집약적인 크기의 GPU 기능과 hello RDMA 특정 운영 체제에만 사용할 수 있습니다. 운영 체제에 따라 tooinstall 필요 하거나 추가 드라이버 또는 다른 소프트웨어를 구성할 수 있습니다. 다음 표에서 hello 이러한 종속성을 요약 합니다. 자세한 내용은 연결된 문서를 참조하세요. 옵션 tooconfigure 일괄 처리 풀에 대 한이 문서의 뒷부분을 참조 합니다.


### <a name="linux-pools---virtual-machine-configuration"></a>Linux 풀 - 가상 컴퓨터 구성

| 크기 | 기능 | 운영 체제 | 필수 소프트웨어 | 풀 설정 |
| -------- | -------- | ----- |  -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/linux/sizes-hpc.md#rdma-capable-instances) | RDMA | SUSE Linux Enterprise Server 12 HPC 또는<br/>CentOS 기반 HPC<br/>(Azure Marketplace) | Intel MPI 5 | 노드 간 통신 사용, 동시 작업 실행 사용 안 함 |
| [NC 시리즈*](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms) | NVIDIA Tesla K80 GPU | Ubuntu 16.04 LTS.<br/>Red Hat Enterprise Linux 7.3 또는<br/>CentOS 기반 7.3<br/>(Azure Marketplace) | NVIDIA CUDA Toolkit 8.0 드라이버 | 해당 없음 | 
| [NV 시리즈](../virtual-machines/linux/n-series-driver-setup.md#install-grid-drivers-for-nv-vms) | NVIDIA Tesla M60 GPU | Ubuntu 16.04 LTS<br/>Red Hat Enterprise Linux 7.3<br/>CentOS 기반 7.3<br/>(Azure Marketplace) | NVIDIA GRID 4.3 드라이버 | 해당 없음 |

*NC24r VM의 RDMA 연결은 Intel MPI와 CentOS 기반 7.3 HPC에서 지원됩니다.



### <a name="windows-pools---virtual-machine-configuration"></a>Windows 풀 - 가상 컴퓨터 구성

| 크기 | 기능 | 운영 체제 | 필수 소프트웨어 | 풀 설정 |
| -------- | ------ | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2 또는<br/>Windows Server 2012(Azure Marketplace) | Microsoft MPI 2012 R2 이상 또는<br/> Intel MPI 5<br/><br/>HpcVMDrivers Azure VM 확장 | 노드 간 통신 사용, 동시 작업 실행 사용 안 함 |
| [NC 시리즈*](../virtual-machines/windows/n-series-driver-setup.md) | NVIDIA Tesla K80 GPU | Windows Server 2016 또는 <br/>Windows Server 2012 R2(Azure Marketplace) | NVIDIA Tesla 드라이버 또는 CUDA Toolkit 8.0 드라이버| 해당 없음 | 
| [NV 시리즈](../virtual-machines/windows/n-series-driver-setup.md) | NVIDIA Tesla M60 GPU | Windows Server 2016 또는<br/>Windows Server 2012 R2(Azure Marketplace) | NVIDIA GRID 4.3 드라이버 | 해당 없음 |

*NC24r VM의 RDMA 연결은 HpcVMDrivers 확장 및 Microsoft MPI 또는 Intel MPI를 사용하는 Windows Server 2012 R2에서 지원됩니다.

### <a name="windows-pools---cloud-services-configuration"></a>Windows 풀 - 클라우드 서비스 구성

> [!NOTE]
> N 시리즈 크기 hello 클라우드 서비스 구성 사용 하 여 일괄 처리 풀에서 지원 되지 않습니다.
>

| 크기 | 기능 | 운영 체제 | 필수 소프트웨어 | 풀 설정 |
| -------- | ------- | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2,<br/>Windows Server 2012 또는<br/>Windows Server 2008 R2(게스트 OS 제품군) | Microsoft MPI 2012 R2 이상 또는<br/>Intel MPI 5<br/><br/>HpcVMDrivers Azure VM 확장 | 노드 간 통신 사용<br/> 동시 작업 실행 사용 안 함 |





## <a name="pool-configuration-options"></a>풀 구성 옵션

tooconfigure 일괄 처리 풀, 일괄 처리 Api hello 및 도구에 대 한 특수 한 VM 크기가 몇 가지 옵션 tooinstall 필요한 소프트웨어 또는 포함 하 여 드라이버를 제공 합니다.

* [시작 작업](batch-api-basics.md#start-task) -리소스 파일 tooan hello에 대 한 Azure 저장소 계정으로 설치 패키지를 업로드할 hello 배치 계정과 같은 지역입니다. Hello 풀 시작 될 때 시작 작업이 명령줄 tooinstall hello 리소스 파일을 자동으로 만듭니다. 자세한 내용은 참조 hello [REST API 문서](/rest/api/batchservice/add-a-pool-to-an-account#bk_starttask)합니다.

  > [!NOTE] 
  > hello 시작 태스크를 관리자 권한 (관리자) 권한으로 실행 해야 하 고 성공에 대 한 대기 해야 합니다.
  >

* [응용 프로그램 패키지](batch-application-packages.md) -압축 된 설치 패키지 tooyour 일괄 처리 계정을 추가 하 고 hello 풀에서 패키지 참조를 구성 합니다. 이 설정은 hello 풀의 모든 노드에서 hello 패키지 압축을 풀고와 업로드 했습니다. Hello 패키지 설치 관리자 인 경우 모든 풀 노드에서 시작 작업이 명령줄 toosilently 설치 hello 앱을 만듭니다. 필요에 따라 작업 노드에서 예약 된 toorun 있을 때에 hello 패키지를 설치 합니다.

* [사용자 정의 풀 이미지](batch-api-basics.md#pool) -사용자 지정 창 만들기 또는 VM 크기 hello에 필요한 드라이버, 소프트웨어 또는 기타 설정을 포함 하는 Linux VM 이미지입니다. Hello 사용자 구독 구성에서 일괄 처리 계정이 만든 경우 hello 일괄 처리 풀에 대 한 사용자 지정 이미지를 지정 합니다. (사용자 지정 이미지 hello 일괄 처리 서비스 구성에는 계정에는 지원 되지 않습니다.) 사용자 지정 이미지 hello 가상 컴퓨터 구성에서 풀과만 사용할 수 있습니다.

  > [!IMPORTANT]
  > Batch 풀에서 Managed Disks 또는 Premium Storage로 만든 사용자 지정 이미지를 현재 사용할 수 없습니다.
  >



* [대형 조선소 일괄 처리](https://github.com/Azure/batch-shipyard) 자동으로 Azure 일괄 처리에 대 한 컨테이너 화 된 작업으로 hello GPU 및 RDMA toowork를 투명 하 게 구성 합니다. Batch Shipyard는 구성 파일에 의해 전적으로 결정됩니다. 여러 가지 샘플 레시피 구성이 사용할 수 있는 hello 등과 같은 GPU 및 RDMA의 작업을 사용할 수 있는 [CNTK GPU 레시피](https://github.com/Azure/batch-shipyard/tree/master/recipes/CNTK-GPU-OpenMPI) N 시리즈 Vm에서 GPU 드라이버를 미리 구성 하 고 Microsoft Cognitive Toolkit 소프트웨어는 Docker 이미지를 로드 합니다.


## <a name="example-microsoft-mpi-on-an-a8-vm-pool"></a>예제: A8 VM 풀의 Microsoft MPI

Azure A8 노드의 풀에서 toorun Windows MPI 응용 프로그램, tooinstall 지원 되는 MPI 구현 해야합니다. 다음은 샘플 단계 tooinstall [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) windows 일괄 처리 응용 프로그램 패키지를 사용 하 여 풀입니다.

1. Hello 다운로드 [설치 패키지](http://go.microsoft.com/FWLink/p/?LinkID=389556) (MSMpiSetup.exe) hello Microsoft MPI의 최신 버전에 대 한 합니다.
2. Hello 패키지의 zip 파일을 만듭니다.
3. Hello 패키지 tooyour 일괄 처리 계정에 업로드 합니다. 단계를 참조 hello [응용 프로그램 패키지](batch-application-packages.md) 지침. *MSMPI*와 같은 응용 프로그램 ID 및 *8.1*과 같은 버전을 지정합니다. 
4. Hello 일괄 처리 Api 또는 Azure 포털을 사용, 노드 및 눈금의 원하는 hello 번호로 hello 클라우드 서비스 구성에서 풀을 만들. hello 아래 표에 나와 MPI 샘플 설정 tooset 시작 태스크를 사용 하 여 무인된 모드에서.

| 설정 | 값 |
| ---- | ----- | 
| **이미지 형식** | 클라우드 서비스 |
| **OS 제품군** | Windows Server 2012 R2(OS 제품군 4) |
| **노드 크기** | A8 표준 |
| **노드 간 통신 사용** | True |
| **노드당 최대 작업** | 1 |
| **응용 프로그램 패키지 참조** | MSMPI |
| **시작 작업 사용** | True<br>**명령 줄** - `"cmd /c %AZ_BATCH_APP_PACKAGE_MSMPI#8.1%\\MSMpiSetup.exe -unattend -force"`<br/>**사용자 ID** - 풀 autouser, 관리자<br/>**성공 대기** - True

## <a name="example-nvidia-tesla-drivers-on-nc-vm-pool"></a>예제: NC VM 풀의 NVIDIA Tesla 드라이버

toorun CUDA Linux NC 노드의 풀에서 응용 프로그램을 hello 노드에서 CUDA 도구 키트 8.0 tooinstall을 해야합니다. hello Toolkit hello 필요한 NVIDIA 테슬라 GPU 드라이버를 설치합니다. 다음은 샘플 단계 toodeploy hello GPU 드라이버와 함께 사용자 지정 16.04 Ubuntu LTS 이미지입니다.

1. Ubuntu 16.04 LTS를 실행하는 Azure NC6 VM을 배포합니다. 예를 들어 hello 미국 남부 중부 지역에 hello VM을 만듭니다. 표준 저장소도 hello VM을 만드는 있는지 확인 하 고 *없이* 디스크를 관리 합니다.
2. Hello 단계 tooconnect toohello VM에 따라 및 [CUDA 드라이버 설치](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms)합니다.
3. Hello Linux 에이전트를 프로 비전 해제 하 고 hello Azure CLI 1.0 명령을 사용 하 여 Linux VM 이미지를 캡처하십시오. 단계는 [Azure에서 실행되는 Linux 가상 컴퓨터 캡처하기](../virtual-machines/linux/capture-image-nodejs.md)를 참조하세요. Hello 이미지 URI 적어 둡니다.
  > [!IMPORTANT]
  > Azure 일괄 처리에 대 한 Azure CLI 2.0 명령 toocapture hello 이미지를 사용 하지 마십시오. 현재 hello CLI 2.0 명령은 관리 되는 디스크를 사용 하 여 만든 Vm을 캡처합니다.
  >
4. Hello 사용자 구독 구성 NC Vm을 지 원하는 있는 영역에 포함 된 일괄 처리 계정 만들기
5. Hello 사용자 지정 이미지를 사용 하 여 풀 hello 일괄 처리 Api 또는 Azure 포털을 사용 하 여 만들고 hello로 원하는 노드 및 소수 자릿수의 숫자입니다. hello 아래 표에 나와 hello 이미지에 대 한 샘플 풀 설정.

| 설정 | 값 |
| ---- | ---- |
| **이미지 형식** | 사용자 지정 이미지 |
| **사용자 지정 이미지** | 이미지 hello 폼의 URI`https://yourstorageaccountdisks.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd` |
| **노드 에이전트 SKU** | batch.node.ubuntu 16.04 |
| **노드 크기** | NC6 표준 |



## <a name="next-steps"></a>다음 단계

* Azure 배치 풀에서 MPI 작업을 toorun 참조 hello [Windows](batch-mpi.md) 또는 [Linux](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/) 예제입니다.

* 일괄 처리에서 GPU 작업의 예 hello 참조 [일괄 처리 대형 조선소](https://github.com/Azure/batch-shipyard/) 레시피 합니다.
