---
title: "aaaAzure 백업 서버 시스템 상태를 보호 하 고 복원 toobare 금속 | Microsoft Docs"
description: "Azure 백업 서버 tooback 시스템 상태를 사용 하 고 완전 복구 (BMR) 보호를 제공 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
keywords: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.targetplatform: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: markgal,masaran
ms.openlocfilehash: d34c8bbdc7cc24c905f81ceaf199698c1ee923db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-system-state-and-restore-toobare-metal-with-azure-backup-server"></a>시스템 상태를 백업 하 고 toobare 금속 Azure 백업 서버를 복원 합니다.

Azure Backup Server는 시스템 상태를 백업하고 BMR(완전 복구) 보호를 제공합니다.

*   **시스템 상태 백업**: 컴퓨터가 시작 되기는 하지만 시스템 파일 및 hello 레지스트리가 손실 됩니다 때 복구할 수 있도록 운영 체제 파일을 백업 합니다. 시스템 상태 백업에는 다음이 포함됩니다.
    * 도메인 구성원: 부팅 파일, COM+ 클래스 등록 데이터베이스, 레지스트리
    * 도메인 컨트롤러: Windows Server Active Directory(NTDS), 부팅 파일, COM+ 클래스 등록 데이터베이스, 레지스트리, 시스템 볼륨(SYSVOL)
    * 클러스터 서비스를 실행하는 컴퓨터: 클러스터 서버 메타데이터
    * 인증서 서비스를 실행하는 컴퓨터: 인증서 데이터
* **완전 복구 백업**: 운영 체제 파일 및 중요 볼륨의 모든 데이터를 백업합니다(사용자 데이터 제외). 기본적으로 BMR 백업에는 시스템 상태 백업이 포함됩니다. 컴퓨터가 시작 되지 않음 고 toorecover 모든 항목이 있는 경우 보호를 제공 합니다.

다음 표에 hello 무엇을 백업 하 고 복구할 수를 요약 합니다. 시스템 상태 및 BMR로 보호할 수 있는 앱 버전에 대한 자세한 내용은 [Azure Backup Server로 백업할 수 있는 항목](backup-mabs-protection-matrix.md)을 참조하세요.

|백업|문제|Azure Backup Server 백업에서 복구|시스템 상태 백업에서 복구|BMR|
|----------|---------|---------------------------|------------------------------------|-------|
|**파일 데이터**<br /><br />정기적인 데이터 백업<br /><br />BMR/시스템 상태 백업|손실된 파일 데이터|Y|N|N|
|**파일 데이터**<br /><br />파일 데이터의 Azure Backup Server 백업<br /><br />BMR/시스템 상태 백업|손실되거나 손상된 운영 체제|N|Y|Y|
|**파일 데이터**<br /><br />파일 데이터의 Azure Backup Server 백업<br /><br />BMR/시스템 상태 백업|손실된 서버(데이터 볼륨 그대로 유지)|N|N|Y|
|**파일 데이터**<br /><br />파일 데이터의 Azure Backup Server 백업<br /><br />BMR/시스템 상태 백업|손실된 서버(데이터 볼륨 손실)|Y|아니요|예(BMR, 이후 백업된 파일 데이터의 정기적인 복구 수행)|
|**SharePoint 데이터**:<br /><br />팜 데이터의 Azure Backup Server 백업<br /><br />BMR/시스템 상태 백업|손실된 사이트, 목록, 목록 항목, 문서|Y|N|N|
|**SharePoint 데이터**:<br /><br />팜 데이터의 Azure Backup Server 백업<br /><br />BMR/시스템 상태 백업|손실되거나 손상된 운영 체제|N|Y|Y|
|**SharePoint 데이터**:<br /><br />팜 데이터의 Azure Backup Server 백업<br /><br />BMR/시스템 상태 백업|재해 복구|N|N|N|
|Windows Server 2012 R2 Hyper-V<br /><br />Hyper-V 호스트 또는 게스트의 Azure Backup Server 백업<br /><br />호스트의 BMR/시스템 상태 백업|손실된 VM|Y|N|N|
|Hyper-V<br /><br />Hyper-V 호스트 또는 게스트의 Azure Backup Server 백업<br /><br />호스트의 BMR/시스템 상태 백업|손실되거나 손상된 운영 체제|N|Y|Y|
|Hyper-V<br /><br />Hyper-V 호스트 또는 게스트의 Azure Backup Server 백업<br /><br />호스트의 BMR/시스템 상태 백업|손실된 Hyper-V 호스트(VM 그대로 유지)|N|N|Y|
|Hyper-V<br /><br />Hyper-V 호스트 또는 게스트의 Azure Backup Server 백업<br /><br />호스트의 BMR/시스템 상태 백업|손실된 Hyper-V 호스트(VM 손실)|N|N|Y<br /><br />BMR, 이후 정기적인 Azure Backup Server 복구 수행|
|SQL Server/Exchange<br /><br />Azure Backup Server 앱 백업<br /><br />BMR/시스템 상태 백업|손실된 앱 데이터|Y|N|N|
|SQL Server/Exchange<br /><br />Azure Backup Server 앱 백업<br /><br />BMR/시스템 상태 백업|손실되거나 손상된 운영 체제|N|y|Y|
|SQL Server/Exchange<br /><br />Azure Backup Server 앱 백업<br /><br />BMR/시스템 상태 백업|손실된 서버(데이터베이스/트랜잭션 로그 그대로 유지)|N|N|Y|
|SQL Server/Exchange<br /><br />Azure Backup Server 앱 백업<br /><br />BMR/시스템 상태 백업|손실된 서버(데이터베이스/트랜잭션 로그 손실)|N|N|Y<br /><br />BMR 복구, 이후 정기적인 Azure Backup Server 복구 수행|

