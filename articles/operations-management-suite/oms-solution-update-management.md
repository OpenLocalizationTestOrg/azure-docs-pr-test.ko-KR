---
title: "OMS의 관리 솔루션 aaaUpdate | Microsoft Docs"
description: "이 문서는 의도 한 toohelp toouse이 솔루션 toomanage 업데이트 하는 방식에 대 한 Windows 및 Linux 컴퓨터를 이해 해야 합니다."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: e33ce6f9-d9b0-4a03-b94e-8ddedcc595d2
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 2dd321913bf049ab1996fd60a2f74b8417084dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-management-solution-in-oms"></a>OMS의 업데이트 관리 솔루션

![업데이트 관리 기호](./media/oms-solution-update-management/update-management-symbol.png)

hello OMS에서 업데이트 관리 솔루션 사용 하면 toomanage 운영 체제에 보안 업데이트, Azure에 배포 된 Windows 및 Linux 컴퓨터에 대 한 온-프레미스 환경 또는 다른 클라우드 공급자입니다.  신속 하 게 모든 에이전트 컴퓨터에서 사용 가능한 업데이트의 hello 상태를 평가 하 고 hello 서버에 대 한 필수 업데이트 설치 프로세스를 관리할 수 있습니다.


## <a name="solution-overview"></a>솔루션 개요
OMS에서 관리 되는 컴퓨터는 평가 및 업데이트 배포를 수행 하기 위한 hello 다음을 사용 합니다.

* Windows 또는 Linux용 OMS 에이전트
* Linux용 PowerShell DSC(필요한 상태 구성)
* Automation Hybrid Runbook Worker
* Windows 컴퓨터용 Microsoft Update 또는 Windows Server Update Services

다음 다이어그램 hello hello 솔루션 평가 하 고 보안 업데이트 tooall 적용 하는 방법을 사용 하 여 hello 동작 및 데이터 흐름의 개념 보기에는 Windows Server 및 Linux 컴퓨터 작업 영역에서 연결 된 보여 줍니다.    

#### <a name="windows-server"></a>Windows Server
![Windows Server 업데이트 관리 프로세스 흐름](media/oms-solution-update-management/update-mgmt-windows-updateworkflow.png)

#### <a name="linux"></a>Linux
![Linux 업데이트 관리 프로세스 흐름](media/oms-solution-update-management/update-mgmt-linux-updateworkflow.png)

Hello 컴퓨터에서 업데이트 준수에 대 한 검색을 수행한 후 hello OMS 에이전트에서 대량 tooOMS hello 정보를 전달 합니다. 창 컴퓨터에서 hello 준수 검사는 기본적으로 12 시간 마다 수행 됩니다.  또한 toohello 검사 일정을 업데이트 호환성 검사 hello hello Microsoft Monitoring Agent (MMA)은 다시 시작, 이전 tooupdate 설치 하는 경우 15 분 이내 및 업데이트 설치 후 시작 됩니다.  Linux 컴퓨터와 hello 준수 검사는 기본적으로 3 시간 마다 수행 됩니다 및 hello MMA 에이전트를 다시 시작 하는 경우 15 분 이내 준수 검사가 시작 됩니다.  

hello 준수 정보를 처리 하 고 hello 솔루션 또는 검색 가능한를 사용 하 여 사용자 정의 또는 사전에 포함 된 hello 대시보드에 요약-쿼리를 정의 합니다.  hello 솔루션 보고 얼마나 최신 hello와 구성 된 toosynchronize는 소스에 기반 하는 컴퓨터입니다.  Hello Windows 컴퓨터는 WSUS 마지막과 동기화 된 경우 Microsoft 업데이트에 따라 구성 된 tooreport tooWSUS hello 결과 표시 Microsoft 업데이트에서 다를 수 있습니다.  hello Linux 컴퓨터에 대해 동일한 구성 tooreport tooa 공용 리포지토리 및 로컬 리포지토리에 있습니다.   

배포 하 고 예약 된 배포를 만들어 hello 업데이트 해야 하는 컴퓨터에서 소프트웨어 업데이트를 설치할 수 있습니다.  로 분류 된 업데이트 *Optional* 필수 업데이트에만 Windows 컴퓨터에 대 한 hello 배포 범위에 포함 되지 않습니다.  hello 예약 된 배포 정의 hello 적용 가능한 업데이트를 명시적으로 컴퓨터를 지정 하거나 선택 하 여 받을 어떤 대상 컴퓨터는 [컴퓨터 그룹](../log-analytics/log-analytics-computer-groups.md) 의 특정 집합의 로그 검색은 기반으로 하는 컴퓨터입니다.  또한 일정 tooapprove를 지정 하 고 업데이트 내에 설치 된 toobe 허용 되는 경우 일정 기간을 지정 합니다.  Azure Automation의 runbook에서 업데이트가 설치됩니다.  이러한 runbook을 볼 수 없고 구성이 필요하지 않습니다.  업데이트 배포를 만들면 시작 hello에 마스터 업데이트 runbook 지정 시간을 포함 하는 hello 컴퓨터 있는지 일정을 만듭니다.  이 마스터 runbook은 필수 업데이트를 설치하는 각 에이전트에서 하위 runbook을 시작합니다.       

Hello 날짜와 hello 업데이트 배포에 지정 된 시간에 hello 대상 컴퓨터는 hello 배포를 병렬로 실행 합니다.  검색을 첫 번째 수행된 tooverify hello 업데이트 여전히 필요 하며이 설치 합니다.  것이 중요 toonote hello 업데이트가 WSUS에 hello 업데이트 배포에서 승인 되지 않은 경우 WSUS 클라이언트 컴퓨터에 대 한 실패 합니다.  hello 결과 hello 적용 된 업데이트를 처리 하 고 hello 대시보드 또는 hello hello 이벤트를 검색 하 여 요약 tooOMS toobe를 전달 됩니다.     

