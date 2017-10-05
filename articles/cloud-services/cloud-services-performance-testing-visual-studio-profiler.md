---
title: "계산 에뮬레이터에서 로컬로 클라우드 서비스 프로파일링 | Microsoft Docs"
services: cloud-services
description: "Visual Studio 프로파일러를 사용하여 클라우드 서비스의 성능 문제를 조사합니다."
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 51c8192d8312dc5cf546b4c357aeecf6f19d56b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="testing-the-performance-of-a-cloud-service-locally-in-the-azure-compute-emulator-using-the-visual-studio-profiler"></a><span data-ttu-id="52125-103">Visual Studio 프로파일러를 사용하여 Azure 계산 에뮬레이터에서 로컬로 클라우드 서비스의 성능 테스트</span><span class="sxs-lookup"><span data-stu-id="52125-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span></span>
<span data-ttu-id="52125-104">다양한 도구와 기법을 사용하여 클라우드 서비스의 성능을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-104">A variety of tools and techniques are available for testing the performance of cloud services.</span></span>
<span data-ttu-id="52125-105">클라우드 서비스를 Azure에 게시할 때 [Azure 응용 프로그램 프로파일링][1]에 설명된 대로 Visual Studio에서 프로파일링 데이터를 수집하고 로컬에서 분석하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="52125-106">[Azure에서 성능 카운터 사용][2]에 설명된 대로 진단을 사용하여 다양한 성능 카운터를 추적할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="52125-107">또한 클라우드에 배포하기 전에 계산 에뮬레이터에서 로컬로 응용 프로그램을 프로파일링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span></span>

<span data-ttu-id="52125-108">이 문서에서는 에뮬레이터를 통해 로컬로 수행할 수 있는 CPU 샘플링 프로파일링 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="52125-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span></span> <span data-ttu-id="52125-109">CPU 샘플링은 주입식이 아닌 프로파일링 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="52125-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="52125-110">지정된 샘플링 간격마다 프로파일러가 호출 스택의 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52125-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span></span> <span data-ttu-id="52125-111">정해진 기간 동안 데이터가 수집되어 보고서에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="52125-111">The data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="52125-112">이 프로파일링 방법은 계산이 많은 응용 프로그램에서 대부분의 CPU 작업이 수행되는 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="52125-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span></span>  <span data-ttu-id="52125-113">이 정보를 통해 응용 프로그램이 대부분의 시간을 보내는 "실행 부하 과다 경로"에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="52125-114">1: 프로파일링을 위해 Visual Studio 구성</span><span class="sxs-lookup"><span data-stu-id="52125-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="52125-115">먼저 프로파일링 시 유용할 수 있는 몇 가지 Visual Studio 구성 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="52125-116">프로파일링 보고서를 이해하려면 응용 프로그램용 기호(.pdb 파일) 및 시스템 라이브러리용 기호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="52125-117">사용 가능한 기호 서버를 참조하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-117">You'll want to make sure that you reference the available symbol servers.</span></span> <span data-ttu-id="52125-118">Visual Studio의 **도구** 메뉴에서 **옵션**, **디버깅**, **기호**를 차례로 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52125-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="52125-119">Microsoft 기호 서버가 **기호 파일(.pdb) 위치**아래에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="52125-120">추가 기호 파일이 있는 http://referencesource.microsoft.com/symbols를 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![기호 옵션][4]

<span data-ttu-id="52125-122">원하는 경우 내 코드만을 설정하여 프로파일러가 생성하는 보고서를 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span></span> <span data-ttu-id="52125-123">내 코드만을 사용하도록 설정하면 함수 호출 스택이 간소화되므로 라이브러리 및 .NET Framework 내부에 제한된 호출은 보고서에서 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="52125-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span></span> <span data-ttu-id="52125-124">**도구** 메뉴에서 **옵션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-124">On the **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="52125-125">**성능 도구** 노드를 확장하고 **일반**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-125">Then expand the **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="52125-126">**프로파일러 보고서에 [내 코드만] 사용**확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span></span>

![내 코드 옵션만][17]

<span data-ttu-id="52125-128">기존 프로젝트나 새 프로젝트에 이러한 지침을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="52125-129">새 프로젝트를 만들어 아래 설명된 기법을 시도하는 경우 C# **Azure 클라우드 서비스** 프로젝트를 선택한 후 **웹 역할** 및 **작업자 역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Azure 클라우드 서비스 프로젝트 역할][5]

<span data-ttu-id="52125-131">예제를 위해 오랜 시간이 걸리고 명백한 성능 문제를 보이는 일부 코드를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="52125-132">예를 들어 작업자 역할 프로젝트에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-132">For example, add the following code to a worker role project:</span></span>

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

