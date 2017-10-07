---
title: "Microsoft Azure에서 PerfInsights aaaHow toouse | Microsoft Docs"
description: "학습 방법을 toouse PerfInsights tootroubleshoot Windows VM 성능 문제."
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a>어떻게 toouse PerfInsights 

[PerfInsights](http://aka.ms/perfinsightsdownload) 유용한 진단 정보 수집 하 고, I/O 스트레스 부하를 실행 한 다음 분석 보고서 toohelp 제공 하는 자동화 된 스크립트는 Microsoft Azure에서 Windows VM 성능 문제를 해결 됩니다. 

VM 성능 문제로 Microsoft 지원 티켓을 열기 전에 이 스크립트를 실행하는 것이 좋습니다.

## <a name="supported-troubleshooting-scenarios"></a>지원되는 문제 해결 시나리오

PerfInsights에서는 고유한 시나리오로 그룹화된 여러 종류의 정보를 수집하고 분석할 수 있습니다.

### <a name="collect-disk-configuration"></a>디스크 구성 수집 

이 시나리오에서는 hello 디스크 구성 및 hello 다음 항목을 포함 하 여 다른 중요 한 정보를 수집 합니다.

-   이벤트 로그

-   모든 들어오는 연결과 나가는 연결에 대한 네트워크 상태

-   네트워크 및 방화벽 구성 설정

-   Hello 시스템에서 현재 실행 중인 모든 응용 프로그램에 대 한 작업 목록

-   Msinfo32 hello 가상 컴퓨터 (VM)에 의해 생성 되는 정보 파일

-   Microsoft SQL Server 데이터베이스 구성 설정 (SQL Server를 실행 하는 서버 hello VM 식별) 하는 경우

-   저장소 안정성 카운터

-   중요한 Windows 핫픽스

-   설치된 필터 드라이버

Hello 시스템에 영향을 하지 않아야 하는 정보의 수동 컬렉션입니다. 

>[!Note]
>이 시나리오는 각각 hello 다음 시나리오에 자동으로 포함 됩니다.

### <a name="benchmarkstorage-performance-test"></a>벤치마크/저장소 성능 테스트

이 시나리오 실행 hello [diskspd](https://github.com/Microsoft/diskspd) 모든 드라이브 연결 toohello VM에 대 한 테스트 (IOPS 및 MBPS) 벤치 마크입니다. 

> [!Note]
> 이 시나리오는 hello 시스템에 영향을 줄 수와 실제 프로덕션 시스템에서 실행 하지 않는 것입니다. 필요한 경우이 시나리오에서에서 실행 전용된 유지 관리 창 tooavoid 문제. 추적 또는 벤치 마크 테스트 인해 발생 하는 워크플로가 증가할 VM의 hello 성능을 저하 될 수 없습니다.
>

### <a name="general-vm-slow-analysis"></a>일반 VM 저속 분석 

이 시나리오를 실행 한 [성능 카운터](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) hello Generalcounters.txt 파일에 지정 하는 hello 카운터를 사용 하 여 추적 합니다. Hello VM으로 식별 되 면 SQL Server를 실행 하는 서버, 성능 카운터 추적 hello Sqlcounters.txt 파일에 있는 hello 카운터를 사용 하 여 실행 됩니다. 또한 성능 진단 데이터도 포함됩니다.

### <a name="vm-slow-analysis-and-benchmark"></a>VM 저속 분석 및 벤치마크

이 시나리오에서는 [성능 카운터](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) 추적을 실행한 다음 [diskspd](https://github.com/Microsoft/diskspd) 벤치마크 테스트를 수행합니다. 

> [!Note]
> 이 시나리오는 hello 시스템에 영향을 줄 수와 실제 프로덕션 시스템에서 실행 하지 않는 것입니다. 필요한 경우이 시나리오에서에서 실행 전용된 유지 관리 창 tooavoid 문제. 추적 또는 벤치 마크 테스트 인해 발생 하는 워크플로가 증가할 VM의 hello 성능을 저하 될 수 없습니다.
>

### <a name="azure-files-analysis"></a>Azure Files 분석 

이 시나리오에서는 네트워크 추적과 함께 특별한 성능 카운터 캡처를 실행합니다. 캡처 모든 hello "SMB 클라이언트 공유" 카운터를 포함합니다. hello 다음은 몇 가지 주요 SMB 클라이언트 공유 성능 카운터 hello 캡처의 일부인입니다.

| **형식**     | **SMB 클라이언트 공유 카운터** |
|--------------|-------------------------------|
| IOPS         | 데이터 요청 수/초             |
|              | 읽기 요청 수/초             |
|              | 쓰기 요청 수/초            |
| 대기 시간      | Avg. 초/데이터 요청         |
|              | 평균 초/읽기                 |
|              | 평균 sec/Write                |
| IO 크기      | 평균 바이트 수/데이터 요청       |
|              | 평균 바이트 수/읽기               |
|              | 평균 바이트 수/쓰기              |
| 처리량   | 데이터 바이트 수/쓰기                |
|              | 읽기 바이트 수/초                |
|              | 쓰기 바이트 수/초               |
| 큐 길이 | 평균 읽기 큐 길이        |
|              | 평균 쓰기 큐 길이       |
|              | 평균 데이터 큐 길이        |

### <a name="custom-configuration"></a>사용자 지정 구성 

사용자 지정 구성을 실행하면 서로 다른 추적을 선택한 개수에 따라 모든 추적(성능 진단, 성능 카운터, xperf, 네트워크, storport)이 병렬로 실행됩니다. 추적 완료 되 면 hello 도구 선택 되어 있으면 hello diskspd 벤치 마크를 실행 합니다. 

> [!Note]
> 이 시나리오는 hello 시스템에 영향을 줄 수와 실제 프로덕션 시스템에서 실행 하지 않는 것입니다. 필요한 경우이 시나리오에서에서 실행 전용된 유지 관리 창 tooavoid 문제. 추적 또는 벤치 마크 테스트 인해 발생 하는 워크플로가 증가할 VM의 hello 성능을 저하 될 수 없습니다.
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a>Hello 스크립트에 의해 어떤 종류의 정보를 수집 하나요?

Windows VM, 디스크 또는 저장소에 대 한 내용은 풀 구성, 성능 카운터, 로그 및 다양 한 추적에서 사용 하는 hello 성능 시나리오에 따라 수집 됩니다.

|수집되는 데이터                              |  |  | 성능 시나리오 |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | 디스크 구성 수집 | 벤치마크/저장소 성능 테스트 | 일반 VM 저속 분석 | VM 저속 분석 및 벤치마크 | Azure Files 분석 | 사용자 지정 구성 |
| 이벤트 로그의 정보      | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| 시스템 정보               | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| 볼륨 매핑                       | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| 디스크 매핑                         | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| 실행 중인 작업                    | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| 저장소 안정성 카운터     | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| 저장소 정보              | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| Fsutil 출력                    | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| 필터 드라이버 정보               | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| Netstat 출력                   | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| 네트워크 구성            | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| 방화벽 구성           | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| SQL Server 구성         | 예                        | 예                                | 예                      | 예                            | 예                  | 예                  |
| 성능 진단 추적 * |                            |                                    | 예                      |                                |                      | 예                  |
| 성능 카운터 추적 **     |                            |                                    |                          |                                |                      | 예                  |
| SMB 카운터 추적 **             |                            |                                    |                          |                                | 예                  |                      |
| SQL Server 카운터 추적 **      |                            |                                    |                          |                                |                      | 예                  |
| XPerf 추적                      |                            |                                    |                          |                                |                      | 예                  |
| StorPort 추적                   |                            |                                    |                          |                                |                      | 예                  |
| 네트워크 추적                    |                            |                                    |                          |                                | 예                  | 예                  |
| Diskspd 벤치마크 추적 ***      |                            | 예                                |                          | 예                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a>성능 진단 추적 (*)

규칙 기반 엔진 hello 배경 toocollect 데이터에서 실행 하 고 지속적인 성능 문제를 진단 합니다. hello 규칙은 현재 지원 됩니다.

- HighCpuUsage 규칙: 높은 CPU 사용 기간을 검색 하 고 해당 기간 동안 hello CPU 사용 하는 소비자를 보여 줍니다.
- HighDiskUsage 규칙: 실제 디스크에서 디스크 사용 기간을 검색 하 고 해당 기간 동안 hello 상위 디스크 사용 소비자를 표시 합니다.
- HighResolutionDiskMetric 규칙: 각 실제 디스크에 대한 50밀리초당 IOPS, 처리량 및 IO 대기 시간 메트릭을 표시합니다. Tooquickly 기간을 제한 하는 디스크를 식별할 수 있습니다.
- HighMemoryUsage 규칙: 높은 메모리 사용 기간을 검색 하 고 해당 기간 동안 hello 상위 메모리 사용 소비자를 표시 합니다.

> [!NOTE] 
> 현재.NET Framework 3.5 hello를 포함 하는 Windows 버전 또는 이후 버전은 지원 됩니다.

### <a name="performance-counter-trace-"></a>성능 카운터 추적 (**)

Hello 다음 성능 카운터를 수집 합니다.

- \Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk
- \Cache\Dirty Pages, \Cache\Lazy Write Flushes/sec, \Server\Pool Nonpaged, Failures, \Server\Pool Paged Failures
- \Network Interface, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments, \Network Adapter, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \Network QoS Policy\Packets, \Per Processor Network Interface Card Activity, \Microsoft Winsock BSP 중에서 선택한 카운터

#### <a name="for-sql-server-instances"></a>SQL Server 인스턴스의 경우
- \SQL Server:Buffer Manager, \SQLServer:Resource Pool Stats, \SQLServer:SQL Statistics\
- \SQLServer:Locks, \SQLServer:General, Statistics
- \SQLServer:Access Methods

#### <a name="for-azure-files"></a>Azure Files의 경우
\SMB Client Shares

### <a name="diskspd-benchmark-trace-"></a>Diskspd 벤치마크 추적 (***)
Diskspd IO 워크로드 테스트[OS 디스크(쓰기) 및 풀 드라이브(읽기/쓰기)]

## <a name="run-hello-perfinsights-on-your-vm"></a>Hello PerfInsights VM에서 실행

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a>어떤 용량은 tooknow hello 스크립트를 실행 하기 전에 

**스크립트 요구 사항**

1.  이 스크립트는 hello hello 성능 문제가 있는 VM에서 실행 되어야 합니다. 

2.  다음 예: 지원 되는 hello: Windows Server 2008 R2, 2012, 2012 R2, 2016; Windows 8.1 및 Windows 10입니다.

**가능한 문제 프로덕션 Vm에서 hello 스크립트를 실행 하는 경우:**

1.  XPerf 또는 DiskSpd를 사용 하 여 구성 된 hello "벤치 마크" 또는 "Custom" 시나리오와 함께 사용 하는 경우 hello 스크립트 hello VM의 hello 성능이 저하 될 수 있습니다. 프로덕션 환경에서 hello 스크립트를 실행할 때 주의 해야 합니다.

2.  DiskSpd를 사용 하 여 구성 된 hello "벤치 마크" 또는 "Custom" 시나리오와 함께 hello 스크립트를 사용 하면 테스트 hello 디스크에서 I/O 작업이 hello 방해가 다른 백그라운드 작업이 있는지 확인 합니다.

3.  기본적으로 hello 스크립트 hello 임시 저장소 드라이브 toocollect 데이터를 사용합니다. 더 긴 시간 동안 사용 하도록 설정 하는 유지 되며, 추적 하는 경우 수집 되는 데이터 양을 hello 관련성 수 있습니다. 이렇게 하면 hello 가용성 따라서이 드라이브에 의존 하는 모든 응용 프로그램에 영향을 주는 hello 임시 디스크 공간을 줄일 수 있습니다.

### <a name="how-do-i-run-perfinsights"></a>PerfInsights를 실행하는 방법 

toorun 스크립트 hello, 다음이 단계를 수행 합니다.

1. [PerfInsights.zip](http://aka.ms/perfinsightsdownload)을 다운로드합니다.

2. Hello PerfInsights.zip 파일 차단을 해제 합니다. 이 마우스 오른쪽 단추로 클릭 hello PerfInsights.zip 파일 선택 toodo **속성**합니다. Hello에 **일반** 탭에서 **차단 해제** 선택한 후 **확인**합니다. Hello 스크립트 추가적인 보안 메시지 표시 없이 실행 되는지 확인 합니다.  

    ![Hello zip 파일의 잠금을 해제합니다](media/how-to-use-perfInsights/unlock-file.png)

3.  임시 드라이브 (기본적으로 보통 hello D 드라이브)에 압축 hello PerfInsights.zip 파일을 확장 합니다. hello 압축 된 파일을 포함 해야 hello 다음 파일 및 폴더:

    ![hello zip 폴더의 파일](media/how-to-use-perfInsights/file-folder.png)

4.  관리자 권한으로 Windows PowerShell을 열고 hello PerfInsights.ps1 스크립트를 실행 합니다.

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    "Y" tooenter를 할 수 있습니다는 tooif toochange hello 실행 정책을 원하는 tooconfirm 요청 합니다.

    Hello 부인 대화 상자에서 Microsoft 기술 지원 서비스와 함께 hello 옵션 tooshare 진단 정보를 제공 됩니다. 또한 toohello 사용권 계약 toocontinue를 동의 해야 합니다. 선택한 다음 **스크립트 실행**을 클릭합니다.

    ![고지 사항 상자](media/how-to-use-perfInsights/disclaimer.png)

5.  사용 가능한 경우, (이 통계에 대 한은) hello 스크립트를 실행할 때 hello 사례 번호를 제출 합니다. 그런 다음 **확인**을 클릭합니다.
    
    ![지원 ID 입력](media/how-to-use-perfInsights/enter-support-number.png)

6.  임시 저장소 드라이브를 선택합니다. hello 스크립트는 hello 드라이브의 드라이브 문자 hello 자동 감지할 수 있습니다. 이 단계에서 문제가 발생 하는 경우 수도 있습니다 tooselect hello 드라이브 라는 메시지가 표시 (hello 기본 드라이브는 D). Hello 로그에 생성 된 로그는 여기에 저장 하는\_컬렉션 폴더입니다. 을 입력 하거나 hello 드라이브 문자를 적용 한 후 클릭 **확인**합니다.

    ![드라이브 입력](media/how-to-use-perfInsights/enter-drive.png)

7.  Hello 제공 목록에서에서 문제 해결 시나리오를 선택 합니다.

       ![지원 시나리오 선택](media/how-to-use-perfInsights/select-scenarios.png)

8.  UI 없이 PerfInsights를 실행할 수도 있습니다.

    hello 다음 실행 hello UI 프롬프트 없이 시나리오 문제 해결 "일반 VM 저속 분석" 명령을 선택 하거나 30 초 동안 데이터를 캡처합니다. 묻는 tooconsent toohello 동일한 부인과 4 단계에서 설명 하는 EULA 합니다.

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    자동 모드에서 PerfInsights toorun 하려는 경우 사용 된 **-AcceptDisclaimerAndShareDiagnostics** 매개 변수입니다. 예를 들어 다음 명령을 hello를 사용 합니다.

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a>Hello 스크립트를 실행 하는 동안 문제를 해결 하려면 어떻게 합니까?

와 함께 hello 스크립트를 실행 하 여 일관성이 없는 상태를 정리할 수 hello 스크립트 비정상적으로 종료 되 면 hello-정리 스위치 다음과 같습니다.

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

Hello hello 임시 드라이브의 자동 검색 하는 동안 문제가 발생을 것일 경우 tooselect hello 드라이브 라는 메시지가 표시 (hello 기본 드라이브는 D).

![드라이브 입력](media/how-to-use-perfInsights/enter-drive.png)

hello 스크립트 hello 유틸리티 도구를 제거 하 고 임시 폴더를 제거 합니다.

### <a name="troubleshooting-other-script-issues"></a>기타 스크립트 문제 해결 

Hello 스크립트를 실행할 때 문제가 발생 하는 경우 Ctrl + C toointerrupt hello 스크립트 실행 키를 누릅니다. tooremove 임시 개체는 hello "비정상적인 종료 후 정리" 섹션을 참조 합니다.

Tooexperience 스크립트 실패를 몇 차례 시도 후에 계속 진행 하면 좋습니다 "디버그 모드" hello 스크립트를 실행 하는 hello를 사용 하 여 "-디버그" 시작할 때 매개 변수 옵션입니다.

Toohello Microsoft 지원 에이전트 역할을 담당 하기 지원을 받는 보낼 hello 오류 발생, hello PowerShell 콘솔의 복사 hello 전체 출력 한 후 toohelp hello 문제를 해결 합니다.

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a>사용자 지정 구성 모드로 hello 스크립트를 실행 하려면 어떻게 합니까?

Hello를 선택 하 여 **사용자 지정** 구성 (사용 하 여 Shift toomulti 선택) 동시에 여러 추적을 활성화할 수 있습니다.

![시나리오 선택](media/how-to-use-perfInsights/select-scenario.png)

Hello 성능 진단, 성능 카운터를 추적, XPerf 추적, 네트워크 추적 또는 Storport 추적 시나리오를 선택 하면 hello 대화 상자에서 hello 지침에 따라 한 hello 추적을 시작한 후에 tooreproduce hello 성능 저하 문제를 시도 하십시오.

대화 상자를 수행 하는 hello 추적을 시작 수 있습니다.

![추적 시작](media/how-to-use-perfInsights/start-trace-message.png)

toostop hello 추적을 두 번째 대화 상자 내에서 tooconfirm hello 명령을 수 있습니다.

![추적 중지](media/how-to-use-perfInsights/stop-trace-message.png)
![추적 중지](media/how-to-use-perfInsights/ok-trace-message.png)

추적 때 hello 또는 작업이 완료 되, d:에 새 파일이 생성 됩니다\\로그\_컬렉션 (또는 hello 임시 드라이브) 라는 **CollectedData\_yyyy-월-일\_hh\_mm \_ss.zip 합니다.** 이 파일 toohello 지원 에이전트 분석을 위해 보낼 수 있습니다.

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a>PerfInsights에서 만든 hello 진단 보고서를 검토 합니다.

Hello 내 **CollectedData\_yyyy-월-일\_hh\_mm\_ss.zip 파일** PerfInsights 생성 하는의 hello 결과 자세히 설명 하는 HTML 보고서를 찾을 수 있습니다 PerfInsights 합니다. tooreview 보고서 hello를 hello 확장 **CollectedData\_yyyy-월-일\_hh\_mm\_ss.zip** 파일을 열고 hello **PerfInsights Report.html**파일입니다.

선택 hello **결과** 탭 합니다.

![찾기 탭](media/how-to-use-perfInsights/findingtab.png)

**참고 사항**

-   빨간색 메시지는 성능 문제를 일으킬 수 있는 알려진 구성 문제입니다.

-   노란색 메시지는 반드시 성능 문제를 일으키지는 않지만 최적이 아닌 구성을 나타내는 경고입니다.

-   파란색 메시지는 유익한 정보만 제공합니다.

검토 hello 빨간색 tooget의 모든 오류 메시지에 대 한 HTTP 링크 hello 한 결과 및 어떻게 영향을 미치는지 hello 성능이 나 성능 액세스에 최적화 된 구성에 대 한 모범 사례에 대 한 정보를 더 자세한 합니다.

### <a name="disk-configuration-tab"></a>디스크 구성 탭

hello **개요** 섹션 hello 저장소 구성, Diskpart 및 저장소 공간에서 정보를 포함 하 여 다른 보기를 표시 합니다.

hello **DiskMap** 및 **VolumeMap** 설명 어떻게 논리는 이중 관점에 볼륨 및 실제 디스크는 기타 관련된 tooeach 합니다.

실제 디스크 관점 (DiskMap) hello hello 테이블 hello 디스크에서 실행 되는 모든 논리 볼륨을 보여 줍니다. 다음 예제는 hello, PhysicalDrive2 여러 파티션을 (J 및 H)에서 만든 논리 볼륨 2를 실행 합니다.

![데이터 탭](media/how-to-use-perfInsights/disktab.png)

Hello 볼륨 관점에서에서 (*VolumeMap*), hello 테이블의 각 논리 볼륨에서 모든 hello 실제 디스크를 표시 합니다. RAID/동적 디스크의 경우 여러 실제 디스크에서 논리 볼륨을 실행할 수 있습니다. 다음 예제는 hello에 *c:\\탑재* 로 구성 하는 "탑재 지점"은 *SpannedDisk* PhysicalDisks에 \#2 및 \#3:

![볼륨 탭](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a>SQL Server 탭

명명 된 hello 보고서의 탭이 추가로 표시는 hello 대상 VM에서 SQL Server 인스턴스를 호스팅하는 경우 **SQL Server**:

![sql 탭](media/how-to-use-perfInsights/sqltab.png)

이 섹션의 hello VM에서 호스팅되는 hello SQL Server 인스턴스 각각에 대해 "개요" 및 추가 하위 탭을 포함 합니다.

hello "개요" 섹션에는 모든 hello 실제 디스크 (시스템 및 데이터 디스크) 실행 되 고 있는 다양 한 데이터 파일 및 트랜잭션 로그 파일을 포함 하는 요약 하는 것이 도움이 테이블 포함 되어 있습니다.

다음 예에서는, hello에 *PhysicalDrive0* hello 모두 때문에 표시 됩니다 (실행 hello C 드라이브) *modeldev* 및 *modellog* hello C 드라이브에 있는 파일 및 서로 다른 형식의 (예: 데이터 파일 및 트랜잭션 로그를 각각):

![로그 정보](media/how-to-use-perfInsights/loginfo.png)

hello SQL Server 인스턴스 관련 탭 hello 선택한 인스턴스에 대 한 기본 정보를 표시 하는 일반 섹션 및 설정, 구성 및 사용자 옵션을 비롯 한 고급 정보에 대 한 추가 섹션이 포함 됩니다.

## <a name="references-toohello-external-tools-used"></a>사용 되는 toohello 외부 도구 참조

### <a name="diskspd"></a>Diskspd

DISKSPD는 저장소 로드 생성기 및 성능 테스트 도구 hello Windows 및 Windows Server 및 클라우드 서버 인프라 엔지니어링 팀에서. 자세한 내용은 [Diskspd](https://github.com/Microsoft/diskspd)를 참조하세요.

### <a name="xperf"></a>XPerf

Xperf는 hello Windows 성능 도구 키트에서에서 명령줄 도구 toocapture 추적입니다.

자세한 내용은 [Windows 성능 도구 키트 - Xperf(영문)](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/)를 참조하세요.

## <a name="next-steps"></a>다음 단계

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a>업로드 진단 기록 및 검토 지원 tooMicrosoft 보고

Microsoft 지원 담당자 hello로 작업할 때 PerfInsights tooassist hello 문제 해결 과정에서 생성 되는 요청 된 tootransmit hello 출력 수도 있습니다.

hello 지원 에이전트 DTM 작업 영역을 만들고 [DTM 포털 (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm)와 고유한 사용자 ID와 암호 링크 toohello 포함 된 전자 메일 메시지를 받게 됩니다.

이 메시지는 **CTS 자동 진단 서비스**(ctsadiag@microsoft.com)에서 보냅니다.

![Hello 메시지의 샘플](media/how-to-use-perfInsights/supportemail.png)

추가 보안을 위해 됩니다 필요 toochange에서 암호를 먼저 사용 합니다.

대화 상자 tooupload hello 있습니다. tooDTM에 로그인 한 후 **CollectedData\_yyyy-월-일\_hh\_mm\_ss.zip** PerfInsights 여 수집 된 파일입니다.
