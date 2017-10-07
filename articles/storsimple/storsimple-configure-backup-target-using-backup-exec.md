---
title: "백업 대상으로 백업 실행 aaaStorSimple 8000 시리즈 | Microsoft Docs"
description: "Veritas 백업 실행 된 hello StorSimple 백업 대상 구성에 설명 합니다."
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/05/2016
ms.author: hkanna
ms.openlocfilehash: 270ad95e1f6b367e80048cad42beb936f205f69c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-backup-exec"></a>Backup Exec에서 백업 대상으로 StorSimple 구성

## <a name="overview"></a>개요

Azure StorSimple은 Microsoft의 하이브리드 클라우드 저장소 솔루션입니다. StorSimple 온-프레미스 저장소와 클라우드 저장소에서 Azure 저장소 계정을 hello 온-프레미스 솔루션 및 데이터를 자동으로 계층화의 확장으로 사용 하 여 지 수 데이터 증가 hello 복잡성을 해결 합니다.

이 문서에서는 Veritas Backup Exec과 StorSimple의 통합 및 두 솔루션을 통합하는 모범 사례에 대해 설명합니다. 또한 백업 Exec toobest tooset StorSimple을 통합 하는 방법을 대 한 권장 사항은으로 만듭니다. 우리는 tooVeritas에 대 한 유용한 정보, 백업 설계자 및 백업 실행 toomeet 개별 백업 요구 사항 및 서비스 수준 계약 (Sla)를 가장 좋은 방법은 tooset hello에 대 한 관리자를 지연합니다.

이 문서는 구성 단계와 주요 개념을 설명하지만 단계별 구성 또는 설치 가이드가 아닙니다. 가정 hello 기본 구성 요소 및 인프라 지 작업 순서 및 준비 toosupport hello 개념을 설명 합니다.

### <a name="who-should-read-this"></a>이 문서의 대상

이 문서의 정보 hello 가장 유용한 toobackup 관리자, 저장소 관리자 및 Windows Server 2012 R2, 이더넷, 클라우드 서비스 및 백업 Exec 저장소의 지식이 있는 저장소 설계자 됩니다.

## <a name="supported-versions"></a>지원되는 버전

