---
title: "로컬로 Azure Functions 개발 및 실행 | Microsoft Docs"
description: "Azure Functions에서 실행하기 전에 로컬 컴퓨터에서 Azure Functions를 코딩 및 테스트하는 방법을 알아봅니다."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: bbe03973dbd7c70463caa6d1a45efae2ec722c05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="c30a6-103">Azure Functions를 로컬로 코딩 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c30a6-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="c30a6-104">[Azure Portal]에 Azure Functions 개발 및 테스트를 위한 도구가 완벽히 제공되지만 많은 개발자는 지역 개발 환경을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-104">While the [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="c30a6-105">Azure Functions를 사용하면 원하는 코드 편집기와 로컬 개발 도구를 쉽게 사용하여 로컬 컴퓨터에서 함수를 개발하고 테스트 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-105">Azure Functions makes it easy to use your favorite code editor and local development tools to develop and test your functions on your local computer.</span></span> <span data-ttu-id="c30a6-106">함수로 Azure에서 이벤트를 트리거할 수 있으며 로컬 컴퓨터에서 C# 및 JavaScript 함수를 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="c30a6-107">Visual Studio C# 개발자인 경우 Azure Functions은 [Visual Studio 2017과도 통합](functions-develop-vs.md)됩니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-the-azure-functions-core-tools"></a><span data-ttu-id="c30a6-108">Azure Functions 핵심 도구 설치</span><span class="sxs-lookup"><span data-stu-id="c30a6-108">Install the Azure Functions Core Tools</span></span>

<span data-ttu-id="c30a6-109">Azure Functions 핵심 도구는 로컬 Windows 컴퓨터에서 실행할 수 있는 Azure Functions 런타임의 로컬 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-109">Azure Functions Core Tools is a local version of the Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="c30a6-110">에뮬레이터 또는 시뮬레이터가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="c30a6-111">Azure에서 Functions를 작동하는 것과 동일한 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-111">It's the same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="c30a6-112">[Azure Functions 핵심 도구]는 npm 패키지로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-112">The [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="c30a6-113">먼저 npm이 포함된 [NodeJS를 설치](https://docs.npmjs.com/getting-started/installing-node)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="c30a6-114">현재 Azure Functions 핵심 도구 패키지는 Windows 컴퓨터에만 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-114">At this time, the Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="c30a6-115">이 제한은 Functions 호스트의 임시 제한 사항 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-115">This restriction is due to a temporary limitation in the Functions host.</span></span>

<span data-ttu-id="c30a6-116">[Azure Functions 핵심 도구]는 다음 명령 별칭을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-116">[Azure Functions Core Tools] adds the following command aliases:</span></span>
* <span data-ttu-id="c30a6-117">**func**</span><span class="sxs-lookup"><span data-stu-id="c30a6-117">**func**</span></span>
* <span data-ttu-id="c30a6-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="c30a6-118">**azfun**</span></span>
* <span data-ttu-id="c30a6-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="c30a6-119">**azurefunctions**</span></span>

<span data-ttu-id="c30a6-120">이러한 별칭은 모두 이 문서의 예제에 표시된 `func` 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-120">All of these alias can be used instead of `func` shown in the examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="c30a6-121">로컬 Functions 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c30a6-121">Create a local Functions project</span></span>

