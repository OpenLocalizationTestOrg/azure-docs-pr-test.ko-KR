---
title: "Cloud Services에서 Azure 진단(.NET)을 사용하는 방법 | Microsoft Docs"
description: "Azure 진단을 사용하면 디버깅, 성능 측정, 모니터링, 트래픽 분석 등을 위해 Azure Cloud Services에서 데이터를 수집할 수 있습니다."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 333d2f26ce043a167fb84858c8327cb39e868ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="32513-103">Azure Cloud Services에서 Azure 진단 사용</span><span class="sxs-lookup"><span data-stu-id="32513-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="32513-104">Azure 진단의 배경은 [Azure 진단 개요](../azure-diagnostics.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32513-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-worker-role"></a><span data-ttu-id="32513-105">작업자 역할에서 진단을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="32513-105">How to Enable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="32513-106">이 연습에서는 .NET EventSource 클래스를 사용하여 원격 분석 데이터를 내보내는 Azure 작업자 역할을 구현하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-106">This walkthrough describes how to implement an Azure worker role that emits telemetry data using the .NET EventSource class.</span></span> <span data-ttu-id="32513-107">Azure 진단은 원격 분석 데이터를 수집하고 이를 Azure Storage 계정에 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-107">Azure Diagnostics is used to collect the telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="32513-108">Visual Studio 작업자 역할을 만드는 경우 Azure .NET SDK 2.4 이상 버전에서 진단 1.0을 솔루션의 일부로 자동으로 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of the solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="32513-109">다음 지침에서는 작업자 역할을 만들고, 솔루션에서 진단 1.0을 사용하지 않도록 설정하고, 진단 1.2 또는 1.3을 작업자 역할에 배포하기 위한 프로세스에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-109">The following instructions describe the process for creating the worker role, disabling Diagnostics 1.0 from the solution, and deploying Diagnostics 1.2 or 1.3 to your worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="32513-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="32513-110">Prerequisites</span></span>
<span data-ttu-id="32513-111">이 문서에서는 Azure 구독이 있으며 Visual Studio와 Azure SDK를 함께 사용 중인 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-111">This article assumes you have an Azure subscription and are using Visual Studio with the Azure SDK.</span></span> <span data-ttu-id="32513-112">Azure 구독이 없는 경우 [무료 평가판][Free Trial]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32513-112">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="32513-113">[Azure PowerShell 버전 0.8.7 이상을 설치 및 구성][Install and configure Azure PowerShell version 0.8.7 or later]해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-113">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="32513-114">1단계: 작업자 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="32513-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="32513-115">**Visual Studio**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="32513-116">.NET Framework 4.5를 대상으로 하는 **Cloud** 템플릿에서 **Azure Cloud Service** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32513-116">Create an **Azure Cloud Service** project from the **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="32513-117">프로젝트의 이름을 "WadExample"로 지정하고 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-117">Name the project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="32513-118">**작업자 역할**을 선택하고 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="32513-119">프로젝트가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="32513-119">The project will be created.</span></span>
4. <span data-ttu-id="32513-120">**솔루션 탐색기**에서 **WorkerRole1** 속성 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-120">In **Solution Explorer**, double-click the **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="32513-121">**구성** 탭에서 **진단 사용**을 선택 취소하여 진단 1.0을 사용하지 않도록 설정합니다(Azure SDK 2.4 이전 버전).</span><span class="sxs-lookup"><span data-stu-id="32513-121">In the **Configuration** tab, un-check **Enable Diagnostics** to disable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="32513-122">솔루션을 빌드하여 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-122">Build your solution to verify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="32513-123">2단계: 코드 계측</span><span class="sxs-lookup"><span data-stu-id="32513-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="32513-124">WorkerRole.cs 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="32513-124">Replace the contents of WorkerRole.cs with the following code.</span></span> <span data-ttu-id="32513-125">[EventSource 클래스][EventSource Class]로부터 상속되는 SampleEventSourceWriter 클래스는 다음 4개의 로깅 메서드를 구현합니다. **SendEnums**, **MessageMethod**, **SetOther** 및 **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="32513-125">The class SampleEventSourceWriter, inherited from the [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="32513-126">**WriteEvent** 메서드에 대한 첫 번째 매개 변수는 각 이벤트의 ID를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-126">The first parameter to the **WriteEvent** method defines the ID for the respective event.</span></span> <span data-ttu-id="32513-127">Run 메서드는 **SampleEventSourceWriter** 클래스에 구현된 각각의 로깅 메서드를 10초마다 호출하는 무한 루프를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-127">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums to int for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through the loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set the maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="32513-128">3단계: 작업자 역할 배포</span><span class="sxs-lookup"><span data-stu-id="32513-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="32513-129">솔루션 Explorer에서 **WadExample** 프로젝트를 선택한 후 **빌드** 메뉴에서 **게시**를 선택하여 Visual Studio 내에서 Azure에 작업자 역할을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-129">Deploy your worker role to Azure from within Visual Studio by selecting the **WadExample** project in the Solution Explorer then **Publish** from the **Build** menu.</span></span>
2. <span data-ttu-id="32513-130">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-130">Choose your subscription.</span></span>
3. <span data-ttu-id="32513-131">**Microsoft Azure 게시 설정** 대화 상자에서 **새로 만들기...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-131">In the **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="32513-132">**클라우드 서비스 및 저장소 계정 만들기** 대화 상자에서 **이름**(예: "WadExample")을 입력하고 지역 또는 선호도 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-132">In the **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="32513-133">**환경**을 **스테이징**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-133">Set the **Environment** to **Staging**.</span></span>
6. <span data-ttu-id="32513-134">다른 **설정**을 적절히 수정하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="32513-135">배포가 완료되면 Azure Portal에서 클라우드 서비스가 **실행 중** 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-135">After deployment has completed, verify in the Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-the-extension"></a><span data-ttu-id="32513-136">4단계: 진단 구성 파일 만들기 및 확장 설치</span><span class="sxs-lookup"><span data-stu-id="32513-136">Step 4: Create your Diagnostics configuration file and install the extension</span></span>
1. <span data-ttu-id="32513-137">다음 PowerShell 명령을 실행하여 공용 구성 파일 스키마 정의를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-137">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="32513-138">XML 파일을 추가 하면 **WorkerRole1** 마우스 오른쪽 단추로 클릭 하 여 프로젝트는 **WorkerRole1** 프로젝트를 마우스 선택 **추가** -> **새 항목...**</span><span class="sxs-lookup"><span data-stu-id="32513-138">Add an XML file to your **WorkerRole1** project by right-clicking on the **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="32513-139"> -> **Visual C# 항목** -> **데이터** -> **XML 파일**.</span><span class="sxs-lookup"><span data-stu-id="32513-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="32513-140">파일 이름을 “WadExample.xml”로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-140">Name the file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="32513-142">WadConfig.xsd를 구성 파일과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-142">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="32513-143">WadExample.xml 편집기 창이 활성 창인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-143">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="32513-144">**F4**를 눌러 **속성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32513-144">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="32513-145">**속성** 창에서 **Schemas** 속성을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-145">Click the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="32513-146">**Schemas** 속성에서</span><span class="sxs-lookup"><span data-stu-id="32513-146">Click the **…**</span></span> <span data-ttu-id="32513-147">**...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-147">in the **Schemas** property.</span></span> <span data-ttu-id="32513-148">**추가...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-148">Click the **Add…**</span></span> <span data-ttu-id="32513-149">단추를 클릭하고 XSD 파일을 저장한 위치로 이동한 후 WadConfig.xsd 파일을 선택하고</span><span class="sxs-lookup"><span data-stu-id="32513-149">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="32513-150">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-150">Click **OK**.</span></span>

