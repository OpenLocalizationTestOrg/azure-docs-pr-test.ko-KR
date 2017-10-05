---
title: "Azure 진단 1.0 구성 스키마 | Microsoft Docs"
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
ms.openlocfilehash: a8fdfb52d5091d3fc9779657737c7430fcfada51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="5cb4b-103">Azure 진단 1.0 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="5cb4b-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="5cb4b-104">Azure 진단은 Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric 및 Cloud Services에서 성능 카운터 및 기타 통계를 수집하는 데 사용되는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="5cb4b-105">이 페이지는 이러한 서비스 중 하나를 사용하는 경우에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="5cb4b-106">Azure 진단은 Azure Monitor, Application Insights 및 Log Analytics와 같은 기타 Microsoft 진단 제품과 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="5cb4b-107">Azure 진단 구성 파일은 진단 모니터를 초기화하는 데 사용되는 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-107">The Azure Diagnostics configuration file defines values that are used to initialize the Diagnostics Monitor.</span></span> <span data-ttu-id="5cb4b-108">이 파일은 진단 모니터가 시작될 때 진단 구성 설정을 초기화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-108">This file is used to initialize diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

 <span data-ttu-id="5cb4b-109">기본적으로 Azure 진단 구성 스키마 파일은 `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` 디렉터리에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-109">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="5cb4b-110">`<version>`을 [Azure SDK](http://www.windowsazure.com/develop/downloads/)의 설치된 버전으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-110">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="5cb4b-111">진단 구성 파일은 일반적으로 시작 프로세스 초기에 진단 데이터 수집을 요하는 시작 작업에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-111">The diagnostics configuration file is typically used with startup tasks that require diagnostic data to be collected earlier in the startup process.</span></span> <span data-ttu-id="5cb4b-112">Azure 진단에 대한 자세한 내용은 [Azure 진단을 사용하여 로깅 데이터 수집](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="5cb4b-113">진단 구성 파일 예제</span><span class="sxs-lookup"><span data-stu-id="5cb4b-113">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="5cb4b-114">다음 예제에서는 일반적인 진단 구성 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-114">The following example shows a typical diagnostics configuration file:</span></span>  

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

      <!-- These three elements specify the special directories   
           that are set up for the log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories the DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative to a local   
                 resource defined in the service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- The counter specifier is in the same format as the imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- The event log name is in the same format as the imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="5cb4b-115">DiagnosticsConfiguration 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="5cb4b-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="5cb4b-116">진단 구성 파일에 대한 XML 네임스페이스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-116">The XML namespace for the diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="5cb4b-117">스키마 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-117">Schema Elements</span></span>  
 <span data-ttu-id="5cb4b-118">진단 구성 파일에는 다음과 같은 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-118">The diagnostics configuration file includes the following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="5cb4b-119">DiagnosticMonitorConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="5cb4b-120">진단 구성 파일의 최상위 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-120">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="5cb4b-121">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-121">Attributes:</span></span>

|<span data-ttu-id="5cb4b-122">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-122">Attribute</span></span>  |<span data-ttu-id="5cb4b-123">유형</span><span class="sxs-lookup"><span data-stu-id="5cb4b-123">Type</span></span>   |<span data-ttu-id="5cb4b-124">필수</span><span class="sxs-lookup"><span data-stu-id="5cb4b-124">Required</span></span>| <span data-ttu-id="5cb4b-125">기본값</span><span class="sxs-lookup"><span data-stu-id="5cb4b-125">Default</span></span> | <span data-ttu-id="5cb4b-126">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="5cb4b-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="5cb4b-128">duration</span><span class="sxs-lookup"><span data-stu-id="5cb4b-128">duration</span></span>|<span data-ttu-id="5cb4b-129">옵션</span><span class="sxs-lookup"><span data-stu-id="5cb4b-129">Optional</span></span> | <span data-ttu-id="5cb4b-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="5cb4b-130">PT1M</span></span>| <span data-ttu-id="5cb4b-131">진단 모니터가 진단 구성 변경을 폴링하는 간격을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-131">Specifies the interval at which the diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="5cb4b-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="5cb4b-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="5cb4b-133">unsignedInt</span></span>|<span data-ttu-id="5cb4b-134">옵션</span><span class="sxs-lookup"><span data-stu-id="5cb4b-134">Optional</span></span>| <span data-ttu-id="5cb4b-135">4000MB</span><span class="sxs-lookup"><span data-stu-id="5cb4b-135">4000 MB.</span></span> <span data-ttu-id="5cb4b-136">값을 제공하는 경우 이 크기를 초과하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="5cb4b-137">모든 로깅 버퍼에 할당된 파일 시스템 저장소의 총 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-137">The total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="5cb4b-138">DiagnosticInfrastructureLogs 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="5cb4b-139">기본 진단 인프라에서 생성하는 로그의 버퍼 구성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-139">Defines the buffer configuration for the logs that are generated by the underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="5cb4b-140">부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="5cb4b-141">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-141">Attributes:</span></span>