## <a name="how-system-state-backup-works"></a>시스템 상태 백업의 작동 방식

시스템 상태 백업을 실행 되 면 백업 서버 hello 서버 시스템 상태 백업을 Windows Server 백업 toorequest와 통신 합니다. 기본적으로 백업 서버 및 Windows Server 백업 hello 드라이브 가장 사용 가능한 여유 공간이 hello를 사용 합니다. 이 드라이브에 대 한 정보는 hello PSDataSourceConfig.xml 파일에 저장 됩니다. 백업에 대 한 Windows Server 백업을 사용 하는 hello 드라이브입니다.

백업 서버 hello 시스템 상태 백업에 사용 하는 hello 드라이브를 사용자 지정할 수 있습니다. Hello 보호 된 서버의 데이터 보호 Manager\MABS\Datasources tooC:\Program Files\Microsoft 이동 합니다. 편집을 위해 hello PSDataSourceConfig.xml 파일을 엽니다. 변경 hello \<c t\> hello 드라이브 문자에 대 한 값입니다. 저장 하 고 hello 파일을 닫습니다. 보호 그룹 집합이 있으면 tooprotect hello 컴퓨터의 시스템 상태를 hello, 일관성 확인을 실행 합니다. 경고가 생성 되는 경우 선택 **보호 그룹 수정** hello 경고 및 다음 전체 hello 마법사. 그다음에 추가적인 일관성 확인을 실행합니다.

참고 hello 보호 서버가 클러스터에 있으면 수 있다는 것을 클러스터 드라이브 hello 가장 사용 가능한 공간이 있는 hello 드라이브로 선택 됩니다. 해당 드라이브 소유권 전환 된 tooanother 노드 된 시스템 상태 백업을 실행 하는 경우 hello 드라이브 사용할 수 없고 hello 백업이 실패 합니다. 이 시나리오에서는 PSDataSourceConfig.xml toopoint tooa 로컬 드라이브를 수정 합니다.

다음으로, Windows Server 백업 WindowsImageBackup hello 복원 폴더의 루트 hello 라는 폴더를 만듭니다. Windows Server 백업 hello 백업 만들기, 모든 hello 데이터는이 폴더에 배치 됩니다. Hello 백업이 완료 되 면 hello 파일은 전송 된 toohello 백업 서버 컴퓨터입니다. 다음 정보는 참고 hello:

* 이 폴더와 해당 내용을 정리 되지 않는 hello 백업 또는 전송이 완료 되 면 합니다. 이 가장 좋은 방법은 toothink hello는 hello 공간 예약 하는 중 hello에 대 한 백업이 완료 된 다음 번입니다.
* hello 폴더에는 백업이 수행 될 때마다 생성 됩니다. 마지막 시스템 상태 백업의 hello 시간을 반영 하는 hello 날짜 및 시간 스탬프입니다.

