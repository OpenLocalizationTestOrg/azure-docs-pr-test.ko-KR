---
title: "Azure Backup 오류 문제 해결: 게스트 에이전트 상태 사용할 수 없음 | Microsoft Docs"
description: "증상, 원인 및 해결책의 Azure 백업 오류 관련된 tooerror: hello VM 에이전트와 통신할 수 없습니다"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
keywords: "Azure 백업; VM 에이전트; 네트워크 연결;"
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: genli;markgal;
ms.openlocfilehash: 724c61ba80d0a9ef91a5f8543ae72bb86968881b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Azure Backup 오류 문제 해결: 에이전트 및/또는 확장 관련 문제

이 문서에서는 백업 실패를 해결 하는 문제 해결 단계 toohelp 관련 tooproblems 통신할 때 VM 에이전트 및 확장에서에서 제공 합니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-toocommunicate-with-azure-backup"></a>Azure 백업에 없습니다 toocommunicate VM 에이전트
등록 하 고 hello Azure 백업 서비스에 대 한 VM 예약 후 백업 VM 에이전트 tootake 지정 시간에 스냅숏으로 hello와 통신 하 여 hello 작업을 시작 합니다. Hello 다음 조건 중 하나를 차례로 tooBackup 오류가 발생할 수 있습니다, 트리거된에서 hello 스냅숏을 방지할 수 있습니다. 아래 문제 해결 hello 순서에 단계를 수행 하 고 작업을 다시 시도 합니다.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>원인 1: [hello VM에 인터넷 액세스가 없는](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>원인 2: [hello 에이전트 hello VM에에서 설치 되어 있지만 (Windows Vm)에 대 한 응답 하지 않습니다](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>원인 3: [hello VM에에서 설치 된 hello agent (Linux Vm)에 대 한 최신이 아닙니다](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>원인 4: [hello 스냅숏 상태를 검색할 수 없습니다 또는 스냅숏을 만들 수 없습니다.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>원인 5: [hello 예비 내선 번호 tooupdate 또는 로드 실패](#the-backup-extension-fails-to-update-or-load)

## <a name="snapshot-operation-failed-due-toono-network-connectivity-on-hello-virtual-machine"></a>Hello 가상 컴퓨터에서 네트워크 연결 toono 인해 스냅숏 작업이 실패 했습니다.
등록 하 고 hello Azure 백업 서비스에 대 한 VM 예약 후 백업 hello VM 예비 내선 번호에-시간 tootake 스냅숏와 통신 하 여 hello 작업을 시작 합니다. Hello 다음 조건 중 하나를 차례로 tooBackup 오류가 발생할 수 있습니다, 트리거된에서 hello 스냅숏을 방지할 수 있습니다. 아래 문제 해결 hello 순서에 단계를 수행 하 고 작업을 다시 시도 합니다.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>원인 1: [hello VM에 인터넷 액세스가 없는](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>원인 2: [hello 스냅숏 상태를 검색할 수 없습니다 또는 스냅숏을 만들 수 없습니다.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>원인 3: [hello 예비 내선 번호 tooupdate 또는 로드 실패](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>VMSnapshot 확장 작업이 실패했습니다.

등록 하 고 hello Azure 백업 서비스에 대 한 VM 예약 후 백업 hello VM 예비 내선 번호에-시간 tootake 스냅숏와 통신 하 여 hello 작업을 시작 합니다. Hello 다음 조건 중 하나를 차례로 tooBackup 오류가 발생할 수 있습니다, 트리거된에서 hello 스냅숏을 방지할 수 있습니다. 아래 문제 해결 hello 순서에 단계를 수행 하 고 작업을 다시 시도 합니다.
##### <a name="cause-1-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>원인 1: [hello 스냅숏 상태를 검색할 수 없습니다 또는 스냅숏을 만들 수 없습니다.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>원인 2: [hello 예비 내선 번호 tooupdate 또는 로드 실패](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>원인 3: [hello VM에 인터넷 액세스가 없는](#the-vm-has-no-internet-access)
##### <a name="cause-4-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>원인 4: [hello 에이전트 hello VM에에서 설치 되어 있지만 (Windows Vm)에 대 한 응답 하지 않습니다](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>원인 5: [hello VM에에서 설치 된 hello agent (Linux Vm)에 대 한 최신이 아닙니다](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-tooperform-hello-operation-as-hello-vm-agent-is-not-responsive"></a>VM 에이전트 hello로 수 없습니다 tooperform hello 작업이 응답 하지 않습니다.

등록 하 고 hello Azure 백업 서비스에 대 한 VM 예약 후 백업 hello VM 예비 내선 번호에-시간 tootake 스냅숏와 통신 하 여 hello 작업을 시작 합니다. Hello 다음 조건 중 하나를 차례로 tooBackup 오류가 발생할 수 있습니다, 트리거된에서 hello 스냅숏을 방지할 수 있습니다. 아래 문제 해결 hello 순서에 단계를 수행 하 고 작업을 다시 시도 합니다.
##### <a name="cause-1-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>원인 1: [hello 에이전트 hello VM에에서 설치 되어 있지만 (Windows Vm)에 대 한 응답 하지 않습니다](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>원인 2: [hello VM에에서 설치 된 hello agent (Linux Vm)에 대 한 최신이 아닙니다](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>원인 3: [hello VM에 인터넷 액세스가 없는](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-hello-operation-in-a-few-minutes"></a>내부 오류로 인해 백업이 실패-hello 작업을 잠시 후에 다시 시도 하십시오

등록 하 고 hello Azure 백업 서비스에 대 한 VM 예약 후 백업 hello VM 예비 내선 번호에-시간 tootake 스냅숏와 통신 하 여 hello 작업을 시작 합니다. Hello 다음 조건 중 하나를 차례로 tooBackup 오류가 발생할 수 있습니다, 트리거된에서 hello 스냅숏을 방지할 수 있습니다. 아래 문제 해결 hello 순서에 단계를 수행 하 고 작업을 다시 시도 합니다.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>원인 1: [hello VM에 인터넷 액세스가 없는](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>원인 2: [hello 에이전트 (Windows Vm)에 대 한 응답 하지 않는 있지만 hello VM에 설치 합니다.](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>원인 3: [hello VM에에서 설치 된 hello agent (Linux Vm)에 대 한 최신이 아닙니다](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>원인 4: [hello 스냅숏 상태를 검색할 수 없습니다 또는 스냅숏을 만들 수 없습니다.](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>원인 5: [hello 예비 내선 번호 tooupdate 또는 로드 실패](#the-backup-extension-fails-to-update-or-load)


## <a name="causes-and-solutions"></a>원인 및 해결 방법

### <a name="hello-vm-has-no-internet-access"></a>hello VM에 인터넷 권한 없음
Hello 배포 요구 사항 마다 hello VM에 인터넷 액세스가 없는 있거나 액세스 toohello Azure 인프라를 금지 하는 위치에 대 한 제한을 합니다.

toofunction hello 백업 확장 해야 올바르게 연결 toohello Azure 공용 IP 주소입니다. hello 확장 hello VM의 tooan Azure 저장소 끝점 (HTTP URL) toomanage hello 스냅숏 명령을 보냅니다. Hello 확장의 공용 인터넷을 결국 백업 실패 액세스 toohello 없습니다.

####  <a name="solution"></a>해결 방법
tooresolve hello 문제, 여기에 나열 된 hello 방법 중 하나를 시도 합니다.
##### <a name="allow-access-toohello-azure-datacenter-ip-ranges"></a>Toohello Azure 데이터 센터 IP 범위 액세스를 허용 합니다.

1. Hello 가져올 [Azure 데이터 센터 Ip 목록](https://www.microsoft.com/download/details.aspx?id=41653) tooallow에 대 한 액세스.
2. Hello를 실행 하 여 hello Ip 차단 해제 **새로 NetRoute** hello 관리자 권한 PowerShell 창에서 Azure VM에에서 대 한 cmdlet입니다. 관리자 권한으로 hello cmdlet을 실행 합니다.
3. tooallow 액세스 toohello ip 주소로 있는 경우 규칙 toohello 네트워크 보안 그룹을 추가 합니다.

##### <a name="create-a-path-for-http-traffic-tooflow"></a>HTTP 트래픽 tooflow에 대 한 경로 만들기

1. 위치 (예를 들어 네트워크 보안 그룹)에 네트워크 제한이 HTTP 프록시 서버 tooroute hello 트래픽을 배포 합니다.
2. hello HTTP 프록시 서버에서 tooallow 액세스 toohello 인터넷이 있는 경우 규칙 toohello 네트워크 보안 그룹을 추가 합니다.

tooset VM 백업에 대 한 HTTP 프록시를 확인 하려면 어떻게 해야 toolearn [Azure 가상 컴퓨터를 사용자 환경 tooback 준비](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups)합니다.

관리 하는 디스크를 사용 하는 경우에 추가 포트 (8443)를 여는 hello 방화벽에서 할 수 있습니다.

### <a name="hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vms"></a>(Windows Vm)에 대 한 응답 하지 않는 있지만 hello VM에에서 설치 된 hello 에이전트

#### <a name="solution"></a>해결 방법
VM 에이전트 hello 손상 되었거나 hello 서비스가 중지 되었습니다. Hello VM 에이전트를 다시 설치 도움이 hello 최신 버전을 가져오고 hello 통신을 다시 시작 됩니다.

1. 확인의 서비스 (services.msc)에서 실행 되는 Windows 게스트 에이전트 서비스에 가상 컴퓨터 hello 여부. Hello Windows 게스트 에이전트 서비스를 다시 시작 하 고 hello 백업 시작<br>
2. 서비스에서 확인할 수 없는 경우 프로그램 및 기능에서 Windows 게스트 에이전트 서비스가 설치되었는지 여부를 확인합니다.
4. 프로그램 및 기능 제거 hello Windows 게스트 에이전트의에서 수 tooview 경우.
5. 다운로드 및 설치 hello [최신 버전의 에이전트 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. 관리자 권한 toocomplete hello 설치를 해야합니다.
6. 그런 다음 수 tooview Windows 게스트 에이전트 서비스의 서비스에 있어야
7. Hello 포털에서 "백업" 지금 "을 클릭 하 여에-필요 시/임시 백업을 실행 해 보십시오.

또한 가상 컴퓨터에 확인  **[hello 시스템에 설치 된.NET 4.5](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**합니다. Hello 서비스와 VM 에이전트 toocommunicate hello에 필요

### <a name="hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vms"></a>hello VM에에서 설치 된 hello agent (Linux Vm)에 대 한 최신이 아닙니다.

#### <a name="solution"></a>해결 방법
Linux VM에 대부분의 에이전트 관련 또는 확장 관련 오류는 이전 VM 에이전트에 영향을 주는 문제로 인해 발생합니다. tootroubleshoot이 문제를 다음 일반 지침을 따릅니다.

1. 에 대 한 hello 지침 [hello Linux VM 에이전트를 업데이트](../virtual-machines/linux/update-agent.md)합니다.

 >[!NOTE]
 >म *강력히 권장* 배포 리포지토리를 사용할 때만 hello 에이전트를 업데이트 합니다. GitHub에서 직접 hello 에이전트 코드를 다운로드 및 업데이트 하는 것은 좋지 않습니다. Hello 최신 에이전트 배포에 필요한 사용할 수 없는 경우 방법에 대 한 배포 지원에 문의 tooinstall 것입니다. 이동 toohello hello 가장 최근의 에이전트에 대 한 toocheck [Windows Azure Linux 에이전트](https://github.com/Azure/WALinuxAgent/releases) hello GitHub 리포지토리에 페이지입니다.

2. Hello 다음 명령을 실행 하 여 해당 hello Azure 에이전트 hello VM에서 실행 중인지 확인:`ps -e`

 Hello 프로세스를 실행 하지 않는 경우 다음 명령을 hello를 사용 하 여 다시 시작 합니다.

 * Ubuntu의 경우: `service walinuxagent start`
 * 기타 배포의 경우: `service waagent start`

3. [Hello 자동 다시 시작 해야 에이전트를 구성](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash)합니다.
4. 새 테스트 백업을 실행합니다. Hello 오류가 계속 되 면 hello 고객의 VM에서 로그를 다음 hello를 수집 하십시오.

   * /var/lib/waagent/*.xml
   * /var/log/waagent.log
   * /var/log/azure/*

waagent의 자세한 로깅이 필요한 경우 다음 단계를 따르세요.

1. Hello /etc/waagent.conf 파일에서 다음 줄 hello 찾습니다: **자세한 로깅을 설정 (y | n)**
2. 변경 hello **Logs.Verbose** 에서 값  *n*  너무*y*합니다.
3. Hello 변경 내용을 저장 하 고 waagent hello이 단원의 이전 단계를 수행 하 여 다시 시작 합니다.

### <a name="hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>hello 스냅숏 상태를 검색할 수 없습니다 또는 스냅숏을 만들 수 없습니다.
hello VM 백업 실행 스냅숏 명령 toohello 기본 저장소 계정을 사용 합니다. 액세스 toohello 저장소 계정이 없습니다 있기 때문에 또는 hello 스냅숏 작업의 hello 실행이 지연 때문에 백업이 실패할 수 있습니다.

#### <a name="solution"></a>해결 방법
다음 조건 hello 스냅숏 작업 실패를 발생할 수 있습니다.

| 원인 | 해결 방법 |
| --- | --- |
| hello VM에 SQL Server 백업이 구성 되었습니다. | 기본적으로 hello VM 백업은 Windows Vm VSS 전체 백업이 실행 됩니다. SQL Server 기반 서버를 실행하고 SQL Server 백업이 구성된 VM에서 스냅숏 실행이 지연될 수 있습니다.<br><br>스냅숏 문제로 인해 백업 실패를 발생 하는 경우 다음 레지스트리 키 hello 설정:<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| hello VM 상태가 잘못 보고 됩니다 RDP hello VM은 종료 합니다. | Hello VM에 원격 데스크톱 (RDP 프로토콜)를 종료 하면 hello 포털 toodetermine hello VM 상태가 올바른지 여부를 확인 합니다. 올바르지 않으면 hello를 사용 하 여 hello 포털에서 VM hello 종료 **종료** hello VM 대시보드에서 옵션입니다. |
| 동일한 클라우드 서비스는 hello에서 많은 Vm을 tooback hello에 구성 동시 합니다. | 모범 사례 toospread는 hello에서 Vm에 대 한 hello 백업 일정에 동일한 클라우드 서비스입니다. |
| 높은 CPU 또는 메모리 사용량에 hello VM 실행 중입니다. | Hello VM 실행 중인 경우 높은 CPU 사용량 (90% 이상) 또는 높은 메모리 사용량, hello 스냅숏 작업을 큐에 대기 했다가 지연 하 고 결국 시간이 초과 합니다. 이 상황에서는 주문형 백업을 시도하세요. |
| dhcp에서 VM hello hello 호스트/패브릭 주소를 가져올 수 없습니다. | DHCP은 hello 백업 toowork IaaS VM에 대 한 hello 게스트 활성화 되어야 합니다.  Hello VM에서에서 가져올 수 없는 hello 호스트/패브릭 주소 DHCP 응답 245, 다운로드 없거나 모든 확장을 실행 합니다. 정적 개인 IP 해야 할 경우 hello 플랫폼을 통해 구성 해야 합니다. 번호 사용 hello 유지 해야 하는 VM 내 DHCP 옵션입니다. 자세한 내용은 [고정 내부 개인 IP 설정](../virtual-network/virtual-networks-reserved-private-ip.md)을 참조하세요. |

### <a name="hello-backup-extension-fails-tooupdate-or-load"></a>예비 내선 번호 hello tooupdate 또는 로드 실패
확장을 로드할 수 없는 경우 스냅숏을 만들 수 없기 때문에 백업이 실패합니다.

#### <a name="solution"></a>해결 방법

**Windows 게스트에 대 한:** hello iaasvmprovider 서비스를 사용할 수 있고 있는지의 시작 유형을 확인 *자동*합니다. Hello 서비스는 이러한 방식으로 구성 되지 않은, 경우 활성화 toodetermine hello 다음 백업 성공 여부.

**Linux 게스트에 대 한:** VMSnapshot Linux (백업에 사용 되는 hello 확장)에 대 한 확인 hello 최신 버전은 1.0.91.0 합니다.<br>


예비 내선 번호 hello 계속 실패 하면 tooupdate 또는 부하 hello VMSnapshot 확장 toobe hello 확장을 제거 하 여 다시 로드를 강제할 수 있습니다. 다음 백업 시도가 hello hello 확장을 다시 로드 됩니다.

toouninstall 확장 hello, 다음 hello지 않습니다.

1. Toohello 이동 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello를 백업 문제가 있는 VM을 찾습니다.
3. **설정**을 클릭합니다.
4. **확장**을 클릭합니다.
5. **Vmsnapshot 확장**을 클릭합니다.
6. **제거**를 클릭합니다.

이 절차는 hello 확장 toobe hello 다음 백업 하는 동안 다시 설치를 수행 합니다.

