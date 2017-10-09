---
title: "aaaDiagnostics 도구 tootroubleshoot StorSimple 8000 장치 | Microsoft Docs"
description: "Hello StorSimple 장치 모드에 설명 하 고 설명 방법을 toochange StorSimple에 대 한 Windows PowerShell toouse hello 장치 모드입니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a>Hello StorSimple 진단 도구 tootroubleshoot 8000 시리즈 장치 문제를 사용 하 여

## <a name="overview"></a>개요

hello StorSimple 진단 도구는 문제 관련된 toosystem, 성능, 네트워크 및 StorSimple 장치에 대 한 하드웨어 구성 요소 상태를 진단합니다. hello 진단 도구는 다양 한 시나리오에서 사용할 수 있습니다. 이러한 시나리오에는 작업 계획, StorSimple 장치 배포, hello 네트워크 환경을 평가 및 작동 하는 장치의 hello 성능을 결정 포함 됩니다. 이 문서에서는 hello 진단 도구에 대해 간략하게 설명 하 고 StorSimple 장치와 hello 도구를 사용할 수 있는 방법을 설명 합니다.

hello 진단 도구는 주로 (8100 및 8600) StorSimple 8000 시리즈 온-프레미스 장치에 대 한 것입니다.

## <a name="run-diagnostics-tool"></a>진단 도구 실행

StorSimple 장치의 Windows PowerShell 인터페이스 hello 통해이 도구를 실행할 수 있습니다. 두 가지 방법으로 tooaccess hello 장치의 로컬 인터페이스.

* [사용 하 여 장치 직렬 콘솔 PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)합니다.
* [StorSimple 용 Windows PowerShell hello 통해 hello 도구에 원격으로 액세스](storsimple-remote-connect.md)합니다.

이 문서에서는 toohello PuTTY 통해 장치 직렬 콘솔 연결을 가정 합니다.

#### <a name="toorun-hello-diagnostics-tool"></a>toorun hello 진단 도구

Hello 장치의 toohello Windows PowerShell 인터페이스를 연결 하 고 나면 다음 단계 toorun hello cmdlet hello를 수행 합니다.
1. Hello 단계를 수행 하 여 toohello 장치 직렬 콘솔에 로그온 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)합니다.

2. Hello 다음 명령을 입력 합니다.

    `Invoke-HcsDiagnostics`

    Hello scope 매개 변수를 지정 하지 않으면 hello cmdlet 모든 hello 진단 테스트를 실행 합니다. 이러한 테스트에는 시스템, 하드웨어 구성 요소 상태, 네트워크 및 성능이 포함됩니다. 
    
    특정 테스트 toorun hello 범위 매개 변수를 지정 합니다. 예를 들어, toorun 유일한 hello 네트워크 테스트, 형식

    `Invoke-HcsDiagnostics -Scope Network`

3. 선택 하 고 hello 출력 hello PuTTY에서에서 복사 추가 분석을 위해 텍스트 파일에는 창입니다.

## <a name="scenarios-toouse-hello-diagnostics-tool"></a>시나리오 toouse hello 진단 도구

Hello 진단 도구 tootroubleshoot hello 네트워크, 성능, 시스템 및 하드웨어 시스템의 상태 hello 사용 합니다. 몇 가지 가능한 시나리오는 다음과 같습니다.

* **장치 오프라인** - 사용자의 StorSimple 8000 시리즈 장치가 오프라인 상태입니다. 그러나 hello Windows PowerShell 인터페이스에서 같습니다 hello 두 컨트롤러가 모두 실행 되 고 지.
    * 이 도구를 사용 하면 toothen hello 네트워크 상태를 확인 합니다.
         
         > [!NOTE]
         > Hello 등록 (또는 설치 마법사를 통해 구성) 하기 전에 장치에서이 도구 tooassess 성능 및 네트워크 설정을 사용 하지 마십시오. 유효한 IP 설치 마법사 및 등록 하는 동안 toohello 장치를 할당 됩니다. 등록되지 않은 장치에서 하드웨어 상태 및 시스템에 대해 이 cmdlet을 실행할 수 있습니다. 예를 들어 hello 범위 매개 변수를 사용 합니다.
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* **영구 장치 문제** -toopersist 것 장치 문제가 발생 하는 합니다. 예를 들어 등록에 실패합니다. 또한 발생할 수 있습니다 장치 문제 hello 장치가 성공적으로 등록 하 고 작업을 잠시 후 합니다.
    * 이 경우 Microsoft 지원에 서비스 요청을 로그하기 전에 임시 문제 해결에 대한 이 도구를 사용합니다. 이 도구 및 캡처 hello 출력이 도구를 실행 하는 것이 좋습니다. 그런 다음이 출력 tooSupport tooexpedite 문제 해결을 제공할 수 있습니다.
    * 하드웨어 구성 요소 또는 클러스터 오류가 발생하는 경우 지원 요청에 로그인해야 합니다.

