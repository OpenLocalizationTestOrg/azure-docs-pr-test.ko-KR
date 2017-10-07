---
title: "진단 1.2 구성 스키마 aaaAzure | Microsoft Docs"
description: "Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric 또는 Cloud Services에서 Azure SDK 2.5를 사용하는 경우에만 해당됩니다."
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
ms.openlocfilehash: 31559317b696556a64b51b58800b176ade9a4679
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-12-configuration-schema"></a>Azure 진단 1.2 구성 스키마
> [!NOTE]
> Azure 진단은 hello 사용 되는 구성 toocollect 성능 카운터 및 Azure 가상 컴퓨터, 가상 컴퓨터 크기 집합, 서비스 패브릭 및 클라우드 서비스에서 기타 통계입니다.  이 페이지는 이러한 서비스 중 하나를 사용하는 경우에만 해당됩니다.
>

Azure 진단은 Azure Monitor, Application Insights 및 Log Analytics와 같은 기타 Microsoft 진단 제품과 함께 사용됩니다.

이 스키마는 hello 가능한 값 hello 진단 모니터를 시작할 때 tooinitialize 진단 구성 설정을 사용할 수 있습니다.  


 Hello 다음 PowerShell 명령을 실행 하 여 hello 공용 구성 파일 스키마 정의 다운로드 합니다.  

```PowerShell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 Azure 진단에 대한 자세한 내용은 [Azure Cloud Services에서 진단을 사용하도록 설정](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/)을 참조하세요.  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Hello 진단 구성 파일의 예  
 다음 예제는 hello 일반적인 진단 구성 파일을 보여 줍니다.  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">  
  <WadCfg>  
    <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  
      <PerformanceCounters scheduledTransferPeriod="PT1M">  
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
      </PerformanceCounters>  
      <Directories scheduledTransferPeriod="PT5M">  
        <IISLogs containerName="iislogs" />  
        <FailedRequestLogs containerName="iisfailed" />  
        <DataSources>  
          <DirectoryConfiguration containerName="mynewprocess">  
            <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
          </DirectoryConfiguration>  
          <DirectoryConfiguration containerName="badapp">  
            <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
          </DirectoryConfiguration>  
          <DirectoryConfiguration containerName="goodapp">  
            <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
          </DirectoryConfiguration>  
        </DataSources>  
      </Directories>  
      <EtwProviders>  
        <EtwEventSourceProviderConfiguration provider="MyProviderClass" scheduledTransferPeriod="PT5M">  
          <Event id="0"/>  
          <Event id="1" eventDestination="errorTable"/>  
          <DefaultEvents />  
        </EtwEventSourceProviderConfiguration>  
        <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
          <Event id="0"/>  
          <DefaultEvents eventDestination="defaultTable"/>  
        </EtwManifestProviderConfiguration>  
      </EtwProviders>  
      <WindowsEventLog scheduledTransferPeriod="PT5M">  
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
        <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
        <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
      </WindowsEventLog>  
      <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
        <CrashDumpConfiguration processName="mynewprocess.exe" />  
        <CrashDumpConfiguration processName="badapp.exe"/>  
      </CrashDumps>  
    </DiagnosticMonitorConfiguration>  
  </WadCfg>  
</PublicConfig>  

```  

## <a name="diagnostics-configuration-namespace"></a>진단 구성 네임스페이스  
 다음은 hello 진단 구성 파일에 대 한 hello XML 네임 스페이스가입니다.  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="publicconfig-element"></a>PublicConfig 요소  
 Hello 진단 구성 파일의 최상위 요소입니다. hello 다음 설명 hello 구성 파일의 hello 요소입니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**WadCfg**|필수입니다. 원격 분석 데이터 toobe hello에 대 한 구성 설정을 수집 합니다.|  
|**StorageAccount**|hello Azure 저장소 계정 toostore hello 데이터에서의 hello 이름입니다. 이 지정할 수 있습니다를 매개 변수로 hello 집합 AzureServiceDiagnosticsExtension cmdlet을 실행 하는 경우.|  
|**LocalResourceDirectory**|hello Monitoring Agent toostore 이벤트 데이터에서 사용 하는 hello 가상 컴퓨터 toobe hello 디렉터리입니다. 그렇지 않으면 집합, hello 기본 디렉터리가 사용 됩니다.<br /><br /> 작업자/웹 역할의 경우: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> 가상 컴퓨터의 경우: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> 필수 특성은 다음과 같습니다.<br /><br /> -                      **경로** -hello 디렉터리에서 Azure 진단을 사용 하는 hello 시스템 toobe에 있습니다.<br /><br /> -                      **expandEnvironment** -환경 변수 hello 경로 이름으로 확장 되는 여부를 제어 합니다.|  

