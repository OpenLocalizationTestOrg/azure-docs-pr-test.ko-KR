---
title: "Azure 진단에서 성능 카운터 aaaUse | Microsoft Docs"
description: "Azure 클라우드 서비스 또는 가상 컴퓨터 toofind 병목 상태에서 성능 카운터를 사용 하 여 및 성능 튜닝 합니다."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a>Azure 응용 프로그램에서 성능 카운터 만들기 및 사용
이 문서에서는의 hello 이점 및 Azure 응용 프로그램에 tooput 성능 카운터 하는 방법을 설명 합니다. Toocollect 데이터를 사용 하 고, 병목 상태를 찾을 하 고, 시스템 및 응용 프로그램 성능을 조정할 수 있습니다.

Windows Server, IIS 및 ASP.NET에 대해 성능 카운터를 수집할 수도 있습니다 및 Azure 웹 역할, 작업자 역할 및 가상 컴퓨터의 toodetermine hello 상태를 사용 합니다. 사용자 지정 성능 카운터를 만들고 사용할 수도 있습니다.  

성능 카운터 데이터를 다음과 같이 검사할 수 있습니다.

1. 원격 데스크톱을 사용 하 여 액세스 하는 hello 성능 모니터 도구와 함께 hello 응용 프로그램 호스트에서 직접
2. Azure 관리 팩 hello를 사용 하 여 System Center Operations manager
3. Hello에 액세스 하는 다른 모니터링 도구와 함께 진단 데이터가 tooAzure 저장소를 전송 합니다. 자세한 내용은 [Azure 저장소에서 진단 데이터 저장 및 보기](https://msdn.microsoft.com/library/azure/hh411534.aspx) 를 참조하세요.  

Hello에서 응용 프로그램의 hello 성능 모니터링에 대 한 자세한 내용은 [Azure 포털](http://portal.azure.com/), 참조 [tooMonitor 클라우드 서비스 방법](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/)합니다.

로깅 및 추적 전략 하며 진단 및 기타 기술 tootroubleshoot 문제를 사용 하 여 깊이 있는 추가 지침은 Azure 응용 프로그램을 최적화 하 고, 참조 [Azure 개발에 대 한 모범 사례 문제 해결 응용 프로그램](https://msdn.microsoft.com/library/azure/hh771389.aspx)합니다.

## <a name="enable-performance-counter-monitoring"></a>성능 카운터 모니터링 사용
성능 카운터는 기본적으로 사용할 수 없습니다. 응용 프로그램 또는 시작 작업 hello 기본 진단 원하는 toomonitor 각 역할 인스턴스에 대 한 에이전트 구성 tooinclude hello 특정 성능 카운터를 수정 해야 합니다.

### <a name="performance-counters-available-for-microsoft-azure"></a>Microsoft Azure에 사용할 수 있는 성능 카운터
Azure는 Windows Server, IIS 및 ASP.NET 스택에서 hello에 대 한 hello 사용할 수 있는 성능 카운터의 하위 집합을 제공합니다. hello 다음 표에서 Azure 응용 프로그램에 대 한 관심 있는 특정의 hello 성능 카운터입니다.

| 카운터 범주: 개체(인스턴스) | 카운터 이름 | 참조 |
| --- | --- | --- |
| .NET CLR Exceptions(*Global*) |# Exceps Thrown / sec |예외 성능 카운터 |
| .NET CLR Memory(*Global*) |% Time in GC |메모리 성능 카운터 |
| ASP.NET |응용 프로그램 다시 시작 |ASP.NET용 성능 카운터 |
| ASP.NET |요청 실행 시간 |ASP.NET용 성능 카운터 |
| ASP.NET |요청이 끊김 |ASP.NET용 성능 카운터 |
| ASP.NET |작업자 프로세스 다시 시작 |ASP.NET용 성능 카운터 |
| ASP.NET Applications(**Total**) |총 요청 수 |ASP.NET용 성능 카운터 |
| ASP.NET Applications(**Total**) |Requests/Sec |ASP.NET용 성능 카운터 |
| ASP.NET v4.0.30319 |요청 실행 시간 |ASP.NET용 성능 카운터 |
| ASP.NET v4.0.30319 |요청 대기 시간 |ASP.NET용 성능 카운터 |
| ASP.NET v4.0.30319 |현재 요청 |ASP.NET용 성능 카운터 |
| ASP.NET v4.0.30319 |대기 중인 요청 |ASP.NET용 성능 카운터 |
| ASP.NET v4.0.30319 |거부된 요청 |ASP.NET용 성능 카운터 |
| 메모리 |Available MBytes |메모리 성능 카운터 |
| 메모리 |커밋된 바이트 |메모리 성능 카운터 |
| Processor(_Total) |% Processor Time |ASP.NET용 성능 카운터 |
| TCPv4 |연결 오류 |TCP Object |
| TCPv4 |Connections Established |TCP Object |
| TCPv4 |Connections Reset |TCP Object |
| TCPv4 |Segments Sent/sec |TCP Object |
| Network Interface(*) |Bytes Received/sec |Network Interface Object |
| Network Interface(*) |Bytes Sent/sec |Network Interface Object |
| Network Interface(Microsoft Virtual Machine Bus Network Adapter _2) |Bytes Received/sec |Network Interface Object |
| Network Interface(Microsoft Virtual Machine Bus Network Adapter _2) |Bytes Sent/sec |Network Interface Object |
| Network Interface(Microsoft Virtual Machine Bus Network Adapter _2) |Bytes Total/sec |Network Interface Object |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a>만들기 및 사용자 지정 성능 카운터 tooyour 응용 프로그램 추가
Azure 지원 toocreate 개이고 웹 역할과 작업자 역할에 대 한 사용자 지정 성능 카운터를 수정 합니다. hello 카운터 tootrack 및 모니터 응용 프로그램 관련 동작을 사용 하는 수 있습니다. 승격된 권한으로 시작 작업, 웹 역할 또는 작업자 역할에서 사용자 지정 성능 카운터 범주 및 지정자를 만들고 삭제할 수 있습니다.

> [!NOTE]
> Toocustom ÷ ´ ֹ 변경 하는 코드에서 사용 권한을 toorun을 높은 해야 합니다. Hello 역할 hello 태그를 포함 해야 hello 코드가 웹 역할 또는 작업자 역할에 포함 된 경우 <Runtime executionContext="elevated" /> hello ServiceDefinition.csdef 파일에 역할 tooinitialize hello에 대 한 적절 합니다.
>
>

사용자 지정 성능 카운터 데이터 tooAzure 저장소 hello 진단 에이전트를 사용 하 여 보낼 수 있습니다.

hello 표준 성능 카운터 데이터는 hello Azure 프로세스에 의해 생성 됩니다. 웹 역할 또는 작업자 역할 응용 프로그램에서 사용자 지정 성능 카운터 데이터를 만들어야 합니다. 참조 [성능 카운터 형식](https://msdn.microsoft.com/library/z573042h.aspx) hello 유형의 사용자 지정 성능 카운터에 저장할 수 있는 데이터에 대 한 내용은 합니다. 웹 역할에서 사용자 지정 성능 카운터 데이터를 만들고 설정하는 예제는 [PerformanceCounters 샘플](http://code.msdn.microsoft.com/azure/) 을 참조하세요.

## <a name="store-and-view-performance-counter-data"></a>성능 카운터 데이터 저장 및 보기
Azure는 기타 진단 정보와 함께 성능 카운터 데이터를 캐시합니다. 이 데이터를 성능 모니터와 같은 원격 데스크톱 액세스 tooview 도구를 사용 하 여 hello 역할 인스턴스가 실행 되는 동안 원격 모니터링할 수 있습니다. hello 역할 인스턴스 외부의 toopersist hello 데이터 hello 진단 에이전트 hello 데이터 tooAzure 저장소를 전송 해야 합니다. hello 캐시 성능 카운터 데이터의 크기 제한을 hello hello 진단 에이전트에서 구성할 수 있습니다 또는 것이 모든 진단 데이터를 hello에 대 한 공유 제한의 toobe 일부를 구성 합니다. Hello 버퍼 크기를 설정 하는 방법에 대 한 자세한 내용은 참조 [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) 및 [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx)합니다. 참조 [스토어 및 Azure 저장소에 진단 데이터 보기](https://msdn.microsoft.com/library/azure/hh411534.aspx) hello 진단 에이전트 tootransfer 데이터 tooa 저장소 계정 설정에 대 한 개요입니다.

Hello 샘플링 된 데이터를 전송 하 고 각 구성 된 성능 카운터 인스턴스는 특정된 샘플링 비율로 기록 되며 toohello 저장소 계정 예약된 전송 요청 또는 요청 시 전송 요청 합니다. 자동 전송은 매 분마다 예약할 수 있습니다. Hello 진단 에이전트에 의해 전송 되는 성능 카운터 데이터는 테이블 WADPerformanceCountersTable, hello 저장소 계정에에서 저장 됩니다. 표준 Azure 저장소 API 메서드를 사용하여 이 테이블에 액세스 및 쿼리할 수 있습니다. 참조 [Microsoft Azure PerformanceCounters 샘플](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) 쿼리하고 표시 hello WADPerformanceCountersTable 테이블에서 성능 카운터 데이터의 예입니다.

> [!NOTE]
> Hello 진단 에이전트 전송 빈도 및 큐 대기 시간에 따라 hello hello 저장소 계정에서 성능 카운터 데이터를 가장 최근의 수 몇 분 정도입니다.
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a>진단 구성 파일을 사용하여 성능 카운터를 사용하도록 설정
Azure 응용 프로그램에서 프로시저 tooenable 성능 카운터를 다음 hello를 사용 합니다.

## <a name="prerequisites"></a>필수 조건
이 섹션에서는 hello 진단 모니터를 응용 프로그램으로 가져온 고 hello 진단 구성 파일 tooyour Visual Studio 솔루션 (SDK 2.4이 하 버전에 diagnostics.wadcfg 또는 SDK 2.5에서 이상 diagnostics.wadcfgx)를 추가 했다고 가정 합니다. 자세한 내용은 [Azure 클라우드 서비스 및 Virtual Machine에서 진단 사용](cloud-services-dotnet-diagnostics.md))의 1, 2단계를 참조하세요.

## <a name="step-1-collect-and-store-data-from-performance-counters"></a>1단계: 성능 카운터에서 데이터 수집 및 저장
Hello 진단 tooyour Visual Studio 솔루션 파일을 추가 하면 Azure 응용 프로그램에서 성능 카운터 데이터의 hello 수집 및 저장을 구성할 수 있습니다. 이 성능 카운터 toohello 진단 파일을 추가 하 여 수행 됩니다. 진단 데이터를 성능 카운터를 포함 하 여 hello 인스턴스에서 먼저 수집 됩니다. hello 데이터 지속형된 toohello WADPerformanceCountersTable 테이블 hello Azure 테이블 서비스에에서 다음을 할 수 있으므로 필요 toospecify hello 응용 프로그램의 저장소 계정. Hello 계산 에뮬레이터에서에서 로컬로 응용 프로그램를 테스트 하는 경우 저장할 수도 있습니다 진단 데이터 로컬 저장소 에뮬레이터의 hello에 있습니다. 진단 데이터를 저장 하기 전에 먼저 toohello를 이동 해야 [Azure 포털](http://portal.azure.com/) 클래식 저장소 계정을 만듭니다. 가장 좋은 방법은 toolocate 저장소 계정에서 Azure 응용 프로그램과 동일한 지리적 위치의 hello 합니다. Hello 유지 하 여 Azure 응용 프로그램 및 저장소 계정은에 hello 동일한 지리적 위치의 외부 대역폭 비용을 지불 하지 않고 대기 시간 단축 합니다.

### <a name="add-performance-counters-toohello-diagnostics-file"></a>성능 카운터 toohello 진단 파일 추가
사용할 수 있는 카운터가 많습니다. hello 다음 예제에서는 웹 및 작업자 역할 모니터링에 대 한 권장 되는 몇 가지 성능 카운터

(SDK 2.4와 그 하위 diagnostics.wadcfg 또는 SDK 2.5에서 이상 diagnostics.wadcfgx) hello 진단 파일을 열고 toohello DiagnosticMonitorConfiguration 요소 다음에 오는 hello를 추가 합니다.

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

hello bufferQuotaInMB 특성 hello hello 데이터 컬렉션 형식 (Azure 로그, IIS 로그 등)에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 합니다. hello 기본값은 0입니다. Hello 할당량에 도달 하면 새 데이터가 추가 되므로 hello 가장 오래 된 데이터가 삭제 됩니다. 모든 hello bufferQuotaInMB 속성의 hello 합계 hello hello OverallQuotaInMB 특성 값 보다 커야 합니다. 저장소 크기는 진단 데이터의 hello 컬렉션에 대 한 요구 됩니다 결정 하는 보다 자세한 논의 알려면의 WAD 설정 섹션 hello [문제 해결에 대 한 유용한 Azure 응용 프로그램 개발](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx)합니다.

hello 예약 된 데이터 전송 간격을 지정 하는, hello scheduledTransferPeriod 특성 toohello 가장 근접 한 분을 반올림 합니다. 다음 예제는 hello, tooPT30M (30 분) 설정 됩니다. 설정 hello 전송 기간 tooa 같은 작은 값으로 1 분, 프로덕션 환경에서 응용 프로그램의 성능을 저하 이지만 진단 작업 결과 신속 하 게 테스트 하는 경우를 확인 하는 데 유용할 수 있습니다. hello 예약 된 전송 기간은 진단 데이터를 응용 프로그램의 hello 성능 영향을 주지 것입니다 충분히 큰 하지만 hello 인스턴스에서 덮어쓸 수 없습니다 만큼 작지 않아서 tooensure 이어야 합니다.

hello counterSpecifier 특성 hello 성능 카운터 toocollect를 지정합니다. hello sampleRate 특성 hello 속도는 hello 성능 카운터를 샘플링할이 경우 30 초를 지정 합니다.

원하는 toocollect hello 성능 카운터를 추가 하면 변경 내용이 toohello 진단 파일을 저장 합니다. 다음으로 hello 진단 데이터를 저장할 toospecify hello 저장소 계정이 있어야 합니다.

### <a name="specify-hello-storage-account"></a>Hello 저장소 계정을 지정합니다
진단 정보 tooyour Azure 저장소 계정으로 지정 해야 toopersist 프로그램 서비스 구성 파일 (ServiceConfiguration.cscfg)에 연결 문자열입니다.

Azure SDK 2.5에 대 한 저장소 계정 hello hello diagnostics.wadcfgx 파일에 지정할 수 있습니다.

> [!NOTE]
> 이러한 지침은 tooAzure SDK 2.4이 하 버전을 적용 하 고 아래 합니다. Azure SDK 2.5에 대 한 저장소 계정 hello hello diagnostics.wadcfgx 파일에 지정할 수 있습니다.
>
>

tooset hello 연결 문자열:

1. 저장소에 대 한 선호 하는 텍스트 편집기 및 연결 문자열을 설정 hello 사용 하 여 hello ServiceConfiguration.Cloud.cscfg 파일을 엽니다. hello *AccountName* 및 *AccountKey* 값은 hello 저장소 계정 대시보드의 액세스 키 아래에서 Azure 포털 hello에 있습니다.

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. Hello ServiceConfiguration.Cloud.cscfg 파일을 저장 합니다.
3. Hello ServiceConfiguration.Local.cscfg 파일을 열고 UseDevelopmentStorage tootrue 설정 되어 있는지 확인 합니다.

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   연결 문자열 hello를 설정 하에 응용 프로그램 응용 프로그램을 배포할 때 진단 데이터 tooyour 저장소 계정에 유지 됩니다.
4. 프로젝트를 저장하고 빌드한 다음 응용 프로그램을 배포합니다.

## <a name="step-2-optional-create-custom-performance-counters"></a>2단계: (옵션) 사용자 지정 성능 카운터 만들기
미리 정의 된 성능 카운터를 또한 toohello, 사용자 고유의 사용자 지정 성능 카운터 toomonitor 웹 또는 작업자 역할을 추가할 수 있습니다. 사용자 지정 성능 카운터 사용된 tootrack 및 모니터 응용 프로그램별 동작 및 수 수 생성 하거나 삭제할 수 시작 작업, 웹 역할 또는 작업자 역할이 승격 된 권한으로 합니다.

hello Azure 진단 에이전트가 hello 성능 카운터 구성을 hello.wadcfg 파일에서 시작한 후 1 분을 새로 고칩니다.  Hello OnStart 메서드에에서 사용자 지정 성능 카운터를 만들고 시작 작업 tooexecute 1 분 이상 걸릴 경우 사용자 지정 성능 카운터는 만들어지지 않은 hello Azure 진단 에이전트가 tooload 하려고 할 때 해당 합니다.  이 시나리오에서는 Azure 진단이 사용자 지정 성능 카운터를 제외한 모든 진단 데이터를 올바르게 캡처하는 것을 확인합니다.  tooresolve이이 문제를 hello 성능 카운터 시작 작업에서 만들거나 이동 hello 성능 카운터를 만든 후 toohello OnStart 메서드 시작 작업의 일부 작동 합니다.

다음 단계는 간단한 사용자 지정 성능 카운터 "\MyCustomCounterCategory\MyButton1Counter" 라는 toocreate hello를 수행 합니다.

1. 응용 프로그램에 대 한 hello 서비스 정의 파일 (CSDEF)을 엽니다.
2. Hello 런타임 요소 toohello WebRole 또는 WorkerRole 요소 tooallow 실행 상승 된 권한으로 추가 합니다.

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. Hello 파일을 저장 합니다.
4. (SDK 2.4와 그 하위 diagnostics.wadcfg 또는 SDK 2.5에서 이상 diagnostics.wadcfgx) hello 진단 파일을 열고 다음 toohello DiagnosticMonitorConfiguration hello 추가

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. Hello 파일을 저장 합니다.
6. 사용자 역할의 OnStart 메서드에 hello 자료를 호출 하기 전에 hello 사용자 지정 성능 카운터 범주를 만듭니다. OnStart 합니다. hello 다음 C# 예제에서는 만들고 사용자 지정 범주 아직 없는 경우:

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. 응용 프로그램 내에서 hello 카운터를 업데이트 합니다. 다음 예에서는 hello Button1_Click 이벤트에 사용자 지정 성능 카운터를 업데이트 합니다.

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. Hello 파일을 저장 합니다.  

사용자 지정 성능 카운터 데이터 이제 hello Azure 진단 모니터에 의해 수집 됩니다.

## <a name="step-3-query-performance-counter-data"></a>3단계: 성능 카운터 데이터 쿼리
응용 프로그램을 배포 하 고 실행 되 고 hello 진단 모니터가 시작 됩니다 되 면 성능 카운터를 수집 하 고 해당 데이터 tooAzure 저장소를 유지 합니다. 서버 탐색기와 같은 도구를 사용 하 여 Visual Studio에서 [Azure 저장소 탐색기](http://azurestorageexplorer.codeplex.com/), 또는 [Azure 진단 관리자](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) cerebrata tooview hello의에서 성능 카운터 데이터 hello WADPerformanceCountersTable 테이블입니다. 또한 프로그래밍 방식으로 사용 하 여 hello 테이블 서비스를 쿼리할 수 있습니다 [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), 또는 [PHP](../cosmos-db/table-storage-how-to-use-php.md)합니다.

hello 다음 C# 예제 hello WADPerformanceCountersTable 테이블에 대 한 기본 쿼리를 보여주며, hello 진단 데이터 tooa CSV 파일을 저장 합니다. Hello ÷ ´ ֹ tooa CSV 파일에 저장 되 면 hello 그래프 Microsoft Excel 또는 다른 도구 toovisualize hello 데이터가 기능을 사용할 수 있습니다. 있는지 tooadd 2012 이상.NET 년 10 월에 대 한 hello Azure SDK에에서 포함 된 참조 tooMicrosoft.WindowsAzure.Storage.dll를 수 있습니다. hello 어셈블리는 설치 된 toohello % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version 됩니다 디렉터리입니다.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

엔터티 tooC # 개체에서 파생 된 사용자 지정 클래스를 사용 하 여 매핑할 **TableEntity**합니다. hello 다음 코드에서는 정의 hello에서 성능 카운터를 나타내는 엔터티 클래스 **WADPerformanceCountersTable** 테이블입니다.

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a>다음 단계
[Azure 진단에 대한 추가 문서 보기](../azure-diagnostics.md)
