---
title: "진단 1.0 구성 스키마 aaaAzure | Microsoft Docs"
description: "Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric 또는 Cloud Services에서 Azure SDK 2.4 이하를 사용하는 경우에만 해당됩니다."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a>Azure 진단 1.0 구성 스키마
> [!NOTE]
> Azure 진단은 hello 사용 되는 구성 toocollect 성능 카운터 및 Azure 가상 컴퓨터, 가상 컴퓨터 크기 집합, 서비스 패브릭 및 클라우드 서비스에서 기타 통계입니다.  이 페이지는 이러한 서비스 중 하나를 사용하는 경우에만 해당됩니다.
>

Azure 진단은 Azure Monitor, Application Insights 및 Log Analytics와 같은 기타 Microsoft 진단 제품과 함께 사용됩니다.

hello Azure 진단 구성 파일 값을 사용 하는 tooinitialize hello 진단 모니터를 정의 합니다. 이 파일은 hello 진단 모니터를 시작 하는 경우 사용 되는 tooinitialize 진단 구성 설정입니다.  

 기본적으로 hello Azure 진단 구성 스키마 파일은 설치 된 toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` 디렉터리입니다. 대체 `<version>` hello 설치 된 버전의 hello [Azure SDK](http://www.windowsazure.com/develop/downloads/)합니다.  

> [!NOTE]
>  hello 진단 구성 파일은 일반적으로 진단 데이터 toobe hello 시작 프로세스의 앞부분에 나오는 수집 해야 하는 시작 작업에 사용 됩니다. Azure 진단에 대한 자세한 내용은 [Azure 진단을 사용하여 로깅 데이터 수집](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7)을 참조하세요.  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Hello 진단 구성 파일의 예  
 다음 예제는 hello 일반적인 진단 구성 파일을 보여 줍니다.  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a>DiagnosticsConfiguration 네임스페이스  
 다음은 hello 진단 구성 파일에 대 한 hello XML 네임 스페이스가입니다.  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a>스키마 요소  
 hello 진단 구성 파일에 hello 요소 다음에 포함 됩니다.


## <a name="diagnosticmonitorconfiguration-element"></a>DiagnosticMonitorConfiguration 요소  
hello hello 진단 구성 파일의 최상위 요소입니다.  

특성:

|특성  |유형   |필수| 기본값 | 설명|  
|-----------|-------|--------|---------|------------|  
|**configurationChangePollInterval**|duration|옵션 | PT1M| 진단 구성 변경에 대 한 hello 진단 모니터를 폴링하는 간격이 hello를 지정합니다.|  
|**overallQuotaInMB**|unsignedInt|옵션| 4000MB 값을 제공하는 경우 이 크기를 초과하지 않아야 합니다. |hello 모든 로깅 버퍼에 할당 된 파일 시스템 저장소의 총 양입니다.|  

## <a name="diagnosticinfrastructurelogs-element"></a>DiagnosticInfrastructureLogs 요소  
Hello 기본 진단 인프라에서 생성 되는 hello 로그에 대 한 hello 버퍼 구성을 정의 합니다.

부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).  

특성:

|특성|형식|설명|  
|---------|----|-----------------|  
|**bufferQuotaInMB**|unsignedInt|선택 사항입니다. Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.<br /><br /> hello 기본값은 0입니다.|  
|**scheduledTransferLogLevelFilter**|string|선택 사항입니다. 전송 되는 로그 항목에 대 한 hello 최소 심각도 수준을 지정 합니다. hello 기본값은 **Undefined**합니다. 사용 가능한 다른 값은 **Verbose**, **Information**, **Warning**, **Error**, 및 **Critical**입니다.|  
|**scheduledTransferPeriod**|duration|선택 사항입니다. Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.<br /><br /> hello 기본값은 pt0s입니다.|  

## <a name="logs-element"></a>Logs 요소  
 기본 Azure 로그에 대 한 hello 버퍼 구성을 정의합니다.

 부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).  

특성:  

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|선택 사항입니다. Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.<br /><br /> hello 기본값은 0입니다.|  
|**scheduledTransferLogLevelFilter**|string|선택 사항입니다. 전송 되는 로그 항목에 대 한 hello 최소 심각도 수준을 지정 합니다. hello 기본값은 **Undefined**합니다. 사용 가능한 다른 값은 **Verbose**, **Information**, **Warning**, **Error**, 및 **Critical**입니다.|  
|**scheduledTransferPeriod**|duration|선택 사항입니다. Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.<br /><br /> hello 기본값은 pt0s입니다.|  

## <a name="directories-element"></a>Directories 요소  
정의할 수 있는 파일 기반 로그에 대 한 hello 버퍼 구성을 정의 합니다.

부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).  


특성:  

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|선택 사항입니다. Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.<br /><br /> hello 기본값은 0입니다.|  
|**scheduledTransferPeriod**|duration|선택 사항입니다. Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.<br /><br /> hello 기본값은 pt0s입니다.|  

## <a name="crashdumps-element"></a>CrashDumps 요소  
 Hello 크래시 덤프 디렉터리를 정의합니다.

 부모 요소: [Directories 요소](#Directories).  

특성:  

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**container**|string|여기서 hello 디렉터리의 내용을 hello는 toobe hello 컨테이너의 hello 이름을 전송 합니다.|  
|**directoryQuotaInMB**|unsignedInt|선택 사항입니다. Hello hello 디렉터리의 최대 크기를 메가바이트 단위로 지정합니다.<br /><br /> hello 기본값은 0입니다.|  

## <a name="failedrequestlogs-element"></a>FailedRequestLogs 요소  
 Hello 실패 한 요청 로그 디렉터리를 정의합니다.

 부모 요소[Directories 요소](#Directories).  

특성:  

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**container**|string|여기서 hello 디렉터리의 내용을 hello는 toobe hello 컨테이너의 hello 이름을 전송 합니다.|  
|**directoryQuotaInMB**|unsignedInt|선택 사항입니다. Hello hello 디렉터리의 최대 크기를 메가바이트 단위로 지정합니다.<br /><br /> hello 기본값은 0입니다.|  

##  <a name="iislogs-element"></a>IISLogs 요소  
 Hello IIS 로그 디렉터리를 정의합니다.

 부모 요소[Directories 요소](#Directories).  

특성:  

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**container**|string|여기서 hello 디렉터리의 내용을 hello는 toobe hello 컨테이너의 hello 이름을 전송 합니다.|  
|**directoryQuotaInMB**|unsignedInt|선택 사항입니다. Hello hello 디렉터리의 최대 크기를 메가바이트 단위로 지정합니다.<br /><br /> hello 기본값은 0입니다.|  

## <a name="datasources-element"></a>DataSources 요소  
 0개 이상의 추가 로그 디렉터리를 정의합니다.

 부모 요소: [Directories 요소](#Directories).

## <a name="directoryconfiguration-element"></a>DirectoryConfiguration 요소  
 로그 파일 toomonitor의 hello 디렉터리를 정의합니다.

 부모 요소: [DataSources 요소](#DataSources)

특성:

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**container**|string|여기서 hello 디렉터리의 내용을 hello는 toobe hello 컨테이너의 hello 이름을 전송 합니다.|  
|**directoryQuotaInMB**|unsignedInt|선택 사항입니다. Hello hello 디렉터리의 최대 크기를 메가바이트 단위로 지정합니다.<br /><br /> hello 기본값은 0입니다.|  

## <a name="absolute-element"></a>Absolute 요소  
 선택적 환경 확장으로 hello 디렉터리 toomonitor의 절대 경로 정의합니다.

 부모 요소: [DirectoryConfiguration 요소](#DirectoryConfiguration).  

특성:  

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**path**|string|필수입니다. hello toohello 디렉터리 toomonitor 절대 경로입니다.|  
|**expandEnvironment**|부울|필수입니다. 경우 너무 설정**true**, hello 경로에 환경 변수 확장 됩니다.|  

## <a name="localresource-element"></a>LocalResource 요소  
 Hello 서비스 정의에 지정 된 경로 상대 tooa 로컬 리소스를 정의 합니다.

 부모 요소: [DirectoryConfiguration 요소](#DirectoryConfiguration).  

특성:  

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**name**|string|필수입니다. hello 디렉터리 toomonitor를 포함 하는 hello 로컬 리소스의 hello 이름입니다.|  
|**relativePath**|string|필수입니다. hello 경로 상대 toohello 로컬 리소스 toomonitor 합니다.|  

## <a name="performancecounters-element"></a>PerformanceCounters 요소  
 Hello 경로 toohello 성능 카운터 toocollect를 정의합니다.

 부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).


 특성:  

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|선택 사항입니다. Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.<br /><br /> hello 기본값은 0입니다.|  
|**scheduledTransferPeriod**|duration|선택 사항입니다. Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.<br /><br /> hello 기본값은 pt0s입니다.|  

## <a name="performancecounterconfiguration-element"></a>PerformanceCounterConfiguration 요소  
 성능 카운터 toocollect hello를 정의합니다.

 부모 요소: [PerformanceCounters 요소](#PerformanceCounters).  

 특성:  

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**counterSpecifier**|string|필수입니다. hello 경로 toohello 성능 카운터 toocollect 합니다.|  
|**sampleRate**|duration|필수입니다. hello 속도 hello에서 성능 카운터를 수집 해야 합니다.|  

## <a name="windowseventlog-element"></a>WindowsEventLog 요소  
 이벤트 로그 toomonitor hello를 정의합니다.

 부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).

  특성:

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|선택 사항입니다. Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.<br /><br /> hello 기본값은 0입니다.|  
|**scheduledTransferLogLevelFilter**|string|선택 사항입니다. 전송 되는 로그 항목에 대 한 hello 최소 심각도 수준을 지정 합니다. hello 기본값은 **Undefined**합니다. 사용 가능한 다른 값은 **Verbose**, **Information**, **Warning**, **Error**, 및 **Critical**입니다.|  
|**scheduledTransferPeriod**|duration|선택 사항입니다. Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.<br /><br /> hello 기본값은 pt0s입니다.|  

## <a name="datasource-element"></a>DataSource 요소  
 이벤트 로그 toomonitor hello를 정의합니다.

 부모 요소: [WindowsEventLog 요소](#windowsEventLog)  

 특성:

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**name**|string|필수입니다. Hello 로그 toocollect를 지정 하는 XPath 식입니다.|  
