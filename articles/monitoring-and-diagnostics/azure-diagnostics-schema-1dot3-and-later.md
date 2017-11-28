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
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="366ef-103">Azure 진단 1.3 이상 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="366ef-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="366ef-104">hello Azure 진단 확장은 toocollect 성능 카운터 및 기타 통계에서 사용 하는 hello 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-104">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="366ef-105">Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="366ef-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="366ef-106">가상 컴퓨터 크기 집합</span><span class="sxs-lookup"><span data-stu-id="366ef-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="366ef-107">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="366ef-107">Service Fabric</span></span> 
> - <span data-ttu-id="366ef-108">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="366ef-108">Cloud Services</span></span> 
> - <span data-ttu-id="366ef-109">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="366ef-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="366ef-110">이 페이지는 이러한 서비스 중 하나를 사용하는 경우에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="366ef-111">이 페이지는 버전 1.3 이상(Azure SDK 2.4 이상)에 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="366ef-112">최신 구성 섹션은 추가 된 버전의 주석 처리 된 tooshow 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-112">Newer configuration sections are commented tooshow in what version they were added.</span></span>  

<span data-ttu-id="366ef-113">hello 구성 파일이 여기에 설명 된 경우 진단 구성 설정을 사용 하는 tooset hello 진단 모니터를 시작 하는 경우</span><span class="sxs-lookup"><span data-stu-id="366ef-113">hello configuration file described here is used tooset diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

