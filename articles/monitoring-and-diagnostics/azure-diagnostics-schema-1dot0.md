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
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="48116-103">Azure 진단 1.0 구성 스키마</span><span class="sxs-lookup"><span data-stu-id="48116-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="48116-104">Azure 진단은 hello 사용 되는 구성 toocollect 성능 카운터 및 Azure 가상 컴퓨터, 가상 컴퓨터 크기 집합, 서비스 패브릭 및 클라우드 서비스에서 기타 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-104">Azure Diagnostics is hello component used toocollect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="48116-105">이 페이지는 이러한 서비스 중 하나를 사용하는 경우에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="48116-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="48116-106">Azure 진단은 Azure Monitor, Application Insights 및 Log Analytics와 같은 기타 Microsoft 진단 제품과 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="48116-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="48116-107">hello Azure 진단 구성 파일 값을 사용 하는 tooinitialize hello 진단 모니터를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-107">hello Azure Diagnostics configuration file defines values that are used tooinitialize hello Diagnostics Monitor.</span></span> <span data-ttu-id="48116-108">이 파일은 hello 진단 모니터를 시작 하는 경우 사용 되는 tooinitialize 진단 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-108">This file is used tooinitialize diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

 <span data-ttu-id="48116-109">기본적으로 hello Azure 진단 구성 스키마 파일은 설치 된 toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-109">By default, hello Azure Diagnostics configuration schema file is installed toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="48116-110">대체 `<version>` hello 설치 된 버전의 hello [Azure SDK](http://www.windowsazure.com/develop/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-110">Replace `<version>` with hello installed version of hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="48116-111">hello 진단 구성 파일은 일반적으로 진단 데이터 toobe hello 시작 프로세스의 앞부분에 나오는 수집 해야 하는 시작 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48116-111">hello diagnostics configuration file is typically used with startup tasks that require diagnostic data toobe collected earlier in hello startup process.</span></span> <span data-ttu-id="48116-112">Azure 진단에 대한 자세한 내용은 [Azure 진단을 사용하여 로깅 데이터 수집](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="48116-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="48116-113">Hello 진단 구성 파일의 예</span><span class="sxs-lookup"><span data-stu-id="48116-113">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="48116-114">다음 예제는 hello 일반적인 진단 구성 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="48116-114">hello following example shows a typical diagnostics configuration file:</span></span>  

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

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="48116-115">DiagnosticsConfiguration 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="48116-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="48116-116">다음은 hello 진단 구성 파일에 대 한 hello XML 네임 스페이스가입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-116">hello XML namespace for hello diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="48116-117">스키마 요소</span><span class="sxs-lookup"><span data-stu-id="48116-117">Schema Elements</span></span>  
 <span data-ttu-id="48116-118">hello 진단 구성 파일에 hello 요소 다음에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48116-118">hello diagnostics configuration file includes hello following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="48116-119">DiagnosticMonitorConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="48116-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="48116-120">hello hello 진단 구성 파일의 최상위 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-120">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="48116-121">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-121">Attributes:</span></span>

|<span data-ttu-id="48116-122">특성</span><span class="sxs-lookup"><span data-stu-id="48116-122">Attribute</span></span>  |<span data-ttu-id="48116-123">유형</span><span class="sxs-lookup"><span data-stu-id="48116-123">Type</span></span>   |<span data-ttu-id="48116-124">필수</span><span class="sxs-lookup"><span data-stu-id="48116-124">Required</span></span>| <span data-ttu-id="48116-125">기본값</span><span class="sxs-lookup"><span data-stu-id="48116-125">Default</span></span> | <span data-ttu-id="48116-126">설명</span><span class="sxs-lookup"><span data-stu-id="48116-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="48116-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="48116-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="48116-128">duration</span><span class="sxs-lookup"><span data-stu-id="48116-128">duration</span></span>|<span data-ttu-id="48116-129">옵션</span><span class="sxs-lookup"><span data-stu-id="48116-129">Optional</span></span> | <span data-ttu-id="48116-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="48116-130">PT1M</span></span>| <span data-ttu-id="48116-131">진단 구성 변경에 대 한 hello 진단 모니터를 폴링하는 간격이 hello를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-131">Specifies hello interval at which hello diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="48116-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48116-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="48116-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48116-133">unsignedInt</span></span>|<span data-ttu-id="48116-134">옵션</span><span class="sxs-lookup"><span data-stu-id="48116-134">Optional</span></span>| <span data-ttu-id="48116-135">4000MB</span><span class="sxs-lookup"><span data-stu-id="48116-135">4000 MB.</span></span> <span data-ttu-id="48116-136">값을 제공하는 경우 이 크기를 초과하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="48116-137">hello 모든 로깅 버퍼에 할당 된 파일 시스템 저장소의 총 양입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-137">hello total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="48116-138">DiagnosticInfrastructureLogs 요소</span><span class="sxs-lookup"><span data-stu-id="48116-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="48116-139">Hello 기본 진단 인프라에서 생성 되는 hello 로그에 대 한 hello 버퍼 구성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-139">Defines hello buffer configuration for hello logs that are generated by hello underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="48116-140">부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48116-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="48116-141">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-141">Attributes:</span></span>

