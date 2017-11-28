---
title: "가상 컴퓨터에서 Azure 진단을 사용하는 방법 | Microsoft Docs"
description: "Azure 진단을 사용하여 디버깅, 성능 측정, 모니터링, 트래픽 분석 등에 대해 Azure 가상 컴퓨터에서 데이터를 수집합니다."
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 8ff6b9825212359617b748aba1c78ed789b130dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="b942b-103">Azure 가상 컴퓨터에서 진단 사용</span><span class="sxs-lookup"><span data-stu-id="b942b-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="b942b-104">Azure 진단의 배경은 [Azure 진단 개요](../monitoring-and-diagnostics/azure-diagnostics.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b942b-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="b942b-105">가상 컴퓨터에서 진단을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b942b-105">How to Enable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="b942b-106">이 연습에서는 개발 컴퓨터에서 Azure 가상 컴퓨터로 진단을 원격으로 설치하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-106">This walk through describes how to remotely install Diagnostics to an Azure virtual machine from a development computer.</span></span> <span data-ttu-id="b942b-107">또한 Azure 가상 컴퓨터에서 실행되고 .NET [EventSource 클래스][EventSource Class]를 사용하여 원격 분석 데이터를 내보내는 응용 프로그램을 구현하는 방법도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-107">You also learn how to implement an application that runs on that Azure virtual machine and emits telemetry data using the .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="b942b-108">Azure 진단은 원격 분석 데이터를 수집하고 이를 Azure Storage 계정에 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-108">Azure Diagnostics is used to collect the telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="b942b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b942b-109">Pre-requisites</span></span>
<span data-ttu-id="b942b-110">이 연습에서는 Azure 구독이 있으며 Visual Studio 2017과 Azure SDK를 함께 사용 중인 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with the Azure SDK.</span></span> <span data-ttu-id="b942b-111">Azure 구독이 없는 경우 [무료 평가판][Free Trial]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-111">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="b942b-112">[Azure PowerShell 버전 0.8.7 이상을 설치 및 구성][Install and configure Azure PowerShell version 0.8.7 or later]해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-112">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="b942b-113">1단계: 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="b942b-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="b942b-114">개발 컴퓨터에서 Visual Studio 2017을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="b942b-115">Visual Studio **서버 Explorer**에서 **Azure**를 확장하고 **가상 컴퓨터**를 마우스 오른쪽 단추로 클릭한 다음 **가상 컴퓨터 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-115">In the Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="b942b-116">**구독 선택** 대화 상자에서 Azure 구독을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-116">Select your Azure subscription in the **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="b942b-117">**가상 컴퓨터 이미지 선택** 대화 상자에서 **Windows Server 2012 R2 Datacenter, June 2017**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in the **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="b942b-118">**가상 컴퓨터 기본 설정**에서 가상 컴퓨터 이름을 "wadexample"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-118">In the **Virtual Machine Basic Settings**, set the virtual machine name to "wadexample".</span></span> <span data-ttu-id="b942b-119">관리자 사용자 이름과 암호를 설정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="b942b-120">**클라우드 서비스 설정** 대화 상자에서 "wadexampleVM"이라는 새 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-120">In the **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="b942b-121">"wadexample"이라는 새 저장소 계정을 만들고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="b942b-122">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="b942b-123">2단계: 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b942b-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="b942b-124">개발 컴퓨터에서 Visual Studio 2017을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="b942b-125">.NET Framework 4.5를 대상으로 하는 새 Visual C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="b942b-126">프로젝트의 이름을 "WadExampleVM"으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-126">Name the project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="b942b-128">Program.cs 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-128">Replace the contents of Program.cs with the following code.</span></span> <span data-ttu-id="b942b-129">**SampleEventSourceWriter** 클래스는 다음 4개의 로깅 메서드를 구현합니다. **SendEnums**, **MessageMethod**, **SetOther** 및 **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="b942b-129">The class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="b942b-130">WriteEvent 메서드에 대한 첫 번째 매개 변수는 각 이벤트의 ID를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-130">The first parameter to the WriteEvent method defines the ID for the respective event.</span></span> <span data-ttu-id="b942b-131">Run 메서드는 **SampleEventSourceWriter** 클래스에 구현된 각각의 로깅 메서드를 10초마다 호출하는 무한 루프를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-131">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums to int for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through the loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. <span data-ttu-id="b942b-132">파일을 저장하고 **빌드** 메뉴에서 **솔루션 빌드**를 선택하여 코드를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-132">Save the file and select **Build Solution** from the **Build** menu to build your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="b942b-133">3단계: 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="b942b-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="b942b-134">**솔루션 Explorer**에서 **WadExampleVM** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **파일 Explorer에서 폴더 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-134">Right-click on the **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="b942b-135">*bin\Debug* 폴더로 이동하고 모든 파일을 복사합니다(WadExampleVM.*).</span><span class="sxs-lookup"><span data-stu-id="b942b-135">Navigate to the *bin\Debug* folder and copy all the files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="b942b-136">**서버 Explorer**에서 가상 컴퓨터를 마우스 오른쪽 단추로 클릭하고 **원격 데스크톱을 사용하여 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-136">In **Server Explorer** right-click on the virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="b942b-137">VM에 연결되면 WadExampleVM이라는 폴더를 만들고 응용 프로그램 파일을 폴더에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-137">Once connected to the VM create a folder named WadExampleVM and paste your application files into the folder.</span></span>
5. <span data-ttu-id="b942b-138">WadExampleVM.exe 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-138">Launch the application WadExampleVM.exe.</span></span> <span data-ttu-id="b942b-139">빈 콘솔 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-the-extension"></a><span data-ttu-id="b942b-140">4단계: 진단 구성 만들기 및 확장 설치</span><span class="sxs-lookup"><span data-stu-id="b942b-140">Step 4: Create your Diagnostics configuration and install the Extension</span></span>
1. <span data-ttu-id="b942b-141">다음 PowerShell 명령을 실행하여 공용 구성 파일 스키마 정의를 개발 컴퓨터로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-141">Download the public configuration file schema definition to your development computer by executing the following PowerShell command:</span></span>

     <span data-ttu-id="b942b-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="b942b-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="b942b-143">Visual Studio에서 새 XML 파일을 엽니다. 이미 열려 있는 프로젝트에서 새로 열거나 열려 있는 프로젝트가 없는 Visual Studio 인스턴스에서 열면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="b942b-144">Visual Studio에서 **추가** -> **새 항목...**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="b942b-145"> -> **Visual C# 항목** -> **데이터** -> **XML 파일**.</span><span class="sxs-lookup"><span data-stu-id="b942b-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="b942b-146">파일 이름을 “WadExample.xml”로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-146">Name the file "WadExample.xml"</span></span>
