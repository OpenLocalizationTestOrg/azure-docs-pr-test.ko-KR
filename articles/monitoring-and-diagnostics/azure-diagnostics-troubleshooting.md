---
title: "Azure 진단 aaaTroubleshooting | Microsoft Docs"
description: "Azure Virtual Machines, Service Fabric 또는 Cloud Services에서 Azure 진단을 사용할 때 문제를 해결합니다."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: robb
ms.openlocfilehash: daaf9fa4c40982eb9ba04030d7e8ea1ad9fe085b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Azure 진단 문제 해결
정보 관련 toousing Azure 진단 문제를 해결 합니다. Azure 진단에 대한 자세한 내용은 [Azure 진단 개요](azure-diagnostics.md)를 참조하세요.

## <a name="logical-components"></a>논리적 구성 요소
**진단 플러그 인 시작 관리자 (DiagnosticsPluginLauncher.exe)**: hello Azure 진단 확장을 시작 합니다. Hello 항목으로 하는 데 사용 프로세스를 가리킵니다.

**진단 플러그 인 (DiagnosticsPlugin.exe)**: 위의 hello 시작 관리자에 의해 시작 되 고 hello Monitoring Agent를 구성, 실행 및 수명을 관리 하는 기본 프로세스입니다. 

**Monitoring Agent (MonAgent\*.exe 프로세스)**: 이러한 프로세스는 hello 작업의 대부분 hello지 않습니다; 즉, 모니터링, 컬렉션 및 전송의 hello 진단 데이터입니다.  

## <a name="logartifact-paths"></a>로그/아티팩트 경로
다음은 hello 경로 toosome 중요 한 로그 및 아티팩트입니다. Toothese hello 나머지 hello 문서 전체에서 참조 유지 했습니다.
### <a name="cloud-services"></a>클라우드 서비스
| 아티팩트 | Path |
| --- | --- |
| **Azure 진단 구성 파일** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version>\Config.txt |
| **로그 파일** | C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version>\ |
| **진단 데이터에 대한 로컬 저장소** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Tables |
| **모니터링 에이전트 구성 파일** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MaConfig.xml |
| **Azure 진단 확장 패키지** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<version> |
| **로그 컬렉션 유틸리티 경로** | %SystemDrive%\Packages\GuestAgent\ |
| **MonAgentHost 로그 파일** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

### <a name="virtual-machines"></a>가상 컴퓨터
| 아티팩트 | Path |
| --- | --- |
| **Azure 진단 구성 파일** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\RuntimeSettings |
| **로그 파일** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\Logs\ |
| **진단 데이터에 대한 로컬 저장소** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Tables |
| **모니터링 에이전트 구성 파일** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Configuration\MaConfig.xml |
| **상태 파일** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<version>\Status |
| **Azure 진단 확장 패키지** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>|
| **로그 컬렉션 유틸리티 경로** | C:\WindowsAzure\Packages |
| **MonAgentHost 로그 파일** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD0107\Configuration\MonAgentHost.<seq_num>.log |

## <a name="metric-data-doesnt-show-in-azure-portal"></a>메트릭 데이터는 Azure Portal에 표시되지 않습니다.
Azure 진단은 Azure Portal에 표시될 수 있는 다수의 메트릭 데이터를 제공합니다. 검사 hello 진단 저장소 계정을 WADMetrics-> 포털에서 이러한 데이터를 표시 하는 문제가 있다면\* toosee hello 해당 메트릭 레코드가 있는 경우 테이블입니다. 여기서 hello hello 테이블의 PartitionKey는 가상 컴퓨터 또는 가상 컴퓨터 크기 집합의 hello 리소스 ID 및 hello RowKey는 hello 메트릭 이름 예: 성능 카운터 이름입니다.

진단 구성을 검사 메트릭을-> hello 리소스 ID 올바르지 않으면 hello 리소스 ID가 올바르게 설정 하는 경우 ResourceId toosee-> 합니다.

