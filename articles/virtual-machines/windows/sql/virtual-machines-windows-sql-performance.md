---
title: "Azure의 SQL Server에 대 한 유용한 aaaPerformance | Microsoft Docs"
description: "Microsoft Azure VM에서 SQL Server 성능을 최적화하기 위한 모범 사례를 제공합니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a0c85092-2113-4982-b73a-4e80160bac36
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: jroth
ms.openlocfilehash: 42ec9fbeb2dec3a654b93bbd08d666369835ee73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-best-practices-for-sql-server-in-azure-virtual-machines"></a>Azure 가상 컴퓨터의 SQL Server에 대한 성능 모범 사례

## <a name="overview"></a>개요

이 항목에서는 Microsoft Azure 가상 컴퓨터의 SQL Server 성능을 최적화하기 위한 모범 사례를 제공합니다. 사용 하 여 계속 좋습니다 Azure 가상 컴퓨터의 SQL Server를 실행 되는 동안 동일한 데이터베이스 성능 튜닝 옵션을 온-프레미스 서버 환경에서 적용 가능한 tooSQL 서버 hello 합니다. 그러나 공용 클라우드에서 관계형 데이터베이스의 hello 성능은 가상 컴퓨터 및 hello 데이터 디스크의 hello 구성의 hello 크기와 같은 많은 요인에 따라 달라 집니다.

SQL Server 이미지를 만들 때 [hello Azure 포털에서에서 Vm을 프로 비전 하는 것이 좋습니다.](virtual-machines-windows-portal-sql-server-provision.md)합니다. SQL Server Vm hello 리소스 관리자와 포털에서에서 사용자를 프로 비전 hello 저장소 구성을 포함 하 여, 모든 권장 사항을 구현 합니다.

이 문서는 hello를 가져오는 데 *최상의* Azure Vm에서 SQL Server에 대 한 성능입니다. 작업이 적은 경우 아래 나열된 모든 최적화 사항이 필요하지 않을 수 있습니다. 이러한 권장 사항을 평가할 때 성능 요구 사항 및 작업 패턴을 고려하세요.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="quick-check-list"></a>빠른 검사 목록

hello 다음은 Azure 가상 컴퓨터에 SQL Server의 최적 성능에 대 한 빠른 검사 목록:

| 영역 | 최적화 |
| --- | --- |
| [VM 크기](#vm-size-guidance) |SQL Enterprise Edition [DS3](../../virtual-machines-windows-sizes-memory.md) 이상<br/><br/>SQL Standard 및 Web Edition [DS2](../../virtual-machines-windows-sizes-memory.md) 이상 |
| [저장소](#storage-guidance) |[프리미엄 저장소](../../../storage/common/storage-premium-storage.md)를 사용합니다. 표준 저장소는 개발/테스트에만 권장됩니다.<br/><br/>Hello 유지 [저장소 계정](../../../storage/common/storage-create-storage-account.md) hello에 SQL Server VM 및 동일한 지역입니다.<br/><br/>Azure를 사용 하지 않도록 설정 [지역 중복 저장소](../../../storage/common/storage-redundancy.md) (지리적 복제) hello 저장소 계정에 있습니다. |
| [디스크](#disks-guidance) |최소 2개의 [P30 디스크](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets)를 사용합니다(로그 파일용 1개, 데이터 파일 및 TempDB용 1개).<br/><br/>데이터베이스 저장소나 로깅을 위해 운영 체제 또는 임시 디스크를 사용하지 않습니다.<br/><br/>Hello 데이터 파일 및 TempDB 호스팅 hello 디스크에서 읽기 캐싱을 사용 하도록 설정 합니다.<br/><br/>Hello 로그 파일을 호스트 하는 디스크에 대 한 캐싱을 사용 하지 마십시오.<br/><br/>중요: hello SQL Server 서비스는 Azure VM 디스크에 대 한 hello 캐시 설정을 변경 하는 경우 중지 합니다.<br/><br/>여러 Azure 데이터 디스크 증가 tooget IO 처리량을 스트라이프 합니다.<br/><br/>문서화된 할당 크기로 포맷합니다. |
| [I/O](#io-guidance) |데이터베이스 페이지 압축을 사용하도록 설정합니다.<br/><br/>데이터 파일에 대해 즉시 파일 초기화를 사용하도록 설정합니다.<br/><br/>제한 하거나 hello 데이터베이스에서 자동 증가 사용 하지 않도록 설정 합니다.<br/><br/>Hello 데이터베이스에서 자동 축소를 사용 하지 않도록 설정 합니다.<br/><br/>시스템 데이터베이스를 비롯 한 모든 데이터베이스 toodata 디스크를 이동 합니다.<br/><br/>SQL Server 오류 로그 및 추적 파일 디렉터리 toodata 디스크를 이동 합니다.<br/><br/>기본 백업 및 데이터베이스 파일 위치를 설정합니다.<br/><br/>잠긴 페이지를 사용하도록 설정합니다.<br/><br/>SQL Server 성능 픽스를 적용합니다. |
| [기능 관련](#feature-specific-guidance) |직접 tooblob 저장소를 백업 합니다. |

대 한 자세한 내용은 *어떻게* 및 *이유* toomake 이러한 최적화를 검토 하십시오 hello 정보와 지침은 다음 섹션에 제공 합니다.

## <a name="vm-size-guidance"></a>VM 크기 지침

성능에 민감한 응용 프로그램에 대 한 것이 좋습니다 hello 다음을 사용 하는 [가상 컴퓨터 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json):

* **SQL Server Enterprise Edition**: DS3 이상
* **SQL Server Standard 및 Web Edition**: DS2 이상

## <a name="storage-guidance"></a>저장소 지침

DS 시리즈(DSv2 시리즈 및 GS 시리즈와 함께) VM은 [프리미엄 저장소](../../../storage/common/storage-premium-storage.md)를 지원합니다. 프리미엄 저장소는 모든 프로덕션 워크로드에 권장됩니다.

> [!WARNING]
> 표준 저장소는 대기 시간 및 대역폭이 다양하므로 개발/테스트 워크로드에만 권장됩니다. 프로덕션 워크로드에는 프리미엄 저장소를 사용해야 합니다.

또한 좋습니다 hello에 Azure 저장소 계정을 만들어야 하면 SQL Server 가상 컴퓨터 tooreduce 전송 지연와 동일한 데이터 센터입니다. 저장소 계정을 만들 때 여러 디스크 간에 일관된 쓰기 순서가 보장되지 않기 때문에 지역에서 복제를 사용하지 않도록 설정합니다. 대신 두 Azure 데이터 센터 간에 SQL Server 재해 복구 기술을 구성하는 것이 좋습니다. 자세한 내용은 [Azure Virtual Machines의 SQL Server에 대한 고가용성 및 재해 복구](virtual-machines-windows-sql-high-availability-dr.md)를 참조하세요.

## <a name="disks-guidance"></a>디스크 지침

Azure VM의 디스크 유형에는 크게 세 가지가 있습니다.

* **OS 디스크**: hello 플랫폼에서는 하나 이상의 디스크를 연결 하는 Azure 가상 컴퓨터를 만들 때 (hello로 표시 된 **C** 드라이브) 운영 체제 디스크에 대 한 VM toohello 합니다. 이 디스크는 저장소에 페이지 Blob으로 저장된 VHD입니다.
* **임시 디스크**: hello 임시 디스크 라는 다른 디스크를 포함 하는 Azure 가상 컴퓨터 (hello로 표시 된 **D**: 드라이브). 이 스크래치 공간에 사용할 수 있는 hello 노드에서 디스크입니다.
* **데이터 디스크**: 이러한 페이지 blob으로 저장소에 저장 되 고 추가 디스크 tooyour 가상 컴퓨터 데이터 디스크로 첨부할 수도 있습니다.

hello 다음 단원에서는 이러한 서로 다른 디스크를 사용 하기 위한 권장 사항.

### <a name="operating-system-disk"></a>운영 체제 디스크

운영 체제 디스크는 운영 체제의 실행 버전으로 부팅하고 탑재할 수 있는 VHD이며 **C** 드라이브로 레이블이 지정됩니다.

Hello 운영 체제 디스크의 기본 캐싱 정책은 **읽기/쓰기**합니다. 성능에 민감한 응용 프로그램에 대 한 hello 운영 체제 디스크 대신 데이터 디스크를 사용 하는 것이 좋습니다. 아래에 데이터 디스크에 hello 섹션을 참조 하십시오.

### <a name="temporary-disk"></a>임시 디스크

임시 저장소 드라이브를 hello로 표시 된 hello **D**: 드라이브 지속형된 tooAzure blob 저장소 않습니다. 사용자 데이터베이스 파일 또는 사용자 트랜잭션 로그 파일 hello 저장 하지 마십시오 **D**: 드라이브입니다.

D 시리즈, Dv2 시리즈 및 G 시리즈 Vm의 경우 이러한 Vm에서 hello 임시 드라이브는 SSD 기반 합니다. 작업 (예:에 대 한 임시 개체 또는 복잡 한 조인을) TempDB의 많이 사용 하는 경우 hello에 TempDB 저장 **D** 드라이브 TempDB 처리량이 늘어나며 발생 하 고 TempDB 대기 시간을 낮출 수 없습니다.

Premium Storage를 지원하는 VM(DS 시리즈, DSv2 시리즈 및 GS 시리즈)의 경우 읽기 캐싱을 사용하도록 설정된 Premium Storage를 지원하는 디스크에 TempDB를 저장하는 것이 좋습니다. 한 가지 예외 toothis 권장; TempDB 사용 쓰기 집약적 이면 TempDB hello 로컬에 저장 하 여 더 높은 성능을 얻을 수 있습니다 **D** 드라이브 SSD 기반 이러한 컴퓨터 크기에도 사용 됩니다.

### <a name="data-disks"></a>데이터 디스크

* **데이터 및 로그 파일에 대 한 데이터 디스크를 사용 하 여**: 여기에 최소한 2 프리미엄 저장소를 사용 하 여 [P30 디스크](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) 여기서 디스크 하나 hello 로그 파일을 포함 하 고 다른 hello hello 데이터 및 TempDB 파일이 포함 되어 있습니다. 각 프리미엄 저장소 디스크 hello 다음 문서에에서 설명 된 대로 다양 한 IOPs 및 대역폭 (MB/s)의 크기에 따라 제공: [디스크에 대 한 프리미엄 저장소를 사용 하 여](../../../storage/common/storage-premium-storage.md)합니다.

* **디스크 스트라이프**: 더 많은 처리량이 필요한 경우 추가 데이터 디스크를 추가하고 디스크 스트라이프를 사용할 수 있습니다. 데이터 디스크를 toodetermine hello 수 tooanalyze hello 수 IOPS 및 대역폭 및 데이터 및 TempDB 파일이 로그 파일에 대 한 필요한의 필요 합니다. 다른 VM 크기 hello 수 IOPs 및 대역폭 지원에 서로 다른 제한이 정의 되어 IOPS 수에 hello 테이블을 참조 하십시오 [VM 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 지침에 따라 hello를 사용 합니다.

  * Windows 8/Windows Server 2012 이상 인지를 사용 하 여 [저장소 공간](https://technet.microsoft.com/library/hh831739.aspx) 지침을 따르는 hello로:

      1. Hello 세트 (스트라이프 크기) interleave oltp 및 데이터 웨어하우징 워크 로드 tooavoid 성능에 미치는 영향 toopartition 정렬 오류 때문에 256KB (262144 바이트)에 대 한 too64 KB (65536 바이트)입니다. 이는 PowerShell로 설정되어야 합니다.
      1. 열 수를 실제 디스크 수로 설정합니다. 8개 이상의 디스크(서버 관리자 UI 아님)를 구성하는 경우 PowerShell을 사용합니다. 

    예를 들어 다음 PowerShell hello에서는 새 hello로 저장소 풀 크기 too64 KB 및 hello 개수 열 too2 인터리브:

    ```powershell
    $PoolCount = Get-PhysicalDisk -CanPool $True
    $PhysicalDisks = Get-PhysicalDisk | Where-Object {$_.FriendlyName -like "*2" -or $_.FriendlyName -like "*3"}

    New-StoragePool -FriendlyName "DataFiles" -StorageSubsystemFriendlyName "Storage Spaces*" -PhysicalDisks $PhysicalDisks | New-VirtualDisk -FriendlyName "DataFiles" -Interleave 65536 -NumberOfColumns 2 -ResiliencySettingName simple –UseMaximumSize |Initialize-Disk -PartitionStyle GPT -PassThru |New-Partition -AssignDriveLetter -UseMaximumSize |Format-Volume -FileSystem NTFS -NewFileSystemLabel "DataDisks" -AllocationUnitSize 65536 -Confirm:$false 
    ```

  * Windows 2008 R2 또는 이전 버전에서는 동적 디스크 (OS 스트라이프 볼륨)를 사용할 수 있습니다 및 hello 스트라이프 크기는 항상 64KB입니다. 이 옵션은 Windows 8/Windows Server 2012부터 사용되지 않습니다. Hello 지원 방침을 참조 하십시오 [가상 디스크 서비스 저장소 관리 API tooWindows 전환 중인](https://msdn.microsoft.com/library/windows/desktop/hh848071.aspx)합니다.

  * 작업에 로그가 많지 않고 전용 IOPS를 필요로 하지 않으면 1개의 저장소 풀만 구성할 수 있습니다. 그렇지 않으면, 저장소 풀 두 개, hello 로그 파일에 대 한와 hello 데이터 파일 및 TempDB에 대 한 다른 저장소 풀을 만듭니다. 사용자의 예상 부하에 따라 각 저장소 풀과 연결 된 디스크의 hello 번호를 확인 합니다. VM 크기가 다르면 연결된 데이터 디스크 수도 다를 수 있다는 점에 유의하세요. 자세한 내용은 [가상 컴퓨터의 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

  * Hello 권장 tooadd hello에서 지 원하는 데이터 디스크의 최대 수는 (개발/테스트 시나리오) 프리미엄 저장소를 사용 하지 않는 경우 사용자 [VM 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 디스크 스트라이프를 사용 합니다.

* **캐싱 정책은**: 프리미엄 저장소에 대 한 데이터 디스크의 데이터 파일 및 TempDB만 호스팅 hello 데이터 디스크에서 읽기 캐싱을 사용 하도록 설정 합니다. 프리미엄 저장소를 사용하지 않는 경우 모든 데이터 디스크에서 모든 캐싱을 사용하도록 설정하지 마세요. 에 대 한 디스크 캐싱 구성 참조 hello 다음 항목: [Set-azureosdisk](https://msdn.microsoft.com/library/azure/jj152847) 및 [Set-azuredatadisk](https://msdn.microsoft.com/library/azure/jj152851.aspx)합니다.

  > [!WARNING]
  > 데이터베이스 손상의 Azure VM 디스크 tooavoid hello 가능성 hello 캐시 설정을 변경할 때는 hello SQL Server 서비스를 중지 합니다.

* **NTFS 할당 단위 크기**: hello 데이터 디스크를 포맷할 때 것이 좋습니다 64KB 할당 단위 크기를 사용 하 여 TempDB 데이터 및 로그 파일에 대 한 합니다.

* **디스크 관리에 대 한 유용한 정보**: 데이터 디스크를 제거 하거나 캐시 변경 형식이 hello 변경 중 hello SQL Server 서비스를 중지 합니다. Hello 캐싱 설정이 서로 hello OS 디스크에서 변경 Azure hello VM을 중지, hello 캐시 종류를 변경 및 hello VM을 다시 시작 합니다. 데이터 디스크의 hello 캐시 설정 변경 되 면 hello VM이 중지 되지 않으면 했지만 hello 데이터 디스크 hello hello 하는 동안 VM 바꾼 다음 다시 연결에서 분리 되어 있습니다.

  > [!WARNING]
  > 이러한 작업 중 SQL Server 서비스 오류 toostop hello 데이터베이스 손상이 될 수 있습니다.

## <a name="io-guidance"></a>I/O 지침

* 응용 프로그램 및 요청을 병렬화 하는 경우 프리미엄 저장소로 hello 최상의 결과 높일 수 있습니다. 프리미엄 저장소는 hello IO 큐 깊이 인 시나리오 1 보다 큰 경우 (있더라도 저장소 집약적인) 단일 스레드 직렬 요청에 대 한 거의 없거나 전혀 없이 성능 향상을 보게 되므로 위해 설계 되었습니다. 예를 들어 SQLIO와 같은 성능 분석 도구의 hello 단일 스레드 테스트 결과 영향을 줄 수 있습니다.

* [데이터베이스 페이지 압축](https://msdn.microsoft.com/library/cc280449.aspx)을 사용하면 I/O가 많은 작업의 성능이 향상될 수 있습니다. 그러나 hello 데이터 압축 hello 데이터베이스 서버에서 hello CPU 소비를 늘릴 수 있습니다.

* 초기 파일 할당에 필요한 인스턴트 파일 초기화 tooreduce hello 시간을 설정 하는 것이 좋습니다. tootake 이점이 즉시 파일 초기화 SE_MANAGE_VOLUME_NAME와 hello SQL Server (MSSQLSERVER) 서비스 계정에 부여 하 고이 toohello 추가 **볼륨 관리 태스크 실행** 보안 정책입니다. SQL Server 플랫폼 이미지를 Azure에 대 한 사용 하는 경우 기본 서비스 계정 (NT Service\MSSQLSERVER) hello toohello는 추가 되지 않습니다 **볼륨 관리 태스크 실행** 보안 정책입니다. 즉, 즉시 파일 초기화는 SQL Server Azure 플랫폼 이미지에서 사용하도록 설정되어 있지 않습니다. SQL Server 서비스 계정 toohello hello를 추가한 후 **볼륨 관리 태스크 실행** 보안 정책, hello SQL Server 서비스를 다시 시작 합니다. 이 기능을 사용하기 위한 보안 고려 사항이 있을 수 있습니다. 자세한 내용은 [데이터베이스 파일 초기화](https://msdn.microsoft.com/library/ms175935.aspx)를 참조하세요.

* **자동 증가** toobe 예기치 않은 증가에 대비한 대책 것으로 간주 됩니다. 일상적으로 자동 증가를 사용하여 사용자 데이터 및 로그 증가를 관리하지 마세요. 사전 자동 증가 사용 하는 경우에 hello 크기 스위치를 사용 하 여 hello 파일을 증가 합니다.

* 확인 **자동 축소** 성능에 부정적인 영향을 줄 수 있습니다 사용할 수 없는 tooavoid 불필요 한 오버 헤드입니다.

* 시스템 데이터베이스를 비롯 한 모든 데이터베이스 toodata 디스크를 이동 합니다. 자세한 내용은 [시스템 데이터베이스 이동](https://msdn.microsoft.com/library/ms345408.aspx)을 참조하세요.

* SQL Server 오류 로그 및 추적 파일 디렉터리 toodata 디스크를 이동 합니다. SQL Server 구성 관리자에서 SQL Server 인스턴스를 마우스 오른쪽 단추로 클릭하고 속성을 선택하여 이를 수행할 수 있습니다. hello 오류 로그 및 추적 파일 설정에서에서 변경할 수 있습니다 hello **시작 매개 변수** 덤프 디렉터리 hello에 지정 된 탭 hello **고급** 탭 hello 스크린 샷 다음 위치를 보여 줍니다. toolook에 대 한 hello 오류 로그 시작 매개 변수입니다.

    ![SQL 오류 로그 스크린샷](./media/virtual-machines-windows-sql-performance/sql_server_error_log_location.png)

* 기본 백업 및 데이터베이스 파일 위치를 설정합니다. 이 항목에서는 hello 권장 사항을 사용 하 고 hello 서버 속성 창에 대 한 hello 변경 합니다. 자세한 내용은 [데이터 및 로그 파일 (SQL Server Management Studio)에 대 한 기본 위치 보기 또는 변경 hello](https://msdn.microsoft.com/library/dd206993.aspx)합니다. hello 다음 스크린 샷에서 위치를 보여 줍니다 toomake 이러한 변경 합니다.

    ![SQL 데이터 로그 및 백업 파일](./media/virtual-machines-windows-sql-performance/sql_server_default_data_log_backup_locations.png)
* Enable는 페이지 tooreduce IO 및 페이지 작업 잠겨 있습니다. 자세한 내용은 참조 [Enable hello Lock Pages in Memory Option (Windows)](https://msdn.microsoft.com/library/ms190730.aspx)합니다.

* SQL Server 2012를 실행 중인 경우 서비스 팩 1 누적 업데이트 10을 설치합니다. 이 업데이트를 SQL Server 2012에서 임시 테이블 구문을 선택 해 서 실행 하면 I/O 성능이 저하 됨에 대 한 hello 수정을 포함 합니다. 자세한 내용은 [기술 자료 문서](http://support.microsoft.com/kb/2958012)를 참조하세요.

* 모든 데이터 파일은 Azure에서 송수신할 때 압축하는 것이 좋습니다.

## <a name="feature-specific-guidance"></a>기능 관련 지침

더 많은 고급 구성 기술을 사용하면 일부 배포에서 추가적인 성능 이점을 얻을 수 있습니다. hello 다음 목록에서는 tooachieve 더 나은 성능을 개선할 수 있는 일부 SQL Server 기능:

* **백업 tooAzure 저장소**: Azure 가상 컴퓨터에서 실행 중인 SQL Server에 대 한 백업을 수행 하는 경우 사용할 수 있습니다 [SQL Server 백업 tooURL](https://msdn.microsoft.com/library/dn435916.aspx)합니다. 이 기능은 SQL Server 2012 SP1 CU2부터 사용 가능 하 고 toohello 연결 된 데이터 디스크를 백업 하기 위한 권장 합니다. 하면 백업/복원/Azure 저장소에서에서 제공 되는 hello 권장을 수행 하는 경우 [SQL Server 백업 tooURL 모범 사례 및 문제 해결 및 Azure 저장소에 저장 된 백업 으로부터 복원](https://msdn.microsoft.com/library/jj919149.aspx)합니다. [Azure 가상 컴퓨터의 SQL Server에 대한 자동화된 백업](virtual-machines-windows-sql-automated-backup.md)을 사용하여 이러한 백업을 자동화할 수도 있습니다.

    사용할 수 있습니다 이전 tooSQL Server 2012, [SQL Server 백업 도구 tooAzure](https://www.microsoft.com/download/details.aspx?id=40740)합니다. 이 도구에는 여러 개의 백업 스트라이프 대상을 사용 하 여 tooincrease 백업 처리량 데 도움이 됩니다.

* **Azure의 SQL Server 데이터 파일**: SQL Server 2014부터 새로운 기능인 [Azure의 SQL Server 데이터 파일](https://msdn.microsoft.com/library/dn385720.aspx)을 사용할 수 있습니다. Azure에서 데이터 파일로 SQL Server를 실행하면 Azure 데이터 디스크를 사용하는 것과 견줄 만한 성능 특성을 보여 줍니다.

## <a name="next-steps"></a>다음 단계

보안 모범 사례는 [Azure Virtual Machines의 SQL Server에 대한 보안 고려 사항](virtual-machines-windows-sql-security.md)을 참조하세요.

[Azure Virtual Machines의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)에서 다른 SQL Server 가상 컴퓨터 항목을 검토하세요.