|<span data-ttu-id="48116-142">특성</span><span class="sxs-lookup"><span data-stu-id="48116-142">Attribute</span></span>|<span data-ttu-id="48116-143">형식</span><span class="sxs-lookup"><span data-stu-id="48116-143">Type</span></span>|<span data-ttu-id="48116-144">설명</span><span class="sxs-lookup"><span data-stu-id="48116-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="48116-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48116-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="48116-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48116-146">unsignedInt</span></span>|<span data-ttu-id="48116-147">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-147">Optional.</span></span> <span data-ttu-id="48116-148">Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-148">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="48116-149">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-149">hello default is 0.</span></span>|  
|<span data-ttu-id="48116-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="48116-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="48116-151">string</span><span class="sxs-lookup"><span data-stu-id="48116-151">string</span></span>|<span data-ttu-id="48116-152">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-152">Optional.</span></span> <span data-ttu-id="48116-153">전송 되는 로그 항목에 대 한 hello 최소 심각도 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-153">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="48116-154">hello 기본값은 **Undefined**합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-154">hello default value is **Undefined**.</span></span> <span data-ttu-id="48116-155">사용 가능한 다른 값은 **Verbose**, **Information**, **Warning**, **Error**, 및 **Critical**입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="48116-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="48116-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="48116-157">duration</span><span class="sxs-lookup"><span data-stu-id="48116-157">duration</span></span>|<span data-ttu-id="48116-158">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-158">Optional.</span></span> <span data-ttu-id="48116-159">Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-159">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="48116-160">hello 기본값은 pt0s입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-160">hello default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="48116-161">Logs 요소</span><span class="sxs-lookup"><span data-stu-id="48116-161">Logs Element</span></span>  
 <span data-ttu-id="48116-162">기본 Azure 로그에 대 한 hello 버퍼 구성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-162">Defines hello buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="48116-163">부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48116-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="48116-164">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-164">Attributes:</span></span>  

|<span data-ttu-id="48116-165">특성</span><span class="sxs-lookup"><span data-stu-id="48116-165">Attribute</span></span>|<span data-ttu-id="48116-166">형식</span><span class="sxs-lookup"><span data-stu-id="48116-166">Type</span></span>|<span data-ttu-id="48116-167">설명</span><span class="sxs-lookup"><span data-stu-id="48116-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48116-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="48116-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48116-169">unsignedInt</span></span>|<span data-ttu-id="48116-170">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-170">Optional.</span></span> <span data-ttu-id="48116-171">Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-171">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="48116-172">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-172">hello default is 0.</span></span>|  
|<span data-ttu-id="48116-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="48116-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="48116-174">string</span><span class="sxs-lookup"><span data-stu-id="48116-174">string</span></span>|<span data-ttu-id="48116-175">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-175">Optional.</span></span> <span data-ttu-id="48116-176">전송 되는 로그 항목에 대 한 hello 최소 심각도 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-176">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="48116-177">hello 기본값은 **Undefined**합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-177">hello default value is **Undefined**.</span></span> <span data-ttu-id="48116-178">사용 가능한 다른 값은 **Verbose**, **Information**, **Warning**, **Error**, 및 **Critical**입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="48116-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="48116-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="48116-180">duration</span><span class="sxs-lookup"><span data-stu-id="48116-180">duration</span></span>|<span data-ttu-id="48116-181">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-181">Optional.</span></span> <span data-ttu-id="48116-182">Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-182">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="48116-183">hello 기본값은 pt0s입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-183">hello default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="48116-184">Directories 요소</span><span class="sxs-lookup"><span data-stu-id="48116-184">Directories Element</span></span>  
<span data-ttu-id="48116-185">정의할 수 있는 파일 기반 로그에 대 한 hello 버퍼 구성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-185">Defines hello buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="48116-186">부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48116-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="48116-187">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-187">Attributes:</span></span>  

