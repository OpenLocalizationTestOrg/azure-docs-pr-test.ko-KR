---
title: "Azure Site Recovery를 사용 하 여 보호에서 aaaExclude 디스크 | Microsoft Docs"
description: "VM tooexclude VMware tooAzure 및 Hyper-v tooAzure 시나리오에 대 한 복제에서 디스크를 근거, 방법에 대해 설명 합니다."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: f47146bc57aeab3fce90123d0894fa86dde93417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exclude-disks-from-replication"></a>복제에서 디스크 제외
이 문서에서는 tooexclude 복제에서 디스크 하는 방법을 설명 합니다. 이런 식으로이 제외 hello 사용 된 복제 대역폭을 최적화 하거나 이러한 디스크를 활용 하는 hello 대상 쪽 리소스 최적화 수 있습니다. hello 기능은 VMware tooAzure 및 Hyper-v tooAzure 시나리오에 대 한 지원 됩니다.

## <a name="prerequisites"></a>필수 조건

기본적으로 컴퓨터의 모든 디스크가 복제됩니다. tooexclude 복제에서 디스크를 수동으로 설치 해야 hello 모바일 서비스 hello 컴퓨터에서 VMware tooAzure에서 복제 하는 경우 복제를 활성화 하기 전에.


## <a name="why-exclude-disks-from-replication"></a>복제에서 디스크를 제외하는 이유는?
다음과 같은 이유로 복제에서 디스크를 제외해야 하는 경우가 자주 있습니다.

- 제외 된 hello 디스크에 churned hello 데이터 중요 하지 않거나 복제 toobe 필요 하지 않습니다.

- 이 데이터를 복제 하지 않는 여 toosave 저장소 및 네트워크 리소스를 원하는 합니다.

## <a name="what-are-hello-typical-scenarios"></a>Hello 일반적인 시나리오는 무엇입니까?
제외에 적합한 후보가 되는 데이터 변동의 구체적인 예를 확인할 수 있습니다. 이러한 기호 tooa 페이징 파일 (pagefile.sys)을 작성 하 고 Microsoft SQL Server의 toohello tempdb 파일에 기록 합니다. Hello 작업과 hello 저장소 하위 시스템에 따라 hello 페이징 파일에는 상당한 양의 변동 등록할 수 있습니다. 그러나 hello 주 사이트 tooAzure에서이 데이터를 복제할 것 리소스를 많이 사용 합니다. 따라서 hello 운영 체제와 hello 페이징 파일에 있는 단일 가상 디스크를 가상 컴퓨터의 toooptimize 복제 단계를 수행 하는 hello를 사용할 수 있습니다.

1. 두 개의 가상 디스크를 hello 단일 가상 디스크를 분할 합니다. 가상 디스크가 하나 hello 운영 체제에 있고 다른 hello hello 페이징 파일입니다.
2. 복제에서 hello 페이징 파일 디스크를 제외 합니다.

마찬가지로, hello 시스템 데이터베이스 파일 및 hello 단계 toooptimize 디스크에 모두 hello Microsoft SQL Server tempdb 파일에 다음을 사용할 수 있습니다.

1. 두 개의 서로 다른 디스크에 hello 시스템 데이터베이스 및 tempdb를 유지 합니다.
2. Hello tempdb 디스크 복제에서 제외 합니다.

## <a name="how-tooexclude-disks-from-replication"></a>어떻게 tooexclude 복제에서 디스크?

### <a name="vmware-tooazure"></a>VMware tooAzure
Hello에 따라 [복제 사용](site-recovery-vmware-to-azure.md) 워크플로 tooprotect hello Azure Site Recovery 포털에서 가상 컴퓨터. Hello 워크플로의 hello 네 번째 단계에서는 hello를 사용 하 여 **디스크 tooREPLICATE** 열 tooexclude 디스크 복제를 선택 합니다. 기본적으로 모든 디스크가 복제하도록 선택됩니다. Tooexclude 복제 및 전체 다음 hello 단계 tooenable 복제에서 디스크의 hello 확인란의 선택을 취소 합니다.

