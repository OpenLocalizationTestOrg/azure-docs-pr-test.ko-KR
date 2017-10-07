---
title: "Azure 진단으로 클라우드 서비스 응용 프로그램에서 aaaTrace hello 흐름 | Microsoft Docs"
description: "추가 추적 메시지 tooan Azure 응용 프로그램 toohelp 디버깅, 성능 측정, 모니터링, 트래픽 분석 합니다."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="2a2d4-103">Azure 진단으로 클라우드 서비스 응용 프로그램의 hello 흐름 추적</span><span class="sxs-lookup"><span data-stu-id="2a2d4-103">Trace hello flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="2a2d4-104">추적은 실행 되는 동안 있습니다 toomonitor hello 응용 프로그램의 실행에 대 한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-104">Tracing is a way for you toomonitor hello execution of your application while it is running.</span></span> <span data-ttu-id="2a2d4-105">Hello를 사용할 수 있습니다 [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), 및 [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) toorecord 정보 오류에 대 한 클래스 및 응용 프로그램 로그, 텍스트 파일 또는 향후 분석을 위해 다른 장치에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-105">You can use hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes toorecord information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="2a2d4-106">추적에 대한 자세한 내용은 [응용 프로그램을 추적 및 계측](https://msdn.microsoft.com/library/zs6s4h68.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="2a2d4-107">추적 문 및 추적 스위치 사용</span><span class="sxs-lookup"><span data-stu-id="2a2d4-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="2a2d4-108">Hello를 추가 하 여 클라우드 서비스 응용 프로그램에서 구현 추적 [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) 하므로 toohello 응용 프로그램 구성 및 tooSystem.Diagnostics.Trace 또는 System.Diagnostics.Debug에 호출 하 여 응용 프로그램 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-108">Implement tracing in your Cloud Services application by adding hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello application configuration and making calls tooSystem.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="2a2d4-109">사용 하 여 hello 구성 파일 *app.config* 작업자 역할과 hello에 대 한 *web.config* 웹 역할에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-109">Use hello configuration file *app.config* for worker roles and hello *web.config* for web roles.</span></span> <span data-ttu-id="2a2d4-110">Visual Studio 템플릿을 사용 하 여 새 호스팅된 서비스를 만들 때 Azure 진단이 자동으로 toohello 프로젝트를 추가 및 hello DiagnosticMonitorTraceListener toohello 해당 구성 파일을 추가 하는 hello 역할에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added toohello project and hello DiagnosticMonitorTraceListener is added toohello appropriate configuration file for hello roles that you add.</span></span>

<span data-ttu-id="2a2d4-111">Trace 문 배치에 대 한 정보를 참조 하십시오. [하는 방법: Trace 문 추가 tooApplication 코드](https://msdn.microsoft.com/library/zd83saa2.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-111">For information on placing trace statements, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="2a2d4-112">코드에 [추적 스위치](https://msdn.microsoft.com/library/3at424ac.aspx) 를 배치하여 추적의 발생 여부와 범위를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="2a2d4-113">이렇게 하면 프로덕션 환경에서 응용 프로그램의 hello 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-113">This lets you monitor hello status of your application in a production environment.</span></span> <span data-ttu-id="2a2d4-114">여러 컴퓨터에서 실행하는 여러 구성 요소를 사용하는 비즈니스 응용 프로그램에서 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="2a2d4-115">자세한 내용은 [방법: 추적 스위치 구성](https://msdn.microsoft.com/library/t06xyy08.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-hello-trace-listener-in-an-azure-application"></a><span data-ttu-id="2a2d4-116">Azure 응용 프로그램에서 hello 추적 수신기를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-116">Configure hello trace listener in an Azure application</span></span>
<span data-ttu-id="2a2d4-117">추적, 디버그 및 TraceSource를 사용 해야 "수신자" toocollect 및 전송 되는 레코드 hello 메시지를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-117">Trace, Debug and TraceSource, require you set up "listeners" toocollect and record hello messages that are sent.</span></span> <span data-ttu-id="2a2d4-118">수신기는 추적 메시지를 수집, 저장 및 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="2a2d4-119">직접 실행 hello 추적 출력 tooan 같은 적절 한 대상, 로그, 창 또는 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-119">They direct hello tracing output tooan appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="2a2d4-120">Azure 진단 hello를 사용 하 여 [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-120">Azure Diagnostics uses hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="2a2d4-121">Hello 절차를 완료 하기 전에 hello Azure 진단 모니터를 초기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-121">Before you complete hello following procedure, you must initialize hello Azure diagnostic monitor.</span></span> <span data-ttu-id="2a2d4-122">toodo이,이 참조 [Microsoft Azure에서 진단 사용](cloud-services-dotnet-diagnostics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-122">toodo this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="2a2d4-123">참고는 Visual Studio에서 제공 되는 hello 템플릿을 사용 하는 경우 hello 수신기의 hello 구성을 자동으로 추가 됩니다 드립니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-123">Note that if you use hello templates that are provided by Visual Studio, hello configuration of hello listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="2a2d4-124">추적 수신기 추가</span><span class="sxs-lookup"><span data-stu-id="2a2d4-124">Add a trace listener</span></span>
1. <span data-ttu-id="2a2d4-125">사용자 역할에 대 한 hello web.config 또는 app.config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-125">Open hello web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="2a2d4-126">다음 코드 toohello 파일 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-126">Add hello following code toohello file.</span></span> <span data-ttu-id="2a2d4-127">Hello 버전 특성 toouse hello 어셈블리의 버전 번호 hello 참조를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-127">Change hello Version attribute toouse hello version number of hello assembly you are referencing.</span></span> <span data-ttu-id="2a2d4-128">hello 어셈블리 버전이 변경 되지 않습니다 반드시 각 Azure SDK 릴리스로 업데이트 tooit는 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-128">hello assembly version does not necessarily change with each Azure SDK release unless there are updates tooit.</span></span>
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > <span data-ttu-id="2a2d4-129">프로젝트 참조 toohello Microsoft.WindowsAzure.Diagnostics 어셈블리 지정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-129">Make sure you have a project reference toohello Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="2a2d4-130">참조 된 Microsoft.WindowsAzure.Diagnostics 어셈블리를 toomatch hello 버전의 hello 위에 hello xml hello 버전 번호를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-130">Update hello version number in hello xml above toomatch hello version of hello referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="2a2d4-131">Hello 구성 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-131">Save hello config file.</span></span>

<span data-ttu-id="2a2d4-132">수신기에 대한 자세한 내용은 [추적 수신기](https://msdn.microsoft.com/library/4y5y10s7.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="2a2d4-133">Hello 단계 tooadd hello 수신기를 완료 한 후에 추적 문 tooyour 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-133">After you complete hello steps tooadd hello listener, you can add trace statements tooyour code.</span></span>

### <a name="tooadd-trace-statement-tooyour-code"></a><span data-ttu-id="2a2d4-134">tooadd 추적 문 tooyour 코드</span><span class="sxs-lookup"><span data-stu-id="2a2d4-134">tooadd trace statement tooyour code</span></span>
1. <span data-ttu-id="2a2d4-135">응용 프로그램에 대한 소스 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-135">Open a source file for your application.</span></span> <span data-ttu-id="2a2d4-136">예를 들어 hello <RoleName>hello 작업자 역할 또는 웹 역할에 대 한.cs 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-136">For example, hello <RoleName>.cs file for hello worker role or web role.</span></span>
2. <span data-ttu-id="2a2d4-137">Hello 다음 추가 이미 추가 되지 않은 경우 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="2a2d4-137">Add hello following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="2a2d4-138">응용 프로그램의 hello 상태에 대 한 toocapture 정보를 표시할 위치 추적 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-138">Add Trace statements where you want toocapture information about hello state of your application.</span></span> <span data-ttu-id="2a2d4-139">다양 한 추적 문이 hello tooformat hello 출력 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-139">You can use a variety of methods tooformat hello output of hello Trace statement.</span></span> <span data-ttu-id="2a2d4-140">자세한 내용은 참조 [하는 방법: Trace 문 추가 tooApplication 코드](https://msdn.microsoft.com/library/zd83saa2.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-140">For more information, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="2a2d4-141">Hello 소스 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a2d4-141">Save hello source file.</span></span>