|<span data-ttu-id="5cb4b-142">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-142">Attribute</span></span>|<span data-ttu-id="5cb4b-143">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-143">Type</span></span>|<span data-ttu-id="5cb4b-144">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="5cb4b-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="5cb4b-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="5cb4b-146">unsignedInt</span></span>|<span data-ttu-id="5cb4b-147">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-147">Optional.</span></span> <span data-ttu-id="5cb4b-148">지정된 데이터에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-148">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="5cb4b-149">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-149">The default is 0.</span></span>|  
|<span data-ttu-id="5cb4b-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="5cb4b-151">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-151">string</span></span>|<span data-ttu-id="5cb4b-152">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-152">Optional.</span></span> <span data-ttu-id="5cb4b-153">전송되는 로그 항목에 대한 최소 심각도 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-153">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="5cb4b-154">기본값은 **Undefined**입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-154">The default value is **Undefined**.</span></span> <span data-ttu-id="5cb4b-155">사용 가능한 다른 값은 **Verbose**, **Information**, **Warning**, **Error**, 및 **Critical**입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="5cb4b-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="5cb4b-157">duration</span><span class="sxs-lookup"><span data-stu-id="5cb4b-157">duration</span></span>|<span data-ttu-id="5cb4b-158">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-158">Optional.</span></span> <span data-ttu-id="5cb4b-159">예약된 데이터 전송 사이의 간격(가장 가까운 시간(분)으로 반올림)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-159">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="5cb4b-160">기본값은 PT0S입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-160">The default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="5cb4b-161">Logs 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-161">Logs Element</span></span>  
 <span data-ttu-id="5cb4b-162">기본 Azure 로그의 버퍼 구성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-162">Defines the buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="5cb4b-163">부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="5cb4b-164">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-164">Attributes:</span></span>  

|<span data-ttu-id="5cb4b-165">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-165">Attribute</span></span>|<span data-ttu-id="5cb4b-166">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-166">Type</span></span>|<span data-ttu-id="5cb4b-167">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="5cb4b-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="5cb4b-169">unsignedInt</span></span>|<span data-ttu-id="5cb4b-170">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-170">Optional.</span></span> <span data-ttu-id="5cb4b-171">지정된 데이터에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-171">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="5cb4b-172">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-172">The default is 0.</span></span>|  
|<span data-ttu-id="5cb4b-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="5cb4b-174">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-174">string</span></span>|<span data-ttu-id="5cb4b-175">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-175">Optional.</span></span> <span data-ttu-id="5cb4b-176">전송되는 로그 항목에 대한 최소 심각도 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-176">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="5cb4b-177">기본값은 **Undefined**입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-177">The default value is **Undefined**.</span></span> <span data-ttu-id="5cb4b-178">사용 가능한 다른 값은 **Verbose**, **Information**, **Warning**, **Error**, 및 **Critical**입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="5cb4b-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="5cb4b-180">duration</span><span class="sxs-lookup"><span data-stu-id="5cb4b-180">duration</span></span>|<span data-ttu-id="5cb4b-181">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-181">Optional.</span></span> <span data-ttu-id="5cb4b-182">예약된 데이터 전송 사이의 간격(가장 가까운 시간(분)으로 반올림)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-182">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="5cb4b-183">기본값은 PT0S입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-183">The default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="5cb4b-184">Directories 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-184">Directories Element</span></span>  
<span data-ttu-id="5cb4b-185">정의할 수 있는 파일 기반 로그의 버퍼 구성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-185">Defines the buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="5cb4b-186">부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="5cb4b-187">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-187">Attributes:</span></span>  