![복제에서 디스크를 제외 하 고 VMware tooAzure 장애 복구에 대 한 복제를 사용 하도록 설정](./media/site-recovery-exclude-disk/v2a-enable-replication-exclude-disk1.png)


>[!NOTE]
>
> * 이미 hello 이동성 서비스가 설치 되어 있는 디스크만 제외할 수 있습니다. Toomanually 설치 hello 모바일 서비스가 필요 하면 복제를 설정한 다음 hello 푸시 메커니즘을 사용 하 여 hello 모바일 서비스에만 설치 됩니다.
> * 기본 디스크만 복제에서 제외할 수 있습니다. 운영 체제 또는 동적 디스크를 제외할 수 없습니다.
> * 복제를 사용하도록 설정한 후 복제에 대해 디스크를 추가 또는 제거할 수 없습니다. Tooadd 원하는 디스크를 제외 하거나, hello 컴퓨터에 대 한 toodisable 보호가 필요 하 고 다시 활성화 합니다.
> * 장애 조치 tooAzure 후 필요한 응용 프로그램 toooperate 프로그램에 대 한 디스크를 제외 하는 경우 복제 된 hello 응용 프로그램 실행 될 수 있도록 Azure에서 수동으로 toocreate hello 디스크를 해야 합니다. 또는 hello 컴퓨터의 장애 조치 하는 동안 Azure 자동화를 복구 계획 toocreate hello 디스크에 통합할 수 있습니다.
> * Window 가상 컴퓨터: Azure에서 수동으로 만드는 디스크는 장애 복구되지 않습니다. 예를 들어 디스크 세 개를 장애 조치하고 Azure Virtual Machines에서 디스크 두 개를 직접 만들면 장애 조치된 디스크 세 개만 장애 복구됩니다. 장애 복구 또는 온-프레미스 tooAzure에서 다시 보호에서 수동으로 만든 디스크를 포함할 수 없습니다.
> * Linux 가상 컴퓨터: Azure에서 수동으로 만드는 디스크는 장애 복구됩니다. 예를 들어 디스크 세 개를 장애 조치(failover)하고 Azure Virtual Machines에서 디스크 두 개를 직접 만들면 다섯 개 모두 장애 복구됩니다. 장애 복구에서 수동으로 만든 디스크는 제외할 수 없습니다.
>

### <a name="hyper-v-tooazure"></a>Hyper-v tooAzure
Hello에 따라 [복제 사용](site-recovery-hyper-v-site-to-azure.md) 워크플로 tooprotect hello Azure Site Recovery 포털에서 가상 컴퓨터. Hello 워크플로의 hello 네 번째 단계에서는 hello를 사용 하 여 **디스크 tooREPLICATE** 열 tooexclude 디스크 복제를 선택 합니다. 기본적으로 모든 디스크가 복제하도록 선택됩니다. Tooexclude 복제 및 전체 다음 hello 단계 tooenable 복제에서 디스크의 hello 확인란의 선택을 취소 합니다.