<span data-ttu-id="52125-133">작업자 역할의 RoleEntryPoint 파생 클래스의 RunAsync 메서드에서 이 코드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="52125-134">동기적으로 실행되는 메서드에 대한 경고는 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-134">(Ignore the warning about the method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace the following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="52125-135">솔루션 구성을 **릴리스**로 설정하여 디버깅(Ctrl+F5) 없이 로컬에서 클라우드 서비스를 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span></span> <span data-ttu-id="52125-136">그러면 로컬에서 응용 프로그램을 실행하기 위한 모든 파일 및 폴더가 생성되고 모든 시뮬레이터가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="52125-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span></span> <span data-ttu-id="52125-137">작업 표시줄에서 계산 에뮬레이터 UI를 시작하여 작업자 역할이 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span></span>

## <a name="2-attach-to-a-process"></a><span data-ttu-id="52125-138">2: 프로세스에 연결</span><span class="sxs-lookup"><span data-stu-id="52125-138">2: Attach to a process</span></span>
<span data-ttu-id="52125-139">Visual Studio 2010 IDE에서 시작하여 응용 프로그램을 프로파일링하는 대신 실행 중인 프로세스에 프로파일러를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span></span> 

<span data-ttu-id="52125-140">프로파일러를 프로세스에 연결하려면 **분석** 메뉴에서 **프로파일러**를 선택한 후 **연결/분리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![프로필 연결 옵션][6]

<span data-ttu-id="52125-142">작업자 역할의 경우 WaWorkerHost.exe 프로세스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-142">For a worker role, find the WaWorkerHost.exe process.</span></span>

![WaWorkerHost 프로세스][7]

<span data-ttu-id="52125-144">프로젝트 폴더가 네트워크 드라이브에 있는 경우 프로파일러에서 프로파일링 보고서를 저장할 다른 위치를 제공하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span></span>

 <span data-ttu-id="52125-145">WaIISHost.exe에 연결하여 웹 역할에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-145">You can also attach to a web role by attaching to WaIISHost.exe.</span></span>
<span data-ttu-id="52125-146">응용 프로그램에 작업자 역할 프로세스가 여러 개 있는 경우 processID를 사용하여 구분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span></span> <span data-ttu-id="52125-147">Process 개체에 액세스하면 프로그래밍 방식으로 processID를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-147">You can query the processID programmatically by accessing the Process object.</span></span> <span data-ttu-id="52125-148">예를 들어 역할에 포함된 RoleEntryPoint 파생 클래스의 Run 메서드에 이 코드를 추가하면 계산 에뮬레이터 UI의 로그에서 연결할 프로세스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="52125-149">로그를 보려면 계산 에뮬레이터 UI를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-149">To view the log, start the Compute Emulator UI.</span></span>

![계산 에뮬레이터 UI 시작][8]

<span data-ttu-id="52125-151">계산 에뮬레이터 UI에서 콘솔 창의 제목 표시줄을 클릭하여 작업자 역할 로그 콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="52125-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span></span> <span data-ttu-id="52125-152">로그에서 프로세스 ID를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-152">You can see the process ID in the log.</span></span>

![프로세스 ID 보기][9]

<span data-ttu-id="52125-154">연결한 후 응용 프로그램 UI의 단계에 따라(필요한 경우) 시나리오를 재현합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span></span>

<span data-ttu-id="52125-155">프로파일링을 중지하려면 **프로파일링 중지** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-155">When you want to stop profiling, choose the **Stop Profiling** link.</span></span>

