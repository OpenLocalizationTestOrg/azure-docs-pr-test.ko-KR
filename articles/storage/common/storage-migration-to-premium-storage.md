---
title: "프리미엄 저장소 aaaMigrating Vm tooAzure | Microsoft Docs"
description: "프로그램 기존 Vm tooAzure 프리미엄 저장소를 마이그레이션하십시오. 프리미엄 저장소는 Azure 가상 컴퓨터에서 실행되는 I/O 사용량이 많은 작업에 대해 대기 시간이 짧은 고성능 디스크 지원을 제공합니다."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a>마이그레이션 tooAzure 프리미엄 저장소 (관리 되지 않는 디스크)

> [!NOTE]
> 이 문서에서는 toomigrate tooa 관리 되지 않는 표준 디스크를 사용 하는 VM을 사용 하는 VM에서 프리미엄 디스크를 관리 하는 방법을 설명 합니다. 새 Vm에 Azure 관리 되는 디스크를 사용 하 고 이전 관리 되지 않는 디스크 toomanaged 디스크를 변환 하는 것이 좋습니다. 관리 디스크 핸들 hello 기본 저장소 계정 하므로 필요가 없습니다. 자세한 내용은 [Managed Disks 개요](../../virtual-machines/windows/managed-disks-overview.md)를 참조하세요.
>

Azure 프리미엄 저장소는 I/O 사용량이 많은 작업을 실행하는 가상 컴퓨터에서 대기 시간이 짧은 고성능 디스크 지원을 제공합니다. Hello 속도 활용 하 고 이러한 디스크는 성능 응용 프로그램의 VM 디스크 tooAzure 프리미엄 저장소를 마이그레이션하여 취할 수 있습니다.

이 가이드의 hello 목적은 toohelp 더 나은 Azure 프리미엄 저장소의 새 사용자가 자신의 현재 시스템 tooPremium 저장소에서에서 부드럽게 전환 toomake 준비입니다. hello 가이드 hello이이 과정의 주요 구성 요소 중 3 개 해결할 수 있습니다.

