---
title: "SharePoint 용 StorSimple 어댑터 aaaInstall | Microsoft Docs"
description: "설명 방법을 tooinstall 및 구성 하거나 SharePoint 서버 팜의 SharePoint 용 StorSimple 어댑터 hello를 제거 합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 9a7347232fb80156d93212e6382cdd4fab98a2d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-hello-storsimple-adapter-for-sharepoint"></a>설치 및 SharePoint 용 StorSimple 어댑터 hello 구성
## <a name="overview"></a>개요
hello SharePoint 용 StorSimple 어댑터는 Microsoft Azure StorSimple 유연한 저장소와 데이터 보호 tooSharePoint 서버 팜을 제공할 수 있도록 하는 구성 요소입니다. Hello SQL Server 콘텐츠 데이터베이스 toohello Microsoft Azure StorSimple 하이브리드 클라우드 저장소 장치로의 hello 어댑터 toomove 큰 BLOB (Binary Object) 콘텐츠를 사용할 수 있습니다.

hello SharePoint 용 StorSimple 어댑터 기능을 원격 RBS (BLOB Storage) 공급자 하며 사용 하 여 SQL Server Remote BLOB Storage 기능 toostore hello 구조화 되지 않은 SharePoint 콘텐츠 (Blob 형식 hello) StorSimple 장치에서 지 원하는 파일 서버에 있습니다.

> [!NOTE]
> SharePoint 용 StorSimple 어댑터 hello SharePoint Server 2010 원격 BLOB 저장소 (RBS)를 지원합니다. SharePoint Server 2010 EBS(External BLOB Storage)를 지원하지 않습니다.


* SharePoint 용 StorSimple 어댑터 toodownload hello 너무 이동[SharePoint 용 StorSimple 어댑터] [ 1] hello Microsoft 다운로드 센터에서에서.
* RBS 및 RBS 제한 계획에 대 한 내용은 이동 너무[결정 하는 SharePoint 2013의 RBS toouse] [ 2] 또는 [(SharePoint Server 2010) RBS 계획] [3].