<span data-ttu-id="366ef-114">hello 확장이 Azure 모니터, Application Insights 및 분석 로그와 같은 다른 Microsoft 진단 제품과 함께에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-114">hello extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="366ef-115">Hello 다음 PowerShell 명령을 실행 하 여 hello 공용 구성 파일 스키마 정의 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-115">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="366ef-116">Azure 진단 사용에 대한 자세한 내용은 [Azure 진단 확장](azure-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="366ef-117">Hello 진단 구성 파일의 예</span><span class="sxs-lookup"><span data-stu-id="366ef-117">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="366ef-118">다음 예제는 hello 일반적인 진단 구성 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-118">hello following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="366ef-119">Hello 이전 XML 구성 파일의 JSON와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-119">JSON equivalent of hello previous XML configuration file.</span></span> 

<span data-ttu-id="366ef-120">다른 변수로 전달 되므로 대부분의 json 사용 경우에서 PublicConfig hello 및 PrivateConfig 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-120">hello PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="366ef-121">이러한 경우에는 Resource Manager 템플릿, 가상 컴퓨터 확장 집합 PowerShell 및 Visual Studio가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="366ef-122">이 페이지 읽기</span><span class="sxs-lookup"><span data-stu-id="366ef-122">Reading this page</span></span>  
 <span data-ttu-id="366ef-123">hello 다음 태그는 대략 hello 예제 앞에 표시 된 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-123">hello tags following are roughly in order shown in hello preceding example.</span></span>  <span data-ttu-id="366ef-124">필요한 위치에 대 한 전체 설명은 표시 되지 않으면, hello 요소 또는 특성에 대 한 hello 페이지를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-124">If you don't see a full description where you expect it, search hello page for hello element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="366ef-125">일반 특성 유형</span><span class="sxs-lookup"><span data-stu-id="366ef-125">Common Attribute Types</span></span>  
 <span data-ttu-id="366ef-126">**scheduledTransferPeriod** 특성이 몇 가지 요소에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="366ef-127">것 hello 간격 예약 된 전송 toostorage toohello 가장 근접 한 분을 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-127">It is hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="366ef-128">hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="366ef-128">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="366ef-129">DiagnosticsConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="366ef-130">*Tree: Root - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="366ef-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="366ef-131">버전 1.3에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-131">Added in version 1.3.</span></span>  

<span data-ttu-id="366ef-132">hello hello 진단 구성 파일의 최상위 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-132">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="366ef-133">**특성** xmlns-hello 진단 구성 파일에 대 한 XML 네임 스페이스 hello:</span><span class="sxs-lookup"><span data-stu-id="366ef-133">**Attribute**  xmlns - hello XML namespace for hello diagnostics configuration file is:</span></span>  
<span data-ttu-id="366ef-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="366ef-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="366ef-135">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-135">Child Elements</span></span>|<span data-ttu-id="366ef-136">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="366ef-137">**PublicConfig**</span></span>|<span data-ttu-id="366ef-138">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-138">Required.</span></span> <span data-ttu-id="366ef-139">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="366ef-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="366ef-140">**PrivateConfig**</span></span>|<span data-ttu-id="366ef-141">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-141">Optional.</span></span> <span data-ttu-id="366ef-142">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="366ef-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="366ef-143">**IsEnabled**</span></span>|<span data-ttu-id="366ef-144">부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-144">Boolean.</span></span> <span data-ttu-id="366ef-145">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="366ef-146">PublicConfig 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-146">PublicConfig Element</span></span>  
 <span data-ttu-id="366ef-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="366ef-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="366ef-148">Hello 공용 진단 구성에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-148">Describes hello public diagnostics configuration.</span></span>  

|<span data-ttu-id="366ef-149">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-149">Child Elements</span></span>|<span data-ttu-id="366ef-150">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="366ef-151">**WadCfg**</span></span>|<span data-ttu-id="366ef-152">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-152">Required.</span></span> <span data-ttu-id="366ef-153">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="366ef-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="366ef-154">**StorageAccount**</span></span>|<span data-ttu-id="366ef-155">hello Azure 저장소 계정 toostore hello 데이터에서의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-155">hello name of hello Azure Storage account toostore hello data in.</span></span> <span data-ttu-id="366ef-156">지정할 수도 있습니다를 매개 변수로 hello 집합 AzureServiceDiagnosticsExtension cmdlet을 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="366ef-156">May also be specified as a parameter when executing hello Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="366ef-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="366ef-157">**StorageType**</span></span>|<span data-ttu-id="366ef-158">*Table*, *Blob* 또는 *TableAndBlob*일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="366ef-159">Table이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-159">Table is default.</span></span> <span data-ttu-id="366ef-160">TableAndBlob 선택 될 때 진단 데이터는 두 번 한 번씩 기록 tooeach 유형.</span><span class="sxs-lookup"><span data-stu-id="366ef-160">When TableAndBlob is chosen, diagnostic data is written twice -- once tooeach type.</span></span>|  
|<span data-ttu-id="366ef-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="366ef-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="366ef-162">여기서 hello Monitoring Agent 이벤트 데이터를 저장 하는 hello 가상 컴퓨터에 hello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-162">hello directory on hello virtual machine where hello Monitoring Agent stores event data.</span></span> <span data-ttu-id="366ef-163">그렇지 않은 경우 설정, hello 기본 디렉터리가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-163">If not, set, hello default directory is used:</span></span><br /><br /> <span data-ttu-id="366ef-164">작업자/웹 역할의 경우: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="366ef-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="366ef-165">가상 컴퓨터의 경우: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="366ef-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="366ef-166">필수 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="366ef-167">- **경로** -hello 디렉터리에서 Azure 진단을 사용 하는 hello 시스템 toobe에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-167">- **path** - hello directory on hello system toobe used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="366ef-168">- **expandEnvironment** -환경 변수 hello 경로 이름으로 확장 되는 여부를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-168">- **expandEnvironment** - Controls whether environment variables are expanded in hello path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="366ef-169">WadCFG 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-169">WadCFG Element</span></span>  
 <span data-ttu-id="366ef-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span><span class="sxs-lookup"><span data-stu-id="366ef-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="366ef-171">식별 하 고 hello 원격 분석 데이터 toobe 수집을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-171">Identifies and configures hello telemetry data toobe collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="366ef-172">DiagnosticMonitorConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="366ef-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="366ef-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="366ef-174">필수</span><span class="sxs-lookup"><span data-stu-id="366ef-174">Required</span></span> 

|<span data-ttu-id="366ef-175">특성</span><span class="sxs-lookup"><span data-stu-id="366ef-175">Attributes</span></span>|<span data-ttu-id="366ef-176">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="366ef-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="366ef-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="366ef-178">hello에서 사용 될 수 있는 로컬 디스크 공간의 최대 크기 hello 다양 한 유형의 진단 데이터는 Azure 진단에서 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-178">hello maximum amount of local disk space that may be consumed by hello various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="366ef-179">hello 기본 설정은 5120MB입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-179">hello default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="366ef-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="366ef-180">**useProxyServer**</span></span> | <span data-ttu-id="366ef-181">IE 설정에 설정 된 대로 Azure 진단 toouse hello 프록시 서버 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-181">Configure Azure Diagnostics toouse hello proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="366ef-182">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-182">Child Elements</span></span>|<span data-ttu-id="366ef-183">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="366ef-184">**CrashDumps**</span></span>|<span data-ttu-id="366ef-185">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="366ef-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="366ef-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="366ef-187">Azure 진단에 의해 생성된 로그의 컬렉션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="366ef-188">hello 진단 인프라 로그는 hello 진단 시스템 자체의 문제를 해결 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-188">hello diagnostic infrastructure logs are useful for troubleshooting hello diagnostics system itself.</span></span> <span data-ttu-id="366ef-189">선택적 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="366ef-190">- **scheduledTransferLogLevelFilter** -hello 로그가 수집의 hello 최소 심각도 수준을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-190">- **scheduledTransferLogLevelFilter** - Configures hello minimum severity level of hello logs collected.</span></span><br /><br /> <span data-ttu-id="366ef-191">- **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-191">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="366ef-192">hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="366ef-192">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="366ef-193">**Directories**</span><span class="sxs-lookup"><span data-stu-id="366ef-193">**Directories**</span></span>|<span data-ttu-id="366ef-194">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="366ef-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="366ef-195">**EtwProviders**</span></span>|<span data-ttu-id="366ef-196">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="366ef-197">**metrics**</span><span class="sxs-lookup"><span data-stu-id="366ef-197">**Metrics**</span></span>|<span data-ttu-id="366ef-198">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="366ef-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="366ef-199">**PerformanceCounters**</span></span>|<span data-ttu-id="366ef-200">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="366ef-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="366ef-201">**WindowsEventLog**</span></span>|<span data-ttu-id="366ef-202">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="366ef-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="366ef-203">**DockerSources**</span></span>|<span data-ttu-id="366ef-204">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="366ef-205">CrashDumps 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-205">CrashDumps Element</span></span>  
 <span data-ttu-id="366ef-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="366ef-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="366ef-207">크래시 덤프의 수집 hello를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-207">Enable hello collection of crash dumps.</span></span>  

|<span data-ttu-id="366ef-208">특성</span><span class="sxs-lookup"><span data-stu-id="366ef-208">Attributes</span></span>|<span data-ttu-id="366ef-209">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="366ef-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="366ef-210">**containerName**</span></span>|<span data-ttu-id="366ef-211">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-211">Optional.</span></span> <span data-ttu-id="366ef-212">Azure 저장소 계정 toobe의 hello blob 컨테이너의 hello 이름이 toostore 크래시 덤프를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-212">hello name of hello blob container in your Azure Storage account toobe used toostore crash dumps.</span></span>|  
|<span data-ttu-id="366ef-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="366ef-213">**crashDumpType**</span></span>|<span data-ttu-id="366ef-214">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-214">Optional.</span></span>  <span data-ttu-id="366ef-215">Azure 진단 toocollect 미니 또는 전체 크래시 덤프를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-215">Configures Azure Diagnostics toocollect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="366ef-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="366ef-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="366ef-217">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-217">Optional.</span></span>  <span data-ttu-id="366ef-218">hello 비율을 구성 **overallQuotaInMB** toobe hello VM에 크래시 덤프에 사용 되도록 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-218">Configures hello percentage of **overallQuotaInMB** toobe reserved for crash dumps on hello VM.</span></span>|  

|<span data-ttu-id="366ef-219">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-219">Child Elements</span></span>|<span data-ttu-id="366ef-220">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="366ef-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="366ef-222">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-222">Required.</span></span> <span data-ttu-id="366ef-223">각 프로세스에 대한 구성 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="366ef-224">hello 다음 특성은도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-224">hello following attribute is also required:</span></span><br /><br /> <span data-ttu-id="366ef-225">**processName** -hello toocollect Azure 진단에 대 한 크래시 덤프를 원하는 hello 프로세스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-225">**processName** - hello name of hello process you want Azure Diagnostics toocollect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="366ef-226">Directories 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-226">Directories Element</span></span> 
 <span data-ttu-id="366ef-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span><span class="sxs-lookup"><span data-stu-id="366ef-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="366ef-228">사용 하도록 설정 hello 디렉터리의 hello 콘텐츠의 컬렉션, IIS 실패 한 액세스 요청 로그 및/또는 IIS 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-228">Enables hello collection of hello contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="366ef-229">선택적 **scheduledTransferPeriod** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="366ef-230">이전 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-230">See explanation earlier.</span></span>  

|<span data-ttu-id="366ef-231">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-231">Child Elements</span></span>|<span data-ttu-id="366ef-232">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="366ef-233">**IISLogs**</span></span>|<span data-ttu-id="366ef-234">이 요소를 포함 하 여 hello 구성에서 IIS 로그 컬렉션을 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-234">Including this element in hello configuration enables hello collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="366ef-235">**containerName** -Azure 저장소 계정 toobe의 hello blob 컨테이너의 hello 이름이 toostore hello IIS 로그를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-235">**containerName** - hello name of hello blob container in your Azure Storage account toobe used toostore hello IIS logs.</span></span>|   
|<span data-ttu-id="366ef-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="366ef-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="366ef-237">이 요소를 포함 하 여 hello 구성에 실패 한 요청 tooan IIS 사이트 또는 응용 프로그램에 대 한 로그 컬렉션을에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-237">Including this element in hello configuration enables collection of logs about failed requests tooan IIS site or application.</span></span> <span data-ttu-id="366ef-238">또한 **Web.config**의 **system.WebServer**에 있는 추적 옵션도 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="366ef-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="366ef-239">**DataSources**</span></span>|<span data-ttu-id="366ef-240">목록 디렉터리 toomonitor입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-240">A list of directories toomonitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="366ef-241">DataSources 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-241">DataSources Element</span></span>  
 <span data-ttu-id="366ef-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span><span class="sxs-lookup"><span data-stu-id="366ef-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="366ef-243">목록 디렉터리 toomonitor입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-243">A list of directories toomonitor.</span></span>  

|<span data-ttu-id="366ef-244">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-244">Child Elements</span></span>|<span data-ttu-id="366ef-245">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="366ef-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="366ef-247">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-247">Required.</span></span> <span data-ttu-id="366ef-248">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="366ef-249">**containerName** -hello 해당 toobe toostore hello 로그 파일을 사용 하 여 Azure 저장소 계정에 hello blob 컨테이너의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-249">**containerName** - hello name of hello blob container in your Azure Storage account that toobe used toostore hello log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="366ef-250">DirectoryConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="366ef-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="366ef-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="366ef-252">어느 hello 포함 될 수 있습니다 **절대** 또는 **LocalResource** 요소 중 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-252">May include either hello **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="366ef-253">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-253">Child Elements</span></span>|<span data-ttu-id="366ef-254">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="366ef-255">**Absolute**</span></span>|<span data-ttu-id="366ef-256">hello toohello 디렉터리 toomonitor 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-256">hello absolute path toohello directory toomonitor.</span></span> <span data-ttu-id="366ef-257">hello 특성 다음 사항이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-257">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="366ef-258">- **경로** -hello toohello 디렉터리 toomonitor 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-258">- **Path** - hello absolute path toohello directory toomonitor.</span></span><br /><br /> <span data-ttu-id="366ef-259">- **expandEnvironment** - 경로의 환경 변수가 확장되어 있는지 여부를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="366ef-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="366ef-260">**LocalResource**</span></span>|<span data-ttu-id="366ef-261">hello 경로 상대 tooa 로컬 리소스 toomonitor 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-261">hello path relative tooa local resource toomonitor.</span></span> <span data-ttu-id="366ef-262">필수 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="366ef-263">- **이름** -hello hello 디렉터리 toomonitor 포함 된 로컬 리소스</span><span class="sxs-lookup"><span data-stu-id="366ef-263">- **Name** - hello local resource that contains hello directory toomonitor</span></span><br /><br /> <span data-ttu-id="366ef-264">- **relativePath** -hello 디렉터리 toomonitor 포함 된 상대 경로 tooName hello</span><span class="sxs-lookup"><span data-stu-id="366ef-264">- **relativePath** - hello path relative tooName that contains hello directory toomonitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="366ef-265">EtwProviders 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-265">EtwProviders Element</span></span>  
 <span data-ttu-id="366ef-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="366ef-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="366ef-267">EventSource의 ETW 이벤트 및/또는 공급자를 기반으로 하는 ETW 매니페스트의 컬렉션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="366ef-268">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-268">Child Elements</span></span>|<span data-ttu-id="366ef-269">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="366ef-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="366ef-271">[EventSource 클래스](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)에서 생성된 이벤트 컬렉션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="366ef-272">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="366ef-273">**공급자** -hello EventSource 이벤트의 hello 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-273">**provider** - hello class name of hello EventSource event.</span></span><br /><br /> <span data-ttu-id="366ef-274">선택적 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="366ef-275">- **scheduledTransferLogLevelFilter** -hello 최소 심각도 수준 tootransfer tooyour 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-275">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="366ef-276">- **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-276">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="366ef-277">hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="366ef-277">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="366ef-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="366ef-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="366ef-279">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="366ef-280">**공급자** -hello hello 이벤트 공급자의 GUID</span><span class="sxs-lookup"><span data-stu-id="366ef-280">**provider** - hello GUID of hello event provider</span></span><br /><br /> <span data-ttu-id="366ef-281">선택적 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="366ef-282">- **scheduledTransferLogLevelFilter** -hello 최소 심각도 수준 tootransfer tooyour 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-282">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="366ef-283">- **scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-283">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="366ef-284">hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="366ef-284">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="366ef-285">EtwEventSourceProviderConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="366ef-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="366ef-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="366ef-287">[EventSource 클래스](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)에서 생성된 이벤트 컬렉션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="366ef-288">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-288">Child Elements</span></span>|<span data-ttu-id="366ef-289">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="366ef-290">**DefaultEvents**</span></span>|<span data-ttu-id="366ef-291">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="366ef-292">**eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름</span><span class="sxs-lookup"><span data-stu-id="366ef-292">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="366ef-293">**Event**</span><span class="sxs-lookup"><span data-stu-id="366ef-293">**Event**</span></span>|<span data-ttu-id="366ef-294">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="366ef-295">**id** -hello 이벤트의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-295">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="366ef-296">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="366ef-297">**eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름</span><span class="sxs-lookup"><span data-stu-id="366ef-297">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="366ef-298">EtwManifestProviderConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="366ef-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="366ef-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="366ef-300">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-300">Child Elements</span></span>|<span data-ttu-id="366ef-301">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="366ef-302">**DefaultEvents**</span></span>|<span data-ttu-id="366ef-303">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="366ef-304">**eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름</span><span class="sxs-lookup"><span data-stu-id="366ef-304">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="366ef-305">**Event**</span><span class="sxs-lookup"><span data-stu-id="366ef-305">**Event**</span></span>|<span data-ttu-id="366ef-306">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="366ef-307">**id** -hello 이벤트의 hello id입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-307">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="366ef-308">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="366ef-309">**eventDestination** -hello에 hello 테이블 toostore hello 이벤트의 이름</span><span class="sxs-lookup"><span data-stu-id="366ef-309">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="366ef-310">Metrics 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-310">Metrics Element</span></span>  
 <span data-ttu-id="366ef-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span><span class="sxs-lookup"><span data-stu-id="366ef-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="366ef-312">빠른 쿼리를 위해 최적화 된 성능 카운터 테이블 toogenerate가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-312">Enables you toogenerate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="366ef-313">Hello에 정의 된 각 성능 카운터 **PerformanceCounters** 요소 또한 toohello 성능 카운터 표에 hello 메트릭 테이블에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-313">Each performance counter that is defined in hello **PerformanceCounters** element is stored in hello Metrics table in addition toohello Performance Counter table.</span></span>  

 <span data-ttu-id="366ef-314">hello **resourceId** 특성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-314">hello **resourceId** attribute is required.</span></span>  <span data-ttu-id="366ef-315">hello hello 하도록 Azure 진단을 배포 하는 가상 컴퓨터의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-315">hello resource ID of hello Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="366ef-316">Hello 가져오기 **resourceID** hello에서 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-316">Get hello **resourceID** from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="366ef-317">**찾아보기** -> **리소스 그룹** -> **<이름\>**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="366ef-318">Hello 클릭 **속성** 타일 및 hello에서 hello 값 복사 **ID** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-318">Click hello **Properties** tile and copy hello value from hello **ID** field.</span></span>  

|<span data-ttu-id="366ef-319">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-319">Child Elements</span></span>|<span data-ttu-id="366ef-320">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="366ef-321">**MetricAggregation**</span></span>|<span data-ttu-id="366ef-322">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="366ef-323">**scheduledTransferPeriod** -예약 된 전송 toostorage hello 간격 toohello 가장 근접 한 분을 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-323">**scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="366ef-324">hello 값은 한 [XML "기간 동안 데이터 형식입니다."](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="366ef-324">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="366ef-325">PerformanceCounters 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="366ef-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="366ef-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="366ef-327">성능 카운터의 hello 컬렉션을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-327">Enables hello collection of performance counters.</span></span>  

 <span data-ttu-id="366ef-328">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-328">Optional attribute:</span></span>  

 <span data-ttu-id="366ef-329">선택적 **scheduledTransferPeriod** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="366ef-330">이전 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-330">See explanation earlier.</span></span>

|<span data-ttu-id="366ef-331">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-331">Child Element</span></span>|<span data-ttu-id="366ef-332">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="366ef-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="366ef-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="366ef-334">hello 특성 다음 사항이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-334">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="366ef-335">- **counterSpecifier** -hello hello 성능 카운터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-335">- **counterSpecifier** - hello name of hello performance counter.</span></span> <span data-ttu-id="366ef-336">예: `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="366ef-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="366ef-337">tooget hello 명령을 실행 호스트에 목록이 성능 카운터 `typeperf`합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-337">tooget a list of performance counters on your host, run hello command `typeperf`.</span></span><br /><br /> <span data-ttu-id="366ef-338">- **sampleRate** -얼마나 자주 hello 카운터를 샘플링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-338">- **sampleRate** - How often hello counter should be sampled.</span></span><br /><br /> <span data-ttu-id="366ef-339">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="366ef-340">**단위** -hello hello 카운터의 측정 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-340">**unit** - hello unit of measure of hello counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="366ef-341">WindowsEventLog 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="366ef-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="366ef-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="366ef-343">Windows 이벤트 로그의 hello 컬렉션을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-343">Enables hello collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="366ef-344">선택적 **scheduledTransferPeriod** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="366ef-345">이전 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="366ef-346">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-346">Child Element</span></span>|<span data-ttu-id="366ef-347">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="366ef-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="366ef-348">**DataSource**</span></span>|<span data-ttu-id="366ef-349">Windows 이벤트 로그 toocollect hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-349">hello Windows Event logs toocollect.</span></span> <span data-ttu-id="366ef-350">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="366ef-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="366ef-351">**이름** -hello windows 이벤트 toobe를 설명 하는 hello XPath 쿼리를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-351">**name** - hello XPath query describing hello windows events toobe collected.</span></span> <span data-ttu-id="366ef-352">예:</span><span class="sxs-lookup"><span data-stu-id="366ef-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="366ef-353">모든 이벤트를 지정 하는 toocollect "*"</span><span class="sxs-lookup"><span data-stu-id="366ef-353">toocollect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="366ef-354">Logs 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-354">Logs Element</span></span>  
 <span data-ttu-id="366ef-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span><span class="sxs-lookup"><span data-stu-id="366ef-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="366ef-356">버전 1.0 및 1.1에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="366ef-357">1.2에는 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-357">Missing in 1.2.</span></span> <span data-ttu-id="366ef-358">1.3에서 다시 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="366ef-359">기본 Azure 로그에 대 한 hello 버퍼 구성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-359">Defines hello buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="366ef-360">특성</span><span class="sxs-lookup"><span data-stu-id="366ef-360">Attribute</span></span>|<span data-ttu-id="366ef-361">형식</span><span class="sxs-lookup"><span data-stu-id="366ef-361">Type</span></span>|<span data-ttu-id="366ef-362">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="366ef-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="366ef-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="366ef-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="366ef-364">**unsignedInt**</span></span>|<span data-ttu-id="366ef-365">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-365">Optional.</span></span> <span data-ttu-id="366ef-366">Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-366">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="366ef-367">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-367">hello default is 0.</span></span>|  
|<span data-ttu-id="366ef-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="366ef-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="366ef-369">**string**</span><span class="sxs-lookup"><span data-stu-id="366ef-369">**string**</span></span>|<span data-ttu-id="366ef-370">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-370">Optional.</span></span> <span data-ttu-id="366ef-371">전송 되는 로그 항목에 대 한 hello 최소 심각도 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-371">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="366ef-372">hello 기본값은 **Undefined**, 모든 로그 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-372">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="366ef-373">(대부분 tooleast 정보의 순서) 대로 다른 가능한 값은 **Verbose**, **정보**, **경고**, **오류**, 및 **중요**합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-373">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="366ef-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="366ef-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="366ef-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="366ef-375">**duration**</span></span>|<span data-ttu-id="366ef-376">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-376">Optional.</span></span> <span data-ttu-id="366ef-377">Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-377">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="366ef-378">hello 기본값은 pt0s입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-378">hello default is PT0S.</span></span>|  
|<span data-ttu-id="366ef-379">**싱크** 1.5에서 추가됨</span><span class="sxs-lookup"><span data-stu-id="366ef-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="366ef-380">**string**</span><span class="sxs-lookup"><span data-stu-id="366ef-380">**string**</span></span>|<span data-ttu-id="366ef-381">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-381">Optional.</span></span> <span data-ttu-id="366ef-382">포인트 tooa 싱크 위치 tooalso 진단 데이터 보내기.</span><span class="sxs-lookup"><span data-stu-id="366ef-382">Points tooa sink location tooalso send diagnostic data.</span></span> <span data-ttu-id="366ef-383">예를 들어 Application Insights입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="366ef-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="366ef-384">DockerSources</span></span>
 <span data-ttu-id="366ef-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span><span class="sxs-lookup"><span data-stu-id="366ef-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="366ef-386">1.9에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-386">Added in 1.9.</span></span>

|<span data-ttu-id="366ef-387">요소 이름</span><span class="sxs-lookup"><span data-stu-id="366ef-387">Element Name</span></span>|<span data-ttu-id="366ef-388">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="366ef-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="366ef-389">**Stats**</span></span>|<span data-ttu-id="366ef-390">Docker 컨테이너에 대 한 통계 toocollect hello 체제 지정</span><span class="sxs-lookup"><span data-stu-id="366ef-390">Tells hello system toocollect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="366ef-391">SinksConfig 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-391">SinksConfig Element</span></span>  
 <span data-ttu-id="366ef-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="366ef-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="366ef-393">해당 위치와 연결 된 위치 toosend 진단 데이터 tooand hello 구성의 목록.</span><span class="sxs-lookup"><span data-stu-id="366ef-393">A list of locations toosend diagnostics data tooand hello configuration associated with those locations.</span></span>  

|<span data-ttu-id="366ef-394">요소 이름</span><span class="sxs-lookup"><span data-stu-id="366ef-394">Element Name</span></span>|<span data-ttu-id="366ef-395">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="366ef-396">**싱크**</span><span class="sxs-lookup"><span data-stu-id="366ef-396">**Sink**</span></span>|<span data-ttu-id="366ef-397">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="366ef-398">싱크 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-398">Sink Element</span></span>
 <span data-ttu-id="366ef-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span><span class="sxs-lookup"><span data-stu-id="366ef-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="366ef-400">버전 1.5에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="366ef-401">위치 toosend 진단 데이터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-401">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="366ef-402">예를 들어 hello Application Insights 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-402">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="366ef-403">특성</span><span class="sxs-lookup"><span data-stu-id="366ef-403">Attribute</span></span>|<span data-ttu-id="366ef-404">형식</span><span class="sxs-lookup"><span data-stu-id="366ef-404">Type</span></span>|<span data-ttu-id="366ef-405">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="366ef-406">**name**</span><span class="sxs-lookup"><span data-stu-id="366ef-406">**name**</span></span>|<span data-ttu-id="366ef-407">string</span><span class="sxs-lookup"><span data-stu-id="366ef-407">string</span></span>|<span data-ttu-id="366ef-408">문자열 식별 hello sinkname 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-408">A string identifying hello sinkname.</span></span>|  

|<span data-ttu-id="366ef-409">요소</span><span class="sxs-lookup"><span data-stu-id="366ef-409">Element</span></span>|<span data-ttu-id="366ef-410">유형</span><span class="sxs-lookup"><span data-stu-id="366ef-410">Type</span></span>|<span data-ttu-id="366ef-411">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="366ef-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="366ef-412">**Application Insights**</span></span>|<span data-ttu-id="366ef-413">string</span><span class="sxs-lookup"><span data-stu-id="366ef-413">string</span></span>|<span data-ttu-id="366ef-414">데이터 tooApplication 통찰력을 보낼 때만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-414">Used only when sending data tooApplication Insights.</span></span> <span data-ttu-id="366ef-415">Hello에 대 한 액세스 권한이 현재 Application Insights 계정에 대 한 계측 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-415">Contain hello Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="366ef-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="366ef-416">**Channels**</span></span>|<span data-ttu-id="366ef-417">string</span><span class="sxs-lookup"><span data-stu-id="366ef-417">string</span></span>|<span data-ttu-id="366ef-418">스트림하는 각 추가 필터링에 대한</span><span class="sxs-lookup"><span data-stu-id="366ef-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="366ef-419">Channels 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-419">Channels Element</span></span>  
 <span data-ttu-id="366ef-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span><span class="sxs-lookup"><span data-stu-id="366ef-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="366ef-421">버전 1.5에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="366ef-422">싱크를 통해 전달되는 로그 데이터의 스트림에 대한 필터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="366ef-423">요소</span><span class="sxs-lookup"><span data-stu-id="366ef-423">Element</span></span>|<span data-ttu-id="366ef-424">유형</span><span class="sxs-lookup"><span data-stu-id="366ef-424">Type</span></span>|<span data-ttu-id="366ef-425">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="366ef-426">**채널**</span><span class="sxs-lookup"><span data-stu-id="366ef-426">**Channel**</span></span>|<span data-ttu-id="366ef-427">string</span><span class="sxs-lookup"><span data-stu-id="366ef-427">string</span></span>|<span data-ttu-id="366ef-428">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="366ef-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="366ef-429">채널 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-429">Channel Element</span></span>
 <span data-ttu-id="366ef-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span><span class="sxs-lookup"><span data-stu-id="366ef-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="366ef-431">버전 1.5에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="366ef-432">위치 toosend 진단 데이터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-432">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="366ef-433">예를 들어 hello Application Insights 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-433">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="366ef-434">특성</span><span class="sxs-lookup"><span data-stu-id="366ef-434">Attributes</span></span>|<span data-ttu-id="366ef-435">유형</span><span class="sxs-lookup"><span data-stu-id="366ef-435">Type</span></span>|<span data-ttu-id="366ef-436">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="366ef-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="366ef-437">**logLevel**</span></span>|<span data-ttu-id="366ef-438">**string**</span><span class="sxs-lookup"><span data-stu-id="366ef-438">**string**</span></span>|<span data-ttu-id="366ef-439">전송 되는 로그 항목에 대 한 hello 최소 심각도 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-439">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="366ef-440">hello 기본값은 **Undefined**, 모든 로그 전송입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-440">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="366ef-441">(대부분 tooleast 정보의 순서) 대로 다른 가능한 값은 **Verbose**, **정보**, **경고**, **오류**, 및 **중요**합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-441">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="366ef-442">**name**</span><span class="sxs-lookup"><span data-stu-id="366ef-442">**name**</span></span>|<span data-ttu-id="366ef-443">**string**</span><span class="sxs-lookup"><span data-stu-id="366ef-443">**string**</span></span>|<span data-ttu-id="366ef-444">hello 채널 toorefer의 고유 이름</span><span class="sxs-lookup"><span data-stu-id="366ef-444">A unique name of hello channel toorefer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="366ef-445">PrivateConfig 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="366ef-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="366ef-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="366ef-447">버전 1.3에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="366ef-448">옵션</span><span class="sxs-lookup"><span data-stu-id="366ef-448">Optional</span></span>  

 <span data-ttu-id="366ef-449">Hello hello 저장소 계정 (이름, 키 및 끝점)의 개인 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-449">Stores hello private details of hello storage account (name, key, and endpoint).</span></span> <span data-ttu-id="366ef-450">이 정보는 toohello 가상 컴퓨터를 전송 되지만에서 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-450">This information is sent toohello virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="366ef-451">자식 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-451">Child Elements</span></span>|<span data-ttu-id="366ef-452">설명</span><span class="sxs-lookup"><span data-stu-id="366ef-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="366ef-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="366ef-453">**StorageAccount**</span></span>|<span data-ttu-id="366ef-454">저장소 계정 toouse hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-454">hello storage account toouse.</span></span> <span data-ttu-id="366ef-455">다음 특성 hello는 필요</span><span class="sxs-lookup"><span data-stu-id="366ef-455">hello following attributes are required</span></span><br /><br /> <span data-ttu-id="366ef-456">- **이름** -hello hello 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-456">- **name** - hello name of hello storage account.</span></span><br /><br /> <span data-ttu-id="366ef-457">- **키** -hello toohello 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-457">- **key** - hello key toohello storage account.</span></span><br /><br /> <span data-ttu-id="366ef-458">- **끝점** -hello 끝점 tooaccess hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-458">- **endpoint** - hello endpoint tooaccess hello storage account.</span></span> <br /><br /> <span data-ttu-id="366ef-459">-**sasToken** (추가 1.8.1)-hello 개인 구성에서 저장소 계정 키를 대신 하는 SAS 토큰을 지정할 수 있습니다. 제공 된 hello 저장소 계정 키가 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in hello private config. If provided, hello storage account key is ignored.</span></span> <br /><span data-ttu-id="366ef-460">Hello SAS 토큰에 대 한 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="366ef-460">Requirements for hello SAS Token:</span></span> <br /><span data-ttu-id="366ef-461">- 계정 SAS 토큰만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-461">- Supports account SAS token only</span></span> <br /><span data-ttu-id="366ef-462">- *b*, *t* 서비스 형식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-462">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="366ef-463">- *a*, *c*, *u*, *w* 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-463">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="366ef-464">- *c*, *o* 리소스 형식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-464">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="366ef-465">-Hello HTTPS 프로토콜만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-465">- Supports hello HTTPS protocol only</span></span> <br /> <span data-ttu-id="366ef-466">- 시작 및 만료 시간이 유효해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-466">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="366ef-467">IsEnabled 요소</span><span class="sxs-lookup"><span data-stu-id="366ef-467">IsEnabled Element</span></span>  
 <span data-ttu-id="366ef-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="366ef-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="366ef-469">부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-469">Boolean.</span></span> <span data-ttu-id="366ef-470">사용 하 여 `true` tooenable hello 진단 또는 `false` toodisable hello 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="366ef-470">Use `true` tooenable hello diagnostics or `false` toodisable hello diagnostics.</span></span>