3. <span data-ttu-id="b942b-147">WadConfig.xsd를 구성 파일과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-147">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="b942b-148">WadExample.xml 편집기 창이 활성 창인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-148">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="b942b-149">**F4**를 눌러 **속성** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-149">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="b942b-150">**속성** 창에서 **Schemas** 속성을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-150">Click on the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="b942b-151">**Schemas** 속성에서</span><span class="sxs-lookup"><span data-stu-id="b942b-151">Click the **…**</span></span> <span data-ttu-id="b942b-152">**...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-152">in the **Schemas** property.</span></span> <span data-ttu-id="b942b-153">**추가...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-153">Click the **Add…**</span></span> <span data-ttu-id="b942b-154">단추를 클릭하고 XSD 파일을 저장한 위치로 이동한 후 WadConfig.xsd 파일을 선택하고</span><span class="sxs-lookup"><span data-stu-id="b942b-154">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="b942b-155">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-155">Click **OK**.</span></span>
4. <span data-ttu-id="b942b-156">WadExample.xml 구성 파일의 내용을 다음 XML로 바꾸고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-156">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="b942b-157">이 구성 파일은 각각 CPU 사용률 및 메모리 사용률을 수집할 두 가지 성능 카운터를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-157">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="b942b-158">그런 다음 이 구성에서는 SampleEventSourceWriter 클래스의 메서드에 해당하는 네 개의 이벤트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-158">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="b942b-159">5단계: Azure 가상 컴퓨터에 원격으로 진단 설치</span><span class="sxs-lookup"><span data-stu-id="b942b-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="b942b-160">VM에서 진단을 관리하는 데 사용되는 PowerShell cmdlet은 Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension 및 Remove-AzureVMDiagnosticsExtension입니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-160">The PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="b942b-161">개발자 컴퓨터에서 Azure PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="b942b-162">VM에 원격으로 진단 기능을 설치하기 위한 스크립트를 실행합니다(`<user>`를 사용자 디렉터리 이름으로 바꿈).</span><span class="sxs-lookup"><span data-stu-id="b942b-162">Execute the script to remotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="b942b-163">`<StorageAccountKey>`를 wadexamplevm 저장소 계정에 대한 저장소 계정 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-163">Replace `<StorageAccountKey>` with the storage account key for your wadexamplevm storage account):</span></span>
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="b942b-164">6단계: 원격 분석 데이터 확인</span><span class="sxs-lookup"><span data-stu-id="b942b-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="b942b-165">Visual Studio **서버 Explorer**에서 wadexample 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-165">In the Visual Studio **Server Explorer** navigate to the wadexample storage account.</span></span> <span data-ttu-id="b942b-166">VM이 5분 정도 실행된 후에는 **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** 및 **WADSetOtherTable** 테이블이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-166">After the VM has been running about 5 minutes you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="b942b-167">수집된 원격 분석을 보려는 테이블 중 하나를 더블 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-167">Double-click on one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="b942b-169">구성 파일 스키마</span><span class="sxs-lookup"><span data-stu-id="b942b-169">Configuration file schema</span></span>
<span data-ttu-id="b942b-170">진단 구성 파일에서는 진단 에이전트가 시작될 때 진단 구성 설정을 초기화하는 데 사용되는 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b942b-170">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="b942b-171">유효한 값 및 예제는 [최신 스키마 참조](https://msdn.microsoft.com/library/azure/mt634524.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b942b-171">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b942b-172">문제 해결</span><span class="sxs-lookup"><span data-stu-id="b942b-172">Troubleshooting</span></span>
<span data-ttu-id="b942b-173">자세한 내용은 [Azure 진단 문제 해결](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b942b-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b942b-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b942b-174">Next steps</span></span>
<span data-ttu-id="b942b-175">수집한 데이터를 변경하거나 문제를 해결하거나 일반적인 진단에 대해 자세히 알아보려면 [가상 컴퓨터 관련 Azure 진단 문서 목록](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b942b-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