Hello 특정 메트릭에 대 한 데이터가 경우 hello 메트릭 (성능 카운터) 포함 된 경우 진단 구성을 검사-PerformanceCounter toosee를 > 합니다. 기본적으로 카운터를 수행 하는 hello를 설정 합니다.
- \Processor(_Total)\% Processor Time
- \Memory\Available Bytes
- \ASP.NET Applications(__Total__)\Requests/Sec
- \ASP.NET Applications(__Total__)\Errors Total/Sec
- \ASP.NET\대기 중인 요청
- \ASP.NET\거부된 요청
- \Processor(w3wp)\% Processor Time
- \Process(w3wp)\Private Bytes
- \Process(WaIISHost)\% Processor Time
- \Process(WaIISHost)\Private Bytes
- \Process(WaWorkerHost)\% Processor Time
- \Process(WaWorkerHost)\Private Bytes
- \Memory\Page Faults/sec
- \.NET CLR Memory(_Global_)\% Time in GC
- \LogicalDisk(C:)\Disk Write Bytes/sec
- \LogicalDisk(C:)\Disk Read Bytes/sec
- \LogicalDisk(D:)\Disk Write Bytes/sec
- \LogicalDisk(D:)\Disk Read Bytes/sec

Hello 구성이 올바르게 설정 되어 있어도 여전히 hello 메트릭 데이터를 볼 수 없는 hello 추가 조사를 위해 아래 hello 지침을 따릅니다.


## <a name="azure-diagnostics-is-not-starting"></a>Azure 진단이 시작되지 않음
살펴보고 **DiagnosticsPluginLauncher.log** 및 **DiagnosticsPlugin.log** hello의 hello 위치에서 파일을 로그 파일 위에 이유에 대 한 내용은 진단에 실패 한 toostart 제공 합니다. 

이러한 로그가 `Monitoring Agent not reporting success after launch`를 표시하는 경우 MonAgentHost.exe를 시작하지 못한 것을 의미합니다. 로그를 검토 hello에 대 한 표시 되어 hello 위치에 `MonAgentHost log file` 위의 hello 섹션에 있습니다.