## <a name="wadcfg-element"></a>WadCFG 요소  
Hello 원격 분석 데이터 toobe 수집에 대 한 구성 설정을 정의 합니다. 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**DiagnosticMonitorConfiguration**|필수입니다. 선택적 특성은 다음과 같습니다.<br /><br /> -                     **overallQuotaInMB** -hello에서 사용 될 수 있는 로컬 디스크 공간의 최대 크기 hello Azure 진단에서 수집 된 진단 데이터의 다양 한 형식입니다. hello 기본 설정은 5120MB입니다.<br /><br /> -                     **useProxyServer** -IE 설정에 설정 된 대로 Azure 진단 구성 toouse hello 프록시 서버 설정 합니다.|  
|**CrashDumps**|크래시 덤프의 수집을 사용하도록 설정합니다. 선택적 특성은 다음과 같습니다.<br /><br /> -                     **containerName** -Azure 저장소 계정 toobe의 hello blob 컨테이너의 hello 이름이 toostore 크래시 덤프를 사용 합니다.<br /><br /> -                     **crashDumpType** -Azure 진단 구성 toocollect 미니 또는 전체 크래시 덤프 합니다.<br /><br /> -                     **directoryQuotaPercentage**-의 hello 비율을 구성 **overallQuotaInMB** toobe hello VM에 크래시 덤프에 사용 되도록 예약 합니다.|  
|**DiagnosticInfrastructureLogs**|Azure 진단에 의해 생성된 로그의 컬렉션을 사용하도록 설정합니다. hello 진단 인프라 로그는 hello 진단 시스템 자체의 문제를 해결 하는 데 유용 합니다. 선택적 특성은 다음과 같습니다.<br /><br /> -                     **scheduledTransferLogLevelFilter** -hello 로그가 수집의 hello 최소 심각도 수준을 구성 합니다.<br /><br /> -                     **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다. hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**Directories**|사용 하도록 설정 hello 디렉터리의 hello 콘텐츠의 컬렉션, IIS 실패 한 액세스 요청 로그 및/또는 IIS 로그 합니다. 선택적 특성:<br /><br /> **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다. hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**EtwProviders**|EventSource의 ETW 이벤트 및/또는 공급자를 기반으로 하는 ETW 매니페스트의 컬렉션을 구성합니다.|  
|**metrics**|이 요소에 빠른 쿼리 최적화 된 성능 카운터 테이블 toogenerate가 있습니다. Hello에 정의 된 각 성능 카운터 **PerformanceCounters** 요소 또한 toohello 성능 카운터 표에 hello 메트릭 테이블에 저장 됩니다. 필수 특성:<br /><br /> **resourceId** -hello 하도록 Azure 진단을 배포 하는 가상 컴퓨터의 hello 리소스 ID입니다. Hello 가져오기 **resourceID** hello에서 [Azure 포털](https://portal.azure.com)합니다. **찾아보기** -> **리소스 그룹** -> **<이름\>**을 선택합니다. Hello 클릭 **속성** 타일 및 hello에서 hello 값 복사 **ID** 필드입니다.|  
|**PerformanceCounters**|성능 카운터의 hello 컬렉션을 수 있습니다. 선택적 특성:<br /><br /> **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다. 값은 [XML "기간 데이터 형식"](http://www.w3schools.com/schema/schema_dtypes_date.asp)입니다.|  
|**WindowsEventLog**|Windows 이벤트 로그의 hello 컬렉션을 수 있습니다. 선택적 특성:<br /><br /> **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다. 값은 [XML "기간 데이터 형식"](http://www.w3schools.com/schema/schema_dtypes_date.asp)입니다.|  

## <a name="crashdumps-element"></a>CrashDumps 요소  
 크래시 덤프의 수집을 사용하도록 설정합니다. 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**CrashDumpConfiguration**|필수입니다. 필수 특성:<br /><br /> **processName** -hello toocollect Azure 진단에 대 한 크래시 덤프를 원하는 hello 프로세스의 이름입니다.|  
|**crashDumpType**|Azure 진단 toocollect 미니 또는 전체 크래시 덤프를 구성합니다.|  
|**directoryQuotaPercentage**|hello 비율을 구성 **overallQuotaInMB** toobe hello VM에 크래시 덤프에 사용 되도록 예약 합니다.|  

## <a name="directories-element"></a>Directories 요소  
 사용 하도록 설정 hello 디렉터리의 hello 콘텐츠의 컬렉션, IIS 실패 한 액세스 요청 로그 및/또는 IIS 로그 합니다. 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**DataSources**|목록 디렉터리 toomonitor입니다.|  
|**FailedRequestLogs**|이 요소를 포함 하 여 hello 구성에 실패 한 요청 tooan IIS 사이트 또는 응용 프로그램에 대 한 로그 컬렉션을에 있습니다. 또한 **Web.config**의 **system.WebServer**에 있는 추적 옵션도 사용하도록 설정해야 합니다.|  
|**IISLogs**|이 요소를 포함 하 여 hello 구성에서 IIS 로그 컬렉션을 hello 있습니다.<br /><br /> **containerName** -Azure 저장소 계정 toobe의 hello blob 컨테이너의 hello 이름이 toostore hello IIS 로그를 사용 합니다.|  

## <a name="datasources-element"></a>DataSources 요소  
 목록 디렉터리 toomonitor입니다. 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**DirectoryConfiguration**|필수입니다. 필수 특성:<br /><br /> **containerName** -Azure 저장소에 hello blob 컨테이너의 hello 이름을 계정 사용 toobe toostore hello 로그 파일입니다.|  

## <a name="directoryconfiguration-element"></a>DirectoryConfiguration 요소  
 **DirectoryConfiguration** 어느 hello 포함 될 수 있습니다 **절대** 또는 **LocalResource** 요소 중 하나만 있습니다. 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**Absolute**|hello toohello 디렉터리 toomonitor 절대 경로입니다. hello 특성 다음 사항이 필요 합니다.<br /><br /> -                     **경로** -hello toohello 디렉터리 toomonitor 절대 경로입니다.<br /><br /> -                      **expandEnvironment** - 경로의 환경 변수가 확장되어 있는지 여부를 구성합니다.|  
|**LocalResource**|hello 경로 상대 tooa 로컬 리소스 toomonitor 합니다. 필수 특성은 다음과 같습니다.<br /><br /> -                     **이름** -hello hello 디렉터리 toomonitor 포함 된 로컬 리소스<br /><br /> -                     **relativePath** -hello 디렉터리 toomonitor 포함 된 상대 경로 tooName hello|  

## <a name="etwproviders-element"></a>EtwProviders 요소  
 EventSource의 ETW 이벤트 및/또는 공급자를 기반으로 하는 ETW 매니페스트의 컬렉션을 구성합니다. 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|[EventSource 클래스](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)에서 생성된 이벤트 컬렉션을 구성합니다. 필수 특성:<br /><br /> **공급자** -hello EventSource 이벤트의 hello 클래스 이름입니다.<br /><br /> 선택적 특성은 다음과 같습니다.<br /><br /> -                     **scheduledTransferLogLevelFilter** -hello 최소 심각도 수준 tootransfer tooyour 저장소 계정입니다.<br /><br /> -                     **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다. 값은 [XML 기간 데이터 형식](http://www.w3schools.com/schema/schema_dtypes_date.asp)입니다.|  
|**EtwManifestProviderConfiguration**|필수 특성:<br /><br /> **공급자** -hello hello 이벤트 공급자의 GUID<br /><br /> 선택적 특성은 다음과 같습니다.<br /><br /> - **scheduledTransferLogLevelFilter** -hello 최소 심각도 수준 tootransfer tooyour 저장소 계정입니다.<br /><br /> -                     **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다. 값은 [XML 기간 데이터 형식](http://www.w3schools.com/schema/schema_dtypes_date.asp)입니다.|  

## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration 요소  
 [EventSource 클래스](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)에서 생성된 이벤트 컬렉션을 구성합니다. 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**DefaultEvents**|선택적 특성:<br /><br /> **eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름|  
|**Event**|필수 특성:<br /><br /> **id** -hello 이벤트의 hello id입니다.<br /><br /> 선택적 특성:<br /><br /> **eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름|  

## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration 요소  
 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**DefaultEvents**|선택적 특성:<br /><br /> **eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름|  
|**Event**|필수 특성:<br /><br /> **id** -hello 이벤트의 hello id입니다.<br /><br /> 선택적 특성:<br /><br /> **eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름|  

## <a name="metrics-element"></a>Metrics 요소  
 빠른 쿼리를 위해 최적화 된 성능 카운터 테이블 toogenerate가 있습니다. 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**MetricAggregation**|필수 특성:<br /><br /> **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다. 값은 [XML 기간 데이터 형식](http://www.w3schools.com/schema/schema_dtypes_date.asp)입니다.|  

## <a name="performancecounters-element"></a>PerformanceCounters 요소  
 성능 카운터의 hello 컬렉션을 수 있습니다. 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**PerformanceCounterConfiguration**|hello 특성 다음 사항이 필요 합니다.<br /><br /> -                     **counterSpecifier** -hello hello 성능 카운터의 이름입니다. 예: `\Processor(_Total)\% Processor Time`. hello 명령을 실행 하 여 호스트에서 성능 카운터 목록은 tooget `typeperf`합니다.<br /><br /> -                     **sampleRate** -얼마나 자주 hello 카운터를 샘플링 됩니다.<br /><br /> 선택적 특성:<br /><br /> **단위** -hello hello 카운터의 측정 단위입니다.|  

## <a name="performancecounterconfiguration-element"></a>PerformanceCounterConfiguration 요소  
 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**annotation**|필수 특성:<br /><br /> **displayName** -hello 카운터에 대 한 hello 표시 이름<br /><br /> 선택적 특성:<br /><br /> **로캘** -hello 카운터 이름을 표시할 때 로캘 toouse hello|  

## <a name="windowseventlog-element"></a>WindowsEventLog 요소  
 다음 표에서 hello 자식 요소에 설명 합니다.  

|요소 이름|설명|  
|------------------|-----------------|  
|**DataSource**|Windows 이벤트 로그 toocollect hello 합니다. 필수 특성:<br /><br /> **이름** -hello windows 이벤트 toobe를 설명 하는 hello XPath 쿼리를 수집 합니다. 예:<br /><br /> `Application!*[System[(Level >= 3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level >= 3]]`<br /><br /> 모든 이벤트를 지정 하는 toocollect "*"입니다.|
