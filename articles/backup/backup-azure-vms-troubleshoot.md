---
title: "Azure 가상 컴퓨터를 사용 하 여 백업 오류 aaaTroubleshoot | Microsoft Docs"
description: "Azure 가상 컴퓨터의 백업 및 복원 문제 해결"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 73214212-57a4-4b57-a2e2-eaf9d7fde67f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: trinadhk;markgal;jpallavi;
ms.openlocfilehash: 9224c47e02b52688adcba5876c674c88502557c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Azure 가상 컴퓨터 백업 문제 해결
> [!div class="op_single_selector"]
> * [복구 서비스 자격 증명 모음](backup-azure-vms-troubleshoot.md)
> * [백업 자격 증명 모음](backup-azure-vms-troubleshoot-classic.md)
>
>

Hello 테이블 아래에 나열 된 정보와 함께 Azure 백업을 사용 하는 동안 발생 한 오류를 해결할 수 있습니다.

## <a name="backup"></a>백업
| 오류 세부 정보 | 해결 방법 |
| --- | --- |
| VM이 더 이상 존재 hello 작업을 수행할 수 없습니다. - 백업 데이터를 삭제하지 않고 가상 컴퓨터의 보호를 중지합니다. 자세한 내용: http://go.microsoft.com/fwlink/?LinkId=808124 |이 hello 주 VM 삭제 되지만 hello 백업 정책을 계속 VM tooback에 대 한 조회 하는 경우 발생 합니다. toofix이이 오류: <ol><li> Hello로 hello 가상 컴퓨터를 다시 만듭니다. 동일한 이름과 동일한 리소스 그룹 이름은 [클라우드 서비스 이름]<br>또는</li><li> 가상 컴퓨터 또는 hello 백업 데이터를 삭제 하지 않고 보호를 중지 합니다. [자세한 내용](http://go.microsoft.com/fwlink/?LinkId=808124).</li></ol> |
| 스냅숏 작업이 hello 가상 컴퓨터-toono 네트워크 연결 실패 했습니다 VM 네트워크 액세스 권한을 갖는지 확인 합니다. 스냅숏 toosucceed 하거나 화이트 리스트 Azure 데이터 센터 IP 범위 또는 네트워크 액세스에 대 한 프록시 서버를 설정 하십시오. 자세한 내용은 참조 너무 http://go.microsoft.com/fwlink/?LinkId=800034 합니다. 이미 프록시 서버를 사용 중인 경우 프록시 서버 설정이 제대로 구성되어 있는지 확인합니다. | 이 오류는 hello hello 가상 컴퓨터에서 아웃 바운드 인터넷 연결을 거부 하는 경우에 throw 됩니다. 인터넷 연결을 VM 스냅샷 확장 tootake hello 가상 컴퓨터의 기본 디스크의 스냅숏에 필요 합니다. [자세한 내용은](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#snapshot-operation-failed-due-to-no-network-connectivity-on-the-virtual-machine) 에 어떻게 toofix 스냅숏 tooblocked 네트워크 액세스 인해 오류가 발생 했습니다. |
| VM 에이전트는 Azure 백업 서비스 hello로 없습니다 toocommunicate입니다. -Hello VM 네트워크에 연결 하 고 hello VM 에이전트 실행 되 고 최신 인지 확인 합니다. 자세한 내용은 참조 하십시오 너무 http://go.microsoft.com/fwlink/?LinkId=800034 |이 오류는 hello VM 에이전트 문제가 있습니다 또는 네트워크 액세스 toohello Azure 인프라 어떤 방식으로든에서 차단 하는 경우에 throw 됩니다. VM 스냅숏 문제 디버깅에 대해 [자세히 알아봅니다](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vm-agent-unable-to-communicate-with-azure-backup).<br> Hello VM 에이전트는 모든 문제를 유발 하지 않는지, hello VM에 다시 시작 합니다. 시간에 잘못 된 VM 상태가 하면 문제가 발생할 수, 하 고이 "잘못 된 상태"를 재설정 hello VM을 다시 시작 합니다. |
| VM이 프로 비전 상태가 실패 함으로-하십시오 hello VM을 다시 시작 하 고 해당 hello VM이 백업에 대 한 실행 중이거나 종료 상태에 있는지 확인 | VM 상태 toobe 프로 비전 상태가 실패 한 잠재 고객 hello 확장 오류 중 하나가 때 발생 합니다. Tooextensions 목록을 이동 하 고 실패 한 확장명 인지 제거한 hello 가상 컴퓨터를 다시 시작 하십시오. 모든 확장이 실행 중 상태인 경우 VM 에이전트 서비스가 실행 중인지 확인합니다. 파일이 없으면 hello VM 에이전트 서비스를 다시 시작 합니다. | 
| VMSnapshot 확장 작업이 실패 했습니다-관리 되는 디스크에 대 한 하십시오 hello 백업 작업을 다시 시도 합니다. Hello 문제가 지속 되 면에서 'http://go.microsoft.com/fwlink/?LinkId=800034' hello 지침을 따릅니다. 그래도 실패하면 Microsoft 지원에 문의하시기 바랍니다. | Azure 백업 서비스 tootrigger 스냅숏으로 실패 한 경우이 오류입니다. VM 스냅숏 디버깅 문제에 대해 [자세히 알아보세요](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vmsnapshot-extension-operation-failed). |
| Toohello 데이터 hello 프리미엄 저장소 디스크에 있는 연결 수 hello 저장소 계정-의 여유 공간 tooinsufficient 인해 hello 가상 컴퓨터의 hello 스냅숏을 복사 확인 저장소 계정에 해당 하는 여유 공간이 있는지 toohello 가상 컴퓨터 | 프리미엄 Vm의 경우 hello 스냅숏 toostorage 계정을 복사 합니다. 이 toomake 있는지 스냅숏을 작업 하는 백업 관리 트래픽이 프리미엄 디스크를 사용 하 여 IOPS toohello 사용할 수 있는 응용 프로그램의 hello 수를 제한 하지 않습니다. 저장소 계정 toohello 자격 증명 모음에 복사한이 위치에서 Azure 백업 서비스 hello hello 스냅숏 toostorage 계정 및 전송 데이터를 복사할 수 50%만 hello 총 저장소 계정 공간을 할당 하는 것이 좋습니다. | 
| 없습니다 tooperform hello 작업으로 hello VM 에이전트가 응답 하지 않습니다. |이 오류는 hello VM 에이전트 문제가 있습니다 또는 네트워크 액세스 toohello Azure 인프라 어떤 방식으로든에서 차단 하는 경우에 throw 됩니다. Windows Vm에 대 한 서비스 및 hello 에이전트 제어판의 프로그램에 표시 되는 여부 hello VM 에이전트 서비스 상태를 확인 합니다. 제어 패널 및 다시 설치 hello 에이전트 설명 했 듯이에서 시도 제거 hello 프로그램 [아래](#vm-agent)합니다. Hello 에이전트를 다시 설치한 후 임시 백업 tooverify를 트리거하십시오. |
| 복구 서비스 확장 작업이 실패했습니다. Hello 가상 컴퓨터에 가상 컴퓨터 에이전트가 최신가 에이전트 서비스가 실행 되 고 있는지 확인 하세요. 백업 작업을 다시 시도하고 실패한 경우 Microsoft 지원에 문의하세요. |VM 에이전트가 만료된 경우에 이 오류가 throw됩니다. Tooupdate hello VM 에이전트 아래의 "hello VM 에이전트 업데이트" 섹션을 참조 하십시오. |
| 가상 컴퓨터가 존재하지 않습니다. - 해당 가상 컴퓨터가 존재하는지 확인하거나 다른 가상 컴퓨터를 선택하세요. |이 오류는 hello 기본 VM을 삭제 하지만 hello 백업 정책을 계속 VM tooperform 백업용 toolook 때 발생 합니다. toofix이이 오류: <ol><li> Hello로 hello 가상 컴퓨터를 다시 만듭니다. 동일한 이름과 동일한 리소스 그룹 이름은 [클라우드 서비스 이름]<br>또는<br></li><li>Hello 백업 데이터를 삭제 하지 않고 hello 가상 컴퓨터 보호를 중지 합니다. [자세한 내용](http://go.microsoft.com/fwlink/?LinkId=808124).</li></ol> |
| 명령을 실행하지 못했습니다. - 현재 이 항목에 대해 다른 작업이 진행 중입니다. 하십시오 hello 이전 작업이 완료 될 때까지 기다린 후 다시 시도 |기존 백업 hello VM에서 실행 되 고 hello 기존 작업을 실행 하는 동안 새 작업을 시작할 수 없습니다. |
| 시간 초과 hello 백업 자격 증명 모음에서 Vhd를 복사-hello 작업을 잠시 후에 다시 시도 하십시오. Hello 문제가 계속 되 면 Microsoft 지원에 문의 합니다. | 이 저장소 쪽에 일시적인 오류가 있는 경우 또는 백업 서비스는 주문 tootransfer 데이터 기간 toovault 제한 시간 내에 VM hello 호스팅 저장소 계정에서 충분 한 IOPS를 받고 있지 않으면 경우 발생 합니다. 백업을 설정하는 동안 [모범 사례](backup-azure-vms-introduction.md#best-practices)를 따랐는지 확인하세요. 로드 되지 않았습니다. VM tooa 다른 저장소 계정을 이동 시도 하 고 백업을 다시 시도 합니다.|
| 내부 오류로 인해 백업이 실패-hello 작업을 잠시 후에 다시 시도 하십시오. Hello 문제가 계속 되 면 Microsoft 지원에 문의 |이 오류는 다음 두 가지 이유로 발생할 수 있습니다. <ol><li> Hello VM 저장소 액세스에 일시적인 문제가 있습니다. 확인 하십시오 [Azure 상태](https://azure.microsoft.com/en-us/status/) toosee 모든 진행 중인 문제가 있는 경우 관련 toocompute, 저장소 또는 네트워킹 hello 지역에 있습니다. Hello 문제가 해결 되 면 hello 백업 작업을 다시 시도 하세요. <li>hello 원본 VM 삭제 하 고 따라서 hello 복구 지점을 만들 수 없습니다. tookeep 백업 데이터 삭제 된 VM에 대 한 hello 하지만 hello 백업 오류 제거: hello VM 보호를 해제 하 고 hello 옵션 tookeep hello 데이터를 선택 합니다. 이 작업에는 hello 예약 된 백업 작업 및 오류 메시지를 되풀이 하는 hello 중지합니다. |
| Hello 선택 항목에 tooinstall hello Azure 복구 서비스 확장 하지 못했습니다.-hello VM 에이전트는 hello Azure 복구 서비스 확장에 대 한 필수 구성 요소. Hello Azure VM 에이전트를 설치 하 고 hello 등록 작업을 다시 시작 |<ol> <li>Hello VM 에이전트가 올바르게 설치 된 경우를 확인 합니다. <li>Hello 플래그 hello VM config 올바르게 설정 되었는지 확인 합니다.</ol> [자세한 내용은](#validating-vm-agent-installation) hello VM 에이전트 및 어떻게 toovalidate hello VM 에이전트 설치를 설치 하는 방법에 대 한 합니다. |
| "COM +가 없습니다 tootalk toohello Microsoft Distributed Transaction Coordinator hello 오류와 함께 확장 설치 실패 |Hello COM + 서비스가 실행 되지 않는 것을 의미 합니다. 이 문제 해결에 대한 도움은 Microsoft 지원에 문의하세요. |
| 스냅숏 작업이 실패 했으며 hello VSS 작업 오류로 "이이 드라이브는 BitLocker 드라이브 암호화로 잠겨 있음. Hello 제어판에서에서이 드라이브의 잠금을 해제 해야 합니다. |Hello VM에 있는 모든 드라이브에 대 한 BitLocker를 해제 하 고 hello VSS 문제가 해결 되는 경우 관찰 |
| VM이 백업을 허용하지 않는 상태입니다. |<ul><li>VM이 실행 중 및 종료 사이의 일시적 상태인지 확인합니다. 그럴 경우 그 중 하나가 hello VM 상태 toobe 기다렸다가 트리거할 다시 백업 합니다. <li> Hello VM Linux VM 및 [보안 강화 Linux]를 사용 하 여 커널 모듈 경우 tooexclude hello Linux 에이전트 경로 필요 (_/var/lib/waagent_) 보안을 통해 정책 toomake 있는지 백업 확장 설치 됩니다.  |
| Azure 가상 컴퓨터를 찾을 수 없습니다. |이 오류는 hello 주 VM 삭제 되었지만 hello 백업 정책을 백업에 대 한 VM tooperform toolook 계속 때 발생 합니다. toofix이이 오류: <ol><li>Hello로 hello 가상 컴퓨터를 다시 만듭니다. 동일한 이름과 동일한 리소스 그룹 이름은 [클라우드 서비스 이름] <br>또는 <li> 이 VM에 대 한 보호를 않도록 hello 백업 작업이 생성 되지 것입니다. </ol> |
| 가상 컴퓨터 에이전트가 hello 가상 컴퓨터에 나타나지 않습니다.-모든 필수 구성 요소 및 hello VM 에이전트를 설치 하십시오 하 고 작업을 hello를 다시 시작 합니다. |[자세한 내용은](#vm-agent) VM 에이전트를 설치 하 고 어떻게 toovalidate hello VM 에이전트를 설치 하는 방법에 대 한 합니다. |
| 상태가 좋지 tooVSS 기록기 인해 스냅숏 작업이 실패 했습니다. |잘못 된 상태에 있는 toorestart VSS (볼륨 섀도 복사본 서비스) 기록기가 필요 합니다. tooachieve이, 상승된 된 명령 프롬프트에서 실행 해야 _vssadmin 목록 작성기_합니다. 출력에는 모든 VSS 기록기와 해당 상태가 포함됩니다. “[1] 안정” 상태가 아닌 모든 VSS 기록기는 관리자 권한 명령 프롬프트에서 다음 명령을 실행하여 다시 시작합니다.<br> _net stop serviceName_ <br> _net start serviceName_|
| Hello 구성의 구문 분석 오류 tooa 인해 스냅숏 작업이 실패 했습니다. |Hello MachineKeys 디렉터리에 대 한 toochanged 권한을 인해 이런: _%systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br>아래 명령을 실행하고 MachineKeys 디렉터리에 대한 권한이 기본 권한인지 확인합니다.<br>_icacls %systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br><br> 기본 권한은 다음과 같습니다.<br>Everyone:(R,W) <br>BUILTIN\Administrators:(F)<br><br>사용 권한을 기본값과 다른 MachineKeys 디렉터리에 표시 되 면 하십시오 toocorrect 권한을 단계 아래, hello 인증서를 삭제 하 고 hello 백업을 트리거.<ol><li>MachineKeys 디렉터리에 대한 권한을 수정합니다.<br>탐색기 보안 속성 및 고급 보안 설정 사용 하 여 hello 디렉터리, 재설정 권한 toohello 기본값 다시, hello 디렉터리에서 모든 (기본값) 보다 추가 되는 사용자 개체를 제거 및 해당 hello 'Everyone' 확인 권한을 특별 한 에 대 한 액세스를 제공 합니다.<br>-폴더 나열/데이터 읽기 <br>-특성 읽기 <br>-확장된 특성 읽기 <br>-파일 만들기/데이터 쓰기 <br>-폴더 만들기/데이터 추가<br>-특성 쓰기<br>-확장된 특성 쓰기<br>- 읽기 권한<br><br><li>‘Issued To’ 필드 = "Windows Azure Service Management for Extensions" 또는 "Windows Azure CRP Certificate Generator"가 지정된 인증서를 모두 삭제합니다.<ul><li>[인증서(로컬 컴퓨터) 콘솔 열기](https://msdn.microsoft.com/library/ms788967(v=vs.110).aspx)<li>‘Issued To’ 필드 = "Windows Azure Service Management for Extensions" 또는 "Windows Azure CRP Certificate Generator"가 지정된 인증서를 모두 삭제합니다(개인 -> 인증서).</ul><li>VM 백업을 트리거합니다. </ol>|
| 가상 컴퓨터가 BEK만으로 암호화되었기 때문에 유효성 검사에 실패했습니다. BEK와 KEK 모두로 암호화된 가상 컴퓨터에서만 백업을 사용할 수 있습니다. |이 경우 가상 시스템을 BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화해야 합니다. 그런 후에 백업을 사용하도록 설정해야 합니다. |
| Azure 백업 서비스에 없는 충분 한 사용 권한을 tooKey 자격 증명 모음에 대 한 백업을 암호화 가상 컴퓨터의 합니다. |Backup 서비스에는 [PowerShell 설명서](backup-azure-vms-automation.md)의 **백업 사용** 섹션에 설명된 단계를 사용하여 PowerShell에서 이러한 권한을 제공해야 합니다. |
|설치에 실패 했습니다 오류는 확장 스냅숏-COM + 없습니다 tootalk toohello Microsoft Distributed Transaction Coordinator가 | 하십시오 시도 toostart windows 서비스 "COM + 시스템 응용 프로그램" (관리자 권한 명령 프롬프트- _net 시작 COMSysApp_). <br>시작하는 동안 실패하면 아래 단계를 수행하세요.<ol><li> "Distributed Transaction Coordinator" 서비스의 로그온 계정 hello "Network Service" 인지 확인 합니다. 그렇지 않은 경우 변경 하십시오 너무 "Network Service"이이 서비스를 다시 시작 했다가 toostart 서비스 "COM + System Application"입니다.'<li>Toostart 계속 실패 하면 제거/설치 "Distributed Transaction Coordinator" 서비스 아래 단계를 수행 하 여:<br> --Hello MSDTC 서비스를 중지 하는 중<br> - 명령 프롬프트 열기(cmd) <br> - “msdtc -uninstall” 명령 실행 <br> - “msdtc -install” 명령 실행 <br> -Hello MSDTC 서비스를 시작 합니다.<li>Windows 서비스 "COM+ 시스템 응용 프로그램"을 시작한 후 포털에서 백업을 트리거합니다.</ol> |
|  TooCOM + 오류 인해 스냅숏 작업이 실패 했습니다. | hello 동작은 toorestart windows 서비스 "COM + System Application" 하는 것이 좋습니다 (관리자 권한 명령 프롬프트- _net 시작 COMSysApp_). Hello 문제가 지속 되 면 hello VM을 다시 시작 합니다. VM에서 지원 하지 않고 hello를 다시 시작 해도 시도 [VMSnapshot 확장 hello 제거](https://docs.microsoft.com/en-us/azure/backup/backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout#cause-3-the-backup-extension-fails-to-update-or-load) hello 백업을 수동으로 트리거 및 합니다. |
| 하나는 toofreeze 되지 않았거나의 자세한 탑재 지점 hello VM tootake 파일 시스템 일관성 있는 스냅숏 | 단계를 수행 하는 hello를 사용 합니다. <ol><li>사용 하 여 탑재 된 모든 장치의 hello 파일 시스템 상태를 확인 _'tune2fs'_ 명령입니다.<br> 예: tune2fs -l /dev/sdb1 \| grep "Filesystem state" <li>파일 시스템에 대 한 상태가 되지 정리를 사용 하 여 hello 장치를 탑재 해제 _'umount'_ 명령 <li> _'fsck'_ 명령을 사용하여 이러한 장치에 대해 FileSystemConsistency Check를 실행합니다. <li> Hello 장치를 다시 탑재 하 고 백업을 시도 합니다.</ol> |
| 스냅숏 작업이 실패 했습니다 보안 네트워크 통신 채널을 만드는 toofailure | <ol><Li> 관리자 권한 모드에서 regedit.exe를 실행하여 레지스트리 편집기를 엽니다. <li> 시스템에 있는 모든 버전의 .NetFramework를 파악합니다. 레지스트리 키 "찾아"의 hello 계층 구조 아래에 있습니다 <li> 레지스트리 키에 있는 각 .NetFramework에 대해 다음 키를 추가합니다. <br> "SchUseStrongCrypto"=dword:00000001 </ol>|
| 스냅숏 작업이 실패 했습니다 Visual Studio 2012 용 Visual c + + 재배포 가능 패키지의 설치에 toofailure | TooC:\Packages\Plugins\Microsoft.Azure.RecoveryServices.VMSnapshot\agentVersion 이동한 vcredist2012_x64를 설치 합니다. 레지스트리 키 값이 서비스 설치를 허용 하는 데 toocorrect 값 즉, 레지스트리 키의 값을 설정 되어 있는지 확인 _찾아_ too3 및 4 하지 설정 됩니다. 설치하는 데 여전히 문제가 발생할 경우 관리자 권한 명령 프롬프트에서 _MSIEXEC /UNREGISTER_를 실행한 후 _MSIEXEC /REGISTER_를 실행하여 설치 서비스를 다시 시작합니다.  |


## <a name="jobs"></a>작업
| 오류 세부 정보 | 해결 방법 |
| --- | --- |
| 이 작업 유형에 대 한 취소를 사용할 수 없습니다-hello 작업이 완료 될 때까지 잠시 기다려 주십시오. |없음 |
| hello 작업이 취소 가능한 상태가 아니므로-hello 작업이 완료 될 때까지 잠시 기다려 주십시오. <br>또는<br> hello 선택한 작업을 취소할 수 있는 상태가 아니므로-hello 작업 toocomplete 잠시 기다려 주십시오. |모든 가능성에 hello 작업이 거의 완료 되었습니다. Hello 작업이 완료 될 때까지 잠시 기다려 주십시오.|
| 진행 중에-취소는 진행 중인 작업에만 지원 하므로 hello 작업을 취소할 수 없습니다. 진행 중인 작업에 대해 취소를 시도하세요. |이 tooa 일시적 상태로 인해 발생합니다. 잠시 기다렸다가 hello 취소 작업을 다시 시도 하십시오. |
| 실패 한 toocancel hello 작업-작업 끝날 때까지 기다려 주십시오. |없음 |

## <a name="restore"></a>복원
| 오류 세부 정보 | 해결 방법 |
| --- | --- |
| 클라우드 내부 오류로 인해 복원 실패 |<ol><li>클라우드 서비스 toowhich toorestore를 시도 하는 DNS 설정으로 구성 됩니다. 다음을 확인하면 알 수 있습니다. <br>$deployment = Get-AzureDeployment -ServiceName "ServiceName" -Slot "Production"     Get-AzureDns -DnsSettings $deployment.DnsSettings<br>구성된 주소가 있으면 DNS 설정이 구성되었다는 의미입니다.<br> <li>클라우드 서비스 toowhich tooyou 려 toorestore 예약 된 Ip로 구성 되어 있으며 기존 Vm 클라우드 서비스에서 중지 된 상태에서.<br>다음 powershell cmdlet을 사용하여 클라우드 서비스에 예약된 IP가 있는지 확인할 수 있습니다.<br>$deployment = Get-AzureDeployment -ServiceName "servicename" -Slot "Production" $dep.ReservedIPName <br><li>Toorestore toosame 클라우드 서비스에서 다음 특수 한 네트워크 구성 사용 하 여 가상 컴퓨터를 하려고 합니다. <br>- 부하 분산 장치 구성의 가상 컴퓨터(내부 및 외부)<br>- 여러 개의 예약된 IP를 사용하는 가상 컴퓨터<br>- 여러 NIC가 있는 가상 컴퓨터<br>Hello UI에서에서 새 클라우드 서비스를 선택 하십시오 또는 너무를 참조 하십시오[복원 고려 사항](backup-azure-arm-restore-vms.md#restoring-vms-with-special-network-configurations) 특수 한 네트워크 구성 된 Vm에 대 한 합니다.</ol> |
| hello 선택한 DNS 이름이 이미 사용 중-하십시오 다른 DNS 이름을 지정 하 고 다시 시도 하십시오. |hello DNS 이름이 여기 참조 toohello 클라우드 서비스 이름 (일반적으로 끝나는. cloudapp.net에). 이 테스트 해야 toobe 고유 합니다. 이 오류가 발생 하면 복원 중 다른 VM 이름을 toochoose 필요. <br><br> 이 오류는 hello Azure 포털의 toousers만 표시 됩니다. hello PowerShell 통해 복원 작업에 성공할 것 데이터만 hello 디스크를 복원 하 고 VM hello를 만들지는 않습니다. hello 오류 hello 디스크 복원 작업 후 사용자가 VM hello를 명시적으로 만들 때 직면 하 게 될 됩니다. |
| hello 지정 된 가상 네트워크 구성이 잘못 되었습니다-उ प क 다른 가상 네트워크 구성 하 고 다시 시도 하십시오. |없음 |
| hello는 클라우드 서비스는 hello hello 가상 컴퓨터 구성의 복원 되 고 일치-예약 된 IP를 사용 하지 않는 하는 다른 클라우드 서비스를 지정 하십시오 하거나 다른 복구 지점 toorestore에서 선택 하지 않습니다는 예약된 된 IP를 사용 하 여 지정 합니다. |없음 |
| 클라우드 서비스에는 다른 클라우드 서비스를 지정 하 여 또는 기존 끝점을 사용 하 여 다시 시도 hello 작업 입력된 끝점-의 수 제한에 도달 했습니다. |없음 |
| 백업 자격 증명 모음과 대상 저장소 계정이 서로 다른 두 지역에-hello 중인 복원 작업에 지정 된 hello 저장소 계정을 확인 hello 백업 자격 증명 모음과 동일한 Azure 지역입니다. |없음 |
| 지원 되는 hello 복원 작업이 않습니다으로 지정한 저장소 계정-만 기본/표준 저장소 계정을 로컬 중복 또는 지역 중복 복제 설정이 지원 됩니다. 지원되는 저장소 계정을 선택하세요. |없음 |
| 복원 작업에 대해 지정 된 저장소 계정의 유형이 온라인있지 않습니다.-복원 작업에 지정 된 hello 저장소 계정이 온라인 상태 인지 확인 |이 Azure 저장소에 또는 tooan 중단 인해 일시적인 오류로 인해 발생할 수 있습니다. 다른 저장소 계정을 선택하세요. |
| 리소스 그룹 할당량에 도달 했으므로-Azure 포털 또는 Azure 고객 지원으로 문의 tooincrease hello 제한에서 일부 리소스 그룹을 삭제 하십시오. |없음 |
| 선택한 서브넷이 존재하지 않습니다. 존재하는 서브넷을 선택하세요. |없음 |
| 백업 서비스 구독에 있는 권한 부여 tooaccess 리소스가 없습니다. |tooresolve 섹션에서 언급 한 단계를 사용 하 여이 첫 번째 복원 디스크 **디스크 백업 복원** 에 [선택 VM 구성 복원](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)합니다. 그 후에 언급 된 PowerShell 단계를 사용 하 여 [복원 된 디스크에서 VM을 만들](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate 복원 된 디스크에서 VM을 전체. |

## <a name="backup-or-restore-taking-time"></a>백업 또는 복원에 시간이 걸림
백업(12시간 초과) 또는 복원 소요 시간(6시간 초과)이 표시되는 경우
* 이해 [toobackup 시간을 형성 하는 요인](backup-azure-vms-introduction.md#total-vm-backup-time) 및 [toorestore 시간을 형성 하는 요인](backup-azure-vms-introduction.md#total-restore-time)합니다.
* [백업 모범 사례](backup-azure-vms-introduction.md#best-practices)를 따라야 합니다. 

## <a name="vm-agent"></a>VM 에이전트
### <a name="setting-up-hello-vm-agent"></a>VM 에이전트 hello 설정
일반적으로 hello VM 에이전트는 hello Azure 갤러리에서에서 생성 된 Vm에 이미 있습니다. 그러나 온-프레미스 데이터 센터에서 마이그레이션된 가상 컴퓨터 hello VM 에이전트가 설치 되어 있어야 합니다. 이러한 Vm에 대 한 hello VM 에이전트 toobe 명시적으로 설치 해야 합니다.

Windows VM의 경우

* 다운로드 및 설치 hello [에이전트 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. 관리자 권한 toocomplete hello 설치를 해야합니다.
* 기본 가상 컴퓨터에 대 한 [hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다. 리소스 관리자 가상 컴퓨터의 경우 이 단계가 필요하지 않습니다.

Linux VM의 경우

* 배포 리포지토리에서 최신 버전을 설치합니다. 배포 리포지토리를 사용할 때만 에이전트를 설치할 것을 **강력히 권장**합니다. 패키지 이름에 대 한 세부 정보를 참조 하십시오 너무[Linux 에이전트 리포지토리](https://github.com/Azure/WALinuxAgent) 
* 클래식 Vm에 대 한 [hello VM 속성을 업데이트](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) 에이전트 hello tooindicate가 설치 되어 있습니다. 리소스 관리자 가상 컴퓨터의 경우 이 단계가 필요하지 않습니다.

### <a name="updating-hello-vm-agent"></a>Hello VM 에이전트를 업데이트합니다.
Windows VM의 경우

* 업데이트 hello VM 에이전트를 다시 설치 하는 hello [VM 에이전트 이진 파일](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)합니다. 그러나 hello VM 에이전트를 업데이트 하는 동안 실행 중인 백업 작업이 수행 되지 tooensure를 해야 합니다.

Linux VM의 경우

* Hello 지침에 따라 [Linux VM 에이전트 업데이트](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.
배포 리포지토리를 사용할 때만 에이전트를 업데이트할 것을 **강력히 권장**합니다. 직접 github에서 hello 에이전트 코드를 다운로드 및 업데이트 하는 것은 좋지 않습니다. 최신 에이전트 배포에 필요한 사용할 수 없는 경우 확장 방법에 대 한 지침은 toodistribution 지원 문의 tooinstall 최신 에이전트입니다. github 리포지토리에서 최신 [Microsoft Azure Linux 에이전트](https://github.com/Azure/WALinuxAgent/releases) 정보를 확인할 수 있습니다.

### <a name="validating-vm-agent-installation"></a>VM 에이전트 설치의 유효성 검사
방법에 대 한 toocheck hello Windows Vm에서 VM 에이전트 버전:

1. Toohello Azure 가상 컴퓨터에 로그인 하 고 toohello 폴더 탐색 *C:\WindowsAzure\Packages*합니다. Hello WaAppAgent.exe 파일이 없는 찾아야 합니다.
2. Hello 파일을 마우스 오른쪽 단추로 클릭 한 다음 너무 이동 하십시오**속성**를 클릭 한 hello **세부 정보** 탭 hello 제품 버전 필드 2.6.1198.718 이루어져야 이상

## <a name="troubleshoot-vm-snapshot-issues"></a>VM 스냅숏 문제 해결
VM 백업 toounderlying 저장소 스냅숏 명령을 발행에 의존 합니다. 고 다니지 않아도 액세스 toostorage 또는 지연 스냅숏 작업 실행에 백업 작업 toofail hello 발생할 수 있습니다. hello 다음 스냅숏 작업 오류가 발생할 수 있습니다.

1. NSG를 사용 하 여 네트워크 액세스 tooStorage 차단<br>
    너무 자세한 방법에 대 한 자세한 내용은[네트워크 액세스 사용](backup-azure-vms-prepare.md#network-connectivity) tooStorage ip 또는 프록시 서버를 통해 어느 허용 목록을 사용 하 여 합니다.
2. Sql Server 백업이 구성된 VM이 스냅숏 작업을 지연시킬 수 있습니다. <br>
   기본적으로 VM 백업은 Windows VM에서 VSS 전체를 백업합니다. VM에서 Sql Server를 실행하고 있으며 Sql Server 백업이 구성된 경우 스냅숏 실행 시 지연이 발생할 수 있습니다. 스냅숏 문제로 인해 백업이 실패하면 다음 레지스트리 키를 설정하세요.

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
   "USEVSSCOPYBACKUP"="TRUE"
   ```
3. VM이 RDP에서 종료되므로 VM 상태가 잘못 보고됩니다.  <br>
   RDP의 hello 가상 컴퓨터를 종료 하는 경우 확인 하십시오 hello 포털에 다시 VM 상태가 올바르게 반영 됩니다. 그렇지 않으면 VM 대시보드 '종료' 옵션을 사용 하 여 포털에 hello VM 종료 하십시오.
4. 5 개 이상의 Vm 공유 hello 동일한 경우 클라우드 서비스, 여러 개의 백업 정책 toostage hello 하지 않게 hello에 시작 되는 최대 4 개의 VM 백업을 백업 시간을 구성할 동시 합니다. Toospread hello 백업 시작을 시간 정책 간의 분리 한 시간에 시도 하십시오.
5. VM이 높은 CPU/메모리에서 실행 중입니다.<br>
   높은 CPU에서 hello 가상 컴퓨터가 실행 중인 경우 usage(>90%) 또는 메모리 스냅숏 작업은 큐에 대기, 지연 및 초과 가져옵니다 결국 됩니다. 이러한 상황에서는 주문형 백업을 시도하세요.

<br>

## <a name="networking"></a>네트워킹
모든 확장 처럼 백업 확장 toohello 공용 인터넷 toowork를 액세스 필요 합니다. 액세스 toohello 다니지 않아도 공용 인터넷에에서 나타날 수 다양 한 방법으로:

* hello 확장 설치가 실패할 수 있습니다.
* (예: 디스크 스냅숏) hello 백업 작업이 실패할 수 있습니다.
* Hello 상태 hello 백업 작업의 표시에 실패할 수 있습니다.

공용 인터넷 주소를 확인 하기 위한 hello 필요 명시 된 [여기](http://blogs.msdn.com/b/mast/archive/2014/06/18/azure-vm-provisioning-stuck-on-quot-installing-extensions-on-virtual-machine-quot.aspx)합니다. VNET hello에 대 한 toocheck hello DNS 구성을 구현 해야 하 고이 정보를 해당 hello Azure Uri를 확인할 수를 확인 합니다.

Hello 이름 확인을 제대로 완료 액세스 toohello Azure Ip에 제공 된 toobe도 필요 합니다. toounblock 액세스 toohello Azure 인프라는 다음이 단계 중 하나를 따르십시오.

1. 화이트 리스트 hello Azure 데이터 센터 IP 범위입니다.
   * Hello 목록이 [Azure 데이터 센터 Ip](https://www.microsoft.com/download/details.aspx?id=41653) toobe 허용 목록입니다.
   * 차단 해제 hello를 사용 하 여 Ip hello [새로 NetRoute](https://technet.microsoft.com/library/hh826148.aspx) cmdlet. (관리자 권한으로 실행) 하는 관리자 권한 PowerShell 창에서 hello Azure VM 내에서이 cmdlet을 실행 합니다.
   * (위치에 있는) 하는 경우 규칙 toohello NSG 추가 tooallow 액세스 toohello Ip입니다.
2. HTTP 트래픽 tooflow에 대 한 경로 만들기
   * 있는 경우 HTTP 프록시 서버 tooroute hello 트래픽을 배포 하는 위치 (예: 네트워크 보안 그룹)에 몇 가지 네트워크 제한 합니다. HTTP 프록시 서버를 찾을 수 단계 toodeploy [여기](backup-azure-vms-prepare.md#network-connectivity)합니다.
   * 추가 규칙 toohello NSG (위치에 있는) 하는 경우 HTTP 프록시 hello에서 tooallow 액세스 toohello 인터넷 합니다.

> [!NOTE]
> DHCP은 hello 게스트 toowork IaaS VM 백업에 대 한 활성화 되어야 합니다.  정적 개인 IP 해야 할 경우 hello 플랫폼을 통해 구성 해야 합니다. 번호 사용 hello 유지 해야 하는 VM 내 DHCP 옵션입니다.
> [고정 내부 개인 IP 설정](../virtual-network/virtual-networks-reserved-private-ip.md)에 대한 자세한 내용을 확인합니다.
>
>
