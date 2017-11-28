---
title: "클라우드 서비스를 로컬로 hello 계산 에뮬레이터에서에서 aaaProfiling | Microsoft Docs"
services: cloud-services
description: "Visual Studio 프로파일러 hello로 클라우드 서비스의 성능 문제를 검토 합니다."
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
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a><span data-ttu-id="d8cbc-103">Hello Azure 계산 에뮬레이터를 사용 하 여 hello Visual Studio 프로파일러에에서 hello 로컬로 클라우드 서비스의 성능 테스트</span><span class="sxs-lookup"><span data-stu-id="d8cbc-103">Testing hello Performance of a Cloud Service Locally in hello Azure Compute Emulator Using hello Visual Studio Profiler</span></span>
<span data-ttu-id="d8cbc-104">다양 한 도구와 기술을 클라우드 서비스의 hello 성능 테스트에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-104">A variety of tools and techniques are available for testing hello performance of cloud services.</span></span>
<span data-ttu-id="d8cbc-105">클라우드 서비스 tooAzure를 게시 하는 경우에 Visual Studio 프로 파일링 데이터 수집 및 분석 하는 것을 유지할 수 있습니다에 설명 된 대로 로컬 [Azure 응용 프로그램 프로 파일링][1]합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-105">When you publish a cloud service tooAzure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="d8cbc-106">에 설명 된 대로 진단 tootrack 다양 한 성능 카운터를 사용할 수도 있습니다 [성능 카운터를 사용 하 여 Azure에서][2]합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-106">You can also use diagnostics tootrack a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="d8cbc-107">도 toohello 클라우드 배포 하기 전에 hello 계산 에뮬레이터에서 로컬로 응용 프로그램 tooprofile를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-107">You might also want tooprofile your application locally in hello compute emulator before deploying it toohello cloud.</span></span>

<span data-ttu-id="d8cbc-108">이 문서 hello 에뮬레이터에서 로컬로 수행할 수 있는 프로 파일링의 hello CPU 샘플링 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-108">This article covers hello CPU Sampling method of profiling, which can be done locally in hello emulator.</span></span> <span data-ttu-id="d8cbc-109">CPU 샘플링은 주입식이 아닌 프로파일링 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="d8cbc-110">지정 된 샘플링 간격 hello 프로파일러는 hello 호출 스택의 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-110">At a designated sampling interval, hello profiler takes a snapshot of hello call stack.</span></span> <span data-ttu-id="d8cbc-111">hello 데이터는 시간 기간 동안 수집 되 고 보고서에 표시 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-111">hello data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="d8cbc-112">이 프로 파일링이 방법을 계산이 많이 필요한 응용 프로그램에서 대부분의 hello CPU 작업이 수행 되는 위치 tooindicate를 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-112">This method of profiling tends tooindicate where in a computationally intensive application most of hello CPU work is being done.</span></span>  <span data-ttu-id="d8cbc-113">여기서 응용 프로그램은 시간을 소비 hello 대부분 hello "실행 부하 과다 경로"에 기회 toofocus hello 이렇게 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-113">This gives you hello opportunity toofocus on hello "hot path" where your application is spending hello most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="d8cbc-114">1: 프로파일링을 위해 Visual Studio 구성</span><span class="sxs-lookup"><span data-stu-id="d8cbc-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="d8cbc-115">먼저 프로파일링 시 유용할 수 있는 몇 가지 Visual Studio 구성 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="d8cbc-116">toomake 의미 hello 프로 파일링 보고서를 응용 프로그램과 시스템 라이브러리에 대 한 기호에 대 한 기호 (.pdb 파일) 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-116">toomake sense of hello profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="d8cbc-117">Toomake 있는지 hello 사용할 수 있는 기호 서버를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-117">You'll want toomake sure that you reference hello available symbol servers.</span></span> <span data-ttu-id="d8cbc-118">toodo hello에이 **도구** Visual Studio에서 메뉴 선택 **옵션**를 눌러 **디버깅**, 다음 **기호**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-118">toodo this, on hello **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="d8cbc-119">Microsoft 기호 서버가 **기호 파일(.pdb) 위치**아래에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="d8cbc-120">추가 기호 파일이 있는 http://referencesource.microsoft.com/symbols를 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![기호 옵션][4]

