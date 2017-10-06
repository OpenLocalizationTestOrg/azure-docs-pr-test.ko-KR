---
title: "Azure 백업 서버 aaaTroubleshoot | Microsoft Docs"
description: "Azure Backup Server 설치, 등록 및 응용 프로그램 워크로드의 백업 및 복원 문제 해결"
services: backup
documentationcenter: 
author: pvrk
manager: shreeshd
editor: 
ms.assetid: 2d73c349-0fc8-4ca8-afd8-8c9029cb8524
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: pullabhk;markgal;
ms.openlocfilehash: 2386cfcfbf7cc686b5c051d2e1a3a884481ccdc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-server"></a>Azure Backup Server 문제 해결

다음 표에 hello에 나열 된 정보와 함께 Azure 백업 서버를 사용 하는 동안 발생 한 오류를 해결할 수 있습니다.


## <a name="installation-issues"></a>설치 문제

| 작업 | 오류 세부 정보 | 해결 방법 |
|-----------|---------------|------------|
|설치 | 설치 프로그램이 레지스트리 메타데이터를 업데이트할 수 없습니다. 이 업데이트에 실패 저장소 사용량의 tooover 사용이 될 수 있습니다. tooavoid이 하십시오 업데이트 hello 트리밍 ReFS 레지스트리 항목입니다. | SYSTEM\CurrentControlSet\Control\FileSystem\RefsEnableInlineTrim hello 레지스트리 키를 조정 합니다. Dword too1 hello 값을 설정 합니다. |
|설치 | 설치 프로그램이 레지스트리 메타데이터를 업데이트할 수 없습니다. 이 업데이트에 실패 저장소 사용량의 tooover 사용이 될 수 있습니다. tooavoid이 하십시오 업데이트 hello 볼륨 SnapOptimization 레지스트리 항목입니다. | 빈 문자열 값을 가진 SOFTWARE\Microsoft 데이터 보호 Manager\Configuration\VolSnapOptimization\WriteIds hello 레지스트리 키를 만듭니다. |

