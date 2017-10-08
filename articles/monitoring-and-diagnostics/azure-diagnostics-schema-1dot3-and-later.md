---
title: "aaaAzure 진단 확장 1.3 이상 구성 스키마 | Microsoft Docs"
description: "스키마 버전 1.3 및 이후 Azure 진단에서 Microsoft Azure SDK 2.4 이상 hello의 일부로 제공 되었습니다."
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
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a>Azure 진단 1.3 이상 구성 스키마
> [!NOTE]
> hello Azure 진단 확장은 toocollect 성능 카운터 및 기타 통계에서 사용 하는 hello 구성 요소입니다.
> - Azure 가상 컴퓨터 
> - 가상 컴퓨터 크기 집합
> - 서비스 패브릭 
> - 클라우드 서비스 
> - 네트워크 보안 그룹
> 
> 이 페이지는 이러한 서비스 중 하나를 사용하는 경우에만 해당됩니다.

이 페이지는 버전 1.3 이상(Azure SDK 2.4 이상)에 유효합니다. 최신 구성 섹션은 추가 된 버전의 주석 처리 된 tooshow 합니다.  

hello 구성 파일이 여기에 설명 된 경우 진단 구성 설정을 사용 하는 tooset hello 진단 모니터를 시작 하는 경우  

hello 확장이 Azure 모니터, Application Insights 및 분석 로그와 같은 다른 Microsoft 진단 제품과 함께에서 사용 됩니다.



Hello 다음 PowerShell 명령을 실행 하 여 hello 공용 구성 파일 스키마 정의 다운로드 합니다.  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

Azure 진단 사용에 대한 자세한 내용은 [Azure 진단 확장](azure-diagnostics.md)을 참조하세요.  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Hello 진단 구성 파일의 예  
 다음 예제는 hello 일반적인 진단 구성 파일을 보여 줍니다.  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
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
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
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

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

Hello 이전 XML 구성 파일의 JSON와 동일 합니다. 

다른 변수로 전달 되므로 대부분의 json 사용 경우에서 PublicConfig hello 및 PrivateConfig 구분 됩니다. 이러한 경우에는 Resource Manager 템플릿, 가상 컴퓨터 확장 집합 PowerShell 및 Visual Studio가 있습니다. 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "ApplicationInsights",
                    "ApplicationInsights": "{Insert InstrumentationKey}",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a>이 페이지 읽기  
 hello 다음 태그는 대략 hello 예제 앞에 표시 된 순서입니다.  필요한 위치에 대 한 전체 설명은 표시 되지 않으면, hello 요소 또는 특성에 대 한 hello 페이지를 검색 합니다.  

## <a name="common-attribute-types"></a>일반 특성 유형  
 **scheduledTransferPeriod** 특성이 몇 가지 요소에 나타납니다. 것 hello 간격 예약 된 전송 toostorage toohello 가장 근접 한 분을 반올림 합니다. hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp)


## <a name="diagnosticsconfiguration-element"></a>DiagnosticsConfiguration 요소  
 *Tree: Root - DiagnosticsConfiguration*

버전 1.3에 추가되었습니다.  

hello hello 진단 구성 파일의 최상위 요소입니다.  

**특성** xmlns-hello 진단 구성 파일에 대 한 XML 네임 스페이스 hello:  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  


|자식 요소|설명|  
|--------------------|-----------------|  
|**PublicConfig**|필수입니다. 이 페이지의 다른 곳에 있는 설명을 참조하세요.|  
|**PrivateConfig**|선택 사항입니다. 이 페이지의 다른 곳에 있는 설명을 참조하세요.|  
|**IsEnabled**|부울 값입니다. 이 페이지의 다른 곳에 있는 설명을 참조하세요.|  

## <a name="publicconfig-element"></a>PublicConfig 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig*

 Hello 공용 진단 구성에 설명 합니다.  

