---
title: "Azure 진단 확장 1.3 이상 구성 스키마 | Microsoft Docs"
description: "Azure 진단용 스키마 버전 1.3 이상은 Microsoft Azure SDK 2.4 이상의 일부로 제공됩니다."
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
ms.openlocfilehash: 0d814825fb08452238a254ccd30bde230380c74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="634ae-103">Azure 진단 1.3 이상 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="634ae-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="634ae-104">Azure 진단 확장은 성능 카운터 및 기타 통계를 수집하는 데 사용하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-104">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="634ae-105">Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="634ae-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="634ae-106">가상 컴퓨터 크기 집합</span><span class="sxs-lookup"><span data-stu-id="634ae-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="634ae-107">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="634ae-107">Service Fabric</span></span> 
> - <span data-ttu-id="634ae-108">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="634ae-108">Cloud Services</span></span> 
> - <span data-ttu-id="634ae-109">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="634ae-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="634ae-110">이 페이지는 이러한 서비스 중 하나를 사용하는 경우에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="634ae-111">이 페이지는 버전 1.3 이상(Azure SDK 2.4 이상)에 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="634ae-112">최신 구성 섹션은 추가된 버전에 표시하도록 주석 처리되었습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-112">Newer configuration sections are commented to show in what version they were added.</span></span>  

<span data-ttu-id="634ae-113">여기에서 설명하는 구성 파일은 진단 모니터가 시작될 때 진단 구성 설정을 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-113">The configuration file described here is used to set diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