![프로파일링 중지 옵션][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="52125-157">3: 성능 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="52125-157">3: View performance reports</span></span>
<span data-ttu-id="52125-158">응용 프로그램에 대한 성능 보고서가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="52125-158">The performance report for your application is displayed.</span></span>

<span data-ttu-id="52125-159">이때 프로파일러는 실행을 중지하고 데이터를 .vsp 파일에 저장한 후 이 데이터의 분석을 보여 주는 보고서를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![프로파일러 보고서][11]

<span data-ttu-id="52125-161">실행 부하 과다 경로에 String.wstrcpy가 표시되는 경우 내 코드만을 클릭하여 사용자 코드만 표시하도록 뷰를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span></span>  <span data-ttu-id="52125-162">String.Concat가 표시되는 경우 모든 코드 표시 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="52125-162">If you see String.Concat, try pressing the Show All Code button.</span></span>

<span data-ttu-id="52125-163">Concatenate 메서드와 String.Concat가 실행 시간의 대부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span></span>

![보고서 분석][12]

<span data-ttu-id="52125-165">이 문서의 문자열 연결 코드를 추가한 경우 해당 작업 목록에 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="52125-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span></span> <span data-ttu-id="52125-166">만들어지고 삭제되는 문자열 수 때문에 가비지 수집 양이 너무 많다는 경고가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span></span>

![성능 경고][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="52125-168">4: 변경 및 성능 비교</span><span class="sxs-lookup"><span data-stu-id="52125-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="52125-169">코드 변경 이전과 이후의 성능을 비교할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-169">You can also compare the performance before and after a code change.</span></span>  <span data-ttu-id="52125-170">실행 중인 프로세스를 중지하고 코드를 편집하여 문자열 연결 작업을 StringBuilder 사용으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="52125-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span></span>

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

<span data-ttu-id="52125-171">다시 성능 실행을 수행한 후 성능을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-171">Do another performance run, and then compare the performance.</span></span> <span data-ttu-id="52125-172">동일한 세션에서 실행된 경우 성능 탐색기에서 두 보고서를 선택하고 바로 가기 메뉴를 연 후 **성능 보고서 비교**를 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52125-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="52125-173">다른 성능 세션의 실행과 비교하려면 **분석** 메뉴를 열고 **성능 보고서 비교**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="52125-174">표시되는 대화 상자에서 두 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-174">Specify both files in the dialog box that appears.</span></span>

![성능 보고서 비교 옵션][15]

<span data-ttu-id="52125-176">보고서에서 두 실행의 차이점이 강조됩니다.</span><span class="sxs-lookup"><span data-stu-id="52125-176">The reports highlight differences between the two runs.</span></span>

![비교 보고서][16]

<span data-ttu-id="52125-178">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-178">Congratulations!</span></span> <span data-ttu-id="52125-179">프로파일러를 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-179">You've gotten started with the profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="52125-180">문제 해결</span><span class="sxs-lookup"><span data-stu-id="52125-180">Troubleshooting</span></span>
* <span data-ttu-id="52125-181">릴리스 빌드를 프로파일링하고 있는지 확인하고 디버깅 없이 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="52125-182">프로파일러 메뉴에서 연결/분리 옵션을 사용할 수 없는 경우 성능 마법사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span></span>
* <span data-ttu-id="52125-183">계산 에뮬레이터 UI를 사용하여 응용 프로그램의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-183">Use the Compute Emulator UI to view the status of your application.</span></span> 
* <span data-ttu-id="52125-184">에뮬레이터에서 응용 프로그램을 시작하거나 프로파일러에 연결하는 데 문제가 있는 경우 계산 에뮬레이터를 종료했다가 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span></span> <span data-ttu-id="52125-185">그래도 문제가 해결되지 않으면 다시 부팅해 보세요.</span><span class="sxs-lookup"><span data-stu-id="52125-185">If that doesn't solve the problem, try rebooting.</span></span> <span data-ttu-id="52125-186">이 문제는 계산 에뮬레이터를 사용하여 실행 중인 배포를 일시 중단하고 제거하는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span></span>
* <span data-ttu-id="52125-187">명령줄에서 프로파일링 명령, 특히 전역 설정을 사용한 경우 VSPerfClrEnv /globaloff가 호출되고 VsPerfMon.exe가 종료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="52125-188">샘플링 시 "PRF0025: 수집한 데이터가 없습니다." 메시지가 표시되는 경우 연결한 프로세스에 CPU 작업이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span></span> <span data-ttu-id="52125-189">계산 작업을 수행하지 않는 응용 프로그램은 샘플링 데이터를 생성하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="52125-190">샘플링이 수행되기 전에 프로세스가 종료되었을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-190">It's also possible that the process exited before any sampling was done.</span></span> <span data-ttu-id="52125-191">프로파일링 중인 역할에 대한 Run 메서드가 종료되지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52125-191">Check to see that the Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52125-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52125-192">Next Steps</span></span>
<span data-ttu-id="52125-193">에뮬레이터를 통한 Azure 이진 계측은 Visual Studio 프로파일러에서 지원되지 않지만 메모리 할당을 테스트하려는 경우 프로파일링 시 해당 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="52125-194">스레드가 잠금 경쟁에 시간을 낭비하는지 확인하는 데 유용한 동시성 프로파일링이나 응용 프로그램 계층 간, 특히 데이터 계층과 작업자 역할 간 상호 작용 시의 성능 문제를 추적하는 데 유용한 계층 상호 작용 프로파일링을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span></span>  <span data-ttu-id="52125-195">앱에서 생성하는 데이터베이스 쿼리를 보고 프로파일링 데이터를 사용하여 데이터베이스 사용을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52125-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span></span> <span data-ttu-id="52125-196">계층 상호 작용 프로파일링에 대한 자세한 내용은 블로그 게시물 [Visual Studio Team System 2010에서 계층 상호 작용 프로파일러 사용][3](영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52125-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
