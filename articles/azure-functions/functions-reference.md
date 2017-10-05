---
title: "Azure Functions 개발 지침 | Microsoft Docs"
description: "프로그래밍 언어 및 바인딩에 관계 없이 Azure에서 함수를 개발하는 데 필요한 Azure Functions 개념 및 기술에 대해 알아봅니다."
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
ms.openlocfilehash: 879be48150cfe13e31064475aa637f13f5f5f9d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-developers-guide"></a><span data-ttu-id="76c95-104">Azure Functions 개발자 가이드</span><span class="sxs-lookup"><span data-stu-id="76c95-104">Azure Functions developers guide</span></span>
<span data-ttu-id="76c95-105">Azure Functions에서 특정 함수는 사용하는 언어나 바인딩에 관계없이 몇 가지 핵심적 기술 개념과 구성 요소를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-105">In Azure Functions, specific functions share a few core technical concepts and components, regardless of the language or binding you use.</span></span> <span data-ttu-id="76c95-106">특정 언어나 바인딩에 해당하는 세부 정보를 학습하기 전에, 모든 항목에 해당하는 이 개요를 꼼꼼히 읽어 보시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-106">Before you jump into learning details specific to a given language or binding, be sure to read through this overview that applies to all of them.</span></span>

<span data-ttu-id="76c95-107">이 문서에서는 [Azure Functions 개요](functions-overview.md)를 이미 읽었고 [트리거, 바인딩, JobHost 런타임 같은 WebJobs SDK 개념](../app-service-web/websites-dotnet-webjobs-sdk.md)에 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-107">This article assumes that you've already read the [Azure Functions overview](functions-overview.md) and are familiar with [WebJobs SDK concepts such as triggers, bindings, and the JobHost runtime](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span> <span data-ttu-id="76c95-108">Azure Functions는 WebJobs SDK를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-108">Azure Functions is based on the WebJobs SDK.</span></span> 

## <a name="function-code"></a><span data-ttu-id="76c95-109">함수 코드</span><span class="sxs-lookup"><span data-stu-id="76c95-109">Function code</span></span>
<span data-ttu-id="76c95-110">*함수* 는 Azure Functions의 기본 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-110">A *function* is the primary concept in Azure Functions.</span></span> <span data-ttu-id="76c95-111">원하는 언어로 함수 코드를 작성하고 코드와 구성 파일을 같은 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-111">You write code for a function in a language of your choice and save the code and configuration files in the same folder.</span></span> <span data-ttu-id="76c95-112">구성의 이름은 `function.json`이며 JSON 구성 데이터가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-112">The configuration is named `function.json`, which contains JSON configuration data.</span></span> <span data-ttu-id="76c95-113">다양한 언어가 지원되며, 각각의 언어에는 해당 언어에 맞춰 가장 잘 작동하도록 최적화된 약간 다른 환경이 갖춰져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-113">Various languages are supported, and each one has a slightly different experience optimized to work best for that language.</span></span> 

<span data-ttu-id="76c95-114">function.json 파일은 함수 바인딩 및 기타 구성 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-114">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="76c95-115">런타임은 이 파일을 사용하여 모니터링할 이벤트와 함수 실행에서 데이터를 전달하고 반환하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-115">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="76c95-116">다음은 function.json 파일의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-116">The following is an example function.json file.</span></span>

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

<span data-ttu-id="76c95-117">함수가 실행되지 않도록 `disabled` 속성을 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-117">Set the `disabled` property to `true` to prevent the function from being executed.</span></span>

<span data-ttu-id="76c95-118">`bindings` 속성은 트리거와 바인딩을 모두 구성하는 곳에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-118">The `bindings` property is where you configure both triggers and bindings.</span></span> <span data-ttu-id="76c95-119">각 바인딩은 몇 가지 공통적인 설정과 특정 바인딩 형식에 해당하는 일부 설정을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-119">Each binding shares a few common settings and some settings, which are specific to a particular type of binding.</span></span> <span data-ttu-id="76c95-120">모든 바인딩에는 다음 설정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-120">Every binding requires the following settings:</span></span>