## <a name="prerequisites"></a>필수 조건
* hello 솔루션 이상, 및 Windows Server 2008에 대 한 업데이트 평가 수행를 지원 하며 업데이트 배포에 대 한 Windows Server 2008 R2 SP1 이상.  Server Core 및 Nano 서버 설치 옵션은 지원되지 않습니다.

    > [!NOTE]
    > 배포 업데이트 tooWindows 서버 2008 R2 s p 1에 대 한 지원을.NET Framework 4.5 및 WMF 5.0 이상이 필요 합니다.
    >  
* Windows 클라이언트 운영 체제는 지원되지 않습니다.  
* Windows 에이전트는 Windows Server Update Services (WSUS) 서버와 구성 된 toocommunicate 이거나 액세스 tooMicrosoft 업데이트 했습니다.  

    > [!NOTE]
    > Windows 에이전트 hello 관리할 수 없습니다 동시에 System Center Configuration Manager.  
    >
* CentOS 6(x86/x64) 및 7(x64)  
* Red Hat Enterprise 6(x86/x64) 및 7(x64)  
* SUSE Linux Enterprise Server 11(x86/x64) 및 12(x64)  
* Ubuntu 12.04 LTS 및 최신 x86/x64   
    > [!NOTE]  
    > ubuntu, 유지 관리 기간 외에 적용 되 고 tooavoid 업데이트 Unattended 업그레이드 패키지 toodisable 자동 업데이트를 다시 구성 합니다. 방법에 대 한 내용은 tooconfigure이,이 참조 [hello Ubuntu Server 가이드의에서 항목을 자동 업데이트](https://help.ubuntu.com/lts/serverguide/automatic-updates.html)합니다.

* Linux 에이전트에 대 한 액세스 tooan 업데이트 리포지토리에 있어야 합니다.  

    > [!NOTE]
    > OMS 에이전트는 Linux 구성할 tooreport toomultiple OMS 작업 영역에 대 한 지원 되지 않습니다이 솔루션.  
    >

너무 tooinstall Linux 용 OMS 에이전트 hello 하 고 hello 최신 버전을 다운로드 하는 방법에 자세한 내용은 참조[Linux 용 Operations Management Suite 에이전트](https://github.com/microsoft/oms-agent-for-linux)합니다.  Tooinstall OMS 에이전트에 대 한 Windows hello 하는 방법에 대 한 내용은 검토 [Windows 용 Operations Management Suite 에이전트](../log-analytics/log-analytics-windows-agents.md)합니다.  

### <a name="permissions"></a>권한
업데이트 배포의 순서 toocreate, toobe 자동화 계정와 로그 분석 작업 영역에서 hello 참가자 역할을 부여 해야 합니다.  

## <a name="solution-components"></a>솔루션 구성 요소
이 솔루션의 hello tooyour 자동화 계정 및 직접 연결 된 에이전트 또는 Operations Manager 연결 된 관리 그룹에 추가 되는 리소스를 다음으로 구성 됩니다.

### <a name="management-packs"></a>관리 팩
System Center Operations Manager 관리 그룹에 연결 된 tooan OMS 작업 영역 이면 hello 다음 관리 팩은 Operations Manager에 설치 됩니다.  이 솔루션을 추가한 후 직접 연결된 Windows 컴퓨터에 이러한 관리 팩도 함께 설치됩니다. 더 할 게 없습니다 tooconfigure 또는 이러한 관리 팩을 사용 하 여 관리 합니다.

* Microsoft System Center Advisor 업데이트 평가 인텔리전스 팩(Microsoft.IntelligencePacks.UpdateAssessment)
* Microsoft.IntelligencePack.UpdateAssessment.Configuration(Microsoft.IntelligencePack.UpdateAssessment.Configuration)
* 업데이트 배포 MP

솔루션 관리 팩 업데이트 되는 방식에 대 한 자세한 내용은 참조 하십시오. [Operations Manager 연결 tooLog 분석](../log-analytics/log-analytics-om-agents.md)합니다.

### <a name="hybrid-worker-groups"></a>Hybrid Worker 그룹
이 솔루션을 사용 하도록 설정 하면 모든 Windows 컴퓨터 tooyour OMS 작업 영역이 자동으로이 솔루션에 포함 된 Hybrid Runbook Worker toosupport hello runbook 구성를 직접 연결 합니다.  Hello 솔루션에서 관리 하는 각 Windows 컴퓨터에 대해 그 아래에 나열 됩니다 hello 자동화 계정 hello 명명 규칙의 hello 하이브리드 Runbook 작업자 그룹 블레이드에서 *Hostname FQDN_GUID*합니다.  계정의 Runbook을 사용하여 이러한 그룹을 대상으로 지정할 수 없으며, 만약 지정하면 오류가 발생합니다. 이러한 그룹은 의도 한 toosupport hello 관리 솔루션만 합니다.   

하지만 Hello 솔루션과 하이브리드 Runbook 작업자 그룹 멤버 자격 둘 다에 동일한 계정 hello를 사용 하는 자동화 계정 toosupport 자동화 runbook에서에서 hello Windows 컴퓨터 tooa Hybrid Runbook Worker 그룹을 추가 할 수 있습니다.  이 기능은 tooversion 7.2.12024.0 hello Hybrid Runbook Worker의 추가 되었습니다.  

## <a name="configuration"></a>구성
Hello 단계 tooadd hello 업데이트 관리 솔루션 tooyour OMS 작업 영역을 다음을 수행 하 고 에이전트가 보고 합니다. Windows 에이전트 tooyour 이미 연결 된 작업 영역 추가 구성 없이 자동으로 추가 됩니다.

메서드를 다음 hello를 사용 하 여 hello 솔루션을 배포할 수 있습니다.

* Hello hello 자동화 및 제어 기능 또는 업데이트 관리 솔루션 선택 하 여 Azure 포털에서에서 Azure 마켓플레이스의
* Hello OMS 작업 영역에서 OMS 솔루션 갤러리에서

이미 있는 경우 자동화 계정 및 연결 하는 OMS 작업 영역 hello에서 동일한 리소스 그룹 및 지역, 자동화 및 제어를 선택 하면 구성을 확인 및만 hello 솔루션을 설치 되며 두 서비스에서 구성 합니다.  제공 동일한 동작을 hello Azure 마켓플레이스의 hello 업데이트 관리 솔루션 선택 합니다.  구독에 배포 된 서비스 중 하나가 없는 경우에서 다음과 같이 hello hello **새 솔루션 만들기** 블레이드 tooinstall hello 다른 미리 권장된 솔루션을 선택 하는 것이 것인지 확인 하 고 있습니다.  필요에 따라 hello 단계를 사용 하 여 OMS 작업 영역에서 설명 하는 hello 업데이트 관리 솔루션 tooyour를 추가할 수 있습니다 [추가 OMS 솔루션](../log-analytics/log-analytics-add-solutions.md) hello 솔루션 갤러리에서에서 합니다.  

### <a name="confirm-oms-agents-and-operations-manager-management-group-connected-toooms"></a>OMS 에이전트와 Operations Manager 관리 그룹 연결 tooOMS 확인

tooconfirm Linux 용 OMS 에이전트를 직접 연결을 OMS와 통신 하 고 Windows 몇 분 후 실행 하거나 로그 검색을 수행 하는 hello:

* Linux - `Type=Heartbeat OSType=Linux | top 500000 | dedup SourceComputerId | Sort Computer | display Table`.  

* Windows - `Type=Heartbeat OSType=Windows | top 500000 | dedup SourceComputerId | Sort Computer | display Table`

Windows 컴퓨터에 oms 에이전트 연결 tooverify 다음 hello를 검토할 수 있습니다.

1.  Microsoft Monitoring Agent 제어판에서 열고 hello에 **Azure 로그 분석 (OMS)** 탭, hello 에이전트 라는 메시지를 표시: **hello Microsoft Monitoring Agent toohello Microsoft 성공적으로 연결 Operations Management Suite 서비스**합니다.   
2.  Hello Windows 이벤트 로그를 열고, 너무 탐색**응용 프로그램 및 서비스 Logs\Operations 관리자** 원본 서비스 커넥터에서에서 이벤트 ID 3000 및 5002로 검색 합니다.  이러한 이벤트 hello 컴퓨터 hello OMS 작업 영역에 등록 및 구성을 수신 했음을 나타냅니다.  

Hello 에이전트가 OMS 서비스 hello로 수 toocommunicate 고 hello로 구성 된 toocommunicate는 경우 방화벽 또는 프록시 서버를 통해 인터넷 hello 방화벽 또는 프록시 서버가 검토 하 여 제대로 구성 되었는지 확인 [네트워크 Windows 에이전트에 대 한 구성을](../log-analytics/log-analytics-windows-agents.md#network) 또는 [Linux 에이전트에 대 한 네트워크 구성을](../log-analytics/log-analytics-agent-linux.md#network)합니다.

> [!NOTE]
> Linux 시스템 프록시 또는 게이트웨이 OMS로 구성 된 toocommunicate를 있으며, 사용자가 온 보 딩 하는 경우이 솔루션에서는 hello를 업데이트 하십시오 *proxy.conf* 권한 toogrant hello omiuser 그룹에 대해 읽기 권한을 hello 파일 다음 명령을 hello 수행:  
> `sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf`  
> `sudo chmod 644 /etc/opt/microsoft/omsagent/proxy.conf`


평가가 수행된 후 새로 추가된 Linux 에이전트의 상태가 **업데이트됨**으로 표시됩니다.  이 프로세스는 too6 시간 정도 걸릴 수 있습니다.

tooconfirm Operations Manager OMS와 통신 하는 관리 그룹 참조 [OMS와 함께 Operations Manager 통합의 유효성을 검사](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-oms)합니다.

## <a name="data-collection"></a>데이터 수집
### <a name="supported-agents"></a>지원되는 에이전트
다음 표에서 hello이이 솔루션에서 지원 되는 연결 된 hello 원본에 설명 합니다.

| 연결된 소스 | 지원됨 | 설명 |
| --- | --- | --- |
| Windows 에이전트 |예 |hello 솔루션 Windows 에이전트에서 시스템 업데이트에 대 한 정보를 수집 하 고 필수 업데이트의 설치를 시작 합니다. |
| Linux 에이전트 |예 |hello 솔루션 Linux 에이전트에서 시스템 업데이트에 대 한 정보를 수집 하 고 지원 되는 배포판에 필수 업데이트의 설치를 시작 합니다. |
| Operations Manager 관리 그룹 |예 |hello 솔루션 연결 된 관리 그룹의 에이전트에서 시스템 업데이트에 대 한 정보를 수집합니다.<br>Operations Manager 에이전트 tooLog hello의에서 직접 연결 분석 필요 하지 않습니다. Hello 관리 그룹 toohello OMS 리포지토리에서 데이터 전달 됩니다. |
| Azure Storage 계정 |아니요 |Azure Storage는 시스템 업데이트에 대한 정보를 포함하지 않습니다. |

### <a name="collection-frequency"></a>수집 빈도
관리되는 Windows 컴퓨터 각각의 경우 검색은 하루에 두 번 수행됩니다. 모든 15 분 hello Windows API 라고 tooquery 마지막 업데이트 시간 toodetermine hello에 대 한 상태가 변경 됨,이 경우 호환성 검사 된 경우.  관리되는 Linux 컴퓨터 각각의 경우 검색은 세 시간마다 수행됩니다.

모든 위치에서 관리 되는 컴퓨터에서 대시보드 업데이트 toodisplay 데이터 hello에 대 한 too6 시간 30 분 걸릴 수 있습니다.   

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여
Hello 업데이트 관리 솔루션 tooyour OMS 작업 영역에 추가 하면 hello **업데이트 관리** tooyour OMS 대시보드에 타일 추가 됩니다. 이 타일의 업데이트 준수 및 사용자 환경에 개수 및 그래픽으로 나타낸 hello 수의 컴퓨터를 표시합니다.<br><br>
![업데이트 관리 요약 타일](media/oms-solution-update-management/update-management-summary-tile.png)  


## <a name="viewing-update-assessments"></a>업데이트 평가 보기
Hello 클릭 **업데이트 관리** 타일 tooopen hello **업데이트 관리** 대시보드 합니다.<br><br> ![업데이트 관리 요약 대시보드](./media/oms-solution-update-management/update-management-dashboard.png)<br>

이 대시보드는 업데이트 상태를 운영 체제 및 업데이트 분류(중요, 보안 또는 기타(예: 정의 업데이트))에 따라 구체적으로 분류하여 보여 줍니다. 이 대시보드에서 각 타일에 hello 결과 배포에 대 한 바탕으로 하는 hello 컴퓨터 동기화 원본에 따라 승인 된 업데이트 된 내용만 반영 합니다.   hello **업데이트 배포** 선택 하면 바둑판식 배열, 일정, 현재 실행 중인 완료 된 배포, 배포 확인할 하거나 새 배포를 예약할 수 있는 toohello 업데이트 배포 페이지를 리디렉션합니다.  

Hello에서 사용할 수 있는 hello 목록에서 하나를 선택 합니다 특정 범주와 미리 정의 된 기준 쿼리 hello 특정 타일 또는 toorun에서 클릭 하 여 모든 레코드를 반환 하는 로그 검색을 실행할 수 **일반적인 업데이트 쿼리** 열입니다.    

## <a name="installing-updates"></a>업데이트 설치
있습니다 수를 만들어 설치 된 업데이트가 필요한 모든 작업 영역에서 Windows 컴퓨터 및 Linux hello에 대 한 업데이트를 평가한 후는 *업데이트 배포*합니다.  업데이트 배포는 하나 이상의 컴퓨터에 필수 업데이트를 예약하여 설치합니다.  Hello 날짜를 지정 하 고 hello 배포용에 시간 tooa 컴퓨터 또는 배포의 hello 범위에 포함 해야 하는 컴퓨터의 그룹입니다.  컴퓨터 그룹에 대해 자세히 toolearn 참조 [로그 분석에서 컴퓨터 그룹](../log-analytics/log-analytics-computer-groups.md)합니다.  업데이트 배포에 컴퓨터 그룹을 포함 하는 경우 그룹 memnbership hello 일정 생성 시 한 번만 계산 됩니다.  후속 변경 tooa 그룹 반영 되지 않습니다.  이 문제를 해결 toowork는 hello 예약 된 업데이트 배포를 삭제 하 고 다시 합니다.

> [!NOTE]
> Windows Vm에서 기본적으로 Azure 마켓플레이스 설정 tooreceive 자동 업데이트에서 Windows Update 서비스는 hello 배포 합니다.  이 문제는이 솔루션 또는 Windows Vm tooyour 작업 영역을 추가한 후 변경 되지 않습니다.  이 솔루션을 사용 하 여 적극적으로 관리 되는 업데이트를 수행 하는 경우 기본 동작을 hello (자동으로 업데이트 적용 됨) 적용 됩니다.  

이미지에서 만든 hello 주문형 Red Hat Enterprise Linux (RHEL) 사용할 수 있는 Azure Marketplace에서의 가상 컴퓨터에는 등록 된 tooaccess hello [Red Hat 업데이트 인프라 (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md) Azure에 배포 합니다.  다른 Linux 배포판의 지원 되는 방법에 따라 hello 배포판 온라인 파일 저장소에서 업데이트 되어야 합니다.  

### <a name="viewing-update-deployments"></a>업데이트 배포 보기
Hello 클릭 **업데이트 배포** 기존 업데이트 배포의 타일 tooview hello 목록입니다.  **예약됨**, **실행 중** 및 **완료됨**와 같은 상태별로 그룹화합니다.<br><br> ![업데이트 배포 일정 페이지](./media/oms-solution-update-management/update-updatedeployment-schedule-page.png)<br>  

다음 표에 hello 각 업데이트 배포에 대해 표시 되는 hello 속성을 설명 합니다.

| 속성 | 설명 |
| --- | --- |
| 이름 |Hello 업데이트 배포의 이름입니다. |
| 일정 |일정의 형식입니다.  사용 가능한 옵션은 *한 번*, *매주 되풀이* 또는 *월별 되풀이*입니다. |
| 시작 시간 |업데이트 배포 hello 날짜 및 시간에 예약 된 toostart입니다. |
| 기간 |분 hello 업데이트 배포 수가 toorun을 허용 됩니다.  Hello 남은 업데이트 될 때까지 기다려야 합니다. 그런 다음이 기간 내에서 모든 업데이트가 설치 되지 않은 경우 hello 다음 업데이트를 배포 합니다. |
| 서버 |Hello 업데이트 배포에 영향을 받는 컴퓨터의 수입니다.  |
| 가동 상태 |Hello 업데이트 배포의 현재 상태입니다.<br><br>가능한 값은 다음과 같습니다.<br>- 시작 안함<br>- 실행 중<br>- 완료됨 |

다음 표에 hello에 hello 열을 포함 하는 완료 된 업데이트 배포 tooview hello 세부 정보 화면을 선택 합니다.  이러한 열은 hello 업데이트 배포 하지 않은 경우 채워집니다 아직 시작 되지 않았습니다.<br><br> ![업데이트 배포 결과의 개요](./media/oms-solution-update-management/update-management-deploymentresults-dashboard.png)

| 열 | 설명 |
| --- | --- |
| **컴퓨터 보기** | |
| Windows 컴퓨터 |Hello hello 업데이트 배포 상태에 의해의 Windows 컴퓨터 수를 나열합니다.  상태 toorun 반환 레코드 hello 업데이트 배포에 대 한 해당 상태를 업데이트 하는 모든 로그 검색을 클릭 합니다. |
| Linux 컴퓨터 |업데이트 배포 상태에 의해 hello에 Linux 컴퓨터의 hello 수를 나열합니다.  상태 toorun 반환 레코드 hello 업데이트 배포에 대 한 해당 상태를 업데이트 하는 모든 로그 검색을 클릭 합니다. |
| 컴퓨터 설치 상태 |Hello 업데이트 배포에에서 포함 된 hello 컴퓨터 및 성공적으로 설치 된 업데이트의 hello 백분율을 나열 합니다. 모든 누락 및 중요 업데이트를 반환 하는 로그 검색 hello 항목 toorun 중 하나를 클릭 합니다. |
| **업데이트 보기** | |
| Windows 업데이트 |Hello 업데이트 배포 및 각 업데이트 마다 해당 설치 상태에 포함 된 Windows 업데이트를 나열 합니다.  업데이트 toorun 모든 해당 특정 업데이트에 대 한 레코드를 업데이트 하거나 클릭 하 여 hello 상태 toorun hello 배포에 대 한 레코드를 업데이트 하는 모든 반환 된 로그 검색을 반환 하는 로그 검색을 선택 합니다. |
| Linux 업데이트 |Hello 업데이트 배포 및 각 업데이트 마다 해당 설치 상태에 포함 된 Linux 업데이트를 나열 합니다.  업데이트 toorun 모든 해당 특정 업데이트에 대 한 레코드를 업데이트 하거나 클릭 하 여 hello 상태 toorun hello 배포에 대 한 레코드를 업데이트 하는 모든 반환 된 로그 검색을 반환 하는 로그 검색을 선택 합니다. |

### <a name="creating-an-update-deployment"></a>업데이트 배포 만들기
Hello를 클릭 하 여 새 업데이트 배포를 만들고 **추가** hello 화면 tooopen hello hello 위쪽에 단추 **새 업데이트 배포** 페이지.  다음 표에 hello에 hello 속성에 대 한 값을 제공 해야 합니다.

| 속성 | 설명 |
| --- | --- |
| 이름 |고유한 이름 tooidentify hello 업데이트 배포 합니다. |
| 표준 시간대 |Hello 시작 시간에 대 한 표준 시간대 toouse 합니다. |
| 일정 형식 | 일정의 형식입니다.  사용 가능한 옵션은 *한 번*, *매주 되풀이* 또는 *월별 되풀이*입니다.  
| 시작 시간 |날짜 및 시간 toostart hello 업데이트 배포 합니다. **참고:** 즉시 toodeploy 사용 해야 할 경우 배포를 실행할 수 곧을 hello는 현재 시간에서 30 분입니다. |
| 기간 |분 hello 업데이트 배포 수가 toorun을 허용 됩니다.  Hello 남은 업데이트 될 때까지 기다려야 합니다. 그런 다음이 기간 내에서 모든 업데이트가 설치 되지 않은 경우 hello 다음 업데이트를 배포 합니다. |
| 컴퓨터 |컴퓨터 또는 컴퓨터 그룹 tooinclude 및 hello 업데이트 배포의에서 대상의 이름입니다.  Hello 드롭 다운 목록에서에서 하나 이상의 항목을 선택 합니다. |

<br><br> ![새 업데이트 배포 페이지](./media/oms-solution-update-management/update-newupdaterun-page.png)

### <a name="time-range"></a>시간 범위
Hello 업데이트 관리 솔루션에에서 분석 된 hello 데이터 hello 범위는 기본적으로 지난 1 일 hello 내에서 생성 된 모든 연결 된 관리 그룹에서 합니다.

hello 데이터의 toochange hello 시간 범위 선택 **데이터를 기반으로** hello hello 대시보드 위쪽에 있습니다. 레코드 생성 또는 6 시간 또는 1 일, 지난 7 일 hello 내에서 업데이트를 선택할 수 있습니다. 또는 **사용자 지정**을 선택하고 사용자 지정 날짜 범위를 지정할 수 있습니다.

## <a name="log-analytics-records"></a>Log Analytics 레코드
업데이트 관리 솔루션 hello hello OMS 리포지토리에 두 종류의 레코드를 만듭니다.

### <a name="update-records"></a>업데이트 레코드
**업데이트**라는 형식의 레코드가 각 컴퓨터에 설치되었거나 필요한 각 업데이트에 만들어집니다. 레코드 업데이트는 다음 표에 hello에 hello 속성이 있습니다.

| 속성 | 설명 |
| --- | --- |
| 형식 |*업데이트* |
| SourceSystem |hello 업데이트의 설치를 승인 하는 hello 소스입니다.<br>가능한 값은 다음과 같습니다.<br>- Microsoft 업데이트<br>- Windows 업데이트<br>- SCCM<br>- Linux 서버(패키지 관리자에서 가져옴) |
| 승인됨 |설치에 대 한 hello 업데이트를 승인 되었는지 여부를 지정 합니다.<br> Linux 서버의 경우 패치가 OMS에서 관리되지 않기 때문에 현재 선택 사항입니다. |
| Windows용 분류 |Hello 업데이트의 분류 합니다.<br>가능한 값은 다음과 같습니다.<br>- 응용 프로그램<br>- 중요 업데이트<br>- 정의 업데이트<br>- 기능 팩<br>- 보안 업데이트<br>- 서비스 팩<br>- 업데이트 롤업<br>- 업데이트 |
| Linux용 분류 |Cassification hello 업데이트 합니다.<br>가능한 값은 다음과 같습니다.<br>- 중요 업데이트<br>- 보안 업데이트<br>- 기타 업데이트 |
| 컴퓨터 |Hello 컴퓨터 이름입니다. |
| InstallTimeAvailable |에이전트가 설치 hello 동일 hello 설치 시간을 다른에서 사용할 수 있는지 여부를 지정 합니다. 업데이트 합니다. |
| InstallTimePredictionSeconds |예상 설치 시간 (초)을 기반으로 다른 설치 에이전트 hello 동일한 업데이트 합니다. |
| KBID |Hello 업데이트를 설명 하는 hello KB 문서 ID입니다. |
| ManagementGroupName |SCOM 에이전트에 대 한 hello 관리 그룹의 이름입니다.  다른 에이전트의 경우 AOI-<workspace ID>입니다. |
| MSRCBulletinID |Hello 업데이트를 설명 하는 hello Microsoft 보안 게시판의 ID입니다. |
| MSRCSeverity |Hello Microsoft 보안 게시판의 심각도입니다.<br>가능한 값은 다음과 같습니다.<br>- 중요<br>- 중요<br>- 보통 |
| 옵션 |Hello 업데이트는 선택 사항 있는지 여부를 지정 합니다. |
| 제품 |Hello 제품 hello 업데이트의 이름이입니다.  클릭 **보기** 브라우저에서 tooopen hello 문서입니다. |
| PackageSeverity |hello Linux 배포판 공급 업체에서 보고 한 대로이 업데이트에서 수정 된 hello 취약점의 hello 심각도입니다. |
| PublishDate |날짜 및 시간을 업데이트 hello 설치 되었습니다. |
| RebootBehavior |Hello 업데이트 하는 경우 다시 부팅 하면를 지정 합니다.<br>가능한 값은 다음과 같습니다.<br>- canrequestreboot<br>- neverreboots |
| RevisionNumber |Hello 업데이트의 수정 번호입니다. |
| SourceComputerId |GUID toouniquely hello 컴퓨터를 식별 합니다. |
| TimeGenerated |날짜 및 시간을 레코드 hello를 마지막으로 업데이트 합니다. |
| 제목 |Hello 업데이트의 제목입니다. |
| UpdateID |GUID toouniquely hello 업데이트를 식별 합니다. |
| UpdateState |이 컴퓨터에 hello 업데이트가 설치 되었는지 여부를 지정 합니다.<br>가능한 값은 다음과 같습니다.<br>설치 된-hello 업데이트는이 컴퓨터에 설치 됩니다.<br>필요한-hello 업데이트 설치 되지 않은 하 고이 컴퓨터에 필요 합니다. |

형식의 레코드를 반환 하는 모든 로그 검색을 수행 하는 경우 **업데이트** hello를 선택할 수 있습니다 **업데이트** hello 검색에서 반환 된 hello 업데이트 요약 타일의 집합을 표시 하는 보기입니다. Hello의 hello 항목을 클릭할 수 **Missing 및 적용 된 업데이트** 및 **필수 및 선택적 업데이트** tooscope hello 보기 toothat 업데이트 집합이 바둑판식으로 표시 합니다. 선택 hello **목록** 또는 **테이블** tooreturn hello 개별 레코드를 확인 합니다.<br>

![레코드 형식 업데이트로 로그 검색 업데이트 보기](./media/oms-solution-update-management/update-la-view-updates.png)  

Hello에 **테이블** 뷰를 클릭할 때 hello **KBID** 모든 레코드 tooopen hello KB 문서를 사용 하 여 브라우저에 대 한 합니다. 이렇게 하면 있습니다 tooquickly hello 특정 업데이트의 hello 세부 정보에 대해 알아보세요.<br>

![타일 레코드 형식 업데이트로 로그 검색 테이블 보기](./media/oms-solution-update-management/update-la-view-table.png)

Hello에 **목록** 보기 hello 클릭 **보기** 링크 다음 toohello KBID tooopen hello KB 문서.<br>

![타일 레코드 형식 업데이트로 로그 검색 목록 보기](./media/oms-solution-update-management/update-la-view-list.png)

### <a name="updatesummary-records"></a>UpdateSummary 레코드
형식이 **UpdateSummary**인 레코드가 각 Windows 에이전트 컴퓨터에 만들어집니다. 이 레코드는 업데이트에 대 한 hello 컴퓨터를 검색 될 때마다 업데이트 됩니다. **UpdateSummary** 레코드는 다음 표에 hello의 hello 속성을 가져야 합니다.

| 속성 | 설명 |
| --- | --- |
| 형식 |UpdateSummary |
| SourceSystem |OpsManager |
| 컴퓨터 |Hello 컴퓨터 이름입니다. |
| CriticalUpdatesMissing |Hello 컴퓨터에 없기 때문에 중요 한 업데이트 수입니다. |
| ManagementGroupName |SCOM 에이전트에 대 한 hello 관리 그룹의 이름입니다. 다른 에이전트의 경우 AOI-<workspace ID>입니다. |
| NETRuntimeVersion |Hello 컴퓨터에 설치 된 hello.NET 런타임 버전입니다. |
| OldestMissingSecurityUpdateBucket |버킷 toocategorize hello 시간 hello 가장 오래 된 누락 된이 컴퓨터에서 보안 업데이트가 게시 되었기 때문입니다.<br>가능한 값은 다음과 같습니다.<br>- 이전<br>- 180일 전<br>- 150일 전<br>- 120일 전<br>- 90일 전<br>- 60일 전<br>- 30일 전<br>- 최근 |
| OldestMissingSecurityUpdateInDays |Hello 가장 오래 된 보안 업데이트 누락이 컴퓨터에 게시 된 후의 일 수입니다. |
| OsVersion |Hello 컴퓨터에 설치 된 hello 운영 체제의 버전입니다. |
| OtherUpdatesMissing |Hello 컴퓨터에 없기 때문에 다른 업데이트 수입니다. |
| SecurityUpdatesMissing |Hello 컴퓨터에 없기 때문에 보안 업데이트의 수입니다. |
| SourceComputerId |GUID toouniquely hello 컴퓨터를 식별 합니다. |
| TimeGenerated |날짜 및 시간을 레코드 hello를 마지막으로 업데이트 합니다. |
| TotalUpdatesMissing |Hello 컴퓨터에서 누락 된 업데이트의 총 수입니다. |
| WindowsUpdateAgentVersion |Hello 컴퓨터에서 hello Windows Update 에이전트 버전 번호입니다. |
| WindowsUpdateSetting |Hello 컴퓨터가 중요 한 업데이트를 설치 하는 방법에 대 한 설정입니다.<br>가능한 값은 다음과 같습니다.<br>- 사용 안 함<br>- 설치하기 전에 알림<br>- 예약된 설치 |
| WSUSServer |URL의 WSUS 서버 hello 컴퓨터가 경우 toouse 하나를 구성 합니다. |

## <a name="sample-log-searches"></a>샘플 로그 검색
다음 표에서 hello이이 솔루션에 의해 수집 된 레코드 업데이트에 대 한 예제 로그 검색을 제공 합니다.

| 쿼리 | 설명 |
| --- | --- |
| Type:Update OSType!=Linux UpdateState=Needed Optional=false Approved!=false &#124; measure count() by Computer |업데이트가 필요한 Windows 기반 서버 컴퓨터 |
| Type:Update OSType=Linux UpdateState!="Not needed" &#124; measure count() by Computer |업데이트가 필요한 Linux 서버 | 
| Type=Update UpdateState=Needed Optional=false &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |업데이트가 누락된 모든 컴퓨터 |
| Type=Update UpdateState=Needed Optional=false Computer="COMPUTER01.contoso.com" &#124; select Computer,Title,KBID,Product,UpdateSeverity,PublishedDate |특정 컴퓨터의 누락된 업데이트(값을 사용자 고유의 컴퓨터 이름으로 대체)|
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") |중요 또는 보안 업데이트가 누락된 모든 컴퓨터 | 
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual &#124; Distinct Computer} &#124; Distinct KBID |업데이트가 수동으로 적용된 컴퓨터에 필요한 중요 또는 보안 업데이트 |
| Type=Event EventLevelName=error Computer IN {Type=Update (Classification="Security Updates" OR Classification="Critical Updates") UpdateState=Needed Optional=false &#124; Distinct Computer} |중요 또는 보안 필수 업데이트가 누락된 컴퓨터의 오류 이벤트 |
| Type=Update Optional=false Classification="Update Rollups" UpdateState=Needed &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |업데이트 롤업이 누락된 모든 컴퓨터 | 
| Type=Update UpdateState=Needed Optional=false &#124; Distinct Title |모든 컴퓨터에 누락된 업데이트 구분 | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Title, UpdateRunName |업데이트 실행에 실패한 업데이트가 있는 Windows 기반 서버 컴퓨터 | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Product, UpdateRunName |업데이트 실행에 실패한 업데이트가 있는 Linux 서버 | 
| Type=UpdateSummary &#124; measure count() by WSUSServer |WSUS 컴퓨터 멤버 자격 | 
| Type=UpdateSummary &#124; measure count() by WindowsUpdateSetting |자동 업데이트 구성 | 
| Type=UpdateSummary WindowsUpdateSetting=Manual |자동 업데이트를 사용하지 않는 컴퓨터 | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" &#124; measure count() by Computer |사용 가능한 패키지 업데이트가 포함 하는 모든 hello Linux 컴퓨터의 목록 | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") &#124; measure count() by Computer |중요 또는 보안 취약점을 해결 하는 패키지 업데이트를 사용할 수 있는 모든 hello Linux 컴퓨터의 목록 | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" |사용 가능한 업데이트가 있는 모든 패키지 목록 | 
| Type=Update  and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") |중요 또는 보안 취약점을 해결하는 업데이트를 사용할 수 있는 모든 패키지 목록 | 
| Type:UpdateRunProgress &#124; measure Count() by UpdateRunName |컴퓨터를 수정한 업데이트 배포 나열 | 
| Type:UpdateRunProgress UpdateRunName="DeploymentName" &#124; measure Count() by Computer |이 업데이트 실행에서 업데이트된 컴퓨터(값을 사용자의 업데이트 배포 이름으로 대체) | 
| Type=Update and OSType=Linux and OSName = Ubuntu &#124; measure count() by Computer |사용 가능한 모든 업데이트와 함께 모든 hello "Ubuntu" 컴퓨터의 목록 | 

## <a name="troubleshooting"></a>문제 해결

이 섹션에서는 toohelp hello 업데이트 관리 솔루션으로 문제 해결 정보를 제공 합니다.  

### <a name="how-do-i-troubleshoot-onboarding-issues"></a>온보딩 문제를 해결하려면 어떻게 할까요?
가상 컴퓨터 또는 tooonboard hello 솔루션을 시도 하는 동안 문제가 발생 하면 확인 hello **응용 프로그램 및 서비스 Logs\Operations 관리자** 포함된이벤트ID4502및이벤트메시지와이벤트에대한이벤트로그**Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**합니다.  다음 표에서 hello 각각에 대 한 특정 오류 메시지 및 가능한 해결을 강조 표시 합니다.  

| Message | 이유 | 해결 방법 |   
|----------|----------|----------|  
| 패치 관리를 위해 컴퓨터 tooRegister를 수 없습니다.<br>예외와 함께 등록이 실패했습니다.<br>System.InvalidOperationException: {"메시지":"컴퓨터가 이미<br>tooa 다른 계정을 등록 합니다. "} | 컴퓨터는 이미 업데이트 관리를 위한 등록 된 tooanother 작업 영역 | 정리 하 여 기존 아티팩트 [hello 하이브리드 runbook 그룹 삭제](../automation/automation-hybrid-runbook-worker.md#remove-hybrid-worker-groups)|  
| 없습니다 너무 등록 패치 관리를 위해 컴퓨터<br>예외와 함께 등록이 실패했습니다.<br>System.Net.Http.HttpRequestException: hello 요청을 보내는 동안 오류가 발생 했습니다. ---><br>System.Net.WebException: hello에 대 한 기본 연결<br>닫혔습니다. 받는 동안<br>예기치 않은 오류가 발생했습니다. ---> System.ComponentModel.Win32Exception:<br>hello 클라이언트와 서버 통신할 수 없습니다.<br>서로 통신할 수 없습니다. | 프록시/게이트웨이/방화벽이 통신을 차단합니다. | [네트워크 요구 사항을 검토합니다.](../automation/automation-offering-get-started.md#network-planning)|  
| 패치 관리를 위해 컴퓨터 tooRegister를 수 없습니다.<br>예외와 함께 등록이 실패했습니다.<br>Newtonsoft.Json.JsonReaderException: 양의 무한대 값을 구문 분석하는 도중에 오류가 발생했습니다. | 프록시/게이트웨이/방화벽이 통신을 차단합니다. | [네트워크 요구 사항을 검토합니다.](../automation/automation-offering-get-started.md#network-planning)| 
| hello 서비스에서 제공 하는 hello 인증서 <wsid>. oms.opinsights.azure.com<br>Microsoft 서비스에 사용된 인증서 기관에서<br>발급한 것이 아닙니다. 네트워크<br>네트워크 관리자 toosee 차단 하는 프록시를 실행 하는 경우<br>TLS/SSL 통신을 가로채는 프록시를 실행 중인지 확인합니다. |프록시/게이트웨이/방화벽이 통신을 차단합니다. | [네트워크 요구 사항을 검토합니다.](../automation/automation-offering-get-started.md#network-planning)|  
| 패치 관리를 위해 컴퓨터 tooRegister를 수 없습니다.<br>예외와 함께 등록이 실패했습니다.<br>AgentService.HybridRegistration.<br>PowerShell.Certificates.CertificateCreationException:<br>Toocreate 자체 서명 된 인증서에 실패 했습니다. ---><br>System.UnauthorizedAccessException: 액세스가 거부되었습니다. | 자체 서명된 인증서 생성 오류 | 시스템 계정에<br>읽기 액세스 toofolder:<br>**C:\ProgramData\Microsoft\**<br>**Crypto\RSA**|  

### <a name="how-do-i-troubleshoot-update-deployments"></a>업데이트 배포를 문제를 해결하려면 어떻게 해야 하나요?
이 솔루션을 지 원하는 hello OMS 작업 영역과 연결 된 자동화 계정 hello 작업 블레이드에서 hello 예약 된 업데이트 배포에 포함 된 hello 업데이트 배포를 담당 하는 hello runbook의 hello 결과 볼 수 있습니다.  runbook hello **패치 MicrosoftOMSComputer** 특정 관리 되는 컴퓨터를 대상으로 하는 자식 runbook 이며 hello verbose Stream 검토 해당 배포에 대 한 자세한 정보를 표시 합니다.  hello 출력 필요한 업데이트를 적용 가능한 표시, 상태, 설치 상태 및 추가 세부 정보를 다운로드 합니다.<br><br> ![배포 작업 상태 업데이트](media/oms-solution-update-management/update-la-patchrunbook-outputstream.png)<br>

자세한 내용은 [Automation Runbook 출력 및 메시지](../automation/automation-runbook-output-and-messages.md)를 참조하세요.   

## <a name="next-steps"></a>다음 단계
* 로그 검색을 사용 하 여 [로그 분석](../log-analytics/log-analytics-log-searches.md) tooview 업데이트 데이터를 자세히 설명 합니다.
* 관리되는 컴퓨터에 대한 업데이트 준수를 표시하는 [고유한 대시보드 만들기](../log-analytics/log-analytics-dashboards.md)
* 중요 업데이트가 컴퓨터에서 누락된 것으로 검색되거나 컴퓨터가 자동 업데이트를 사용하지 않도록 설정한 경우 [경고 만들기](../log-analytics/log-analytics-alerts.md)  