4. <span data-ttu-id="32513-151">WadExample.xml 구성 파일의 내용을 다음 XML로 바꾸고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-151">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="32513-152">이 구성 파일은 각각 CPU 사용률 및 메모리 사용률을 수집할 두 가지 성능 카운터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-152">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="32513-153">그런 다음 이 구성에서는 SampleEventSourceWriter 클래스의 메서드에 해당하는 네 개의 이벤트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-153">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="32513-154">5단계: 작업자 역할에 진단 설치</span><span class="sxs-lookup"><span data-stu-id="32513-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="32513-155">웹 또는 작업자 역할에서 진단을 관리하는 데 사용되는 PowerShell cmdlet은 Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension 및 Remove-AzureServiceDiagnosticsExtension입니다.</span><span class="sxs-lookup"><span data-stu-id="32513-155">The PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="32513-156">Azure PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="32513-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="32513-157">작업자 역할에 진단을 설치하기 위한 스크립트를 실행합니다(*StorageAccountKey*를 wadexample 저장소 계정의 저장소 계정 키로 바꾸고 *config_path*를 *WadExample.xml* 파일에 대한 경로로 바꿈).</span><span class="sxs-lookup"><span data-stu-id="32513-157">Execute the script to install Diagnostics on your worker role (replace *StorageAccountKey* with the storage account key for your wadexample storage account and *config_path* with the path to the *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="32513-158">6단계: 원격 분석 데이터 확인</span><span class="sxs-lookup"><span data-stu-id="32513-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="32513-159">Visual Studio **서버 탐색기**에서 wadexample 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-159">In the Visual Studio **Server Explorer**, navigate to the wadexample storage account.</span></span> <span data-ttu-id="32513-160">클라우드 서비스가 5분 정도 실행된 후에는 **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** 및 **WADSetOtherTable** 테이블이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32513-160">After the cloud service has been running about five (5) minutes, you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="32513-161">수집된 원격 분석을 보려는 테이블 중 하나를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-161">Double-click one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="32513-163">구성 파일 스키마</span><span class="sxs-lookup"><span data-stu-id="32513-163">Configuration File Schema</span></span>
<span data-ttu-id="32513-164">진단 구성 파일에서는 진단 에이전트가 시작될 때 진단 구성 설정을 초기화하는 데 사용되는 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="32513-164">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="32513-165">유효한 값 및 예제는 [최신 스키마 참조](https://msdn.microsoft.com/library/azure/mt634524.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32513-165">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="32513-166">문제 해결</span><span class="sxs-lookup"><span data-stu-id="32513-166">Troubleshooting</span></span>
<span data-ttu-id="32513-167">문제가 있는 경우 일반적인 문제에 대한 도움말인 [Azure 진단 문제 해결](../azure-diagnostics-troubleshooting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32513-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32513-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32513-168">Next Steps</span></span>
<span data-ttu-id="32513-169">수집한 데이터를 변경하거나 문제를 해결하거나 일반적인 진단에 대해 자세히 알아보려면 [관련된 Azure Virtual Machine 진단 문서 목록을 참조하세요](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="32513-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