| <span data-ttu-id="76c95-121">속성</span><span class="sxs-lookup"><span data-stu-id="76c95-121">Property</span></span> | <span data-ttu-id="76c95-122">값/형식</span><span class="sxs-lookup"><span data-stu-id="76c95-122">Values/Types</span></span> | <span data-ttu-id="76c95-123">설명</span><span class="sxs-lookup"><span data-stu-id="76c95-123">Comments</span></span> |
| --- | --- | --- |
| `type` |<span data-ttu-id="76c95-124">string</span><span class="sxs-lookup"><span data-stu-id="76c95-124">string</span></span> |<span data-ttu-id="76c95-125">바인딩 형식</span><span class="sxs-lookup"><span data-stu-id="76c95-125">Binding type.</span></span> <span data-ttu-id="76c95-126">예: `queueTrigger`</span><span class="sxs-lookup"><span data-stu-id="76c95-126">For example, `queueTrigger`.</span></span> |
| `direction` |<span data-ttu-id="76c95-127">'in', 'out'</span><span class="sxs-lookup"><span data-stu-id="76c95-127">'in', 'out'</span></span> |<span data-ttu-id="76c95-128">함수 안으로 데이터를 수신할 바인딩인지 또는 함수의 데이터를 전송할 바인딩인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-128">Indicates whether the binding is for receiving data into the function or sending data from the function.</span></span> |
| `name` |<span data-ttu-id="76c95-129">string</span><span class="sxs-lookup"><span data-stu-id="76c95-129">string</span></span> |<span data-ttu-id="76c95-130">함수에서 바인딩 데이터에 사용되는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-130">The name that is used for the bound data in the function.</span></span> <span data-ttu-id="76c95-131">C#의 경우 인수 이름이며, JavaScript의 경우 키/값 목록의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-131">For C#, this is an argument name; for JavaScript, it's the key in a key/value list.</span></span> |

## <a name="function-app"></a><span data-ttu-id="76c95-132">함수 앱</span><span class="sxs-lookup"><span data-stu-id="76c95-132">Function app</span></span>
<span data-ttu-id="76c95-133">함수 앱은 Azure 앱 서비스에서 함께 관리되는 하나 이상의 개별 함수 함수로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-133">A function app is comprised of one or more individual functions that are managed together by Azure App Service.</span></span> <span data-ttu-id="76c95-134">함수 앱의 모든 함수는 동일한 가격 책정 계획, 연속 배포 및 런타임 버전을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-134">All of the functions in a function app share the same pricing plan, continuous deployment and runtime version.</span></span> <span data-ttu-id="76c95-135">여러 언어로 작성된 함수는 동일한 함수 앱을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-135">Functions written in multiple languages can all share the same function app.</span></span> <span data-ttu-id="76c95-136">함수 앱을 함수를 구성하고 전체적으로 관리하는 방법으로 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-136">Think of a function app as a way to organize and collectively manage your functions.</span></span> 

## <a name="runtime-script-host-and-web-host"></a><span data-ttu-id="76c95-137">런타임(스크립트 호스트 및 웹 호스트)</span><span class="sxs-lookup"><span data-stu-id="76c95-137">Runtime (script host and web host)</span></span>
<span data-ttu-id="76c95-138">런타임 또는 스크립트 호스트는 이벤트를 수신하고, 데이터를 수집하여 보내고, 최종적으로 코드를 실행하는 기본 WebJobs SDK 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-138">The runtime, or script host, is the underlying WebJobs SDK host that listens for events, gathers and sends data, and ultimately runs your code.</span></span> 

<span data-ttu-id="76c95-139">HTTP 트리거를 용이하게 하기 위해 프로덕션 시나리오에서 스크립트 호스트 앞에 위치하도록 설계된 웹 호스트도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-139">To facilitate HTTP triggers, there is also a web host that is designed to sit in front of the script host in production scenarios.</span></span> <span data-ttu-id="76c95-140">두 개의 호스트가 있으면 웹 호스트에서 관리하는 프런트 엔드 트래픽에서 스크립트 호스트를 격리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-140">Having two hosts helps to isolate the script host from the front end traffic managed by the web host.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="76c95-141">폴더 구조</span><span class="sxs-lookup"><span data-stu-id="76c95-141">Folder Structure</span></span>
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

