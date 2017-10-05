---
title: "Azure Backup Server 문제 해결 | Microsoft Docs"
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
ms.openlocfilehash: 5672bb1e17dac4ae0aaa67f936676d6c2fc5ef12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-azure-backup-server"></a>Azure Backup Server 문제 해결

다음 표에 나열된 정보를 참조하여 Azure Backup Server를 사용하는 동안 발생하는 오류를 해결할 수 있습니다.


## <a name="installation-issues"></a>설치 문제

| 작업 | 오류 세부 정보 | 해결 방법 |
|-----------|---------------|------------|
|설치 | 설치 프로그램이 레지스트리 메타데이터를 업데이트할 수 없습니다. 이 업데이트 오류로 인해 저장소가 지나치게 사용될 수 있습니다. 이 문제를 방지하려면 ReFS Trimming 레지스트리 항목을 업데이트하세요. | 레지스트리 키 SYSTEM\CurrentControlSet\Control\FileSystem\RefsEnableInlineTrim을 조정합니다. Dword 값을 1로 설정합니다. |
|설치 | 설치 프로그램이 레지스트리 메타데이터를 업데이트할 수 없습니다. 이 업데이트 오류로 인해 저장소가 지나치게 사용될 수 있습니다. 이 문제를 방지하려면 Volume SnapOptimization 레지스트리 항목을 업데이트하세요. | 빈 문자열 값을 사용하여 레지스트리 키 SOFTWARE\Microsoft Data Protection Manager\Configuration\VolSnapOptimization\WriteIds를 만듭니다. |

