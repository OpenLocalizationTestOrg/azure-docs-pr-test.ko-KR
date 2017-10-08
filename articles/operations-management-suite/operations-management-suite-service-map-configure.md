---
title: "Operations Management Suite에서 서비스 맵을 aaaConfigure | Microsoft Docs"
description: "서비스 맵을 Windows에서 응용 프로그램 구성 요소를 자동으로 검색 하는 Operations Management Suite 솔루션 및 Linux 시스템 및 지도 hello 서비스 간의 통신 합니다. 이 문서에서는 사용자 환경에 서비스 맵을 배포하고 다양한 시나리오에서 사용하는 것에 대해 자세히 설명합니다."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>Operations Management Suite의 서비스 맵 구성
Windows 및 Linux 시스템에서 응용 프로그램 구성 요소를 자동으로 검색 하는 서비스 지도 및 지도 hello 서비스 간의 통신 합니다. Tooview 때 서버-으로 볼 중요 한 서비스를 제공 하는 상호 연결 된 시스템 사용할 수 있습니다. 서비스 맵은 서버, 프로세스 및 에이전트 설치 이외에 구성이 필요 없는 TCP 연결 아키텍처의 포트 간 연결을 보여 줍니다.

이 문서에서는 서비스 맵 및 온 보 딩 에이전트 구성의 hello 세부 정보를 설명 합니다. 서비스 맵을 사용 하는 방법은 참조 하십시오. [hello 서비스 맵 솔루션을 사용 하 여 Operations Management Suite에서](operations-management-suite-service-map.md)합니다.

## <a name="dependency-agent-downloads"></a>종속성 에이전트 다운로드
| 파일 | OS | 버전 | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>연결된 소스
서비스 맵을 hello Microsoft 종속성 에이전트가에서 해당 데이터를 가져옵니다. hello 종속성 에이전트가 OMS 에이전트의 연결 tooOperations Management Suite에 대 한 hello에 따라 달라 집니다. 이 서버 hello OMS 에이전트 설치 및 구성 놓은 다음 hello 종속성 에이전트를 설치할 수 있어야 함을 의미 합니다. hello 다음 설명 hello 서비스 맵 솔루션을 지원 하는 hello 연결 원본입니다.