![복제에서 디스크를 제외 하 고 Hyper-v tooAzure 장애 복구에 대 한 복제를 사용 하도록 설정](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

>[!NOTE]
>
> * 기본 디스크만 복제에서 제외할 수 있습니다. 운영 체제 디스크를 제외할 수 없습니다. 동적 디스크는 제외하지 않는 것이 좋습니다. Azure Site Recovery는 가상 하드 디스크 (VHD)는 기본 또는 동적 이므로 hello 게스트 가상 컴퓨터를 식별할 수 없습니다.  모든 종속 동적 볼륨 디스크를 제외 하지 않으면 hello 보호 된 동적 디스크는 장애 조치 가상 컴퓨터에서 오류가 발생 한 디스크 되며 hello 해당 디스크에 데이터에 액세스할 수 없기.
> * 복제를 사용하도록 설정한 후 복제에 대해 디스크를 추가 또는 제거할 수 없습니다. Tooadd 원하는 디스크를 제외 하거나, toodisable 보호 hello 가상 컴퓨터에 대 한 필요 하 고 다시 활성화 합니다.
> * 응용 프로그램 toooperate에 필요한 디스크를 제외 하면 장애 조치 tooAzure 후 해야 Azure에서 수동으로 toocreate hello 디스크 복제 hello 응용 프로그램 실행 될 수 있도록 합니다. 또는 hello 컴퓨터의 장애 조치 하는 동안 Azure 자동화를 복구 계획 toocreate hello 디스크에 통합할 수 있습니다.
> * Azure에서 수동으로 만드는 디스크는 장애 복구되지 않습니다. 예를 들어 디스크 3 개 상에 실패 하 고 직접 Azure 가상 컴퓨터에서 두 개 이상의 디스크를 만들 경우 Azure tooHyper-V를 다시 장애 조치 된 3 개의 디스크 장애 됩니다. 장애 복구 또는 Hyper-v tooAzure에서 역방향 복제를 수동으로 만든 디스크를 포함할 수 없습니다.



## <a name="end-to-end-scenarios-of-exclude-disks"></a>디스크 제외의 종단 간 시나리오
두 시나리오 toounderstand hello 제외 디스크 기능을 살펴보겠습니다.

- SQL Server tempdb 디스크
- 페이징 파일(pagefile.sys) 디스크

### <a name="exclude-hello-sql-server-tempdb-disk"></a>Hello SQL Server tempdb 디스크는 제외
제외할 수 있는 tempdb가 있는 SQL Server 가상 컴퓨터를 살펴보겠습니다.

hello hello 가상 디스크의 이름이 SalesDB 합니다.

Hello 원본 가상 컴퓨터 디스크에는 다음과 같습니다.


**디스크 이름** | **게스트 운영 체제 디스크#** | **드라이브 문자** | **Hello 디스크에 데이터 형식**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | 운영 체제 디스크
DB-Disk1| Disk1 | D:\ | SQL 시스템 데이터베이스 및 사용자 데이터베이스 1
DB-디스크 2 (보호에서 제외 된 hello 디스크) | Disk2 | E:\ | 임시 파일
DB-Disk3 (보호에서 제외 된 hello 디스크) | Disk3 | F:\ | SQL tempdb 데이터베이스 (폴더 경로 (F:\MSSQL\Data\) < b r/>< b r/> 장애 조치 하기 전에 hello 폴더 경로 기록 합니다.
DB-Disk4 | Disk4 |G:\ |사용자 데이터베이스 2

이기 때문에 두 개의 hello 가상 컴퓨터의 디스크에 데이터 변동이 일시적 이며 hello SalesDB 가상 컴퓨터를 보호 하는 동안 디스크 2 및 Disk3 복제에서 제외 합니다. Azure Site Recovery는 해당 디스크를 복제하지 않습니다. 장애 조치 시 해당 디스크 hello Azure에서 가상 컴퓨터를 장애 조치 되지 않습니다.

디스크 hello Azure 가상 컴퓨터 장애 조치 후에 다음과 같습니다.

**게스트 운영 체제 디스크#** | **드라이브 문자** | **Hello 디스크에 데이터 형식**
--- | --- | ---
DISK0 | C:\ | 운영 체제 디스크
Disk1 | E:\ | 임시 저장 < b r / >< b r / > Azure이이 디스크를 추가 하 고 hello 첫 번째 사용 가능한 드라이브 문자를 지정 합니다.
Disk2 | D:\ | SQL 시스템 데이터베이스 및 사용자 데이터베이스 1
Disk3 | G:\ | 사용자 데이터베이스 2

E: 디스크 2 및 Disk3 hello SalesDB 가상 컴퓨터에서 제외 된, 이므로 hello 사용 가능한 목록에서 첫 번째 드라이브 문자 hello 합니다. Azure e: toohello 임시 저장소 볼륨을 할당합니다. 모든 복제 hello 디스크에 대 한 hello 드라이브 문자 유지 hello 동일 합니다.

Hello SQL tempdb 디스크 하 던 Disk3 (tempdb 폴더 경로 F:\MSSQL\Data\), 복제에서 제외 되었습니다. hello 디스크 hello 장애 조치 가상 컴퓨터에서 사용할 수 없는 경우 결과적으로, hello SQL 서비스 중지 상태에서 이며 hello F:\MSSQL\Data 경로 해야 합니다.

이 경로 두 가지 방법으로 toocreate:

- 새 디스크를 추가하고 tempdb 폴더 경로를 할당합니다.
- Hello tempdb 폴더 경로 대 한 기존 임시 저장소 디스크를 사용 합니다.

#### <a name="add-a-new-disk"></a>새 디스크 추가:

1. SQL tempdb.mdf 및 장애 조치 하기 전에 고려의 hello 경로 적어 둡니다.
2. Hello Azure 포털에서에서 새 디스크 toohello 장애 조치 가상 컴퓨터 추가 hello와 같거나 크기가 더 hello 소스 SQL tempdb 디스크 (Disk3)과 같은 합니다.
3. Azure 가상 컴퓨터 toohello에 로그인 합니다. Hello 디스크 관리 (diskmgmt.msc) 콘솔에서 초기화 및 포맷 hello 새로 추가 된 디스크.
4. 같은 드라이브 문자 hello SQL tempdb 디스크 (f:)에서 사용 하는 할당 번호입니다.
5. Hello f: 볼륨 (F:\MSSQL\Data)에서 tempdb 폴더를 만듭니다.
6. Hello 서비스 콘솔에서 hello SQL 서비스를 시작 합니다.

#### <a name="use-an-existing-temporary-storage-disk-for-hello-sql-tempdb-folder-path"></a>Hello SQL tempdb 폴더 경로 대 한 기존 임시 저장소 디스크를 사용 합니다.

1. 명령 프롬프트를 엽니다.
2. Hello 명령 프롬프트에서 복구 모드에서 SQL Server를 실행 합니다.

        Net start MSSQLSERVER /f / T3608

3. Hello sqlcmd toochange hello tempdb 경로 toohello 새 경로 따라를 실행 합니다.

        sqlcmd -A -S SalesDB        **Use your SQL DBname**
        USE master;     
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = tempdev, FILENAME = 'E:\MSSQL\tempdata\tempdb.mdf');
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = templog, FILENAME = 'E:\MSSQL\tempdata\templog.ldf');       
        GO


