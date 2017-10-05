---
title: "스트리밍 로그 및 콘솔"
description: "스트리밍 로그 및 콘솔 개요"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: 120ce6b115820728b9f853e9ff349beb0ef29c9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="streaming-logs-and-the-console"></a><span data-ttu-id="14b33-103">스트리밍 로그 및 콘솔</span><span class="sxs-lookup"><span data-stu-id="14b33-103">Streaming Logs and the Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="14b33-104">스트리밍 로그</span><span class="sxs-lookup"><span data-stu-id="14b33-104">Streaming Logs</span></span>
<span data-ttu-id="14b33-105">**Azure Portal**은 통합 스트리밍 로그 뷰어를 제공하며, 이 뷰어에서 **App Service** 앱의 추적 이벤트를 실시간으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-105">The **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="14b33-106">이 기능을 설정하려면 몇 가지 간단한 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="14b33-107">코드에 추적 쓰기</span><span class="sxs-lookup"><span data-stu-id="14b33-107">Write traces in your code</span></span>
* <span data-ttu-id="14b33-108">앱에 대해 응용 프로그램 **진단 로그**를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="14b33-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="14b33-109">**Azure portal**의 기본 제공 **스트리밍 로그** UI에서 스트림을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-109">View the stream from the built-in **Streaming Logs** UI in the **Azure portal**.</span></span>

### <a name="how-to-write-traces-in-your-code"></a><span data-ttu-id="14b33-110">코드에서 추적을 쓰는 방법</span><span class="sxs-lookup"><span data-stu-id="14b33-110">How to write traces in your code</span></span>
<span data-ttu-id="14b33-111">코드에 추적을 쓰는 작업은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="14b33-112">C#에서는 다음 코드를 쓰기만 하면 될 정도로 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-112">In C# it's as easy as writing the following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="14b33-113">The Trace class lives in the System.Diagnostics namespace.</span><span class="sxs-lookup"><span data-stu-id="14b33-113">The Trace class lives in the System.Diagnostics namespace.</span></span>

<span data-ttu-id="14b33-114">node.js 앱에서는 다음 코드를 쓰면 동일한 결과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-114">In a node.js app you can write this code to achieve the same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a><span data-ttu-id="14b33-115">스트리밍 로그를 사용하고 보는 방법</span><span class="sxs-lookup"><span data-stu-id="14b33-115">How to enable and view the streaming logs</span></span>
<span data-ttu-id="14b33-116">![][BrowseSitesScreenshot] 진단은 앱별로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="14b33-117">이 기능을 사용하도록 설정할 사이트로 이동하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-117">Start by browsing to the site you would like to enable this feature on.</span></span>  

<span data-ttu-id="14b33-118">![][DiagnosticsLogs] 설정 메뉴에서 **모니터링** 섹션으로 스크롤하고 **(1) 진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-118">![][DiagnosticsLogs] From settings menu, scroll down to the **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="14b33-119">그런 다음 **응용 프로그램 로깅(파일 시스템)** 또는 **응용 프로그램 로깅(blob)**을 **(2) 활성화**합니다. **수준** 옵션을 통해 캡처할 추적의 심각도 수준을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** The **Level** option lets you change the severity level of traces to capture.</span></span> <span data-ttu-id="14b33-120">**세부 정보 표시**는 모든 추적 스트리밍을 수집하므로, 이 기능에 익숙해지고 싶으면 이 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-120">If you're just trying to get familiar with the feature, set the level to **Verbose** to ensure all of your trace statements are collected.</span></span>

<span data-ttu-id="14b33-121">블레이드의 위에 있는 **저장** 을 클릭하면 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-121">Click **SAVE** at the top of the blade and you're ready to view logs.</span></span>

> [!NOTE]
> <span data-ttu-id="14b33-122">더 높은 **심각도 수준**을 설정하면 로그에 더 많은 리소스를 사용하여 더 상세한 추적이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-122">The higher the **severity level** the more resources are consumed to log and the more traces are produced.</span></span> <span data-ttu-id="14b33-123">**심각도 수준**이 프로덕션 또는 높은 트래픽 사이트에 대해 적절한 세부 정보 표시로 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-123">Make sure **severity level** is configured to the correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="14b33-124">![][StreamingLogsScreenshot] Azure Portal 내에서 **스트리밍 로그**를 보려면 설정 메뉴의 **모니터링** 섹션에서 **(1) 로그 스트림**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-124">![][StreamingLogsScreenshot] To view the **streaming logs** from within the Azure portal, click on **(1) Log Stream** also in the **Monitoring** section of the settings menu.</span></span> <span data-ttu-id="14b33-125">앱에서 추적 문을 활발하게 쓰는 경우 **(2) 스트리밍 로그 UI**에서 거의 실시간으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-125">If your app is actively writing trace statements, then you should see them in the **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="14b33-126">콘솔</span><span class="sxs-lookup"><span data-stu-id="14b33-126">Console</span></span>
<span data-ttu-id="14b33-127">**Azure Portal**에서는 앱에 대한 콘솔 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-127">The **Azure portal** provides console access to your app.</span></span> <span data-ttu-id="14b33-128">앱의 파일 시스템을 탐색하고 powershell/cmd 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="14b33-129">콘솔 명령을 실행할 때 실행 중인 앱 코드와 동일한 권한 집합이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-129">You are bound by the same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="14b33-130">보호된 디렉터리에 대한 액세스 또는 관리자 권한이 필요한 스크립트 실행은 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-130">Access to protected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="14b33-131">![][ConsoleScreenshot] 설정 메뉴에서 **개발 도구** 섹션으로 스크롤하고 **(1) 콘솔**을 클릭하면 **(2) 콘솔** UI가 오른쪽에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="14b33-131">![][ConsoleScreenshot] From settings menu, scroll down to **Development Tools** section and click on **(1) Console** and the **(2) console** UI opens to the right.</span></span>

<span data-ttu-id="14b33-132">**콘솔**에 친숙해지려면 다음과 같은 기본 명령을 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="14b33-132">To get familiar with the **console**, try basic commands like:</span></span>

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