<span data-ttu-id="634ae-114">확장은 Azure Monitor, Application Insights 및 Log Analytics와 같은 기타 Microsoft 진단 제품과 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-114">The extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="634ae-115">다음 PowerShell 명령을 실행하여 공용 구성 파일 스키마 정의를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-115">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="634ae-116">Azure 진단 사용에 대한 자세한 내용은 [Azure 진단 확장](azure-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="634ae-117">진단 구성 파일 예제</span><span class="sxs-lookup"><span data-stu-id="634ae-117">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="634ae-118">다음 예제에서는 일반적인 진단 구성 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-118">The following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="634ae-119">이전 XML 구성 파일에 해당하는 JSON입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-119">JSON equivalent of the previous XML configuration file.</span></span> 

<span data-ttu-id="634ae-120">PublicConfig와 PrivateConfig는 구분되는데, 대부분의 json 사용 사례에서 다른 변수로 전달되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-120">The PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="634ae-121">이러한 경우에는 Resource Manager 템플릿, 가상 컴퓨터 확장 집합 PowerShell 및 Visual Studio가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="634ae-122">이 페이지 읽기</span><span class="sxs-lookup"><span data-stu-id="634ae-122">Reading this page</span></span>  
 <span data-ttu-id="634ae-123">다음 태그는 대략 앞의 예제에 표시된 순서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-123">The tags following are roughly in order shown in the preceding example.</span></span>  <span data-ttu-id="634ae-124">필요한 위치에 전체 설명이 표시되지 않으면 요소 또는 특성에 대한 페이지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-124">If you don't see a full description where you expect it, search the page for the element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="634ae-125">일반 특성 유형</span><span class="sxs-lookup"><span data-stu-id="634ae-125">Common Attribute Types</span></span>  
 <span data-ttu-id="634ae-126">**scheduledTransferPeriod** 특성이 몇 가지 요소에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="634ae-127">저장소에 예약된 전송 사이의 간격은 가장 가까운 시간(분)으로 반올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-127">It is the interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="634ae-128">값은 [XML "기간 데이터 형식"](http://www.w3schools.com/schema/schema_dtypes_date.asp)입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-128">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="634ae-129">DiagnosticsConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="634ae-130">*Tree: Root - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="634ae-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="634ae-131">버전 1.3에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-131">Added in version 1.3.</span></span>  

<span data-ttu-id="634ae-132">진단 구성 파일의 최상위 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-132">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="634ae-133">**특성** xmlns - 진단 구성 파일에 대한 XML 네임스페이스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-133">**Attribute**  xmlns - The XML namespace for the diagnostics configuration file is:</span></span>  
<span data-ttu-id="634ae-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="634ae-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="634ae-135">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-135">Child Elements</span></span>|<span data-ttu-id="634ae-136">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="634ae-137">**PublicConfig**</span></span>|<span data-ttu-id="634ae-138">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-138">Required.</span></span> <span data-ttu-id="634ae-139">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="634ae-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="634ae-140">**PrivateConfig**</span></span>|<span data-ttu-id="634ae-141">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-141">Optional.</span></span> <span data-ttu-id="634ae-142">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="634ae-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="634ae-143">**IsEnabled**</span></span>|<span data-ttu-id="634ae-144">부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-144">Boolean.</span></span> <span data-ttu-id="634ae-145">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="634ae-146">PublicConfig 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-146">PublicConfig Element</span></span>  
 <span data-ttu-id="634ae-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="634ae-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="634ae-148">공용 진단 구성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-148">Describes the public diagnostics configuration.</span></span>  

|<span data-ttu-id="634ae-149">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-149">Child Elements</span></span>|<span data-ttu-id="634ae-150">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="634ae-151">**WadCfg**</span></span>|<span data-ttu-id="634ae-152">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-152">Required.</span></span> <span data-ttu-id="634ae-153">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="634ae-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="634ae-154">**StorageAccount**</span></span>|<span data-ttu-id="634ae-155">데이터를 저장할 Azure Storage 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-155">The name of the Azure Storage account to store the data in.</span></span> <span data-ttu-id="634ae-156">Set-AzureServiceDiagnosticsExtension cmdlet을 실행할 때 매개 변수로 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-156">May also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="634ae-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="634ae-157">**StorageType**</span></span>|<span data-ttu-id="634ae-158">*Table*, *Blob* 또는 *TableAndBlob*일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="634ae-159">Table이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-159">Table is default.</span></span> <span data-ttu-id="634ae-160">TableAndBlob을 선택하면 진단 데이터는 각 형식당 한 번씩, 두 번 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-160">When TableAndBlob is chosen, diagnostic data is written twice -- once to each type.</span></span>|  
|<span data-ttu-id="634ae-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="634ae-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="634ae-162">모니터링 에이전트가 이벤트 데이터를 저장하는 가상 컴퓨터의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-162">The directory on the virtual machine where the Monitoring Agent stores event data.</span></span> <span data-ttu-id="634ae-163">설정되어 있지 않은 경우 기본 디렉터리가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-163">If not, set, the default directory is used:</span></span><br /><br /> <span data-ttu-id="634ae-164">작업자/웹 역할의 경우: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="634ae-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="634ae-165">가상 컴퓨터의 경우: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="634ae-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="634ae-166">필수 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="634ae-167">- **경로** - Azure 진단에서 사용되는 시스템의 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-167">- **path** - The directory on the system to be used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="634ae-168">- **expandEnvironment** - 환경 변수가 경로 이름에서 확장되는지 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-168">- **expandEnvironment** - Controls whether environment variables are expanded in the path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="634ae-169">WadCFG 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-169">WadCFG Element</span></span>  
 <span data-ttu-id="634ae-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span><span class="sxs-lookup"><span data-stu-id="634ae-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="634ae-171">수집할 원격 분석 데이터를 식별 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-171">Identifies and configures the telemetry data to be collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="634ae-172">DiagnosticMonitorConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="634ae-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="634ae-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="634ae-174">필수</span><span class="sxs-lookup"><span data-stu-id="634ae-174">Required</span></span> 

|<span data-ttu-id="634ae-175">특성</span><span class="sxs-lookup"><span data-stu-id="634ae-175">Attributes</span></span>|<span data-ttu-id="634ae-176">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="634ae-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="634ae-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="634ae-178">Azure 진단으로 수집된 진단 데이터의 다양한 형식에서 사용될 수 있는 로컬 디스크 공간의 최대 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-178">The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="634ae-179">기본 설정은 5120MB입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-179">The default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="634ae-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="634ae-180">**useProxyServer**</span></span> | <span data-ttu-id="634ae-181">IE 설정에서 설정한 대로 프록시 서버 설정을 사용하도록 Azure 진단을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-181">Configure Azure Diagnostics to use the proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="634ae-182">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-182">Child Elements</span></span>|<span data-ttu-id="634ae-183">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="634ae-184">**CrashDumps**</span></span>|<span data-ttu-id="634ae-185">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="634ae-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="634ae-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="634ae-187">Azure 진단에 의해 생성된 로그의 컬렉션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="634ae-188">진단 인프라 로그는 진단 시스템 자체의 문제 해결에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-188">The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself.</span></span> <span data-ttu-id="634ae-189">선택적 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="634ae-190">- **scheduledTransferLogLevelFilter** - 수집된 로그의 최소 심각도 수준을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-190">- **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.</span></span><br /><br /> <span data-ttu-id="634ae-191">- **scheduledTransferPeriod** - 저장소에 예약된 전송 사이의 간격으로 가장 가까운 시간(분)으로 반올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-191">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="634ae-192">값은 [XML "기간 데이터 형식"](http://www.w3schools.com/schema/schema_dtypes_date.asp)입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-192">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="634ae-193">**Directories**</span><span class="sxs-lookup"><span data-stu-id="634ae-193">**Directories**</span></span>|<span data-ttu-id="634ae-194">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="634ae-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="634ae-195">**EtwProviders**</span></span>|<span data-ttu-id="634ae-196">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="634ae-197">**metrics**</span><span class="sxs-lookup"><span data-stu-id="634ae-197">**Metrics**</span></span>|<span data-ttu-id="634ae-198">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="634ae-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="634ae-199">**PerformanceCounters**</span></span>|<span data-ttu-id="634ae-200">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="634ae-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="634ae-201">**WindowsEventLog**</span></span>|<span data-ttu-id="634ae-202">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="634ae-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="634ae-203">**DockerSources**</span></span>|<span data-ttu-id="634ae-204">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="634ae-205">CrashDumps 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-205">CrashDumps Element</span></span>  
 <span data-ttu-id="634ae-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="634ae-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="634ae-207">크래시 덤프의 수집을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-207">Enable the collection of crash dumps.</span></span>  

|<span data-ttu-id="634ae-208">특성</span><span class="sxs-lookup"><span data-stu-id="634ae-208">Attributes</span></span>|<span data-ttu-id="634ae-209">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="634ae-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="634ae-210">**containerName**</span></span>|<span data-ttu-id="634ae-211">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-211">Optional.</span></span> <span data-ttu-id="634ae-212">크래시 덤프를 저장하는 데 사용할 Azure Storage 계정의 blob 컨테이너의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-212">The name of the blob container in your Azure Storage account to be used to store crash dumps.</span></span>|  
|<span data-ttu-id="634ae-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="634ae-213">**crashDumpType**</span></span>|<span data-ttu-id="634ae-214">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-214">Optional.</span></span>  <span data-ttu-id="634ae-215">최소 또는 전체 크래시 덤프를 수집하도록 Azure 진단을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-215">Configures Azure Diagnostics to collect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="634ae-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="634ae-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="634ae-217">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-217">Optional.</span></span>  <span data-ttu-id="634ae-218">VM에서 크래시 덤프에 대해 예약될 **overallQuotaInMB**의 비율을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-218">Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.</span></span>|  

|<span data-ttu-id="634ae-219">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-219">Child Elements</span></span>|<span data-ttu-id="634ae-220">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="634ae-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="634ae-222">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-222">Required.</span></span> <span data-ttu-id="634ae-223">각 프로세스에 대한 구성 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="634ae-224">다음과 같은 특성도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-224">The following attribute is also required:</span></span><br /><br /> <span data-ttu-id="634ae-225">**processName** - Azure 진단에서 크래시 덤프를 수집하도록 할 프로세스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-225">**processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="634ae-226">Directories 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-226">Directories Element</span></span> 
 <span data-ttu-id="634ae-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span><span class="sxs-lookup"><span data-stu-id="634ae-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="634ae-228">디렉터리, IIS 실패한 액세스 요청 로그 및/또는 IIS 로그의 콘텐츠 수집을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-228">Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="634ae-229">선택적 **scheduledTransferPeriod** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="634ae-230">이전 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-230">See explanation earlier.</span></span>  

|<span data-ttu-id="634ae-231">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-231">Child Elements</span></span>|<span data-ttu-id="634ae-232">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="634ae-233">**IISLogs**</span></span>|<span data-ttu-id="634ae-234">이 요소를 구성에 포함하면 IIS 로그의 컬렉션이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-234">Including this element in the configuration enables the collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="634ae-235">**containerName** - IIS를 저장하는 데 사용할 Azure Storage 계정의 blob 컨테이너의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-235">**containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.</span></span>|   
|<span data-ttu-id="634ae-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="634ae-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="634ae-237">이 요소를 구성에 포함하면 IIS 사이트 또는 응용 프로그램에 실패 한 요청에 대한 로그 컬렉션이 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-237">Including this element in the configuration enables collection of logs about failed requests to an IIS site or application.</span></span> <span data-ttu-id="634ae-238">또한 **Web.config**의 **system.WebServer**에 있는 추적 옵션도 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="634ae-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="634ae-239">**DataSources**</span></span>|<span data-ttu-id="634ae-240">모니터링할 디렉터리의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-240">A list of directories to monitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="634ae-241">DataSources 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-241">DataSources Element</span></span>  
 <span data-ttu-id="634ae-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span><span class="sxs-lookup"><span data-stu-id="634ae-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="634ae-243">모니터링할 디렉터리의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-243">A list of directories to monitor.</span></span>  

|<span data-ttu-id="634ae-244">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-244">Child Elements</span></span>|<span data-ttu-id="634ae-245">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="634ae-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="634ae-247">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-247">Required.</span></span> <span data-ttu-id="634ae-248">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="634ae-249">**containerName** - 로그 파일을 저장하는 데 사용할 Azure Storage 계정의 blob 컨테이너의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-249">**containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="634ae-250">DirectoryConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="634ae-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="634ae-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="634ae-252">**Absolute** 또는 **LocalResource** 요소 중 하나를 포함하되, 모두 포함할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-252">May include either the **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="634ae-253">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-253">Child Elements</span></span>|<span data-ttu-id="634ae-254">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="634ae-255">**Absolute**</span></span>|<span data-ttu-id="634ae-256">모니터링할 디렉터리의 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-256">The absolute path to the directory to monitor.</span></span> <span data-ttu-id="634ae-257">다음과 같은 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-257">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="634ae-258">- **Path** - 모니터링할 디렉터리의 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-258">- **Path** - The absolute path to the directory to monitor.</span></span><br /><br /> <span data-ttu-id="634ae-259">- **expandEnvironment** - 경로의 환경 변수가 확장되어 있는지 여부를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="634ae-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="634ae-260">**LocalResource**</span></span>|<span data-ttu-id="634ae-261">모니터링할 로컬 리소스의 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-261">The path relative to a local resource to monitor.</span></span> <span data-ttu-id="634ae-262">필수 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="634ae-263">- **Name** - 모니터링할 디렉터리를 포함하는 로컬 리소스</span><span class="sxs-lookup"><span data-stu-id="634ae-263">- **Name** - The local resource that contains the directory to monitor</span></span><br /><br /> <span data-ttu-id="634ae-264">- **relativePath** -모니터링할 디렉터리를 포함하는 이름의 상대 경로</span><span class="sxs-lookup"><span data-stu-id="634ae-264">- **relativePath** - The path relative to Name that contains the directory to monitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="634ae-265">EtwProviders 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-265">EtwProviders Element</span></span>  
 <span data-ttu-id="634ae-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="634ae-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="634ae-267">EventSource의 ETW 이벤트 및/또는 공급자를 기반으로 하는 ETW 매니페스트의 컬렉션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="634ae-268">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-268">Child Elements</span></span>|<span data-ttu-id="634ae-269">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="634ae-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="634ae-271">[EventSource 클래스](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)에서 생성된 이벤트 컬렉션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="634ae-272">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="634ae-273">**provider** - EventSource 이벤트의 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-273">**provider** - The class name of the EventSource event.</span></span><br /><br /> <span data-ttu-id="634ae-274">선택적 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="634ae-275">- **scheduledTransferLogLevelFilter** - 저장소 계정으로 전송할 최소 심각도 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-275">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="634ae-276">- **scheduledTransferPeriod** - 저장소에 예약된 전송 사이의 간격으로 가장 가까운 시간(분)으로 반올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-276">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="634ae-277">값은 [XML "기간 데이터 형식"](http://www.w3schools.com/schema/schema_dtypes_date.asp)입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-277">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="634ae-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="634ae-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="634ae-279">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="634ae-280">**provider** - 이벤트 공급자의 GUID</span><span class="sxs-lookup"><span data-stu-id="634ae-280">**provider** - The GUID of the event provider</span></span><br /><br /> <span data-ttu-id="634ae-281">선택적 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="634ae-282">- **scheduledTransferLogLevelFilter** - 저장소 계정으로 전송할 최소 심각도 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-282">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="634ae-283">- **scheduledTransferPeriod** - 저장소에 예약된 전송 사이의 간격으로 가장 가까운 시간(분)으로 반올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-283">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="634ae-284">값은 [XML "기간 데이터 형식"](http://www.w3schools.com/schema/schema_dtypes_date.asp)입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-284">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="634ae-285">EtwEventSourceProviderConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="634ae-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="634ae-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="634ae-287">[EventSource 클래스](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx)에서 생성된 이벤트 컬렉션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="634ae-288">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-288">Child Elements</span></span>|<span data-ttu-id="634ae-289">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="634ae-290">**DefaultEvents**</span></span>|<span data-ttu-id="634ae-291">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="634ae-292">**eventDestination** - 이벤트를 저장할 테이블의 이름</span><span class="sxs-lookup"><span data-stu-id="634ae-292">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="634ae-293">**Event**</span><span class="sxs-lookup"><span data-stu-id="634ae-293">**Event**</span></span>|<span data-ttu-id="634ae-294">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="634ae-295">**id** - 이벤트의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-295">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="634ae-296">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="634ae-297">**eventDestination** - 이벤트를 저장할 테이블의 이름</span><span class="sxs-lookup"><span data-stu-id="634ae-297">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="634ae-298">EtwManifestProviderConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="634ae-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="634ae-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="634ae-300">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-300">Child Elements</span></span>|<span data-ttu-id="634ae-301">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="634ae-302">**DefaultEvents**</span></span>|<span data-ttu-id="634ae-303">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="634ae-304">**eventDestination** - 이벤트를 저장할 테이블의 이름</span><span class="sxs-lookup"><span data-stu-id="634ae-304">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="634ae-305">**Event**</span><span class="sxs-lookup"><span data-stu-id="634ae-305">**Event**</span></span>|<span data-ttu-id="634ae-306">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="634ae-307">**id** - 이벤트의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-307">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="634ae-308">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="634ae-309">**eventDestination** - 이벤트를 저장할 테이블의 이름</span><span class="sxs-lookup"><span data-stu-id="634ae-309">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="634ae-310">Metrics 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-310">Metrics Element</span></span>  
 <span data-ttu-id="634ae-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span><span class="sxs-lookup"><span data-stu-id="634ae-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="634ae-312">빠른 쿼리를 위해 최적화된 성능 카운터 테이블을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-312">Enables you to generate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="634ae-313">**PerformanceCounters** 요소에 정의되어 있는 각 성능 카운터는 성능 카운터 테이블에 추가된 메트릭 테이블에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-313">Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.</span></span>  

 <span data-ttu-id="634ae-314">**resourceId** 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-314">The **resourceId** attribute is required.</span></span>  <span data-ttu-id="634ae-315">Azure 진단을 배포하는 가상 컴퓨터의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-315">The resource ID of the Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="634ae-316">[Azure Portal](https://portal.azure.com)에서 **resourceID**를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-316">Get the **resourceID** from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="634ae-317">**찾아보기** -> **리소스 그룹** -> **<이름\>**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="634ae-318">**속성** 타일을 클릭하고 **ID** 필드에서 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-318">Click the **Properties** tile and copy the value from the **ID** field.</span></span>  

|<span data-ttu-id="634ae-319">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-319">Child Elements</span></span>|<span data-ttu-id="634ae-320">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="634ae-321">**MetricAggregation**</span></span>|<span data-ttu-id="634ae-322">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="634ae-323">**scheduledTransferPeriod** - 저장소에 예약된 전송 사이의 간격으로 가장 가까운 시간(분)으로 반올림됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-323">**scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="634ae-324">값은 [XML "기간 데이터 형식"](http://www.w3schools.com/schema/schema_dtypes_date.asp)입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-324">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="634ae-325">PerformanceCounters 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="634ae-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="634ae-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="634ae-327">성능 카운터의 컬렉션을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-327">Enables the collection of performance counters.</span></span>  

 <span data-ttu-id="634ae-328">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-328">Optional attribute:</span></span>  

 <span data-ttu-id="634ae-329">선택적 **scheduledTransferPeriod** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="634ae-330">이전 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-330">See explanation earlier.</span></span>

|<span data-ttu-id="634ae-331">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-331">Child Element</span></span>|<span data-ttu-id="634ae-332">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="634ae-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="634ae-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="634ae-334">다음과 같은 특성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-334">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="634ae-335">- **counterSpecifier** - 성능 카운터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-335">- **counterSpecifier** - The name of the performance counter.</span></span> <span data-ttu-id="634ae-336">예: `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="634ae-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="634ae-337">호스트에서 성능 카운터의 목록을 가져오려면 명령 `typeperf`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-337">To get a list of performance counters on your host, run the command `typeperf`.</span></span><br /><br /> <span data-ttu-id="634ae-338">- **sampleRate** - 카운터가 샘플링되는 주기입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-338">- **sampleRate** - How often the counter should be sampled.</span></span><br /><br /> <span data-ttu-id="634ae-339">선택적 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="634ae-340">**unit** - 카운터의 측정 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-340">**unit** - The unit of measure of the counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="634ae-341">WindowsEventLog 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="634ae-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="634ae-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="634ae-343">Windows 이벤트 로그의 컬렉션을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-343">Enables the collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="634ae-344">선택적 **scheduledTransferPeriod** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="634ae-345">이전 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="634ae-346">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-346">Child Element</span></span>|<span data-ttu-id="634ae-347">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="634ae-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="634ae-348">**DataSource**</span></span>|<span data-ttu-id="634ae-349">수집할 Windows 이벤트 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-349">The Windows Event logs to collect.</span></span> <span data-ttu-id="634ae-350">필수 특성:</span><span class="sxs-lookup"><span data-stu-id="634ae-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="634ae-351">**name** - 수집할 Windows 이벤트를 설명하는 XPath 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-351">**name** - The XPath query describing the windows events to be collected.</span></span> <span data-ttu-id="634ae-352">예:</span><span class="sxs-lookup"><span data-stu-id="634ae-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="634ae-353">모든 이벤트를 수집하려면 “*”를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-353">To collect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="634ae-354">Logs 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-354">Logs Element</span></span>  
 <span data-ttu-id="634ae-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span><span class="sxs-lookup"><span data-stu-id="634ae-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="634ae-356">버전 1.0 및 1.1에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="634ae-357">1.2에는 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-357">Missing in 1.2.</span></span> <span data-ttu-id="634ae-358">1.3에서 다시 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="634ae-359">기본 Azure 로그의 버퍼 구성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-359">Defines the buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="634ae-360">특성</span><span class="sxs-lookup"><span data-stu-id="634ae-360">Attribute</span></span>|<span data-ttu-id="634ae-361">형식</span><span class="sxs-lookup"><span data-stu-id="634ae-361">Type</span></span>|<span data-ttu-id="634ae-362">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="634ae-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="634ae-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="634ae-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="634ae-364">**unsignedInt**</span></span>|<span data-ttu-id="634ae-365">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-365">Optional.</span></span> <span data-ttu-id="634ae-366">지정된 데이터에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-366">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="634ae-367">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-367">The default is 0.</span></span>|  
|<span data-ttu-id="634ae-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="634ae-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="634ae-369">**string**</span><span class="sxs-lookup"><span data-stu-id="634ae-369">**string**</span></span>|<span data-ttu-id="634ae-370">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-370">Optional.</span></span> <span data-ttu-id="634ae-371">전송되는 로그 항목에 대한 최소 심각도 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-371">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="634ae-372">기본값은 **Undefined**로, 모든 로그를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-372">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="634ae-373">정보가 적은 순서대로 사용 가능한 다른 값을 나열하면 다음과 같습니다. **자세한 정보**, **정보**, **경고**, **오류**, **중요**</span><span class="sxs-lookup"><span data-stu-id="634ae-373">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="634ae-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="634ae-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="634ae-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="634ae-375">**duration**</span></span>|<span data-ttu-id="634ae-376">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-376">Optional.</span></span> <span data-ttu-id="634ae-377">예약된 데이터 전송 사이의 간격(가장 가까운 시간(분)으로 반올림)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-377">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="634ae-378">기본값은 PT0S입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-378">The default is PT0S.</span></span>|  
|<span data-ttu-id="634ae-379">**싱크** 1.5에서 추가됨</span><span class="sxs-lookup"><span data-stu-id="634ae-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="634ae-380">**string**</span><span class="sxs-lookup"><span data-stu-id="634ae-380">**string**</span></span>|<span data-ttu-id="634ae-381">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-381">Optional.</span></span> <span data-ttu-id="634ae-382">또한 진단 데이터를 보내는 싱크 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-382">Points to a sink location to also send diagnostic data.</span></span> <span data-ttu-id="634ae-383">예를 들어 Application Insights입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="634ae-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="634ae-384">DockerSources</span></span>
 <span data-ttu-id="634ae-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span><span class="sxs-lookup"><span data-stu-id="634ae-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="634ae-386">1.9에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-386">Added in 1.9.</span></span>

|<span data-ttu-id="634ae-387">요소 이름</span><span class="sxs-lookup"><span data-stu-id="634ae-387">Element Name</span></span>|<span data-ttu-id="634ae-388">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="634ae-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="634ae-389">**Stats**</span></span>|<span data-ttu-id="634ae-390">Docker 컨테이너에 대한 통계를 수집하도록 시스템에 지시</span><span class="sxs-lookup"><span data-stu-id="634ae-390">Tells the system to collect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="634ae-391">SinksConfig 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-391">SinksConfig Element</span></span>  
 <span data-ttu-id="634ae-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="634ae-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="634ae-393">진단 데이터를 보낼 위치와 그러한 위치와 관련된 구성의 목록 입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-393">A list of locations to send diagnostics data to and the configuration associated with those locations.</span></span>  

|<span data-ttu-id="634ae-394">요소 이름</span><span class="sxs-lookup"><span data-stu-id="634ae-394">Element Name</span></span>|<span data-ttu-id="634ae-395">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="634ae-396">**싱크**</span><span class="sxs-lookup"><span data-stu-id="634ae-396">**Sink**</span></span>|<span data-ttu-id="634ae-397">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="634ae-398">싱크 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-398">Sink Element</span></span>
 <span data-ttu-id="634ae-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span><span class="sxs-lookup"><span data-stu-id="634ae-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="634ae-400">버전 1.5에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="634ae-401">진단 데이터를 보낼 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-401">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="634ae-402">예를 들어 Application Insights 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-402">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="634ae-403">특성</span><span class="sxs-lookup"><span data-stu-id="634ae-403">Attribute</span></span>|<span data-ttu-id="634ae-404">형식</span><span class="sxs-lookup"><span data-stu-id="634ae-404">Type</span></span>|<span data-ttu-id="634ae-405">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="634ae-406">**name**</span><span class="sxs-lookup"><span data-stu-id="634ae-406">**name**</span></span>|<span data-ttu-id="634ae-407">string</span><span class="sxs-lookup"><span data-stu-id="634ae-407">string</span></span>|<span data-ttu-id="634ae-408">sinkname을 식별하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-408">A string identifying the sinkname.</span></span>|  

|<span data-ttu-id="634ae-409">요소</span><span class="sxs-lookup"><span data-stu-id="634ae-409">Element</span></span>|<span data-ttu-id="634ae-410">유형</span><span class="sxs-lookup"><span data-stu-id="634ae-410">Type</span></span>|<span data-ttu-id="634ae-411">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="634ae-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="634ae-412">**Application Insights**</span></span>|<span data-ttu-id="634ae-413">string</span><span class="sxs-lookup"><span data-stu-id="634ae-413">string</span></span>|<span data-ttu-id="634ae-414">데이터를 Application Insights로 전송하는 경우에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-414">Used only when sending data to Application Insights.</span></span> <span data-ttu-id="634ae-415">액세스 권한이 있는 활성 Application Insights 계정에 대한 계측 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-415">Contain the Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="634ae-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="634ae-416">**Channels**</span></span>|<span data-ttu-id="634ae-417">string</span><span class="sxs-lookup"><span data-stu-id="634ae-417">string</span></span>|<span data-ttu-id="634ae-418">스트림하는 각 추가 필터링에 대한</span><span class="sxs-lookup"><span data-stu-id="634ae-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="634ae-419">Channels 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-419">Channels Element</span></span>  
 <span data-ttu-id="634ae-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span><span class="sxs-lookup"><span data-stu-id="634ae-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="634ae-421">버전 1.5에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="634ae-422">싱크를 통해 전달되는 로그 데이터의 스트림에 대한 필터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="634ae-423">요소</span><span class="sxs-lookup"><span data-stu-id="634ae-423">Element</span></span>|<span data-ttu-id="634ae-424">유형</span><span class="sxs-lookup"><span data-stu-id="634ae-424">Type</span></span>|<span data-ttu-id="634ae-425">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="634ae-426">**채널**</span><span class="sxs-lookup"><span data-stu-id="634ae-426">**Channel**</span></span>|<span data-ttu-id="634ae-427">string</span><span class="sxs-lookup"><span data-stu-id="634ae-427">string</span></span>|<span data-ttu-id="634ae-428">이 페이지의 다른 곳에 있는 설명을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="634ae-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="634ae-429">채널 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-429">Channel Element</span></span>
 <span data-ttu-id="634ae-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span><span class="sxs-lookup"><span data-stu-id="634ae-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="634ae-431">버전 1.5에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="634ae-432">진단 데이터를 보낼 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-432">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="634ae-433">예를 들어 Application Insights 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-433">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="634ae-434">특성</span><span class="sxs-lookup"><span data-stu-id="634ae-434">Attributes</span></span>|<span data-ttu-id="634ae-435">유형</span><span class="sxs-lookup"><span data-stu-id="634ae-435">Type</span></span>|<span data-ttu-id="634ae-436">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="634ae-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="634ae-437">**logLevel**</span></span>|<span data-ttu-id="634ae-438">**string**</span><span class="sxs-lookup"><span data-stu-id="634ae-438">**string**</span></span>|<span data-ttu-id="634ae-439">전송되는 로그 항목에 대한 최소 심각도 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-439">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="634ae-440">기본값은 **Undefined**로, 모든 로그를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-440">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="634ae-441">정보가 적은 순서대로 사용 가능한 다른 값을 나열하면 다음과 같습니다. **자세한 정보**, **정보**, **경고**, **오류**, **중요**</span><span class="sxs-lookup"><span data-stu-id="634ae-441">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="634ae-442">**name**</span><span class="sxs-lookup"><span data-stu-id="634ae-442">**name**</span></span>|<span data-ttu-id="634ae-443">**string**</span><span class="sxs-lookup"><span data-stu-id="634ae-443">**string**</span></span>|<span data-ttu-id="634ae-444">참조 하는 채널의 고유 이름</span><span class="sxs-lookup"><span data-stu-id="634ae-444">A unique name of the channel to refer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="634ae-445">PrivateConfig 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="634ae-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="634ae-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="634ae-447">버전 1.3에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="634ae-448">옵션</span><span class="sxs-lookup"><span data-stu-id="634ae-448">Optional</span></span>  

 <span data-ttu-id="634ae-449">저장소 계정(이름, 키 및 끝점)의 개인 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-449">Stores the private details of the storage account (name, key, and endpoint).</span></span> <span data-ttu-id="634ae-450">이 정보는 가상 컴퓨터에 전송되지만 여기에서 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-450">This information is sent to the virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="634ae-451">자식 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-451">Child Elements</span></span>|<span data-ttu-id="634ae-452">설명</span><span class="sxs-lookup"><span data-stu-id="634ae-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="634ae-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="634ae-453">**StorageAccount**</span></span>|<span data-ttu-id="634ae-454">사용할 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-454">The storage account to use.</span></span> <span data-ttu-id="634ae-455">다음과 같은 특성이 필요</span><span class="sxs-lookup"><span data-stu-id="634ae-455">The following attributes are required</span></span><br /><br /> <span data-ttu-id="634ae-456">- **이름** - 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-456">- **name** - The name of the storage account.</span></span><br /><br /> <span data-ttu-id="634ae-457">- **키** - 저장소 계정의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-457">- **key** - The key to the storage account.</span></span><br /><br /> <span data-ttu-id="634ae-458">- **끝점** - 저장소 계정에 액세스하는 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-458">- **endpoint** - The endpoint to access the storage account.</span></span> <br /><br /> <span data-ttu-id="634ae-459">-**sasToken**(1.8.1에 추가됨) - 개인 구성에서 저장소 계정 키 대신 SAS 토큰을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="634ae-460">제공된 경우 저장소 계정 키가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-460">If provided, the storage account key is ignored.</span></span> <br /><span data-ttu-id="634ae-461">SAS 토큰에 대한 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="634ae-461">Requirements for the SAS Token:</span></span> <br /><span data-ttu-id="634ae-462">- 계정 SAS 토큰만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-462">- Supports account SAS token only</span></span> <br /><span data-ttu-id="634ae-463">- *b*, *t* 서비스 형식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-463">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="634ae-464">- *a*, *c*, *u*, *w* 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-464">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="634ae-465">- *c*, *o* 리소스 형식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-465">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="634ae-466">- HTTPS 프로토콜만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-466">- Supports the HTTPS protocol only</span></span> <br /> <span data-ttu-id="634ae-467">- 시작 및 만료 시간이 유효해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-467">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="634ae-468">IsEnabled 요소</span><span class="sxs-lookup"><span data-stu-id="634ae-468">IsEnabled Element</span></span>  
 <span data-ttu-id="634ae-469">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="634ae-469">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="634ae-470">부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-470">Boolean.</span></span> <span data-ttu-id="634ae-471">`true`를 사용하여 진단을 사용하도록 설정하거나 `false`를 사용하여 진단을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="634ae-471">Use `true` to enable the diagnostics or `false` to disable the diagnostics.</span></span>