| 연결된 원본 | 지원됨 | 설명 |
|:--|:--|:--|
| Windows 에이전트 | 예 | 서비스 맵은 Windows 에이전트 컴퓨터에서 데이터를 분석하고 수집합니다. <br><br>또한 toohello에서 [OMS 에이전트](../log-analytics/log-analytics-windows-agents.md), Windows 에이전트 hello Microsoft 종속성 에이전트가 필요 합니다. Hello 참조 [지원 되는 운영 체제](#supported-operating-systems) 운영 체제 버전의 전체 목록은 합니다. |
| Linux 에이전트 | 예 | 서비스 맵은 Linux 에이전트 컴퓨터에서 데이터를 분석하고 수집합니다. <br><br>또한 toohello에서 [OMS 에이전트](../log-analytics/log-analytics-linux-agents.md), Linux 에이전트 hello Microsoft 종속성 에이전트가 필요 합니다. Hello 참조 [지원 되는 운영 체제](#supported-operating-systems) 운영 체제 버전의 전체 목록은 합니다. |
| System Center Operations Manager 관리 그룹 | 예 | 서비스 맵은 연결된 [System Center Operations Manager 관리 그룹](../log-analytics/log-analytics-om-agents.md)의 Windows 및 Linux 에이전트에서 데이터를 분석하고 수집합니다. <br><br>Hello System Center Operations Manager 에이전트 컴퓨터 tooOperations의 직접 연결 관리 제품군은 필수입니다. Hello 관리 그룹 toohello Operations Management Suite 리포지토리에서 데이터가 전달 됩니다.|
| Azure Storage 계정 | 아니요 | 서비스 맵을 데이터 수집 에이전트 컴퓨터에서에서 데이터가 없는 이므로 Azure 저장소에서 toocollect 합니다. |

서비스 맵은 64비트 플랫폼만 지원합니다.

Windows에서 Microsoft Monitoring Agent (MMA) hello System Center Operations Manager 및 Operations Management Suite toogather과 송신 모니터링 데이터에 사용 됩니다. (이 에이전트 hello 컨텍스트에 따라 System Center Operations Manager 에이전트, OMS 에이전트, 로그 분석 에이전트, MMA, 또는 직접 에이전트 hello 라고 합니다.) System Center Operations Manager 및 Operations Management Suite는 MMA hello의 다양 한 hello 아웃 상자 버전을 제공합니다. 이러한 버전 수 각각 보고 tooSystem Center Operations Manager, tooOperations 관리 도구 모음 또는 tooboth 합니다.  

Linux에서 Linux 수집 및 모니터링 데이터 tooOperations 관리 제품군을 사용 하는 전송에 대 한 OMS 에이전트를 hello 합니다. System Center Operations Manager 관리 그룹을 통해 연결 된 tooOperations 관리 제품군을 사용 하는 서버 또는 OMS 직접 에이전트를 사용 하는 서버에서 서비스 맵을 사용할 수 있습니다.  

이 문서에서는 지칭 tooall 에이전트-여부 Linux 또는 Windows에 있는지 여부를 "OMS 에이전트입니다." hello tooa System Center Operations Manager 관리 그룹 또는 직접 tooOperations 관리 도구 모음-연결 컨텍스트에 대 한 필요한 경우에 hello 에이전트의 hello 특정 배포 이름을 사용 합니다.

hello 서비스 맵 에이전트 자체 데이터를 전송 하지 않습니다 하 고 모든 변경 내용 toofirewalls 또는 포트 필요 하지 않습니다. 서비스 맵에서 hello 데이터는 직접 또는 hello OMS 게이트웨이 통해 hello OMS 에이전트 tooOperations Management Suite에서 항상 전송 됩니다.

![서비스 맵 에이전트](media/oms-service-map/agents.png)

관리 그룹 연결 tooOperations Management Suite는 System Center Operations Manager 고객 인 경우

- System Center Operations Manager 에이전트 hello 인터넷 tooconnect tooOperations Management Suite에 액세스할 수 있도록 하는 경우 추가 구성이 필요 하지 않습니다.  
- System Center Operations Manager 에이전트에 액세스할 수 없으면 Operations Management Suite hello 인터넷을 통해 System Center Operations manager tooconfigure hello OMS 게이트웨이 toowork를 해야 합니다.
  
Hello OMS 직접 에이전트를 사용 하는 경우 tooconnect tooOperations 관리 제품군 또는 tooyour OMS 게이트웨이 tooconfigure hello OMS 에이전트 자체 필요 합니다. hello OMS 게이트웨이에서 다운로드할 수 있습니다 hello [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=52666)합니다.

### <a name="management-packs"></a>관리 팩
서비스 맵을 Operations Management Suite 작업 영역에서 활성화 되 면 300 KB 관리 팩 해당 작업 영역에서 tooall hello Windows 서버 전송 됩니다. System Center Operations Manager 에이전트를 사용 하는 경우는 [연결 된 관리 그룹](../log-analytics/log-analytics-om-agents.md), System Center Operations Manager에서 서비스 맵을 관리 팩 hello를 배포 합니다. Hello 에이전트 직접 연결 되어 있는 경우 Operations Management Suite는 hello 관리 팩을 제공 합니다.

관리 팩 hello Microsoft.IntelligencePacks.ApplicationDependencyMonitor 라고 합니다. 서 면된 too%Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\ 합니다. hello 데이터 소스 hello 관리 팩을 사용 하는 % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID > \ \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll 합니다.

## <a name="installation"></a>설치
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a>Microsoft Windows에 hello 종속성 에이전트 설치
관리자 권한이 필요한 tooinstall 인지 hello 에이전트를 제거 합니다.

hello 종속성 에이전트 InstallDependencyAgent Windows.exe를 통해 Windows 컴퓨터에 설치 됩니다. 옵션 없이이 실행 파일을 실행 하는 경우에 마법사를 대화형으로 tooinstall을 따를 수 시작 합니다.  

각 Windows 컴퓨터에서 단계 tooinstall hello 종속성 에이전트 다음 hello를 사용 합니다.

1.  설치에 hello 지침을 사용 하 여 OMS 에이전트 hello [연결 Windows 컴퓨터 toohello azure에서 로그 분석 서비스](../log-analytics/log-analytics-windows-agents.md)합니다.
2.  Hello Windows 에이전트를 다운로드 하 고 다음 명령을 hello를 사용 하 여 실행. <br>`InstallDependencyAgent-Windows.exe`
3.  Hello 마법사 tooinstall hello 에이전트를 따릅니다.
4.  Hello 종속성 에이전트 toostart 실패 하면 자세한 오류 정보에 대 한 hello 로그를 확인 합니다. Windows 에이전트에서 hello 로그 디렉터리는 %Programfiles%\Microsoft 종속성 Agent\logs입니다. 

#### <a name="windows-command-line"></a>Windows 명령줄
Hello 테이블 tooinstall 명령줄에서 다음에서 옵션을 사용 합니다. toosee hello를 사용 하 여 hello 설치 관리자를 실행 한 hello 설치 플래그 목록은 /? 플래그를 사용하여 설치 관리자를 실행합니다.

    InstallDependencyAgent-Windows.exe /?

| 플래그 | 설명 |
|:--|:--|
| /? | Hello 명령줄 옵션의 목록을 가져옵니다. |
| /S | 사용자 프롬프트 없이 자동 설치를 수행합니다. |

Hello Windows 종속성 에이전트에 대 한 파일은 기본적으로 C:\Program Files\Microsoft 종속성 에이전트에 배치 됩니다.

### <a name="install-hello-dependency-agent-on-linux"></a>Linux에서 hello 종속성 에이전트를 설치 합니다.
루트 액세스가 필요한 tooinstall 되었거나 hello 에이전트를 구성 합니다.

hello 종속성 에이전트 InstallDependencyAgent Linux64.bin, 자동 압축 풀기 이진과 셸 스크립트를 통해 Linux 컴퓨터에 설치 됩니다. 사용 하 여 sh hello 파일을 실행 하거나 추가할 수 있습니다 권한 toohello 파일 자체를 실행 합니다.
 
Hello 단계 tooinstall hello 종속성 에이전트는 각 Linux 컴퓨터에서 다음을 사용 합니다.

1.  설치에 hello 지침을 사용 하 여 OMS 에이전트 hello [수집 및 Linux 컴퓨터에서 데이터를 관리](https://technet.microsoft.com/library/mt622052.aspx)합니다.
2.  다음 명령을 hello를 사용 하 여 루트로 hello Linux 종속성 에이전트를 설치 합니다.<br>`sh InstallDependencyAgent-Linux64.bin`
3.  Hello 종속성 에이전트 toostart 실패 하면 자세한 오류 정보에 대 한 hello 로그를 확인 합니다. Linux 에이전트 hello 로그 디렉터리는 /var/opt/microsoft/dependency-agent/log입니다.

hello 설치 플래그를 사용 하는 hello 설치 프로그램을 실행 목록 toosee hello-도움말 플래그 다음과 같습니다.

    InstallDependencyAgent-Linux64.bin -help

| 플래그 | 설명 |
|:--|:--|
| -help | Hello 명령줄 옵션의 목록을 가져옵니다. |
| -s | 사용자 프롬프트 없이 자동 설치를 수행합니다. |
| --check | 사용 권한 및 hello 운영 체제를 확인 하십시오. 하지만 hello 에이전트를 설치 하지 마십시오. |

Hello 종속성 에이전트에 대 한 파일은 다음 디렉터리 hello에 배치 됩니다.

| 파일 | 위치 |
|:--|:--|
| 코어 파일 | /opt/microsoft/dependency-agent |
| 로그 파일 | /var/opt/microsoft/dependency-agent/log |
| 구성 파일 | /etc/opt/microsoft/dependency-agent/config |
| 서비스 실행 파일 | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| 이진 저장소 파일 | /var/opt/microsoft/dependency-agent/storage |

## <a name="installation-script-examples"></a>설치 스크립트 예제
tooeasily 한 번에 많은 서버에 hello 종속성 에이전트를 배포, toouse 스크립트는 데 도움이 됩니다. 다음 스크립트 예제 toodownload hello를 사용 하 고 Windows 또는 Linux hello 종속성 에이전트를 설치할 수 있습니다.

### <a name="powershell-script-for-windows"></a>Windows용 PowerShell 스크립트
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>Linux용 셸 스크립트
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a>필요한 상태 구성
toodeploy hello 종속성 에이전트 필요한 상태 구성을 통해 hello xPSDesiredStateConfiguration 모듈 및 약간의 hello 다음과 같은 코드를 사용할 수 있습니다.
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a>제거
### <a name="uninstall-hello-dependency-agent-on-windows"></a>Hello Windows에서 종속성 에이전트 제거
관리자는 hello 종속성 에이전트에 대 한 Windows 제어판을 통해 제거할 수 있습니다.

관리자는 %Programfiles%\Microsoft 종속성 Agent\Uninstall.exe toouninstall hello 종속성 에이전트를 실행할 수도 있습니다.

### <a name="uninstall-hello-dependency-agent-on-linux"></a>Hello Linux에서 종속성 에이전트 제거
toocompletely 제거 hello Linux에서 종속성 에이전트, hello 에이전트 자체를 제거 하 고 hello 에이전트와 함께 자동으로 설치 되는 커넥터 hello 해야 합니다. 다음 단일 명령을 hello를 사용 하 여 두를 제거할 수 있습니다.

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>문제 해결
서비스 맵을 설치하거나 실행하는 데 문제가 있으면 이 섹션이 도움이 될 수 있습니다. 그래도 문제를 해결할 수 없으면 Microsoft 지원에 문의해 주세요.

### <a name="dependency-agent-installation-problems"></a>종속성 에이전트 설치 문제
#### <a name="installer-asks-for-a-reboot"></a>설치 관리자에서 다시 부팅을 요청함
hello 종속성 에이전트 *일반적으로* 설치 또는 제거 시 다시 부팅이 필요 하지 않습니다. 그러나 특정 드문 경우 지만 Windows 서버 설치와 함께 다시 부팅 toocontinue가 필요합니다. 이 일반적으로 hello Microsoft Visual c + + 재배포 가능 패키지, 종속성, 잠긴된 된 파일로 인해 다시 부팅 해야 하는 경우 발생 합니다.

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a>메시지 "수 없습니다 종속성 에이전트 tooinstall: Visual Studio 런타임 라이브러리 tooinstall 실패 했습니다 (코드 [code_number] =)" 표시

Microsoft 종속성 에이전트가 hello hello Microsoft Visual Studio 런타임 라이브러리를 기반으로 합니다. Hello 라이브러리를 설치 하는 동안 문제가 없는 경우 메시지를 얻을 수 있습니다. 

hello 런타임 라이브러리 설치 관리자는 hello %LOCALAPPDATA%\temp 폴더에 로그를 만듭니다. hello 파일은 dd_vcredist_arch_yyyymmddhhmmss.log, 여기서 *arch* "amd64" 또는 "x86" 및 *yyyymmddhhmmss* hello 날짜와 시간 (24 시간제) hello 로그를 만들 때입니다. hello 로그는 설치를 차단 하는 hello 문제에 대 한 세부 정보를 제공 합니다.

것이 유용한 tooinstall hello [최신 런타임 라이브러리](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) 직접 첫 번째입니다.

hello 다음 표에 코드 번호 및 권장된 해결 방안과 있습니다.

| 코드 | 설명 | 해결 방법 |
|:--|:--|:--|
| 0x17 | hello 라이브러리 설치 관리자 설치 실패 하는 Windows 업데이트가 필요 합니다. | Hello 가장 최근의 라이브러리 설치 관리자 로그를 확인 하십시오.<br><br>참조를 너무 "Windows8.1 KB2999226 x64.msu" 다음 줄 "0x80240017 오류: 실패 한 tooexecute MSU 패키지를" hello 필수 구성 요소 tooinstall KB2999226 필요가 없습니다. Hello hello 필수 구성 요소에서 지침에 따라 [windows에서 유니버설 C 런타임](https://support.microsoft.com/kb/2999226)합니다. Windows Update toorun 할 수도 있으며 순서 tooinstall hello 필수 구성 요소에 여러 번 다시 부팅 수 있습니다.<br><br>Hello Microsoft 종속성 에이전트가 설치를 다시 실행 합니다. |

### <a name="post-installation-issues"></a>사후 설치 문제
#### <a name="server-doesnt-appear-in-service-map"></a>서버가 서비스 맵에 표시되지 않습니다.
종속성 에이전트 설치 성공 했지만 서버 hello 서비스 맵 솔루션에에서 표시 되지 않는 경우:
* Hello 종속성 에이전트가 성공적으로 설치 되어 있습니까? Hello 서비스를 설치 하는 경우 toosee 확인 하 고 실행 하 여이 확인할 수 있습니다.<br><br>
**Windows**: "Microsoft 종속성 에이전트가." 라는 hello 서비스에 대 한 확인<br>
**Linux**: "microsoft-종속성-에이전트가." 프로세스를 실행 하는 hello에 대 한 확인

* Hello에 연결 되어 [무료 가격 책정 계층 Operations Management Suite/로그 분석의](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? toofive 고유 서비스 맵 서버를에 대 한 hello 무료 계획에서 허용 됩니다. Hello 이전 5 개 더 이상 데이터를 보내는 경우에 서비스 맵에서 모든 후속 서버에 표시 되지 않습니다.

* 서버 보내는 로그 및 성능 데이터 tooOperations 관리 도구 모음 이란? 검색 tooLog 이동한 hello 다음 컴퓨터에 대 한 쿼리를 실행 합니다. 

        * Computer="<your computer name here>" | measure count() by Type
        
  Hello 결과에 다양 한 이벤트를 발전할 수 있습니까? Hello 데이터는 이른? 이 경우에 OMS 에이전트 제대로 작동 및 hello Operations Management Suite 서비스와 통신 합니다. 그렇지 않은 경우 확인 서버에 OMS 에이전트 hello: [Windows 용 OMS 에이전트 문제 해결](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) 또는 [문제 해결 Linux 용 OMS 에이전트](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md)합니다.

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>서버가 서비스 맵에 표시되지만 프로세스가 없습니다.
서버에서 서비스 맵을 표시 되는데 해당 hello 나타내는 없는 프로세스 또는 연결 데이터 종속성 에이전트가 설치 되어 실행, 있지만 hello 커널 드라이버 로드 하지 못했습니다. 

Hello C:\Program Files\Microsoft 종속성 Agent\logs\wrapper.log 파일 (Windows) 또는 /var/opt/microsoft/dependency-agent/log/service.log 파일 (Linux)를 확인 합니다. hello 파일의 마지막 줄 hello는 hello 커널 로드 하지 못했습니다. 이유를 나타냅니다. 예를 들어 hello 커널 지원 되지 않는 linux 사용자 커널을 업데이트 합니다.

## <a name="data-collection"></a>데이터 수집
각 에이전트 tootransmit 대략 예상할 수 있는 복잡 한 정도 시스템 종속성이이 따라 하루 25MB입니다. 각 에이전트는 15초마다 서비스 맵 종속성 데이터를 보냅니다.  

hello 종속성 에이전트는 일반적으로 시스템 메모리의 0.1% 및 0.1% 시스템 CPU 소비 합니다.

## <a name="supported-azure-regions"></a>지원되는 Azure 지역
서비스 맵을 hello 다음 Azure 지역에서에서 현재 제공 됩니다.
- 미국 동부
- 서유럽
- 미국 중서부


## <a name="supported-operating-systems"></a>지원되는 운영 체제
hello 다음 섹션에 나열 hello 종속성 에이전트에 대 한 운영 체제 hello 지원 합니다. 서비스 맵은 모든 운영 체제의 32비트 아키텍처를 지원하지 않습니다.

### <a name="windows-server"></a>Windows Server
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

### <a name="windows-desktop"></a>Windows 데스크톱
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux 및 Oracle Linux(RHEL 커널 포함)
- 기본 및 SMP Linux 커널 릴리스만 지원됩니다.
- PAE 및 Xen과 같은 비표준 커널 릴리스는 Linux 배포판에 대해 지원되지 않습니다. 예를 들어 "2.6.16.21-0.8-xen"의 릴리스 문자열 hello 사용 하는 시스템은 지원 되지 않습니다.
- 표준 커널의 재컴파일을 포함한 사용자 지정 커널은 지원되지 않습니다.
- CentOSPlus 커널은 지원되지 않습니다.
- Oracle UEK(Unbreakable Enterprise Kernel)에 대해서는 이 문서의 뒷부분에서 다룹니다.


#### <a name="red-hat-linux-7"></a>Red Hat Linux 7
| OS 버전 | 커널 버전 |
|:--|:--|
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7.2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6
| OS 버전 | 커널 버전 |
|:--|:--|
| 6.0 | 2.6.32-71 |
| 6.1 | 2.6.32-131 |
| 6.2 | 2.6.32-220 |
| 6.3 | 2.6.32-279 |
| 6.4 | 2.6.32-358 |
| 6.5 | 2.6.32-431 |
| 6.6 | 2.6.32-504 |
| 6.7 | 2.6.32-573 |
| 6.8 | 2.6.32-642 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5
| OS 버전 | 커널 버전 |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18-417<br>2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Unbreakable Enterprise Kernel을 갖춘 Oracle Enterprise Linux

#### <a name="oracle-linux-6"></a>Oracle Linux 6
| OS 버전 | 커널 버전
|:--|:--|
| 6.2 | Oracle 2.6.32-300(UEK R1) |
| 6.3 | Oracle 2.6.39-200(UEK R2) |
| 6.4 | Oracle 2.6.39-400(UEK R2) |
| 6.5 | Oracle 2.6.39-400(UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400(UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| OS 버전 | 커널 버전
|:--|:--|
| 5.8 | Oracle 2.6.32-300(UEK R1) |
| 5.9 | Oracle 2.6.39-300(UEK R2) |
| 5.10 | Oracle 2.6.39-400(UEK R2) |
| 5.11 | Oracle 2.6.39-400(UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11
| OS 버전 | 커널 버전
|:--|:--|
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10
| OS 버전 | 커널 버전
|:--|:--|
| 10 SP4 | 2.6.16.60 |

## <a name="diagnostic-and-usage-data"></a>진단 및 사용 현황 데이터
Microsoft는 자동으로 사용 하 여 사용자 hello 서비스 맵 서비스 사용 및 성능 데이터를 수집합니다. Microsoft는이 데이터 tooprovide를 사용 하 여 및 hello 품질, 보안 및 hello 서비스 맵 서비스의 무결성을 향상 합니다. 데이터는 운영 체제 버전과 같은 소프트웨어의 hello 구성에 대 한 정보를 포함 합니다. 또한 순서 tooprovide 정확 하 고 효율적인 문제 해결 기능에 IP 주소, DNS 이름 및 워크스테이션의 이름을 포함 합니다. 이름, 주소 또는 기타 연락처 정보는 수집하지 않습니다.

데이터 수집 및 사용에 대 한 자세한 내용은 참조 hello [Microsoft 온라인 서비스 개인정보취급방침](https://go.microsoft.com/fwlink/?LinkId=512132)합니다.



## <a name="next-steps"></a>다음 단계
- 너무 방법에 대해 알아봅니다[서비스 맵을 사용 하 여](operations-management-suite-service-map.md) 배포 및 구성 되었습니다.