## <a name="bmr-backup"></a>BMR 백업

BMR (시스템 상태 백업을 포함)에 대 한 hello 백업 작업을 직접 tooa 공유 컴퓨터에 저장 되며 hello 백업 서버입니다. Tooa 폴더 hello 보호 된 서버에 저장 되지 않습니다.

Windows Server 백업 호출 하 고 해당 BMR 백업에 대 한 hello 복제 볼륨을 공유 하는 백업 서버. 이 경우 Windows Server 백업 toouse hello hello 가장 여유 공간이 드라이브를 알 수 없습니다. 대신, hello 작업에 대해 생성 된 hello 공유를 사용 합니다.

Hello 백업이 완료 되 면 hello 파일은 전송 된 toohello 백업 서버 컴퓨터입니다. 로그는 C:\Windows\Logs\WindowsServerBackup에 저장됩니다.

## <a name="prerequisites-and-limitations"></a>필수 구성 요소 및 제한 사항

-   Windows Server 2003을 실행하는 컴퓨터나 클라이언트 운영 체제를 실행하는 컴퓨터에서는 BMR이 지원되지 않습니다.

-   BMR를 보호할 수 없습니다 및 동일한 hello에 대 한 시스템 상태를 다른 보호 그룹에 컴퓨터입니다.

-   Backup Server 컴퓨터에서는 BMR을 위해 자체적으로 보호할 수 없습니다.

-   BMR에 대 한 단기 보호 tootape (디스크-테이프 또는 D2T) 지원 되지 않습니다. 장기 저장소 tootape (디스크-에-디스크-테이프, 또는 D2D2T) 사용할 수 있습니다.

-   BMR 보호를 위해 Windows Server 백업 hello 보호 된 컴퓨터에 설치 되어야 합니다.

-   BMR 보호를 위해 달리 시스템 상태 보호 백업 서버 없는 공간 요구 사항이 hello 보호 된 컴퓨터에 있습니다. Windows Server 백업 백업을 toohello 백업 서버 컴퓨터를 직접 전송합니다. 백업 서버 hello에 hello 백업 전송 작업이 표시 되지 않으면 **작업** 보기.

-   백업 서버는 BMR에 대 한 30GB의 hello 복제본 볼륨에 공간을 예약합니다. Hello에이 변경할 수 있습니다 **디스크 할당** 페이지 hello 보호 그룹 수정 마법사를 사용 하거나 hello Get-datasourcediskallocation 및 Set-datasourcediskallocation PowerShell cmdlet을 사용 하 여 합니다. Hello 복구 지점 볼륨에 BMR 보호는 6GB 약 5 일의 보존 기간에 대 한 필요합니다.
    * 참고 15GB 보다 hello 복제본 볼륨 크기 tooless을 줄일 수 없습니다.
    * 백업 서버 hello BMR 데이터 원본의 hello 크기를 계산 하지 않습니다. 모든 서버에 대해 30GB를 가정합니다. 사용자 환경에서 예상 하는 BMR 백업의 hello 크기에 따라 hello 값을 변경 합니다. 모든 중요 한 볼륨에 사용 된 공간의 합 hello로 BMR 백업의 hello 크기를 대략 계산할 수 있습니다. 중요한 볼륨 = 부팅 볼륨 + 시스템 볼륨 + 시스템 상태 데이터 호스트 볼륨(예: Active Directory).

-   시스템 상태 보호 tooBMR 보호에서 변경한 경우 BMR 보호에서 필요한 공간이 줄어듭니다 hello *복구 지점 볼륨*합니다. 그러나 hello hello 볼륨에 여분의 공간 회수 되지 않습니다. Hello에 hello 볼륨 크기를 수동으로 축소할 수 있습니다 **디스크 할당 수정** hello 보호 그룹 수정 마법사의 페이지나 hello Get-datasourcediskallocation 및 Set-datasourcediskallocation PowerShell cmdlet을 사용 하 여 합니다.

    BMR 보호 hello에 더 많은 공간이 필요 시스템 상태 보호 tooBMR 보호에서 변경 하면 *복제 볼륨*합니다. hello 볼륨을 자동으로 확장 됩니다. Toochange hello 기본 공간 할당 하려는 경우 hello Modify-diskallocation PowerShell cmdlet을 사용 합니다.

