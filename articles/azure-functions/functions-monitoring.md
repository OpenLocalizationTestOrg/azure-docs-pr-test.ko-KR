---
title: "Azure 함수 aaaMonitoring | Microsoft Docs"
description: "자세한 내용은 방법 toomonitor Azure 함수입니다."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="04ade-104">Azure Functions 모니터링</span><span class="sxs-lookup"><span data-stu-id="04ade-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="04ade-105">개요</span><span class="sxs-lookup"><span data-stu-id="04ade-105">Overview</span></span> 


<span data-ttu-id="04ade-106">hello **모니터** 탭에 각 기능을 통해 tooreview 있습니다 함수의 각 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-106">hello **Monitor** tab for each function allows you tooreview each execution of a function.</span></span>

![Azure Functions 모니터 탭](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="04ade-108">실행을 클릭 하면 tooreview hello 기간, 입력된 데이터, 오류 및 관련된 로그 파일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-108">Clicking an execution allows you tooreview hello duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="04ade-109">이 탭은 함수를 디버그하고 성능을 조정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="04ade-110">Hello를 사용 하는 경우 [호스팅 계획 소비](functions-overview.md#pricing) Azure 함수에 대 한 hello **모니터링** hello 함수 응용 프로그램 개요 블레이드에서 타일 모든 데이터가 표시 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-110">When using hello [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, hello **Monitoring** tile in hello Function App overview blade will not show any data.</span></span> <span data-ttu-id="04ade-111">Hello 플랫폼에서 동적으로 확장 하 고 이러한 메트릭을 사용 계획에 적용 되므로, 계산 인스턴스를 관리 하는 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-111">This is because hello platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="04ade-112">기능 앱 toomonitor hello 사용이 문서의 hello 지침을 대신 사용 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-112">toomonitor hello usage of your Function Apps, you should instead use hello guidance in this article.</span></span>
> 
> <span data-ttu-id="04ade-113">다음 스크린 샷에서 hello 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-113">hello following screen-shot shows an example:</span></span>
> 
> ![기본 리소스 블레이드 hello에 대 한 모니터링](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="04ade-115">실시간 모니터링</span><span class="sxs-lookup"><span data-stu-id="04ade-115">Real-time monitoring</span></span>

<span data-ttu-id="04ade-116">아래와 같이 **라이브 이벤트 스트림**을 클릭하면 실시간 모니터링을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![라이브 hello 모니터 탭에 대 한 이벤트 스트림 옵션](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="04ade-118">아래와 같이 hello 라이브 이벤트 스트림 새 브라우저 탭에서 그래프로 나타낼 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-118">hello live event stream will be graphed in a new browser tab as shown below.</span></span> 

![라이브 이벤트 스트림 예제](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="04ade-120">입력 하 여 데이터 toofail toobe를 일으킬 수 있는 알려진된 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-120">There is a known issue that may cause your data toofail toobe populated.</span></span> <span data-ttu-id="04ade-121">Tooclose hello 브라우저 탭 포함 hello 라이브 이벤트 스트림과 클릭이 발생 하면 할 수 있습니다 **라이브 이벤트 스트림** 다시 tooallow 것 tooproperly 이벤트 스트림 데이터를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-121">If you experience this, you may need tooclose hello browser tab containing hello live event stream and then click **live event stream** again tooallow it tooproperly populate your event stream data.</span></span> 

<span data-ttu-id="04ade-122">hello 라이브 이벤트 스트림 hello 함수에 대 한 통계를 다음 그래프 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-122">hello live event stream will graph hello following statistics for your function:</span></span>

* <span data-ttu-id="04ade-123">초당 시작된 실행</span><span class="sxs-lookup"><span data-stu-id="04ade-123">Executions started per second</span></span>
* <span data-ttu-id="04ade-124">초당 완료된 실행</span><span class="sxs-lookup"><span data-stu-id="04ade-124">Executions completed per second</span></span>
* <span data-ttu-id="04ade-125">초당 실패한 실행</span><span class="sxs-lookup"><span data-stu-id="04ade-125">Executions failed per second</span></span>
* <span data-ttu-id="04ade-126">평균 실행 시간(밀리초)</span><span class="sxs-lookup"><span data-stu-id="04ade-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="04ade-127">이 통계는 실시간 있지만 hello hello 실행 데이터의 그래프 실제 10 초 정도 대기 시간이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-127">These statistics are real-time but hello actual graphing of hello execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="04ade-128">명령줄에서 로그 파일 모니터링</span><span class="sxs-lookup"><span data-stu-id="04ade-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="04ade-129">로그 파일 tooa 명령줄 세션 hello Azure 명령줄 인터페이스 (CLI) 또는 PowerShell을 사용 하 여 로컬 워크스테이션에서 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-129">You can stream log files tooa command line session on a local workstation using hello Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a><span data-ttu-id="04ade-130">함수 hello Azure CLI를 사용 하는 응용 프로그램 로그 파일 모니터링</span><span class="sxs-lookup"><span data-stu-id="04ade-130">Monitoring function app log files with hello Azure CLI</span></span>

<span data-ttu-id="04ade-131">시작 tooget [hello Azure CLI를 설치 합니다.](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="04ade-131">tooget started, [install hello Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="04ade-132">Hello 다음을 사용 하 여 Azure 계정에 로그인 명령 또는 중 하나를에서 설명 하는 다른 옵션 hello [hello Azure CLI에서에서 tooAzure 로그인](../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-132">Log into your Azure account using hello following command, or any of hello other options covered in, [Log in tooAzure from hello Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="04ade-133">사용 하 여 hello 다음 명령은 tooenable Azure CLI 서비스 관리 (ASM) 모드: 합니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-133">Use hello following command tooenable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="04ade-134">여러 구독이 있는 경우 구독 및 집합 hello 현재 구독 toohello 구독 함수 앱을 포함 하는 다음 명령을 toolist hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-134">If you have multiple subscriptions, use hello following commands toolist your subscriptions and set hello current subscription toohello subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="04ade-135">hello 다음 명령이 스트리밍되지 앱 toohello 함수 명령줄의 hello 로그 파일:</span><span class="sxs-lookup"><span data-stu-id="04ade-135">hello following command will stream hello log files of your function app toohello command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="04ade-136">PowerShell로 함수 앱 로그 파일 모니터링</span><span class="sxs-lookup"><span data-stu-id="04ade-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="04ade-137">시작 tooget [Azure PowerShell 설치 및 구성](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-137">tooget started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="04ade-138">Azure 계정 hello 다음 명령을 실행 하 여 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-138">Add your Azure account by running hello following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="04ade-139">여러 구독이 있는 경우 목록으로 만들면 이름별으로 구독은 현재 선택 된 hello 올바른 hello 기반으로 하는 경우 명령 toosee 다음 hello로 `IsCurrent` 속성:</span><span class="sxs-lookup"><span data-stu-id="04ade-139">If you have multiple subscriptions, you can list them by name with hello following command toosee if hello correct subscription is hello currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="04ade-140">Tooset hello 활성 구독 toohello 함수 앱을 포함 해야 할 경우 다음 명령을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-140">If you need tooset hello active subscription toohello one containing your function app, use hello following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="04ade-141">스트림 hello 다음 명령을 hello로 tooyour PowerShell 세션을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-141">Stream hello logs tooyour PowerShell session with hello following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="04ade-142">자세한 내용은 참조 너무[하는 방법: 웹 응용 프로그램에 대 한 로그 스트림](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs)합니다.</span><span class="sxs-lookup"><span data-stu-id="04ade-142">For more information refer too[How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="04ade-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04ade-143">Next steps</span></span>
<span data-ttu-id="04ade-144">자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="04ade-144">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="04ade-145">기능 테스트</span><span class="sxs-lookup"><span data-stu-id="04ade-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="04ade-146">기능 크기 조정</span><span class="sxs-lookup"><span data-stu-id="04ade-146">Scale a function</span></span>](functions-scale.md)

