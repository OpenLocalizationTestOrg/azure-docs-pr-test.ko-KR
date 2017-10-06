---
title: "aaaAzure VMware tooAzure에서 사이트 복구 문제 해결 | Microsoft Docs"
description: "Azure 가상 컴퓨터를 복제할 때 오류 문제 해결"
services: site-recovery
documentationcenter: 
author: asgang
manager: srinathv
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/24/2017
ms.author: asgang
ms.openlocfilehash: 912097c8892540dd798ba025e0b10374ca51d664
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>모바일 서비스 강제 설치 문제 해결

이 문서는 보호 사용을 위한 toosource 서버의 tooinstall hello 모바일 서비스를 시도할 때 직면 하는 hello 일반적인 문제를 설명 합니다.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(오류 코드 95107) 보호를 사용하도록 설정할 수 없습니다.
**오류 코드** | **가능한 원인** | **오류 관련 권장 사항**
--- | --- | ---
95107 </br>***메시지-*** 오류 코드로 hello 이동성 서비스 toohello 원본 컴퓨터의 강제 설치 하지 못했습니다. ***EP0858***합니다. <br> Hello 자격 증명을 제공 tooinstall 모바일 서비스는 잘못 되었거나 hello 사용자 계정에 권한이 없습니다. | 사용자 자격 증명 제공 tooinstall 모바일 서비스가 원본 컴퓨터에서 잘못 되었습니다. | 구성 서버에 대 한 hello 원본 컴퓨터에 대해 제공 된 hello 사용자 자격 증명이 올바른지 확인 하십시오. <br> tooadd/편집 사용자 자격 증명: 이동 tooconfiguration 서버 > Cspsconfigtool 아이콘 > 계정을 관리 합니다. </br> 또한 확인 아래 필수 구성 요소는 선택 된 toosuccessfully 완료를 강제 설치 합니다.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(오류 코드 95015) 보호를 사용하도록 설정할 수 없습니다.
**오류 코드** | **가능한 원인** | **오류 관련 권장 사항**
--- | --- | ---
95105 </br>***메시지-*** 오류 코드로 hello 이동성 서비스 toohello 원본 컴퓨터의 강제 설치 하지 못했습니다. ***EP0856***합니다. <br> Hello 원본 컴퓨터에 사용할 수 없습니다 "파일 및 프린터 공유" 또는 hello 프로세스 서버와 hello 소스 컴퓨터 간의 네트워크 연결 문제가 있습니다.| 파일 및 인쇄 공유 사용 안 함 | "파일 및 프린터 공유" hello 원본 컴퓨터에 hello Go toohello 원본 컴퓨터의 Windows 방화벽에서에서 허용 > 아래에서 Windows 방화벽 설정 > "응용 프로그램 또는 기능 방화벽을 통해 허용" > "파일 및 모든 프로필에 대해 프린터 공유"를 선택 합니다. </br> 또한 확인 아래 필수 구성 요소는 선택 된 toosuccessfully 완료를 강제 설치 합니다.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(오류 코드 95117) 보호를 사용하도록 설정할 수 없습니다.
**오류 코드** | **가능한 원인** | **오류 관련 권장 사항**
--- | --- | ---
95117 </br>***메시지-*** 오류 코드로 hello 이동성 서비스 toohello 원본 컴퓨터의 강제 설치 하지 못했습니다. ***EP0865***합니다. <br> Hello 원본 컴퓨터가 실행 되지 않는 또는 hello 프로세스 서버와 hello 소스 컴퓨터 간의 네트워크 연결 문제가 있습니다. | 프로세스 서버와 원본 서버 간의 네트워크 연결 | 프로세스 서버와 원본 서버 간의 연결을 확인합니다. </br> 또한 확인 아래 필수 구성 요소는 선택 된 toosuccessfully 완료를 강제 설치 합니다.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(오류 코드 95103) 보호를 사용하도록 설정할 수 없습니다.
**오류 코드** | **가능한 원인** | **오류 관련 권장 사항**
--- | --- | ---
95103 </br>***메시지-*** 오류 코드로 hello 이동성 서비스 toohello 원본 컴퓨터의 강제 설치 하지 못했습니다. ***EP0854***합니다. <br> "Windows Management Instrumentation (WMI)" hello 원본 컴퓨터에서 허용 되지 않으므로 또는 hello 프로세스 서버와 hello 소스 컴퓨터 간의 네트워크 연결 문제가 있습니다.| Windows Management Instrumentation (WMI) hello Windows 방화벽에서 차단 | Hello Windows 방화벽에서에서 Windows Management Instrumentation (WMI)를 허용 합니다. [Windows 방화벽 설정] 아래에서 > [방화벽을 통해 앱 또는 기능 허용] > [모든 프로필에 대해 WMI 선택]을 선택합니다. </br> 또한 확인 아래 필수 구성 요소는 선택 된 toosuccessfully 완료를 강제 설치 합니다.