<span data-ttu-id="c30a6-122">로컬로 실행하는 경우 Functions 프로젝트는 host.json 및 local.settings.json 파일이 있는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-122">When running locally, a Functions project is a directory that has the files host.json and local.settings.json.</span></span> <span data-ttu-id="c30a6-123">이 디렉터리는 Azure의 함수 앱에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-123">This directory is the equivalent of a function app in Azure.</span></span> <span data-ttu-id="c30a6-124">Azure Functions 폴더 구조에 대한 자세한 내용은 [Azure Functions 개발자 가이드](functions-reference.md#folder-structure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c30a6-124">To learn more about the Azure Functions folder structure, see the [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="c30a6-125">명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-125">At a command prompt, run the following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="c30a6-126">출력은 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-126">The output looks like the following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="c30a6-127">Git 리포지토리 만들기를 옵트아웃하려면 `--no-source-control [-n]` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-127">To opt out of creating a Git repository, use the option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="c30a6-128">로컬 설정 파일</span><span class="sxs-lookup"><span data-stu-id="c30a6-128">Local settings file</span></span>

<span data-ttu-id="c30a6-129">local.settings.json 파일은 앱 설정, 연결 문자열 및 Azure Functions 핵심 도구에 대한 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-129">The file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="c30a6-130">구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-130">It has the following structure:</span></span>

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| <span data-ttu-id="c30a6-131">설정</span><span class="sxs-lookup"><span data-stu-id="c30a6-131">Setting</span></span>      | <span data-ttu-id="c30a6-132">설명</span><span class="sxs-lookup"><span data-stu-id="c30a6-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="c30a6-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="c30a6-133">**IsEncrypted**</span></span> | <span data-ttu-id="c30a6-134">**true**로 설정하면 모든 값은 로컬 컴퓨터 키를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-134">When set to **true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="c30a6-135">`func settings` 명령과 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-135">Used with `func settings` commands.</span></span> <span data-ttu-id="c30a6-136">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-136">Default value is **false**.</span></span> |
| <span data-ttu-id="c30a6-137">**값**</span><span class="sxs-lookup"><span data-stu-id="c30a6-137">**Values**</span></span> | <span data-ttu-id="c30a6-138">로컬에서 실행될 때 사용되는 응용 프로그램 설정의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="c30a6-139">이 개체에 응용 프로그램 설정을 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="c30a6-139">Add your application settings to this object.</span></span>  |
| <span data-ttu-id="c30a6-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="c30a6-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="c30a6-141">Azure Functions 런타임에서 내부적으로 사용되는 Azure Storage 계정에 연결 문자열을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-141">Sets the connection string to the Azure Storage account that is used internally by the Azure Functions runtime.</span></span> <span data-ttu-id="c30a6-142">저장소 계정은 함수의 트리거를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-142">The storage account supports your function's triggers.</span></span> <span data-ttu-id="c30a6-143">이 저장소 계정 연결 설정은 HTTP 트리거 함수를 제외한 모든 함수에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="c30a6-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="c30a6-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="c30a6-145">함수 로그를 저장하는 데 사용되는 Azure Storage 계정에 연결 문자열을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-145">Sets the connection string to the Azure Storage account that is used to store the function logs.</span></span> <span data-ttu-id="c30a6-146">이 선택적 값을 사용하면 포털에서 로그에 액세스 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-146">This optional value makes the logs accessible in the portal.</span></span>|
| <span data-ttu-id="c30a6-147">**호스트**</span><span class="sxs-lookup"><span data-stu-id="c30a6-147">**Host**</span></span> | <span data-ttu-id="c30a6-148">이 섹션의 설정은 로컬에서 실행할 때 Functions 호스트 프로세스를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-148">Settings in this section customize the Functions host process when running locally.</span></span> | 
| <span data-ttu-id="c30a6-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="c30a6-149">**LocalHttpPort**</span></span> | <span data-ttu-id="c30a6-150">로컬 Functions 호스트(`func host start` 및 `func run`)를 실행할 때 사용되는 기본 포트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-150">Sets the default port used when running the local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="c30a6-151">`--port` 명령줄 옵션이 이 값보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-151">The `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="c30a6-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="c30a6-152">**CORS**</span></span> | <span data-ttu-id="c30a6-153">[CORS(원본 간 리소스 공유)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)에 허용된 원본을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-153">Defines the origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="c30a6-154">원본은 공백 없이 쉼표로 구분된 목록으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="c30a6-155">와일드카드 값(**\***)이 지원되므로 모든 원본에서 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-155">The wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="c30a6-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="c30a6-156">**ConnectionStrings**</span></span> | <span data-ttu-id="c30a6-157">함수에 대한 데이터베이스 연결 문자열을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-157">Contains the database connection strings for your functions.</span></span> <span data-ttu-id="c30a6-158">이 개체의 연결 문자열은 공급자 유형이 **System.Data.SqlClient**인 환경에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-158">Connection strings in this object are added to the environment with the provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="c30a6-159">대부분의 트리거와 바인딩에는 환경 변수 또는 앱 설정의 이름에 매핑되는 **연결** 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-159">Most triggers and bindings have a **Connection** property that maps to the name of an environment variable or app setting.</span></span> <span data-ttu-id="c30a6-160">각 연결 속성에 대해 local.settings.json 파일에 정의된 앱 설정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="c30a6-161">이러한 설정은 코드에서 환경 변수로 읽을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="c30a6-162">C#에서는 [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) 또는 [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="c30a6-163">JavaScript에서는 `process.env`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="c30a6-164">시스템 환경 변수로 지정된 설정은 local.settings.json 파일의 값보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-164">Settings specified as a system environment variable take precedence over values in the local.settings.json file.</span></span> 

<span data-ttu-id="c30a6-165">local.settings.json 파일의 설정은 로컬에서 실행할 때 Functions 도구에서만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-165">Settings in the local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="c30a6-166">기본적으로 이러한 설정은 프로젝트가 Azure에 게시될 때 자동으로 마이그레이션되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-166">By default, these settings are not migrated automatically when the project is published to Azure.</span></span> <span data-ttu-id="c30a6-167">[게시할 때](#publish) `--publish-local-settings` 스위치를 사용하여 이러한 설정이 Azure의 함수 앱에 추가되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-167">Use the `--publish-local-settings` switch [when you publish](#publish) to make sure these settings are added to the function app in Azure.</span></span>

<span data-ttu-id="c30a6-168">**AzureWebJobsStorage**에 유효한 저장소 연결 문자열이 설정되어 있지 않으면 다음 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-168">When no valid storage connection string is set for **AzureWebJobsStorage**, the following error message is shown:</span></span>  

><span data-ttu-id="c30a6-169">local.settings.json에 AzureWebJobsStorage 값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="c30a6-170">이 값은 HTTP 이외의 모든 트리거에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="c30a6-171">'func azure functionary fetch-app-settings <functionAppName>'을 실행하거나 local.settings.json에 연결 문자열을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="c30a6-172">앱 설정 구성</span><span class="sxs-lookup"><span data-stu-id="c30a6-172">Configure app settings</span></span>

<span data-ttu-id="c30a6-173">연결 문자열 값을 설정하려면 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-173">To set a value for connection strings, you can do one of the following:</span></span>
* <span data-ttu-id="c30a6-174">[Azure Storage 탐색기](http://storageexplorer.com/)에서 연결 문자열을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-174">Enter the connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="c30a6-175">다음 중 하나의 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-175">Use one of the following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="c30a6-176">두 명령 모두 먼저 Azure에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-176">Both commands require you to first sign-in to Azure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="c30a6-177">함수 만들기</span><span class="sxs-lookup"><span data-stu-id="c30a6-177">Create a function</span></span>

<span data-ttu-id="c30a6-178">함수를 만들려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-178">To create a function, run the following command:</span></span>

```
func new
``` 
<span data-ttu-id="c30a6-179">`func new`는 다음 선택적 인수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-179">`func new` supports the following optional arguments:</span></span>

| <span data-ttu-id="c30a6-180">인수</span><span class="sxs-lookup"><span data-stu-id="c30a6-180">Argument</span></span>     | <span data-ttu-id="c30a6-181">설명</span><span class="sxs-lookup"><span data-stu-id="c30a6-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="c30a6-182">C#, F# 또는 JavaScript와 같은 템플릿 프로그래밍 언어</span><span class="sxs-lookup"><span data-stu-id="c30a6-182">The template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="c30a6-183">템플릿 이름</span><span class="sxs-lookup"><span data-stu-id="c30a6-183">The template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="c30a6-184">함수 이름</span><span class="sxs-lookup"><span data-stu-id="c30a6-184">The function name.</span></span> |

<span data-ttu-id="c30a6-185">예를 들어 JavaScript HTTP 트리거를 만들려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-185">For example, to create a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="c30a6-186">큐 트리거 함수를 만들려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-186">To create a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="c30a6-187">로컬로 함수 실행</span><span class="sxs-lookup"><span data-stu-id="c30a6-187">Run functions locally</span></span>

<span data-ttu-id="c30a6-188">Functions 프로젝트를 실행하려면 Functions 호스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-188">To run a Functions project, run the Functions host.</span></span> <span data-ttu-id="c30a6-189">이 호스트는 프로젝트의 모든 함수에 대한 트리거를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-189">The host enables triggers for all functions in the project:</span></span>

```
func host start
```

<span data-ttu-id="c30a6-190">`func host start`는 다음 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-190">`func host start` supports the following options:</span></span>

| <span data-ttu-id="c30a6-191">옵션</span><span class="sxs-lookup"><span data-stu-id="c30a6-191">Option</span></span>     | <span data-ttu-id="c30a6-192">설명</span><span class="sxs-lookup"><span data-stu-id="c30a6-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="c30a6-193">수신 대기할 로컬 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-193">The local port to listen on.</span></span> <span data-ttu-id="c30a6-194">기본값: 7071</span><span class="sxs-lookup"><span data-stu-id="c30a6-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="c30a6-195">옵션은 `VSCode` 및 `VS`입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-195">The options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="c30a6-196">CORS 원본의 공백 없이 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="c30a6-197">사용할 노드 디버거의 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-197">The port for the node debugger to use.</span></span> <span data-ttu-id="c30a6-198">기본값: launch.json 값 또는 5858</span><span class="sxs-lookup"><span data-stu-id="c30a6-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="c30a6-199">콘솔 추적 수준입니다(해제, 자세한 정보 표시, 정보, 경고 또는 오류).</span><span class="sxs-lookup"><span data-stu-id="c30a6-199">The console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="c30a6-200">기본값: 정보</span><span class="sxs-lookup"><span data-stu-id="c30a6-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="c30a6-201">Functions 호스트를 시작할 제한 시간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-201">The time out for the Functions host t     o start, in seconds.</span></span> <span data-ttu-id="c30a6-202">기본값: 20초</span><span class="sxs-lookup"><span data-stu-id="c30a6-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="c30a6-203">http://localhost:{port}가 아니라 https://localhost:{port}에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-203">Bind to https://localhost:{port} rather than to http://localhost:{port}.</span></span> <span data-ttu-id="c30a6-204">기본적으로 이 옵션은 사용자 컴퓨터에 신뢰할 수 있는 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="c30a6-205">프로세스를 종료하기 전에 추가 입력에 대해 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-205">Pause for additional input before exiting the process.</span></span> <span data-ttu-id="c30a6-206">IDE(통합 개발 환경)에서 Azure Functions 핵심 도구를 시작할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="c30a6-207">Functions 호스트가 시작되면 HTTP 트리거 함수의 URL이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-207">When the Functions host starts, it outputs the URL of HTTP-triggered functions:</span></span>

```
Found the following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="c30a6-208">VS 코드 또는 Visual Studio에서 디버그</span><span class="sxs-lookup"><span data-stu-id="c30a6-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="c30a6-209">디버거를 연결하려면 `--debug` 인수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-209">To attach a debugger, pass the `--debug` argument.</span></span> <span data-ttu-id="c30a6-210">JavaScript 함수를 디버그하려면 Visual Studio Code를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-210">To debug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="c30a6-211">C# 함수의 경우 Visual Studio를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="c30a6-212">C# 함수를 디버그하려면 `--debug vs`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-212">To debug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="c30a6-213">[Azure Functions Visual Studio 2017 도구](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/)를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="c30a6-214">호스트를 시작하고 JavaScript 디버깅을 설정하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-214">To launch the host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="c30a6-215">그런 다음 Visual Studio Code의 **디버그** 뷰에서 **Azure Functions에 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-215">Then, in Visual Studio Code, in the **Debug** view, select **Attach to Azure Functions**.</span></span> <span data-ttu-id="c30a6-216">중단점을 연결하고, 변수를 검사하고, 코드를 단계별로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Visual Studio Code를 사용한 JavaScript 디버깅](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-to-a-function"></a><span data-ttu-id="c30a6-218">테스트 데이터를 함수에 전달</span><span class="sxs-lookup"><span data-stu-id="c30a6-218">Passing test data to a function</span></span>

<span data-ttu-id="c30a6-219">`func run <FunctionName>`을 사용하여 함수를 직접 호출하고 함수에 대한 입력 데이터를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for the function.</span></span> <span data-ttu-id="c30a6-220">이 명령은 Azure Portal에서 **테스트** 탭을 사용하여 함수를 실행하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-220">This command is similar to running a function using the **Test** tab in the Azure portal.</span></span> <span data-ttu-id="c30a6-221">이 명령은 전체 Functions 호스트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-221">This command launches the entire Functions host.</span></span>

<span data-ttu-id="c30a6-222">`func run`은 다음 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-222">`func run` supports the following options:</span></span>

| <span data-ttu-id="c30a6-223">옵션</span><span class="sxs-lookup"><span data-stu-id="c30a6-223">Option</span></span>     | <span data-ttu-id="c30a6-224">설명</span><span class="sxs-lookup"><span data-stu-id="c30a6-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="c30a6-225">인라인 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="c30a6-226">함수를 실행하기 전에 호스트 프로세스에 디버거를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-226">Attach a debugger to the host process before running the function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="c30a6-227">로컬 Functions 호스트가 준비될 때까지의 대기 시간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-227">Time to wait (in seconds) until the local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="c30a6-228">콘텐츠로 사용할 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-228">The file name to use as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="c30a6-229">입력에 대한 메시지를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-229">Does not prompt for input.</span></span> <span data-ttu-id="c30a6-230">자동화 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="c30a6-231">예를 들어 HTTP 트리거 함수를 호출하고 콘텐츠 본문을 전달하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-231">For example, to call an HTTP-triggered function and pass content body, run the following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="c30a6-232"><a name="publish"></a>Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="c30a6-232"><a name="publish"></a>Publish to Azure</span></span>

<span data-ttu-id="c30a6-233">Azure의 함수 앱에 Functions 프로젝트를 게시하려면 `publish` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-233">To publish a Functions project to a function app in Azure, use the `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="c30a6-234">다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-234">You can use the following options:</span></span>

| <span data-ttu-id="c30a6-235">옵션</span><span class="sxs-lookup"><span data-stu-id="c30a6-235">Option</span></span>     | <span data-ttu-id="c30a6-236">설명</span><span class="sxs-lookup"><span data-stu-id="c30a6-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="c30a6-237">local.settings.json의 설정을 Azure에 게시하고, 설정이 이미 있는 경우 덮어쓸지 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-237">Publish settings in local.settings.json to Azure, prompting to overwrite if the setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="c30a6-238">`-i`와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-238">Must be used with `-i`.</span></span> <span data-ttu-id="c30a6-239">Azure의 AppSettings을 로컬 값으로 덮어씁니다(서로 다른 경우).</span><span class="sxs-lookup"><span data-stu-id="c30a6-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="c30a6-240">기본값은 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-240">Default is prompt.</span></span>|

<span data-ttu-id="c30a6-241">`publish` 명령은 Functions 프로젝트 디렉터리의 콘텐츠를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-241">The `publish` command uploads the contents of the Functions project directory.</span></span> <span data-ttu-id="c30a6-242">파일을 로컬로 삭제하는 경우 `publish` 명령은 Azure에서 해당 파일을 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-242">If you delete files locally, the `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="c30a6-243">[Azure Portal]에서 [Kudu 도구](functions-how-to-use-azure-function-app-settings.md#kudu)를 사용하여 Azure에서 파일을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-243">You can delete files in Azure by using the [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in the [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c30a6-244">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c30a6-244">Next steps</span></span>

<span data-ttu-id="c30a6-245">Azure Functions 핵심 도구는 [오픈 소스이며 GitHub에서 호스팅](https://github.com/azure/azure-functions-cli)됩니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="c30a6-246">버그 또는 기능 요청을 제출하려면 [GitHub 문제를 개설](https://github.com/azure/azure-functions-cli/issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="c30a6-246">To file a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[Azure Functions 핵심 도구]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure Portal]: https://portal.azure.com 