|자식 요소|설명|  
|--------------------|-----------------|  
|**WadCfg**|필수입니다. 이 페이지의 다른 곳에 있는 설명을 참조하세요.|  
|**StorageAccount**|hello Azure 저장소 계정 toostore hello 데이터에서의 hello 이름입니다. 지정할 수도 있습니다를 매개 변수로 hello 집합 AzureServiceDiagnosticsExtension cmdlet을 실행 하는 경우.|  
|**StorageType**|*Table*, *Blob* 또는 *TableAndBlob*일 수 있습니다. Table이 기본값입니다. TableAndBlob 선택 될 때 진단 데이터는 두 번 한 번씩 기록 tooeach 유형.|  
|**LocalResourceDirectory**|여기서 hello Monitoring Agent 이벤트 데이터를 저장 하는 hello 가상 컴퓨터에 hello 디렉터리입니다. 그렇지 않은 경우 설정, hello 기본 디렉터리가 사용 됩니다.<br /><br /> 작업자/웹 역할의 경우: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> 가상 컴퓨터의 경우: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> 필수 특성은 다음과 같습니다.<br /><br /> - **경로** -hello 디렉터리에서 Azure 진단을 사용 하는 hello 시스템 toobe에 있습니다.<br /><br /> - **expandEnvironment** -환경 변수 hello 경로 이름으로 확장 되는 여부를 제어 합니다.|  

## <a name="wadcfg-element"></a>WadCFG 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*
 
 식별 하 고 hello 원격 분석 데이터 toobe 수집을 구성 합니다.  


## <a name="diagnosticmonitorconfiguration-element"></a>DiagnosticMonitorConfiguration 요소 
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*

 필수 

|특성|설명|  
|----------------|-----------------|  
| **overallQuotaInMB** | hello에서 사용 될 수 있는 로컬 디스크 공간의 최대 크기 hello 다양 한 유형의 진단 데이터는 Azure 진단에서 수집 합니다. hello 기본 설정은 5120MB입니다.<br />
|**useProxyServer** | IE 설정에 설정 된 대로 Azure 진단 toouse hello 프록시 서버 설정을 구성 합니다.|  

<br /> <br />

|자식 요소|설명|  
|--------------------|-----------------|  
|**CrashDumps**|이 페이지의 다른 곳에 있는 설명을 참조하세요.|  
|**DiagnosticInfrastructureLogs**|Azure 진단에 의해 생성된 로그의 컬렉션을 사용하도록 설정합니다. hello 진단 인프라 로그는 hello 진단 시스템 자체의 문제를 해결 하는 데 유용 합니다. 선택적 특성은 다음과 같습니다.<br /><br /> - **scheduledTransferLogLevelFilter** -hello 로그가 수집의 hello 최소 심각도 수준을 구성 합니다.<br /><br /> - **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다. hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**Directories**|이 페이지의 다른 곳에 있는 설명을 참조하세요.|  
|**EtwProviders**|이 페이지의 다른 곳에 있는 설명을 참조하세요.|  
|**metrics**|이 페이지의 다른 곳에 있는 설명을 참조하세요.|  
|**PerformanceCounters**|이 페이지의 다른 곳에 있는 설명을 참조하세요.|  
|**WindowsEventLog**|이 페이지의 다른 곳에 있는 설명을 참조하세요.| 
|**DockerSources**|이 페이지의 다른 곳에 있는 설명을 참조하세요. | 



## <a name="crashdumps-element"></a>CrashDumps 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*
 
 크래시 덤프의 수집 hello를 사용 하도록 설정 합니다.  

|특성|설명|  
|----------------|-----------------|  
|**containerName**|선택 사항입니다. Azure 저장소 계정 toobe의 hello blob 컨테이너의 hello 이름이 toostore 크래시 덤프를 사용 합니다.|  
|**crashDumpType**|선택 사항입니다.  Azure 진단 toocollect 미니 또는 전체 크래시 덤프를 구성합니다.|  
|**directoryQuotaPercentage**|선택 사항입니다.  hello 비율을 구성 **overallQuotaInMB** toobe hello VM에 크래시 덤프에 사용 되도록 예약 합니다.|  

|자식 요소|설명|  
|--------------------|-----------------|  
|**CrashDumpConfiguration**|필수입니다. 각 프로세스에 대한 구성 값을 정의합니다.<br /><br /> hello 다음 특성은도 필요 합니다.<br /><br /> **processName** -hello toocollect Azure 진단에 대 한 크래시 덤프를 원하는 hello 프로세스의 이름입니다.|  