<span data-ttu-id="76c95-142">Azure 앱 서비스에서 함수를 함수 앱에 배포하기 위한 프로젝트를 설정하는 경우에는, 이 폴더 구조를 사용자의 사이트 코드로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-142">When setting-up a project for deploying functions to a function app in Azure App Service, you can treat this folder structure as your site code.</span></span> <span data-ttu-id="76c95-143">배포 시 패키지 설치 또는 코드 transpilation 수행을 위하여 지속적인 통합 및 배포 같은 기존 툴 또는 사용자 지정 배포 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-143">You can use existing tools like continuous integration and deployment, or custom deployment scripts for doing deploy time package installation or code transpilation.</span></span>

> [!NOTE]
> <span data-ttu-id="76c95-144">`host.json` 파일과 함수 폴더를 `wwwroot` 폴더에 직접 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-144">Make sure to deploy your `host.json` file and function folders directly to the `wwwroot` folder.</span></span> <span data-ttu-id="76c95-145">배포에 `wwwroot` 폴더를 포함하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="76c95-145">Do not include the `wwwroot` folder in your deployments.</span></span> <span data-ttu-id="76c95-146">그렇지 않으면 `wwwroot\wwwroot` 폴더가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-146">Otherwise, you end up with `wwwroot\wwwroot` folders.</span></span> 
> 
> 

## <span data-ttu-id="76c95-147"><a id="fileupdate"></a> 함수 앱 파일을 업데이트하는 방법</span><span class="sxs-lookup"><span data-stu-id="76c95-147"><a id="fileupdate"></a> How to update function app files</span></span>
<span data-ttu-id="76c95-148">Azure 포털에 기본 제공되는 함수 편집기를 사용하면 함수에 대한 코드 파일 및 *function.json* 파일을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-148">The function editor built into the Azure portal lets you update the *function.json* file and the code file for a function.</span></span> <span data-ttu-id="76c95-149">*package.json* 또는 *project.json* 또는 종속성 등의 다른 파일을 업로드하거나 업데이트하려면 다른 배포 방법을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-149">To upload or update other files such as *package.json* or *project.json* or dependencies, you have to use other deployment methods.</span></span>

<span data-ttu-id="76c95-150">함수 앱은 App Service를 기반으로 하므로 [표준 웹앱에 사용할 수 있는 배포 옵션](../app-service-web/web-sites-deploy.md)을 함수 앱에 모두 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-150">Function apps are built on App Service, so all the [deployment options available to standard web apps](../app-service-web/web-sites-deploy.md) are also available for function apps.</span></span> <span data-ttu-id="76c95-151">함수 앱 파일을 업로드하거나 업데이트하는 데 사용할 수 있는 방법이 몇 가지 입니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-151">Here are some methods you can use to upload or update function app files.</span></span> 

#### <a name="to-use-app-service-editor"></a><span data-ttu-id="76c95-152">앱 서비스 편집기 사용하기</span><span class="sxs-lookup"><span data-stu-id="76c95-152">To use App Service Editor</span></span>
1. <span data-ttu-id="76c95-153">Azure Functions 포털에서 **함수 앱 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-153">In the Azure Functions portal, click **Function app settings**.</span></span>
2. <span data-ttu-id="76c95-154">**고급 설정** 섹션에서 **App Service 설정으로 이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-154">In the **Advanced Settings** section, click **Go to App Service Settings**.</span></span>
3. <span data-ttu-id="76c95-155">**개발 도구** 아래 앱 메뉴 탐색 창에서 **App Service 편집기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-155">Click **App Service Editor** in App Menu Nav under **DEVELOPMENT TOOLS**.</span></span>
4. <span data-ttu-id="76c95-156">**이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-156">click **Go**.</span></span>
   
   <span data-ttu-id="76c95-157">App Service 편집기가 로드된 후에 *host.json* 파일과 *wwwroot* 하위의 함수 폴더를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-157">After App Service Editor loads, you'll see the *host.json* file and function folders under *wwwroot*.</span></span> 