## <a name="registration-and-agent-related-issues"></a>등록 및 에이전트 관련 문제
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 자격 증명 모음에 등록 | 잘못된 자격 증명 모음이 제공되었습니다. 파일이 손상되었거나 복구 서비스와 연결된 최신 자격 증명이 없습니다. | 이 오류를 해결하려면  <ol><li> 자격 증명 모음에서 최신 자격 증명 파일을 다운로드하고 다시 시도합니다. <br>또는</li> <li> 위의 작업이 작동하지 않으면 자격 증명을 다른 로컬 디렉터리에 다운로드하거나 새 자격 증명 모음을 만듭니다. <br>또는</li> <li> [이 블로그](https://azure.microsoft.com/blog/troubleshooting-common-configuration-issues-with-azure-backup/)에 명시된 대로 날짜 및 시간 설정을 업데이트해 봅니다. <br>또는</li> <li> c:\windows\temp에 65000개 이상의 파일이 있는지 확인합니다. 오래된 파일을 다른 위치에 이동하거나 임시 폴더의 항목을 삭제합니다. <br>또는</li> <li> 인증서의 상태를 확인합니다. <br> a. "컴퓨터 인증서 관리"(제어판에서)를 엽니다. <br> b. "개인" 노드 및 자식 노드 "인증서"를 확장합니다. <br> c.  인증서 "Miscrosoft Azure Tools"를 제거합니다. <br> d. Azure Backup 클라이언트에서 등록을 다시 시도합니다. <br> 또는 </li> <li> 그룹 정책이 구현되어 있는지 확인합니다. </li></ol> |
| 보호된 서버에 에이전트 푸시 | \<ServerName>에서 DPM 에이전트 코디네이터 서비스와 통신 오유로 인해 에이전트 작업에 실패했습니다. | **제품에 표시된 권장 작업이 작동하지 않는 경우**, <ol><li> 신뢰할 수 없는 도메인에서 컴퓨터를 연결하는 경우 [다음](https://technet.microsoft.com/library/hh757801(v=sc.12).aspx) 단계를 따르세요. <br> 또는 </li><li> 신뢰할 수 있는 도메인에서 컴퓨터를 연결하는 경우 [이 블로그](https://blogs.technet.microsoft.com/dpm/2012/02/06/data-protection-manager-agent-network-troubleshooting/)에 간략히 설명된 단계를 따르세요. <br>또는</li><li> 문제 해결 단계로 바이러스 백신을 사용하지 않도록 설정합니다. 문제가 해결되면 바이러스 백신 설정을 [이 문서](https://technet.microsoft.com/library/hh757911.aspx)에 제안된 대로 수정합니다.</li></ol> |
| 보호된 서버에 에이전트 푸시 | 서버에 대해 지정된 자격 증명이 올바르지 않습니다. | **제품에 표시된 권장 작업이 작동하지 않는 경우**, <br> [이 문서](https://technet.microsoft.com/library/hh758186(v=sc.12).aspx#BKMK_Manual)에 지정된 대로 프로덕션 서버에 보호 에이전트를 수동으로 설치합니다.|
| Azure Backup Agent가 Azure Backup 서비스에 연결할 수 없습니다(ID: 100050). | Azure Backup Agent가 Azure Backup 서비스에 연결할 수 없습니다. | **제품에 표시된 권장 작업이 작동하지 않는 경우**, <br>1. 관리자 권한 프롬프트에서 다음 명령을 실행합니다. psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe" Internet Explorer 창이 열립니다. <br/> 2. 도구 -> 인터넷 옵션 -> 연결 -> LAN 설정으로 이동합니다. <br/> 3. 시스템 계정에 대한 프록시 설정을 확인합니다. 프록시 IP 및 포트를 설정합니다. <br/> 4. Internet Explorer를 닫습니다.|
| Azure Backup Agent 설치 실패 | Microsoft Azure Recovery Services 설치에 실패했습니다. 시스템에 Microsoft Azure Recovery Services 설치로 인한 모든 변경 사항은 롤백되었습니다. (ID: 4024) | Azure Agent 수동 설치


## <a name="configuring-protection-group"></a>보호 그룹 구성
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 보호 그룹 구성 | DPM은 보호된 컴퓨터(보호된 컴퓨터 이름)에 응용 프로그램 구성 요소를 열거할 수 없습니다. | 관련 데이터 원본/구성 요소 수준의 보호 그룹 구성 UI 화면에서 '새로 고침'을 클릭합니다. |
| 보호 그룹 구성 | 보호를 구성할 수 없음 | 보호된 서버가 SQL Server인 경우 [이 문서](https://technet.microsoft.com/library/hh757977(v=sc.12).aspx)에 명시된 대로 보호된 컴퓨터에 대한 시스템 계정(NTAuthority\System)에 sysadmin 역할 권한이 제공되었는지 확인하세요.
| 보호 그룹 구성 | 이 보호 그룹에 대한 저장소 풀에 여유 공간이 부족합니다. | 저장소 풀에 추가된 디스크는 [파티션을 포함해야 합니다](https://technet.microsoft.com/library/hh758075(v=sc.12).aspx). 디스크에서 기존 볼륨을 삭제한 후 저장소 풀에 추가합니다.|
| 정책 변경 |백업 정책을 수정할 수 없습니다. 오류: 내부 서비스 오류 [0x29834]로 인해 현재 작업이 실패했습니다. 잠시 후 작업을 다시 시도하세요. 문제가 지속되면 Microsoft 지원에 문의하세요. |**원인:**<br/>이 오류는 보안 설정이 활성화되고 위에서 지정된 최소값 미만으로 보존 범위를 줄이려고 하고 지원되지 않는 버전(MAB 버전 2.0.9052 및 Azure Backup Server 업데이트 1 이전)에 있는 경우 발생합니다. <br/>**권장 작업:**<br/> 이 경우 정책 관련 업데이트를 계속 진행할 수 있도록 지정된 최소 보존 기간(매일 7일, 매주 4주, 매달 3주 또는 매년 1년) 이상으로 보존 기간을 설정해야 합니다. 필요에 따라 선호되는 방법은 백업 에이전트 및 Azure Backup Server를 업데이트하여 모든 보안 업데이트를 활용하는 것입니다. |

## <a name="backup"></a>백업
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 백업 | 복제본이 불일치 | 복제본 불일치 원인에 대한 자세한 내용과 관련 제안 사항은 [여기](https://technet.microsoft.com/library/cc161593.aspx)에서 확인할 수 있습니다. <br> <ol><li> 시스템 상태/BMR 백업의 경우 보호된 서버에 Windows Server 백업이 설치되어 있는지 여부를 확인하세요. </li><li> DPM/MABS 서버의 DPM 저장소 풀에서 공간 관련 문제를 확인하고 필요에 따라 저장소를 할당합니다. </li><li> 보호된 서버에서 볼륨 섀도 복사 서비스의 상태를 확인합니다. 비활성 상태인 경우 수동으로 시작하도록 설정하거나 서버에서 서비스를 시작합니다. 그런 다음 DPM/MABS 콘솔로 다시 돌아가 일관성 검사 작업과 동기화를 시작합니다.</li></ol>|
| 백업 | 작업을 실행하는 동안 예기치 않은 오류가 발생했습니다. 장치가 준비되지 않았습니다. | **제품에 표시된 권장 작업이 작동하지 않는 경우**, <br> <ol><li>섀도 복사 저장소 공간을 보호 그룹의 항목에서 무제한으로 설정하고 일관성 검사를 실행합니다. <br></li> 또는 <li>기존 보호 그룹을 삭제하고 안에 개별 항목이 들어 있는 새로운 그룹을 여러 개 만듭니다.</li></ol> |
| 백업 | 시스템 상태만 백업하는 경우 보호된 컴퓨터에 시스템 상태 백업을 저장하기에 충분한 여유 공간이 있는지 확인합니다. | <ol><li>보호된 컴퓨터에 WSB가 설치되어 있는지 확인합니다.</li><li>시스템 상태에 대해 보호된 컴퓨터에 충분한 공간이 있는지 확인합니다. 이 작업을 수행하는 가장 쉬운 방법은 보호된 컴퓨터로 이동하여 WSB를 열고 선택 항목을 클릭하고 BMR을 선택하는 것입니다. 그러면 UI에 이 작업을 위해 얼마나 많은 공간이 필요한지 표시됩니다. WSB를 열고 -> 로컬 백업 -> 백업 일정 -> 백업 구성 선택 -> 전체 서버를 선택합니다(크기가 표시됨). 검증에 이 크기를 사용합니다.</li></ol>
| 백업 | 온라인 복구 지점 생성 실패 | "Miscrosoft Azure Backup Agent에서 선택한 볼륨의 스냅숏을 만들 수 없습니다." 오류 메시지가 표시되면 복제본 및 복구 지점 볼륨에서 공간을 늘려 보세요.
| 백업 | 온라인 복구 지점 생성 실패 | "Windows Azure Backup Agent에서 OBEngine 서비스에 연결할 수 없습니다." 오류 메시지가 나타나면 컴퓨터에서 실행 중인 서비스 목록에 OBEngine이 있는지 확인합니다. OBEngine 서비스가 실행 중이 아닌 경우 "net start OBEngine" 명령을 사용하여 OBEngine 서비스를 시작합니다.
| 백업 | 온라인 복구 지점 생성 실패 | "이 서버의 암호화에 사용할 암호가 설정되어 있지 않습니다. 암호화의 암호를 구성하십시오." 오류 메시지가 표시되면 암호화에 사용할 암호를 구성하세요. 실패하면 <br> <ol><li>스크래치 위치가 존재하는지 여부를 확인합니다. 레지스트리 HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config에 언급된 위치에 "ScratchLocation" 이름이 존재해야 합니다.</li><li> 스크래치 위치가 존재하는 경우 이전 암호를 사용하여 다시 등록하세요. **암호화에 사용할 암호를 구성할 때마다 안전한 위치에 보관하세요.**</li><ol>
| 백업 | BMR에 대한 백업 실패 | BMR 크기가 매우 큰 경우 일부 응용 프로그램 파일을 OS 드라이브로 이동한 후 다시 시도합니다. |
| 백업 | 파일/공유 폴더에 액세스하는 동안 오류가 발생했습니다. | [여기](https://technet.microsoft.com/library/hh757911.aspx)에 제안된 대로 바이러스 백신 설정을 수정해 봅니다.|
| 백업 | VMware VM에 대한 온라인 복구 지점 생성 작업에 실패했습니다. DPM이 ChangeTracking 정보를 가져오는 동안 VMware에서 오류가 발생했습니다. ErrorCode - FileFaultFault(ID 33621) |  1. 영향을 받는 VM에 대해 VMWare에서 ctk 재설정 <br/> 독립 디스크가 VMWare에 준비되어 있지 않은지 확인 <br/> 영향을 받는 VM에 대한 보호를 중지하고 새로 고침 단추로 다시 보호 <br/> 영향을 받는 VM에 대해 CC 실행|


## <a name="change-passphrase"></a>암호 변경
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 암호 변경 |입력한 보안 PIN이 잘못되었습니다. 이 작업을 완료하려면 올바른 보안 PIN을 입력하세요. |**원인:**<br/> 이 오류는 중요한 작업(예: 암호 변경)을 수행하는 동안 잘못되거나 만료된 보안 PIN을 입력하는 경우 발생합니다. <br/>**권장 작업:**<br/> 작업을 완료하려면 유효한 보안 PIN을 입력해야 합니다. PIN을 가져오려면 Azure Portal에 로그인하고 [Recovery Services 자격 증명 모음] > [설정] > [속성] > [보안 PIN 생성]으로 이동합니다. 이 PIN을 사용하여 암호를 변경합니다. |
| 암호 변경 |작업이 실패했습니다. ID: 120002 |**원인:**<br/>이 오류는 보안 설정이 활성화되고 암호를 변경하려고 하고 지원되지 않는 버전에 있는 경우 발생합니다.<br/>**권장 작업:**<br/> 암호를 변경하려면 먼저 백업 에이전트를 최소 버전 최소 2.0.9052로, Azure Backup Server를 최소 업데이트 1로 업데이트한 다음 유효한 보안 PIN을 입력해야 합니다. PIN을 가져오려면 Azure Portal에 로그인하고 [Recovery Services 자격 증명 모음] > [설정] > [속성] > [보안 PIN 생성]으로 이동합니다. 이 PIN을 사용하여 암호를 변경합니다. |


## <a name="configure-email-notifications"></a>전자 메일 알림 구성
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| Office 365 계정을 사용하여 전자 메일 알림을 설정하려고 합니다. | 오류 ID: 2013 가져오기| **원인:**<br/> Office 365 계정을 사용하려고 합니다. <br/> **권장 작업:**<br/> 가장 먼저 Exchange에서 DPM 서버에 대해 “Allow Anonymous Relay on a Receive Connector”(수신 커넥터에서 익명 릴레이 허용)가 설정되어 있는지 확인해야 합니다. 구성 방법에 대한 링크가 있습니다. http://technet.microsoft.com/en-us/library/bb232021.aspx <br/> 내부 SMTP 릴레이를 사용할 수 없고 Office 365 서버를 사용하여 설정해야 할 경우 IIS가 릴레이가 되도록 설정할 수 있습니다. <br/> IIS를 사용하여 SMTP를 O365로 릴레이할 수 있도록 DPM 서버를 구성해야 합니다(https://technet.microsoft.com/en-us/library/aa995718(v=exchg.65).aspx) O365로 릴레이하도록 IIS 설정 <br/> 중요 정보: 3단계->g->ii에서 반드시 domain\user가 아닌 user@domain.com 형식을 사용하세요. <br/> DPM을 SMTP 서버, 포트 587로 로컬 서버 이름을 사용하도록 지정하면 사용자에게 전자 메일이 전송됩니다. <br/> DPM SMTP 설정 페이지의 사용자 이름과 암호는 DPM이 사용 설정되어 있는 도메인 계정이어야 합니다. <br/> 참고: SMTP 서버 주소를 변경할 경우 새 설정으로 변경하고 설정 상자를 닫은 후 다시 열어 새 값이 적용되었는지 확인하세요.  단순히 변경 및 테스트한다고 해서 새 설정이 적용되는 것은 아니므로, 이 방법으로 테스트하는 것이 모범 사례입니다. <br/> 이 프로세스 중 언제라도 DPM 콘솔을 닫고 다음 레지스트리 키를 편집하여 이러한 설정을 정리할 수 있습니다.<br/> HKLM\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Notification\ <br/> SMTPPassword 및 SMTPUserName 키를 삭제합니다. <br/> 다시 시작할 때 UI에 다시 추가할 수 있습니다.