|<span data-ttu-id="5cb4b-188">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-188">Attribute</span></span>|<span data-ttu-id="5cb4b-189">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-189">Type</span></span>|<span data-ttu-id="5cb4b-190">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="5cb4b-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="5cb4b-192">unsignedInt</span></span>|<span data-ttu-id="5cb4b-193">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-193">Optional.</span></span> <span data-ttu-id="5cb4b-194">지정된 데이터에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-194">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="5cb4b-195">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-195">The default is 0.</span></span>|  
|<span data-ttu-id="5cb4b-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="5cb4b-197">duration</span><span class="sxs-lookup"><span data-stu-id="5cb4b-197">duration</span></span>|<span data-ttu-id="5cb4b-198">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-198">Optional.</span></span> <span data-ttu-id="5cb4b-199">예약된 데이터 전송 사이의 간격(가장 가까운 시간(분)으로 반올림)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-199">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="5cb4b-200">기본값은 PT0S입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-200">The default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="5cb4b-201">CrashDumps 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-201">CrashDumps Element</span></span>  
 <span data-ttu-id="5cb4b-202">크래시 덤프 디렉터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-202">Defines the crash dumps directory.</span></span>

 <span data-ttu-id="5cb4b-203">부모 요소: [Directories 요소](#Directories).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="5cb4b-204">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-204">Attributes:</span></span>  

|<span data-ttu-id="5cb4b-205">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-205">Attribute</span></span>|<span data-ttu-id="5cb4b-206">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-206">Type</span></span>|<span data-ttu-id="5cb4b-207">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-208">**container**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-208">**container**</span></span>|<span data-ttu-id="5cb4b-209">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-209">string</span></span>|<span data-ttu-id="5cb4b-210">디렉터리의 내용이 전송될 컨테이너의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-210">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="5cb4b-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="5cb4b-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="5cb4b-212">unsignedInt</span></span>|<span data-ttu-id="5cb4b-213">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-213">Optional.</span></span> <span data-ttu-id="5cb4b-214">디렉터리의 최대 크기(MB)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-214">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="5cb4b-215">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-215">The default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="5cb4b-216">FailedRequestLogs 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="5cb4b-217">실패한 요청 로그 디렉터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-217">Defines the failed request log directory.</span></span>

 <span data-ttu-id="5cb4b-218">부모 요소[Directories 요소](#Directories).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="5cb4b-219">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-219">Attributes:</span></span>  

|<span data-ttu-id="5cb4b-220">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-220">Attribute</span></span>|<span data-ttu-id="5cb4b-221">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-221">Type</span></span>|<span data-ttu-id="5cb4b-222">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-223">**container**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-223">**container**</span></span>|<span data-ttu-id="5cb4b-224">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-224">string</span></span>|<span data-ttu-id="5cb4b-225">디렉터리의 내용이 전송될 컨테이너의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-225">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="5cb4b-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="5cb4b-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="5cb4b-227">unsignedInt</span></span>|<span data-ttu-id="5cb4b-228">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-228">Optional.</span></span> <span data-ttu-id="5cb4b-229">디렉터리의 최대 크기(MB)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-229">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="5cb4b-230">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-230">The default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="5cb4b-231">IISLogs 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-231">IISLogs Element</span></span>  
 <span data-ttu-id="5cb4b-232">IIS 로그 디렉터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-232">Defines the IIS log directory.</span></span>

 <span data-ttu-id="5cb4b-233">부모 요소[Directories 요소](#Directories).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="5cb4b-234">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-234">Attributes:</span></span>  

|<span data-ttu-id="5cb4b-235">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-235">Attribute</span></span>|<span data-ttu-id="5cb4b-236">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-236">Type</span></span>|<span data-ttu-id="5cb4b-237">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-238">**container**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-238">**container**</span></span>|<span data-ttu-id="5cb4b-239">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-239">string</span></span>|<span data-ttu-id="5cb4b-240">디렉터리의 내용이 전송될 컨테이너의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-240">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="5cb4b-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="5cb4b-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="5cb4b-242">unsignedInt</span></span>|<span data-ttu-id="5cb4b-243">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-243">Optional.</span></span> <span data-ttu-id="5cb4b-244">디렉터리의 최대 크기(MB)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-244">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="5cb4b-245">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-245">The default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="5cb4b-246">DataSources 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-246">DataSources Element</span></span>  
 <span data-ttu-id="5cb4b-247">0개 이상의 추가 로그 디렉터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="5cb4b-248">부모 요소: [Directories 요소](#Directories).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="5cb4b-249">DirectoryConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="5cb4b-250">모니터링할 로그 파일의 디렉터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-250">Defines the directory of log files to monitor.</span></span>

 <span data-ttu-id="5cb4b-251">부모 요소: [DataSources 요소](#DataSources)</span><span class="sxs-lookup"><span data-stu-id="5cb4b-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="5cb4b-252">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-252">Attributes:</span></span>

|<span data-ttu-id="5cb4b-253">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-253">Attribute</span></span>|<span data-ttu-id="5cb4b-254">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-254">Type</span></span>|<span data-ttu-id="5cb4b-255">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-256">**container**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-256">**container**</span></span>|<span data-ttu-id="5cb4b-257">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-257">string</span></span>|<span data-ttu-id="5cb4b-258">디렉터리의 내용이 전송될 컨테이너의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-258">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="5cb4b-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="5cb4b-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="5cb4b-260">unsignedInt</span></span>|<span data-ttu-id="5cb4b-261">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-261">Optional.</span></span> <span data-ttu-id="5cb4b-262">디렉터리의 최대 크기(MB)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-262">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="5cb4b-263">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-263">The default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="5cb4b-264">Absolute 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-264">Absolute Element</span></span>  
 <span data-ttu-id="5cb4b-265">선택적 환경 확장을 사용하여 모니터링할 디렉터리의 절대 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-265">Defines an absolute path of the directory to monitor with optional environment expansion.</span></span>

 <span data-ttu-id="5cb4b-266">부모 요소: [DirectoryConfiguration 요소](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="5cb4b-267">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-267">Attributes:</span></span>  

|<span data-ttu-id="5cb4b-268">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-268">Attribute</span></span>|<span data-ttu-id="5cb4b-269">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-269">Type</span></span>|<span data-ttu-id="5cb4b-270">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-271">**path**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-271">**path**</span></span>|<span data-ttu-id="5cb4b-272">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-272">string</span></span>|<span data-ttu-id="5cb4b-273">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-273">Required.</span></span> <span data-ttu-id="5cb4b-274">모니터링할 디렉터리의 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-274">The absolute path to the directory to monitor.</span></span>|  
|<span data-ttu-id="5cb4b-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-275">**expandEnvironment**</span></span>|<span data-ttu-id="5cb4b-276">부울</span><span class="sxs-lookup"><span data-stu-id="5cb4b-276">boolean</span></span>|<span data-ttu-id="5cb4b-277">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-277">Required.</span></span> <span data-ttu-id="5cb4b-278">**true**로 설정하면 경로의 환경 변수가 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-278">If set to **true**, environment variables in the path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="5cb4b-279">LocalResource 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-279">LocalResource Element</span></span>  
 <span data-ttu-id="5cb4b-280">서비스 정의에 정의된 로컬 리소스의 상대 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-280">Defines a path relative to a local resource defined in the service definition.</span></span>

 <span data-ttu-id="5cb4b-281">부모 요소: [DirectoryConfiguration 요소](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="5cb4b-282">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-282">Attributes:</span></span>  

|<span data-ttu-id="5cb4b-283">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-283">Attribute</span></span>|<span data-ttu-id="5cb4b-284">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-284">Type</span></span>|<span data-ttu-id="5cb4b-285">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-286">**name**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-286">**name**</span></span>|<span data-ttu-id="5cb4b-287">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-287">string</span></span>|<span data-ttu-id="5cb4b-288">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-288">Required.</span></span> <span data-ttu-id="5cb4b-289">모니터링할 디렉터리를 포함하는 로컬 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-289">The name of the local resource that contains the directory to monitor.</span></span>|  
|<span data-ttu-id="5cb4b-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-290">**relativePath**</span></span>|<span data-ttu-id="5cb4b-291">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-291">string</span></span>|<span data-ttu-id="5cb4b-292">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-292">Required.</span></span> <span data-ttu-id="5cb4b-293">모니터링할 로컬 리소스의 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-293">The path relative to the local resource to monitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="5cb4b-294">PerformanceCounters 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="5cb4b-295">수집할 성능 카운터의 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-295">Defines the path to the performance counter to collect.</span></span>

 <span data-ttu-id="5cb4b-296">부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="5cb4b-297">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-297">Attributes:</span></span>  

|<span data-ttu-id="5cb4b-298">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-298">Attribute</span></span>|<span data-ttu-id="5cb4b-299">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-299">Type</span></span>|<span data-ttu-id="5cb4b-300">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="5cb4b-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="5cb4b-302">unsignedInt</span></span>|<span data-ttu-id="5cb4b-303">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-303">Optional.</span></span> <span data-ttu-id="5cb4b-304">지정된 데이터에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-304">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="5cb4b-305">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-305">The default is 0.</span></span>|  
|<span data-ttu-id="5cb4b-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="5cb4b-307">duration</span><span class="sxs-lookup"><span data-stu-id="5cb4b-307">duration</span></span>|<span data-ttu-id="5cb4b-308">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-308">Optional.</span></span> <span data-ttu-id="5cb4b-309">예약된 데이터 전송 사이의 간격(가장 가까운 시간(분)으로 반올림)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-309">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="5cb4b-310">기본값은 PT0S입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-310">The default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="5cb4b-311">PerformanceCounterConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="5cb4b-312">수집할 성능 카운터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-312">Defines the performance counter to collect.</span></span>

 <span data-ttu-id="5cb4b-313">부모 요소: [PerformanceCounters 요소](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="5cb4b-314">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-314">Attributes:</span></span>  

|<span data-ttu-id="5cb4b-315">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-315">Attribute</span></span>|<span data-ttu-id="5cb4b-316">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-316">Type</span></span>|<span data-ttu-id="5cb4b-317">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-318">**counterSpecifier**</span></span>|<span data-ttu-id="5cb4b-319">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-319">string</span></span>|<span data-ttu-id="5cb4b-320">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-320">Required.</span></span> <span data-ttu-id="5cb4b-321">수집할 성능 카운터의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-321">The path to the performance counter to collect.</span></span>|  
|<span data-ttu-id="5cb4b-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-322">**sampleRate**</span></span>|<span data-ttu-id="5cb4b-323">duration</span><span class="sxs-lookup"><span data-stu-id="5cb4b-323">duration</span></span>|<span data-ttu-id="5cb4b-324">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-324">Required.</span></span> <span data-ttu-id="5cb4b-325">성능 카운터를 수집할 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-325">The rate at which the performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="5cb4b-326">WindowsEventLog 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="5cb4b-327">모니터링할 이벤트 로그를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-327">Defines the event logs to monitor.</span></span>

 <span data-ttu-id="5cb4b-328">부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="5cb4b-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="5cb4b-329">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-329">Attributes:</span></span>

|<span data-ttu-id="5cb4b-330">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-330">Attribute</span></span>|<span data-ttu-id="5cb4b-331">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-331">Type</span></span>|<span data-ttu-id="5cb4b-332">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="5cb4b-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="5cb4b-334">unsignedInt</span></span>|<span data-ttu-id="5cb4b-335">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-335">Optional.</span></span> <span data-ttu-id="5cb4b-336">지정된 데이터에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-336">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="5cb4b-337">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-337">The default is 0.</span></span>|  
|<span data-ttu-id="5cb4b-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="5cb4b-339">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-339">string</span></span>|<span data-ttu-id="5cb4b-340">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-340">Optional.</span></span> <span data-ttu-id="5cb4b-341">전송되는 로그 항목에 대한 최소 심각도 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-341">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="5cb4b-342">기본값은 **Undefined**입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-342">The default value is **Undefined**.</span></span> <span data-ttu-id="5cb4b-343">사용 가능한 다른 값은 **Verbose**, **Information**, **Warning**, **Error**, 및 **Critical**입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="5cb4b-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="5cb4b-345">duration</span><span class="sxs-lookup"><span data-stu-id="5cb4b-345">duration</span></span>|<span data-ttu-id="5cb4b-346">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-346">Optional.</span></span> <span data-ttu-id="5cb4b-347">예약된 데이터 전송 사이의 간격(가장 가까운 시간(분)으로 반올림)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-347">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="5cb4b-348">기본값은 PT0S입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-348">The default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="5cb4b-349">DataSource 요소</span><span class="sxs-lookup"><span data-stu-id="5cb4b-349">DataSource Element</span></span>  
 <span data-ttu-id="5cb4b-350">모니터링할 이벤트 로그를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-350">Defines the event log to monitor.</span></span>

 <span data-ttu-id="5cb4b-351">부모 요소: [WindowsEventLog 요소](#windowsEventLog)</span><span class="sxs-lookup"><span data-stu-id="5cb4b-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="5cb4b-352">특성:</span><span class="sxs-lookup"><span data-stu-id="5cb4b-352">Attributes:</span></span>

|<span data-ttu-id="5cb4b-353">특성</span><span class="sxs-lookup"><span data-stu-id="5cb4b-353">Attribute</span></span>|<span data-ttu-id="5cb4b-354">형식</span><span class="sxs-lookup"><span data-stu-id="5cb4b-354">Type</span></span>|<span data-ttu-id="5cb4b-355">설명</span><span class="sxs-lookup"><span data-stu-id="5cb4b-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="5cb4b-356">**name**</span><span class="sxs-lookup"><span data-stu-id="5cb4b-356">**name**</span></span>|<span data-ttu-id="5cb4b-357">string</span><span class="sxs-lookup"><span data-stu-id="5cb4b-357">string</span></span>|<span data-ttu-id="5cb4b-358">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-358">Required.</span></span> <span data-ttu-id="5cb4b-359">수집할 로그를 지정하는 XPath 식입니다.</span><span class="sxs-lookup"><span data-stu-id="5cb4b-359">An XPath expression specifying the log to collect.</span></span>|  