<span data-ttu-id="d8cbc-122">원하는 경우 단순화할 수 있습니다 hello 보고 내 코드만 옵션을 설정 하 여 해당 hello 프로파일러를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-122">If desired, you can simplify hello reports that hello profiler generates by setting Just My Code.</span></span> <span data-ttu-id="d8cbc-123">내 코드만 사용 함수 호출 스택은 완전히 내부 toolibraries를 호출 하 고.NET Framework hello hello 보고서에서 숨겨진 간소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal toolibraries and hello .NET Framework are hidden from hello reports.</span></span> <span data-ttu-id="d8cbc-124">Hello에 **도구** 메뉴 선택 **옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-124">On hello **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="d8cbc-125">다음 hello 확장 **성능 도구** 노드를 선택 하 고 **일반**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-125">Then expand hello **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="d8cbc-126">에 대 한 hello 확인란 선택 **내 코드만 사용 프로파일러 보고서에 대 한**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-126">Select hello checkbox for **Enable Just My Code for profiler reports**.</span></span>

![내 코드 옵션만][17]

<span data-ttu-id="d8cbc-128">기존 프로젝트나 새 프로젝트에 이러한 지침을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="d8cbc-129">새 프로젝트 tootry hello 아래에 설명 된 기술을 만드는 경우 선택 하는 C# **Azure 클라우드 서비스** 프로젝트를 선택 하 고는 **웹 역할** 및 **작업자 역할**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-129">If you create a new project tootry hello techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Azure 클라우드 서비스 프로젝트 역할][5]

<span data-ttu-id="d8cbc-131">예를 들어에서는 시간이 많이 걸리고 몇 가지 확실 한 성능 문제를 보여 줍니다.는 몇 가지 코드 tooyour 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-131">For example purposes, add some code tooyour project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="d8cbc-132">예를 들어 다음 코드 tooa 작업자 역할 프로젝트 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-132">For example, add hello following code tooa worker role project:</span></span>

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

<span data-ttu-id="d8cbc-133">Hello hello 작업자 역할의 RoleEntryPoint 파생 클래스에서 RunAsync 메서드에서에서이 코드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-133">Call this code from hello RunAsync method in hello worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="d8cbc-134">(동기적으로 실행 하는 hello 방법에 대 한 hello 경고를 무시 합니다.)</span><span class="sxs-lookup"><span data-stu-id="d8cbc-134">(Ignore hello warning about hello method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="d8cbc-135">빌드 및 클라우드 서비스를 로컬로 실행할 (Ctrl + F5)을 디버깅 하지 않고 된 hello 솔루션 구성도**릴리스**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-135">Build and run your cloud service locally without debugging (Ctrl+F5), with hello solution configuration set too**Release**.</span></span> <span data-ttu-id="d8cbc-136">이렇게 하면 hello 응용 프로그램을 로컬로 실행에 대해 생성 된 모든 파일 및 폴더 및 모든 hello 에뮬레이터 시작 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-136">This ensures that all files and folders are created for running hello application locally, and ensures that all hello emulators are started.</span></span> <span data-ttu-id="d8cbc-137">작업자 역할을 실행 하는 hello 작업 표시줄 tooverify에서 hello 계산 에뮬레이터 UI를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-137">Start hello Compute Emulator UI from hello taskbar tooverify that your worker role is running.</span></span>

## <a name="2-attach-tooa-process"></a><span data-ttu-id="d8cbc-138">2: tooa 프로세스 연결</span><span class="sxs-lookup"><span data-stu-id="d8cbc-138">2: Attach tooa process</span></span>
<span data-ttu-id="d8cbc-139">Visual Studio 2010 IDE hello에서 시작 하 여 hello 응용 프로그램을 프로 파일링, 대신 프로세스를 실행 하는 hello 프로파일러 tooa를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-139">Instead of profiling hello application by starting it from hello Visual Studio 2010 IDE, you must attach hello profiler tooa running process.</span></span> 