|<span data-ttu-id="48116-188">특성</span><span class="sxs-lookup"><span data-stu-id="48116-188">Attribute</span></span>|<span data-ttu-id="48116-189">형식</span><span class="sxs-lookup"><span data-stu-id="48116-189">Type</span></span>|<span data-ttu-id="48116-190">설명</span><span class="sxs-lookup"><span data-stu-id="48116-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48116-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="48116-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48116-192">unsignedInt</span></span>|<span data-ttu-id="48116-193">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-193">Optional.</span></span> <span data-ttu-id="48116-194">Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-194">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="48116-195">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-195">hello default is 0.</span></span>|  
|<span data-ttu-id="48116-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="48116-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="48116-197">duration</span><span class="sxs-lookup"><span data-stu-id="48116-197">duration</span></span>|<span data-ttu-id="48116-198">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-198">Optional.</span></span> <span data-ttu-id="48116-199">Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-199">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="48116-200">hello 기본값은 pt0s입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-200">hello default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="48116-201">CrashDumps 요소</span><span class="sxs-lookup"><span data-stu-id="48116-201">CrashDumps Element</span></span>  
 <span data-ttu-id="48116-202">Hello 크래시 덤프 디렉터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-202">Defines hello crash dumps directory.</span></span>

 <span data-ttu-id="48116-203">부모 요소: [Directories 요소](#Directories).</span><span class="sxs-lookup"><span data-stu-id="48116-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="48116-204">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-204">Attributes:</span></span>  

|<span data-ttu-id="48116-205">특성</span><span class="sxs-lookup"><span data-stu-id="48116-205">Attribute</span></span>|<span data-ttu-id="48116-206">형식</span><span class="sxs-lookup"><span data-stu-id="48116-206">Type</span></span>|<span data-ttu-id="48116-207">설명</span><span class="sxs-lookup"><span data-stu-id="48116-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-208">**container**</span><span class="sxs-lookup"><span data-stu-id="48116-208">**container**</span></span>|<span data-ttu-id="48116-209">string</span><span class="sxs-lookup"><span data-stu-id="48116-209">string</span></span>|<span data-ttu-id="48116-210">여기서 hello 디렉터리의 내용을 hello는 toobe hello 컨테이너의 hello 이름을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-210">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="48116-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48116-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="48116-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48116-212">unsignedInt</span></span>|<span data-ttu-id="48116-213">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-213">Optional.</span></span> <span data-ttu-id="48116-214">Hello hello 디렉터리의 최대 크기를 메가바이트 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-214">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="48116-215">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-215">hello default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="48116-216">FailedRequestLogs 요소</span><span class="sxs-lookup"><span data-stu-id="48116-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="48116-217">Hello 실패 한 요청 로그 디렉터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-217">Defines hello failed request log directory.</span></span>

 <span data-ttu-id="48116-218">부모 요소[Directories 요소](#Directories).</span><span class="sxs-lookup"><span data-stu-id="48116-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="48116-219">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-219">Attributes:</span></span>  

|<span data-ttu-id="48116-220">특성</span><span class="sxs-lookup"><span data-stu-id="48116-220">Attribute</span></span>|<span data-ttu-id="48116-221">형식</span><span class="sxs-lookup"><span data-stu-id="48116-221">Type</span></span>|<span data-ttu-id="48116-222">설명</span><span class="sxs-lookup"><span data-stu-id="48116-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-223">**container**</span><span class="sxs-lookup"><span data-stu-id="48116-223">**container**</span></span>|<span data-ttu-id="48116-224">string</span><span class="sxs-lookup"><span data-stu-id="48116-224">string</span></span>|<span data-ttu-id="48116-225">여기서 hello 디렉터리의 내용을 hello는 toobe hello 컨테이너의 hello 이름을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-225">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="48116-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48116-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="48116-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48116-227">unsignedInt</span></span>|<span data-ttu-id="48116-228">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-228">Optional.</span></span> <span data-ttu-id="48116-229">Hello hello 디렉터리의 최대 크기를 메가바이트 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-229">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="48116-230">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-230">hello default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="48116-231">IISLogs 요소</span><span class="sxs-lookup"><span data-stu-id="48116-231">IISLogs Element</span></span>  
 <span data-ttu-id="48116-232">Hello IIS 로그 디렉터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-232">Defines hello IIS log directory.</span></span>

 <span data-ttu-id="48116-233">부모 요소[Directories 요소](#Directories).</span><span class="sxs-lookup"><span data-stu-id="48116-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="48116-234">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-234">Attributes:</span></span>  

|<span data-ttu-id="48116-235">특성</span><span class="sxs-lookup"><span data-stu-id="48116-235">Attribute</span></span>|<span data-ttu-id="48116-236">형식</span><span class="sxs-lookup"><span data-stu-id="48116-236">Type</span></span>|<span data-ttu-id="48116-237">설명</span><span class="sxs-lookup"><span data-stu-id="48116-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-238">**container**</span><span class="sxs-lookup"><span data-stu-id="48116-238">**container**</span></span>|<span data-ttu-id="48116-239">string</span><span class="sxs-lookup"><span data-stu-id="48116-239">string</span></span>|<span data-ttu-id="48116-240">여기서 hello 디렉터리의 내용을 hello는 toobe hello 컨테이너의 hello 이름을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-240">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="48116-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48116-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="48116-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48116-242">unsignedInt</span></span>|<span data-ttu-id="48116-243">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-243">Optional.</span></span> <span data-ttu-id="48116-244">Hello hello 디렉터리의 최대 크기를 메가바이트 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-244">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="48116-245">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-245">hello default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="48116-246">DataSources 요소</span><span class="sxs-lookup"><span data-stu-id="48116-246">DataSources Element</span></span>  
 <span data-ttu-id="48116-247">0개 이상의 추가 로그 디렉터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="48116-248">부모 요소: [Directories 요소](#Directories).</span><span class="sxs-lookup"><span data-stu-id="48116-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="48116-249">DirectoryConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="48116-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="48116-250">로그 파일 toomonitor의 hello 디렉터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-250">Defines hello directory of log files toomonitor.</span></span>

 <span data-ttu-id="48116-251">부모 요소: [DataSources 요소](#DataSources)</span><span class="sxs-lookup"><span data-stu-id="48116-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="48116-252">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-252">Attributes:</span></span>

|<span data-ttu-id="48116-253">특성</span><span class="sxs-lookup"><span data-stu-id="48116-253">Attribute</span></span>|<span data-ttu-id="48116-254">형식</span><span class="sxs-lookup"><span data-stu-id="48116-254">Type</span></span>|<span data-ttu-id="48116-255">설명</span><span class="sxs-lookup"><span data-stu-id="48116-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-256">**container**</span><span class="sxs-lookup"><span data-stu-id="48116-256">**container**</span></span>|<span data-ttu-id="48116-257">string</span><span class="sxs-lookup"><span data-stu-id="48116-257">string</span></span>|<span data-ttu-id="48116-258">여기서 hello 디렉터리의 내용을 hello는 toobe hello 컨테이너의 hello 이름을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-258">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="48116-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48116-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="48116-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48116-260">unsignedInt</span></span>|<span data-ttu-id="48116-261">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-261">Optional.</span></span> <span data-ttu-id="48116-262">Hello hello 디렉터리의 최대 크기를 메가바이트 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-262">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="48116-263">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-263">hello default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="48116-264">Absolute 요소</span><span class="sxs-lookup"><span data-stu-id="48116-264">Absolute Element</span></span>  
 <span data-ttu-id="48116-265">선택적 환경 확장으로 hello 디렉터리 toomonitor의 절대 경로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-265">Defines an absolute path of hello directory toomonitor with optional environment expansion.</span></span>

 <span data-ttu-id="48116-266">부모 요소: [DirectoryConfiguration 요소](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48116-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="48116-267">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-267">Attributes:</span></span>  

|<span data-ttu-id="48116-268">특성</span><span class="sxs-lookup"><span data-stu-id="48116-268">Attribute</span></span>|<span data-ttu-id="48116-269">형식</span><span class="sxs-lookup"><span data-stu-id="48116-269">Type</span></span>|<span data-ttu-id="48116-270">설명</span><span class="sxs-lookup"><span data-stu-id="48116-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-271">**path**</span><span class="sxs-lookup"><span data-stu-id="48116-271">**path**</span></span>|<span data-ttu-id="48116-272">string</span><span class="sxs-lookup"><span data-stu-id="48116-272">string</span></span>|<span data-ttu-id="48116-273">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-273">Required.</span></span> <span data-ttu-id="48116-274">hello toohello 디렉터리 toomonitor 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-274">hello absolute path toohello directory toomonitor.</span></span>|  
|<span data-ttu-id="48116-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="48116-275">**expandEnvironment**</span></span>|<span data-ttu-id="48116-276">부울</span><span class="sxs-lookup"><span data-stu-id="48116-276">boolean</span></span>|<span data-ttu-id="48116-277">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-277">Required.</span></span> <span data-ttu-id="48116-278">경우 너무 설정**true**, hello 경로에 환경 변수 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48116-278">If set too**true**, environment variables in hello path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="48116-279">LocalResource 요소</span><span class="sxs-lookup"><span data-stu-id="48116-279">LocalResource Element</span></span>  
 <span data-ttu-id="48116-280">Hello 서비스 정의에 지정 된 경로 상대 tooa 로컬 리소스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-280">Defines a path relative tooa local resource defined in hello service definition.</span></span>

 <span data-ttu-id="48116-281">부모 요소: [DirectoryConfiguration 요소](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48116-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="48116-282">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-282">Attributes:</span></span>  

|<span data-ttu-id="48116-283">특성</span><span class="sxs-lookup"><span data-stu-id="48116-283">Attribute</span></span>|<span data-ttu-id="48116-284">형식</span><span class="sxs-lookup"><span data-stu-id="48116-284">Type</span></span>|<span data-ttu-id="48116-285">설명</span><span class="sxs-lookup"><span data-stu-id="48116-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-286">**name**</span><span class="sxs-lookup"><span data-stu-id="48116-286">**name**</span></span>|<span data-ttu-id="48116-287">string</span><span class="sxs-lookup"><span data-stu-id="48116-287">string</span></span>|<span data-ttu-id="48116-288">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-288">Required.</span></span> <span data-ttu-id="48116-289">hello 디렉터리 toomonitor를 포함 하는 hello 로컬 리소스의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-289">hello name of hello local resource that contains hello directory toomonitor.</span></span>|  
|<span data-ttu-id="48116-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="48116-290">**relativePath**</span></span>|<span data-ttu-id="48116-291">string</span><span class="sxs-lookup"><span data-stu-id="48116-291">string</span></span>|<span data-ttu-id="48116-292">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-292">Required.</span></span> <span data-ttu-id="48116-293">hello 경로 상대 toohello 로컬 리소스 toomonitor 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-293">hello path relative toohello local resource toomonitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="48116-294">PerformanceCounters 요소</span><span class="sxs-lookup"><span data-stu-id="48116-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="48116-295">Hello 경로 toohello 성능 카운터 toocollect를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-295">Defines hello path toohello performance counter toocollect.</span></span>

 <span data-ttu-id="48116-296">부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48116-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="48116-297">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-297">Attributes:</span></span>  

|<span data-ttu-id="48116-298">특성</span><span class="sxs-lookup"><span data-stu-id="48116-298">Attribute</span></span>|<span data-ttu-id="48116-299">형식</span><span class="sxs-lookup"><span data-stu-id="48116-299">Type</span></span>|<span data-ttu-id="48116-300">설명</span><span class="sxs-lookup"><span data-stu-id="48116-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48116-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="48116-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48116-302">unsignedInt</span></span>|<span data-ttu-id="48116-303">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-303">Optional.</span></span> <span data-ttu-id="48116-304">Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-304">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="48116-305">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-305">hello default is 0.</span></span>|  
|<span data-ttu-id="48116-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="48116-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="48116-307">duration</span><span class="sxs-lookup"><span data-stu-id="48116-307">duration</span></span>|<span data-ttu-id="48116-308">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-308">Optional.</span></span> <span data-ttu-id="48116-309">Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-309">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="48116-310">hello 기본값은 pt0s입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-310">hello default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="48116-311">PerformanceCounterConfiguration 요소</span><span class="sxs-lookup"><span data-stu-id="48116-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="48116-312">성능 카운터 toocollect hello를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-312">Defines hello performance counter toocollect.</span></span>

 <span data-ttu-id="48116-313">부모 요소: [PerformanceCounters 요소](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="48116-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="48116-314">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-314">Attributes:</span></span>  

|<span data-ttu-id="48116-315">특성</span><span class="sxs-lookup"><span data-stu-id="48116-315">Attribute</span></span>|<span data-ttu-id="48116-316">형식</span><span class="sxs-lookup"><span data-stu-id="48116-316">Type</span></span>|<span data-ttu-id="48116-317">설명</span><span class="sxs-lookup"><span data-stu-id="48116-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="48116-318">**counterSpecifier**</span></span>|<span data-ttu-id="48116-319">string</span><span class="sxs-lookup"><span data-stu-id="48116-319">string</span></span>|<span data-ttu-id="48116-320">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-320">Required.</span></span> <span data-ttu-id="48116-321">hello 경로 toohello 성능 카운터 toocollect 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-321">hello path toohello performance counter toocollect.</span></span>|  
|<span data-ttu-id="48116-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="48116-322">**sampleRate**</span></span>|<span data-ttu-id="48116-323">duration</span><span class="sxs-lookup"><span data-stu-id="48116-323">duration</span></span>|<span data-ttu-id="48116-324">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-324">Required.</span></span> <span data-ttu-id="48116-325">hello 속도 hello에서 성능 카운터를 수집 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-325">hello rate at which hello performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="48116-326">WindowsEventLog 요소</span><span class="sxs-lookup"><span data-stu-id="48116-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="48116-327">이벤트 로그 toomonitor hello를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-327">Defines hello event logs toomonitor.</span></span>

 <span data-ttu-id="48116-328">부모 요소: [DiagnosticMonitorConfiguration 요소](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48116-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="48116-329">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-329">Attributes:</span></span>

|<span data-ttu-id="48116-330">특성</span><span class="sxs-lookup"><span data-stu-id="48116-330">Attribute</span></span>|<span data-ttu-id="48116-331">형식</span><span class="sxs-lookup"><span data-stu-id="48116-331">Type</span></span>|<span data-ttu-id="48116-332">설명</span><span class="sxs-lookup"><span data-stu-id="48116-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48116-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="48116-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48116-334">unsignedInt</span></span>|<span data-ttu-id="48116-335">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-335">Optional.</span></span> <span data-ttu-id="48116-336">Hello hello 지정에 사용할 수 있는 파일 시스템 저장소의 최대 크기를 지정 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-336">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="48116-337">hello 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-337">hello default is 0.</span></span>|  
|<span data-ttu-id="48116-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="48116-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="48116-339">string</span><span class="sxs-lookup"><span data-stu-id="48116-339">string</span></span>|<span data-ttu-id="48116-340">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-340">Optional.</span></span> <span data-ttu-id="48116-341">전송 되는 로그 항목에 대 한 hello 최소 심각도 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-341">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="48116-342">hello 기본값은 **Undefined**합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-342">hello default value is **Undefined**.</span></span> <span data-ttu-id="48116-343">사용 가능한 다른 값은 **Verbose**, **Information**, **Warning**, **Error**, 및 **Critical**입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="48116-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="48116-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="48116-345">duration</span><span class="sxs-lookup"><span data-stu-id="48116-345">duration</span></span>|<span data-ttu-id="48116-346">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-346">Optional.</span></span> <span data-ttu-id="48116-347">Hello toohello 가장 근접 한 분을 반올림 하는 데이터의 예약 된 전송 간격을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-347">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="48116-348">hello 기본값은 pt0s입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-348">hello default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="48116-349">DataSource 요소</span><span class="sxs-lookup"><span data-stu-id="48116-349">DataSource Element</span></span>  
 <span data-ttu-id="48116-350">이벤트 로그 toomonitor hello를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="48116-350">Defines hello event log toomonitor.</span></span>

 <span data-ttu-id="48116-351">부모 요소: [WindowsEventLog 요소](#windowsEventLog)</span><span class="sxs-lookup"><span data-stu-id="48116-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="48116-352">특성:</span><span class="sxs-lookup"><span data-stu-id="48116-352">Attributes:</span></span>

|<span data-ttu-id="48116-353">특성</span><span class="sxs-lookup"><span data-stu-id="48116-353">Attribute</span></span>|<span data-ttu-id="48116-354">형식</span><span class="sxs-lookup"><span data-stu-id="48116-354">Type</span></span>|<span data-ttu-id="48116-355">설명</span><span class="sxs-lookup"><span data-stu-id="48116-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48116-356">**name**</span><span class="sxs-lookup"><span data-stu-id="48116-356">**name**</span></span>|<span data-ttu-id="48116-357">string</span><span class="sxs-lookup"><span data-stu-id="48116-357">string</span></span>|<span data-ttu-id="48116-358">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-358">Required.</span></span> <span data-ttu-id="48116-359">Hello 로그 toocollect를 지정 하는 XPath 식입니다.</span><span class="sxs-lookup"><span data-stu-id="48116-359">An XPath expression specifying hello log toocollect.</span></span>|  