## <a name="directories-element"></a>Directories 요소 
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*

 사용 하도록 설정 hello 디렉터리의 hello 콘텐츠의 컬렉션, IIS 실패 한 액세스 요청 로그 및/또는 IIS 로그 합니다.  

 선택적 **scheduledTransferPeriod** 특성입니다. 이전 설명을 참조하세요.  

|자식 요소|설명|  
|--------------------|-----------------|  
|**IISLogs**|이 요소를 포함 하 여 hello 구성에서 IIS 로그 컬렉션을 hello 있습니다.<br /><br /> **containerName** -Azure 저장소 계정 toobe의 hello blob 컨테이너의 hello 이름이 toostore hello IIS 로그를 사용 합니다.|   
|**FailedRequestLogs**|이 요소를 포함 하 여 hello 구성에 실패 한 요청 tooan IIS 사이트 또는 응용 프로그램에 대 한 로그 컬렉션을에 있습니다. 또한 **Web.config**의 **system.WebServer**에 있는 추적 옵션도 사용하도록 설정해야 합니다.|  
|**DataSources**|목록 디렉터리 toomonitor입니다.| 




## <a name="datasources-element"></a>DataSources 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*

 목록 디렉터리 toomonitor입니다.  

|자식 요소|설명|  
|--------------------|-----------------|  
|**DirectoryConfiguration**|필수입니다. 필수 특성:<br /><br /> **containerName** -hello 해당 toobe toostore hello 로그 파일을 사용 하 여 Azure 저장소 계정에 hello blob 컨테이너의 이름입니다.|  





## <a name="directoryconfiguration-element"></a>DirectoryConfiguration 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*

 어느 hello 포함 될 수 있습니다 **절대** 또는 **LocalResource** 요소 중 하나만 있습니다.  

|자식 요소|설명|  
|--------------------|-----------------|  
|**Absolute**|hello toohello 디렉터리 toomonitor 절대 경로입니다. hello 특성 다음 사항이 필요 합니다.<br /><br /> - **경로** -hello toohello 디렉터리 toomonitor 절대 경로입니다.<br /><br /> - **expandEnvironment** - 경로의 환경 변수가 확장되어 있는지 여부를 구성합니다.|  
|**LocalResource**|hello 경로 상대 tooa 로컬 리소스 toomonitor 합니다. 필수 특성은 다음과 같습니다.<br /><br /> - **이름** -hello hello 디렉터리 toomonitor 포함 된 로컬 리소스<br /><br /> - **relativePath** -hello 디렉터리 toomonitor 포함 된 상대 경로 tooName hello|  



## <a name="etwproviders-element"></a>EtwProviders 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*

 EventSource의 ETW 이벤트 및/또는 공급자를 기반으로 하는 ETW 매니페스트의 컬렉션을 구성합니다.  

|자식 요소|설명|  
|--------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|[EventSource 클래스](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)에서 생성된 이벤트 컬렉션을 구성합니다. 필수 특성:<br /><br /> **공급자** -hello EventSource 이벤트의 hello 클래스 이름입니다.<br /><br /> 선택적 특성은 다음과 같습니다.<br /><br /> - **scheduledTransferLogLevelFilter** -hello 최소 심각도 수준 tootransfer tooyour 저장소 계정입니다.<br /><br /> - **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다. hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**EtwManifestProviderConfiguration**|필수 특성:<br /><br /> **공급자** -hello hello 이벤트 공급자의 GUID<br /><br /> 선택적 특성은 다음과 같습니다.<br /><br /> - **scheduledTransferLogLevelFilter** -hello 최소 심각도 수준 tootransfer tooyour 저장소 계정입니다.<br /><br /> - **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다. hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*

 [EventSource 클래스](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)에서 생성된 이벤트 컬렉션을 구성합니다.  

|자식 요소|설명|  
|--------------------|-----------------|  
|**DefaultEvents**|선택적 특성:<br/><br/> **eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름|  
|**Event**|필수 특성:<br /><br /> **id** -hello 이벤트의 hello id입니다.<br /><br /> 선택적 특성:<br /><br /> **eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름|  



## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*

|자식 요소|설명|  
|--------------------|-----------------|  
|**DefaultEvents**|선택적 특성:<br /><br /> **eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름|  
|**Event**|필수 특성:<br /><br /> **id** -hello 이벤트의 hello id입니다.<br /><br /> 선택적 특성:<br /><br /> **eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름|  



## <a name="metrics-element"></a>Metrics 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*

 빠른 쿼리를 위해 최적화 된 성능 카운터 테이블 toogenerate가 있습니다. Hello에 정의 된 각 성능 카운터 **PerformanceCounters** 요소 또한 toohello 성능 카운터 표에 hello 메트릭 테이블에 저장 됩니다.  

 hello **resourceId** 특성이 필요 합니다.  hello hello 하도록 Azure 진단을 배포 하는 가상 컴퓨터의 리소스 ID입니다. Hello 가져오기 **resourceID** hello에서 [Azure 포털](https://portal.azure.com)합니다. **찾아보기** -> **리소스 그룹** -> **<이름\>**을 선택합니다. Hello 클릭 **속성** 타일 및 hello에서 hello 값 복사 **ID** 필드입니다.  

|자식 요소|설명|  
|--------------------|-----------------|  
|**MetricAggregation**|필수 특성:<br /><br /> **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다. hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="performancecounters-element"></a>PerformanceCounters 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*

 성능 카운터의 hello 컬렉션을 수 있습니다.  

 선택적 특성:  

 선택적 **scheduledTransferPeriod** 특성입니다. 이전 설명을 참조하세요.

|자식 요소|설명|  
|-------------------|-----------------|  
|**PerformanceCounterConfiguration**|hello 특성 다음 사항이 필요 합니다.<br /><br /> - **counterSpecifier** -hello hello 성능 카운터의 이름입니다. 예: `\Processor(_Total)\% Processor Time`. tooget hello 명령을 실행 호스트에 목록이 성능 카운터 `typeperf`합니다.<br /><br /> - **sampleRate** -얼마나 자주 hello 카운터를 샘플링 됩니다.<br /><br /> 선택적 특성:<br /><br /> **단위** -hello hello 카운터의 측정 단위입니다.|  




## <a name="windowseventlog-element"></a>WindowsEventLog 요소
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*
 
 Windows 이벤트 로그의 hello 컬렉션을 수 있습니다.  

 선택적 **scheduledTransferPeriod** 특성입니다. 이전 설명을 참조하세요.  

|자식 요소|설명|  
|-------------------|-----------------|  
|**DataSource**|Windows 이벤트 로그 toocollect hello 합니다. 필수 특성:<br /><br /> **이름** -hello windows 이벤트 toobe를 설명 하는 hello XPath 쿼리를 수집 합니다. 예:<br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> 모든 이벤트를 지정 하는 toocollect "*"|  




## <a name="logs-element"></a>Logs 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*

 버전 1.0 및 1.1에서 제공됩니다. 1.2에는 제공되지 않습니다. 1.3에서 다시 추가됩니다.  

 기본 Azure 로그에 대 한 hello 버퍼 구성을 정의합니다.  

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|**unsignedInt**|선택 사항입니다. Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.<br /><br /> hello 기본값은 0입니다.|  
|**scheduledTransferLogLevelFilterr**|**string**|선택 사항입니다. 전송 되는 로그 항목에 대 한 hello 최소 심각도 수준을 지정 합니다. hello 기본값은 **Undefined**, 모든 로그 전송입니다. (대부분 tooleast 정보의 순서) 대로 다른 가능한 값은 **Verbose**, **정보**, **경고**, **오류**, 및 **중요**합니다.|  
|**scheduledTransferPeriod**|**duration**|선택 사항입니다. Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.<br /><br /> hello 기본값은 pt0s입니다.|  
|**싱크** 1.5에서 추가됨|**string**|선택 사항입니다. 포인트 tooa 싱크 위치 tooalso 진단 데이터 보내기. 예를 들어 Application Insights입니다.|  

## <a name="dockersources"></a>DockerSources
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*

 1.9에 추가되었습니다.

|요소 이름|설명|  
|------------------|-----------------|  
|**Stats**|Docker 컨테이너에 대 한 통계 toocollect hello 체제 지정|  

## <a name="sinksconfig-element"></a>SinksConfig 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*

 해당 위치와 연결 된 위치 toosend 진단 데이터 tooand hello 구성의 목록.  

|요소 이름|설명|  
|------------------|-----------------|  
|**싱크**|이 페이지의 다른 곳에 있는 설명을 참조하세요.|  

## <a name="sink-element"></a>싱크 요소
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*

 버전 1.5에 추가되었습니다.  

 위치 toosend 진단 데이터를 정의합니다. 예를 들어 hello Application Insights 서비스입니다.  

|특성|형식|설명|  
|---------------|----------|-----------------|  
|**name**|string|문자열 식별 hello sinkname 합니다.|  

|요소|유형|설명|  
|-------------|----------|-----------------|  
|**Application Insights**|string|데이터 tooApplication 통찰력을 보낼 때만 사용 합니다. Hello에 대 한 액세스 권한이 현재 Application Insights 계정에 대 한 계측 키를 포함 합니다.|  
|**Channels**|string|스트림하는 각 추가 필터링에 대한|  

## <a name="channels-element"></a>Channels 요소  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*

 버전 1.5에 추가되었습니다.  

 싱크를 통해 전달되는 로그 데이터의 스트림에 대한 필터를 정의합니다.  

|요소|유형|설명|  
|-------------|----------|-----------------|  
|**채널**|string|이 페이지의 다른 곳에 있는 설명을 참조하세요.|  

## <a name="channel-element"></a>채널 요소
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*

 버전 1.5에 추가되었습니다.  

 위치 toosend 진단 데이터를 정의합니다. 예를 들어 hello Application Insights 서비스입니다.  

|특성|유형|설명|  
|----------------|----------|-----------------|  
|**logLevel**|**string**|전송 되는 로그 항목에 대 한 hello 최소 심각도 수준을 지정 합니다. hello 기본값은 **Undefined**, 모든 로그 전송입니다. (대부분 tooleast 정보의 순서) 대로 다른 가능한 값은 **Verbose**, **정보**, **경고**, **오류**, 및 **중요**합니다.|  
|**name**|**string**|hello 채널 toorefer의 고유 이름|  


## <a name="privateconfig-element"></a>PrivateConfig 요소 
 *Tree: Root - DiagnosticsConfiguration - PrivateConfig*

 버전 1.3에 추가되었습니다.  

 옵션  

 Hello hello 저장소 계정 (이름, 키 및 끝점)의 개인 정보를 저장합니다. 이 정보는 toohello 가상 컴퓨터를 전송 되지만에서 검색할 수 없습니다.  

|자식 요소|설명|  
|--------------------|-----------------|  
|**StorageAccount**|저장소 계정 toouse hello 합니다. 다음 특성 hello는 필요<br /><br /> - **이름** -hello hello 저장소 계정의 이름입니다.<br /><br /> - **키** -hello toohello 저장소 계정 키입니다.<br /><br /> - **끝점** -hello 끝점 tooaccess hello 저장소 계정입니다. <br /><br /> -**sasToken** (추가 1.8.1)-hello 개인 구성에서 저장소 계정 키를 대신 하는 SAS 토큰을 지정할 수 있습니다. 제공 된 hello 저장소 계정 키가 무시 됩니다. <br />Hello SAS 토큰에 대 한 요구 사항: <br />- 계정 SAS 토큰만 지원합니다. <br />- *b*, *t* 서비스 형식이 필요합니다. <br /> - *a*, *c*, *u*, *w* 권한이 필요합니다. <br /> - *c*, *o* 리소스 형식이 필요합니다. <br /> -Hello HTTPS 프로토콜만을 지원합니다. <br /> - 시작 및 만료 시간이 유효해야 합니다.|  


## <a name="isenabled-element"></a>IsEnabled 요소  
 *Tree: Root - DiagnosticsConfiguration - IsEnabled*

 부울 값입니다. 사용 하 여 `true` tooenable hello 진단 또는 `false` toodisable hello 진단 합니다.