* [Hello 마이그레이션 tooPremium 저장소에 대 한 계획](#plan-the-migration-to-premium-storage)
* [준비 및 복사 가상 하드 디스크 (Vhd) tooPremium 저장소](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [Premium Storage를 사용하여 Azure 가상 컴퓨터 만들기](#create-azure-virtual-machine-using-premium-storage)

다른 플랫폼 tooAzure 프리미엄 저장소에서에서 Vm을 마이그레이션할 수도 있고 표준 저장소 tooPremium 저장소에서에서 기존 Azure Vm을 마이그레이션할 수도 있습니다. 이 가이드에서는 두 시나리오의 단계를 다룹니다. 시나리오에 따라 hello 관련 섹션에 지정 된 hello 단계를 수행 합니다.

> [!NOTE]
> Premium Storage의 기능 개요 및 가격 책정은 Premium Storage: [Azure 가상 컴퓨터 워크로드를 위한 고성능 저장소](storage-premium-storage.md)를 참조하세요. 응용 프로그램에 대 한 hello 최상의 성능을 위해 높은 IOPS tooAzure 프리미엄 저장소를 필요로 하는 가상 컴퓨터 디스크를 마이그레이션하는 것이 좋습니다. 디스크에 높은 IOPS가 필요하지 않은 경우, 가상 컴퓨터 디스크 데이터를 SSD가 아닌 하드 디스크 드라이브(HDD)에 저자하는 표준 저장소를 사용하여 비용을 절약할 수 있습니다.
>

이 가이드에서 제공 하는 hello 단계 앞뒤 모두 hello 마이그레이션 프로세스 완료의 전체 추가 작업 필요할 수 있습니다. Hello 응용 프로그램 내에서 자체 응용 프로그램에서 가동 중지 시간이 필요할 수 있는 코드를 변경 하거나 가상 네트워크 또는 끝점을 구성을 예로 들 수 있습니다. 이러한 작업은 고유한 tooeach 응용 프로그램 및이 가이드 toomake hello 전체 전환 tooPremium 최대한 원활 하 게 저장소에에서 제공 된 hello 단계와 함께 완료 해야 합니다.

## <a name="plan-the-migration-to-premium-storage"></a>Hello 마이그레이션 tooPremium 저장소에 대 한 계획
이 섹션 준비 toofollow이 문서의 hello 마이그레이션 단계는 toomake hello 최선의 결정 VM 및 디스크 유형에 대를 사용 하면을 확인 합니다.

### <a name="prerequisites"></a>필수 조건
* Azure 구독이 필요합니다. 구독이 없다면, 한 달의 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 구독하거나 [Azure 가격 책정](https://azure.microsoft.com/pricing/)을 방문하여 추가 옵션을 참고합니다.
* PowerShell cmdlet tooexecute hello Microsoft Azure PowerShell 모듈을 해야 합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello에 대 한 지점 및 설치 지침을 설치 합니다.
* 프리미엄 저장소에서 실행 하는 Azure Vm toouse를 계획할 때는 toouse hello 프리미엄 저장소 가능 Vm 해야 합니다. Premium Storage 지원 VM에서 표준 저장소 디스크와 Premium Storage 디스크를 모두 사용할 수 있습니다. 프리미엄 저장소 디스크는 이후 hello에서 더 많은 VM 형식과 함께 사용할 수 있습니다. 사용 가능한 Azure VM 디스크 유형 및 크기에 대한 자세한 내용은 [가상 컴퓨터 크기](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 및 [클라우드 서비스 크기](../../cloud-services/cloud-services-sizes-specs.md)를 참조하세요.

### <a name="considerations"></a>고려 사항
Azure VM 지원 응용 프로그램은 VM 당 저장소 too256 TB를 유지할 수 있도록 여러 프리미엄 저장소 디스크를 연결 합니다. 프리미엄 저장소를 사용할 경우 읽기 작업의 대기 시간이 매우 짧은 상태로 VM당 80,000 IOPS(초당 입/출력 작업 수) 및 VM당 디스크 처리량 초당 2000MB를 얻을 수 있습니다. 다양한 VM 및 디스크 옵션이 있습니다. 이 섹션은 toohelp toofind 워크 로드에 가장 적합 한 옵션입니다.

#### <a name="vm-sizes"></a>VM 크기
hello Azure VM 크기 사양에 나열 된 [가상 컴퓨터의 크기](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 프리미엄 저장소를 사용 하 고 작업에 가장 적합 한 hello 가장 적절 한 VM 크기를 선택 하는 가상 컴퓨터의 hello 성능 특성을 검토 합니다. VM toodrive hello 디스크 트래픽에 사용할 수 있는 충분 한 대역폭이 있는지 확인 합니다.

#### <a name="disk-sizes"></a>디스크 크기
VM에서 사용할 수 있는 디스크에는 다섯 종류가 있으며 각 종류에는 특정 IOP 및 처리량 제한이 있습니다. 이러한 제한은 때 고려해 용량, 성능, 확장성, 관점에서 응용 프로그램의 hello 요구 사항에 따라 VM에 대 한 hello 디스크 유형을 선택 하 고 최대 로드 합니다.

| 프리미엄 디스크 유형  | P10   | P20   | P30            | P40            | P50            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| 디스크 크기           | 128GB| 512GB| 1,024GB(1TB) | 2,048GB(2TB) | 4,095GB(4TB) | 
| 디스크당 IOPS       | 500   | 2,300  | 5,000           | 7,500           | 7,500           | 
| 디스크당 처리량 | 초당 100MB | 초당 150MB | 초당 200MB | 초당 250MB | 초당 250MB |

사용자 워크로드에 따라 추가 데이터 디스크가 VM에 필요한 경우를 결정합니다. 여러 영구 데이터 디스크 tooyour VM에 연결할 수 있습니다. 필요한 경우에 hello 디스크 tooincrease hello 용량 및 성능 hello 볼륨에 걸쳐 스트라이프 할 수 있습니다. (디스크 스트라이프란 무엇인지 [여기서](storage-premium-storage-performance.md#disk-striping) 확인하세요.) [저장소 공간][4]을 사용하여 프리미엄 저장소 데이터 디스크를 스트라이프하는 경우, 사용되는 각 디스크에 대해 하나의 열로 구성해야 합니다. 그렇지 않으면 hello 전반적인 성능이 hello 스트라이프 볼륨의 수 있습니다 hello 디스크에 걸쳐 트래픽의 toouneven 배포 인해 예상 보다 더 낮은. Linux Vm에 대 한 hello를 사용할 수 있습니다 *mdadm* 유틸리티 tooachieve hello 동일 합니다. 자세한 내용은 [Linux에서 소프트웨어 RAID 구성](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 문서를 참조하세요.

#### <a name="storage-account-scalability-targets"></a>저장소 계정의 확장성 목표
프리미엄 저장소 계정 추가 toohello의 확장성 목표를 수행 하는 hello가 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md)합니다. 응용 프로그램 요구 사항 단일 저장소 계정의 확장성 목표 hello를 초과 하는 경우 응용 프로그램 toouse 여러 저장소 계정을 빌드하고 해당 저장소 계정에서 데이터를 분할 합니다.

| 총 계정 용량 | 로컬 중복 저장소 계정의 총 대역폭 |
|:--- |:--- |
| 디스크 용량: 35TB<br />스냅숏 용량: 10TB |인바운드 + 아웃 바운드에 대 한 초당 기가 비트 too50 |

에 대 한 자세한 내용은 프리미엄 저장소 사양에 hello, 체크 아웃 [확장성 및 성능 목표 프리미엄 저장소를 사용 하는 경우](storage-premium-storage.md#scalability-and-performance-targets)합니다.

#### <a name="disk-caching-policy"></a>디스크 캐싱 정책
디스크 캐싱 정책은 기본적으로 *읽기 전용* 모든 hello 프리미엄 데이터 디스크에 대 한 및 *읽기 / 쓰기* hello 프리미엄 운영 체제 디스크에 대 한 toohello VM을 연결 합니다. 이 구성 설정은 응용 프로그램의 IOs 용 tooachieve hello 최적의 성능은 것이 좋습니다. 쓰기가 많거나 쓰기 전용인 디스크의 경우(예: SQL Server 로그 파일) 더 나은 응용 프로그램 성능을 얻기 위해 디스크 캐싱을 사용하지 않도록 설정합니다. 사용 하 여 기존 데이터 디스크에 대 한 hello 캐시 설정을 업데이트할 수 [Azure 포털](https://portal.azure.com) 또는 hello *-HostCaching* hello의 매개 변수 *Set-azuredatadisk* cmdlet.

#### <a name="location"></a>위치
Azure 프리미엄 저장소를 사용할 수 있는 위치를 선택합니다. 사용 가능한 위치에 대한 최신 정보는 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services)를 참조하세요. Hello에 Vm 있는 동일한 지역의 저장소 계정이 VM hello 별도 영역에 있는 경우에 비해 훨씬 더 나은 성능을 제공 됩니다에 대 한 저장소 디스크는 hello hello 합니다.

#### <a name="other-azure-vm-configuration-settings"></a>기타 Azure VM 구성 설정
Azure VM을 만들 때 됩니다 tooconfigure 특정 VM 설정은 라는 메시지가 표시 됩니다. 수정 하거나 나중에 다른 사용자를 추가 하는 동안 VM hello의 hello 수명 동안 고정 되는 설정 기억 하십시오. 이러한 Azure VM 구성 설정 검토 하 고 있는지 확인이 적절 하 게 구성 toomatch 작업 부하 요구 사항입니다.

### <a name="optimization"></a>최적화
[Azure Premium Storage: 고성능을 위한 설계](storage-premium-storage-performance.md) Azure Premium Storage를 사용하여 고성능 응용 프로그램을 구축하기 위한 지침을 제공합니다. 성능 모범 사례 적용 가능한 tootechnologies 응용 프로그램에서 사용 하는 함께 hello 지침을 따를 수 있습니다.

## <a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>준비 하 고 가상 하드 디스크 (Vhd) tooPremium 저장소를 복사 합니다.
다음 단원을 hello VM에서 Vhd를 준비 하 고 Vhd tooAzure 저장소 복사에 대 한 지침을 제공 합니다.

* [시나리오 1: "마이그레이션하는 중입니다 기존 Azure Vm tooAzure 프리미엄 저장소."](#scenario1)
* [시나리오 2: "마이그레이션하는 중입니다 Vm에서 다른 플랫폼 tooAzure 프리미엄 저장소."](#scenario2)

### <a name="prerequisites"></a>필수 조건
tooprepare hello Vhd 마이그레이션에 필요 합니다.

* Azure 구독, 저장소 계정 및 해당 저장소의 컨테이너 계정 toowhich VHD를 복사할 수 있습니다. Hello 대상 저장소 계정 요구 사항에 따라 표준 또는 프리미엄 저장소 계정 수 있는지 확인 합니다.
* VHD에서 여러 VM 인스턴스 toocreate를 계획 하는 경우 도구 toogeneralize 번호입니다. 예를 들어 Ubuntu용 virt-sysprep 또는 Windows용 sysprep입니다.
* 한 도구 tooupload hello VHD 파일 toohello 저장소 계정입니다. 참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md) 하거나 사용 하 여 프로그램 [Azure 저장소 탐색기](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)합니다. 이 가이드에서 설명 hello AzCopy 도구를 사용 하 여 VHD를 복사 합니다.

> [!NOTE]
> 최적의 성능을 위해서는 azcopy를 동기 복사 옵션을 선택 하면 VHD를 복사 하 여 hello에 있는 Azure VM에서 다음이 도구 중 하나를 실행 하 여 hello 대상 저장소 계정과 동일한 지역입니다. 다른 지역에는 Azure VM에서 VHD를 복사 하는 경우 성능이 느려질 수 있습니다.
>
> 제한 된 대역폭을 통해 많은 양의 데이터를 복사 하기 위한 것이 좋습니다 [hello Azure 가져오기/내보내기 서비스 tootransfer 데이터 tooBlob 저장소를 사용 하 여](../storage-import-export-service.md); 이렇게 하면 tootransfer 전달 하드 디스크에서 데이터 tooan Azure 드라이브 데이터 센터입니다. Hello Azure 가져오기/내보내기 서비스 toocopy 데이터 tooa 표준 저장소 계정 에서만 사용할 수 있습니다. Hello 데이터는 표준 저장소 계정에 사용 하 여 어느 hello [Blob 복사 API](https://msdn.microsoft.com/library/azure/dd894037.aspx) 또는 AzCopy tootransfer hello 데이터 tooyour 프리미엄 저장소 계정입니다.
>
> Microsoft Azure는 고정된 크기의 VHD 파일만을 지원합니다. 동적 VHD 또는 VHDX 파일은 지원되지 않습니다. 동적 VHD를 설정한 경우 변환할 수 있습니다 hello를 사용 하 여 toofixed 크기 [CONVERT-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.
>
>

### <a name="scenario1"></a>시나리오 1: "마이그레이션하는 중입니다 기존 Azure Vm tooAzure 프리미엄 저장소."
기존 Azure Vm에서 VM 중지 hello 마이그레이션하는 경우 원하는 VHD의 hello 유형당 Vhd를 준비 하 고 hello AzCopy 또는 PowerShell VHD를 복사 합니다.

hello VM toomigrate 깨끗 한 상태로 아래로 완전히 toobe가 필요합니다. Hello 마이그레이션 완료 될 때까지 가동 중지 시간이 됩니다.

#### <a name="step-1-prepare-vhds-for-migration"></a>1단계. 마이그레이션할 VHD를 준비합니다.
기존 Azure Vm tooPremium 저장소를 마이그레이션하는 경우 VHD 수 있습니다.

* 일반화된 운영 체제 이미지
* 고유의 운영 체제 디스크
* 데이터 디스크

아래에서는 VHD를 준비하기 위한 3가지 시나리오를 살펴봅니다.

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a>사용 하 여 일반화 된 운영 체제 VHD toocreate 여러 VM 인스턴스
업로드 하는 경우 사용 되는 toocreate 될 VHD 제네릭 Azure VM의 여러 인스턴스를 sysprep 유틸리티를 사용 하 여 VHD를 먼저 일반화 해야 합니다. 이 적용 됩니다 tooa 온-프레미스에 VHD 또는 hello 클라우드입니다. Sysprep은 VHD hello에서 모든 컴퓨터 관련 정보를 제거합니다.

> [!IMPORTANT]
> 스냅숏을 찍거나 VM을 백업하기 전에 일반화합니다. Sysprep를 실행 중인 사용 중지 하 고 hello VM 인스턴스를 할당 취소 됩니다. Windows 운영 체제 VHD toosysprep 아래 단계를 수행 합니다. Note는 hello Sysprep 명령을 실행 해야 합니다 tooshut hello 가상 컴퓨터를 중단 합니다. Sysprep에 대한 자세한 내용은 [Sysprep 개요](http://technet.microsoft.com/library/hh825209.aspx) 또는 [Sysprep 기술 참조](http://technet.microsoft.com/library/cc766049.aspx)를 참조하세요.
>
>

1. 관리자로 명령 프롬프트 창을 엽니다.
2. 다음 명령은 tooopen Sysprep hello를 입력 합니다.

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. 시스템 준비 도구 hello 선택 입력 시스템 기본적으로 (oobe 첫 실행 경험)을 선택 hello 일반화 확인란을 선택 **종료**, 클릭 하 고 **확인**hello 이미지 아래에 표시 된 것 처럼 합니다. Sysprep은 hello 운영 체제를 일반화 되 고 hello 시스템 종료 됩니다.

    ![][1]

Ubuntu VM에 대 한 사용 virt sysprep tooachieve hello 동일 합니다. 자세한 내용은 [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) 를 참조하세요. 참고 항목 일부 hello 오픈 소스 [Linux 서버 프로 비전 소프트웨어](http://www.cyberciti.biz/tips/server-provisioning-software.html) 다른 Linux 운영 체제에 대 한 합니다.

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a>고유 운영 체제 VHD toocreate 단일 VM 인스턴스를 사용 하 여
Hello hello 컴퓨터 특정 데이터를 필요로 하는 VM에서 실행 중인 응용 프로그램를 설정한 경우에 VHD hello을 일반화 하지 마세요. 일반화 되지 않은 VHD를 사용 하는 toocreate 고유한 Azure VM 인스턴스 수 있습니다. 예를들어 VHD에 도메인 컨트롤러가 있는 경우, sysprep를 실행하면 도메인 컨트롤러가 비효율적이게 됩니다. VHD hello을 일반화 하기 전의 sysprep를 실행 중인 VM과 hello 영향을 실행 하는 hello 응용 프로그램을 검토 합니다.

##### <a name="register-data-disk-vhd"></a>데이터 디스크 VHD 등록
있는 경우 Azure toobe에 데이터 디스크 마이그레이션된를 이러한 데이터 디스크는 종료를 사용 하는 hello Vm 있는지 확인 해야 합니다.

프리미엄 저장소 toocopy VHD tooAzure 아래에 설명 된 hello 단계에 따라 프로 비전 된 데이터 디스크로 등록 하십시오.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>2단계. VHD에 대 한 hello 대상 만들기
VHD를 유지 관리하기 위한 저장소 계정을 만듭니다. Hello 지점 위치 계획할 때는 다음 고려 toostore Vhd:

* hello 대상 프리미엄 저장소 계정입니다.
* 저장소 계정 위치 hello hello 최종 단계에서 만들 프리미엄 저장소 지원 되는 Azure Vm으로 동일 해야 합니다. 새 저장소 계정을 tooa 또는 필요에 따라 동일한 저장소 계정 계획 toouse hello를 복사할 수 있습니다.
* 복사 하 고 hello 다음 단계에 대 한 hello 대상 저장소 계정의 hello 저장소 계정 키를 저장 합니다.

데이터 디스크에 대 한 표준 저장소 계정 (예를 들어 디스크 냉각기 저장소에 있는)에 일부 데이터 디스크를 tookeep를 선택할 수 있지만 좋습니다 프로덕션 작업 toouse 프리미엄 저장소에 대 한 모든 데이터를 이동할 수 있습니다.

#### <a name="copy-vhd-with-azcopy-or-powershell"></a>3단계. AzCopy 또는 PowerShell을 사용하여 VHD 복사
컨테이너 경로 저장소 계정 키 tooprocess를 이러한 두 옵션 중 하나 toofind 필요 합니다. 컨테이너 경로 및 저장소 계정 키는 **Azure Portal** > **저장소**에서 찾을 수 있습니다. "https://myaccount.blob.core.windows.net/mycontainer/" hello 컨테이너 URL 표시 됩니다.

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a>옵션 1: AzCopy를 사용하여 VHD 복사(비동기 복사)
AzCopy를 사용 하 여 hello VHD hello 인터넷을 통해 쉽게 업로드할 수 있습니다. Hello Vhd의 hello 크기에 따라 시간이 걸릴 수 있습니다. 이 옵션을 사용 하는 경우 toocheck hello 저장소 계정 송/수신 제한 해야 합니다. 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md) 를 참조하세요.

1. [최신 버전의 AzCopy](http://aka.ms/downloadazcopy)
2. Azure PowerShell 및 이동 toohello AzCopy를 설치한 폴더를 엽니다.
3. 사용 하 여 hello 다음 명령에서 "Source" toocopy hello VHD 파일 너무 "Destination"입니다.

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    예제:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    Hello AzCopy 명령에에서 사용 되는 hello 매개 변수에 대 한 설명은 다음과 같습니다.

   * **/ 소스:  *&lt;소스&gt;:***  hello 폴더 또는 hello VHD를 포함 하는 저장소 컨테이너 URL의 위치입니다.
   * **/ SourceKey:  *&lt;소스-계정 키&gt;:***  hello 원본 저장소 계정의 저장소 계정 키입니다.
   * **/ Dest:  *&lt;대상&gt;:***  저장소 컨테이너 URL toocopy hello VHD를 합니다.
   * **/ DestKey:  *&lt;dest-계정 키&gt;:***  hello 대상 저장소 계정의 저장소 계정 키입니다.
   * **/ 패턴:  *&lt;파일 이름&gt;:***  hello VHD toocopy의 hello 파일 이름을 지정 합니다.

AzCopy를 사용 하 여 대 한 자세한 내용은 도구, 참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md)합니다.

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a>옵션 2: PowerShell을 사용하여 VHD 복사(동기 복사)
시작 AzureStorageBlobCopy hello PowerShell cmdlet을 사용 하 여 hello VHD 파일을 복사할 수도 있습니다. Hello Azure PowerShell toocopy VHD에서 다음 명령을 사용 합니다. 원본 및 대상 저장소 계정에서 해당 값을 가진 <> hello 값을 교체 합니다. toouse이 명령에 대상 저장소 계정에 vhd를 호출 하는 컨테이너가 있어야 합니다. Hello 컨테이너가 존재 하지 않는 경우 hello 명령을 실행 하기 전에 만듭니다.

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

예제:

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <a name="scenario2"></a>시나리오 2: "마이그레이션하는 중입니다 Vm에서 다른 플랫폼 tooAzure 프리미엄 저장소."
비 Azure 클라우드 저장소 tooAzure에서 VHD를 마이그레이션하는 경우 먼저 hello VHD tooa 로컬 디렉터리를 내보내야 합니다. Hello 로컬 VHD를 저장할 디렉터리를의 전체 소스 경로 hello 있고 다음 tooupload AzCopy를 사용 하 여 그 tooAzure 저장소입니다.

#### <a name="step-1-export-vhd-tooa-local-directory"></a>1단계. 내보내기 VHD tooa 로컬 디렉터리
##### <a name="copy-a-vhd-from-aws"></a>AWS에서 VHD 복사
1. AWS를 사용 하는 hello EC2 인스턴스 tooa Amazon S3 버킷에서 VHD를 내보냅니다. Hello Amazon EC2 인스턴스 내보내기 tooinstall hello Amazon EC2 CLI (명령줄 인터페이스) 도구에 대 한 Amazon 설명서에에서 설명 된 hello 단계를 따르고 hello-인스턴스-내보내기-작업 만들기 명령 tooexport hello EC2 인스턴스 tooa VHD 파일을 실행 합니다. 수 있는지 toouse **VHD** hello 디스크 &#95; 이미지 &#95;에 대 한 Hello를 실행 하는 경우 형식 변수 **-인스턴스-내보내기-작업 만들기** 명령입니다. hello 내보낸된 VHD 파일에에서 저장 됩니다 hello Amazon S3 버킷을 그 과정 지정 합니다.

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. Hello S3 버킷을에서 hello VHD 파일을 다운로드 합니다. 선택 hello VHD 파일에 다음 **동작** > **다운로드**합니다.

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a>다른 비-Azure 클라우드에서 VHD 복사
비 Azure 클라우드 저장소 tooAzure에서 VHD를 마이그레이션하는 경우 먼저 hello VHD tooa 로컬 디렉터리를 내보내야 합니다. VHD를 저장할 로컬 디렉터리 hello의 hello 전체 소스 경로 복사 합니다.

##### <a name="copy-a-vhd-from-on-premises"></a>온-프레미스에서 VHD 복사
온-프레미스 환경에서 VHD를 마이그레이션하는 hello 전체 소스 경로 VHD 저장 위치 해야 합니다. hello 소스 경로 서버 위치 또는 파일 공유를 수 있습니다.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>2단계. VHD에 대 한 hello 대상 만들기
VHD를 유지 관리하기 위한 저장소 계정을 만듭니다. Hello 지점 위치 계획할 때는 다음 고려 toostore Vhd:

* hello 대상 저장소 계정에는 응용 프로그램 요구 사항에 따라 표준 또는 프리미엄 저장소 수 있습니다.
* 저장소 계정 지역이 hello hello 최종 단계에서 만들 프리미엄 저장소 지원 되는 Azure Vm으로 동일 해야 합니다. 새 저장소 계정을 tooa 또는 필요에 따라 동일한 저장소 계정 계획 toouse hello를 복사할 수 있습니다.
* 복사 하 고 hello 다음 단계에 대 한 hello 대상 저장소 계정의 hello 저장소 계정 키를 저장 합니다.

이 프로덕션 작업 toouse 프리미엄 저장소에 대 한 모든 데이터를 이동할 수 있습니다.

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a>3단계. Hello VHD tooAzure 저장소에 업로드
Hello 로컬 디렉터리에 VHD를가지고 AzCopy 또는 AzurePowerShell tooupload hello.vhd 파일 tooAzure 저장소를 사용할 수 있습니다. 두 가지 업로드 옵션이 제공됩니다.

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a>Azure PowerShell Add-azurevhd tooupload hello.vhd 파일을 사용 하 여 옵션 1:

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<Uri>의 예로 ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***를 들 수 있습니다. <FileInfo>의 예로 ***"C:\path\to\upload.vhd"***를 들 수 있습니다.

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a>AzCopy tooupload hello.vhd 파일을 사용 하 여 옵션 2:
AzCopy를 사용 하 여 hello VHD hello 인터넷을 통해 쉽게 업로드할 수 있습니다. Hello Vhd의 hello 크기에 따라 시간이 걸릴 수 있습니다. 이 옵션을 사용 하는 경우 toocheck hello 저장소 계정 송/수신 제한 해야 합니다. 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md) 를 참조하세요.

1. [최신 버전의 AzCopy](http://aka.ms/downloadazcopy)
2. Azure PowerShell 및 이동 toohello AzCopy를 설치한 폴더를 엽니다.
3. 사용 하 여 hello 다음 명령에서 "Source" toocopy hello VHD 파일 너무 "Destination"입니다.

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    예제:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    Hello AzCopy 명령에에서 사용 되는 hello 매개 변수에 대 한 설명은 다음과 같습니다.

   * **/ 소스:  *&lt;소스&gt;:***  hello 폴더 또는 hello VHD를 포함 하는 저장소 컨테이너 URL의 위치입니다.
   * **/ SourceKey:  *&lt;소스-계정 키&gt;:***  hello 원본 저장소 계정의 저장소 계정 키입니다.
   * **/ Dest:  *&lt;대상&gt;:***  저장소 컨테이너 URL toocopy hello VHD를 합니다.
   * **/ DestKey:  *&lt;dest-계정 키&gt;:***  hello 대상 저장소 계정의 저장소 계정 키입니다.
   * **/ BlobType: 페이지:** hello 대상 연결 되는 페이지 blob을 지정 합니다.
   * **/ 패턴:  *&lt;파일 이름&gt;:***  hello VHD toocopy의 hello 파일 이름을 지정 합니다.

AzCopy를 사용 하 여 대 한 자세한 내용은 도구, 참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md)합니다.

##### <a name="other-options-for-uploading-a-vhd"></a>VHD를 업로드하기 위한 기타 옵션
Hello 방법을 다음 중 하나를 사용 하 여 VHD tooyour 저장소 계정을 업로드할 수 있습니다.

* [Azure 저장소 Blob 복사 API](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [Azure Storage 탐색기 Blob 업로드](https://azurestorageexplorer.codeplex.com/)
* [저장소 가져오기/내보내기 서비스 REST API 참조](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> 예상 업로드 시간이 7일보다 긴 경우 가져오기/내보내기 서비스를 사용하는 것이 좋습니다. 사용할 수 있습니다 [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) 데이터 크기와 전송 단위에서 tooestimate hello 시간입니다.
>
> 가져오기/내보내기 수 toocopy tooa 표준 저장소 계정을 사용 합니다. AzCopy와 같은 도구를 사용 하 여 표준 저장소 toopremium 저장소 계정에서 toocopy가 필요 합니다.
>
>

## <a name="create-azure-virtual-machine-using-premium-storage"></a>Premium Storage를 사용하여 Azure VM 만들기
Hello VHD를 업로드 또는 복사 toohello 원하는 저장소 계정으로 운영 체제 이미지 또는 운영 체제 디스크 시나리오에 따라이 섹션 tooregister hello VHD의에서 hello 지침을 따릅니다 한 다음 여기에서 VM 인스턴스를 만듭니다. hello 데이터 디스크 VHD 수 첨부 toohello VM 생성 합니다.
예제 마이그레이션 스크립트는이 섹션의 hello 끝에서 제공 됩니다. 이 간단한 스크립트가 모든 시나리오에 적합한 것은 아닙니다. 특정 시나리오와 tooupdate hello 스크립트 toomatch를 할 수 있습니다. 이 스크립트는 tooyour 시나리오를 적용 하는 경우 toosee 아래를 참조 [A 예제 마이그레이션 스크립트](#a-sample-migration-script)합니다.

### <a name="checklist"></a>검사 목록
1. 모든 hello VHD 디스크 복사 될 때까지 대기 완료 되었습니다.
2. 프리미엄 저장소를 마이그레이션하는 hello 지역에서 사용할 수 있는지 확인 합니다.
3. 사용 하려는 hello 새 VM 시리즈를 결정 합니다. 프리미엄 저장소를 사용할 수 있어야 하 고 hello 영역의 hello 가용성에 따라 및 사용자 요구에 따라 hello 크기 여야 합니다.
4. 사용 하 여 hello 정확한 VM 크기를 결정 합니다. VM 크기에 있는 데이터 디스크 개수 충분히 큰 toosupport hello toobe 필요 합니다. 예: 4 개의 데이터 디스크가 있는 경우 hello VM 2 개 이상의 코어 있어야 합니다. 또한 처리 능력, 메모리 및 네트워크 대역폭 요구 사항을 고려합니다.
5. Hello 대상 지역에서 프리미엄 저장소 계정을 만듭니다. 이 계정이 hello hello에 대 한 사용 하 여 새 VM입니다.
6. 정보 포함 하 고 hello 현재 VM 디스크 및 해당 VHD blob hello 목록을 포함 하 여 편리 합니다.

응용 프로그램의 가동 중지 시간을 준비합니다. 클린 마이그레이션 toodo toostop 모든 hello 처리는 hello 현재 시스템에서 합니다. 경우에 표시할 수 있습니다 마이그레이션할 수 없는 tooconsistent 상태 toohello 새 플랫폼입니다. 작동 중단 기간 hello 디스크 toomigrate의 데이터 양을 hello에 따라 달라 집니다.

> [!NOTE]
> 특수 한 VHD 디스크에서 Azure 리소스 관리자 VM을 만드는 경우를 참조 하십시오 너무[이 서식 파일](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) 기존 디스크를 사용 하 여 리소스 관리자 VM을 배포 합니다.
>
>

### <a name="register-your-vhd"></a>장치를 등록합니다.
운영 체제 VHD 또는 데이터 디스크 tooa tooattach에서 VM toocreate 새 VM을 먼저 등록 해야 합니다. VHD 시나리오에 따라 아래 단계를 따르세요.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>운영 체제 VHD toocreate 여러 Azure VM 인스턴스 일반화
VHD는 운영 체제 이미지를 일반화 된 toohello 저장소 계정을 업로드 후 등록로 **Azure VM 이미지** 에서 하나 이상의 VM 인스턴스를 만들 수 있도록 합니다. Azure VM의 OS 이미지 형식으로 다음 PowerShell cmdlet tooregister hello VHD를 사용 합니다. VHD 복사 된 위치의 hello 전체 컨테이너 URL을 제공 합니다.

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

복사 하 고이 새 Azure VM 이미지의 hello 이름을 저장 합니다. 위의 hello 예제 *OSImageName*합니다.

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>고유 운영 체제 VHD toocreate 단일 Azure VM 인스턴스
Hello 후 고유 운영 체제 VHD는 업로드 된 toohello 저장소 계정로 등록 한 **Azure OS 디스크** 에서 VM 인스턴스를 만들 수 있도록 합니다. Azure OS 디스크로 이러한 PowerShell cmdlet tooregister VHD를 사용 합니다. VHD 복사 된 위치의 hello 전체 컨테이너 URL을 제공 합니다.

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

복사 하 고이 새 Azure 운영 체제 디스크의 hello 이름을 저장 합니다. 위의 hello 예제 *OSDisk*합니다.

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a>데이터 디스크 VHD toobe toonew Azure VM 인스턴스 연결
Hello 데이터 디스크 VHD가 업로드 후 toostorage 계정으로 등록 된 Azure 데이터 디스크 연결된 tooyour 수 있도록 새 DS 시리즈, DSv2 시리즈 또는 GS 시리즈 Azure VM 인스턴스.

Azure 데이터 디스크와 이러한 PowerShell cmdlet tooregister VHD를 사용 합니다. VHD 복사 된 위치의 hello 전체 컨테이너 URL을 제공 합니다.

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

복사 하 고이 새 Azure 데이터 디스크의 hello 이름을 저장 합니다. 위의 hello 예제 *DataDisk*합니다.

### <a name="create-a-premium-storage-capable-vm"></a>Premium Storage 지원 VM 만들기
새 DS 시리즈, DSv2 시리즈 또는 GS 시리즈 VM 만들기, 운영 체제 이미지를 한 번 hello 또는 OS 디스크로 등록 됩니다. 사용 하려는 hello 운영 체제 이미지 또는 운영 체제 디스크 이름을 등록 합니다. Hello 프리미엄 저장소 계층에서 hello VM 유형을 선택 합니다. 아래 예제에서 사용 하 여 hello *Standard_DS2* VM 크기입니다.

> [!NOTE]
> Hello 디스크 크기 toomake 용량 및 성능 요구 사항 및 hello 사용 가능한 Azure 디스크 크기와 일치 하는지를 업데이트 합니다.
>
>

Toocreate 아래에 따라 hello 단계별 PowerShell cmdlet에는 새 VM hello 합니다. 먼저, hello 공통 매개 변수를 설정 합니다.

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

먼저, 클라우드 서비스를 호스트할 새 Vm을 만듭니다.

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

다음으로 시나리오에 따라 hello Azure VM 인스턴스를 hello 운영 체제 이미지 또는 등록 OS 디스크를에서 만듭니다.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>운영 체제 VHD toocreate 여러 Azure VM 인스턴스 일반화
Hello 하나 이상의 새 인스턴스를 만들고 DS 시리즈 Azure VM hello를 사용 하 여 **Azure OS 이미지** 등록 합니다. 아래와 같이 새 VM을 만들 때이 OS 이미지 이름을 hello VM 구성을 지정 합니다.

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>고유 운영 체제 VHD toocreate 단일 Azure VM 인스턴스
Hello를 사용 하 여 새 DS 시리즈 Azure VM 인스턴스를 만들고 **Azure OS 디스크** 등록 합니다. 아래와 같이 새 VM을 hello 만들 때이 OS 디스크 이름은 hello VM 구성에서 지정 합니다.

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

클라우드 서비스, 지역, 저장소 계정, 가용성 집합 및 캐싱 정책 등의 기타 Azure VM 정보를 지정합니다. Note hello VM 인스턴스는 관련 된 운영 체제와 함께 배치 해야 합니다. 또는 데이터 디스크를 선택 하는 hello 클라우드 서비스, 지역 및 저장소 계정 모두에 있어야 하므로 hello hello 기본 해당 디스크의 Vhd와 동일한 위치입니다.

### <a name="attach-data-disk"></a>데이터 디스크 연결
마지막으로 등록 한 경우 데이터 디스크 Vhd로 toohello 첨부할 새로운 프리미엄 저장소 지원 Azure VM입니다.

다음 PowerShell cmdlet tooattach 데이터 디스크 toohello 사용 하 여 새 VM hello 캐싱 정책을 지정 합니다. Hello 아래 예에서 캐싱 정책은 설정 되어 너무*ReadOnly*합니다.

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> 추가 단계가 필요한 toosupport 있을 수 있는 응용 프로그램에서 다룰 수 없는이 가이드입니다.
>
>

### <a name="checking-and-plan-backup"></a>확인 및 백업 계획
동일한 로그인 id와 암호를 사용 하 여 hello 액세스 실행 되 고 새 VM이 위쪽 hello 한 번 hello 원본 VM으로 이며 모든 항목이 예상 대로 작동 하는지 확인 합니다. Hello 스트라이프 볼륨을 포함 한 모든 hello 설정에 제공 됩니다. 새 VM hello 합니다.

hello 마지막 단계는 새 VM hello 응용 프로그램의 요구 사항에 따라 hello에 대 한 tooplan 백업 및 유지 관리 일정입니다.

### <a name="a-sample-migration-script"></a>샘플 마이그레이션 스크립트
여러 Vm toomigrate를 설정한 경우에 PowerShell 스크립트를 통해 자동화 유용할 수 있습니다. 다음은 VM의 hello 마이그레이션을 자동화 하는 샘플 스크립트입니다. 참고는 아래 스크립트는 하나의 예 되며 hello 현재 VM 디스크에 대 한 몇 가지 가정을 합니다. 특정 시나리오와 tooupdate hello 스크립트 toomatch를 할 수 있습니다.

hello 가정은:

* 클래식 Azure VM을 만듭니다.
* 원본 OS 디스크와 원본 데이터 디스크가 동일한 저장소 계정 및 동일한 컨테이너에 있습니다. OS 디스크 및 데이터 디스크에 없는 경우 동일한 hello를 저장소 계정 및 컨테이너를 통해 AzCopy 또는 Azure PowerShell toocopy Vhd를 사용할 수 있습니다. Toohello 이전 단계를 참조 하십시오: [AzCopy 또는 PowerShell 복사 VHD](#copy-vhd-with-azcopy-or-powershell)합니다. 이 스크립트 toomeet 편집 시나리오에는 다른 선택 하지만 더 쉽고 빠르게 이후 AzCopy 또는 PowerShell을 사용 하 여는 것이 좋습니다.

hello 자동화 스크립트는 아래에 제공 됩니다. 특정 시나리오를 hello 스크립트 toomatch 업데이트 및 사용자 정보로 텍스트를 바꿉니다.

> [!NOTE]
> Hello 기존 스크립트를 사용 하 여 원본 VM의 네트워크 구성을 hello 유지 하지 않습니다. 마이그레이션된 Vm에 toore-config hello 네트워킹 설정 해야 합니다.
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <a name="optimization"></a>최적화
현재 VM 구성을 사용자 지정할 수 있습니다 표준 디스크와 잘 toowork 특히 합니다. 예를 들어, tooincrease hello 성능 스트라이프 볼륨에서 많은 디스크를 사용 하 여입니다. 예를 들어, 프리미엄 저장소에 개별적으로 4 개를 사용 하는 대신 단일 디스크를 포함 하면 수 toooptimize hello 비용을 수 있습니다. 최적화 등이 필요 toobe 상황별으로에서 처리 및 hello 마이그레이션 후 사용자 지정 단계를 필요로 합니다. 또한, 이때 데이터베이스 및 hello 설치에 정의 된 hello 디스크 레이아웃에 의존 하는 응용 프로그램에 대 한이 프로세스 제대로 작동 하지 않을 수 있습니다.

##### <a name="preparation"></a>준비
1. 전체 hello hello에 설명 된 대로 간단한 마이그레이션을 이전 섹션. Hello 최적화가 수행 될 됩니다 hello 마이그레이션 후 새 VM입니다.
2. 최적화 된 hello 구성 필요한 hello 새 디스크 크기를 정의 합니다.
3. 현재 디스크/볼륨 toohello hello 새 디스크 사양의 매핑을 확인 합니다.

##### <a name="execution-steps"></a>실행 단계
1. 프리미엄 저장소 VM hello에 hello 적절 한 크기와 hello 새 디스크를 만듭니다.
2. 로그인 toohello VM 및 복사 hello 데이터 hello 현재 볼륨 toohello 새 디스크 toothat 볼륨을 매핑하는입니다. Toomap tooa 새 디스크를 필요로 하는 모든 hello 현재 볼륨에 대해이 작업을 수행 합니다.
3. Hello 응용 프로그램 설정 tooswitch toohello 새 디스크를 바꾼 다음으로 hello 이전 볼륨을 분리 하십시오.

디스크 성능 향상을 위해 hello 응용 프로그램 튜닝을 참조 하십시오 너무[응용 프로그램 성능 최적화](storage-premium-storage-performance.md#optimizing-application-performance)합니다.

### <a name="application-migrations"></a>응용 프로그램 마이그레이션
데이터베이스 및 기타 복잡 한 응용 프로그램 hello 마이그레이션에 대 한 hello 응용 프로그램 공급자에 의해 정의 된 특별 한 단계가 필요할 수 있습니다. Toorespective 응용 프로그램 설명서를 참조 하십시오. 예: 일반적으로 백업 및 복원을 통해 데이터베이스를 마이그레이션할 수 있습니다.

## <a name="next-steps"></a>다음 단계
Hello 다음 가상 컴퓨터 마이그레이션에 대 한 특정 시나리오에 대 한 리소스를 참조 하십시오.

* [저장소 계정 간에 Azure 가상 컴퓨터 마이그레이션](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [만들고 Windows Server VHD tooAzure 업로드 합니다.](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [만들고 해당 Contains hello Linux 운영 체제 가상 하드 디스크를 업로드 합니다.](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [AWS Amazon tooMicrosoft Azure에서에서 가상 컴퓨터를 마이그레이션하거나](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

또한, 다음 Azure 저장소 및 Azure 가상 컴퓨터에 대 한 자세한 리소스 toolearn hello를 참조 하십시오.

* [Azure 저장소](https://azure.microsoft.com/documentation/services/storage/)
* [Azure 가상 컴퓨터](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [프리미엄 저장소: Azure 가상 컴퓨터 워크로드를 위한 고성능 저장소](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
