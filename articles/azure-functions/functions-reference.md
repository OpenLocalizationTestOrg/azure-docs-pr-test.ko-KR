---
title: "Azure 기능을 개발 하는 것에 대 한 aaaGuidance | Microsoft Docs"
description: "Hello Azure 함수 개념과 모든 프로그래밍 언어 및 바인딩을 통해 azure에서 toodevelop 함수 해야 하는 기술에 알아봅니다."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "개발자 가이드, Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a><span data-ttu-id="e9d03-104">Azure Functions 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="e9d03-104">Azure Functions developers guide</span></span>
<span data-ttu-id="e9d03-105">Azure 함수에서 특정 기능 몇 가지 핵심 기술 개념 및 hello 언어 또는 바인딩 사용에 관계 없이 구성 요소를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-105">In Azure Functions, specific functions share a few core technical concepts and components, regardless of hello language or binding you use.</span></span> <span data-ttu-id="e9d03-106">지정 된 언어 또는 바인딩 세부 정보 특정 tooa 학습에 대해 알아보기, 그중에서 tooall 적용 되는이 개요를 통해 있는지 tooread 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-106">Before you jump into learning details specific tooa given language or binding, be sure tooread through this overview that applies tooall of them.</span></span>

<span data-ttu-id="e9d03-107">이 문서에서는 hello 이미 읽어본 가정 [Azure 함수 개요](functions-overview.md) 익숙하지 [트리거, 바인딩 및 hello JobHost 런타임 같은 WebJobs SDK 개념](../app-service-web/websites-dotnet-webjobs-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-107">This article assumes that you've already read hello [Azure Functions overview](functions-overview.md) and are familiar with [WebJobs SDK concepts such as triggers, bindings, and hello JobHost runtime](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span> <span data-ttu-id="e9d03-108">Azure 함수 hello WebJobs SDK를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-108">Azure Functions is based on hello WebJobs SDK.</span></span> 

## <a name="function-code"></a><span data-ttu-id="e9d03-109">함수 코드</span><span class="sxs-lookup"><span data-stu-id="e9d03-109">Function code</span></span>
<span data-ttu-id="e9d03-110">A *함수* 는 hello Azure 함수에서 기본 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-110">A *function* is hello primary concept in Azure Functions.</span></span> <span data-ttu-id="e9d03-111">사용자가 선택한 언어는 함수에 대 한 코드를 작성 하 고 hello 코드를 저장 및 구성 파일에서 같은 폴더 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-111">You write code for a function in a language of your choice and save hello code and configuration files in hello same folder.</span></span> <span data-ttu-id="e9d03-112">hello 구성의 이름은 `function.json`, JSON 구성 데이터가 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-112">hello configuration is named `function.json`, which contains JSON configuration data.</span></span> <span data-ttu-id="e9d03-113">다양 한 언어를 지원 하 고 각 옵션에 약간 다른 환경에 최적화 된 toowork 해당 언어에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-113">Various languages are supported, and each one has a slightly different experience optimized toowork best for that language.</span></span> 

<span data-ttu-id="e9d03-114">hello function.json 파일 hello 함수 바인딩 및 기타 구성 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-114">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="e9d03-115">hello 런타임은이 파일 toodetermine hello 이벤트 toomonitor 및 toopass 데이터를 한 반환 데이터에서 실행이 작동 방식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-115">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="e9d03-116">hello 다음은 function.json 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-116">hello following is an example function.json file.</span></span>

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

<span data-ttu-id="e9d03-117">집합 hello `disabled` 속성 너무`true` tooprevent hello 함수 실행 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-117">Set hello `disabled` property too`true` tooprevent hello function from being executed.</span></span>

<span data-ttu-id="e9d03-118">hello `bindings` 속성은 트리거와 바인딩을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-118">hello `bindings` property is where you configure both triggers and bindings.</span></span> <span data-ttu-id="e9d03-119">각 바인딩에 몇 가지 일반 설정 및 특정 tooa 특정 유형의 바인딩 일부 설정을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-119">Each binding shares a few common settings and some settings, which are specific tooa particular type of binding.</span></span> <span data-ttu-id="e9d03-120">모든 바인딩에 hello를 설정을 다음 사항이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-120">Every binding requires hello following settings:</span></span>

| <span data-ttu-id="e9d03-121">속성</span><span class="sxs-lookup"><span data-stu-id="e9d03-121">Property</span></span> | <span data-ttu-id="e9d03-122">값/형식</span><span class="sxs-lookup"><span data-stu-id="e9d03-122">Values/Types</span></span> | <span data-ttu-id="e9d03-123">설명</span><span class="sxs-lookup"><span data-stu-id="e9d03-123">Comments</span></span> |
| --- | --- | --- |
| `type` |<span data-ttu-id="e9d03-124">string</span><span class="sxs-lookup"><span data-stu-id="e9d03-124">string</span></span> |<span data-ttu-id="e9d03-125">바인딩 형식</span><span class="sxs-lookup"><span data-stu-id="e9d03-125">Binding type.</span></span> <span data-ttu-id="e9d03-126">예: `queueTrigger`</span><span class="sxs-lookup"><span data-stu-id="e9d03-126">For example, `queueTrigger`.</span></span> |
| `direction` |<span data-ttu-id="e9d03-127">'in', 'out'</span><span class="sxs-lookup"><span data-stu-id="e9d03-127">'in', 'out'</span></span> |<span data-ttu-id="e9d03-128">Hello 바인딩이 hello 함수에 데이터를 받기 또는 hello 함수에서 데이터를 보내는 지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-128">Indicates whether hello binding is for receiving data into hello function or sending data from hello function.</span></span> |
| `name` |<span data-ttu-id="e9d03-129">string</span><span class="sxs-lookup"><span data-stu-id="e9d03-129">string</span></span> |<span data-ttu-id="e9d03-130">hello 함수에 데이터 바인딩된 하는 hello에 사용 되는 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-130">hello name that is used for hello bound data in hello function.</span></span> <span data-ttu-id="e9d03-131">C#의 경우이 프로그램 인수 이름입니다. JavaScript 용 hello 키/값 목록에는 키의 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-131">For C#, this is an argument name; for JavaScript, it's hello key in a key/value list.</span></span> |

## <a name="function-app"></a><span data-ttu-id="e9d03-132">함수 앱</span><span class="sxs-lookup"><span data-stu-id="e9d03-132">Function app</span></span>
<span data-ttu-id="e9d03-133">함수 앱은 Azure 앱 서비스에서 함께 관리되는 하나 이상의 개별 함수 함수로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-133">A function app is comprised of one or more individual functions that are managed together by Azure App Service.</span></span> <span data-ttu-id="e9d03-134">모든 함수 앱 공유에서 hello 함수 hello 같은 가격 계획, 지속적인 배포 및 런타임 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-134">All of hello functions in a function app share hello same pricing plan, continuous deployment and runtime version.</span></span> <span data-ttu-id="e9d03-135">함수 hello를 공유 하는 모든으로 여러 언어로 작성 된 응용 프로그램을 작동 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-135">Functions written in multiple languages can all share hello same function app.</span></span> <span data-ttu-id="e9d03-136">방법은 tooorganize로 함수 응용 프로그램의 생각 하 고 전체적으로 프로그램 기능을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-136">Think of a function app as a way tooorganize and collectively manage your functions.</span></span> 

## <a name="runtime-script-host-and-web-host"></a><span data-ttu-id="e9d03-137">런타임(스크립트 호스트 및 웹 호스트)</span><span class="sxs-lookup"><span data-stu-id="e9d03-137">Runtime (script host and web host)</span></span>
<span data-ttu-id="e9d03-138">hello 런타임 또는 스크립트 호스트는 이벤트를 수신, 수집 및 데이터를 보냅니다 및 궁극적으로 코드를 실행 하는 hello 원본으로 사용 하는 WebJobs SDK 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-138">hello runtime, or script host, is hello underlying WebJobs SDK host that listens for events, gathers and sends data, and ultimately runs your code.</span></span> 

<span data-ttu-id="e9d03-139">HTTP toofacilitate 트리거 디자인 된 toosit hello 스크립트 호스트 프로덕션 시나리오에서 앞에 있는 웹 호스트 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-139">toofacilitate HTTP triggers, there is also a web host that is designed toosit in front of hello script host in production scenarios.</span></span> <span data-ttu-id="e9d03-140">호스트 두 개 있으면 hello 웹 호스트에서 관리 하는 hello 프런트 엔드 트래픽에서 tooisolate hello 스크립트 호스트는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-140">Having two hosts helps tooisolate hello script host from hello front end traffic managed by hello web host.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="e9d03-141">폴더 구조</span><span class="sxs-lookup"><span data-stu-id="e9d03-141">Folder Structure</span></span>
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

<span data-ttu-id="e9d03-142">때 함수 tooa 함수 응용 Azure 앱 서비스의 배포에 대 한 프로젝트 설정에, 사이트 코드와이 폴더 구조를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-142">When setting-up a project for deploying functions tooa function app in Azure App Service, you can treat this folder structure as your site code.</span></span> <span data-ttu-id="e9d03-143">배포 시 패키지 설치 또는 코드 transpilation 수행을 위하여 지속적인 통합 및 배포 같은 기존 툴 또는 사용자 지정 배포 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-143">You can use existing tools like continuous integration and deployment, or custom deployment scripts for doing deploy time package installation or code transpilation.</span></span>

> [!NOTE]
> <span data-ttu-id="e9d03-144">있는지 toodeploy 확인 프로그램 `host.json` 파일과 함수 폴더 직접 toohello `wwwroot` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-144">Make sure toodeploy your `host.json` file and function folders directly toohello `wwwroot` folder.</span></span> <span data-ttu-id="e9d03-145">Hello를 넣지 마십시오 `wwwroot` 폴더에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-145">Do not include hello `wwwroot` folder in your deployments.</span></span> <span data-ttu-id="e9d03-146">그렇지 않으면 `wwwroot\wwwroot` 폴더가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-146">Otherwise, you end up with `wwwroot\wwwroot` folders.</span></span> 
> 
> 

## <span data-ttu-id="e9d03-147"><a id="fileupdate"></a>Tooupdate 앱 파일을 작동 하는 방법</span><span class="sxs-lookup"><span data-stu-id="e9d03-147"><a id="fileupdate"></a> How tooupdate function app files</span></span>
<span data-ttu-id="e9d03-148">hello Azure 포털에 내장 된 hello 함수 편집기를 사용 하면 hello 업데이트 *function.json* 파일 및 함수에 대 한 hello 코드 파일.</span><span class="sxs-lookup"><span data-stu-id="e9d03-148">hello function editor built into hello Azure portal lets you update hello *function.json* file and hello code file for a function.</span></span> <span data-ttu-id="e9d03-149">tooupload 또는 다른 업데이트와 같은 파일 *package.json* 또는 *project.json* 또는 종속성을 다른 배포 방법 toouse 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-149">tooupload or update other files such as *package.json* or *project.json* or dependencies, you have toouse other deployment methods.</span></span>

<span data-ttu-id="e9d03-150">기능 앱은 기반으로 앱 서비스 하므로 모든 hello [배포 옵션을 사용할 수 있는 toostandard 웹 앱](../app-service-web/web-sites-deploy.md) 기능 앱에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-150">Function apps are built on App Service, so all hello [deployment options available toostandard web apps](../app-service-web/web-sites-deploy.md) are also available for function apps.</span></span> <span data-ttu-id="e9d03-151">다음은 일부 방법 tooupload 사용 하거나 함수 응용 프로그램 파일을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-151">Here are some methods you can use tooupload or update function app files.</span></span> 

#### <a name="toouse-app-service-editor"></a><span data-ttu-id="e9d03-152">toouse 응용 프로그램 서비스 편집기</span><span class="sxs-lookup"><span data-stu-id="e9d03-152">toouse App Service Editor</span></span>
1. <span data-ttu-id="e9d03-153">Hello 함수 Azure 포털에서 클릭 **앱 설정 작동**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-153">In hello Azure Functions portal, click **Function app settings**.</span></span>
2. <span data-ttu-id="e9d03-154">Hello에 **고급 설정** 섹션에서 클릭 **tooApp 서비스 설정 이동**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-154">In hello **Advanced Settings** section, click **Go tooApp Service Settings**.</span></span>
3. <span data-ttu-id="e9d03-155">**개발 도구** 아래 앱 메뉴 탐색 창에서 **App Service 편집기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-155">Click **App Service Editor** in App Menu Nav under **DEVELOPMENT TOOLS**.</span></span>
4. <span data-ttu-id="e9d03-156">**이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-156">click **Go**.</span></span>
   
   <span data-ttu-id="e9d03-157">서비스 응용 프로그램 편집기를 로드 한 후 표시 hello *host.json* 아래에 있는 파일 및 함수 폴더 *wwwroot*합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-157">After App Service Editor loads, you'll see hello *host.json* file and function folders under *wwwroot*.</span></span> 
5. <span data-ttu-id="e9d03-158">열려 있는 파일 tooedit, 또는에서 끌어서 놓기 development 컴퓨터 tooupload 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-158">Open files tooedit them, or drag and drop from your development machine tooupload files.</span></span>

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a><span data-ttu-id="e9d03-159">toouse hello 함수 응용 프로그램의 SCM (Kudu) 끝점</span><span class="sxs-lookup"><span data-stu-id="e9d03-159">toouse hello function app's SCM (Kudu) endpoint</span></span>
1. <span data-ttu-id="e9d03-160">`https://<function_app_name>.scm.azurewebsites.net`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-160">Navigate to: `https://<function_app_name>.scm.azurewebsites.net`.</span></span>
2. <span data-ttu-id="e9d03-161">**디버그 콘솔 > CMD**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-161">Click **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="e9d03-162">너무 이동`D:\home\site\wwwroot\` tooupdate *host.json* 또는 `D:\home\site\wwwroot\<function_name>` tooupdate 함수의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-162">Navigate too`D:\home\site\wwwroot\` tooupdate *host.json* or `D:\home\site\wwwroot\<function_name>` tooupdate a function's files.</span></span>
4. <span data-ttu-id="e9d03-163">Tooupload hello hello 파일 표에서 적절 한 폴더에 파일을 끌어서 드롭.</span><span class="sxs-lookup"><span data-stu-id="e9d03-163">Drag-and-drop a file you want tooupload into hello appropriate folder in hello file grid.</span></span> <span data-ttu-id="e9d03-164">두 가지 영역을 hello 파일 표에서 파일을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-164">There are two areas in hello file grid where you can drop a file.</span></span> <span data-ttu-id="e9d03-165">에 대 한 *.zip* 파일 hello 레이블을 사용 하는 상자가 나타납니다. "여기 tooupload 끌어서의 압축을 풉니다."</span><span class="sxs-lookup"><span data-stu-id="e9d03-165">For *.zip* files, a box appears with hello label "Drag here tooupload and unzip."</span></span> <span data-ttu-id="e9d03-166">다른 파일 형식에 대 한 hello "의 압축을 푸는" 상자 외부에 있으면 서 hello 파일 눈금에서 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-166">For other file types, drop in hello file grid but outside hello "unzip" box.</span></span>

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a><span data-ttu-id="e9d03-167">toouse 연속 배포</span><span class="sxs-lookup"><span data-stu-id="e9d03-167">toouse continuous deployment</span></span>
<span data-ttu-id="e9d03-168">Hello 항목의 지침을 hello [Azure 함수에 대 한 연속 배포](functions-continuous-deployment.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-168">Follow hello instructions in hello topic [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span>

## <a name="parallel-execution"></a><span data-ttu-id="e9d03-169">병렬 실행</span><span class="sxs-lookup"><span data-stu-id="e9d03-169">Parallel execution</span></span>
<span data-ttu-id="e9d03-170">여러 개의 트리거 이벤트가 함수가 단일 스레드 런타임 처리할 수 있는 것 보다 빠르게 발생할 때 hello 런타임 동시에 여러 번 hello 함수를 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-170">When multiple triggering events occur faster than a single-threaded function runtime can process them, hello runtime may invoke hello function multiple times in parallel.</span></span>  <span data-ttu-id="e9d03-171">함수 앱 hello를 사용 하는 경우 [호스팅 계획 소비](functions-scale.md#how-the-consumption-plan-works), hello 함수 앱 자동으로 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-171">If a function app is using hello [Consumption hosting plan](functions-scale.md#how-the-consumption-plan-works), hello function app could scale out automatically.</span></span>  <span data-ttu-id="e9d03-172">Hello 함수 응용 프로그램의 각 인스턴스에 hello 앱 실행 하는지 hello 호스팅 계획 또는 일반 소비 [앱 서비스 계획을 호스팅](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), 여러 스레드를 사용 하 여 병렬로 동시 함수 호출을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-172">Each instance of hello function app, whether hello app runs on hello Consumption hosting plan or a regular [App Service hosting plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), might process concurrent function invocations in parallel using multiple threads.</span></span>  <span data-ttu-id="e9d03-173">각 함수 응용 프로그램 인스턴스에서 동시 함수 호출의 최대 수 hello hello 함수 앱 내에서 다른 함수에서 사용 하는 hello 리소스와 마찬가지로 잘 사용 되 고 트리거 hello 유형을에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-173">hello maximum number of concurrent function invocations in each function app instance varies based on hello type of trigger being used as well as hello resources used by other functions within hello function app.</span></span>

## <a name="functions-runtime-versioning"></a><span data-ttu-id="e9d03-174">Functions 런타임 버전 관리</span><span class="sxs-lookup"><span data-stu-id="e9d03-174">Functions runtime versioning</span></span>

<span data-ttu-id="e9d03-175">Hello 런타임 버전을 hello 함수 hello를 사용 하 여 구성할 수 있습니다 `FUNCTIONS_EXTENSION_VERSION` 앱 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-175">You can configure hello version of hello Functions runtime using hello `FUNCTIONS_EXTENSION_VERSION` app setting.</span></span> <span data-ttu-id="e9d03-176">예를 들어 hello 값 "~ 1" 함수에서 사용 하는 앱으로 사용 하 여 1의 주 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-176">For example, hello value "~1" indicates that your Function App will use 1 as its major version.</span></span> <span data-ttu-id="e9d03-177">출시 되는 함수 앱은 업그레이드 된 tooeach 새 부 버전.</span><span class="sxs-lookup"><span data-stu-id="e9d03-177">Function Apps are upgraded tooeach new minor version as they are released.</span></span> <span data-ttu-id="e9d03-178">Hello에 hello 함수 응용 프로그램의 정확한 버전을 볼 수 있습니다 **설정을** hello Azure 포털에서에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-178">You can view hello exact version of your Function App in hello **Settings** tab in hello Azure Portal.</span></span>

## <a name="repositories"></a><span data-ttu-id="e9d03-179">리포지토리</span><span class="sxs-lookup"><span data-stu-id="e9d03-179">Repositories</span></span>
<span data-ttu-id="e9d03-180">Azure 기능에 대 한 hello 코드는 오픈 소스 이며 GitHub 리포지토리에 저장:</span><span class="sxs-lookup"><span data-stu-id="e9d03-180">hello code for Azure Functions is open source and stored in GitHub repositories:</span></span>

* [<span data-ttu-id="e9d03-181">Azure Functions 런타임</span><span class="sxs-lookup"><span data-stu-id="e9d03-181">Azure Functions runtime</span></span>](https://github.com/Azure/azure-webjobs-sdk-script/)
* [<span data-ttu-id="e9d03-182">Azure Functions 포털</span><span class="sxs-lookup"><span data-stu-id="e9d03-182">Azure Functions portal</span></span>](https://github.com/projectkudu/AzureFunctionsPortal)
* [<span data-ttu-id="e9d03-183">Azure Functions 템플릿</span><span class="sxs-lookup"><span data-stu-id="e9d03-183">Azure Functions templates</span></span>](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [<span data-ttu-id="e9d03-184">Azure WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="e9d03-184">Azure WebJobs SDK</span></span>](https://github.com/Azure/azure-webjobs-sdk/)
* [<span data-ttu-id="e9d03-185">Azure WebJobs SDK 확장</span><span class="sxs-lookup"><span data-stu-id="e9d03-185">Azure WebJobs SDK Extensions</span></span>](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a><span data-ttu-id="e9d03-186">바인딩</span><span class="sxs-lookup"><span data-stu-id="e9d03-186">Bindings</span></span>
<span data-ttu-id="e9d03-187">지원되는 모든 바인딩을 포함하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-187">Here is a table of all supported bindings.</span></span>

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a><span data-ttu-id="e9d03-188">문제 보고</span><span class="sxs-lookup"><span data-stu-id="e9d03-188">Reporting Issues</span></span>
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a><span data-ttu-id="e9d03-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9d03-189">Next steps</span></span>
<span data-ttu-id="e9d03-190">자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="e9d03-190">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="e9d03-191">Azure Functions에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="e9d03-191">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="e9d03-192">Azure Functions C# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="e9d03-192">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="e9d03-193">Azure Functions F# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="e9d03-193">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="e9d03-194">Azure Functions NodeJS 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="e9d03-194">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="e9d03-195">Azure Functions 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="e9d03-195">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* <span data-ttu-id="e9d03-196">[Azure 함수: hello 여행](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) hello Azure 앱 서비스 팀 블로그에 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d03-196">[Azure Functions: hello Journey](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) on hello Azure App Service team blog.</span></span> <span data-ttu-id="e9d03-197">Azure Functions 개발에 대한 기록</span><span class="sxs-lookup"><span data-stu-id="e9d03-197">A history of how Azure Functions was developed.</span></span>

