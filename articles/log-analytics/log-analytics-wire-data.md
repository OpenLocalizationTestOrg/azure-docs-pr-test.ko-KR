---
title: "로그 분석에서 데이터 솔루션 aaaWire | Microsoft Docs"
description: "실시간 데이터는 Operations Manager 및 Windows 연결 에이전트를 포함하여 OMS 에이전트 컴퓨터에서 통합된 네트워크 및 성능 데이터입니다. 네트워크 데이터 결합 되어 데이터 서로 로그 데이터 toohelp와 연결 합니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a>Log Analytics에서 Wire Data 2.0(미리 보기) 솔루션

![Wire Data 기호](./media/log-analytics-wire-data/wire-data2-symbol.png)

Wire Data는 Operations Manager, Windows 연결 및 Linux 에이전트를 포함하여 OMS 에이전트 컴퓨터에서 통합된 네트워크 및 성능 데이터입니다. 네트워크 데이터 결합 되어 데이터 서로 다른 로그 데이터 toohelp 사용자와 연결 합니다.

또한 tooOMS 에이전트 hello 실시간 데이터 솔루션 IT 인프라의 컴퓨터에 설치 하는 Microsoft 종속성 에이전트가 사용 합니다. 네트워크에 대 한 컴퓨터에서 종속성 에이전트 모니터 네트워크 전송 되는 데이터 tooand 수준 2-3에 hello [OSI 모델](https://en.wikipedia.org/wiki/OSI_model), 다양 한 프로토콜 및 사용 되는 포트 hello 포함 합니다. 데이터가 분석 tooLog 보내지면 다음 에이전트를 사용 합니다.

> [!NOTE]
> Hello 이전 버전의 hello 실시간 데이터 솔루션 toonew 작업 영역을 추가할 수 없습니다. Toouse hello 원래 실시간 데이터 솔루션 사용 하도록 설정 하는 경우 계속할 수 있습니다 것입니다. 그러나 실시간 데이터 2.0 toouse 먼저 제거 해야 hello 원래 버전.

기본적으로 Log Analytics는 Windows에 기본 제공된 카운터에서 CPU, 메모리, 디스크 및 네트워크 성능 데이터에 대해 기록된 데이터를 수집합니다. 네트워크 및 기타 데이터 수집은 실시간으로 수행 서브넷 및 hello 컴퓨터에서 사용 되는 응용 프로그램 수준 프로토콜을 포함 하 여 각 에이전트에 대 한 합니다. Hello 로그 탭 hello 설정 페이지에서 다른 성능 카운터를 추가할 수 있습니다.

사용한 적이 있다면 [sFlow](http://www.sflow.org/) 또는 다른 소프트웨어를 [Cisco의 NetFlow 프로토콜](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), 다음 통계를 hello 및 실시간 데이터에서 참조 하는 데이터는 친숙 한 tooyou 됩니다.

기본 제공 로그 검색 쿼리 hello 유형 중 일부는 다음과 같습니다.

- 실시간 데이터를 제공하는 에이전트
- 실시간 데이터를 제공하는 에이전트의 IP 주소
- IP 주소에서 아웃바운드 통신
- 응용 프로그램 프로토콜에서 보낸 바이트 수
- 응용 프로그램 서비스에서 보낸 바이트 수
- 서로 다른 프로토콜에서 받은 바이트 수
- IP 버전을 통해 보내고 받은 총 바이트 수
- 안정적으로 측정된 평균 연결 대기 시간
- 네트워크 트래픽을 시작 또는 수신한 컴퓨터 프로세스
- 프로세스에 대한 네트워크 트래픽의 양

실시간 데이터를 사용 하 여 검색 하는 경우 필터링 할 수 있습니다 및 상위 에이전트 및 상위 프로토콜에 대 한 그룹 데이터 tooview 정보 hello 합니다. 또는 특정 컴퓨터(IP 주소/MAC 주소)가 언제, 얼마나 오래 통신하며 기본적으로 얼마나 많은 데이터를 전송하는지 볼 수 있으며 검색 기반의 네트워크 트래픽에 대한 메타데이터를 확인할 수 있습니다.

그러나 메타데이터를 보는 것이므로 자세한 문제 해결에 반드시 유용한 것은 아닙니다. Log Analytics의 실시간 데이터는 네트워크 데이터를 전체 캡처한 것이 아닙니다. 따라서 심도 있는 패킷 수준 문제 해결에는 적절하지 않습니다. hello 에이전트 사용 시의 이점은 hello, tooother 컬렉션 메서드 비교, tooinstall 가전 제품, 네트워크 스위치를 다시 구성 하거나 하지 복잡 한 구성을 수행 됩니다. 실시간 데이터는 단순히 에이전트 기반-hello 에이전트 컴퓨터에 설치 하 고 해당 네트워크 트래픽을 모니터링 합니다. 또 다른 이점은 toomonitor 작업의 클라우드 공급자, 호스팅 서비스 공급자 또는 hello 사용자 hello 패브릭 계층을 소유 하지 않은 Microsoft Azure에서 실행 하려는 경우입니다.

## <a name="connected-sources"></a>연결된 소스

실시간 데이터를 Microsoft 종속성 에이전트가 hello에서 해당 데이터를 가져옵니다. hello 종속성 에이전트가 OMS 에이전트의 연결 tooLog 분석에 대 한 hello에 따라 달라 집니다. 즉, 서버 hello OMS 에이전트는 설치 하 고 처음에 구성 되어 있어야 합니다. 그런 다음 hello 종속성 에이전트를 설치 합니다. hello 다음 설명 hello 실시간 데이터 솔루션을 지원 하는 hello 연결 원본입니다.

| **연결된 원본** | **지원됨** | **설명** |
| --- | --- | --- |
| Windows 에이전트 | 예 | Wire Data는 Windows 에이전트 컴퓨터에서 데이터를 분석하고 수집합니다. <br><br> 또한 toohello에서 [OMS 에이전트](log-analytics-windows-agents.md), Windows 에이전트 hello Microsoft 종속성 에이전트가 필요 합니다. Hello 참조 [지원 되는 운영 체제](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) 운영 체제 버전의 전체 목록은 합니다. |
| Linux 에이전트 | 예 | Wire Data는 Linux 에이전트 컴퓨터에서 데이터를 분석하고 수집합니다.<br><br> 또한 toohello에서 [OMS 에이전트](log-analytics-linux-agents.md), Linux 에이전트 hello Microsoft 종속성 에이전트가 필요 합니다. Hello 참조 [지원 되는 운영 체제](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) 운영 체제 버전의 전체 목록은 합니다. |
| System Center Operations Manager 관리 그룹 | 예 | Wire Data는 연결된 [System Center Operations Manager 관리 그룹](log-analytics-om-agents.md)의 Windows 및 Linux 에이전트에서 데이터를 분석하고 수집합니다. <br><br> Hello System Center Operations Manager 에이전트 컴퓨터 tooLog의 직접 연결 분석은 필수입니다. 데이터가는 hello 관리 그룹 tooLog 분석에서에서 전달 됩니다. |
| Azure Storage 계정 | 아니요 | 실시간 데이터 데이터 수집 에이전트 컴퓨터에서에서 데이터가 없는 이므로 Azure 저장소에서 toocollect 합니다. |

Windows에서 Microsoft Monitoring Agent (MMA) hello toogather System Center Operations Manager와 로그 분석에서 사용 되 고 데이터 보내기. Hello 컨텍스트에 따라 hello 에이전트는 System Center Operations Manager 에이전트, OMS 에이전트, 로그 분석 에이전트, MMA, 또는 직접 에이전트 hello를 라고 합니다. System Center Operations Manager와 로그 분석의 hello MMA 약간 다른 버전을 제공합니다. 이러한 버전 수 각각 보고 tooSystem Center Operations Manager, 분석, tooLog 또는 tooboth 합니다.

Linux에서 Linux 용 OMS 에이전트 hello를 수집 하 고 데이터 tooLog 분석을 보냅니다. System Center Operations Manager 관리 그룹을 통해 연결 된 tooLog 분석 서버 또는 OMS 직접 에이전트를 사용 하는 서버에서 실시간 데이터를 사용할 수 있습니다.

이 문서에서는 tooall 에이전트를 여부 참조 Linux 또는 Windows에 연결 된 tooa System Center Operations Manager 관리 그룹 또는 직접 tooLog 분석 여부 hello 제한 됩니다 _OMS 에이전트_합니다. 컨텍스트에 대 한 필요한 경우에 hello 에이전트의 hello 특정 배포 이름을 사용 합니다.

hello 종속성 에이전트 자체 데이터를 전송 하지 않습니다 하 고 모든 변경 내용 toofirewalls 또는 포트 필요 하지 않습니다. hello 데이터가 실시간 데이터에서 항상 전송 됩니다 hello OMS 에이전트 tooLog 분석 하거나 직접 또는 OMS 게이트웨이 hello를 사용 하 여 합니다.

![에이전트 다이어그램](./media/log-analytics-wire-data/agents.png)

관리 그룹 연결 tooLog 분석 있는 System Center Operations Manager 사용자 인 경우

- System Center Operations Manager 에이전트는 hello 인터넷 tooconnect tooLog 분석을 액세스할 수 있는 경우 추가 구성이 필요 합니다.
- System Center Operations Manager 에이전트 hello 인터넷을 통해 로그 분석에 액세스할 수 없으면 System Center Operations manager tooconfigure hello OMS 게이트웨이 toowork를 해야 합니다.

Hello 직접 에이전트를 사용 하는 경우 tooconnect tooLog 분석 또는 OMS 게이트웨이 tooyour tooconfigure hello OMS 에이전트 자체 필요 합니다. Hello에서 hello OMS 게이트웨이 다운로드할 수 있습니다 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=52666)합니다.

## <a name="prerequisites"></a>필수 조건

- Hello 필요 [정보 및 분석](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) 솔루션 제공 합니다.
- Hello 이전 버전의 hello 실시간 데이터 솔루션을 사용 하는 경우 먼저 제거 해야 있습니다. 그러나 hello 원래 실시간 데이터 솔루션을 통해 캡처된 모든 데이터는 실시간 데이터 2.0 및 로그 검색에서 계속 제공 합니다.
- 관리자 권한이 필요한 tooinstall는 또는 hello 종속성 에이전트를 제거 합니다.
- hello 종속성 에이전트는 64 비트 운영 체제와 컴퓨터에 설치 되어야 합니다.

### <a name="operating-systems"></a>운영 체제

hello 다음 섹션에 나열 hello 종속성 에이전트에 대 한 운영 체제 hello 지원 합니다. Wire Data는 모든 운영 체제의 32비트 아키텍처를 지원하지 않습니다.

#### <a name="windows-server"></a>Windows Server

- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

#### <a name="windows-desktop"></a>Windows 데스크톱

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux 및 Oracle Linux(RHEL 커널 포함)

- 기본 및 SMP Linux 커널 릴리스만 지원됩니다.
- PAE 및 Xen과 같은 비표준 커널 릴리스는 Linux 배포판에 대해 지원되지 않습니다. 예를 들어 hello 릴리스 문자열의 시스템과 _2.6.16.21-0.8-xen_ 지원 되지 않습니다.
- 표준 커널의 재컴파일을 포함한 사용자 지정 커널은 지원되지 않습니다.
- CentOSPlus 커널은 지원되지 않습니다.
- Oracle UEK(Unbreakable Enterprise Kernel)에 대해서는 이 문서의 뒷부분에서 다룹니다.

#### <a name="red-hat-linux-7"></a>Red Hat Linux 7

| **OS 버전** | **커널 버전** |
| --- | --- |
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7.2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6

| **OS 버전** | **커널 버전** |
| --- | --- |
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

| **OS 버전** | **커널 버전** |
| --- | --- |
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398 <br> 2.6.18-400 <br>2.6.18-402 <br>2.6.18-404 <br>2.6.18-406 <br> 2.6.18-407 <br> 2.6.18-408 <br> 2.6.18-409 <br> 2.6.18-410 <br> 2.6.18-411 <br> 2.6.18-412 <br> 2.6.18-416 <br> 2.6.18-417 <br> 2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Unbreakable Enterprise Kernel을 갖춘 Oracle Enterprise Linux

#### <a name="oracle-linux-6"></a>Oracle Linux 6

| **OS 버전** | **커널 버전** |
| --- | --- |
| 6.2 | Oracle 2.6.32-300(UEK R1) |
| 6.3 | Oracle 2.6.39-200(UEK R2) |
| 6.4 | Oracle 2.6.39-400(UEK R2) |
| 6.5 | Oracle 2.6.39-400(UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400(UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| **OS 버전** | **커널 버전** |
| --- | --- |
| 5.8 | Oracle 2.6.32-300(UEK R1) |
| 5.9 | Oracle 2.6.39-300(UEK R2) |
| 5.10 | Oracle 2.6.39-400(UEK R2) |
| 5.11 | Oracle 2.6.39-400(UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11

| **OS 버전** | **커널 버전** |
| --- | --- |
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10

| **OS 버전** | **커널 버전** |
| --- | --- |
| 10 SP4 | 2.6.16.60 |

#### <a name="dependency-agent-downloads"></a>종속성 에이전트 다운로드

| **파일** | **OS** | **버전** | **SHA-256** |
| --- | --- | --- | --- |
| [InstallDependencyAgent-Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent-Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |



## <a name="configuration"></a>구성

Hello 단계 tooconfigure hello 실시간 데이터 솔루션의 작업 영역에 대 한 다음을 수행 합니다.

1. Hello에서 hello 활동 로그 분석 솔루션을 사용 하도록 설정 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.
2. Tooget 데이터 하려는 각 컴퓨터에 hello 종속성 에이전트를 설치 합니다. hello 종속성 에이전트는 모든 컴퓨터에는 에이전트가 필요 하지 수 있으므로 연결 tooimmediate 인접 한 항목을 모니터링할 수 있습니다.

### <a name="install-hello-dependency-agent-on-windows"></a>Windows hello 종속성 에이전트를 설치 합니다.

관리자 권한이 필요한 tooinstall 인지 hello 에이전트를 제거 합니다.

hello 종속성 에이전트 InstallDependencyAgent Windows.exe를 통해 Windows를 실행 하는 컴퓨터에 설치 됩니다. 옵션 없이이 실행 파일을 실행 하는 경우에 마법사를 대화형으로 tooinstall을 따를 수 시작 합니다.

Hello 단계 tooinstall hello 종속성 에이전트 Windows를 실행 하는 각 컴퓨터에서 다음을 사용 합니다.

1. 설치에 hello 지침을 사용 하 여 OMS 에이전트 hello [연결 Windows 컴퓨터 toohello azure에서 로그 분석 서비스](log-analytics-windows-agents.md)합니다.
2. Hello 링크를 사용 하 여 hello 이전 단원의 hello Windows 에이전트를 다운로드 한 후 다음 명령을 hello를 사용 하 여 실행: InstallDependencyAgent Windows.exe
3. Hello 마법사 tooinstall hello 에이전트를 따릅니다.
4. Hello 종속성 에이전트 toostart 실패 하면 자세한 오류 정보에 대 한 hello 로그를 확인 합니다. Windows 에이전트에서 hello 로그 디렉터리는 %Programfiles%\Microsoft 종속성 Agent\logs입니다.

#### <a name="windows-command-line"></a>Windows 명령줄

Hello 테이블 tooinstall 명령줄에서 다음에서 옵션을 사용 합니다. toosee hello를 사용 하 여 hello 설치 관리자를 실행 한 hello 설치 플래그 목록은 /? 플래그를 사용하여 설치 관리자를 실행합니다.

InstallDependencyAgent-Windows.exe /?

| **플래그** | **설명** |
| --- | --- |
| <code>/?</code> | Hello 명령줄 옵션의 목록을 가져옵니다. |
| <code>/S</code> | 사용자 프롬프트 없이 자동 설치를 수행합니다. |

Hello Windows 종속성 에이전트에 대 한 파일은 기본적으로 C:\Program Files\Microsoft 종속성 에이전트에 배치 됩니다.

### <a name="install-hello-dependency-agent-on-linux"></a>Linux에서 hello 종속성 에이전트를 설치 합니다.

루트 액세스가 필요한 tooinstall 되었거나 hello 에이전트를 구성 합니다.

hello 종속성 에이전트 InstallDependencyAgent Linux64.bin, 자동 압축 풀기 이진과 셸 스크립트를 통해 Linux 컴퓨터에 설치 됩니다. 사용 하 여 hello 파일을 실행할 수 있습니다 _sh_ 하거나 추가 사용 권한을 toohello 파일 자체를 실행 합니다.

Hello 단계 tooinstall hello 종속성 에이전트는 각 Linux 컴퓨터에서 다음을 사용 합니다.

1. 설치에 hello 지침을 사용 하 여 OMS 에이전트 hello [수집 및 Linux 컴퓨터에서 데이터를 관리](log-analytics-agent-linux.md)합니다.
2. Hello 링크를 사용 하 여 hello 이전 단원의 hello 종속성 Linux 에이전트를 다운로드 한 후 다음 명령을 hello를 사용 하 여 루트로 설치: sh InstallDependencyAgent Linux64.bin
3. Hello 종속성 에이전트 toostart 실패 하면 자세한 오류 정보에 대 한 hello 로그를 확인 합니다. Linux 에이전트 hello 로그 디렉터리는: /var/opt/microsoft/dependency-agent/log 합니다.

toosee hello로 hello 설치 프로그램을 실행 hello 설치 플래그 목록은 `-help` 플래그 다음과 같습니다.

```
InstallDependencyAgent-Linux64.bin -help
```

| **플래그** | **설명** |
| --- | --- |
| <code>-help</code> | Hello 명령줄 옵션의 목록을 가져옵니다. |
| <code>-s</code> | 사용자 프롬프트 없이 자동 설치를 수행합니다. |
| <code>--check</code> | 사용 권한 및 hello 운영 체제를 확인 하십시오. 하지만 hello 에이전트를 설치 하지 마십시오. |

Hello 종속성 에이전트에 대 한 파일은 다음 디렉터리 hello에 배치 됩니다.

| **파일** | **위치** |
| --- | --- |
| 코어 파일 | /opt/microsoft/dependency-agent |
| 로그 파일 | /var/opt/microsoft/dependency-agent/log |
| 구성 파일 | /etc/opt/microsoft/dependency-agent/config |
| 서비스 실행 파일 | /opt/microsoft/dependency-agent/bin/microsoft-dependency-agent<br><br>/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager |
| 이진 저장소 파일 | /var/opt/microsoft/dependency-agent/storage |

### <a name="installation-script-examples"></a>설치 스크립트 예제

tooeasily 한 번에 많은 서버에 hello 종속성 에이전트를 배포, toouse 스크립트는 데 도움이 됩니다. 다음 스크립트 예제 toodownload hello를 사용 하 고 Windows 또는 Linux hello 종속성 에이전트를 설치할 수 있습니다.

#### <a name="powershell-script-for-windows"></a>Windows용 PowerShell 스크립트

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a>Linux용 셸 스크립트

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a>필요한 상태 구성

toodeploy hello 종속성 에이전트 필요한 상태 구성을 통해 hello xPSDesiredStateConfiguration 모듈 및 약간의 hello 다음과 같은 코드를 사용할 수 있습니다.

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a>Hello 종속성 에이전트 제거

다음 섹션에서는 toohelp hello 종속성 에이전트를 제거 하는 hello를 사용 합니다.

#### <a name="uninstall-hello-dependency-agent-on-windows"></a>Hello Windows에서 종속성 에이전트 제거

관리자는 hello 종속성 에이전트에 대 한 Windows 제어판을 통해 제거할 수 있습니다.

관리자는 %Programfiles%\Microsoft 종속성 Agent\Uninstall.exe toouninstall hello 종속성 에이전트를 실행할 수도 있습니다.

#### <a name="uninstall-hello-dependency-agent-on-linux"></a>Hello Linux에서 종속성 에이전트 제거

toocompletely 제거 hello Linux에서 종속성 에이전트, hello 에이전트 자체를 제거 하 고 hello 에이전트와 함께 자동으로 설치 되는 커넥터 hello 해야 합니다. 다음 단일 명령을 hello를 사용 하 여 두를 제거할 수 있습니다.

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a>관리 팩

실시간 데이터는 로그 분석 작업 영역에서 활성화 되 면 해당 작업 영역에서 300 KB 관리 팩 tooall hello Windows 서버를 전송 됩니다. System Center Operations Manager 에이전트를 사용 하는 경우는 [연결 된 관리 그룹](log-analytics-om-agents.md), System Center Operations Manager에서 관리 팩 종속성 모니터 hello를 배포 합니다. Hello 에이전트 직접 연결 되어 있는 경우 로그 분석은 hello 관리 팩을 제공 합니다.

관리 팩 hello Microsoft.IntelligencePacks.ApplicationDependencyMonitor 라고 합니다. 이것은 %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs에 기록됩니다. 관리 팩 hello를 사용 하는 hello 데이터 원본이: % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\ \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll 합니다.

## <a name="using-hello-solution"></a>Hello 솔루션을 사용 하 여

**설치 하 고 hello 솔루션 구성**

다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.

- 실시간 데이터 솔루션 hello는 Windows Server 2012 R2, Windows 8.1 및 이후 운영 체제를 실행 중인 컴퓨터에서 데이터를 가져옵니다.
- Tooacquire 실시간 데이터에서 대상 컴퓨터에 Microsoft.NET Framework 4.0 이상이 필요 합니다.
- Hello 실시간 데이터 솔루션 tooyour 로그 분석 작업 영역에서 설명 하는 hello 프로세스를 사용 하 여 추가 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다. 추가 구성은 필요 없습니다.
- 이미 추가 toohave hello 솔루션을 필요로 하는 특정 솔루션에 대 한 tooview 실시간 데이터를 원하는 경우 tooyour 작업 영역입니다.

에이전트가 설치 되어 있고 hello 솔루션을 설치한 후 hello 실시간 데이터 2.0 타일 작업 영역에 나타납니다.

> [!NOTE]
> 현재 hello OMS 포털 tooview 실시간 데이터를 사용 해야 합니다. Hello Azure 포털 tooview 실시간 데이터를 사용할 수 없습니다.

![Wire Data 타일](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a>실시간 데이터 2.0 hello 솔루션을 사용 하 여

Hello OMS 포털에서 클릭 hello **실시간 데이터 2.0** tooopen hello 실시간 데이터 대시보드 타일입니다. hello 대시보드는 다음 표에 hello에 hello 블레이드를 포함 합니다. 각 블레이드 hello에 대 한 조건을 블레이드 범위 및 시간 범위를 지정 했는지 일치 too10 항목을 나열 합니다. 클릭 하 여 모든 레코드를 반환 하는 로그 검색을 실행할 수 있습니다 **스크롤하게** hello 블레이드의 또는 hello 블레이드 헤더를 클릭 하 여 hello 맨 아래에 있습니다.

| **블레이드** | **설명** |
| --- | --- |
| 네트워크 트래픽을 캡처하는 에이전트 | 네트워크 트래픽을 캡처하는 에이전트의 hello 수를 표시 하 고 hello 상위 10 개의 컴퓨터에 트래픽을 캡처하는 나열 합니다. 에 대 한 로그 검색 번호 toorun hello 클릭 <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>합니다. Hello 총 캡처된 바이트 수를 반환 하는 로그 검색 hello 목록 toorun에 있는 컴퓨터를 클릭 합니다. |
| 로컬 서브넷 | 로컬 서브넷 검색 에이전트 hello 수가 표시 됩니다.  에 대 한 로그 검색 번호 toorun hello 클릭 <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> hello 각을 통해 보낸 바이트 수와 모든 서브넷을 나열 하 합니다. Hello 목록 toorun에서 서브넷 hello hello 서브넷을 통해 전송 된 바이트의 총 수를 반환 하는 로그 검색을 클릭 합니다. |
| 응용 프로그램 수준 프로토콜 | 에이전트에서 검색 된 것으로 사용 중인 응용 프로그램 수준 프로토콜 hello 수를 표시 합니다. 에 대 한 로그 검색 번호 toorun hello 클릭 <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>합니다. 프로토콜 toorun hello 총 hello 프로토콜을 사용 하 여 보낸 바이트 수를 반환 하는 로그 검색을 클릭 합니다. |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Wire Data 대시보드](./media/log-analytics-wire-data/wire-data-dash.png)

Hello를 사용할 수 있습니다 **네트워크 트래픽을 캡처하는 에이전트** 블레이드 toodetermine 컴퓨터에서 사용 되는 얼마나 많은 네트워크 대역폭입니다. 이 블레이드 도와 쉽게 찾기 hello _chattiest_ 사용자 환경에서 컴퓨터입니다. 이러한 컴퓨터는 오버로드되거나 비정상적으로 작동하거나 보통 때보다 더 많은 네트워크 리소스를 사용할 수 있습니다.

![로그 검색 예제](./media/log-analytics-wire-data/log-search-example01.png)

마찬가지로, hello를 사용할 수 있습니다 **로컬 서브넷** 블레이드 toodetermine 네트워크 트래픽 양을 서브넷을 통해 이동 됩니다. 사용자는 종종 응용 프로그램의 중요한 영역 주위 서브넷을 정의합니다. 이 블레이드는 해당 영역에 대한 뷰를 제공합니다.

![로그 검색 예제](./media/log-analytics-wire-data/log-search-example02.png)

hello **응용 프로그램 수준 프로토콜** 블레이드 유용 도움이 되었기 때문에 알 수 사용 중인 프로토콜입니다. 예를 들어 SSH toonot 네트워크 환경에서 사용 될 예상할 수 있습니다. Hello 블레이드에서 사용할 수 있는 정보를 볼 수 확인 하거나 사용자 기대 disprove 신속 하 게 합니다.

![로그 검색 예제](./media/log-analytics-wire-data/log-search-example03.png)

이 예에서 드릴 인투 SSH 세부 정보 toosee SSH 및 다른 많은 통신 세부 사항을 사용 하 여 컴퓨터를 수 있습니다.

![sh 검색 결과](./media/log-analytics-wire-data/ssh-details.png)

프로토콜 트래픽을 늘리거나 시간이 지남에 따라 점점 감소 하는 경우 유용한 tooknow 이기도 합니다. 예를 들어 hello 응용 프로그램에 의해 전송 되는 데이터 양이 증가 하는 경우 수 있는 것을 알고 있어야 이거나 주목할 만한를 찾아볼 수 있습니다.

## <a name="input-data"></a>데이터 입력

실시간 데이터는 네트워크 트래픽 사용 하도록 설정한 hello 에이전트를 사용 하는 방법에 대 한 메타 데이터를 수집 합니다. 각 에이전트는 약 15초마다 데이터를 보냅니다.

## <a name="output-data"></a>출력 데이터

각 형식의 입력 데이터에 대해 종류가 _WireData_인 레코드가 만들어집니다. WireData 레코드 hello 표 다음에 표시 된 속성을 가져야 합니다.

| 속성 | 설명 |
|---|---|
| 컴퓨터 | 데이터가 수집된 컴퓨터 이름 |
| TimeGenerated | Hello 레코드의 시간 |
| LocalIP | Hello 로컬 컴퓨터의 IP 주소 |
| SessionState | 연결 또는 연결 끊김 |
| ReceivedBytes | 받은 바이트의 양 |
| ProtocolName | 사용 하는 hello 네트워크 프로토콜의 이름 |
| IPVersion | IP 버전 |
| 방향 | 인바운드 또는 아웃바운드 |
| MaliciousIP | 알려진 악의적인 원본의 IP 주소 |
| 심각도 | 의심되는 맬웨어 심각도 |
| RemoteIPCountry | Hello 원격 IP 주소의 국가 |
| ManagementGroupName | Hello Operations Manager 관리 그룹의 이름 |
| SourceSystem | 데이터가 수집된 원본 |
| SessionStartTime | 세션의 시작 시간 |
| SessionEndTime | 세션의 종료 시간 |
| LocalSubnet | 데이터가 수집된 서브넷 |
| LocalPortNumber | 로컬 포트 번호 |
| RemoteIP | Hello 원격 컴퓨터에서 사용 하는 원격 IP 주소 |
| RemotePortNumber | Hello 원격 IP 주소에서 사용 하는 포트 번호입니다. |
| SessionID | 두 개의 IP 주소 간의 통신 세션을 식별하는 고유 값 |
| SentBytes | 보낸 바이트 수 |
| TotalBytes | 세션 중에 보낸 총 바이트 수 |
| ApplicationProtocol | 사용되는 네트워크 프로토콜의 유형   |
| ProcessID | Windows 프로세스 ID |
| ProcessName | Hello 프로세스의 경로 파일 이름 |
| RemoteIPLongitude | IP 경도 값 |
| RemoteIPLatitude | IP 위도 값 |


## <a name="next-steps"></a>다음 단계

- [로그 검색](log-analytics-log-searches.md) tooview 실시간 데이터 검색 레코드를 자세히 설명 합니다.