-   [Backup Exec 16 이상 버전](http://backupexec.com/compatibility)
-   [StorSimple 업데이트 3 이상 버전](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a>StorSimple이 백업 대상인 이유는 무엇인가요?

StorSimple이 백업 대상으로 적합한 이유는 다음과 같습니다.

-   Toouse 백업 응용 프로그램에 대 한 표준, 로컬 저장소는 별다른 변경 없이 빠른 백업 대상으로 제공합니다. StorSimple을 사용하여 최근 백업을 빠르게 복원할 수도 있습니다.
-   해당 클라우드는 Azure 클라우드 저장소 계정 toouse와 원활 하 게 통합 되어 계층화 비용 효율적인 Azure 저장소입니다.
-   재해 복구를 위해 오프사이트 저장소를 자동으로 제공합니다.

## <a name="key-concepts"></a>주요 개념

모든 저장소 솔루션을 Sla, hello 솔루션의 저장소 성능의 신중 하 게 평가와 마찬가지로, 변경 및 용량 증가 요구의 속도가 중요 한 toosuccess입니다. hello 주 아이디어는 클라우드 계층을 도입 하 여 액세스 시간 및 처리량 toohello 클라우드에에서 역할을 기본 StorSimple toodo의 hello 기능 하는 일입니다.

StorSimple는 데이터 (핫 데이터)의 잘 정의 된 작업 집합에서 작동 하는 디자인 된 tooprovide 저장소 tooapplications입니다. 이 모델에서는 데이터의 작업 집합 hello hello 로컬 계층에 저장 된 이며 hello 나머지 휴무일/콜드/보관 데이터 집합을 계층화 된 toohello 클라우드입니다. 이 모델은 hello 다음 그림에에서 표시 됩니다. hello 평평한 거의 녹색 선은 hello hello StorSimple 장치의 로컬 계층에 저장 된 hello 데이터를 나타냅니다. hello 빨강 선 나타내는 모든 계층에서 hello StorSimple 솔루션에 저장 된 데이터의 총 hello 합니다. hello 평평한 녹색 선과 hello 지 수 빨간색 곡선 hello 공간 hello 총 hello 클라우드에 저장 된 데이터의 양을 나타냅니다.

**StorSimple 계층화**
![StorSimple 계층화 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)

StorSimple 백업 대상으로 적합된 toooperate 임을 염두에서 이러한 구조를 찾을 수 있습니다. StorSimple을 사용하면 다음 작업을 수행할 수 있습니다.
-   데이터의 hello 로컬 작업 집합에서 가장 자주 발생 하면 복원을 수행 합니다.
-   복원 사항이 자주 오프 사이트 재해 복구 및 오래 된 데이터에 대 한 hello 클라우드를 사용 합니다.

## <a name="storsimple-benefits"></a>StorSimple 이점

StorSimple 원활 하 게 통합 되어 있는 Microsoft Azure는 온-프레미스 솔루션을 제공 하 고 원활 하 게 활용 하기 위해 여 tooon 온-프레미스 액세스 클라우드 저장소입니다.

StorSimple 자동 반도체 장치 (SSD) 및 serial attached SCSI (SAS) 저장소에는 온-프레미스 장치를 hello와 Azure 저장소 계층화를 사용 합니다. 자주 액세스 한 데이터 hello SAS 및 SSD 계층에 로컬 자동 계층화 유지 합니다. 자주 액세스 되지 않는 데이터 tooAzure 저장소를 이동합니다.

StorSimple은 다음과 같은 이점을 제공합니다.

-   Hello 클라우드 tooachieve 최고의 사용 하는 고유 중복 제거와 압축 알고리즘 수준 중복 제거
-   고가용성
-   Azure 지역에서 복제를 사용하여 지역에서 복제
-   Azure 통합
-   Hello 클라우드에 데이터 암호화
-   향상된 재해 복구 및 규정 준수

StorSimple은 기본 백업 대상과 보조 백업 대상이라는 두 가지 주요 배포 시나리오를 제공하지만 기본적으로는 일반 블록 저장소 장치입니다. StorSimple가 모든 hello 압축 및 중복 제거 합니다. 원활 하 게 전송 하 고 hello 클라우드 및 hello 응용 프로그램 및 파일 시스템 간에 데이터를 검색 합니다.

StorSimple에 대한 자세한 내용은 [StorSimple 8000 시리즈: 하이브리드 클라우드 저장소 솔루션](storsimple-overview.md)을 참조하세요. 또한 hello를 검토할 수 있습니다 [기술 StorSimple 8000 시리즈 사양](storsimple-technical-specifications-and-compliance.md)합니다.

> [!IMPORTANT]
> StorSimple 장치를 백업 대상으로 사용하는 것은 StorSimple 8000 업데이트 3 이상 버전에서만 지원됩니다.

## <a name="architecture-overview"></a>아키텍처 개요

hello 다음 표에서 보여 hello 장치 모델 아키텍처에 대 한 초기 지침.

**로컬 및 클라우드 저장소의 StorSimple 용량**

| 저장소 용량       | 8100          | 8600            |
|------------------------|---------------|-----------------|
| 로컬 저장소 용량 | &lt; 10TiB\*  | &lt; 20TiB\*  |
| 클라우드 저장소 용량 | &gt; 200TiB\* | &gt; 500TiB\* |
\*저장소 크기는 중복 제거 또는 압축을 사용한다고 가정하지 않습니다.

**기본 및 보조 백업의 StorSimple 용량**

| 백업 시나리오  | 로컬 저장소 용량  | 클라우드 저장소 용량  |
|---|---|---|
| 기본 백업  | 빠른 복구 toomeet 복구 지점 목표 (RPO)에 대 한 로컬 저장소에 저장 된 최근의 백업 | 클라우드 용량에 적합한 백업 기록(RPO) |
| 보조 백업 | 클라우드 용량에 백업 데이터의 보조 복사본을 저장할 수 있습니다.  | 해당 없음  |

## <a name="storsimple-as-a-primary-backup-target"></a>기본 백업 대상인 StorSimple

이 시나리오에서는 StorSimple 볼륨 toohello 백업 응용 프로그램에서 백업에 대 한 유일한 리포지토리입니다 hello로 표시 됩니다. hello 다음 그림에서는 백업 및 복원에 대 한 볼륨을 계층화 된 모든 백업을 사용 하 여 StorSimple 있는 솔루션 아키텍처를 보여 줍니다.

![기본 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>기본 대상 백업 논리 단계

1.  hello 백업 서버 연락처 hello 대상 백업 에이전트 및 hello 백업 에이전트 toohello 백업 서버 데이터를 전송 합니다.
2.  서버를 백업 하는 hello 데이터를 쓰는 toohello StorSimple 볼륨 계층입니다.
3.  서버를 백업 하는 hello hello 카탈로그 데이터베이스를 업데이트 한 다음 hello 백업 작업을 완료 합니다.
4.  스냅숏 스크립트 hello StorSimple 클라우드 스냅숏 관리자를 (시작 또는 삭제)를 트리거합니다.
5.  서버 hello 백업 보존 정책에 따라 만료 된 백업을 삭제 합니다.


### <a name="primary-target-restore-logical-steps"></a>기본 대상 복원 논리 단계

1.  서버를 백업 하는 hello 시작 hello 저장소 리포지토리에서 hello 적절 한 데이터를 복원 합니다.
2.  hello 백업 에이전트에서 서버를 백업 하는 hello hello 데이터를 받습니다.
3.  서버를 백업 하는 hello hello 복원 작업을 완료합니다.

## <a name="storsimple-as-a-secondary-backup-target"></a>보조 백업 대상인 StorSimple

이 시나리오에서 StorSimple 볼륨은 주로 장기 보존 또는 보관에 사용됩니다.

hello 다음 그림 초기 백업을의 아키텍처를 보여 줍니다.와 성능 우선 대상 볼륨을 복원 합니다. 이러한 백업을 복사 하 고 보관 된 tooa StorSimple 볼륨 집합 일정에 따라 계층입니다.

이 보존 정책 용량 및 성능 요구를 처리할 수 있도록 중요 한 toosize 고성능 볼륨은 합니다.

![보조 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>보조 대상 백업 논리 단계

1.  hello 백업 서버 연락처 hello 대상 백업 에이전트 및 hello 백업 에이전트 toohello 백업 서버 데이터를 전송 합니다.
2.  서버를 백업 하는 hello toohigh 고성능 저장소 데이터를 씁니다.
3.  서버를 백업 하는 hello hello 카탈로그 데이터베이스를 업데이트 한 다음 hello 백업 작업을 완료 합니다.
4.  hello 백업 서버 백업을 tooStorSimple 보존 정책에 따라 복사 합니다.
5.  스냅숏 스크립트 hello StorSimple 클라우드 스냅숏 관리자를 (시작 또는 삭제)를 트리거합니다.
6.  서버 hello 백업 보존 정책에 따라 만료 된 백업을 삭제 합니다.

### <a name="secondary-target-restore-logical-steps"></a>보조 대상 복원 논리 단계

1.  서버를 백업 하는 hello 시작 hello 저장소 리포지토리에서 hello 적절 한 데이터를 복원 합니다.
2.  hello 백업 에이전트에서 서버를 백업 하는 hello hello 데이터를 받습니다.
3.  서버를 백업 하는 hello hello 복원 작업을 완료합니다.

## <a name="deploy-hello-solution"></a>Hello 솔루션 배포

Hello 솔루션 배포 세 단계가 필요 합니다.
1. Hello 네트워크 인프라를 준비 합니다.
2. 백업 대상으로 StorSimple 장치를 배포합니다.
3. Backup Exec을 배포합니다.

각 단계는 hello 다음 섹션에서에서 자세히 설명 합니다.

### <a name="set-up-hello-network"></a>Hello 네트워크 설정

StorSimple은 Azure 클라우드 hello와 통합 하는 솔루션 이기 때문에 StorSimple 작업 하 고 활성 연결 toohello Azure 클라우드 필요 합니다. 이 연결은 클라우드 스냅숏, 관리 및 메타 데이터 전송 및 tootier 덜된 오래 된 데이터 tooAzure 클라우드 저장소와 같은 작업에 사용 됩니다.

Hello 솔루션 tooperform 최적으로 좋습니다 이러한 네트워킹 모범 사례를 수행:

-   StorSimple 계층화 tooAzure 연결 하는 hello 링크 대역폭 요구 사항을 충족 해야 합니다. tooachieve이 hello 필요한 서비스 품질 (QoS) 수준 tooyour 인프라 스위치 toomatch 적용 RPO 및 복구 시간 목표 (RTO) Sla 합니다.
-   최대 Azure Blob 저장소 액세스 대기 시간은 약 80ms여야 합니다.

### <a name="deploy-storsimple"></a>StorSimple 배포

단계별 StorSimple 배포 지침은 [온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough-u2.md)를 참조하세요.

### <a name="deploy-backup-exec"></a>Backup Exec 배포

Backup Exec 설치 모범 사례는 [Backup Exec 설치에 대한 모범 사례](https://www.veritas.com/support/en_US/article.000068207)(영문)를 참조하세요.

## <a name="set-up-hello-solution"></a>Hello 솔루션 설정

이 섹션에서는 몇 가지 구성 예를 보여 줍니다. hello 다음 예제 및 권장 사항을 설명 hello 가장 기본적이 고 기본 구현 합니다. 이 구현은 수 tooyour 특정 백업 요구 사항이 직접 적용 되지 않습니다.

### <a name="set-up-storsimple"></a>StorSimple 설정

| StorSimple 배포 작업  | 추가 설명 |
|---|---|
| 온-프레미스 StorSimple 장치를 배포합니다. | 지원되는 버전: 업데이트 3 이상 버전 |
| Hello 백업 대상을 설정 합니다. | 이러한 명령을 tooturn 사용 하거나 tooget 상태 및 백업 대상 모드를 해제 합니다. 자세한 내용은 참조 [tooa StorSimple 장치를 원격으로 연결](storsimple-remote-connect.md)합니다.</br> 백업 모드 tooturn: `Set-HCSBackupApplianceMode -enable`합니다. </br> 백업 모드 tooturn: `Set-HCSBackupApplianceMode -disable`합니다. </br> 백업 모드 설정의 tooget hello 현재 상태: `Get-HCSBackupApplianceMode`합니다. |
| Hello 백업 데이터를 저장 하 여 볼륨에 대 한 일반적인 볼륨 컨테이너를 만듭니다. 볼륨 컨테이너에 있는 모든 데이터의 중복을 제거합니다. | StorSimple 볼륨 컨테이너는 중복 제거 도메인을 정의합니다.  |
| StorSimple 볼륨을 만듭니다. | 볼륨 크기에 클라우드 스냅숏 지속 시간에 영향을 주므로 닫기 toohello 예상 사용 가능한으로 크기에 따라 볼륨을 만듭니다. 방법에 대 한 내용은 toosize는 볼륨에 대해 알아보세요 [보존 정책](#retention-policies)합니다.</br> </br> 사용 하 여 StorSimple 볼륨 및 선택 hello 계층 **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 확인란 합니다. </br> 로컬로 고정된 볼륨만 사용하는 것은 지원되지 않습니다. |
| 모든 hello 백업 대상 볼륨에 대 한 고유 StorSimple 백업 정책을 만듭니다. | StorSimple 백업 정책을 hello 볼륨 일관성 그룹을 정의합니다. |
| Hello 스냅숏을 만료 hello 일정을 사용 하지 않도록 설정 합니다. | 스냅숏은 후처리 작업으로 트리거됩니다. |

### <a name="set-up-hello-host-backup-server-storage"></a>Hello 호스트 서버 백업 저장소 설정

Toothese 지침에 따라 hello 호스트 서버 백업 저장소를 설정 합니다.  

- [Windows 디스크 관리]에서 만든 스팬 볼륨은 사용하지 않습니다. 스팬 디스크는 지원하지 않습니다.
- 64KB 할당 크기의 NTFS를 사용하여 볼륨을 포맷합니다.
- Hello StorSimple 볼륨에 매핑합니다 직접 toohello 백업 Exec 서버입니다.
    - 물리적 서버에 대한 iSCSI를 사용합니다.
    - 가상 서버에 대한 통과 디스크를 사용합니다.

## <a name="best-practices-for-storsimple-and-backup-exec"></a>StorSimple 및 Backup Exec에 대한 모범 사례

다음 섹션 hello에 toohello 지침에 따라 솔루션을 설정 합니다.

### <a name="operating-system-best-practices"></a>운영 체제 모범 사례

-   Windows Server 암호화 및 hello NTFS 파일 시스템에 대 한 중복 제거를 사용 하지 않도록 설정 합니다.
-   Hello StorSimple 볼륨에서 Windows Server 조각 모음을 사용 하지 않도록 설정 합니다.
-   Windows 서버 hello에 StorSimple 볼륨 인덱싱을 사용 하지 않도록 설정 합니다.
-   (대해서가 아니라 hello StorSimple 볼륨) hello 원본 호스트에서 바이러스 검사를 실행 합니다.
-   Hello 기본값 해제 [Windows 서버 유지 관리](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) 작업 관리자입니다. Hello 같은 방법으로 다음 중 하나를 수행 합니다.
   - Windows 작업 스케줄러에서 유지 관리 configurator hello 해제 합니다.
   - Windows Sysinternals에서 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)을 다운로드합니다. PsExec을 다운로드한 후 관리자 권한으로 Azure PowerShell을 실행하고 다음을 입력합니다.
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>StorSimple 모범 사례

  -   Hello StorSimple 장치 너무 업데이트 되 게[업데이트 3 이상](storsimple-install-update-3.md)합니다.
  -   iSCSI 및 클라우드 트래픽을 격리합니다. StorSimple 및 hello 백업 서버 사이의 트래픽이 전용된 iSCSI 연결을 사용 합니다.
  -   StorSimple 장치가 전용 백업 대상인지 확인합니다. 혼합 워크로드는 RTO 및 RPO에 영향을 주기 때문에 지원하지 않습니다.

### <a name="backup-exec-best-practices"></a>Backup Exec 모범 사례

-   백업 실행 StorSimple 볼륨 아니라 hello 서버의 로컬 드라이브에 설치 되어야 합니다.
-   Hello 백업 Exec 저장소 설정 **동시 쓰기 작업** toohello 최대 허용 합니다.
    -   Hello 백업 Exec 저장소 설정 **블록 및 버퍼 크기** too512 (kb)입니다.
    -   Backup Exec 저장소 **버퍼링된 읽기 및 쓰기**로 설정합니다.
-   StorSimple은 Backup Exec 전체 백업과 증분 백업을 지원합니다. 가상 백업과 차등 백업은 사용하지 않는 것이 좋습니다.
-   백업 데이터 파일에는 특정 작업에 대한 데이터만 포함되어야 합니다. 예를 들어 다른 작업에 미디어 추가가 허용되지 않습니다.
-   작업 검증을 사용하지 않도록 설정합니다. 필요한 경우 hello 최근의 백업 작업 이후 확인을 예약 해야 합니다. 것이 중요 한 toounderstand이이 작업에 백업 시간에 영향을 줍니다.
-   **저장소** > **사용자 디스크** > **세부 정보** > **속성**을 차례로 선택합니다. **디스크 공간 미리 할당**을 해제합니다.

최신 백업 Exec 설정을 hello 및 이러한 요구 사항을 구현 하기 위한 모범 사례에 대 한 참조 [hello Veritas 웹 사이트](https://www.veritas.com)합니다.

## <a name="retention-policies"></a>보존 정책

Hello 가장 일반적인 백업 보존 정책 유형 중 하나는 할아버지, 아버지 및 Son (GFS) 정책입니다. GFS 정책에서는 증분 백업이 매일 수행되고, 전체 백업은 매주 및 매월 수행됩니다. 이 정책을 적용하면 6개의 계층화된 StorSimple 볼륨이 만들어집니다. 볼륨을 하나 포함 hello 매주, 매월 및 매년 전체 백업 합니다. hello 다른 5 개의 볼륨 매일 증분 백업을 저장 합니다.

다음 예제는 hello, GFS 회전을 사용 합니다. hello 예제 hello 다음을 가정합니다.

-   중복 제거되지 않거나 압축되지 않은 데이터를 사용합니다.
-   전체 백업은 각각 1TiB입니다.
-   매일 증분 백업은 각각 500GiB입니다.
-   4개의 매주 백업이 1개월 동안 보관됩니다.
-   12개의 매월 백업이 1년 동안 보관됩니다.
-   1개의 매년 백업이 10년 동안 보관됩니다.

26-TiB 만들 hello 가정을 앞에 따라, StorSimple 볼륨 hello 매월 및 매년 전체 백업에 대 한 계층입니다. 5-TiB 만들기 StorSimple 볼륨을 각 hello 증분 매일 백업에 대 한 계층입니다.

| 백업 유형 보존 | 크기(TiB) | GFS 승수\* | 총 용량(TiB)  |
|---|---|---|---|
| 매주 전체 | 1 | 4  | 4 |
| 매일 증분 | 0.5 | 20(주기는 월별 주 수와 동일함) | 12(추가 할당량의 경우 2) |
| 매월 전체 | 1 | 12 | 12 |
| 매년 전체 | 1  | 10 | 10 |
| GFS 요구 사항 |   | 38 |   |
| 추가 할당량  | 4  |   | 42개의 총 GFS 요구 사항  |
\*hello GFS 승수는 hello 번호 복사본 tooprotect 필요 하 고이 toomeet 백업 정책 요구 사항을 유지 합니다.

## <a name="set-up-backup-exec-storage"></a>Backup Exec 저장소 설정

### <a name="tooset-up-backup-exec-storage"></a>백업 Exec 저장소 tooset

1.  Hello 백업 Exec 관리 콘솔에서 선택 **저장소** > **구성 저장소** > **디스크 기반 저장소나**  >   **다음**합니다.

    ![Backup Exec 관리 콘솔 - 저장소 구성 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image4.png)

2.  **디스크 저장소**, **다음**을 차례로 선택합니다.

    ![Backup Exec 관리 콘솔 - 저장소 선택 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image5.png)

3.  대표 이름을 입력합니다(예: **토요일 전체** 및 설명). **다음**을 선택합니다.

    ![Backup Exec 관리 콘솔 - 이름 및 설명 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image7.png)

4.  선택 hello 디스크 toocreate hello 디스크 저장 장치를 선택 하 고 선택 **다음**합니다.

    ![Backup Exec 관리 콘솔 - 저장소 디스크 선택 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image9.png)

5.  Hello 쓰기 작업 수가 너무 증가**16**를 선택한 후 **다음**합니다.

    ![Backup Exec 관리 콘솔 - 동시 쓰기 작업 설정 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image10.png)

6.  Hello 설정을 검토 한 다음 선택 **마침**합니다.

    ![Backup Exec 관리 콘솔 - 저장소 구성 요약 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image11.png)

7.  각 볼륨 할당의 hello 끝 hello 저장소 장치 설정을 toomatch에서 권장 하는 것을 변경 [백업 Exec 및 StorSimple에 대 한 모범 사례](#best-practices-for-storsimple-and-backup-exec)합니다.

    ![Backup Exec 관리 콘솔 - 저장소 장치 설정 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image12.png)

8.  StorSimple 볼륨 tooBackup Exec 할당 끝날 때까지 1-7 단계를 반복 합니다.

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>StorSimple을 기본 백업 대상으로 설정

> [!NOTE]
> 계층화 된 toohello 클라우드 된 백업에서 데이터 복원 클라우드 속도에서 발생 합니다.

hello 다음 그림은 일반적인 볼륨 tooa 백업 작업의 hello 매핑. 이 경우 모든 hello 주별 백업 toohello 토요일 전체 디스크 수 있으며 hello 증분 백업을 매핑할 tooMonday 금요일 증분 디스크. 모든 hello 백업 및 복원은 StorSimple 볼륨을 계층화 된 합니다.

![기본 백업 대상 구성 논리 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>기본 백업 대상인 StorSimple에 대한 GFS 일정 예

다음은 GFS 회전 일정(4주, 매월 및 매년)의 예입니다.

| 빈도/백업 유형 | 전체 | 증분(1-5일)  |   
|---|---|---|
| 매주(1-4주) | 토요일 | 월요일-금요일 |
| 매월  | 토요일  |   |
| 매년 | 토요일  |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-backup-job"></a>StorSimple 볼륨 tooa 백업 실행 백업 작업 할당

hello 다음 시퀀스 가정 백업 Exec 및 hello 대상 호스트를 사용 하는 hello 백업 Exec 에이전트 지침에 따라 구성 됩니다.

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-backup-job"></a>tooassign StorSimple 볼륨 tooa 백업 실행 백업 작업

1.  Hello 백업 Exec 관리 콘솔에서 선택 **호스트** > **백업** > **백업 tooDisk**합니다.

    ![백업 Exec 관리 콘솔을 호스트에서 백업과 백업 toodisk 선택](./media/storsimple-configure-backup-target-using-backup-exec/image14.png)

2.  Hello에 **백업 정의 속성** 대화 상자의 **백업**선택, **편집**합니다.

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 대화 상자](./media/storsimple-configure-backup-target-using-backup-exec/image15.png)

3.  RPO 및 RTO 요구 사항을 충족 하 고 tooVeritas 모범 사례를 준수 있도록 전체 및 증분 백업을 설정 합니다.

4.  Hello에 **백업 옵션** 대화 상자에서 **저장소**합니다.

    ![Backup Exec 관리 콘솔 - 백업 옵션 저장소 대화 상자](./media/storsimple-configure-backup-target-using-backup-exec/image16.png)

5.  해당 StorSimple 볼륨 tooyour 백업 일정을 할당 합니다.

    > [!NOTE]
    > **압축** 및 **암호화 유형** 너무 설정**None**합니다.

6.  아래 **확인**선택, hello **이 작업에 대 한 데이터를 확인 하지 않습니다** 확인란 합니다. 이 옵션을 사용하면 StorSimple 계층화에 영향을 줄 수 있습니다.

    > [!NOTE]
    > 조각 모음, 인덱싱 및 배경 확인 부정적인 영향을 미칠 hello StorSimple을 계층으로 구성 합니다.

    ![Backup Exec 관리 콘솔 - 백업 옵션 설정 확인](./media/storsimple-configure-backup-target-using-backup-exec/image17.png)

7.  요구 사항 백업 옵션 toomeet hello 나머지를 설정 했으므로, 선택 **확인** toofinish 합니다.

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>StorSimple을 보조 백업 대상으로 설정

> [!NOTE]
>계층화 된 toohello 클라우드 된 백업에서 데이터 복원을 클라우드 속도에서 발생 합니다.

이 모델에는 임시 캐시 저장소 (아닌 StorSimple) 미디어 tooserve가 있어야 합니다. 예를 들어 redundant array of independent disk (RAID) 볼륨 tooaccommodate 공간, 입/출력 (I/O) 및 대역폭을 사용할 수 있습니다. RAID 5, 50 및 10을 사용하는 것이 좋습니다.

hello 다음 그림은 일반적인 단기 보존 로컬 (toohello 서버) 볼륨 및 장기 보존 볼륨에 보관 합니다. 이 시나리오에서는 모든 백업이 실행 hello 로컬 (toohello 서버)에서 RAID 볼륨. 이러한 백업을 주기적으로 복제 및 보관 된 tooan 보관 볼륨입니다. 것은 중요 한 toosize 로컬 (toohello 서버) RAID 볼륨 단기 용량 및 성능 요구 되는 보존을 처리할 수 있도록 합니다.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>보조 백업 대상 GFS 예제인 StorSimple

![보조 백업 대상인 StorSimple 논리 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetdiagram.png)

hello 다음 표를 hello 로컬 및 StorSimple 디스크에서 백업 toorun tooset 합니다. 여기에는 개별 용량 및 전체 용량에 대한 요구 사항이 있습니다.

### <a name="backup-configuration-and-capacity-requirements"></a>백업 구성 및 용량 요구 사항

| 백업 유형 및 보존 | 구성된 저장소 | 크기(TiB) | GFS 승수 | 총 용량\*(TiB) |
|---|---|---|---|---|
| 1주차(전체 및 증분) |로컬 디스크(단기)| 1 | 1 | 1 |
| StorSimple 2-4주 |StorSimple 디스크(장기) | 1 | 4 | 4 |
| 매월 전체 |StorSimple 디스크(장기) | 1 | 12 | 12 |
| 매년 전체 |StorSimple 디스크(장기) | 1 | 1 | 1 |
|GFS 볼륨 크기 요구 사항 |  |  |  | 18*|
\* 총 용량에는 17TiB의 StorSimple 디스크 및 1TiB 로컬 RAID 볼륨이 포함됩니다.


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a>GFS 예제 일정: GFS 회전 매주, 매월 및 매년 일정

| 주 | 전체 | 증분 1일차 | 증분 2일차 | 증분 3일차 | 증분 4일차 | 증분 5일차 |
|---|---|---|---|---|---|---|
| 1주차 | 로컬 RAID 볼륨  | 로컬 RAID 볼륨 | 로컬 RAID 볼륨 | 로컬 RAID 볼륨 | 로컬 RAID 볼륨 | 로컬 RAID 볼륨 |
| 2주차 | StorSimple 2-4주 |   |   |   |   |   |
| 3주차 | StorSimple 2-4주 |   |   |   |   |   |
| 4주차 | StorSimple 2-4주 |   |   |   |   |   |
| 매월 | StorSimple 매월 |   |   |   |   |   |
| 매년 | StorSimple 매년  |   |   |   |   |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-archive-and-deduplication-job"></a>StorSimple는 볼륨 tooa 백업 Exec 보관 및 중복 제거 작업 할당

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-archive-and-duplication-job"></a>tooassign StorSimple 볼륨 tooa 백업 Exec 중복 및 보관 작업

1.  Hello 백업 Exec 관리 콘솔에서 마우스 오른쪽 단추로 클릭 hello 작업 tooarchive tooa StorSimple 볼륨을 선택 하 고 선택 **백업 정의 속성** > **편집**합니다.

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 탭](./media/storsimple-configure-backup-target-using-backup-exec/image19.png)

2.  선택 **추가 단계** > **tooDisk 중복** > **편집**합니다.

    ![Backup Exec 관리 콘솔 - 스테이지 추가](./media/storsimple-configure-backup-target-using-backup-exec/image20.png)

3.  Hello에 **중복 옵션** 대화 상자, 선택 hello 값에 대 한 toouse 원하는 **소스** 및 **일정**합니다.

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image21.png)

4.  Hello에 **저장소** 드롭 다운 목록, 선택 hello StorSimple 볼륨 hello 보관 작업 toostore hello 데이터입니다.

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image22.png)

5.  선택 **확인**를 선택한 후 hello **이 작업에 대 한 데이터를 확인 하지 않습니다** 확인란 합니다.

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image23.png)

6.  **확인**을 선택합니다.

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image24.png)

7.  Hello에 **백업** 열을 새 단계를 추가 합니다. 사용 하 여 hello 원본에 대 한 **증분**합니다. Hello 대상에 대 한 hello hello 증분 백업 작업이 모두 보관 하는 StorSimple 볼륨을 선택 합니다. 1-6단계를 반복합니다.

## <a name="storsimple-cloud-snapshots"></a>StorSimple 클라우드 스냅숏

StorSimple 클라우드 스냅숏 StorSimple 장치에 상주 하는 hello 데이터를 보호 합니다. 클라우드 스냅숏을 만드는 해당 tooshipping 로컬 백업 테이프 tooan 오프 사이트 시설입니다. Azure 지역 중복 저장소를 사용 하 여 클라우드 스냅숏을 만드는 경우 해당 tooshipping 백업 테이프 toomultiple 사이트입니다. 재해가 발생 한 후 장치 toorestore 해야 할 경우에 다른 StorSimple 장치를 온라인 상태로 전환 수도 있으며 장애 조치를 수행 수 있습니다. Hello 장애 조치 후 hello 가장 최근 클라우드 스냅숏의 수 tooaccess hello 데이터 (클라우드 속도로) 있을 수 있습니다.

hello 섹션 다음 방법을 toocreate 간단한 스크립트 toostart 및 delete StorSimple 클라우드 스냅숏 백업 후 처리 과정을 설명 합니다.

> [!NOTE]
> 수동으로 또는 프로그래밍 방식으로 만든 스냅숏을 hello StorSimple 스냅숏 만료 정책을 따르지 않습니다. 이러한 스냅숏은 수동 또는 프로그래밍 방식으로 삭제되어야 합니다.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>스크립트를 사용하여 클라우드 스냅숏 시작 및 삭제

> [!NOTE]
> Hello 규정 준수 및 데이터 보존 영향 StorSimple 스냅숏 삭제 하기 전에 신중 하 게 평가 합니다. 방법에 대 한 자세한 내용은 toorun 백업 후 스크립트 참조 hello [백업 Exec 설명서](https://www.veritas.com/support/en_US/15047.html)합니다.

### <a name="backup-lifecycle"></a>백업 주기

![백업 주기 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/backuplifecycle.png)

### <a name="requirements"></a>요구 사항

-   hello 스크립트를 실행 하는 hello 서버 tooAzure 클라우드 리소스에 액세스 있어야 합니다.
-   hello 사용자 계정에는 hello 필요한 사용 권한이 있어야 합니다.
-   Hello로 StorSimple 백업 정책이 연결 StorSimple 볼륨 설정할 수 있지만으로 해제 해야 합니다.
-   StorSimple 리소스 이름, 등록 키, 장치 이름 및 백업 정책 id입니다. hello 필요 합니다.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart 또는 클라우드 스냅숏 삭제

1.  [Azure PowerShell 설치](/powershell/azure/overview)
2.  [게시 설정 및 구독 정보를 다운로드하여 가져옵니다](https://msdn.microsoft.com/library/dn385850.aspx).
3.  Hello Azure 클래식 포털에서 hello 리소스 이름을 가져올 및 [StorSimple Manager 서비스에 대 한 등록 키](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)합니다.
4.  Hello 스크립트를 실행 하는 hello 서버에서 관리자 권한으로 PowerShell을 실행 합니다. 다음 명령을 입력합니다.

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    참고 hello 백업 정책 id입니다.
5.  메모장에서 코드 다음 hello를 사용 하 여 새 PowerShell 스크립트를 만듭니다.

    다음 코드 조각을 복사하여 붙여넣습니다.
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
      Hello PowerShell 스크립트 toohello 저장 Azure 저장 한 동일한 위치에 게시 설정 합니다. 예를 들어 C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1로 저장합니다.
6.  백업 실행에 백업 실행 작업 옵션 전처리 편집 및 사후 명령을 처리 하 여 hello 스크립트 tooyour 백업 작업을 추가 합니다.

    ![Backup Exec 콘솔 - 백업 옵션, 전처리 및 후처리 명령 탭](./media/storsimple-configure-backup-target-using-backup-exec/image25.png)

> [!NOTE]
> 매일 백업 작업의 hello 끝에 후 처리 스크립트로 StorSimple 클라우드 스냅숏 백업 정책을 실행 하는 것이 좋습니다. 어떻게를 tooback 및 복원 RPO 및 RTO를 충족 하 여 백업 응용 프로그램 환경 toohelp 문의 백업 프로그램 설계자에 대 한 자세한 내용은 합니다.

## <a name="storsimple-as-a-restore-source"></a>복원 원본인 StorSimple

StorSimple 장치에서 복원하면 모든 블록 저장소 장치에서 복원하는 것처럼 작동합니다. 계층화 된 toohello 클라우드 데이터의 복원 클라우드 속도에서 발생 합니다. 로컬 데이터에 대 한 복원 hello 장치의 hello 로컬 디스크 속도에서 발생합니다. 방법에 대 한 내용은 tooperform 복원 하는 hello 백업 Exec 설명서를 참조 하십시오. TooBackup Exec 복원에 대 한 모범 사례를 준수 하는 것이 좋습니다.

## <a name="storsimple-failover-and-disaster-recovery"></a>StorSimple 장애 조치(failover) 및 재해 복구

> [!NOTE]
> 백업 대상 시나리오의 경우 StorSimple 클라우드 어플라이언스는 복원 대상으로 지원되지 않습니다.

재해는 다양한 요인으로 발생할 수 있습니다. 다음 표에서 hello 일반적인 재해 복구 시나리오를 나열 합니다.

| 시나리오 | 영향 | 어떻게 toorecover | 참고 사항 |
|---|---|---|---|
| StorSimple 장치 오류 | 백업 및 복원 작업이 중단됩니다. | Hello 실패 한 장치를 교체 하 고 수행할 [StorSimple 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다. | Tooperform 장치 복구 후 복원 해야 할 경우 hello 클라우드 toohello 새 장치에서 전체 데이터 작업 집합이 검색 됩니다. 모든 작업이 클라우드 속도로 수행됩니다. hello 인덱싱 및 다시 검색 프로세스를 카탈로그 작업을 검사 하 고 hello 클라우드 계층 toohello 로컬 장치 계층은 시간이 많이 소요 될 수 있는에서 가져온 모든 백업 세트 toobe를 발생할 수 있습니다. |
| Backup Exec 서버 오류 | 백업 및 복원 작업이 중단됩니다. | 에 설명 된 대로 데이터베이스 복원을 수행 하 고 hello 백업 서버를 다시 빌드해야 [어떻게 toodo 수동 백업 및 복원 중 백업 Exec (BEDB) 데이터베이스](http://www.veritas.com/docs/000041083)합니다. | Hello 백업 Exec 서버 hello 재해 복구 사이트에서 복원 하거나 다시 작성 해야 합니다. Hello 데이터베이스 toohello 최근 지점을 복원 합니다. Hello 복원할 백업 실행 데이터베이스 된 최신 백업 작업과 동기화 되지 않았습니다. 인덱싱 및 카탈로그 만들기가 필요 합니다. 이 인덱스 및 카탈로그 프로세스를 다시 검색을 검사 하 고 hello 클라우드 계층 toohello 로컬 장치 계층에서 가져온 모든 백업 세트 toobe를 발생할 수 있습니다. 그러면 더욱 시간이 많이 걸립니다. |
| 백업 서버 hello와 StorSimple의 hello 손실 되는 사이트 오류 | 백업 및 복원 작업이 중단됩니다. | 먼저 StorSimple을 복원한 다음 Backup Exec을 복원합니다. | 먼저 StorSimple을 복원한 다음 Backup Exec을 복원합니다. Tooperform 장치 복구 후 복원 해야 할 경우 hello 전체 데이터 작업 집합이 hello 클라우드 toohello 새 장치에서 검색 됩니다. 모든 작업이 클라우드 속도로 수행됩니다. |

## <a name="references"></a>참조

hello 다음 문서는이 문서에 대 한 참조 된:

- [StorSimple 다중 경로 I/O 설정](storsimple-configure-mpio-windows-server.md)
- [저장소 시나리오: 씬 프로비전](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [GPT 드라이브 사용](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [공유 폴더의 섀도 복사본 설정](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>다음 단계

- 너무 방법에 대 한 자세한[백업 세트에서 복원이](storsimple-restore-from-backup-set-u2.md)합니다.
- 에 대 한 자세한 방법에 대 한 tooperform [장치 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다.