## <a name="registration-and-agent-related-issues"></a>등록 및 에이전트 관련 문제
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| Tooa 자격 증명 모음 등록 | 잘못된 자격 증명 모음이 제공되었습니다. hello 파일이 손상 되었거나 복구 서비스와 연결 된 최신 자격도 hello가 없습니다. | toofix이이 오류: <ol><li> Hello 자격 증명 모음에서 hello 최신 자격 증명 파일을 다운로드 하 고 다시 시도 하십시오 <br>또는</li> <li> Hello 자격 증명 tooa 다른 로컬 디렉터리에 다운로드를 시도 하거나 새 자격 증명 모음 만들기 작업 위의 hello 작동 하지 않는 경우 <br>또는</li> <li> Hello 날짜를 업데이트 시도 및 시간 설정에 명시 된 대로 [이 블로그](https://azure.microsoft.com/blog/troubleshooting-common-configuration-issues-with-azure-backup/) <br>또는</li> <li> c:\windows\temp에 65000개 이상의 파일이 있는지 확인합니다. 오래 된 파일 tooanother 위치를 이동 하거나 hello Temp 폴더에 있는 hello 항목 삭제 <br>또는</li> <li> 인증서의 hello 상태를 확인 합니다. <br> a. (Hello 제어판)에서 "컴퓨터 인증서 관리"를 열으십시오 <br> b. 부모 노드와 자식 노드 "인증서" hello "개인" 노드를 확장 합니다. <br> c.  "Windows Azure Tools" hello 인증서 제거 <br> d. Azure 백업 클라이언트 hello에에서 hello 등록을 다시 시도 하십시오. <br> 또는 </li> <li> 그룹 정책이 구현되어 있는지 확인합니다. </li></ol> |
| Tooprotected 서버는 에이전트 | hello 에이전트 작업이 실패 했습니다 hello DPM 에이전트 코디네이터 서비스와 통신 오류 때문에 \<서버 이름 > | **권장 조치 hello 제품에 표시 된 hello 작동 하지 않는 경우**, <ol><li> 신뢰할 수 없는 도메인에서 컴퓨터를 연결하는 경우 [다음](https://technet.microsoft.com/library/hh757801(v=sc.12).aspx) 단계를 따르세요. <br> 또는 </li><li> 신뢰할 수 있는 도메인에서 컴퓨터를 연결 하는 경우에 설명 된 hello 단계를 사용 하 여 문제 해결 [이 블로그](https://blogs.technet.microsoft.com/dpm/2012/02/06/data-protection-manager-agent-network-troubleshooting/) <br>또는</li><li> 문제 해결 단계로 바이러스 백신을 사용하지 않도록 설정합니다. Hello 문제를 해결 하는 경우 [이 문서]에 설명 된 대로 hello 바이러스 백신 설정을 수정 (https://technet.microsoft.com/library/hh757911.aspx)</li></ol> |
| Tooprotected 서버는 에이전트 | 서버에 대 한 지정 된 hello 자격 증명이 올바르지 않습니다. | **권장 조치 hello 제품에 표시 된 hello 작동 하지 않는 경우**, <br> 에 지정 된 대로 hello 프로덕션 서버에서 수동으로 tooinstall hello 보호 에이전트를 시도 [이 문서](https://technet.microsoft.com/library/hh758186(v=sc.12).aspx#BKMK_Manual)|
| Azure 백업 에이전트에서 없습니다 tooconnect toohello Azure 백업 서비스 (ID: 100050) | hello Azure Backup Agent가 없습니다 tooconnect toohello Azure 백업 서비스. | **권장 조치 hello 제품에 표시 된 hello 작동 하지 않는 경우**, <br>1. 관리자 권한 프롬프트에서 다음 명령을 실행합니다. psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe" Internet Explorer 창이 열립니다. <br/> 2. 이동 tooTools-> 인터넷 옵션-> 연결-> LAN 설정 합니다. <br/> 3. 시스템 계정에 대한 프록시 설정을 확인합니다. 프록시 IP 및 포트를 설정합니다. <br/> 4. Internet Explorer를 닫습니다.|
| Azure Backup Agent 설치 실패 | hello Microsoft Azure 복구 서비스 설치에 실패 했습니다. Microsoft Azure 복구 서비스 설치 toohello 시스템 hello에서 변경한 모든 내용은 롤백 되었습니다. (ID: 4024) | Azure Agent 수동 설치


## <a name="configuring-protection-group"></a>보호 그룹 구성
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 보호 그룹 구성 | DPM은 보호된 컴퓨터(보호된 컴퓨터 이름)에 응용 프로그램 구성 요소를 열거할 수 없습니다. | Hello에서 '새로 고침을 클릭 hello 관련 데이터 원본/구성 요소 수준에서 보호 그룹 UI 화면을 구성 합니다. |
| 보호 그룹 구성 | 없습니다 tooconfigure 보호 | Hello 보호 된 서버는 SQL server를 확인 하십시오 여부 sysadmin 역할 권한이 제공 되었습니다 toohello 시스템 계정 (NTAuthority\System) hello 보호 된 컴퓨터에서에 명시 된 대로 [이 문서](https://technet.microsoft.com/library/hh757977(v=sc.12).aspx)
| 보호 그룹 구성 | 이 보호 그룹에 대 한 hello 저장소 풀의 여유 공간이 부족 한 | 디스크 toohello 저장소 풀에 추가 되는 hello [파티션에 포함 되 면 안](https://technet.microsoft.com/library/hh758075(v=sc.12).aspx)합니다. Hello 디스크의 기존 볼륨을 모두 삭제 한 다음 toohello 저장소 풀 추가|
| 정책 변경 |hello 백업 정책을 수정할 수 없습니다. 오류: tooan 내부 서비스 오류 [0x29834] 인해 hello 현재 작업이 실패 했습니다. Hello 작업을 잠시 후 다시 시도 하십시오. Hello 문제가 지속 되 면 Microsoft 지원에 문의 하세요. |**원인:**<br/>이 오류에는 보안 설정 사용 hello 최소 값 위에 지정 된 아래의 tooreduce 보존 범위를 시도 하 고 지원 되지 않는 버전 MAB 버전 2.0.9052 및 Azure 백업 서버 업데이트 1) (아래에 있는 경우 제공 됩니다. <br/>**권장 작업:**<br/> Hello 최소 보존 지정 된 기간 (3 주 매주, 매월 또는 매년에 대 한 1 년 동안 매일, 4 개의 주에 대 한 일) 위에 보존 기간을 설정 해야이 경우 tooproceed 정책과 관련 업데이트 합니다. 선호 되는 방법은 tooupdate 백업 에이전트와 Azure 백업 서버 tooleverage 것 필요에 따라 모든 hello 보안 업데이트 합니다. |

## <a name="backup"></a>백업
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 백업 | 복제본이 불일치 | 복제본 불일치와 관련 된 제안 hello 원인에 대 한 자세한 정보를 볼 수 [여기](https://technet.microsoft.com/library/cc161593.aspx) <br> <ol><li> 시스템 상태/BMR 백업의 경우 보호된 서버에 Windows Server 백업이 설치되어 있는지 여부를 확인하세요. </li><li> 관련 된 공간을 확인 DPM 저장소에 대해 문제 hello DPM/MABS 서버 풀 및 필요에 따라 저장소 할당 </li><li> Hello hello 보호 된 서버에서 볼륨 섀도 복사본 서비스의 hello 상태를 확인 합니다. 에 있는 경우 사용할 수 없는 상태 toostart 수동으로 설정 하 고 hello 서버의 hello 서비스를 시작 합니다. 그런 다음 toohello DPM/MABS 콘솔 돌아가서 일관성 확인 hello 동기화를 시작 하십시오.</li></ol>|
| 백업 | Hello 작업을 실행 하는 동안 예기치 않은 오류가 발생 했습니다., hello 장치가 준비 되지 않았습니다. | **권장 조치 hello 제품에 표시 된 hello 작동 하지 않는 경우**, <br> <ol><li>Hello 항목 hello 보호 그룹에 대해 섀도 복사본 저장소 공간 toounlimited hello를 설정 하 고 hello 일관성 확인 실행 <br></li> 또는 <li>Hello 기존 보호 그룹 삭제를 시도 하 고 여러 새로 만들 – 각 개별 항목에 하나</li></ol> |
| 백업 | 시스템 상태만 백업 하는 경우 hello 보호 된 컴퓨터 toostore hello 시스템 상태 백업에 충분 한 여유 공간이 있는지 확인 | <ol><li>해당 hello WSB hello 보호 된 컴퓨터에 설치 되었는지 확인</li><li>충분 한 공간이 hello 시스템 상태에 대 한 hello 보호 된 컴퓨터에 존재 하는지 확인: 가장 쉬운 방법은 toodo hello toogo toohello 보호 된 컴퓨터를 열고 WSB 및 hello 선택을 클릭 하 여 BMR를 선택 합니다. hello UI는 다음 알려 얼마나 많은 공간이이 필요 합니다. WSB를 열고 -> 로컬 백업 -> 백업 일정 -> 백업 구성 선택 -> 전체 서버를 선택합니다(크기가 표시됨). 검증에 이 크기를 사용합니다.</li></ol>
| 백업 | 온라인 복구 지점 생성 실패 | Hello 오류 메시지가 표시 되 면 "Windows Azure Backup Agent가 없습니다 toocreate 선택한 hello에 대 한 스냅숏을 볼륨", 복제 및 복구 지점 볼륨의 증가 hello 공간을 시도 하십시오.
| 백업 | 온라인 복구 지점 생성 실패 | Hello 오류 메시지가 표시 되 면 "hello Windows Azure Backup Agent toohello OBEngine 서비스에 연결할 수 없습니다", OBEngine hello 컴퓨터에서 실행 중인 서비스 hello 목록에 있으면 해당 hello를 확인 합니다. Hello OBEngine 서비스에서 "사용 하 여 hello net start OBEngine" 명령 toostart hello OBEngine 서비스를 실행 하지 않으면 합니다.
| 백업 | 온라인 복구 지점 생성 실패 | Hello 오류 메시지가 표시 되 면 "hello이이 서버에 대 한 암호화의 암호가 설정 되지 않았습니다. 암호화의 암호를 구성하십시오." 오류 메시지가 표시되면 암호화에 사용할 암호를 구성하세요. 실패하면 <br> <ol><li>hello 스크래치 위치 있는지 여부를 확인 합니다. 이름이 "ScratchLocation" hello 레지스트리 HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config에에서 표시 된 hello 위치 존재 해야 합니다.</li><li> Hello 스크래치 위치가 있는 경우 hello 이전 암호를 사용 하 여 다시 등록 해 보십시오. **암호화에 사용할 암호를 구성할 때마다 안전한 위치에 보관하세요.**</li><ol>
| 백업 | BMR에 대한 백업 실패 | BMR 크기가 거 대 한,이 경우 일부 응용 프로그램 파일 tooOS 드라이브를 이동한 후 다시 시도 하십시오. |
| 백업 | 파일/공유 폴더에 액세스하는 동안 오류가 발생했습니다. | 권장 하는 대로 hello 바이러스 백신 설정을 수정 하세요 [여기](https://technet.microsoft.com/library/hh757911.aspx)|
| 백업 | VMware VM에 대한 온라인 복구 지점 생성 작업에 실패했습니다. Tooget 변경 내용 추적 정보를 시도 하는 동안 VMware에서 오류가 발생 했습니다. ErrorCode - FileFaultFault(ID 33621) |  1. Vm을 영향을 받는 hello에 대 한 hello ctk vmware, 다시 설정 <br/> 독립 디스크가 VMWare에 준비되어 있지 않은지 확인 <br/> 영향을 받는 hello Vm에 대 한 보호를 중지 하 고 새로 고침 단추를 다시 보호 <br/> 영향을 받는 hello Vm에 대 한 한 CC 실행|


## <a name="change-passphrase"></a>암호 변경
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 암호 변경 |입력한 보안 PIN이 잘못되었습니다. 올바른 보안 PIN toocomplete hello이이 작업을 제공 합니다. |**원인:**<br/> 이 오류는 중요한 작업(예: 암호 변경)을 수행하는 동안 잘못되거나 만료된 보안 PIN을 입력하는 경우 발생합니다. <br/>**권장 작업:**<br/> toocomplete hello 작업 유효한 보안 PIN을 입력 해야 합니다. tooget hello PIN tooAzure 포털에 로그인 하 고 탐색 tooRecovery 서비스 자격 증명 모음 > 설정 > 속성 > 보안 PIN을 생성 합니다. 이 PIN toochange 암호를 사용 합니다. |
| 암호 변경 |작업이 실패했습니다. ID: 120002 |**원인:**<br/>이 오류에는 보안 설정 사용, toochange 암호 시도 및 지원 되지 않는 버전에 있는 경우 제공 됩니다.<br/>**권장 작업:**<br/> 첫 번째 업데이트 백업 에이전트 toominimum 버전 최소 2.0.9052 및 Azure 백업 서버 toominimum 업데이트 1을 해야 toochange 암호, 유효한 보안 PIN을 입력 합니다. tooget hello PIN tooAzure 포털에 로그인 하 고 탐색 tooRecovery 서비스 자격 증명 모음 > 설정 > 속성 > 보안 PIN을 생성 합니다. 이 PIN toochange 암호를 사용 합니다. |


## <a name="configure-email-notifications"></a>전자 메일 알림 구성
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| Office 365 계정을 사용 하 여 전자 메일 알림 구성 함으로써 tooset을 하려고 합니다. | 오류 ID: 2013 가져오기| **원인:**<br/> Toouse Office 365 계정 시도 <br/> **권장 작업:**<br/> hello 먼저 tooensure 된다는 점입니다 "허용 익명 릴레이에 수신 커넥터" DPM 서버에 대 한 Exchange에서 설치 합니다. 방법에 대 한 링크를 여기 tooconfigure이: http://technet.microsoft.com/en-us/library/bb232021.aspx <br/> 내부 SMTP 릴레이 사용 하는 서버에 Office 365를 사용 하 여를 tooset 필요한 수 없는 경우 설정할 수 있습니다 IIS toobe 릴레이이 있습니다. <br/> Tooconfigure hello DPM 서버 toobe 수 toorelay hello SMTP tooO365 https://technet.microsoft.com/en-us/library/aa995718(v=exchg.65).aspx toosetup IIS toorelay tooO365 IIS를 사용 하 여 필요 합니다. <br/> 중요 정보: 단계 3-g > 있는지 toouse 수, ii-> user@domain.com 형식과 하지 도메인 \ 사용자 <br/> 지점 DPM toouse 포트 587 SMTP 서버로 로컬 servername hello 및 다음 hello 전자 메일에서 발생 해야 하는 사용자 전자 메일을 hello 합니다. <br/> hello 사용자 이름 및 암호 hello DPM SMTP 설정 페이지에 DPM이 hello 도메인의 도메인 계정 이어야 합니다. <br/> 참고: hello SMTP 서버 주소를 변경할 때는 hello toonew 설정 변경, hello 설정 상자 닫은 후 toobe hello 새 값에 적용 되었는지 확인 합니다.  단순히 변경 하 고 테스트는 항상 사용 하지 hello 새 설정을 이러한 방식으로 테스트 하는 것이 좋습니다. <br/> 이 프로세스 중 언제 든 DPM 콘솔을 닫고 hello 다음 레지스트리 키를 편집 하 여 이러한 설정을 지울 수 있습니다.<br/> HKLM\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Notification\ <br/> SMTPPassword 및 SMTPUserName 키를 삭제합니다. <br/> 다시 시작할 때 hello UI에 다시에 추가할 수 있습니다.