## <a name="check-push-install-logs-for-errors"></a>강제 설치 로그에서 오류 확인

Hello 구성/프로세스 서버에서 이동 'PushinstallService'에 있는 toofile <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand hello 소스 hello 문제 및 사용 하 여 아래 단계 tooresolve hello 문제를 해결 합니다.</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Windows에 대한 강제 설치 필수 조건
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>[파일 및 프린터 공유]가 사용하도록 설정되었는지 확인
"파일 및 프린터 공유" 및 "Windows Management Instrumentation" hello 소스 컴퓨터 hello Windows 방화벽에서 허용 </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>원본 컴퓨터가 도메인에 가입된 경우 </br>
GPMC(그룹 정책 관리 콘솔)를 사용하여 방화벽 설정을 구성합니다.
1. 로그인 tooActive 디렉터리 도메인 컴퓨터 관리자 권한으로 연 그룹 정책 관리 콘솔 (GPMC 합니다. 시작 하는 실행 MSC > 실행).</br>
3. GPMC에 설치 되어 있지 않으면 링크를 따라 이동 hello 너무[설치 hello GPMC](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. Hello GPMC 콘솔 트리에서 hello 포리스트 및 도메인의 그룹 정책 개체를 두 번 클릭 하 고 너무 탐색 "기본 도메인 정책"입니다. </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. 마우스 오른쪽 단추로 [기본 도메인 정책] > [편집]을 클릭하면 > 새 [그룹 정책 관리 편집기] 창이 열립니다. </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. Hello 그룹 정책 관리 편집기에서에서 탐색 tooComputer 구성 > 정책 > 관리 템플릿 > 네트워크 > 네트워크 연결 > Windows 방화벽입니다. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. 다음 도메인 프로 파일 및 표준 프로필에 대 한 설정을 hello를 사용 하도록 설정 </br>
a)  예외 [Windows 방화벽: 인바운드 파일 및 프린터 공유 예외 허용]을 두 번 클릭합니다. [사용]을 선택하고 [확인]을 클릭합니다. </br>
a)  예외 [Windows 방화벽: 인바운드 원격 관리 예외 허용]을 두 번 클릭합니다. [사용]을 선택하고 [확인]을 클릭합니다. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>원본 컴퓨터가 도메인에 가입되지 않고 작업 그룹의 일부가 아닌 경우 </br>
원격 컴퓨터에서 방화벽 설정 구성(작업 그룹의 경우):
1. Toohello 원본 컴퓨터를 이동 합니다.</br>
2. [Windows 방화벽 설정] 아래에서 > [방화벽을 통해 앱 또는 기능 허용] > [모든 프로필에 대해 파일 및 프린터 공유]를 선택합니다. </br>
3. [Windows 방화벽 설정] 아래에서 > [방화벽을 통해 앱 또는 기능 허용] > [모든 프로필에 대해 WMI 선택]을 선택합니다. </br>

#### <a name="disable-remote-user-account-control-uac"></a>원격 UAC(사용자 계정 컨트롤)를 사용하지 않도록 설정
레지스트리 키 toopush hello 모바일 서비스를 사용 하 여 UAC 사용 안 함
1. [시작] > [실행] > regedit 입력 > ENTER 키 클릭
2. Hello 다음 레지스트리 하위 키를 누릅니다: 찾아
3. Hello LocalAccountTokenFilterPolicy 레지스트리 항목이 존재 하지 않는 경우 다음이 단계를 따르십시오.
4. Hello 편집 메뉴 > 새로 만들기 > DWORD 값을 클릭 합니다.
5. LocalAccountTokenFilterPolicy를 입력하고 ENTER 키를 누릅니다.
6. LocalAccountTokenFilterPolicy를 마우스 오른쪽 단추로 클릭하고 [수정]을 클릭합니다.
7. Hello 값 데이터 상자에 1를 입력 한 다음 확인을 클릭 합니다.
8. 레지스트리 편집기를 종료합니다.


## <a name="push-install-pre-requisites-for-linux"></a>Linux에 대한 강제 설치 필수 조건:

1. Hello 소스 Linux 서버에 루트 사용자를 만듭니다. (Hello 강제 설치 및 업데이트에 대해서만이 계정을 사용)</br>
2. Hello 소스 Linux 서버에 모든 네트워크 어댑터와 관련 된 hello 로컬 호스트 이름 tooIP 주소 매핑하는 항목에 해당 hello /etc/hosts 파일을 확인 합니다. </br>
3. Hello 최신 openssh, openssh-서버 및 openssl 패키지 원본 Linux 서버에 설치 되어 있는지 확인 합니다. </br>
Ssh 포트 22가 활성화되어 실행 중인지 확인합니다. </br>
4. Hello 원본 서버에서 에이전트의 오래 된 항목이 이미 있는 경우 hello 오래 된 에이전트를 제거 하 고 hello 서버를 다시 부팅, 확인 에이전트를 다시 설치 합니다. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a>Hello sshd_config 파일에서 SFTP 하위 시스템 및 암호 인증을 사용 하도록 설정
1. 원본 서버에서 루트로 로그인합니다. </br>
2. Hello 파일 /etc/ssh/sshd_config 파일에</br> PasswordAuthentication로 시작 하는 hello 줄을 찾습니다. </br>
3. d.   Hello 줄 주석 처리를 제거 하 고 hello "no" 값을 너무 "yes" 변경 합니다. </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. "하위 시스템"로 시작 하는 hello 줄을 찾아 hello 줄 주석 처리를 제거 합니다. </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Hello 변경 내용을 저장 하 고 hello sshd 서비스를 다시 시작 합니다. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>구성/프로세스 서버에서 강제 설치를 확인합니다.
#### <a name="validate-credentials-for-discovery-and-installation"></a>검색 및 설치에 대한 자격 증명 유효성 검사

1. 구성 서버에서 Cspsconfigtool을 시작합니다.</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. 보호에 사용 하는 hello 계정 hello 원본 컴퓨터에 대 한 관리자 권한이 있는지 확인 합니다. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>프로세스 서버와 원본 서버 간의 연결 확인
1. 프로세스 서버에서 인터넷 연결을 확인합니다.
2. wbemtest.exe를 사용하여 WMI 연결을 확인합니다. </br>
Hello 프로세스 서버에서 시작 클릭 > 실행 > wbemtest.exe > 표시 된 것 처럼 Windows Management Instrumentation Tester 창을 열어야 합니다.</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
연결 클릭 > hello Namespace 입력 사용자 이름 및 암호에 hello 원본 서버 IP를 입력 (원본 컴퓨터가 도메인에 가입 된 경우 제공 "domainName\username"으로 사용자 이름과 함께 hello 도메인 이름입니다. 원본 컴퓨터를 작업 그룹에만 hello 사용자 이름을 제공 합니다.) 패킷 개인 정보로 hello 인증 수준을 선택 합니다. </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   [연결]을 클릭합니다. 이제 데이터를 제공 하는 hello로 hello WMI 연결 성공 해야 하며 아래와 같이 hello Windows Management Instrumentation Tester 창 표시 됩니다. </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   WMI 연결이 실패한 경우 오류 메시지가 팝업됩니다. 아래 스크린샷은 hello 응용 프로그램을 허용 하는 Windows 방화벽에서 WMI/원격 관리 설정 하지 않은 경우 실패 한 시도 보여 줍니다. </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. Hello WMI 상태 및 연결을 확인 합니다.</br>
Hello 구성/프로세스 서버에서 </br>
시작 > 실행 > wmimgmt.msc > 작업 > 기타 작업 > tooanother 컴퓨터 (소스 컴퓨터)에 연결 합니다. </br>
연결이 세밀 하 게 보호 및 검사에 사용 되는 hello 계정의 hello 자격 증명을 입력 합니다. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>지정된 자격 증명을 사용하여 원본 컴퓨터의 네트워크 공유 폴더를 PS(프로세스 서버)에서 원격으로 액세스할 수 있는지 확인합니다.
  1. 열려 있는 파일 탐색기, 로그온 tooProcess 서버 (PS) 컴퓨터 > hello 주소 표시줄 글꼴로 > "\\\source-machine-ip\C$" > enter 키를 누릅니다. </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. 파일 탐색기에서 자격 증명을 요청합니다. Hello 사용자 이름 및 암호 입력 > 확인을 클릭 합니다.</br>
   원본 컴퓨터가 도메인에 가입 된 경우에 "domainName\username"으로 사용자 이름과 함께 hello 도메인 이름을 제공 합니다.</br>
   원본 컴퓨터가 작업 그룹에 포함 된 경우만 hello "username"을 제공 합니다. </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. 연결이 성공적이 원격에서 프로세스 서버 (PS) 원본 컴퓨터의 hello 폴더를 볼 수 있습니다. </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> 연결에 실패한 경우 모든 필수 조건을 충족하는지 확인하세요.
>

"Windows Management Instrumentation" tooopen 사용 하지 않으려는 경우 또한 수동으로 설치할 수 있습니다 모바일 서비스 hello 원본 컴퓨터에 있습니다.</br> [GUI를 통해 모바일 서비스 수동 설치](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[구성 관리자를 통한 설치 지침](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>다음 단계
- [VMware 가상 컴퓨터의 복제 설정](vmware-walkthrough-enable-replication.md)