4. Hello Microsoft SQL Server 서비스를 중지 합니다.

        Net stop MSSQLSERVER
5. Hello Microsoft SQL Server 서비스를 시작 합니다.

        Net start MSSQLSERVER

임시 저장소 디스크에 대 한 Azure 지침 따르면 toohello를 참조 하십시오.

* [Azure Vm toostore SQL Server TempDB 및 버퍼 풀 확장에서 Ssd를 사용 하 여](https://blogs.technet.microsoft.com/dataplatforminsider/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)
* [Azure Virtual Machines의 SQL Server에 대한 성능 모범 사례](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

### <a name="failback-from-azure-tooan-on-premises-host"></a>장애 복구 (Azure tooan 온-프레미스 호스트)에서
이제 Azure tooyour 온-프레미스 Hyper-v 또는 VMware 호스트에서 장애 조치 될 때 복제 된 hello 디스크에 대해 알아보겠습니다. Azure에서 수동으로 만드는 디스크는 복제되지 않습니다. 예를 들어 디스크 세 개를 장애 조치하고 Azure Virtual Machines에서 두 개를 직접 만들면 장애 조치된 디스크 세 개만 장애 복구됩니다. 장애 복구 또는 온-프레미스 tooAzure에서 다시 보호에서 수동으로 생성 된 디스크를 포함할 수 없습니다. Hello 임시 저장소 디스크 tooon 온-프레미스 호스트 복제 하지 않습니다.

#### <a name="failback-toooriginal-location-recovery"></a>장애 복구 toooriginal 위치 복구

Hello 이전 예제에서는 Azure 가상 컴퓨터 디스크 구성을 hello는 다음과 같습니다.

**게스트 운영 체제 디스크#** | **드라이브 문자** | **Hello 디스크에 데이터 형식**
--- | --- | ---
DISK0 | C:\ | 운영 체제 디스크
Disk1 | E:\ | 임시 저장 < b r / >< b r / > Azure이이 디스크를 추가 하 고 hello 첫 번째 사용 가능한 드라이브 문자를 지정 합니다.
Disk2 | D:\ | SQL 시스템 데이터베이스 및 사용자 데이터베이스 1
Disk3 | G:\ | 사용자 데이터베이스 2


#### <a name="vmware-tooazure"></a>VMware tooAzure
Toohello 원래 위치로 장애 복구 완료 되 면 hello 장애 복구 가상 컴퓨터 디스크 구성에서 제외 된 디스크를 필요가 없습니다. VMware tooAzure에서 제외 된 디스크는 hello 장애 복구 가상 컴퓨터에서 사용할 수 없습니다.

Azure tooon 온-프레미스 VMware에서 계획 된 장애 조치 후 hello VMWare 가상 컴퓨터 (원래 위치) 디스크에는 다음과 같습니다.

**게스트 운영 체제 디스크#** | **드라이브 문자** | **Hello 디스크에 데이터 형식**
--- | --- | ---
DISK0 | C:\ | 운영 체제 디스크
Disk1 | D:\ | SQL 시스템 데이터베이스 및 사용자 데이터베이스 1
Disk2 | G:\ | 사용자 데이터베이스 2

#### <a name="hyper-v-tooazure"></a>Hyper-v tooAzure
장애 복구는 toohello 원래 위치를 hello 장애 복구 가상 컴퓨터 디스크 구성 남아 있는 Hyper-v에 대 한 원래 가상 컴퓨터 디스크 구성의 동일를 hello 합니다. Hyper-v 사이트 tooAzure에서 제외 된 디스크는 hello 장애 복구 가상 컴퓨터에서 사용할 수 있습니다.

Azure tooon 온-프레미스 Hyper-v에서 계획 된 장애 조치 후 hello Hyper-v 가상 컴퓨터 (원래 위치) 디스크에는 다음과 같습니다.

**디스크 이름** | **게스트 운영 체제 디스크#** | **드라이브 문자** | **Hello 디스크에 데이터 형식**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 |   C:\ | 운영 체제 디스크
DB-Disk1 | Disk1 | D:\ | SQL 시스템 데이터베이스 및 사용자 데이터베이스 1
DB-Disk2(제외된 디스크) | Disk2 | E:\ | 임시 파일
DB-Disk3(제외된 디스크) | Disk3 | F:\ | SQL tempdb 데이터베이스(폴더 경로(F:\MSSQL\Data\))
DB-Disk4 | Disk4 | G:\ | 사용자 데이터베이스 2


#### <a name="exclude-hello-paging-file-pagefilesys-disk"></a>Hello 페이징 파일 (pagefile.sys) 디스크는 제외

제외할 수 있는 페이징 파일 디스크가 있는 가상 컴퓨터를 살펴보겠습니다.
다음 두 가지 경우가 있습니다.

#### <a name="case-1-hello-paging-file-is-configured-on-hello-d-drive"></a>사례 1: hello 페이징 파일 hello d: 드라이브에 구성 된
Hello 디스크 구성은 다음과 같습니다.


**디스크 이름** | **게스트 운영 체제 디스크#** | **드라이브 문자** | **Hello 디스크에 데이터 형식**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | 운영 체제 디스크
DB-Disk1 (hello 보호에서 제외 된 hello 디스크) | Disk1 | D:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | 사용자 데이터 1
DB-Disk3 | Disk3 | F:\ | 사용자 데이터 2

Hello 페이징 파일 설정을 hello 원본 가상 컴퓨터에는 다음과 같습니다.

![원본 가상 컴퓨터의 페이징 파일 설정](./media/site-recovery-exclude-disk/pagefile-on-d-drive-sourceVM.png)


VMware tooAzure 또는 Hyper-v tooAzure hello 가상 컴퓨터의 장애 조치 후 디스크 hello Azure 가상 컴퓨터에는 다음과 같습니다.

**디스크 이름** | **게스트 운영 체제 디스크#** | **드라이브 문자** | **Hello 디스크에 데이터 형식**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | 운영 체제 디스크
DB-Disk1 | Disk1 | D:\ | 임시 저장소</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | 사용자 데이터 1
DB-Disk3 | Disk3 | F:\ | 사용자 데이터 2

D: Disk1 (d:)를 제외 되므로 hello hello 사용 가능한 목록에서 첫 번째 드라이브 문자. Azure는 d: toohello 임시 저장소 볼륨을 할당합니다. D:를 hello Azure 가상 컴퓨터에서 사용할 수 있으므로 가상 컴퓨터 유지 hello의 hello 페이징 파일 설정이 hello 동일 합니다.

Hello 페이징 파일 설정을 hello Azure 가상 컴퓨터에는 다음과 같습니다.

![Azure Virtual Machine의 페이징 파일 설정](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover.png)

#### <a name="case-2-hello-paging-file-is-configured-on-another-drive-other-than-d-drive"></a>사례 2: hello 페이징 파일 (d: 드라이브) 이외의 다른 드라이브에 구성 된

Hello 원본 가상 컴퓨터 디스크 구성을 다음과 같습니다.

**디스크 이름** | **게스트 운영 체제 디스크#** | **드라이브 문자** | **Hello 디스크에 데이터 형식**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | 운영 체제 디스크
DB-Disk1 (보호에서 제외 된 hello 디스크) | Disk1 | G:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | 사용자 데이터 1
DB-Disk3 | Disk3 | F:\ | 사용자 데이터 2

Hello 페이징 파일 설정을 hello 온-프레미스 가상 컴퓨터에는 다음과 같습니다.

![페이징 hello 온-프레미스 가상 컴퓨터에서 파일 설정](./media/site-recovery-exclude-disk/pagefile-on-g-drive-sourceVM.png)

Hello tooAzure VMware/Hyper-v 기반에서으로 가상 컴퓨터의 장애 조치 후 디스크 hello Azure 가상 컴퓨터에는 다음과 같습니다.

**디스크 이름**| **게스트 운영 체제 디스크#**| **드라이브 문자** | **Hello 디스크에 데이터 형식**
--- | --- | --- | ---
DB-Disk0-OS | DISK0  |C:\ |운영 체제 디스크
DB-Disk1 | Disk1 | D:\ | 임시 저장소</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | 사용자 데이터 1
DB-Disk3 | Disk3 | F:\ | 사용자 데이터 2

D: hello 사용 가능한 hello 목록에서 첫 번째 드라이브 문자 이기 때문에 Azure는 d: toohello 임시 저장소 볼륨을 할당 합니다. 모든 복제 hello 디스크에 대 한 hello 드라이브 문자 남아 hello 동일 합니다. Hello g: 디스크 사용 가능 하지 않으므로 hello 시스템 페이징 파일 hello에 대 한 hello c: 드라이브를 사용 합니다.

Hello 페이징 파일 설정을 hello Azure 가상 컴퓨터에는 다음과 같습니다.

![Azure Virtual Machine의 페이징 파일 설정](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover-2.png)

## <a name="next-steps"></a>다음 단계
배포가 설정되고 실행된 후에는 다양한 장애 조치(Failover)에 대해 [자세히 알아보세요](site-recovery-failover.md).