* **낮은 장치 성능** - 사용자의 StorSimple 장치 속도가 느립니다.
    * 이 경우이 cmdlet을 범위 매개 변수 집합 tooperformance 함께 실행 합니다. Hello 출력을 분석 합니다. 읽기 / 쓰기 대기 시간이 hello 클라우드를 가져옵니다. 사용 하 여 hello 대기 시간이 최대 달성 가능한 대상으로 hello 내부 데이터 처리에 대 한 약간의 오버 헤드에 모아 놓은 다음 hello 시스템에 hello 워크 로드를 배포를 보고 합니다. 자세한 내용은 이동 너무[hello 네트워크 tootroubleshoot 장치 성능 테스트를 사용 하 여](#network-test)합니다.


## <a name="diagnostics-test-and-sample-outputs"></a>진단 테스트 및 샘플 출력

### <a name="hardware-test"></a>하드웨어 테스트

이 테스트는 hello 하드웨어 구성 요소, hello USM 펌웨어 및 시스템에서 실행 하는 hello 디스크 펌웨어의 hello 상태를 확인 합니다.

* 보고 hello 하드웨어 구성 요소는 해당 구성 요소 실패 한 hello 테스트 또는 hello 시스템에 없습니다.
* hello USM 펌웨어와 디스크 펌웨어 버전 hello 컨트롤러 0, 컨트롤러 1에 대 한 보고 되 고 시스템의 공유 구성 요소. 하드웨어 구성 요소의 전체 목록은 다음으로 이동합니다.

    * [기본 인클로저의 구성 요소](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [EBOD 인클로저의 구성 요소](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> Hello 하드웨어 테스트 실패 한 구성 요소를 보고 하는 경우 [Microsoft 지원 인 서비스 요청은 로그인](storsimple-contact-microsoft-support.md)합니다.

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a>8100 장치에서 실행되는 하드웨어 테스트의 샘플 출력

다음은 StorSimple 8100 장치의 샘플 출력입니다. EBOD 인클로저 hello hello 8100 모델 장치에 존재 하지 않습니다. 따라서 hello EBOD 컨트롤러 구성 요소 보고 되지 않습니다.

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a>시스템 테스트

이 테스트는 hello 시스템 정보, 사용 가능한 hello 업데이트, hello 클러스터 정보 및 장치에 대 한 hello 서비스 정보를 보고합니다.

* hello 모델, 장치 일련 번호, 표준 시간대, 컨트롤러의 상태 및 hello 시스템에서 실행 중인 hello 자세한 소프트웨어 버전 hello 시스템 정보에 포함 됩니다. 다양 한 너무 이동 시스템 매개 변수는 hello 출력으로 보고 toounderstand hello[시스템 정보를 해석 하](#appendix-interpreting-system-information)합니다.

* hello 업데이트 가용성 hello 일반 연결 및 유지 관리 모드를 사용할 수 있는지 여부를 보고 하 고 연결 된 패키지 이름입니다. 경우 `RegularUpdates` 및 `MaintenanceModeUpdates` 는 `false`, hello 업데이트 제공 되지 않습니다 나타냅니다. 사용자 장치가 최신 상태입니다.
* hello 클러스터 정보 모든 hello HCS 클러스터 그룹 및 해당 상태의 다양 한 논리적 구성 요소에 hello 정보를 포함 합니다. Hello 보고서의이 섹션에 있는 오프 라인 클러스터 그룹에 표시 되 면 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)합니다.
* hello 이름과 모든 hello HCS의 상태 및 장치에서 실행 되는 Ci 서비스 hello 서비스 정보에 포함 됩니다. 이 정보는 hello 장치 문제 해결에 hello Microsoft 지원에 대 한 유용 합니다.

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a>8100 장치에서 실행되는 시스템 테스트의 샘플 출력

8100 장치에서 실행 하는 hello 시스템 테스트의 샘플 출력 다음과 같습니다.

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a>네트워크 테스트

이 테스트는 hello 네트워크 인터페이스, 포트, DNS 및 NTP 서버 간의 연결, SSL 인증서, 저장소 계정 자격 증명, 연결 toohello 업데이트 서버 및 StorSimple 장치에서 웹 프록시 연결 hello 상태를 확인합니다.

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a>DATA0만 사용하는 경우 네트워크 테스트의 샘플 출력

다음은 hello 8100 장치의 샘플 출력입니다. Hello 출력에서 볼 수입니다.
* DATA 0 및 DATA 1 네트워크 인터페이스만 사용하도록 설정 및 구성되어 있습니다.
* 데이터 2-5 hello 포털에서 사용 되지 않습니다.
* hello DNS 서버 구성이 올바른지와 hello 장치 hello DNS 서버를 통해 연결할 수 있습니다.
* hello NTP 서버 연결 해도 됩니다.
* 포트 80 및 443이 열려 있습니다. 그러나 포트 9354는 차단되어 있습니다. Hello에 따라 [시스템 네트워크 요구 사항](storsimple-system-requirements.md), hello 서비스 버스 통신용 tooopen이이 포트가 필요 합니다.
* hello SSL 인증 유효합니다.
* hello 장치 toohello 저장소 계정에 연결할 수 있습니다: _myss8000storageacct_합니다.
* hello 연결 tooUpdate 서버 유효 합니다.
* 이 장치에는 hello 웹 프록시 구성 되지 않았습니다.

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a>DATA0 및 DATA1을 사용하는 경우 네트워크 테스트의 샘플 출력

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a>성능 테스트

이 테스트를 통해 장치에 대 한 hello 클라우드 읽기 / 쓰기 대기 시간이 hello 클라우드 성능을 보고합니다. 이 도구에 사용 되는 tooestablish StorSimple에서 얻을 수 있는 hello 클라우드 성능 기준을 수 있습니다. hello 도구 보고서 hello 최대 성능을 (읽기 / 쓰기 대기 시간에 대 한 모범 사례 시나리오) 연결을 가져올 수 있습니다.

Hello 도구 hello 최대 달성 가능한 성능을 보고, 여기서 사용 하 여 hello를 배포할 때 대상 hello 작업으로 읽기 / 쓰기 대기 시간을 보고 합니다.

hello 테스트 hello 장치에서 hello 다른 볼륨 유형과 관련 된 hello blob 크기를 시뮬레이트합니다. 일반 계층화되고 로컬로 고정된 일반 볼륨의 백업은 64KB Blob 크기를 사용합니다. 선택된 보관 옵션을 사용하는 계층화된 볼륨은 512KB Blob 데이터 크기를 사용합니다. 장치에는 계층화 된 볼륨과 로컬 고정 볼륨 구성 된 유일한 hello 테스트 해당 too64 KB blob 데이터 크기 실행 됩니다.

이 도구 toouse를 hello 다음 단계를 수행 합니다.

1.  첫째, 계층화된 볼륨과 선택된 보관 옵션을 사용하는 계층화된 볼륨의 조합을 만듭니다. 이 작업을 실행 하면 해당 hello 도구 테스트를 실행 hello 64 KB와 512KB에 대 한 blob 크기입니다.

2. 만들고 hello 볼륨 구성 후 hello cmdlet을 실행 합니다. 형식:

    `Invoke-HcsDiagnostics -Scope Performance`

3. Hello 도구에서 보고 하는 hello 읽기 / 쓰기 대기 시간을 기록해 둡니다. 이 테스트는 hello 결과 보고 하기 전에 몇 분 toorun을 걸릴 수 있습니다.

4. Hello 연결 대기 시간이 너무 hello에서 모든 범위를 예상 경우 hello hello 도구에서 보고 하는 대기 시간으로 사용할 수 달성 가능한 최대 대상 hello 작업 부하를 배포 하는 경우. 내부 데이터 처리를 위해 약간의 오버헤드를 고려해야 합니다.

    보고 된 hello 읽기 / 쓰기 대기 시간이 hello 진단 도구가 높습니다.

    1. Blob 서비스에 대 한 Storage Analytics를 구성 하 고 hello Azure 저장소 계정에 대 한 hello 출력 toounderstand hello 대기를 분석 합니다. 자세한 지침은 이동 너무[설정 및 구성 저장소 분석](../storage/common/storage-enable-and-view-metrics.md)합니다. 이러한 대기는 또한 최고 / 비교 가능한 toohello 숫자 hello StorSimple 진단 도구에서에서 받은, Azure 저장소 인 서비스 요청은 toolog을 할 수 있습니다.

    2. Hello 저장소 계정 대기 시간이 부족 한 경우, 대기 시간을 네트워크에서 발급 하 여 네트워크 관리자 tooinvestigate에 게 문의 하십시오.

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a>8100 장치에서 실행되는 성능 테스트의 샘플 출력

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a>부록: 시스템 정보 해석

다음은 어떤 hello에 매핑할 hello 시스템 정보에는 다양 한 Windows PowerShell 매개 변수를 설명 하는 테이블입니다. 

| PowerShell 매개 변수    | 설명  |
|-------------------------|------------------|
| 인스턴스 ID             | 모든 컨트롤러에는 고유 식별자 또는 연결된 GUID입니다.|
| 이름                    | hello hello Azure 포털을 통해 장치를 배포 하는 동안 구성 된 대로 hello 장치의 식별 이름입니다. hello 기본 이름은 hello 장치 일련 번호입니다. |
| 모델                   | StorSimple 8000 시리즈 장치의 hello 모델입니다. hello 모델 8100 또는 8600 수 있습니다.|
| SerialNumber            | hello 장치 일련 번호 hello 공장에서 할당 되 고 길이가 15 자. 예를 들어, 8600-SHX0991003G44HT는 다음을 나타냅니다.<br> 8600-hello 장치 모델이입니다.<br>SHX –는 hello 제조 사이트.<br> 0991003 - 특정 제품을 나타냅니다. <br> G44HT hello 마지막 5 자리는 toocreate 고유한 일련 번호를 증가 합니다. 순차적인 집합이 아닐 수 있습니다.|
| TimeZone                | hello 장치 표준 시간대에에서 구성 된 대로 hello Azure 포털 장치 배포 중입니다.|
| CurrentController       | 연결 된 toothrough StorSimple 장치의 Windows PowerShell 인터페이스를 hello는 hello 컨트롤러입니다.|
| ActiveController        | 장치에서 활성화 되어 있고 모든 hello 네트워크 및 디스크 작업을 제어 하는 hello 컨트롤러입니다. 이는 컨트롤러 0 또는 컨트롤러 1일 수 있습니다.  |
| Controller0Status       | 장치에서 컨트롤러 0의 hello 상태입니다. 복구 모드에서 기본 또는 연결할 수 없습니다. hello 컨트롤러 상태 수 있습니다.|
| Controller1Status       | 컨트롤러 1의 장치에서 상태를 hello입니다.  복구 모드에서 기본 또는 연결할 수 없습니다. hello 컨트롤러 상태 수 있습니다.|
| SystemMode              | StorSimple 장치의 전반적인 상태를 hello 합니다. hello 장치 상태는 보통, 수, 유지 관리 또는 폐기 된 (toodeactivated hello Azure 포털에서에서 해당).|
| FriendlySoftwareVersion | toohello 장치 소프트웨어 버전에 해당 하는 친숙 한 문자열 hello입니다. 업데이트 4를 실행 하는 시스템에 대 한 hello 친숙 한 소프트웨어 버전은 StorSimple 8000 시리즈 업데이트 4.0 것입니다.|
| HcsSoftwareVersion      | 장치에서 실행 중인 hello HCS 소프트웨어 버전입니다. 예를 들어, HCS 소프트웨어 버전 해당 tooStorSimple 8000 hello 시리즈 업데이트 4.0은 6.3.9600.17820 합니다. |
| ApiVersion              | hello hello HCS 장치의 Windows PowerShell API의 hello 소프트웨어 버전입니다.|
| VhdVersion              | 장치 hello hello 출하 시 이미지의 hello 소프트웨어 버전과 함께 제공 되었습니다. 장치 toofactory 기본값을 다시 설정 하면이 소프트웨어 버전을 실행 합니다.|
| OSVersion               | hello hello hello 장치에서 실행 되는 Windows Server 운영 체제의 소프트웨어 버전입니다. hello StorSimple 장치 hello too6.3.9600 해당 하는 Windows Server 2012 r 2를 기반으로 합니다.|
| CisAgentVersion         | StorSimple 장치에서 실행 하 여 Ci 에이전트에 대 한 hello 버전입니다. 이 에이전트는 Azure에서 실행 되는 hello StorSimple Manager 서비스와 통신 하는 데 도움이 됩니다.|
| MdsAgentVersion         | hello 버전 해당 toohello Mds 에이전트 StorSimple 장치에서 실행 합니다. 이 에이전트는 데이터 toohello 이동 모니터링 및 진단 서비스 (MDS).|
| Lsisas2Version          | StorSimple 장치에서 해당 toohello LSI 드라이버 버전 hello 합니다.|
| 용량                | hello hello 장치 바이트에서의 총 용량입니다.|
| RemoteManagementMode    | Windows PowerShell 인터페이스를 통해 hello 장치는 원격으로 관리 수 있는지 여부를 나타냅니다. |
| FipsMode                | 장치에서 hello 미국 연방 정보 FIPS (Processing Standard) 모드를 사용 하는지 여부를 나타냅니다. hello FIPS 140 표준은 hello 중요 한 데이터 보호를 위해 미국 연방 정부 컴퓨터 시스템에서 사용할 수 있도록 승인 하는 암호화 알고리즘을 정의 합니다. 업데이트 4 이상을 실행하는 장치의 경우 FIPS 모드는 기본적으로 활성화되어 있습니다. |

## <a name="next-steps"></a>다음 단계

* Hello 자세한 [hello Invoke HcsDiagnostics cmdlet의 구문을](https://technet.microsoft.com/library/mt795371.aspx)합니다.

* 너무 방법에 대 한 자세한[배포 문제를 해결](storsimple-troubleshoot-deployment.md) StorSimple 장치에 있습니다.