<span data-ttu-id="d8cbc-140">hello에 tooattach hello 프로파일러 tooa 프로세스 **분석** 메뉴 선택 **프로파일러** 및 **연결/분리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-140">tooattach hello profiler tooa process, on hello **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![프로필 연결 옵션][6]

<span data-ttu-id="d8cbc-142">작업자 역할에 대 한 hello WaWorkerHost.exe 프로세스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-142">For a worker role, find hello WaWorkerHost.exe process.</span></span>

![WaWorkerHost 프로세스][7]

<span data-ttu-id="d8cbc-144">프로젝트 폴더는 네트워크 드라이브에 있으면 hello 프로파일러가 묻습니다 tooprovide 프로 파일링 보고서는 다른 위치 toosave hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-144">If your project folder is on a network drive, hello profiler will ask you tooprovide another location toosave hello profiling reports.</span></span>

 <span data-ttu-id="d8cbc-145">TooWaIISHost.exe 연결 하 여 tooa 웹 역할에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-145">You can also attach tooa web role by attaching tooWaIISHost.exe.</span></span>
<span data-ttu-id="d8cbc-146">Toouse hello processID toodistinguish 필요한 응용 프로그램에 여러 작업자 역할 프로세스가 있는 경우 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-146">If there are multiple worker role processes in your application, you need toouse hello processID toodistinguish them.</span></span> <span data-ttu-id="d8cbc-147">Hello 프로세스 개체에 액세스 하 여 hello 나타나지 않지만 processID를 프로그래밍 방식으로 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-147">You can query hello processID programmatically by accessing hello Process object.</span></span> <span data-ttu-id="d8cbc-148">예를 들어 hello RoleEntryPoint 파생 클래스의 코드 toohello Run 메서드가이 역할에 추가 하면 수 확인 하면 로그 hello 계산 에뮬레이터 UI tooknow에 어떤 프로세스 tooconnect 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-148">For example, if you add this code toohello Run method of hello RoleEntryPoint-derived class in a role, you can look at the log in hello Compute Emulator UI tooknow what process tooconnect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="d8cbc-149">계산 에뮬레이터 UI 시작 hello tooview hello 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-149">tooview hello log, start hello Compute Emulator UI.</span></span>

![Hello 계산 에뮬레이터 UI를 시작 합니다.][8]

<span data-ttu-id="d8cbc-151">Hello 콘솔 창의 제목 표시줄을 클릭 하 여 hello 계산 에뮬레이터 UI에서에서 hello 작업자 역할 로그 콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-151">Open hello worker role log console window in hello Compute Emulator UI by clicking on hello console window's title bar.</span></span> <span data-ttu-id="d8cbc-152">Hello 로그에 hello 프로세스 ID를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-152">You can see hello process ID in hello log.</span></span>

![프로세스 ID 보기][9]

<span data-ttu-id="d8cbc-154">응용 프로그램의 UI (필요한 경우) tooreproduce hello 시나리오에서 hello 단계를 수행 하는 하나, 첨부</span><span class="sxs-lookup"><span data-stu-id="d8cbc-154">One you've attached, perform hello steps in your application's UI (if needed) tooreproduce hello scenario.</span></span>

<span data-ttu-id="d8cbc-155">Toostop 프로 파일링에 하려는 경우 선택 hello **프로 파일링 중지** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-155">When you want toostop profiling, choose hello **Stop Profiling** link.</span></span>

![프로파일링 중지 옵션][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="d8cbc-157">3: 성능 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="d8cbc-157">3: View performance reports</span></span>
<span data-ttu-id="d8cbc-158">응용 프로그램에 대 한 hello 성능 보고서가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-158">hello performance report for your application is displayed.</span></span>

<span data-ttu-id="d8cbc-159">이 시점에서 hello 프로파일러 실행이 중지 되는 vsp 파일에 데이터를 저장 및이 데이터의 분석을 보여 주는 보고서가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-159">At this point, hello profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![프로파일러 보고서][11]

<span data-ttu-id="d8cbc-161">String.wstrcpy hello에 표시 되 면 실행 부하 과다 경로 내 코드만 toochange hello 클릭 tooshow 사용자 코드에만 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-161">If you see String.wstrcpy in hello Hot Path, click on Just My Code toochange hello view tooshow user code only.</span></span>  <span data-ttu-id="d8cbc-162">String.Concat 표시 되 면 hello 모든 코드 표시 단추를 누르면 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-162">If you see String.Concat, try pressing hello Show All Code button.</span></span>

<span data-ttu-id="d8cbc-163">Hello Concatenate 메서드와 hello 실행 시간의 많은 부분을 차지 String.Concat 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-163">You should see hello Concatenate method and String.Concat taking up a large portion of hello execution time.</span></span>

![보고서 분석][12]

<span data-ttu-id="d8cbc-165">이 문서의 hello 문자열 연결 코드를 추가한 경우이 대 한 hello 작업 목록에서에서 경고를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-165">If you added hello string concatenation code in this article, you should see a warning in hello Task List for this.</span></span> <span data-ttu-id="d8cbc-166">이 가비지 컬렉션은 생성 되 고 삭제 하는 문자열의 toohello 수 때문에 과도 한 양의 하다는 경고가 나타날 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-166">You may also see a warning that there is an excessive amount of garbage collection, which is due toohello number of strings that are created and disposed.</span></span>

![성능 경고][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="d8cbc-168">4: 변경 및 성능 비교</span><span class="sxs-lookup"><span data-stu-id="d8cbc-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="d8cbc-169">또한 코드 변경 전후의 hello 성능을 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-169">You can also compare hello performance before and after a code change.</span></span>  <span data-ttu-id="d8cbc-170">프로세스를 실행 하는 hello를 중지 하 고 hello 코드 tooreplace hello 문자열 연결 작업 hello 사용과 StringBuilder의 편집:</span><span class="sxs-lookup"><span data-stu-id="d8cbc-170">Stop hello running process, and edit hello code tooreplace hello string concatenation operation with hello use of StringBuilder:</span></span>

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

<span data-ttu-id="d8cbc-171">다른 성능 실행을 수행 하 고 hello 성능을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-171">Do another performance run, and then compare hello performance.</span></span> <span data-ttu-id="d8cbc-172">성능 탐색기 hello 경우 hello 실행은의 hello 동일한 세션 수만 두 보고서, hello 바로 가기 메뉴를 열고 선택한 선택 **성능 보고서 비교**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-172">In hello Performance Explorer, if hello runs are in hello same session, you can just select both reports, open hello shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="d8cbc-173">다른 성능 세션에서 실행 toocompare hello를 열고, **분석** 메뉴 선택 **성능 보고서 비교**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-173">If you want toocompare with a run in another performance session, open hello **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="d8cbc-174">표시 되는 hello 대화 상자에서 두 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-174">Specify both files in hello dialog box that appears.</span></span>

![성능 보고서 비교 옵션][15]

<span data-ttu-id="d8cbc-176">hello 보고서 hello 두 실행 간의 차이 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-176">hello reports highlight differences between hello two runs.</span></span>

![비교 보고서][16]

<span data-ttu-id="d8cbc-178">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-178">Congratulations!</span></span> <span data-ttu-id="d8cbc-179">Hello 프로파일러와 함께 시작 했으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-179">You've gotten started with hello profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d8cbc-180">문제 해결</span><span class="sxs-lookup"><span data-stu-id="d8cbc-180">Troubleshooting</span></span>
* <span data-ttu-id="d8cbc-181">릴리스 빌드를 프로파일링하고 있는지 확인하고 디버깅 없이 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="d8cbc-182">Hello 연결/분리 옵션 hello 프로파일러 메뉴를 사용 하지 않는 경우 hello 성능 마법사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-182">If hello Attach/Detach option is not enabled on hello Profiler menu, run hello Performance Wizard.</span></span>
* <span data-ttu-id="d8cbc-183">응용 프로그램의 hello tooview hello 상태를 계산 에뮬레이터 UI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-183">Use hello Compute Emulator UI tooview hello status of your application.</span></span> 
* <span data-ttu-id="d8cbc-184">Hello 에뮬레이터에서 응용 프로그램을 시작 하는 데 문제가 있으면 또는 프로파일러 hello를 연결 하는 경우에 hello 계산 에뮬레이터를 종료 하 고 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-184">If you have problems starting applications in hello emulator, or attaching hello profiler, shut down hello compute emulator and restart it.</span></span> <span data-ttu-id="d8cbc-185">Hello 문제가 해결 되지를 다시 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-185">If that doesn't solve hello problem, try rebooting.</span></span> <span data-ttu-id="d8cbc-186">계산 에뮬레이터 toosuspend hello를 사용 하 여 실행 중인 배포를 제거 하는 경우이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-186">This problem can occur if you use hello Compute Emulator toosuspend and remove running deployments.</span></span>
* <span data-ttu-id="d8cbc-187">특히 전역 설정 hello 명령을 명령줄에서 프로 파일링 하는 hello를 모두 사용한 경우에 VSPerfClrEnv /globaloff가 호출 된 및 VsPerfMon.exe 종료 된 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-187">If you have used any of hello profiling commands from the command line, especially hello global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="d8cbc-188">Hello 메시지를 샘플링 하는 경우 표시 되 면 "PRF0025: 데이터가 수집 된" hello toohas CPU 활동을 연결 프로세스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-188">If when sampling, you see hello message "PRF0025: No data was collected," check that hello process you attached toohas CPU activity.</span></span> <span data-ttu-id="d8cbc-189">계산 작업을 수행하지 않는 응용 프로그램은 샘플링 데이터를 생성하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="d8cbc-190">해당 수행 된 모든 샘플링 전에 hello 프로세스를 종료할 수 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-190">It's also possible that hello process exited before any sampling was done.</span></span> <span data-ttu-id="d8cbc-191">프로 파일링 하는 역할에 대 한 hello Run 메서드가 종료 되지 않는 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-191">Check toosee that hello Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8cbc-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8cbc-192">Next Steps</span></span>
<span data-ttu-id="d8cbc-193">Hello 에뮬레이터에서 Azure 이진 계측는 hello Visual Studio 프로파일러에 지원 되지 않지만 tootest 메모리 할당 하려는 경우 프로 파일링 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-193">Instrumenting Azure binaries in hello emulator is not supported in hello Visual Studio profiler, but if you want tootest memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="d8cbc-194">선택할 수도 있습니다 동시성 프로 파일링는 데 도움이 되는 응용 프로그램 계층 간에 상호 작용할 때 성능 문제를 추적 하는 데 도움이 되를 스레드 잠금을 경쟁 하는 시간을 낭비 하 있는지 여부를 결정 하거나 계층 상호 작용 프로 파일링 가장 자주 사이의 hello 데이터 계층 작업자 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between hello data tier and a worker role.</span></span>  <span data-ttu-id="d8cbc-195">응용 프로그램을 생성 하는 hello 데이터베이스 쿼리를 볼 수 있으며 데이터 tooimprove hello database 사용 하 여 프로 파일링 하는 hello를 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-195">You can view hello database queries that your app generates and use hello profiling data tooimprove your use of hello database.</span></span> <span data-ttu-id="d8cbc-196">계층 상호 작용 프로 파일링 하는 방법에 대 한 내용은 hello 블로그 게시물을 참조 하십시오. [연습: Visual Studio Team System 2010에서 계층 상호 작용 프로파일러 hello를 사용 하 여][3]합니다.</span><span class="sxs-lookup"><span data-stu-id="d8cbc-196">For information about tier interaction profiling, see hello blog post [Walkthrough: Using hello Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

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
