---
title: "Azure 진단으로 클라우드 서비스 응용 프로그램의 흐름 추적 | Microsoft Docs"
description: "Azure 응용 프로그램에 추적 메시지를 추가하여 디버깅, 성능 측정, 모니터링, 트래픽 분석 등을 할 수 있습니다."
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
ms.openlocfilehash: 35b4a4270846c54a1ca760e803ef7adba60cf03b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="trace-the-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="aff71-103">Azure 진단으로 클라우드 서비스 응용 프로그램의 흐름 추적</span><span class="sxs-lookup"><span data-stu-id="aff71-103">Trace the flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="aff71-104">추적은 실행되는 동안 응용 프로그램의 실행을 모니터링하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-104">Tracing is a way for you to monitor the execution of your application while it is running.</span></span> <span data-ttu-id="aff71-105">[System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx) 및 [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) 클래스를 사용하여 로그의 오류 및 응용 프로그램 실행, 텍스트 파일 또는 차후 분석을 위한 다른 장치에 대한 정보를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-105">You can use the [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes to record information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="aff71-106">추적에 대한 자세한 내용은 [응용 프로그램을 추적 및 계측](https://msdn.microsoft.com/library/zs6s4h68.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aff71-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="aff71-107">추적 문 및 추적 스위치 사용</span><span class="sxs-lookup"><span data-stu-id="aff71-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="aff71-108">[DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) 를 응용 프로그램 구성에 추가하고 응용 프로그램 코드에 System.Diagnostics.Trace 또는 System.Diagnostics.Debug에 대해 호출하여 클라우드 서비스 응용 프로그램에서 추적을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-108">Implement tracing in your Cloud Services application by adding the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) to the application configuration and making calls to System.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="aff71-109">작업자 역할에 대해 구성 파일 *app.config* 및 웹 역할에 대해 *web.config*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-109">Use the configuration file *app.config* for worker roles and the *web.config* for web roles.</span></span> <span data-ttu-id="aff71-110">Visual Studio 템플릿을 사용하여 새 호스티드 서비스를 만드는 경우 Azure 진단이 프로젝트에 자동으로 추가되고 DiagnosticMonitorTraceListener가 추가하는 역할에 대한 적절한 구성 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added to the project and the DiagnosticMonitorTraceListener is added to the appropriate configuration file for the roles that you add.</span></span>

<span data-ttu-id="aff71-111">추적 문 배치에 대한 정보는 [방법: 응용 프로그램 코드에 추적 문 추가](https://msdn.microsoft.com/library/zd83saa2.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aff71-111">For information on placing trace statements, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="aff71-112">코드에 [추적 스위치](https://msdn.microsoft.com/library/3at424ac.aspx) 를 배치하여 추적의 발생 여부와 범위를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="aff71-113">이렇게 하면 프로덕션 환경에서 응용 프로그램의 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-113">This lets you monitor the status of your application in a production environment.</span></span> <span data-ttu-id="aff71-114">여러 컴퓨터에서 실행하는 여러 구성 요소를 사용하는 비즈니스 응용 프로그램에서 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="aff71-115">자세한 내용은 [방법: 추적 스위치 구성](https://msdn.microsoft.com/library/t06xyy08.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aff71-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-the-trace-listener-in-an-azure-application"></a><span data-ttu-id="aff71-116">Azure 응용 프로그램에서 추적 수신기 구성</span><span class="sxs-lookup"><span data-stu-id="aff71-116">Configure the trace listener in an Azure application</span></span>
<span data-ttu-id="aff71-117">추적, 디버그 및 TraceSource는 전송된 메시지를 수집하고 기록할 "수신기" 설정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-117">Trace, Debug and TraceSource, require you set up "listeners" to collect and record the messages that are sent.</span></span> <span data-ttu-id="aff71-118">수신기는 추적 메시지를 수집, 저장 및 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="aff71-119">추적 출력을 로그, 창 또는 텍스트 파일과 같은 적절한 대상에 직접 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-119">They direct the tracing output to an appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="aff71-120">Azure 진단은 [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-120">Azure Diagnostics uses the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="aff71-121">다음 절차를 완료하기 전에 Azure 진단 모니터를 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-121">Before you complete the following procedure, you must initialize the Azure diagnostic monitor.</span></span> <span data-ttu-id="aff71-122">이렇게 하려면 [Microsoft Azure에서 진단 사용](cloud-services-dotnet-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aff71-122">To do this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="aff71-123">Visual Studio에서 제공되는 서식 파일을 사용하는 경우 수신기의 구성은 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-123">Note that if you use the templates that are provided by Visual Studio, the configuration of the listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="aff71-124">추적 수신기 추가</span><span class="sxs-lookup"><span data-stu-id="aff71-124">Add a trace listener</span></span>
1. <span data-ttu-id="aff71-125">사용자의 역할에 대한 web.config 또는 app.config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-125">Open the web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="aff71-126">파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-126">Add the following code to the file.</span></span> <span data-ttu-id="aff71-127">참조할 어셈블리의 버전 번호를 사용하려면 버전 특성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-127">Change the Version attribute to use the version number of the assembly you are referencing.</span></span> <span data-ttu-id="aff71-128">어셈블리 버전은 업데이트가 없는 경우 각 Azure SDK 릴리스로 변경할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-128">The assembly version does not necessarily change with each Azure SDK release unless there are updates to it.</span></span>
   
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
   > <span data-ttu-id="aff71-129">Microsoft.WindowsAzure.Diagnostics 어셈블리에 대한 프로젝트 참조가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-129">Make sure you have a project reference to the Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="aff71-130">참조된 Microsoft.WindowsAzure.Diagnostics 어셈블리의 버전과 일치하도록 위의 xml의 버전 번호를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-130">Update the version number in the xml above to match the version of the referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="aff71-131">구성 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-131">Save the config file.</span></span>

<span data-ttu-id="aff71-132">수신기에 대한 자세한 내용은 [추적 수신기](https://msdn.microsoft.com/library/4y5y10s7.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aff71-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="aff71-133">수신기를 추가하는 단계를 완료한 후 코드에 추적 문을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-133">After you complete the steps to add the listener, you can add trace statements to your code.</span></span>

### <a name="to-add-trace-statement-to-your-code"></a><span data-ttu-id="aff71-134">코드에 추적 문을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="aff71-134">To add trace statement to your code</span></span>
1. <span data-ttu-id="aff71-135">응용 프로그램에 대한 소스 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-135">Open a source file for your application.</span></span> <span data-ttu-id="aff71-136">예를 들어 작업자 역할 또는 웹 역할에 대한 <RoleName>.cs 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-136">For example, the <RoleName>.cs file for the worker role or web role.</span></span>
2. <span data-ttu-id="aff71-137">아직 추가되지 않은 경우 문을 사용하여 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-137">Add the following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="aff71-138">응용 프로그램의 상태에 대한 정보를 캡처하려는 추적 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-138">Add Trace statements where you want to capture information about the state of your application.</span></span> <span data-ttu-id="aff71-139">다양한 메서드를 사용하여 추적 문의 출력을 포맷할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-139">You can use a variety of methods to format the output of the Trace statement.</span></span> <span data-ttu-id="aff71-140">자세한 내용은 [방법: 응용 프로그램 코드에 추적 문 추가](https://msdn.microsoft.com/library/zd83saa2.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aff71-140">For more information, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="aff71-141">소스 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="aff71-141">Save the source file.</span></span>