5. <span data-ttu-id="76c95-158">파일을 열어서 편집하거나, 배포 컴퓨터에서 끌어서 놓기로 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-158">Open files to edit them, or drag and drop from your development machine to upload files.</span></span>

#### <a name="to-use-the-function-apps-scm-kudu-endpoint"></a><span data-ttu-id="76c95-159">함수 앱의 SCM(Kudu) 끝점을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="76c95-159">To use the function app's SCM (Kudu) endpoint</span></span>
1. <span data-ttu-id="76c95-160">`https://<function_app_name>.scm.azurewebsites.net`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-160">Navigate to: `https://<function_app_name>.scm.azurewebsites.net`.</span></span>
2. <span data-ttu-id="76c95-161">**디버그 콘솔 > CMD**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-161">Click **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="76c95-162">`D:\home\site\wwwroot\`으로 이동하여 *host.json*을 업데이트하거나 `D:\home\site\wwwroot\<function_name>`로 이동하여 함수 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-162">Navigate to `D:\home\site\wwwroot\` to update *host.json* or `D:\home\site\wwwroot\<function_name>` to update a function's files.</span></span>
4. <span data-ttu-id="76c95-163">파일 그리드에서 적절한 폴더로 업로드할 파일을 끌어서 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-163">Drag-and-drop a file you want to upload into the appropriate folder in the file grid.</span></span> <span data-ttu-id="76c95-164">파일을 삭제할 수 있는 파일 표에는 두 가지 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-164">There are two areas in the file grid where you can drop a file.</span></span> <span data-ttu-id="76c95-165">*.zip* 파일의 경우 "여기에 끌어 와서 업로드하고 압축을 풉니다" 레이블이 있는 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-165">For *.zip* files, a box appears with the label "Drag here to upload and unzip."</span></span> <span data-ttu-id="76c95-166">다른 파일 형식의 경우 "압축" 상자 외부에 파일 표를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-166">For other file types, drop in the file grid but outside the "unzip" box.</span></span>

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on the consumption plan --DonnaM -->

#### <a name="to-use-continuous-deployment"></a><span data-ttu-id="76c95-167">연속 배포를 사용하려면</span><span class="sxs-lookup"><span data-stu-id="76c95-167">To use continuous deployment</span></span>
<span data-ttu-id="76c95-168">[Azure Functions에 대한 연속 배포](functions-continuous-deployment.md)항목의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-168">Follow the instructions in the topic [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span>

## <a name="parallel-execution"></a><span data-ttu-id="76c95-169">병렬 실행</span><span class="sxs-lookup"><span data-stu-id="76c95-169">Parallel execution</span></span>
<span data-ttu-id="76c95-170">복수의 트리거 이벤트가 단일 스레드 함수 런타임이 해당 이벤트를 처리할 수 있는 속도보다 빨리 발생하면 런타임은 병렬 모드로 함수를 여러 번 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-170">When multiple triggering events occur faster than a single-threaded function runtime can process them, the runtime may invoke the function multiple times in parallel.</span></span>  <span data-ttu-id="76c95-171">함수 앱이 [소비 호스팅 계획](functions-scale.md#how-the-consumption-plan-works)을 사용하는 경우 함수 앱은 자동으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-171">If a function app is using the [Consumption hosting plan](functions-scale.md#how-the-consumption-plan-works), the function app could scale out automatically.</span></span>  <span data-ttu-id="76c95-172">앱이 소비 호스팅 계획 또는 일반 [App Service 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)에서 실행되는지 여부에 관계없이 함수 앱의 각 인스턴스는 여러 스레드를 사용하여 동시 함수 호출을 병렬로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-172">Each instance of the function app, whether the app runs on the Consumption hosting plan or a regular [App Service hosting plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), might process concurrent function invocations in parallel using multiple threads.</span></span>  <span data-ttu-id="76c95-173">각 함수 앱 인스턴스의 최대 동시 함수 호출 수는 함수 앱 내의 다른 함수에서 사용하는 리소스뿐만 아니라 사용 중인 트리거 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-173">The maximum number of concurrent function invocations in each function app instance varies based on the type of trigger being used as well as the resources used by other functions within the function app.</span></span>

## <a name="functions-runtime-versioning"></a><span data-ttu-id="76c95-174">Functions 런타임 버전 관리</span><span class="sxs-lookup"><span data-stu-id="76c95-174">Functions runtime versioning</span></span>

<span data-ttu-id="76c95-175">`FUNCTIONS_EXTENSION_VERSION` 앱 설정을 사용하여 Functions 런타임의 버전을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-175">You can configure the version of the Functions runtime using the `FUNCTIONS_EXTENSION_VERSION` app setting.</span></span> <span data-ttu-id="76c95-176">예를 들어 “”~1은 함수 앱이 주요 버전으로 1을 사용한다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-176">For example, the value "~1" indicates that your Function App will use 1 as its major version.</span></span> <span data-ttu-id="76c95-177">함수 앱은 부 버전이 새로 릴리스될 때마다 업그레이드됩니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-177">Function Apps are upgraded to each new minor version as they are released.</span></span> <span data-ttu-id="76c95-178">Azure Portal의 **설정** 탭에서 함수 앱의 정확한 버전을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-178">You can view the exact version of your Function App in the **Settings** tab in the Azure Portal.</span></span>

## <a name="repositories"></a><span data-ttu-id="76c95-179">리포지토리</span><span class="sxs-lookup"><span data-stu-id="76c95-179">Repositories</span></span>
<span data-ttu-id="76c95-180">Azure Functions에 대한 코드는 공개 소스이며 GitHub 리포지토리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-180">The code for Azure Functions is open source and stored in GitHub repositories:</span></span>

* [<span data-ttu-id="76c95-181">Azure Functions 런타임</span><span class="sxs-lookup"><span data-stu-id="76c95-181">Azure Functions runtime</span></span>](https://github.com/Azure/azure-webjobs-sdk-script/)
* [<span data-ttu-id="76c95-182">Azure Functions 포털</span><span class="sxs-lookup"><span data-stu-id="76c95-182">Azure Functions portal</span></span>](https://github.com/projectkudu/AzureFunctionsPortal)
* [<span data-ttu-id="76c95-183">Azure Functions 템플릿</span><span class="sxs-lookup"><span data-stu-id="76c95-183">Azure Functions templates</span></span>](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [<span data-ttu-id="76c95-184">Azure WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="76c95-184">Azure WebJobs SDK</span></span>](https://github.com/Azure/azure-webjobs-sdk/)
* [<span data-ttu-id="76c95-185">Azure WebJobs SDK 확장</span><span class="sxs-lookup"><span data-stu-id="76c95-185">Azure WebJobs SDK Extensions</span></span>](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a><span data-ttu-id="76c95-186">바인딩</span><span class="sxs-lookup"><span data-stu-id="76c95-186">Bindings</span></span>
<span data-ttu-id="76c95-187">지원되는 모든 바인딩을 포함하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="76c95-187">Here is a table of all supported bindings.</span></span>

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a><span data-ttu-id="76c95-188">문제 보고</span><span class="sxs-lookup"><span data-stu-id="76c95-188">Reporting Issues</span></span>
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a><span data-ttu-id="76c95-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76c95-189">Next steps</span></span>
<span data-ttu-id="76c95-190">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76c95-190">For more information, see the following resources:</span></span>

* [<span data-ttu-id="76c95-191">Azure Functions에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="76c95-191">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="76c95-192">Azure Functions C# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="76c95-192">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="76c95-193">Azure Functions F# 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="76c95-193">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="76c95-194">Azure Functions NodeJS 개발자 참조</span><span class="sxs-lookup"><span data-stu-id="76c95-194">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="76c95-195">Azure Functions 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="76c95-195">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* <span data-ttu-id="76c95-196">[Azure Functions: Azure 앱 서비스](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) 팀 블로그 과정.</span><span class="sxs-lookup"><span data-stu-id="76c95-196">[Azure Functions: The Journey](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) on the Azure App Service team blog.</span></span> <span data-ttu-id="76c95-197">Azure Functions 개발에 대한 기록</span><span class="sxs-lookup"><span data-stu-id="76c95-197">A history of how Azure Functions was developed.</span></span>