hello이 개요의 나머지 부분 간략하게 설명 hello 및 역할에 SharePoint 용 StorSimple 어댑터 hello hello SharePoint 용량 및 성능 한도 수의 설치 및 hello 어댑터를 구성 하기 전에 합니다. 이 정보를 검토 한 후 이동 너무[SharePoint 용 StorSimple 어댑터](#storsimple-adapter-for-sharepoint-installation) toobegin hello 어댑터 설정 합니다.

### <a name="storsimple-adapter-for-sharepoint-benefits"></a>SharePoint용 StorSimple 어댑터의 이점
SharePoint 사이트에서 콘텐츠는 하나 이상의 콘텐츠 데이터베이스에 구조화되지 않은 BLOB 데이터로 저장됩니다. 기본적으로 이러한 데이터베이스는 SQL Server를 실행 하 고 SharePoint 서버 팜의 hello에 살고 있는 여부를 지정 하는 컴퓨터에서 호스팅됩니다. BLOB는 신속하게 크기가 증가할 수 있으며 이는 많은 온-프레미스 저장소를 소비합니다. 이러한 이유로 toofind 할 수 있습니다 더 저렴 다른 저장소 솔루션입니다. SQL Server 원격 Blob 저장소 (RBS) hello SQL Server 데이터베이스 외부의 hello 파일 시스템에 BLOB 콘텐츠를 저장할 수 있는 라고 하는 기술을 제공 합니다. Rbs를 사용 하면 Blob hello 파일 시스템에서 SQL Server를 실행 하는 hello 컴퓨터에 상주 하거나 다른 서버 컴퓨터의 hello 파일 시스템에 저장할 수 있습니다.

RBS는 hello tooenable SharePoint에서 RBS SharePoint 용 StorSimple 어댑터와 같은 RBS 공급자를 사용 해야 합니다. RBS를 유지할 수 있으므로 Blob tooa 서버 hello Microsoft Azure StorSimple 시스템에 의해 백업 이동 hello SharePoint 용 StorSimple 어댑터 작동 합니다. Microsoft Azure StorSimple 다음 hello BLOB 데이터 저장 로컬 또는 hello 클라우드 사용량에 따라 합니다. 매우 활발 하는 Blob (일반적으로 참조 tooas 계층 1 또는 핫 데이터) 로컬로 상주 합니다. 빈도가 낮은 데이터와 보관 데이터 hello 클라우드에 상주합니다. 콘텐츠 데이터베이스에서 RBS를 사용 하도록 설정한 후 SharePoint에서 만든 모든 새 BLOB 콘텐츠는 hello 콘텐츠 데이터베이스 및 hello StorSimple 장치에 저장 됩니다.

RBS hello Microsoft Azure StorSimple 구현은 hello를 이점은 다음을 제공 합니다.

* 서버에 의해 이동 BLOB 콘텐츠 tooa 별도 SQL Server 응답성을 향상 시킬 수 있는 SQL Server hello 쿼리 로드를 줄일 수 있습니다. 
* Azure StorSimple은 중복 제거와 압축 tooreduce 데이터 크기를 사용 합니다.
* Azure StorSimple hello 형태의 로컬 및 클라우드 스냅숏 데이터 보호를 제공합니다. 또한 hello StorSimple 장치에 hello 데이터베이스 자체를 배치 하는 경우 백업할 수 있습니다 hello 콘텐츠 데이터베이스와 Blob을 함께 크래시 일관성이 있는 방식으로. (Hello 콘텐츠 데이터베이스 이동 toohello 장치 에서만 hello StorSimple 8000 시리즈 장치에 대 한 지원 됩니다. 이 기능은 지원 되지 않습니다 hello 5000 또는 7000 시리즈에 대 한.)
* Azure StorSimple는 장애 조치, 파일 및 볼륨 복구(테스트 복구 포함)를 포함하는 재해 복구 기능과 신속한 데이터 복원을 포함합니다.
* SharePoint 콘텐츠 BLOB tooperform 항목 수준 복구를 데이터의 StorSimple 스냅숏과 함께 Kroll Ontrack PowerControls 등의 데이터 복구 소프트웨어를 사용할 수 있습니다. (이 데이터 복구 소프트웨어는 별도 구매입니다.)
* SharePoint 용 StorSimple 어댑터 hello 중앙 위치에서 사용 되 면 전체 SharePoint 솔루션 toomanage를 허용 되는 hello SharePoint 중앙 관리 포털에 연결 합니다.

BLOB 콘텐츠 toohello 파일 시스템 이동 하면 기타 비용 절감 효과 이점이 제공할 수 있습니다. 예를 들어 RBS를 사용 하 여 비용이 많이 드는 계층 1 저장소에 대 한 hello 필요성을 줄일 수 있습니다 및 hello 콘텐츠 데이터베이스를 축소 하기 때문에 RBS hello hello SharePoint 서버 팜에 필요한 데이터베이스 수를 줄일 수 있습니다. 그러나 데이터베이스 크기 제한 및 RBS 이외의 콘텐츠 양을 hello 등의 기타 요인을 저장소 요구 사항에 영향을 줄 수 있습니다. RBS를 사용 하 여 hello 비용 및 이점에 대 한 자세한 내용은 참조 [(SharePoint Foundation 2010) RBS 계획] [ 4] 및 [결정 하는 SharePoint 2013의 RBS toouse] [ 5].

### <a name="capacity-and-performance-limits"></a>용량 및 성능 제한
SharePoint 솔루션에 RBS 사용을 고려 하기 전에 테스트 하는 hello 성능과 용량 제한 SharePoint Server 2010 및 SharePoint Server 2013 및 이러한 제한을 tooacceptable 성능 간의 관계를 인식 해야 합니다. 자세한 내용은 [소프트웨어 경계 및 SharePoint 2013에 대한 한계](https://technet.microsoft.com/library/cc262787.aspx)를 참조하세요.

RBS를 구성 하기 전에 hello 다음을 검토 합니다.

* 해당 hello 총 크기 (콘텐츠 데이터베이스의 hello 크기)와 연결된 된 표면화 된 Blob의 hello 크기를 더한 SharePoint에서 지 원하는 hello RBS 크기 제한을 초과 하지 않는 콘텐츠 hello 있는지 확인 하십시오. 이 제한은 200GB입니다. 
  
    **toomeasure 콘텐츠 데이터베이스 및 BLOB 크기**
  
  1. Hello 중앙 관리 WFE에서이 쿼리를 실행 합니다. Hello SharePoint 관리 셸을 시작 하 고 hello 다음 Windows PowerShell 명령 tooget hello hello 콘텐츠 데이터베이스의 크기를 입력 하십시오.
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      이 단계는 hello 디스크에 hello 콘텐츠 데이터베이스의 hello 크기를 가져옵니다.
  2. Hello에 각 콘텐츠 데이터베이스에서 SQL server 상자 hello SQL Management Studio에서 SQL 쿼리를 다음 중 하나를 실행 하 고 1 단계에서 얻은 hello 결과 toohello 번호를 추가 합니다.
     
     SharePoint 2013 콘텐츠 데이터베이스에서 다음을 입력합니다.
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     SharePoint 2010 콘텐츠 데이터베이스에서 다음을 입력합니다.
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     이 단계는 hello 외부화 된 Blob의 hello 크기를 가져옵니다.
* 에 저장 하는 모든 BLOB 및 데이터베이스 콘텐츠 로컬로 hello StorSimple 장치는 것이 좋습니다. hello StorSimple 장치는 고가용성을 위해 2 개 노드 클러스터. Hello 콘텐츠 데이터베이스와 Blob hello StorSimple 장치에 배치 하면 고가용성을 제공 합니다.
  
    기존 SQL Server 마이그레이션 모범 사례 toomove hello 콘텐츠 데이터베이스 toohello StorSimple 장치를 사용 합니다. 모든 BLOB 콘텐츠 hello 데이터베이스에서 RBS 통해 이동된 toohello 파일 공유 된 후에 hello 데이터베이스를 이동 합니다. Toomove hello 콘텐츠 데이터베이스 toohello StorSimple 장치를 선택 하는 경우를 기본 볼륨으로 hello 장치에서 hello 콘텐츠 데이터베이스 저장소를 구성 하는 것이 좋습니다.
* Microsoft Azure StorSimple, 계층화 된 볼륨을 사용 하는 경우에 방법이 없습니다 tooguarantee 콘텐츠 hello StorSimple 장치에 로컬로 저장 하는 Azure 클라우드 저장소 계층화 된 tooMicrosoft 되지 않습니다. 따라서 SharePoint RBS와 함께 로컬로 고정된 StorSimple 볼륨을 사용하는 것이 좋습니다. 이렇게 하면 모든 BLOB 콘텐츠 hello StorSimple 장치에서 로컬로 유지 되 고 이동된 tooMicrosoft Azure 않습니다.
* Hello StorSimple 장치에 hello 콘텐츠 데이터베이스를 저장 하지 않는 경우 기존의 SQL Server 고가용성 모범 사례를 지 원하는 RBS를 사용 합니다. SQL Server 미러링이 지원하지 않는 반면 SQL Server 클러스터링은 RBS를 지원합니다. 

> [!WARNING]
> RBS를 설정 하지 않은 경우 hello 콘텐츠 데이터베이스 toohello StorSimple 장치를 이동 하지 않는 것이 좋습니다. 테스트되지 않은 구성입니다.

## <a name="storsimple-adapter-for-sharepoint-installation"></a>SharePoint 설치용 StorSimple 어댑터
SharePoint 용 StorSimple 어댑터 hello를 설치할 수 있습니다, 전에 hello StorSimple 장치를 구성 하 고 hello SharePoint 서버 팜 및 SQL Server 인스턴스화가 모든 필수 구성 요소를 충족 하는지 확인 해야 합니다. 이 자습서에는 설치 및 SharePoint 용 StorSimple 어댑터 hello를 업그레이드 하는 절차 뿐만 아니라 구성 요구 사항을 설명 합니다.

## <a name="configure-prerequisites"></a>필수 조건 구성
SharePoint 용 StorSimple 어댑터 hello를 설치할 수 있습니다, 전에 hello StorSimple 장치, SharePoint 서버 팜 및 SQL Server 인스턴스화가 다음 필수 구성 요소는 hello를 충족 하는지 확인 합니다.

### <a name="system-requirements"></a>시스템 요구 사항
SharePoint 용 StorSimple 어댑터 hello hello로 작동 하는 다음 하드웨어 및 소프트웨어:

* 지원되는 운영 체제 – Windows Server 2008 R2 SP1, Windows Server 2012 또는 Windows Server 2012 R2
* 지원되는 SharePoint 버전 – SharePoint Server 2010 또는 SharePoint Server 2013
* 지원되는 SQL Server 버전 – SQL Server 2008 Enterprise Edition, SQL Server 2008 R2 Enterprise Edition 또는 SQL Server 2012 Enterprise Edition
* 지원되는 StorSimple 장치 – StorSimple 8000 시리즈, StorSimple 7000 시리즈 또는 StorSimple 5000 시리즈입니다.

### <a name="storsimple-device-configuration-prerequisites"></a>StorSimple 장치 필수 구성 요소
hello StorSimple 장치에는 블록 장치 이며 따라서 hello 데이터를 호스팅할 수 있는 파일 서버가 필요 합니다. Hello SharePoint 팜에서 기존 서버 대신 별도 서버를 사용 하는 것이 좋습니다. 이 파일 서버 해야 수에 hello 동일한 로컬 영역 네트워크 (LAN) hello SQL 서버 컴퓨터와 hello 콘텐츠 데이터베이스를 호스트 하 합니다.

> [!TIP]
> * 고가용성을 위해 SharePoint 팜을 구성 하는 경우 또한 고가용성을 위해 hello 파일 서버를 배포 해야 합니다.
> * Hello StorSimple 장치에 hello 콘텐츠 데이터베이스를 저장 하지 않는 경우 RBS를 지 원하는 기존의 고가용성 모범 사례를 사용 합니다. SQL Server 미러링이 지원하지 않는 반면 SQL Server 클러스터링은 RBS를 지원합니다. 


StorSimple 장치를 올바르게 구성 되어 있고 해당 적절 한 볼륨 toosupport SharePoint 배포 구성 되어 있고 SQL Server 컴퓨터에서 액세스할 수 있는지 확인 합니다. 너무 이동[온-프레미스 StorSimple 장치 배포](storsimple-8000-deployment-walkthrough-u2.md) 아직 배포 및 StorSimple 장치를 구성 해야 하는 경우. Note hello StorSimple 장치의; hello IP 주소 SharePoint 용 StorSimple 어댑터 중 해야 합니다.

또한 BLOB 표면화에 사용 되는 해당 hello 볼륨 toobe hello 요구 사항을 준수를 충족 해야 합니다.

* hello 볼륨은 64KB 할당 단위 크기도 포맷 되어야 합니다.
* 웹 프런트 엔드 (WFE) 및 응용 프로그램 서버에는 범용 명명 규칙 (UNC) 경로 통해 수 tooaccess hello 볼륨 이어야 합니다.
* hello SharePoint 서버 팜 구성된 toowrite toohello 볼륨 이어야 합니다.

> [!NOTE]
> 모든 BLOB 표면화 hello StorSimple 장치를 통해 이동 해야 설치 하 고 hello 어댑터 구성 후 (hello 장치는 hello 볼륨 tooSQL 서버 시키며 hello 저장소 계층을 관리). BLOB 표면화에 다른 대상을 사용할 수 없습니다.


Hello BLOB의 toouse StorSimple 스냅숏 관리자 tootake 스냅숏을 계획 하 고 데이터베이스 데이터, SQL 기록기 서비스 tooimplement hello를 사용할 수 있도록 hello 데이터베이스 서버에 있는지 tooinstall StorSimple 스냅숏 관리자를 사용할 경우 hello Windows 볼륨 섀도 복사본 서비스 (VSS)입니다.

> [!IMPORTANT]
> StorSimple 스냅숏 관리자 hello SharePoint VSS 기록기를 지원 하지 않으며 SharePoint 데이터의 응용 프로그램 일치 스냅숏을 사용할 수 없습니다. SharePoint 시나리오에서 StorSimple Snapshot Manager는 크래시 일관성이 있는 백업만 제공합니다.


## <a name="sharepoint-farm-configuration-prerequisites"></a>SharePoint 팜 필수 구성 요소
SharePoint 서버 팜이 올바르게 구성되어있는지 다음과 같이 확인합니다.

* SharePoint server 팜이 정상 상태에서 인지 확인 하 고 hello 다음을 확인 합니다.
* 모든 SharePoint WFE와 응용 프로그램 서버 hello 팜에 등록 실행 하는 및 기반이 설치 hello StorSimple 어댑터 SharePoint에 대 한 hello 서버에서 ping을 실행할 수 있습니다.
* SharePoint Timer service (SPTimerV3 또는 SPTimerV4) hello 각 WFE 서버와 응용 프로그램 서버에서 실행 중입니다.
* SharePoint Timer service hello와 hello IIS 응용 프로그램 풀을 모두 hello SharePoint 중앙 관리 사이트가 실행 되는 관리 권한을 가집니다.
* Internet Explorer 보안 강화 컨텍스트(IE ESC)가 사용되지 않는지 확인합니다. 이러한 단계 toodisable IE ESC를 수행 합니다.
  
  1. Internet Explorer의 모든 인스턴스를 닫습니다.
  2. Hello 서버 관리자를 시작 합니다.
  3. Hello 왼쪽된 창에서 클릭 **로컬 서버**합니다.
  4. Hello에 오른쪽 창에서 다음 너무**IE 보안 강화 구성**, 클릭 **에**합니다.
  5. **관리자**에서 **끄기**를 클릭합니다.
  6. **확인**을 클릭합니다.

## <a name="remote-blob-storage-rbs-prerequisites"></a>RBS(Remote BLOB Storage) 필수 구성 요소
SQL Server 중 지원되는 버전을 사용하고 있는지 확인합니다. 만 hello 다음 버전은 지원 되 고 수 toouse RBS:

* SQL Server 2008 Enterprise 버전
* SQL Server 2008 R2 Enterprise 버전
* SQL Server 2012 Enterprise 버전

Blob은 tooSQL 서버를 표시 하는 StorSimple 장치 hello 해당 볼륨에만 표면화 될 수 있습니다. BLOB 표면화를 위해 다른 대상은 지원되지 않습니다.

모든 필수 구성 요소 구성 단계를 완료 하는 경우 너무 이동할[SharePoint 용 StorSimple 어댑터 설치 hello](#install-the-storsimple-adapter-for-sharepoint)합니다.

## <a name="install-hello-storsimple-adapter-for-sharepoint"></a>SharePoint 용 StorSimple 어댑터 hello 설치
SharePoint 용 StorSimple 어댑터 단계 tooinstall hello 다음 hello를 사용 합니다. Hello 소프트웨어를 다시 설치 하는 경우 참조 [업그레이드 하거나 SharePoint 용 StorSimple 어댑터 hello를 다시 설치](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint)합니다. hello 설치에 필요한 hello 시간 hello 전체 SharePoint 서버 팜의 SharePoint 데이터베이스 수에 따라 달라 집니다.

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a>RBS 구성
SharePoint 용 StorSimple 어댑터 hello를 설치한 후 hello 절차 다음에 설명 된 대로 RBS를 구성 합니다.

> [!TIP]
> SharePoint 용 StorSimple 어댑터 hello hello SharePoint 중앙 관리 페이지 RBS toobe hello SharePoint 팜의 각 콘텐츠 데이터베이스에서 활성화 또는 비활성화에 연결 합니다. 그러나, 활성화 또는 hello 콘텐츠 데이터베이스에서 RBS를 비활성화 하면 팜 구성에 따라 일시적으로 중단 될 수 있습니다 hello SharePoint 웹 프런트 엔드 (WFE)의 가용성을 hello는 IIS 재설정 합니다. (프런트 엔드 부하 분산 장치, hello 현재 서버 작업, 및 등의 hello 사용 등의 요소 수 제한 하거나 이러한 중단이 제거 합니다.) 장애 로부터 tooprotect 사용자가 사용 하도록 설정 하거나 계획 된 유지 관리 기간 동안에 RBS를 사용 하지 않도록 설정 하 좋습니다.


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a>가비지 수집 구성
개체를 SharePoint 사이트에서 삭제 한 경우은 삭제 되지 않습니다 자동으로 hello RBS 저장소 볼륨에서. 대신,는 비동기 백그라운드 유지 관리 프로그램 분리 된 Blob 저장소에서 삭제 hello 파일입니다. 시스템 관리자가이 프로세스 toorun를 주기적으로 예약할 수 있습니다 또는 필요할 때마다 해당를 시작할 수 있습니다.

RBS를 사용하도록 설정하면 이 유지 관리 프로그램(Microsoft.Data.SqlRemoteBlobs.Maintainer.exe)은 모든 SharePoint WFE 서버 및 응용 프로그램 서버에 자동으로 설치됩니다. hello 프로그램 hello 수정할 수 있는 위치에에서 설치 된: *드라이브 부팅*: files\microsoft SQL Remote Blob Storage 10.50\Maintainer\

구성 및 유지 관리 프로그램 hello를 사용 하는 방법에 대 한 정보를 참조 하십시오. [SharePoint Server 2013에서 RBS 유지 관리][8]합니다.

> [!IMPORTANT]
> hello RBS 유지 관리 프로그램은 리소스를 많이 사용 합니다. Hello SharePoint 팜에서 활동이 적은 기간 동안 toorun 것 예약 해야 합니다.


### <a name="delete-orphaned-blobs-immediately"></a>분리된 BLOB 즉시 삭제
Toodelete 분리 된 Blob를 즉시 필요 하면 지침에 따라 hello를 사용할 수 있습니다. 이러한 지침은 어떻게 이렇게 SharePoint 2013 환경에 다음과 같은 구성 요소가 hello로의 예가 note:

* hello 콘텐츠 데이터베이스 이름은 WSS_Content입니다.
* hello SQL Server 이름은 SHRPT13 SQL12\SHRPT13입니다.
* hello 웹 응용 프로그램 이름은 SharePoint-80입니다.

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-hello-storsimple-adapter-for-sharepoint"></a>업그레이드 하거나 SharePoint 용 StorSimple 어댑터 hello를 다시 설치
다음 프로시저 tooupgrade SharePoint 서버 hello를 사용 하 여 SharePoint 또는 toosimply 업그레이드에 대 한 StorSimple 어댑터를 다시 설치 또는 기존 SharePoint 서버 팜의 hello 어댑터를 다시 설치 합니다.

> [!IMPORTANT]
> Hello tooupgrade를 시도 하기 전에 다음 정보를 검토 하 여 SharePoint 소프트웨어 및/또는 업그레이드 하거나 SharePoint 용 StorSimple 어댑터 hello를 다시 설치 합니다.
> 
> * 모든 이전에 RBS 통해 tooexternal 저장소 제공 됩니다 hello 다시 설치를 완료 될 때까지 옮겨진 파일 및 hello RBS 기능 다시 활성화 됩니다. toolimit 사용자에 영향을 줄, 업그레이드 또는 계획 된 유지 관리 기간 동안 다시 설치를 수행 합니다.
> * hello 업그레이드/다시 설치에 필요한 hello 시간 hello 총 hello SharePoint 서버 팜의 SharePoint 데이터베이스 수에 따라 달라질 수 있습니다.
> * Hello 업그레이드/다시 설치가 완료 되 면 hello 콘텐츠 데이터베이스 tooenable RBS 필요 합니다. 자세한 내용은 [RBS 구성](#configure-rbs)을 참조하세요.
> * 매우 많은 (200 보다 큼) 데이터베이스에 있는 SharePoint 팜에 대해 RBS를 구성 하는 경우 hello **SharePoint 중앙 관리** 페이지 시간이 초과 될 수 있습니다. 이 경우 hello 페이지를 새로 고칩니다. Hello 구성 프로세스에는 영향을 주지 않습니다.


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a>SharePoint용 StorSimple 어댑터 제거
다음 절차를 수행 하는 hello toomove hello Blob toohello SQL Server 콘텐츠 데이터베이스를 백업 하 고 제거 하 여 SharePoint 용 StorSimple 어댑터를 hello 하는 방법을 설명 합니다. 

> [!IMPORTANT]
> Hello 어댑터 소프트웨어를 제거 하기 전에 toomove hello Blob 백 toohello 콘텐츠 데이터베이스 해야 합니다.


### <a name="before-you-begin"></a>시작하기 전에
Hello toohello SQL Server 콘텐츠 데이터베이스를 백업 하 고 hello 어댑터 제거 프로세스를 시작 하는 hello 데이터를 이동 하기 전에 다음 정보를 수집 합니다.

* RBS를 사용할 수 있는 모든 hello 데이터베이스의 hello 이름
* hello의 hello UNC 경로는 BLOB 저장소 구성

### <a name="move-hello-blobs-back-toohello-content-databases"></a>Hello Blob 백 toohello 콘텐츠 데이터베이스 이동
SharePoint 소프트웨어에 대 한 hello StorSimple 어댑터를 제거 하기 전에 모든 Blob 표면화 백 toohello SQL Server 콘텐츠 데이터베이스로 되었던 hello 마이그레이션할 해야 있습니다. 모든 hello Blob 백 toohello 콘텐츠 데이터베이스를 이동 하기 전에 SharePoint 용 StorSimple 어댑터 toouninstall hello 시도 하면 hello 경고 메시지의 뒤에 표시 됩니다.

![경고 메시지](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="toomove-hello-blobs-back-toohello-content-databases"></a>toomove hello Blob 백 toohello 콘텐츠 데이터베이스
1. 각 표면화 hello 개체를 다운로드 합니다.
2. 열기 hello **SharePoint 중앙 관리** 너무 찾아서 페이지**시스템 설정**합니다.
3. **Azure StorSimple**에서 **StorSimple 어댑터 구성**을 클릭합니다.
4. Hello에 **StorSimple 어댑터 구성** 페이지에서 hello **사용 하지 않도록 설정** 각 hello tooremove 외부 BLOB 저장소에서 지정 하는 콘텐츠 데이터베이스 아래 단추입니다. 
5. SharePoint에서 hello 개체를 삭제 하 고 다시 업로드 합니다.

또는 Microsoft hello를 사용할 수 있습니다` RBS Migrate()` SharePoint에 포함 된 PowerShell cmdlet. 자세한 내용은 [RBS에서 콘텐츠 마이그레이션](https://technet.microsoft.com/library/ff628255.aspx)을 참조하세요.

Hello Blob 백 toohello 콘텐츠 데이터베이스를 이동한 후 이동 toohello 다음 단계: [제거 hello 어댑터](#uninstall-the-adapter)합니다.

### <a name="uninstall-hello-adapter"></a>Hello 어댑터 제거
Hello Blob 백 toohello SQL Server 콘텐츠 데이터베이스를 이동한 후 hello SharePoint 용 StorSimple 어댑터 옵션 toouninstall hello를 다음 중 하나를 사용 합니다.

#### <a name="toouse-hello-installation-program-toouninstall-hello-adapter"></a>toouse hello 설치 프로그램 toouninstall hello 어댑터
1. 계정을 관리자 권한 toolog toohello 웹 프런트 엔드 서버의 (WFE) 사용 합니다.
2. SharePoint 설치 관리자에 대 한 hello StorSimple 어댑터를 두 번 클릭 합니다. hello 설치 마법사를 시작합니다.
   
    ![설치 마법사](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. **다음**을 누릅니다. 다음 페이지 hello가 나타납니다.
   
    ![설치 마법사 제거 페이지](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. 클릭 **제거** tooselect hello 제거 프로세스입니다. 다음 페이지 hello가 나타납니다.
   
    ![설치 마법사 확인 페이지](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. 클릭 **제거** tooconfirm hello 제거 합니다. hello 다음 진행률 페이지가 나타납니다.
   
    ![설치 마법사 진행률 페이지](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. Hello 제거가 완료 되 면 hello 마침 페이지가 표시 됩니다. 클릭 **마침** tooclose hello 설정 마법사입니다.

#### <a name="toouse-hello-control-panel-toouninstall-hello-adapter"></a>toouse hello 제어판 toouninstall hello 어댑터
1. Hello 제어판을 열고 클릭 **프로그램 및 기능**합니다.
2. **SharePoint용 StorSimple 어댑터**를 선택하고 **제거**를 클릭합니다.

## <a name="next-steps"></a>다음 단계
[StorSimple에 대해 자세히 알아봅니다](storsimple-overview.md).

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx
