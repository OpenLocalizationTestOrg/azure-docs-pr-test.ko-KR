---
title: "aaaWhat은 StorSimple 스냅숏 관리자 인지 확인 | Microsoft Docs"
description: "StorSimple 스냅숏 관리자 hello의 아키텍처 및 해당 기능에 설명합니다."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6094c31e-e2d9-4592-8a15-76bdcf60a754
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: v-sharos
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79ce7b7e1970ac862038af2a0e67065b6fb6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toostorsimple-snapshot-manager"></a>소개 tooStorSimple 스냅숏 관리자

## <a name="overview"></a>개요
StorSimple 스냅숏 관리자는 Microsoft Azure StorSimple 환경에서 데이터 보호 및 백업 관리를 간소화하는 Microsoft Management Console(MMC) 스냅인입니다. StorSimple 스냅숏 관리자를 관리할 수 있습니다 hello 클라우드 및 hello 데이터 센터에서 데이터를 Microsoft Azure StorSimple 단일 통합된 저장소 솔루션으로 따라서 있어 백업 프로세스가 단순화 되 고 비용이 절감 합니다.

이 개요 hello StorSimple 스냅숏 관리자를 소개 하 고 해당 기능을 설명 및 Microsoft Azure StorSimple에서 해당 역할에 설명 합니다. 

Hello 전체 Microsoft Azure StorSimple 시스템에서 SharePoint 용 StorSimple 장치 hello, StorSimple Manager 서비스, StorSimple 스냅숏 관리자 및 StorSimple 어댑터 등의 개요를 참조 하십시오. [StorSimple 8000 시리즈: 하이브리드 클라우드 저장소 솔루션](storsimple-overview.md)합니다. 

> [!NOTE]
> * StorSimple 스냅숏 관리자 toomanage Microsoft Azure StorSimple 가상 배열 (라고도 StorSimple 온-프레미스 가상 장치)를 사용할 수 없습니다.
> * StorSimple 장치에서 tooinstall StorSimple 업데이트 2를 계획할 수 있는지 toodownload hello 최신 버전의 StorSimple 스냅숏 관리자를 설치 **StorSimple 업데이트 2를 설치 하기 전에**합니다. hello 최신 버전의 StorSimple 스냅숏 관리자가 이전 버전과 호환 하며 모든 릴리스된 버전의 Microsoft Azure StorSimple과 작동 합니다. Tooupdate 할 hello 이전 버전의 StorSimple 스냅숏 관리자를 사용 하는 경우 it (않아도 toouninstall hello 이전 버전 hello 새 버전을 설치 하기 전에).
> 
> 

## <a name="storsimple-snapshot-manager-purpose-and-architecture"></a>StorSimple 스냅숏 관리자 용도 및 아키텍처
StorSimple 스냅숏 관리자 제공 toocreate 일치를 사용할 수 있는 중앙 관리 콘솔, 로컬의 지정 시간 백업 복사본 및 클라우드 데이터입니다. 예를 들어 hello 콘솔을 사용할 수 있습니다.

* 볼륨을 구성, 백업 및 삭제합니다.
* 볼륨 구성 데이터를 백업 하는 그룹 tooensure는 응용 프로그램 일치 합니다.
* 미리 정해진 일정에 따라 데이터가 백업되도록 백업 정책을 관리합니다.
* 로컬 만들고 클라우드 스냅숏 hello 클라우드에 저장 하 고 재해 복구에 사용할 수 있습니다.

StorSimple 스냅숏 관리자 hello 인출 hello hello 호스트에 hello VSS 공급자에 등록 하는 응용 프로그램 목록은 제공 합니다. 응용 프로그램에서 사용 하 고 볼륨 그룹 tooconfigure 제안 하는 hello 볼륨 그런 다음 toocreate 응용 프로그램 일치 백업을 확인 합니다. StorSimple 스냅숏 관리자는 이러한 볼륨 그룹 toogenerate 된 백업 복사본을 응용 프로그램 일치를 사용 합니다. (응용 프로그램 일관성은 모든 관련 파일 및 데이터베이스가 동기화 되 고 hello 시간에 특정 한 시점에 hello 응용 프로그램의 실제 상태를 나타내는 경우 존재 합니다.) 

StorSimple 스냅숏 관리자 백업을 hello 마지막 백업 이후의 hello 변경 내용만 캡처하는 증분 스냅숏의 hello 큐인지. 결과적으로, 백업 저장소가 덜 필요 하고 신속하게 생성 및 복원할 수 있습니다. StorSimple 스냅숏 관리자 hello Windows 볼륨 섀도 복사본 서비스 (VSS) tooensure 스냅숏을 응용 프로그램에 일관 된 데이터 캡처를 사용 합니다. (자세한 내용은 toohello 통합 Windows 볼륨 섀도 복사본 서비스 섹션으로 이동). StorSimple 스냅숏 관리자를 사용하여 백업 일정을 만들거나 필요에 따라 즉시 백업을 수행할 수 있습니다. Toorestore 데이터 백업, StorSimple 스냅숏 관리자 수를 유지 해야 하는 경우 로컬의 카탈로그 또는 클라우드 스냅숏에서 선택 합니다. Azure StorSimple 복원만 hello 데이터는 필요할 때에 필요한 복원 작업 동안 데이터 가용성의 지연을 방지 합니다.)

![StorSimple 스냅숏 관리자 아키텍처](./media/storsimple-what-is-snapshot-manager/HCS_SSM_Overview.png)

**StorSimple 스냅숏 관리자 아키텍처** 

## <a name="support-for-multiple-volume-types"></a>여러 볼륨 유형에 대한 지원
StorSimple 스냅숏 관리자 tooconfigure hello를 사용 하 여 및 hello 다음 유형의 볼륨을 백업할 수 있습니다. 

* **기본 볼륨** – 기본 볼륨은 기본 디스크의 단일 파티션입니다. 
* **단순 볼륨** – 단순 볼륨은 단일 동적 디스크의 디스크 공간을 포함하는 동적 볼륨입니다. 단순 볼륨 디스크의 단일 영역 구성 되거나 여러 영역에 함께 연결 되어 있는 hello 같은 디스크. 단순 볼륨은 동적 디스크에서만 만들 수 있습니다. 단순 볼륨은 내결함성이 없습니다.
* **동적 볼륨** – 동적 볼륨은 동적 디스크에서 만든 볼륨입니다. 동적 디스크는 컴퓨터의 동적 디스크에 포함 된 볼륨에 대 한 데이터베이스 tootrack 정보를 사용 합니다. 
* **동적 볼륨 미러링을** – 동적 볼륨 미러링을 hello RAID 1 아키텍처에 구축 됩니다. RAID 1에서는 동일한 데이터가 둘 이상의 디스크에 기록되어 미러링 세트를 이룹니다. 읽기 요청 hello를 포함 하는 모든 디스크에 의해 처리 될 수 데이터를 요청 합니다.
* **클러스터 공유 볼륨** -클러스터 공유 볼륨 (Csv)의 경우와 장애 조치 클러스터의 여러 노드에서 동시에 읽거나 쓸 수 toohello 같은 디스크. 한 노드에서 tooanother 노드 간에서 장애 조치 드라이브 소유권 또는 탑재, 분리 및 제거 된 볼륨에서 변경 하지 않고도 신속 하 게 발생할 수 있습니다. 

> [!IMPORTANT]
> Csv와 Csv 이외의 hello 혼합 하지 않는 같은 스냅숏에 합니다. 한 스냅숏에서의 CSV와 비 CSV 혼용은 지원되지 않습니다. 
> 
> 

StorSimple 스냅숏 관리자 toorestore 전체 볼륨 그룹을 사용 하거나 개별 볼륨을 복제 하 고 개별 파일을 복구할 수 있습니다.