-   BMR 보호 toosystem 상태 보호에서 변경 하면 hello 복구 지점 볼륨에 더 많은 공간이 필요 합니다. 백업 서버 tooautomatically hello 볼륨 높임 해 보십시오. Hello 저장소 풀에 공간이 부족 오류가 발생 합니다.

    BMR 보호 toosystem 상태 보호에서 변경 하면 hello 보호 된 컴퓨터에 공간이 필요 합니다. 시스템 상태 보호 hello 복제본 toohello 로컬 컴퓨터를 처음으로 작성 한 후 그 toohello 백업 서버 컴퓨터를 전송 하는 때문입니다.

## <a name="before-you-begin"></a>시작하기 전에

1.  **Azure Backup Server 배포**. Backup Server가 제대로 배포되어 있는지 확인합니다. 자세한 내용은 다음을 참조하세요.
    * [System requirements for Azure Backup Server](http://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)(Azure Backup Server 시스템 요구 사항)
    * [Backup Server 보호 매트릭스](backup-mabs-protection-matrix.md)

2.  **저장소 설정**. 디스크를 azure의 hello 클라우드 및 테이프에 백업 데이터를 저장할 수 있습니다. 자세한 내용은 [Prepare data storage](https://docs.microsoft.com/system-center/dpm/plan-long-and-short-term-data-storage)(데이터 저장소 준비)를 참조하세요.

3.  **Hello 보호 에이전트 설정**합니다. Tooback를 원하는 hello 컴퓨터에 hello 보호 에이전트를 설치 합니다. 자세한 내용은 참조 [hello DPM 보호 에이전트 배포](http://docs.microsoft.com/system-center/dpm/deploy-dpm-protection-agent)합니다.

## <a name="back-up-system-state-and-bare-metal"></a>시스템 상태 백업 및 완전 복구 백업
[Deploy protection groups](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups)(보호 그룹 배포)의 설명대로 보호 그룹을 설정합니다. BMR를 보호할 수 없습니다 및 hello에 대 한 시스템 상태 같은 서로 다른 그룹에 컴퓨터입니다. 또한 BMR을 선택하면 시스템 상태가 자동으로 사용하도록 설정됩니다.


1.  백업 서버 관리자 콘솔에서 선택 hello에서 tooopen hello 새 보호 그룹 만들기 마법사 **보호** > **동작** > **보호 그룹 만들기 그룹**합니다.

2.  Hello에 **보호 그룹 종류 선택** 페이지 **서버**를 선택한 후 **다음**합니다.

3.  Hello에 **그룹 구성원 선택** 페이지 hello 컴퓨터를 확장 하 고 다음 중 하나를 선택 **BMR** 또는 **시스템 상태**합니다.

    Hello에 대 한 BMR와 시스템 상태를 보호할 수 없습니다 기억 서로 다른 그룹에 동일한 컴퓨터. 또한 BMR을 선택하면 시스템 상태가 자동으로 사용하도록 설정됩니다. 자세한 내용은 [Deploy protection groups](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups)(보호 그룹 배포)를 참조하세요.

4.  Hello에 **데이터 보호 방법 선택** 페이지, toohandle 단기 및 장기 백업 방법을 선택 합니다. 단기 백업은 먼저 toodisk 항상, Azure 백업 (단기 또는 장기)을 사용 하 여 클라우드 hello 디스크 toohello Azure에서에서 백업의 hello 옵션으로 합니다. 대체 toolong 장기 백업 toohello 클라우드 tooset 장기 백업 tooa 독립 실행형 테이프 장치 또는 테이프 라이브러리를 tooBackup 서버에 연결 된입니다.

5.  Hello에 **단기 목표 선택** 페이지에서 원하는 tooback 디스크에 대 한 tooshort 장기 저장소를 선택 합니다.
    1. 에 대 한 **보존 범위**, tookeep hello 디스크에 데이터를 원하는 기간을 선택 합니다. 
    2. 에 대 한 **동기화 빈도**, toorun는 증분 백업 toodisk 빈도 선택 합니다. Tooset 백업 간격을 사용 하지 않으려면 hello를 확인할 수 있습니다 **복구 지점 직전** 옵션입니다. Backup Server에서는 각 복구 지점이 예약되기 직전에 빠른 전체 백업을 실행합니다.

6.  Hello에 장기 저장을 위해 toostore 테이프의 데이터를 원하는 **장기 목표 지정** 페이지에서 원하는 tookeep 테이프 데이터 (1-99 년) 기간을 선택 합니다. 
    1. 에 대 한 **백업 빈도**, 백업 tootape 실행할지 시간 간격을 선택 합니다. hello 주파수 선택한 hello 보존 범위를 기반으로 합니다.
        * Hello 보존 범위가 1-99 년 이면 매일, 매주, 격주 별, 월별, 분기별, 반년 마다 또는 매년 백업을 toooccur를 선택할 수 있습니다.
        * Hello 보존 범위가 1-11 개월 경우 매일, 매주, 격주 별 또는 매월 백업을 toooccur를 선택할 수 있습니다.
        * Hello 보존 범위가 1-4 주일 경우 매일 또는 매주 백업을 toooccur를 선택할 수 있습니다.

    2. Hello에 **선택 테이프 및 라이브러리 세부 정보** 페이지, 선택 hello 테이프 및 라이브러리 toouse 및 데이터를 압축 및 암호화 된 여부.

7.  Hello에 **디스크 할당 검토** 페이지 hello 보호 그룹에 대해 할당 되는 hello 저장소 풀 디스크 공간을 검토 합니다.

    1. **총 데이터 크기** tooback를 원하는 hello 데이터의 hello 크기입니다.
    2. **Azure 백업 서버를 프로 비전 된 디스크 공간 toobe** 백업 서버 hello 보호 그룹에 대해 권장 하는 hello 공간이 있습니다. 백업 서버 hello 설정에 따라 hello 이상적인 백업 볼륨을 선택 합니다. 그러나 hello 백업 볼륨 선택 항목을 편집할 수 **할당 세부 정보를 디스크**합니다. 
    3. 작업의 경우 hello 드롭 다운 메뉴에서 hello 기본 설정 저장소를 선택 합니다. Hello 값을 변경 하는 편집 **총 저장소** 및 **사용 가능한 저장소** hello에 **사용 가능한 디스크 저장소** 창. Underprovisioned 공간은 hello 백업 서버 볼륨 toohello tooensure 부드러운 백업을 추가 제안 하는 저장소 크기입니다.

8.  Hello에 **복제본 만들기 방법 선택** 페이지에서 원하는 toohandle hello 전체 초기 데이터 복제를 선택 합니다. Hello 네트워크를 통해 tooreplicate를 선택 하면 사용량이 적은 시간을 선택 하는 것이 좋습니다. 많은 양의 데이터에 대 한 또는 보다 작은 가장 적합 한 네트워크 조건에 대 한 이동식 미디어를 사용 하 여 hello 오프 라인으로 데이터를 복제 하는 것이 좋습니다.

9. Hello에 **일관성 확인 옵션 선택** 페이지에서 원하는 tooautomate 일관성 확인을 선택 합니다. 일치 하지 않아 또는 일정에 따라 복제본 데이터에 불일치가 있는 경우에 검사를 toorun을 선택할 수 있습니다. Tooconfigure 자동 일관성 검사를 사용 하지 않으려는 경우에 언제 든 지 수동 확인을 실행할 수 있습니다. 수동 확인을 hello toorun **보호** hello 백업 서버 관리자 콘솔의 영역 hello 보호 그룹을 선택한 다음 마우스 오른쪽 단추로 클릭 **일관성 확인 수행**합니다.

10. Hello에 Azure 백업을 사용 하 여 tooback toohello 클라우드를 선택 하는 경우 **온라인 보호 데이터 지정** 페이지에서 원하는 tooAzure tooback hello 워크 로드를 선택 했는지 확인 합니다.

11. Hello에 **온라인 백업 일정 지정** 페이지 tooAzure 실시할 얼마나 자주 증분 백업을 선택 합니다. 백업을 toorun 모든 일, 주, 월 및 연도, 예약 하 고 선택 hello 날짜 및 시간을 실행 해야 할 수 있습니다. 백업은 하루 tootwice를 발생할 수 있습니다. 될 때마다 백업 실행 데이터 복구 지점은 Azure에 만들어지는 hello 서버 백업 디스크에 저장 된 hello 백업 데이터의 hello 복사본에서 합니다.

12. Hello에 **온라인 보존 정책 지정** 페이지에서 Azure의 hello 매일, 매주, 매월 및 매년 백업에서 생성 된 hello 복구 지점 유지 되는 방법을 선택 합니다.

13. Hello에 **온라인 복제 선택** 페이지에서 데이터의 초기 전체 복제를 hello 발생 하는 방법을 선택 합니다. 오프 라인 수행 하거나 hello 네트워크를 통해 복제할 수 있습니다 (오프 라인 시드) 백업 합니다. 오프 라인 백업 hello Azure 가져오기 기능을 사용합니다. 자세한 내용은 [Azure Backup의 오프라인 백업 워크플로](backup-azure-backup-import-export.md)를 참조하세요.

14. Hello에 **요약** 페이지에서 설정을 검토 합니다. 선택한 후 **그룹 만들기**, hello 데이터의 초기 복제가 실행 됩니다. 데이터 복제 완료 되 면 hello에 **상태** 페이지 hello 보호 그룹 상태가 **확인**합니다. 백업 다음 당 hello 보호 그룹 설정 수행 됩니다.

## <a name="recover-system-state-or-bmr"></a>시스템 상태 또는 BMR 복구
BMR 또는 시스템 상태 tooa 네트워크 위치를 복구할 수 있습니다. BMR을 백업한 경우 Windows 복구 환경 (WinRE) toostart 시스템을 사용 하 고 toohello 네트워크에 연결 합니다. 그런 다음 hello 네트워크 위치에서 Windows Server 백업 toorecover를 사용 합니다. 시스템 상태를 백업한 경우 Windows Server 백업 toorecover hello 네트워크 위치에서 사용할 것입니다.

### <a name="restore-bmr"></a>BMR 복원
Hello 백업 서버 컴퓨터에 복구를 실행 합니다.

1.  Hello에 **복구** 창, 찾기 hello 컴퓨터 toorecover, 한 다음 선택 **완전 복구**합니다.

2.  사용 가능한 복구 지점은 hello 달력에 굵게에 표시 됩니다. Hello 날짜와 시간을 원하는 toouse hello 복구 지점 선택 합니다.

3.  Hello에 **복구 유형 선택** 페이지에서 선택 **tooa 네트워크 폴더에 복사 합니다.**

4.  Hello에 **대상 지정** 페이지 toocopy hello 데이터를 넣을 위치 선택 합니다. 해당 hello 선택한 대상 필요한 toohave 공간이 충분 해야 합니다. 새 폴더를 만드는 것이 좋습니다.

5.  Hello에 **복구 옵션 지정** 페이지, 보안 설정 tooapply hello 선택 합니다. 그런 다음 toouse 저장 영역 네트워크 (SAN) 할지 여부를 선택-신속한 복구를 위해 하드웨어 스냅숏을 기반으로 합니다. (이것은 옵션 기능 toocreate hello과 복제 toomake 분할이 기능을 사용할 수 있는 SAN이 있는 경우에 쓰기 가능한 것입니다. 또한 hello 보호 된 컴퓨터 및 백업 서버 컴퓨터 해야 toohello 연결 된 동일한 네트워크.)

6.  알림 옵션을 설정합니다. Hello에 **확인** 페이지에서 **복구**합니다.

Hello 공유 위치를 설정 합니다.

1.  Hello 복원 위치 hello 백업 toohello 폴더를 이동 합니다.

2.  hello hello 공유 폴더의 루트는 hello WindowsImageBackup 폴더가 되도록 windowsimagebackup 보다 한 수준 hello 폴더를 공유 합니다. 이렇게 하지 않으면 경우 복원 hello 백업을 찾을 수 없습니다. Windows 복구 환경 (WinRE)을 사용 하 여 tooconnect, hello 올바른 IP 주소 및 자격 증명으로 WinRE에 액세스할 수 있는 공유를 해야 합니다.

Hello 시스템을 복원 합니다.

1.  복원 하는 hello 시스템에 대 한 hello Windows DVD를 사용 하 여 toorestore hello 이미지 하려는 hello 컴퓨터를 시작 합니다.

2.  Hello 첫 번째 페이지에서 언어 및 로캘 설정을 확인 합니다. Hello에 **설치** 페이지에서 **컴퓨터 복구**합니다.

3.  Hello에 **시스템 복구 옵션** 페이지에서 **앞에서 만든 시스템 이미지를 사용 하 여 컴퓨터를 복원**합니다.

4.  Hello에 **시스템 이미지 백업 선택** 페이지 **시스템 이미지 선택** > **고급** > **시스템에 대 한 검색 hello 네트워크에서 이미지**합니다. 경고가 나타나면 **예**를 선택합니다. Toohello 공유 경로 이동 하 고 hello 자격 증명을 입력 hello 복구 지점을 선택 합니다. 이렇게 하면 해당 복구 지점에서 사용할 수 있는 특정 백업이 검색됩니다. Toouse 사용할 hello 복구 지점을 선택 합니다.

5.  Hello에 **toorestore hello 백업 방법을 선택** 페이지에서 **디스크 포맷 및 다시 분할**합니다. Hello 다음 페이지에서 설정을 확인 합니다. 

6.  선택 toobegin hello 복원 **마침**합니다. 다시 시작해야 합니다.

### <a name="restore-system-state"></a>시스템 상태 복원

Backup Server에서 복구를 실행합니다.

1.  Hello에 **복구** 창 찾기 hello 컴퓨터 toorecover를 원하고 다음 선택 **완전 복구**합니다.

2.  사용 가능한 복구 지점은 hello 달력에 굵게에 표시 됩니다. Hello 날짜와 시간을 원하는 toouse hello 복구 지점 선택 합니다.

3.  Hello에 **복구 유형 선택** 페이지 **tooa 네트워크 폴더에 복사**합니다.

4.  Hello에 **대상 지정** 페이지에서 toocopy hello 데이터입니다. 해당 hello 선택한 대상 필요한 공간이 충분 해야 합니다. 새 폴더를 만드는 것이 좋습니다.

5.  Hello에 **복구 옵션 지정** 페이지, 보안 설정 tooapply hello 선택 합니다. 신속한 복구를 위해 SAN 기반 하드웨어 스냅숏을 toouse를 제거할지를 선택 합니다. (이것은 옵션 기능 toocreate hello 및 복제 toomake 분할이 기능으로 SAN을 포함 하는 경우에 쓰기 가능한 것입니다. Hello 보호 된 컴퓨터 및 백업 서버 서버가 연결 된 toohello 있어야 합니다. 또한 같은 네트워크.)

6.  알림 옵션을 설정합니다. Hello에 **확인** 페이지에서 **복구**합니다.

Windows Server 백업을 실행합니다.

1.  **작업** > **복구** > **이 서버** > **다음**을 선택합니다.

2.  선택 **다른 서버**선택, hello **위치 유형 지정** 페이지를 선택한 다음 선택 **원격 공유 폴더**합니다. Hello 복구 지점을 포함 하는 hello 경로 toohello 폴더를 입력 합니다.

3.  Hello에 **복구 유형 선택** 페이지 **시스템 상태**합니다. 

4. Hello에 **시스템 상태 복구에 대 한 위치 선택** 페이지 **원래 위치**합니다.

5.  Hello에 **확인** 페이지에서 **복구**합니다. Hello 복원 후 hello 서버를 다시 시작 합니다.

6.  또한 명령 프롬프트에서 hello 시스템 상태 복원을 실행할 수 있습니다. toodo이,이 시작 Windows Server 백업 toorecover hello 컴퓨터에 원하는 합니다. 명령 프롬프트에서 tooget hello 버전 식별자를 입력 합니다.```wbadmin get versions -backuptarget \<servername\sharename\>```

    Hello 버전 식별자 toostart hello 시스템 상태 복원을 사용 합니다. Hello 명령 프롬프트에서 다음을 입력 합니다.```wbadmin start systemstaterecovery -version:<versionidentified> -backuptarget:<servername\sharename>```

    Toostart hello 복구 있는지 확인 합니다. Hello 명령 프롬프트 창의 hello 프로세스를 볼 수 있습니다. 복원 로그가 생성됩니다. Hello 복원 후 hello 서버를 다시 시작 합니다.

