---
title: "Azure Functions 모니터링 | Microsoft 문서"
description: "Azure Functions를 모니터링하는 방법에 대해 알아봅니다."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure 함수, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="8cb6e-104">Azure Functions 모니터링</span><span class="sxs-lookup"><span data-stu-id="8cb6e-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="8cb6e-105">개요</span><span class="sxs-lookup"><span data-stu-id="8cb6e-105">Overview</span></span> 


<span data-ttu-id="8cb6e-106">각 함수에 대한 **모니터** 탭을 사용하면 함수의 각 실행을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-106">The **Monitor** tab for each function allows you to review each execution of a function.</span></span>

![Azure Functions 모니터 탭](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="8cb6e-108">실행을 클릭하면 기간, 입력 데이터, 오류 및 관련 로그 파일을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="8cb6e-109">이 탭은 함수를 디버그하고 성능을 조정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="8cb6e-110">Azure Functions에 [소비 호스팅 계획](functions-overview.md#pricing)을 사용하는 경우 함수 앱 개요 블레이드의 **모니터링** 타일에서 데이터를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span></span> <span data-ttu-id="8cb6e-111">이는 플랫폼에서 계산 인스턴스를 동적으로 확장하고 관리하여 이러한 메트릭이 소비 계획에서 의미가 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="8cb6e-112">함수 앱의 사용을 모니터링하려면 이 문서의 지침을 대신 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span></span>
> 
> <span data-ttu-id="8cb6e-113">다음 스크린샷에서는 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-113">The following screen-shot shows an example:</span></span>
> 
> ![기본 리소스 블레이드에서 모니터링](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="8cb6e-115">실시간 모니터링</span><span class="sxs-lookup"><span data-stu-id="8cb6e-115">Real-time monitoring</span></span>

<span data-ttu-id="8cb6e-116">아래와 같이 **라이브 이벤트 스트림**을 클릭하면 실시간 모니터링을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![모니터 탭의 라이브 이벤트 스트림 옵션](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="8cb6e-118">라이브 이벤트 스트림은 아래와 같이 새 브라우저 탭에서 그래프로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-118">The live event stream will be graphed in a new browser tab as shown below.</span></span> 

![라이브 이벤트 스트림 예제](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="8cb6e-120">데이터를 채우지 못하게 하는 알려진 문제점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-120">There is a known issue that may cause your data to fail to be populated.</span></span> <span data-ttu-id="8cb6e-121">이 문제가 발생하면 라이브 이벤트 스트림을 포함하고 있는 브라우저 탭을 닫은 다음 **라이브 이벤트 스트림**을 다시 클릭하여 이벤트 스트림 데이터를 제대로 채울 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span></span> 

<span data-ttu-id="8cb6e-122">라이브 이벤트 스트림은 함수에 대한 다음 통계를 그래프로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-122">The live event stream will graph the following statistics for your function:</span></span>

* <span data-ttu-id="8cb6e-123">초당 시작된 실행</span><span class="sxs-lookup"><span data-stu-id="8cb6e-123">Executions started per second</span></span>
* <span data-ttu-id="8cb6e-124">초당 완료된 실행</span><span class="sxs-lookup"><span data-stu-id="8cb6e-124">Executions completed per second</span></span>
* <span data-ttu-id="8cb6e-125">초당 실패한 실행</span><span class="sxs-lookup"><span data-stu-id="8cb6e-125">Executions failed per second</span></span>
* <span data-ttu-id="8cb6e-126">평균 실행 시간(밀리초)</span><span class="sxs-lookup"><span data-stu-id="8cb6e-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="8cb6e-127">이러한 통계는 실시간이지만 실행 데이터의 실제 그래프표시에는 약 10초의 대기 시간이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="8cb6e-128">명령줄에서 로그 파일 모니터링</span><span class="sxs-lookup"><span data-stu-id="8cb6e-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="8cb6e-129">Azure CLI(Command Line Interface) 또는 PowerShell을 사용하여 로그 파일을 로컬 워크스테이션의 명령줄 세션으로 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a><span data-ttu-id="8cb6e-130">Azure CLI로 함수 앱 로그 파일 모니터링</span><span class="sxs-lookup"><span data-stu-id="8cb6e-130">Monitoring function app log files with the Azure CLI</span></span>

<span data-ttu-id="8cb6e-131">시작하려면 [Azure CLI를 설치](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="8cb6e-132">다음 명령 또는 [Azure CLI에서 Azure에 로그인](../xplat-cli-connect.md)에 나오는 다른 옵션을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="8cb6e-133">다음 명령을 사용하여 ASM(Azure CLI Service Management) 모드를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="8cb6e-134">구독이 여러 개인 경우 다음 명령을 사용하여 구독을 나열하고 현재 구독을 함수 앱이 포함된 구독으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="8cb6e-135">다음 명령은 함수 앱의 로그 파일을 명령줄로 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-135">The following command will stream the log files of your function app to the command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="8cb6e-136">PowerShell로 함수 앱 로그 파일 모니터링</span><span class="sxs-lookup"><span data-stu-id="8cb6e-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="8cb6e-137">시작하려면 [Azure PowerShell을 설치 및 구성](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-137">To get started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="8cb6e-138">다음 명령을 실행하여 Azure 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-138">Add your Azure account by running the following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="8cb6e-139">구독이 여러 개인 경우 다음 명령으로 구독을 나열하여 `IsCurrent` 속성에 따라 올바른 구독이 현재 선택되어 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="8cb6e-140">활성 구독을 함수 앱을 포함하고 있는 구독으로 설정해야 하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-140">If you need to set the active subscription to the one containing your function app, use the following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="8cb6e-141">다음 명령을 사용하여 로그를 PowerShell 세션으로 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-141">Stream the logs to your PowerShell session with the following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="8cb6e-142">자세한 내용은 [방법: 웹앱의 로그 스트리밍](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8cb6e-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8cb6e-143">Next steps</span></span>
<span data-ttu-id="8cb6e-144">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cb6e-144">For more information, see the following resources:</span></span>

* [<span data-ttu-id="8cb6e-145">기능 테스트</span><span class="sxs-lookup"><span data-stu-id="8cb6e-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="8cb6e-146">기능 크기 조정</span><span class="sxs-lookup"><span data-stu-id="8cb6e-146">Scale a function</span></span>](functions-scale.md)