* [볼륨 및 볼륨 그룹](#volumes-and-volume-groups) 
* [백업 유형 및 백업 정책](#backup-types-and-backup-policies) 

StorSimple 스냅숏 관리자 기능에 대 한 자세한 내용은 toouse, 참조 및 [StorSimple 스냅숏 관리자 사용자 인터페이스](storsimple-use-snapshot-manager.md)합니다.

## <a name="volumes-and-volume-groups"></a>볼륨 및 볼륨 그룹
StorSimple 스냅숏 관리자를 사용하여 볼륨을 만든 다음 볼륨 그룹에 구성합니다. 

StorSimple 스냅숏 관리자 볼륨 그룹 toocreate 된 백업 복사본을 응용 프로그램 일치를 사용 합니다. 응용 프로그램 일관성은 모든 관련 파일 및 데이터베이스가 동기화 되 고 hello 시간에 특정 한 시점에 응용 프로그램의 실제 상태를 나타내는 경우 존재 합니다. 볼륨 그룹 (라 하 고 있는 *일관성 그룹*)의 백업 hello 기반을 형성 또는 복원 작업입니다.

볼륨 그룹은 볼륨 컨테이너와 같은 hello 되지 않습니다. 볼륨 컨테이너는 클라우드 저장소 계정과, 암호화 및 대역폭 소비 등과 같은 기타 특성을 공유합니다. 단일 볼륨 컨테이너는 씬 프로 비전 too256 StorSimple 볼륨을 포함할 수 있습니다. 볼륨 컨테이너에 대 한 자세한 내용은 이동 너무[볼륨 컨테이너 관리](storsimple-manage-volume-containers.md)합니다. 볼륨 그룹은 toofacilitate 백업 작업을 구성 하는 볼륨의 컬렉션입니다. Toodifferent 볼륨 컨테이너는 단일 볼륨 그룹에 배치 속하고 한 다음 해당 볼륨 그룹에 대 한 백업 정책을 만들 수 있는 두 개의 볼륨을 선택 하면 각 볼륨 백업 됩니다 hello 적합 한 볼륨 컨테이너에서 hello 적절 한 저장소를 사용 하 여 계정입니다.

> [!NOTE]
> 볼륨 그룹의 모든 볼륨은 단일 클라우드 서비스 공급자에서 가져와야 합니다.
> 
> 

## <a name="integration-with-windows-volume-shadow-copy-service"></a>Windows 볼륨 섀도 복사본 서비스와의 통합
StorSimple 스냅숏 관리자 hello Windows 볼륨 섀도 복사본 서비스 (VSS) toocapture 응용 프로그램에 일관 된 데이터를 사용합니다. VSS는 VSS 인식 응용 프로그램 toocoordinate hello 증분 스냅숏 만들기와 통신 하 여 응용 프로그램 일관성을 지원 합니다. VSS는 hello 응용 프로그램을 일시적으로 비활성 또는 정지는 스냅숏이 만들어질 때 되도록 합니다. 

SQL Server 및 제네릭 NTFS 볼륨과 VSS의 hello StorSimple 스냅숏 관리자 구현은 작동 합니다. hello 프로세스는 다음과 같습니다. 

1. 이면 일반적으로 데이터 관리 및 보호 솔루션 (예: StorSimple 스냅숏 관리자) 또는 백업 응용 프로그램 요청자는 VSS를 호출 하 고 toogather 정보 hello 대상 응용 프로그램에서 기록기 소프트웨어 hello에서 묻습니다.
2. VSS 연락처 hello 기록기 구성 요소 tooretrieve hello 데이터에 설명 합니다. hello 기록기 hello hello 데이터 toobe 백업에 대 한 설명을 제공 합니다. 
3. VSS는 hello 기록기 tooprepare hello 응용 프로그램 백업에 대 한 신호를 보냅니다. hello 기록기 트랜잭션 로그 및 등의 업데이트 열려 있는 트랜잭션을 완료 하 여 hello 데이터 백업에 대 한를 준비 하 고 VSS에 알립니다.
4. VSS는 tootemporarily 중지 hello 응용 프로그램 데이터를 저장 하 고 hello 섀도 복사본을 만드는 동안 데이터가 없는 toohello 볼륨에 기록 되어 있는지 확인 hello 기록기에 지시 합니다. 이 단계로 데이터 일관성을 유지하며 60초 이하가 걸립니다.
5. VSS는 hello 공급자 toocreate hello 섀도 복사본에 지시합니다. 소프트웨어 또는 하드웨어 기반, 될 수 있는 공급자는 필요에 따라 섀도 복사본을 만들고 현재 실행 중인 hello 볼륨을 관리 합니다. hello 공급자 hello 섀도 복사본을 만들고 완료 되 면 VSS에 알립니다.
6. VSS 연락처 hello 기록기 toonotify hello 응용 프로그램 I/O를 다시 시작할 수 있는 및 tooconfirm 섀도 하는 동안 I/O가 성공적으로 일시 중지 하는 생성을 복사 합니다. 
7. Hello 복사가 성공적 이면 VSS hello 복사본의 위치 toohello 요청자에 게 반환 합니다. 
8. Hello 섀도 복사본을 만드는 동안 데이터 작성 된 경우 다음 hello 백업은 일치 하지 않을 수 있습니다. VSS는 hello 섀도 복사본을 삭제 하 고 hello 요청자에 게 알립니다. hello 요청자 hello 백업 프로세스를 자동으로 반복 하거나 알릴 안녕 관리자 tooretry 나중에 해당 합니다.

다음 그림 hello를 참조 하십시오.

![VSS 프로세스](./media/storsimple-what-is-snapshot-manager/HCS_SSM_VSS_process.png)

**Windows 볼륨 섀도 복사본 서비스 프로세스** 

## <a name="backup-types-and-backup-policies"></a>백업 유형 및 백업 정책
StorSimple 스냅숏 관리자와 데이터를 백업 및 로컬과 hello 클라우드에 저장할 수 있습니다. StorSimple 스냅숏 관리자 tooback 데이터를 즉시 사용할 수 있습니다 또는 자동으로 백업을 수행 하는 것에 대 한 백업 정책 toocreate 일정을 사용할 수 있습니다. 백업 정책을 유지 되는 스냅숏 toospecify를 사용 합니다. 

### <a name="backup-types"></a>백업 유형
StorSimple 스냅숏 관리자 toocreate hello 백업 유형만 사용할 수 있습니다.

* **로컬 스냅숏** – 로컬 스냅숏은 hello StorSimple 장치에 저장 된 볼륨 데이터의 지정 시간 복사본입니다. 일반적으로 이러한 유형의 백업은 신속하게 만들고 복원할 수 있습니다. 로컬 스냅숏은 로컬 백업 사본처럼 사용할 수 있습니다.
* **클라우드 스냅숏** – 클라우드 스냅숏은 hello 클라우드에 저장 된 볼륨 데이터의 지정 시간 복사본입니다. 클라우드 스냅숏은 같습니다 tooa 스냅숏 다른 오프 사이트 저장소 시스템에 복제 합니다. 클라우드 스냅숏은 특히 재해 복구 상황에서 유용합니다.

### <a name="on-demand-and-scheduled-backups"></a>주문 및 예약 백업
StorSimple 스냅숏 관리자와 즉시 만들 일회성 백업 toobe를 시작할 수 있습니다 또는 백업 작업을 되풀이 백업 정책 tooschedule를 사용할 수 있습니다.

백업 정책은 tooschedule 정기 백업 미 실시를 사용할 수 있는 자동화 된 규칙의 집합입니다. 백업 정책이 있습니다 toodefine hello 빈도 및 매개 변수는 특정 볼륨 그룹의 스냅숏을 만들기 위한. 로컬에 대 한 정책 toospecify 시작 및 만료 날짜, 시간, 빈도 및 보존 요구를 사용할 수 있습니다 및 클라우드 스냅숏 합니다. 정책은 정의한 직후에 적용됩니다. 

StorSimple 스냅숏 관리자 tooconfigure를 사용 하거나 필요할 때마다 백업 정책을 다시 구성할 수 있습니다. 

만드는 각 백업 정책에 대 한 정보를 다음 hello를 구성할 수 있습니다.

* **이름** – hello의 고유 이름을 hello 백업 정책을 선택 합니다.
* **형식** – 유형의 백업 정책, 로컬 스냅숏 또는 클라우드 스냅숏 hello 합니다.
* **볼륨 그룹** – hello 볼륨 그룹 toowhich hello 선택한 백업 정책이 할당 됩니다.
* **보존** – hello tooretain 백업 복사본의 수입니다. Hello를 확인 하는 경우 **모든** 상자에서 모든 백업 복사본이 hello 최대 볼륨당 백업 복사본 수에 도달할 때까지 유지 됩니다, 어떤 지점 hello에 정책은 실패 하 고 오류 메시지를 생성 합니다. 또는 백업 tooretain (1부터 64)의 수를 지정할 수 있습니다.
* **날짜** – hello 백업 정책을 생성 하는 hello 날짜입니다.

백업 정책 구성에 대 한 내용은 이동 너무[StorSimple 스냅숏 관리자를 사용 하 여 toocreate 백업 정책 관리 및](storsimple-snapshot-manager-manage-backup-policies.md)합니다.

### <a name="backup-job-monitoring-and-management"></a>백업 작업 모니터링 및 관리
StorSimple 스냅숏 관리자 toomonitor hello를 사용 하 고 예정 된, 예약 및 완료 된 백업 작업을 관리할 수 있습니다. 또한 StorSimple 스냅숏 관리자 완료 too64 백업 카탈로그를 제공합니다. Hello 카탈로그 toofind 사용 및 볼륨 또는 개별 파일을 복원할 수 있습니다. 

백업 작업을 모니터링 하는 방법에 대 한 내용은 이동 너무[tooview StorSimple 스냅숏 관리자를 사용 하 여 백업 작업을 관리 하 고](storsimple-snapshot-manager-manage-backup-jobs.md)합니다.

## <a name="next-steps"></a>다음 단계
* 에 대 한 자세한 내용은 [StorSimple 솔루션 tooadminister StorSimple 스냅숏 관리자를 사용 하 여](storsimple-snapshot-manager-admin.md)합니다.
* [StorSimple 스냅숏 관리자 다운로드](https://www.microsoft.com/download/details.aspx?id=44220)

