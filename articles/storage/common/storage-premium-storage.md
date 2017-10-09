---
title: "aaaHigh 성능 프리미엄 저장소 및 Azure Vm에 대 한 디스크 관리 | Microsoft Docs"
description: "Azure VM의 고성능 Premium Storage 및 관리 디스크에 대해 자세히 알아봅니다. Azure DS 시리즈, DSv2 시리즈, GS 시리즈 및 Fs 시리즈 VM은 Premium Storage를 지원합니다."
services: storage
documentationcenter: 
author: ramankumarlive
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: ramankum
ms.openlocfilehash: 5f08e615869ed59a9d80d798ec191dd4d3abc3e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-premium-storage-and-managed-disks-for-vms"></a>VM의 고성능 Premium Storage 및 관리 디스크
Azure Premium Storage는 입력/출력(I/O) 사용량이 많은 워크로드가 있는 VM(가상 컴퓨터)에서 대기 시간이 짧은 고성능 디스크 지원을 제공합니다. Premium Storage를 사용하는 VM 디스크는 SSD(반도체 드라이브)에 데이터를 저장합니다. tootake 이점은 hello 속도 및 프리미엄 저장소 디스크의 성능을 기존 VM 디스크 tooPremium 저장소를 마이그레이션할 수 있습니다.

Azure에서 여러 프리미엄 저장소 디스크 tooa VM을 연결할 수 있습니다. 여러 디스크를 사용 하 여 VM 당 저장소 too256 TB 응용 프로그램을 제공 합니다. 프리미엄 저장소로 응용 프로그램 80,000 I/O 작업 / 초 (IOPS) VM 당과 too2, 000 m b / 초 (m B/초) VM 당를 디스크 처리량을 향상할 수 있습니다. 읽기 작업의 대기 시간이 매우 짧습니다.

프리미엄 저장소로 Azure tootruly 리프트 시프트 까다로운 엔터프라이즈 응용 프로그램 Dynamics AX, Dynamics CRM, Exchange Server, SAP Business Suite 및 SharePoint 팜 toohello 클라우드 같은 hello 기능을 제공 합니다. 일관된 고성능 및 짧은 대기 시간을 필요로 하는 SQL Server, Oracle, MongoDB, MySQL, Redis 등 성능 집약적 데이터베이스 워크로드를 응용 프로그램에서 실행할 수 있습니다.

> [!NOTE]
> 응용 프로그램에 대 한 최상의 성능을 위해서는 hello 높은 IOPS tooPremium 저장소를 필요로 하는 VM 디스크를 마이그레이션하는 것이 좋습니다. 디스크에 높은 IOPS가 필요하지 않으면 표준 Azure Storage에 유지하여 비용을 제한할 수 있습니다. 표준 저장소는 SSD 대신 HDD(하드 디스크 드라이브)에 VM 디스크 데이터를 저장합니다.
> 

Azure는 Vm에 대 한 두 가지 방법으로 toocreate 프리미엄 저장소 디스크 제공합니다.

* **관리되지 않는 디스크**

    hello 원래 방법은 관리 되지 않는 toouse 디스크입니다. 관리 되지 않는 디스크, 해당 tooyour VM 디스크는 toostore hello 가상 하드 디스크 (VHD) 파일을 사용 하는 hello 저장소 계정을 관리할 수 있습니다. VHD 파일은 Azure Storage 계정에 페이지 Blob으로 저장됩니다. 

* **관리되는 디스크**

    선택 하는 경우 [Azure 관리 되는 디스크](../../virtual-machines/windows/managed-disks-overview.md), Azure가 VM 디스크를 사용 하는 hello 저장소 계정을 관리 합니다. Hello 디스크 유형 (프리미엄 또는 표준)와 필요한 hello 디스크의 hello 크기 지정 합니다. Azure 만들고에서 hello 디스크를 관리 합니다. 저장소 계정에 대 한 확장성 제한 내에서 유지 되는 여러 저장소 계정 tooensure에 hello 디스크를 배치 하는 방법에 대 한 tooworry가 필요는 없습니다. Azure가 알아서 처리해 드립니다.

관리 되는 디스크, tootake 활용 하는 다양 한 기능을 선택 하는 것이 좋습니다.

프리미엄 저장소 시작 tooget [무료 Azure 계정 만들기](https://azure.microsoft.com/pricing/free-trial/)합니다. 

프로그램 기존 Vm tooPremium 저장소 마이그레이션에 대 한 정보를 참조 하십시오. [Windows VM에서 관리 되지 않는 디스크 toomanaged 디스크 변환](../../virtual-machines/windows/convert-unmanaged-to-managed-disks.md) 또는 [Linux VM에서 관리 되지 않는 디스크 toomanaged 디스크 변환](../../virtual-machines/linux/convert-unmanaged-to-managed-disks.md)합니다.

> [!NOTE]
> Premium Storage는 대부분의 지역에서 사용할 수 있습니다. 에 대 한 사용 가능한 영역 목록은 hello에 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services)는 hello 영역을 살펴보고 지원 프리미엄 지원 크기 시리즈 Vm (DS 시리즈, DSV2 시리즈, GS 시리즈 및 Fs 시리즈 Vm) 지원 됩니다.
> 

## <a name="features"></a>기능

다음은 프리미엄 저장소의 hello 기능 중 일부입니다.

* **Premium Storage 디스크**

    프리미엄 저장소에서는 VM 디스크 일 수 있는 연결 toospecific 크기 시리즈 Vm입니다. Premium Storage는 DS 시리즈, DSv2 시리즈, GS 시리즈, Ls 시리즈 및 Fs 시리즈 VM을 지원합니다. P4(32GB), P6(64GB), P10(128GB), P20(512GB), P30(1024GB), P40(2048GB), P50(4095GB)과 같은 일곱 가지 디스크 크기를 선택할 수 있습니다. P4 및 P6 디스크 크기는 아직 Managed Disks에 대해서만 지원됩니다. 디스크 크기마다 자체 성능 사양이 있습니다. 응용 프로그램 요구 사항에 따라 하나 이상의 디스크 tooyour VM을 연결할 수 있습니다. Hello 사양에서 더 자세하게에서 설명 [프리미엄 저장소 확장성 및 성능 목표가](#scalability-and-performance-targets)합니다.

* **프리미엄 페이지 Blob**

    Premium Storage에서는 페이지 Blob을 지원합니다. 프리미엄 저장소에서 Vm에 대 한 페이지 blob toostore 영구, 관리 되지 않는 디스크를 사용 합니다. 표준 Azure Storage와 달리 Premium Storage는 블록 Blob, 추가 Blob, 파일, 테이블 또는 큐를 지원하지 않습니다. 프리미엄 페이지 blob P10 tooP50 및 P60에서 6 개 크기를 지원 (8191GiB). P60 프리미엄 페이지 blob VM 디스크도 연결 됩니다. 지원 되는 toobe 않습니다. 

    프리미엄 저장소 계정에 있는 모든 개체는 페이지 Blob이 됩니다. hello 페이지 blob의 hello tooone 지원 되는 프로 비전 된 크기를 맞춥니다. 이 때문에 프리미엄 저장소 계정을 위한 용도가 아닙니다 toobe toostore 아주 작은 blob을 사용 합니다.

* **Premium Storage 계정**

    toostart 프리미엄 저장소를 사용 하 여 관리 되지 않는 디스크에 대 한 프리미엄 저장소 계정을 만듭니다. Hello에 [Azure 포털](https://portal.azure.com), toocreate 프리미엄 저장소 계정 선택 hello **프리미엄** 성능 계층입니다. 선택 hello **로컬 중복 저장소 (LRS)** 복제 옵션입니다. 또한 너무 hello 유형을 설정 하 여 프리미엄 저장소 계정을 만들 수**Premium_LRS** hello 다음 위치 중 하나에서:
    * [저장소 REST API](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference)(버전 2014-02-14 이상)
    * [Service Management REST API](http://msdn.microsoft.com/library/azure/ee460799.aspx)(버전 2014-10-01 이상, Azure 클래식 배포인 경우)
    * [Azure Storage 리소스 공급자 REST API](https://docs.microsoft.com/rest/api/storagerp)(Azure Resource Manager 배포인 경우)
    * [Azure PowerShell](/powershell/azureps-cmdlets-docs.md)(버전 0.8.10 이상)

    프리미엄 저장소 계정 제한에 대 한 toolearn 참조 [프리미엄 저장소 확장성 및 성능 목표가](#premium-storage-scalability-and-performance-targets)합니다.

* **프리미엄 로컬 중복 저장소**

    프리미엄 저장소 계정을 hello replication 옵션으로만 로컬 중복 저장소를 지원합니다. 로컬 중복 저장소는 단일 지역 내 hello 데이터 복사본이 3 개 유지합니다. 지역적 재해 복구를 위해 [Azure Backup](../../backup/backup-introduction-to-azure-backup.md)을 사용하여 VM 디스크를 다른 지역에 백업해야 합니다. 또한 hello 백업 자격 증명 모음으로 지역 중복 저장소 (GRS) 계정을 사용 해야 합니다. 

    Azure는 저장소 계정을 관리되지 않는 디스크의 컨테이너로 사용합니다. 관리되지 않는 디스크로 Azure DS 시리즈, DSv2 시리즈, GS 시리즈 또는 Fs 시리즈 VM을 만들고 프리미엄 저장소 계정을 선택하는 경우 운영 체제와 데이터 디스크가 해당 저장소 계정에 저장됩니다.

## <a name="supported-vms"></a>지원되는 VM
Premium Storage는 DS 시리즈, DSv2 시리즈, GS 시리즈, Ls 시리즈 및 Fs 시리즈 VM을 지원합니다. 이러한 VM 유형에는 표준 및 프리미엄 저장소 디스크를 사용할 수 있습니다. Premium Storage와 호환되지 않는 VM 시리즈에서는 프리미엄 저장소 디스크를 사용할 수 없습니다.

Azure에서 Windows용 VM 유형 및 크기에 대한 자세한 내용은 [Windows VM 크기](../../virtual-machines/virtual-machines-windows-sizes-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요. Azure에서 Linux용 VM 유형 및 크기에 대한 자세한 내용은 [Linux VM 크기](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

Hello DS 시리즈, DSv2 시리즈, GS 시리즈의 hello 기능 중 일부는 이러한 Ls 시리즈 및 Fs 시리즈 Vm:

* **클라우드 서비스**

    DS 시리즈 Vm tooa 클라우드 서비스를 DS 시리즈 Vm만 추가할 수 있습니다. DS 시리즈 Vm tooan 기존 클라우드 서비스를 DS 시리즈 Vm 이외의 모든 형식을 추가 하지 마십시오. 기존 Vhd tooa 새 클라우드 서비스 DS 시리즈 Vm만를 실행 하는 마이그레이션할 수 있습니다. Toouse hello 새 클라우드 서비스를 사용 하 여 DS 시리즈 Vm에 호스트에 대 한 동일한 가상 IP 주소를 hello 하려는 경우 [예약 된 IP 주소](../../virtual-network/virtual-networks-instance-level-public-ip.md)합니다. GS 시리즈 Vm tooan 기존 클라우드 서비스를 GS 시리즈 Vm만 추가할 수 있습니다.

* **운영 체제 디스크**

    프리미엄 저장소 VM toouse는 프리미엄 또는 표준 운영 체제 디스크를 설정할 수 있습니다. Hello 최고의 사용 환경을 프리미엄 저장소-기반 운영 체제 디스크를 사용 하는 것이 좋습니다.

* **데이터 디스크**

    Premium을 사용할 수 있으며, 표준 디스크에 동일한 프리미엄 저장소 VM hello 합니다. 프리미엄 저장소로 VM을 프로 비전 수 있으며 여러 영구 데이터 디스크 toohello VM에 연결할 수 있습니다. 필요한 tooincrease hello 용량 및 성능 hello 볼륨의 디스크에서 스트라이프 할 수 있습니다.

    > [!NOTE]
    > [저장소 공간](http://technet.microsoft.com/library/hh831739.aspx)을 사용하여 프리미엄 저장소 데이터 디스크를 스트라이프하는 경우, 저장소 공간은 사용하는 각 디스크에 대해 하나의 열로 설정해야 합니다. 그렇지 않으면 전체 hello 스트라이프 볼륨의 성능 보다 낮을 수 있습니다 hello 디스크에 걸쳐 트래픽의 불균등 한 배포 때문에 필요 합니다. 기본적으로 서버 관리자에서 too8 디스크 구성에 대 한 열을 설정할 수 있습니다. 8 개 이상의 디스크를 사용 하도록 설정한 경우 PowerShell toocreate hello 볼륨을 사용 합니다. Hello 수의 열을 수동으로 지정 합니다. 그렇지 않으면 hello 서버 관리자 UI 더 많은 디스크가 있는 경우에 toouse 8 열을 계속 합니다. 예를 들어 단일 스트라이프 세트에 32개의 디스크가 있다면 32개의 열을 지정합니다. 열의 toospecify hello 수 hello 가상 디스크에에서 사용 되는, hello [New-virtualdisk](http://technet.microsoft.com/library/hh848643.aspx) PowerShell cmdlet을 사용 하 여 hello *NumberOfColumns* 매개 변수입니다. 자세한 내용은 [저장소 공간 개요](http://technet.microsoft.com/library/hh831739.aspx) 및 [저장소 공간 FAQ](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx)를 참조하세요.
    >
    > 

* **캐시**

    프리미엄 저장소를 지 원하는 hello 크기 일련의 Vm는 높은 수준의 처리량 및 대기 시간에 대 한 고유한 캐싱 기능이 있습니다. 캐싱 용량은 hello 기본 프리미엄 저장소 디스크 성능을 초과 합니다. 프리미엄 저장소 디스크에 대 한 정책 너무 캐싱 hello 디스크를 설정할 수 있습니다**ReadOnly**, **ReadWrite**, 또는 **None**합니다. hello 기본 캐싱 정책은 디스크가 **ReadOnly** 모든 프리미엄 데이터 디스크에 대 한 및 **ReadWrite** 운영 체제 디스크에 대 한 합니다. 응용 프로그램에 대 한 최적의 성능을 위해 사용 하 여 hello 캐시 설정을 수정 합니다. 예를 들어 읽기 작업이 너무 많은 또는 읽기 전용 데이터 디스크에 대 한 SQL Server 데이터 파일 등 설정 hello 디스크 캐싱 정책은 너무**ReadOnly**합니다. 쓰기 전용 또는 쓰기 집약적 데이터 디스크에 대 한 SQL Server 로그 파일과 같이 hello 디스크 설정 캐싱 정책은 너무**None**합니다. 프리미엄 저장소 디자인을 최적화에 대 한 더 toolearn 참조 [프리미엄 저장소와 성능 위한 디자인](storage-premium-storage-performance.md)합니다.

* **분석**

    프리미엄 저장소에서 디스크를 사용 하 여 VM 성능 tooanalyze hello에 VM 진단을 설정 [Azure 포털](https://portal.azure.com)합니다. 자세한 내용은 [Azure 진단 확장을 통한 Azure VM 모니터링](https://azure.microsoft.com/blog/2014/09/02/windows-azure-virtual-machine-monitoring-with-wad-extension/)을 참조하세요. 

    toosee 디스크 성능, 사용 하 여 운영 체제 기반 도구와 같은 [Windows 성능 모니터](https://technet.microsoft.com/library/cc749249.aspx) Windows Vm 용과 hello [iostat](http://linux.die.net/man/1/iostat) Linux Vm에 대 한 명령입니다.

* **VM 규모 한도 및 성능**

    각 프리미엄 저장소에서 지 원하는 VM 크기에 규모 조정 한도 및 IOPS, 대역폭 및 hello VM 당 첨부할 수 있는 디스크 수에 대 한 성능 사양이 있습니다. 프리미엄 저장소 디스크를 사용 하 여 Vm이 있는 경우 충분 한 IOPS 및 대역폭 VM toodrive 디스크 트래픽에 인지 확인 합니다.

    예를 들어, STANDARD_DS1 VM에는 프리미엄 저장소 디스크 트래픽에 대해 32MB/초의 전용 대역폭이 있습니다. P10 프리미엄 저장소 디스크는 100MB/초의 대역폭을 제공할 수 있습니다. P10 프리미엄 저장소 디스크를 연결 된 toothis VM 으로만 too32 m B/초를 이동할 수 있습니다. Hello 최대 100MB/s hello P10 디스크를 제공할 수 있습니다 사용할 수 없습니다.

    현재 hello hello DS 시리즈에서에서 가장 큰 VM는 hello Standard_DS15_v2입니다. hello Standard_DS15_v2 모든 디스크에 걸쳐 too960 MB/s를 제공할 수 있습니다. hello hello GS 시리즈에서에서 가장 큰 VM는 hello Standard_GS5입니다. hello Standard_GS5 too2, 000 MB/s 모든 디스크를 제공할 수 있습니다.

    이러한 한도는 디스크 트래픽에만 해당됩니다. 이러한 한도에 캐시 적중 수 및 네트워크 트래픽은 포함되지 않습니다. VM 네트워크 트래픽에는 별도의 대역폭이 제공됩니다. 네트워크 트래픽에 대 한 대역폭은 프리미엄 저장소 디스크에서 사용 되는 전용 hello 대역폭와에서 다릅니다.

    Hello 최신 내용은 최대 IOPS 및 처리량 (대역폭)에 대 한 프리미엄 저장소에서 지 원하는 Vm에 대 한 [Windows VM 크기](/azure/virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [Linux VM 크기](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

    프리미엄 저장소 디스크 및 해당 IOPS 및 처리량 제한은 대 한 자세한 내용은 hello 다음 섹션의 hello 표를 참조 합니다.

## <a name="scalability-and-performance-targets"></a>확장성 및 성능 대상
이 섹션에서는 프리미엄 저장소를 사용 하는 경우 hello 확장성 및 성능 목표 tooconsider를 설명 합니다.

프리미엄 저장소 계정 확장성 목표를 수행 하는 hello를 사항이 있습니다.

| 총 계정 용량 | 로컬 중복 저장소 계정의 총 대역폭 |
| --- | --- | 
| 디스크 용량: 35TB <br>스냅숏 용량: 10TB | 에 대 한 초당 기가 비트 too50 인바운드<sup>1</sup> + 아웃 바운드<sup>2</sup> |

<sup>1</sup> tooa 저장소 계정에 전송 되는 모든 데이터 (요청 수)

<sup>2</sup> 저장소 계정에서 수신하는 모든 데이터(응답)

자세한 내용은 [Azure Storage 확장성 및 성능 목표](storage-scalability-targets.md)를 참조하세요.

프리미엄 저장소 계정을 사용 하는 관리 되지 않는 디스크에 대 한 응용 프로그램에 단일 저장소 계정의 확장성 목표 hello 초과 하는 경우 toomigrate toomanaged 디스크를 할 수 있습니다. Toomigrate toomanaged 디스크를 사용 하지 않으려는 응용 프로그램 toouse 저장소 계정을 여러 개를 빌드하십시오. 그런 다음 이 저장소 계정 간에 데이터를 분할합니다. 예를 들어 여러 Vm 간에 tooattach 51-t B 디스크 하려는 경우 분산에 두 개의 저장소 계정이 있습니다. 35 TB 단일 프리미엄 저장소 계정에 대 한 hello 제한입니다. 단일 프리미엄 저장소 계정에 35TB를 넘는 프로비전된 디스크가 없도록 해야 합니다.

### <a name="premium-storage-disk-limits"></a>Premium Storage 디스크 한도
프리미엄 저장소 디스크 hello 디스크의 크기 hello 구축 판단 하는 경우 hello 최대 IOPS 및 처리량 (대역폭). Azure에서는 P4(Managed Disks에만 해당), P6(Managed Disks에만 해당), P10, P20, P30, P40 및 P50과 같은 일곱 가지 프리미엄 저장소 디스크를 제공합니다. 각 프리미엄 저장소 디스크 유형에는 특정 IOPS 및 처리량 한도가 있습니다. Hello 디스크 유형에 대 한 제한은 hello 다음 표에 설명 되어 있습니다.

| 프리미엄 디스크 유형  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| 디스크 크기           | 32GB| 64GB| 128GB| 512GB            | 1,024GB(1TB)    | 2,048GB(2TB)    | 4,095GB(4TB)    | 
| 디스크당 IOPS       | 120   | 240   | 500   | 2,300              | 5,000              | 7,500              | 7,500              | 
| 디스크당 처리량 | 초당 25MB  | 초당 50MB  | 초당 100MB | 초당 150MB | 초당 200MB | 초당 250MB | 초당 250MB | 

> [!NOTE]
> 에 설명 된 대로 충분 한 대역폭을 VM toodrive 디스크 트래픽에 사용할 수 있는지 확인 [프리미엄 저장소에서 지 원하는 Vm](#premium-storage-supported-vms)합니다. 이렇게 하지 않으면 디스크 처리량 및 IOPS는 제한 된 toolower 값. 최대 처리량 및 IOPS hello 앞에 테이블에에서 설명 된 hello 디스크 제한에 없는 hello VM 제한에 기반 합니다.  
> 
> 

프리미엄 저장소 확장성 및 성능 목표에 대 한 몇 가지 중요 한 사항이 tooknow 다음과 같습니다.

* **프로비전된 용량 및 성능**

    표준 저장소와 달리 프리미엄 저장소 디스크를 프로 비전 할 때 hello 용량, IOPS, 및 해당 디스크의 처리량을 보장 됩니다. 예를 들어 P50 디스크를 만들면 Azure에서 해당 디스크에 저장소 용량 4,095GB, 7,500IOPS, 250MB/초 처리량이 프로비전됩니다. 응용 프로그램 hello 용량 및 성능의 일부나 전부 사용할 수 있습니다.

* **디스크 크기**

    지도 azure 프리미엄 저장소 디스크 옵션 hello 섹션 앞의 hello 테이블에 지정 된 대로 가장 가까운 디스크 크기 (반올림) toohello를 hello 합니다. 예를 들어 100GB의 디스크 크기는 P10 옵션으로 분류됩니다. 수행할 수 있습니다 too500 IOPS를와 too100 MB/s 처리량을 합니다. 마찬가지로 400GB의 디스크 크기는 P20으로 분류됩니다. Too2, 150 m B/초 처리량 300 IOPS 수행할 수 있습니다.
    
    > [!NOTE]
    > 기존 디스크의 hello 크기를 쉽게 늘릴 수 있습니다. 예를 들어 30GB 디스크 too128 GB 또는 TB 짝수 too1 tooincrease hello 크기를 좋습니다. 또는 할 수 있습니다 tooconvert P20 디스크 tooa P30 디스크 용량이 더 이상의 IOPS 및 처리량 필요 하기 때문입니다. 
    > 
 
* **I/O 크기**

    I/O hello 크기는 256KB입니다. 전송 되는 hello 데이터 256KB 보다 작은 경우 1 I/O 단위를 간주 됩니다. 더 큰 I/O 크기는 256KB 크기의 여러 I/O로 계산됩니다. 예를 들어 1,100KB I/O는 I/O 단위 5개로 계산됩니다.

* **처리량**

    쓰기 toohello 디스크를 포함 하는 hello 처리량 한도 작성과 디스크 읽기 작업을 hello 캐시에서 처리 되지 않습니다. 예를 들어 P10 디스크는 디스크당 처리량이 100MB/초입니다. P10 디스크에 대 한 유효한 처리량의 몇 가지 예는 다음 표에 hello에 나와 있습니다.

    | P10 디스크당 최대 처리량 | 디스크에서 캐시 없이 읽기 | 쓰기를 비 캐시 toodisk |
    | --- | --- | --- |
    | 100MB/초 | 100MB/초 | 0 |
    | 100MB/초 | 0 | 100MB/초 |
    | 100MB/초 | 60MB/s | 40MB/초 |

* **캐시 적중 수**

    캐시 적중 hello IOPS 또는 hello 디스크 처리량을 할당 하 여 제한 되지 않습니다. 예를 들어, 사용 하는 경우 데이터 디스크는 **ReadOnly** 캐시 설정 hello 캐시에서 처리 되는 읽기, 프리미엄 저장소에서 지원 되는 VM에는 주체 toohello IOPS 및 처리량 대문자 hello 디스크의 합니다. 디스크의 hello 작업은 주로 경우 읽기, 매우 높은 처리량 표시 될 수 있습니다. hello 캐시 주체 tooseparate IOPS 및 처리량 제한은 hello VM 수준 hello VM 크기에 따라 언제는입니다. DS 시리즈 VM은 대략 캐시 및 로컬 SSD I/O에 대해 코어당 4,000 IOPS 및 33MB/초입니다. GS 시리즈 VM은 캐시 및 로컬 SSD I/O에 대해 코어당 5,000 IOPS 및 50MB/초의 한도를 포함합니다. 

## <a name="throttling"></a>제한
조정이 발생할 수 있으며, IOPS 응용 프로그램이 나 처리량 프리미엄 저장소 디스크에 대 한 할당 된 hello 제한을 초과 합니다. 제한도 발생할 수 있습니다 hello VM에서 모든 디스크 전체 디스크 트래픽의 hello VM에 사용할 수 있는 hello 디스크 대역폭 제한을 초과 하는 경우. tooavoid 제한 hello 보류 중인 hello 디스크에 대 한 I/O 요청 수를 제한 하는 것이 좋습니다. 사용 해야만 프로 비전 하는 hello 디스크에 대 한 확장성 및 성능 목표가 hello 디스크 대역폭 사용 가능한 toohello VM 기반으로 하는 제한입니다.  

응용 프로그램을 디자인할 때 hello 가장 짧은 대기 시간을 얻을 수 tooavoid 제한 합니다. 그러나 hello 보류 중인 hello 디스크에 대 한 I/O 요청 수가 너무 작은 경우, 응용 프로그램 활용할 수 없습니다 hello은 사용할 수 있는 toohello 디스크 최대 IOPS 및 처리량 수준입니다.

다음 예제는 hello toocalculate 제한 수준 하는 방법을 보여 줍니다. 모든 계산은 256KB의 I/O 단위 크기를 기반으로 합니다.

### <a name="example-1"></a>예 1
응용 프로그램이 P10 디스크에서 초당 16KB 크기의 495개 I/O를 처리했습니다. hello I/O 단위 495 IOPS로 계산 됩니다. 2MB I/O를 시도 하면 동일한 두 번째 hello을 hello 총 I/O 단위의 같은 too495 + 8 IOPS입니다. 때문에 이것이 2MB I/O 2, 048 KB/256KB = 8 I/O 단위 = hello I/O 단위 크기는 256KB 있는 경우. 495 + 8의 합 hello hello 디스크에 대 한 hello 500 IOPS 제한을 초과 하기 때문에 제한이 발생 합니다.

### <a name="example-2"></a>예 2
응용 프로그램이 P10 디스크에서 256KB 크기의 400개 I/O를 처리했습니다. 사용 하는 hello 총 대역폭은 (400 &#215; 256) / 1, 024 KB = 100MB/s입니다. P10 디스크의 처리량 제한은 100MB/초입니다. 응용 프로그램이 해당 1 초 동안에서 tooperform 더 많은 I/O 작업 시도 하면, hello 할당 한도 초과 하기 때문에 제한 된 됩니다.

### <a name="example-3"></a>예 3
연결된 두 P30 디스크와 DS4 VM이 있습니다. 각 P30 디스크는 처리량이 200MB/초입니다. 하지만 DS4 VM은 256MB/초의 총 디스크 대역폭 용량입니다. Hello에이 DS4 VM에는 연결 된 디스크 toohello 최대 처리량을 감당할 수 없습니다 동시 합니다. tooresolve이를 하나의 디스크에 대 한 s 및 56 MB/s에서 다른 디스크 hello/200MB의 트래픽을 유지할 수 있습니다. 디스크 트래픽 hello 합계 256 m B/초를 초과, 디스크 트래픽을 제한 되었습니다.

> [!NOTE]
> 디스크 트래픽 대부분 구성 된 경우 작은 I/O 크기, 응용 프로그램 hello 처리량 한도 하기 전에 hello IOPS 제한에 도달 합니다. 그러나 hello 디스크 트래픽 대부분 구성 된 경우 대형 I/O 크기, 응용 프로그램은 제한에 도달 hello 처리량 먼저 hello IOPS 제한 대신. 최적 I/O 크기를 사용하여 응용 프로그램의 IOPS 및 처리 용량을 최대화할 수 있습니다. 또한 hello 대기 중인 디스크에 대 한 I/O 요청 수를 제한할 수 있습니다.
> 

프리미엄 저장소를 사용 하 여 고성능을 위해 설계에 대 한 더 toolearn 참조 [프리미엄 저장소와 성능 위한 디자인](storage-premium-storage-performance.md)합니다.

## <a name="snapshots-and-copy-blob"></a>Blob 스냅숏 생성 및 복사

toohello 저장소 서비스를 hello VHD 파일은 페이지 blob입니다. 페이지 blob의 스냅숏을 만들 수 있으며 tooa 다른 저장소 계정 등의 tooanother 위치를 복사할 수 있습니다.

### <a name="unmanaged-disks"></a>관리되지 않는 디스크

만들 [증분 스냅숏](../../virtual-machines/windows/incremental-snapshots.md) 같은 관리 되지 않는 프리미엄 디스크 hello에 대 한 스냅숏 저장소를 사용 하면 표준 방식으로 합니다. 프리미엄 저장소는 hello replication 옵션으로만 로컬 중복 저장소를 지원합니다. 스냅숏을 만들 다음 hello 스냅숏을 tooa 지리적 중복 표준 저장소 계정이 복사 하는 것이 좋습니다. 자세한 내용은 [Azure Storage 중복 옵션](storage-redundancy.md)을 참조하세요.

연결 된 tooa VM 디스크가 있는 경우 hello 디스크에서 일부 API 작업이 허용 되지 않습니다. 예를 들어 수행할 수 없습니다는 [Blob 복사](/rest/api/storageservices/Copy-Blob) hello 디스크가 경우 해당 blob에 대 한 작업이 tooa VM을 연결 합니다. 대신, hello를 사용 하 여 해당 blob의 스냅숏을 먼저 만들 [스냅숏 Blob](/rest/api/storageservices/Snapshot-Blob) REST API입니다. 그런 다음 hello 수행 [Blob 복사](/rest/api/storageservices/Copy-Blob) hello 스냅숏 toocopy hello의 디스크를 연결 합니다. 또는 hello 디스크를 분리 하 고 필요한 모든 작업을 수행할 수 있습니다.

다음 제한 hello toopremium 저장소 blob 스냅숏 적용 됩니다.

| 프리미엄 저장소 한도 | 값 |
| --- | --- |
| Blob당 최대 스냅숏 수 | 100 |
| 스냅숏의 저장소 계정 용량<br>(스냅숏의 데이터만 포함합니다. 기본 Blob의 데이터는 포함하지 않습니다.) | 10TB |
| 연속 스냅숏 사이의 최소 시간 | 10분 |

전자 메일로 toomaintain 지리적 중복 복사본을 AzCopy 또는 Blob 복사를 사용 하 여 스냅숏을 프리미엄 저장소 계정 tooa 표준 지역 중복 저장소 계정에서 복사할 수 있습니다. 자세한 내용은 참조 [hello AzCopy 명령줄 유틸리티와 함께 데이터를 전송](storage-use-azcopy.md) 및 [Blob 복사](/rest/api/storageservices/Copy-Blob)합니다.

프리미엄 저장소 계정에서 페이지 Blob에 대한 REST 작업을 수행하는 방법에 대한 자세한 내용은 [Azure Premium Storage로 Blob service 작업](http://go.microsoft.com/fwlink/?LinkId=521969)을 참조하세요.

### <a name="managed-disks"></a>관리 디스크

관리 되는 디스크에 대 한 스냅숏은 hello 관리 되는 디스크의 읽기 전용 복사본입니다. 표준 관리 디스크도 hello 스냅숏이 저장 됩니다. 현재 관리 디스크에 대해 [증분 스냅숏](../../virtual-machines/windows/incremental-snapshots.md)은 지원되지 않습니다. toolearn tootake 관리 되는 디스크에 대 한 스냅숏을 확인 하려면 어떻게 해야 [Azure 관리 되는 것에 저장 된 VHD의 복사본을 만들고 Windows에서 관리 되는 스냅숏을 사용 하 여 디스크](../../virtual-machines/windows/snapshot-copy-managed-disk.md) 또는 [Azure 관리 되는 것에 저장 된 VHD의 복사본을 만들 디스크 관리를 사용 하 여 Linux의 스냅숏은](../../virtual-machines/linux/snapshot-copy-managed-disk.md)합니다.

관리 되는 디스크를 연결 된 tooa VM 이면 hello 디스크에서 일부 API 작업이 허용 되지 않습니다. 예를 들어 hello 디스크가 연결 된 tooa VM 되는 동안 공유 액세스 서명 (SAS) tooperform 복사 작업을 생성할 수 없습니다. 대신 먼저 hello 디스크의 스냅숏을 만들고 hello 스냅숏의 hello 복사를 수행 합니다. 또는 hello 디스크를 분리 하 고 SAS tooperform hello 복사 작업을 생성 합니다.


## <a name="premium-storage-for-linux-vms"></a>Linux VM용 Premium Storage
Linux Vm의 프리미엄 저장소를 설정 하는 정보 toohelp 다음 hello를 사용할 수 있습니다.

프리미엄 저장소 디스크를 모든 너무 집합을 캐시에 대 한 프리미엄 저장소에서 대상으로 tooachieve 확장성**ReadOnly** 또는 **없음**, hello 파일 시스템을 탑재 하는 경우 "장애"를 사용 하지 않도록 해야 합니다. Hello toopremium 저장소 디스크는 이러한 캐시 설정에 대 한 내구성 기록 하기 때문에이 시나리오에서는 장벽이 필요는 없습니다. Hello 쓰기 요청이 성공적으로 완료 되 면 데이터가 기록 toohello 영구 저장소입니다. toodisable "장벽을" hello 메서드를 다음 중 하나를 사용 합니다. 파일 시스템에 대 한 hello 하나를 선택 합니다.
  
* 에 대 한 **reiserFS**, toodisable 장벽을 hello를 사용 하 여 `barrier=none` 옵션 탑재 합니다. (tooenable 장벽을 사용 하 여 `barrier=flush`.)
* 에 대 한 **ext3/ext4**, toodisable 장벽을 hello를 사용 하 여 `barrier=0` 옵션 탑재 합니다. (tooenable 장벽을 사용 하 여 `barrier=1`.)
* 에 대 한 **XFS**, toodisable 장벽을 hello를 사용 하 여 `nobarrier` 옵션 탑재 합니다. (tooenable 장벽을 사용 하 여 `barrier`.)
* 프리미엄 저장소 디스크의 캐시도**ReadWrite**, 장벽을 쓰기 내 구성을 사용 하도록 설정 합니다.
* 볼륨 레이블 toopersist hello VM을 다시 시작한 후 업데이트 해야 /etc/fstab hello 범용 고유 식별자 (UUID) 참조 toohello 디스크와 합니다. 자세한 내용은 참조 [추가 관리 되는 디스크 tooa Linux VM](../../virtual-machines/linux/add-disk.md)합니다.

다음의 Linux 배포판 hello Azure 프리미엄 저장소에 대 한 유효성 검사 되었습니다. 더 나은 성능과 안정성 프리미엄 저장소에 대 한 프로그램 Vm tooone 최소한 이러한 버전으로 업그레이드 하는 권장 (또는 tooa 이후 버전). Azure에 대 한 최신 Linux Integration Services LIS (), v 4.0 hello 일부 hello 버전이 필요 합니다. 분포를 설치 하 고 toodownload hello 표 다음에 나열 된 hello 링크를 따라 이동 합니다. 유효성 검사 완료 될 때 이미지 toohello 목록을 추가 합니다. 유효성 검사 시 이미지마다 성능이 다른 것으로 나타납니다. 성능은 워크로드 특성 및 이미지 설정에 따라 달라집니다. 다른 종류의 워크로드에 대해 서로 다른 이미지가 조정됩니다.

| 배포 | 버전 | 지원되는 커널 | 세부 정보 |
| --- | --- | --- | --- |
| Ubuntu | 12.04 | 3.2.0-75.110+ | Ubuntu-12_04_5-LTS-amd64-server-20150119-en-us-30GB |
| Ubuntu | 14.04 | 3.13.0-44.73+ | Ubuntu-14_04_1-LTS-amd64-server-20150123-en-us-30GB |
| Debian | 7.x, 8.x | 3.16.7-ckt4-1+ | &nbsp; |
| SUSE | SLES 12| 3.12.36-38.1+| suse-sles-12-priority-v20150213 <br> suse-sles-12-v20150213 |
| SUSE | SLES 11 SP4 | 3.0.101-0.63.1+ | &nbsp; |
| CoreOS | 584.0.0+| 3.18.4+ | CoreOS 584.0.0 |
| CentOS | 6.5, 6.6, 6.7, 7.0 | &nbsp; | [LIS4 필요](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Hello 다음 섹션의 참고를 참조 하십시오.* |
| CentOS | 7.1+ | 3.10.0-229.1.2.el7+ | [LIS4 권장](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Hello 다음 섹션의 참고를 참조 하십시오.* |
| RHEL(Red Hat Enterprise Linux) | 6.8+, 7.2+ | &nbsp; | &nbsp; |
| Oracle | 6.0+, 7.2+ | &nbsp; | UEK4 또는 RHCK |
| Oracle | 7.0-7.1 | &nbsp; | UEK4 또는 RHCK w/[LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |
| Oracle | 6.4-6.7 | &nbsp; | UEK4 또는 RHCK w/[LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |


### <a name="lis-drivers-for-openlogic-centos"></a>OpenLogic CentOS용 LIS 드라이버

OpenLogic CentOS Vm을 실행 하는 경우 최신 드라이버를 hello 명령 tooinstall hello를 실행 합니다.

```
sudo rpm -e hypervkvpd  ## (Might return an error if not installed. That's OK.)
sudo yum install microsoft-hyper-v
```

tooactivate hello 새 드라이버 hello 컴퓨터를 다시 시작 합니다.

## <a name="pricing-and-billing"></a>가격 책정 및 대금 청구

프리미엄 저장소를 사용 하 여 hello 청구 고려 사항에 따라 적용 됩니다.

* **프리미엄 저장소 디스크 및 Blob 크기**

    프리미엄 저장소 디스크 또는 blob에 대 한 청구 hello 디스크 또는 blob의 사용자를 프로 비전 하는 hello 크기에 따라 달라 집니다. Azure 지도 hello 프리미엄 저장소 디스크 옵션에 가장 가까운 toohello 프로 비전 된 크기 (반올림). 자세한 내용은 hello 표를 참조 [프리미엄 저장소 확장성 및 성능 목표가](#premium-storage-scalability-and-performance-targets)합니다. 각 디스크 지도 tooa 지원 디스크 크기를 프로 비전 하 고 그에 따라 요금이 청구 됩니다. 프리미엄 저장소 제공 hello에 대 한 월간 가격으로 hello를 사용 하 여 프로 비전 된 디스크에 대 한 청구 매시간 비례하여 지정 됩니다. 예를 들어 P10 디스크를 프로 비전 하 고 20 시간 후에 삭제 하는 경우 hello P10 할부 too20 시간 제공에 대 한 요금이 청구 됩니다. 이 hello 양의 기록 toohello 디스크 또는 hello IOPS 및 처리량이 사용 되는 실제 데이터에 관계 없이입니다.

* **프리미엄 관리되지 않는 디스크 스냅숏**

    관리 되지 않는 프리미엄 디스크에 대 한 스냅숏 hello 스냅숏에 사용 되는 hello 추가 용량에 대 한 요금이 청구 됩니다. 스냅숏에 대한 자세한 내용은 [Blob의 스냅숏 만들기](/rest/api/storageservices/Snapshot-Blob)를 참조하세요.

* **프리미엄 관리 디스크 스냅숏**

    관리 되는 디스크의 스냅숏은 hello 디스크의 읽기 전용 복사본입니다. hello 디스크 표준 관리 디스크도 저장 됩니다. 스냅숏 비용 hello 표준 관리 디스크는 동일 합니다. 예를 들어 128 GB 프리미엄 관리 되는 디스크의 스냅숏을 수행 하는 경우 hello hello 스냅숏 비용은 해당 tooa 128 GB 표준 관리 디스크입니다.  

* **아웃바운드 데이터 전송**

    [아웃바운드 데이터 전송](https://azure.microsoft.com/pricing/details/data-transfers/)(Azure 데이터 센터에서 데이터 전송) 시 대역폭 사용에 대해 청구가 발생합니다.

Premium Storage에 대한 가격 책정, Premium Storage 지원 VM 및 관리 디스크에 대해 자세히 알아보려면 다음 문서를 참조하세요.

* [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/storage/)
* [Virtual Machines 가격 책정](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [관리 디스크 가격 책정](https://azure.microsoft.com/pricing/details/managed-disks/)

## <a name="azure-backup-support"></a>Azure Backup 지원 

지역적 재해 복구를 위해 [Azure Backup](../../backup/backup-introduction-to-azure-backup.md) 및 GRS 저장소 계정을 백업 자격 증명 모음으로 사용하여 VM 디스크를 다른 지역에 백업해야 합니다.

백업 작업이 백업 보존 정책, 시간 기반 백업 및 쉽게 VM 복원할와 toocreate Azure 백업을 사용 합니다. 관리 및 관리되지 않는 디스크 모두에 Backup을 사용할 수 있습니다. 자세한 내용은 [관리되지 않는 디스크와 함께 VM용 Azure Backup](../../backup/backup-azure-vms-first-look-arm.md) 및 [관리 디스크와 함께 VM용 Azure Backup](../../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup)을 참조하세요. 

## <a name="next-steps"></a>다음 단계
프리미엄 저장소에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.

### <a name="design-and-implement-with-premium-storage"></a>Premium Storage를 사용하여 디자인 및 구현
* [Premium Storage를 사용한 성능을 위한 디자인](storage-premium-storage-performance.md)
* [Premium Storage에서 Blob Storage 작업](http://go.microsoft.com/fwlink/?LinkId=521969)

### <a name="operational-guidance"></a>운영 가이드
* [프리미엄 저장소 tooAzure 마이그레이션](../common/storage-migration-to-premium-storage.md)

### <a name="blog-posts"></a>블로그 게시물
* [일반적으로 제공되는 Azure Premium Storage](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)
* [GS 시리즈 hello 발표: 가장 큰 프리미엄 저장소 지원 toohello 추가 Vm에 hello 공용 클라우드](https://azure.microsoft.com/blog/azure-has-the-most-powerful-vms-in-the-public-cloud/)