hello 로그 파일의 마지막 줄 hello hello 종료 코드를 포함합니다.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
찾을 **음수** 종료 코드, toohello 참조 [종료 코드 테이블](#azure-diagnostics-plugin-exit-codes) hello에 [참조](#references)합니다.

## <a name="diagnostics-data-is-not-logged-tooazure-storage"></a>진단 데이터는 기록 되지 tooAzure 저장소
데이터가 없는 나타나 hello 데이터의 일부만 표시 되지 않는 나타나는지 확인 합니다.

### <a name="diagnostics-infrastructure-logs"></a>진단 인프라 로그
진단 인프라 로그는 Azure 진단에서 실행되는 모든 오류를 기록하는 위치입니다. 설정 되어 있는지 확인 하십시오 ([하는 방법?](#how-to-check-diagnostics-extension-configuration)) 구성에서 진단 인프라 로그를 캡처하고 hello에 표시 되는 모든 관련 오류 메시지를 신속 하 게 찾고 `DiagnosticInfrastructureLogsTable` 구성 된 저장소 계정의 테이블에에서 있습니다.

### <a name="no-data-is-showing-up"></a>데이터가 표시되지 않음
hello 완전히 누락 된 이벤트 데이터의 가장 일반적인 이유는 잘못 정의 된 저장소 계정 정보입니다.

해결 방법: 진단 구성을 수정하고 진단을 다시 설치합니다.

Hello 저장소 계정이 제대로 구성 되었고, 원격 경우 hello 컴퓨터 및 확인으로 데스크톱 DiagnosticsPlugin.exe 있으며 MonAgentCore.exe 실행 됩니다. 이러한 프로세스가 실행되고 있지 않으면 [Azure 진단이 시작되지 않음](#azure-diagnostics-is-not-starting)을 따르고, Hello 프로세스를 실행할 경우 너무 점프[로컬로 캡처된 가져오는 데이터는](#is-data-getting-captured-locally) 에 여기에서이 가이드를 따릅니다.

### <a name="part-of-hello-data-is-missing"></a>Hello 데이터 부분은 누락
일부 데이터는 가져올 수 있지만 다른 일부는 그렇지 않습니다. 즉, hello 데이터 수집/전송 파이프라인이 올바르게 설정 됩니다. Hello 하위 섹션에 따라 어떤 hello 문제 toonarrow 다음과 같습니다.
#### <a name="is-collection-configured"></a>컬렉션이 구성되어 있습니까? 
진단 구성에는 특정 유형의 데이터 toobe 수집에 대 한 지시 하는 hello 부분이 포함 됩니다. [구성을 검토](#how-to-check-diagnostics-extension-configuration) toomake 있는지 하지 원하는 데이터에 대 한 사용자 컬렉션에 대해 구성 하지 않았습니다.
#### <a name="is-hello-host-generating-data"></a>Hello 호스트는 데이터를 생성 합니다.
- **성능 카운터**: 성능 모니터를 열고 hello 카운터를 확인 합니다.
- **추적 로그**: 원격 데스크톱을 VM hello 및 TextWriterTraceListener toohello 앱 구성 파일을 추가 합니다.  Http://msdn.microsoft.com/library/sk36c28t.aspx tooset을 hello 텍스트 수신기를 참조 하십시오.  있는지 hello 확인 `<trace>` 요소에 `<trace autoflush="true">`합니다.<br />
생성된 추적 로그가 표시되지 않으면 [누락된 추적 로그에 대한 자세한 정보](#more-about-trace-logs-missing)를 따릅니다.
- **ETW 추적**: hello VM에 원격 데스크톱 및 PerfView 설치 합니다.  PerfView에서 파일 -> 사용자 명령 -> Listen etwprovder1,etwprovider2 등을 차례로 실행합니다.  Note hello Listen 명령은 대/소문자 구분 및 ETW 공급자의 hello 쉼표로 구분 된 목록 간의 공백 수 없습니다.  Toorun hello 명령이 실패 하면 hello의 오른쪽 아래 hello Perfview 도구 toosee 시도한 toorun와 어떤 hello 결과 무엇 이었습니까에 hello '로그인' 단추를 클릭 합니다.  Hello 입력이 위쪽과 몇 초 후에 새 창이 팝업 다음 올바른 것으로 가정 하면 ETW 추적을 보는 시작 됩니다.
- **이벤트 로그**: 원격 데스크톱 hello VM 사용 합니다. 열기 `Event Viewer` hello 이벤트 존재를 확인 합니다.
#### <a name="is-data-getting-captured-locally"></a>데이터가 로컬로 캡처되고 있습니까?
Hello 데이터를 가져오는 캡처됩니다 로컬로 확인.
hello 데이터는 로컬에 저장 `*.tsf` 파일 [진단 데이터에 대 한 로컬 저장소 hello](#log-artifacts-path)합니다. 다른 종류의 로그는 서로 다른 `.tsf` 파일에 수집됩니다. hello 이름은 azure 저장소에 유사한 toohello 테이블 이름을 있습니다. 예를 들어 `Performance Counters`는 `PerformanceCountersTable.tsf`에 수집되고, 이벤트 로그는 `WindowsEventLogsTable.tsf`에 수집됩니다. Hello 지침에 따라 [로컬 로그 추출](#local-log-extraction) tooopen hello 로컬 컬렉션 파일 섹션 및 디스크에 수집 된 가져오기 표시 되었는지 확인 합니다.

로컬로 수집 가져오기 로그를 참조 하는 이미 한 있지 않을 경우 확인 데이터를 생성 하는 hello 호스트는, 구성 문제가 있을 가능성이 높습니다. 신중 하 게 hello 적절 한 섹션에 대 한 구성을 검토 합니다. 또한 MonitoringAgent에 대해 생성 된 hello 구성 검토 [MaConfig.xml](#log-artifacts-path) hello 관련 로그 원본과 azure 진단 구성 간의 변환을에서 손실 되지 있는지를 설명 하는 일부 섹션 인지 확인 및 모니터링 에이전트 구성을 적용 합니다.
#### <a name="is-data-getting-transferred"></a>데이터가 전송되고 있습니까?
확인 한 경우 hello 데이터는 가져오는 로컬로 캡처되지만 있습니다 여전히 표시 되지 않는 저장소 계정에: 
- 무엇 보다도, 올바른 저장소 계정을 입력 하 고 저장소 계정을 지정 하는 키 etc.for hello 롤오버 롤오버 하지 않은 있는지 확인 합니다. 클라우드 서비스의 경우 사람들이 `useDevelopmentStorage=true`를 업데이트하지 않는 경우가 종종 있습니다.
- 제공된 저장소 계정이 올바른 경우 - Hello 구성 요소 tooreach 공용 저장소 끝점 허용 하지 않는 일부 네트워크 관련 제한이 없는 있는지 확인 합니다. Tooremote 데스크톱 hello 사용 하는 한 가지 방법은 toodo 컴퓨터 시도 toowrite 사항이 toohello 직접 동일한 저장소 계정입니다.
- 마지막으로, 모니터링 에이전트에서 오류를 보고하고 있는지 확인할 수 있습니다. 모니터링 에이전트 해당 로그를 기록 `maeventtable.tsf` 에 [진단 데이터에 대 한 로컬 저장소 hello](#log-artifacts-path)합니다. 지침에 따라 [로컬 로그 추출](#local-log-extraction) 섹션 tooopen이이 파일을 시도 하 고 있는지 파악 `errors` toostorage 쓰는지를 나타내는 오류 tooread 로컬 파일입니다.

### <a name="capturing--archiving-logs"></a>로그 캡처 및 보관
Hello 단계 위의 단계를 진행 하지만 수 알 수 없는 잘못 된 대상과 지원 팀에 연락 하는 방법에 대 한 연구 하 고 있습니다. hello 첫 번째로 요청 받을 수 있습니다는 컴퓨터에서 toocollect 로그입니다. 사용자가 직접 수행하면 시간을 절약할 수 있습니다. Hello 실행 `CollectGuestLogs.exe` 에서 유틸리티 [로그 수집 유틸리티 경로](#log-artifacts-path) hello에 모든 관련 azure 로그가 포함 된 zip 파일을 생성 하 고 동일한 폴더입니다.

## <a name="diagnostics-data-tables-not-found"></a>진단 데이터 테이블을 찾을 수 없음
ETW 이벤트를 보유 하는 Azure 저장소의 hello 테이블 코드 다음 hello를 사용 하 여 이름이 지정 됩니다.

```C#
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

다음은 예제입니다.

```XML
        <EtwEventSourceProviderConfiguration provider="prov1">
          <Event id="1" />
          <Event id="2" eventDestination="dest1" />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider="prov2">
          <DefaultEvents eventDestination="dest2" />
        </EtwEventSourceProviderConfiguration>
```
```JSON
"EtwEventSourceProviderConfiguration": [
    {
        "provider": "prov1",
        "Event": [
            {
                "id": 1
            },
            {
                "id": 2,
                "eventDestination": "dest1"
            }
        ],
        "DefaultEvents": {
            "eventDestination": "DefaultEventDestination",
            "sinks": ""
        }
    },
    {
        "provider": "prov2",
        "DefaultEvents": {
            "eventDestination": "dest2"
        }
    }
]
```
4개의 테이블을 생성합니다.

| 이벤트 | 테이블 이름 |
| --- | --- |
| provider=”prov1” &lt;Event id=”1” /&gt; |WADEvent+MD5(“prov1”)+”1” |
| provider=”prov1” &lt;Event id=”2” eventDestination=”dest1” /&gt; |WADdest1 |
| provider=”prov1” &lt;DefaultEvents /&gt; |WADDefault+MD5(“prov1”) |
| provider=”prov2” &lt;DefaultEvents eventDestination=”dest2” /&gt; |WADdest2 |

## <a name="references"></a>참조

### <a name="how-toocheck-diagnostics-extension-configuration"></a>어떻게 toocheck 진단 확장 구성
가장 쉬운 방법은 toocheck hello 확장 구성은 toonavigate toohttp://resources.azure.com, toohello 가상 컴퓨터 또는 클라우드 서비스는 hello Azure 진단 확장에서 탐색 (IaaSDiagnostics / PaaDiagnostics)을 확인 하지 못했습니다.

원격 데스크톱을 사용 hello 시스템과 hello Azure 진단 구성 파일에 hello 적절 한 섹션에서 설명 하는 또는 [여기](#log-artifacts-path)합니다.

검색 하거나 사례에서 **Microsoft.Azure.Diagnostics** hello에 대 한 다음 **xmlCfg** 또는 **WadCfg** 필드입니다. 

가상 컴퓨터의 경우 hello WadCfg 필드가 있으면, 것 hello 구성 되며, json에서입니다. Hello xmlCfg 필드가 있는 경우 hello 구성 XML 고 base64 인코딩된 있음을 의미 합니다. 너무 필요한[디코딩해야](http://www.bing.com/search?q=base64+decoder) toosee hello 진단에 의해 로드 된 XML입니다.

클라우드 서비스 역할에 대 한 디스크에서 hello 구성을 선택 하면 hello 데이터는 base64 인코딩 까다롭기 때문에 너무[디코딩해야](http://www.bing.com/search?q=base64+decoder) toosee hello 진단에 의해 로드 된 XML입니다.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Azure 진단 플러그 인 종료 코드
hello 플러그 인 hello 다음 종료 코드를 반환 합니다.

| 종료 코드 | 설명 |
| --- | --- |
| 0 |성공. |
| -1 |일반 오류. |
| -2 |없습니다 tooload hello rcf 파일입니다.<p>이 내부 오류는 hello 게스트 에이전트 플러그 인 시작 관리자가 수동으로 호출 하지 올바르게 hello VM에 경우에 발생 해야 합니다. |
| -3 |Hello 진단 구성 파일을 로드할 수 없습니다.<p><p>해결 방법: 구성 파일이 스키마 유효성 검사를 통과하지 못한 것이 원인입니다. hello 솔루션은 tooprovide hello 스키마를 준수 하는 구성 파일입니다. |
| -4 |모니터링 에이전트 진단 hello의 다른 인스턴스가 이미 hello 로컬 리소스 디렉터리를 사용 하 고 있습니다.<p><p>해결 방법: **LocalResourceDirectory**를 참조하세요. |
| -6 |hello 게스트 에이전트 플러그 인 실행 프로그램에 잘못 된 명령줄을 사용 하 여 toolaunch 진단을 하려고 했습니다.<p><p>이 내부 오류는 hello 게스트 에이전트 플러그 인 시작 관리자가 수동으로 호출 하지 올바르게 hello VM에 경우에 발생 해야 합니다. |
| -10 |hello 진단 플러그 인 처리 되지 않은 예외와 함께 종료 되었습니다. |
| -11 |hello 게스트 에이전트에서 없습니다 toocreate hello 프로세스를 시작 하 고 에이전트를 모니터링 하는 hello 모니터링입니다.<p><p>해결 방법: 시스템 리소스가 사용 가능한 toolaunch 새 프로세스가 있는지 확인 합니다.<p> |
| -101 |Hello 진단 플러그 인을 호출할 때 잘못 된 인수입니다.<p><p>이 내부 오류는 hello 게스트 에이전트 플러그 인 시작 관리자가 수동으로 호출 하지 올바르게 hello VM에 경우에 발생 해야 합니다. |
| -102 |hello 플러그 인 프로세스는 없습니다 tooinitialize 자체입니다.<p><p>해결 방법: 시스템 리소스가 사용 가능한 toolaunch 새 프로세스가 있는지 확인 합니다. |
| -103 |hello 플러그 인 프로세스는 없습니다 tooinitialize 자체입니다. 특히 없습니다 toocreate hello로 거 개체 이므로입니다.<p><p>해결 방법: 시스템 리소스가 사용 가능한 toolaunch 새 프로세스가 있는지 확인 합니다. |
| -104 |없습니다 tooload hello rcf 파일 hello 게스트 에이전트에서 제공 합니다.<p><p>이 내부 오류는 hello 게스트 에이전트 플러그 인 시작 관리자가 수동으로 호출 하지 올바르게 hello VM에 경우에 발생 해야 합니다. |
| -105 |hello 진단 플러그 인 hello 진단 구성 파일을 열 수 없습니다.<p><p>이 내부 오류는 hello 진단 플러그 인은 수동으로 호출 하지 올바르게 hello VM에 경우에 발생 해야 합니다. |
| -106 |Hello 진단 구성 파일을 읽을 수 없습니다.<p><p>해결 방법: 구성 파일이 스키마 유효성 검사를 통과하지 못한 것이 원인입니다. 따라서 hello 솔루션은 tooprovide hello 스키마를 준수 하는 구성 파일입니다. 참조 [어떻게 toocheck 진단 확장 구성](#how-to-check-diagnostics-extension-configuration)합니다. |
| -107 |에이전트를 모니터링 하는 hello 리소스 디렉터리 패스 toohello 올바르지 않습니다.<p><p>이 내부 오류는 hello 모니터링 에이전트는 수동으로 호출 하지 올바르게 hello VM에 경우에 발생 해야 합니다.</p> |
| -108 |Hello 진단 구성 파일 hello 모니터링 에이전트 구성 파일에 없습니다 tooconvert 하 고 있습니다.<p><p>이 내부 오류는 hello 진단 플러그 인 잘못 된 구성 파일을 사용 하 여 수동으로 호출 하는 경우에 발생 해야 합니다. |
| -110 |일반 진단 구성 오류.<p><p>이 내부 오류는 hello 진단 플러그 인 잘못 된 구성 파일을 사용 하 여 수동으로 호출 하는 경우에 발생 해야 합니다. |
| -111 |없습니다 toostart hello 모니터링 에이전트입니다.<p><p>해결 방법: 사용 가능한 시스템 리소스가 충분한지 확인합니다. |
| -112 |일반 오류 |

### <a name="local-log-extraction"></a>로컬 로그 추출
로그와으로 아티팩트를 수집 하는 에이전트 모니터링 hello `.tsf` 파일입니다. `.tsf` 파일은 읽을 수 없지만 다음과 같이 `.csv`로 변환할 수 있습니다: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
새 파일을 호출 `<relevantLogFile>.csv` 에 만들어지는 hello 동일 hello에 해당 경로 `.tsf` 파일입니다.

**참고**: 하기만 하면 toorun hello 주 tsf 파일 (예: PerformanceCountersTable.tsf)에 대해이 유틸리티입니다. 함께 제공 된 파일이 hello (예: PerformanceCountersTables_\*\*001.tsf, PerformanceCountersTables_\*\*002. tsf 등) 자동으로 처리 됩니다.

### <a name="more-about-trace-logs-missing"></a>누락된 추적 로그에 대한 자세한 정보

**참고:** 이 대부분 적용 toocloud 서비스 hello DiagnosticsMonitorTraceListener IaaS VM에서 실행 중인 응용 프로그램에서 구성한 경우를 제외 합니다. 

- DiagnosticMonitorTraceListener hello web.config 또는 app.config에 구성 되어 있는지 hello를 확인 합니다.  이 클라우드 서비스 프로젝트에서 기본적으로 구성 되어 있지만 일부 고객을 주석으로 hello 추적 문을 toonot 시키는 아웃 진단에서 수집 합니다. 
- 로그 hello 실행 하거나 OnStart 메서드에서 작성 시작 되 면 hello app.config에 DiagnosticMonitorTraceListener가 있는지 hello를 확인 합니다.  기본적으로 hello web.config에 있지만 w3wp.exe; 내에서 실행 되는 toocode 적용 되는 WaIISHost.exe에서 실행 되는 app.config toocapture 추적에 필요 합니다.
- Diagnostics.Debug.WriteXXX 대신 Diagnostics.Trace.TraceXXX를 사용하고 있는지 확인합니다.  hello 디버그 문을 제거 될 예정 릴리스 빌드에서 합니다.
- Hello 컴파일된 코드는 실제로 hello Diagnostics.Trace 줄 (Reflector, ildasm 또는 ILSpy tooverify 사용)에 있는지 확인 합니다.  Diagnostics.Trace 명령은 hello TRACE 조건부 컴파일 기호를 사용 하지 않는 한 hello 컴파일된 이진 파일에서 제거 됩니다.  Msbuild toobuild hello 프로젝트를 사용 하는 경우에 일반적인 문제 toorun입니다.

## <a name="known-issues-and-mitigations"></a>알려진 문제 및 완화 방법
다음은 알려진 문제 및 완화 방법을 보여 주는 목록입니다.

**1. .NET 4.5 종속성**

WAD에는 .NET Framework 4.5 이상에 대한 런타임 종속성이 있습니다. 이 작성의 hello 시 모든 공식 azure 가상 컴퓨터 기본 이미지 뿐만 아니라 클라우드 서비스에 대 한 프로 비전 된 모든 컴퓨터는.NET 4.5 했거나 위에 설치 합니다. 그러나 여전히 가능한 tooland toorun WAD.NET 4.5가 없는 컴퓨터에서 이상 할 경우에는 이 문제는 오래된 이미지 또는 스냅숏에서 컴퓨터를 만들거나 사용자 지정 디스크를 가져올 때 발생합니다.

DiagnosticsPluginLauncher.exe를 실행할 때 일반적으로 **255** 종료 코드로 매니페스트되지만, Toohello 처리 되지 않은 예외 때문에 오류 상황이 발생합니다. 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**완화 방법:** 컴퓨터에 .NET 4.5 이상을 설치합니다.

**2. 저장소에서 사용할 수 있지만 포털에서 표시되지 않는 성능 카운터 데이터**

가상 컴퓨터 포털 환경에는 기본적으로 특정 성능 카운터가 표시됩니다. 경우 표시 되지 않으면 hello 데이터 저장소에서 사용할 수 있기 때문에 생성 됩니다. 다음을 확인하세요.
- Hello 데이터 저장소에서에 카운터 이름을 영어로 합니다. Hello 카운터 이름은 영어에 없으면 포털 메트릭 차트 됩니다 수 toorecognize 것입니다.
- 와일드 카드를 사용 하는 경우 (\*) 성능 카운터 이름에 hello 포털 수 toocorrelate hello 구성 되 고 카운터 수집 되지 것입니다.

**완화**: hello 컴퓨터의 언어 tooEnglish 시스템 계정에 대 한 변경 합니다. 제어판 지역-> 관리-> 설정 복사->->는 사용자 지정 언어 hello 되지 않도록 "시작 화면 및 시스템 계정"을 선택 취소 toosystem 계정을 적용 합니다. 또한 포털 toobe 기본 소비 경험을 원하는 경우 와일드 카드를 사용 하지 마십시오 있는지 확인 합니다.
