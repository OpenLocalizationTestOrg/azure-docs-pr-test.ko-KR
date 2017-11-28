---
title: "aaaDevelop 및 실행된 Azure 로컬로 함수 | Microsoft Docs"
description: "Toocode 및 테스트 Azure 작동 방식을 로컬 컴퓨터에 Azure 함수에서 실행 하기 전에 알아봅니다."
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
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="5f502-103">Azure Functions를 로컬로 코딩 및 테스트</span><span class="sxs-lookup"><span data-stu-id="5f502-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="5f502-104">Hello 동안 [Azure 포털] 전체 개발을 위한 도구 집합 및 많은 개발자에 게 테스트 Azure 기능은 선호 로컬 개발 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-104">While hello [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="5f502-105">Azure 기능 쉽게 toouse를 사용 하면 즐겨 코드 편집기 및 로컬 개발 도구 toodevelop 및 로컬 컴퓨터에 함수를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-105">Azure Functions makes it easy toouse your favorite code editor and local development tools toodevelop and test your functions on your local computer.</span></span> <span data-ttu-id="5f502-106">함수로 Azure에서 이벤트를 트리거할 수 있으며 로컬 컴퓨터에서 C# 및 JavaScript 함수를 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="5f502-107">Visual Studio C# 개발자인 경우 Azure Functions은 [Visual Studio 2017과도 통합](functions-develop-vs.md)됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-hello-azure-functions-core-tools"></a><span data-ttu-id="5f502-108">Hello Azure 함수 핵심 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-108">Install hello Azure Functions Core Tools</span></span>

<span data-ttu-id="5f502-109">Azure 함수 핵심 도구는 로컬 Windows 컴퓨터에서 실행할 수 있는 hello Azure 함수 런타임의 로컬 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-109">Azure Functions Core Tools is a local version of hello Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="5f502-110">에뮬레이터 또는 시뮬레이터가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="5f502-111">같은 런타임 Azure 에서도 해당 powers hello에 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-111">It's hello same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="5f502-112">hello [Azure 함수 핵심 도구] npm 패키지로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-112">hello [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="5f502-113">먼저 npm이 포함된 [NodeJS를 설치](https://docs.npmjs.com/getting-started/installing-node)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="5f502-114">Hello Azure 함수 핵심 도구 패키지 이때 Windows 컴퓨터에 설치할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-114">At this time, hello Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="5f502-115">이 제한은 hello 함수 호스트에서 tooa 임시 제한 사항 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-115">This restriction is due tooa temporary limitation in hello Functions host.</span></span>

<span data-ttu-id="5f502-116">[Azure 함수 핵심 도구] hello 명령 별칭 뒤에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-116">[Azure Functions Core Tools] adds hello following command aliases:</span></span>
* <span data-ttu-id="5f502-117">**func**</span><span class="sxs-lookup"><span data-stu-id="5f502-117">**func**</span></span>
* <span data-ttu-id="5f502-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="5f502-118">**azfun**</span></span>
* <span data-ttu-id="5f502-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="5f502-119">**azurefunctions**</span></span>

<span data-ttu-id="5f502-120">이러한 별칭의 모든 대신 사용할 수 있습니다 `func` 이 항목의 hello 예제에 표시 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-120">All of these alias can be used instead of `func` shown in hello examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="5f502-121">로컬 Functions 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="5f502-121">Create a local Functions project</span></span>

<span data-ttu-id="5f502-122">로컬로 실행 하는 경우 함수 프로젝트 파일 host.json hello 및 local.settings.json 들어 있는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-122">When running locally, a Functions project is a directory that has hello files host.json and local.settings.json.</span></span> <span data-ttu-id="5f502-123">이 디렉터리는 Azure에서 함수 응용 프로그램의 해당 하는 hello는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-123">This directory is hello equivalent of a function app in Azure.</span></span> <span data-ttu-id="5f502-124">toolearn hello Azure 함수 폴더 구조에 대 한 자세한 참조 hello [Azure 함수 개발자 가이드](functions-reference.md#folder-structure)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-124">toolearn more about hello Azure Functions folder structure, see hello [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="5f502-125">명령 프롬프트에서 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-125">At a command prompt, run hello following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="5f502-126">hello 출력 hello 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-126">hello output looks like hello following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="5f502-127">Git 리포지토리, hello 옵션 사용을 만드는 tooopt `--no-source-control [-n]`합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-127">tooopt out of creating a Git repository, use hello option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="5f502-128">로컬 설정 파일</span><span class="sxs-lookup"><span data-stu-id="5f502-128">Local settings file</span></span>

<span data-ttu-id="5f502-129">hello 파일 local.settings.json 응용 프로그램 설정, 연결 문자열 및 Azure 함수 핵심 도구에 대 한 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-129">hello file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="5f502-130">Hello 구조를 따르는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-130">It has hello following structure:</span></span>

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
| <span data-ttu-id="5f502-131">설정</span><span class="sxs-lookup"><span data-stu-id="5f502-131">Setting</span></span>      | <span data-ttu-id="5f502-132">설명</span><span class="sxs-lookup"><span data-stu-id="5f502-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="5f502-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="5f502-133">**IsEncrypted**</span></span> | <span data-ttu-id="5f502-134">설정 된 경우 너무**true**, 모든 값은 로컬 컴퓨터 키를 사용 하 여 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-134">When set too**true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="5f502-135">`func settings` 명령과 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-135">Used with `func settings` commands.</span></span> <span data-ttu-id="5f502-136">기본값은 **false**입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-136">Default value is **false**.</span></span> |
| <span data-ttu-id="5f502-137">**값**</span><span class="sxs-lookup"><span data-stu-id="5f502-137">**Values**</span></span> | <span data-ttu-id="5f502-138">로컬에서 실행될 때 사용되는 응용 프로그램 설정의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="5f502-139">응용 프로그램 설정 toothis 개체를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-139">Add your application settings toothis object.</span></span>  |
| <span data-ttu-id="5f502-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="5f502-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="5f502-141">집합 hello 문자열 toohello hello Azure 함수 런타임에 의해 내부적으로 사용 되는 Azure 저장소 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-141">Sets hello connection string toohello Azure Storage account that is used internally by hello Azure Functions runtime.</span></span> <span data-ttu-id="5f502-142">hello 저장소 계정은 함수의 트리거를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-142">hello storage account supports your function's triggers.</span></span> <span data-ttu-id="5f502-143">이 저장소 계정 연결 설정은 HTTP 트리거 함수를 제외한 모든 함수에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="5f502-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="5f502-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="5f502-145">Hello 연결 문자열 toohello Azure 저장소 계정으로 사용 되는 toostore hello 기능 로그를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-145">Sets hello connection string toohello Azure Storage account that is used toostore hello function logs.</span></span> <span data-ttu-id="5f502-146">이 옵션 값은 hello 로그 hello 포털에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-146">This optional value makes hello logs accessible in hello portal.</span></span>|
| <span data-ttu-id="5f502-147">**호스트**</span><span class="sxs-lookup"><span data-stu-id="5f502-147">**Host**</span></span> | <span data-ttu-id="5f502-148">이 섹션의 설정을 로컬로 실행 하는 경우 hello 함수 호스트 프로세스를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-148">Settings in this section customize hello Functions host process when running locally.</span></span> | 
| <span data-ttu-id="5f502-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="5f502-149">**LocalHttpPort**</span></span> | <span data-ttu-id="5f502-150">집합 hello hello 로컬 함수 호스트를 실행할 때 사용 되는 기본 포트 (`func host start` 및 `func run`).</span><span class="sxs-lookup"><span data-stu-id="5f502-150">Sets hello default port used when running hello local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="5f502-151">hello `--port` 명령줄 옵션이이 값 보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-151">hello `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="5f502-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="5f502-152">**CORS**</span></span> | <span data-ttu-id="5f502-153">정의에 허용 되는 hello origin [크로스-원본 자원 공유 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-153">Defines hello origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="5f502-154">원본은 공백 없이 쉼표로 구분된 목록으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="5f502-155">와일드 카드 값 hello (**\***)은 지원의 모든 원본 요청을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-155">hello wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="5f502-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="5f502-156">**ConnectionStrings**</span></span> | <span data-ttu-id="5f502-157">함수에 대 한 hello 데이터베이스 연결 문자열을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-157">Contains hello database connection strings for your functions.</span></span> <span data-ttu-id="5f502-158">이 개체의 연결 문자열의 hello 공급자 형식과 toohello 환경 추가 **System.Data.SqlClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-158">Connection strings in this object are added toohello environment with hello provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="5f502-159">대부분의 트리거와 바인딩은는 **연결** 환경 변수 또는 응용 프로그램 설정의 toohello 이름을 매핑하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-159">Most triggers and bindings have a **Connection** property that maps toohello name of an environment variable or app setting.</span></span> <span data-ttu-id="5f502-160">각 연결 속성에 대해 local.settings.json 파일에 정의된 앱 설정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="5f502-161">이러한 설정은 코드에서 환경 변수로 읽을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="5f502-162">C#에서는 [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) 또는 [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="5f502-163">JavaScript에서는 `process.env`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="5f502-164">시스템 환경 변수로 지정 된 설정을 hello local.settings.json 파일의 값 보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-164">Settings specified as a system environment variable take precedence over values in hello local.settings.json file.</span></span> 

<span data-ttu-id="5f502-165">Hello local.settings.json 파일의 설정은 로컬로 실행 하는 경우에 함수 도구에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-165">Settings in hello local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="5f502-166">기본적으로 이러한 설정은 마이그레이션되지 않습니다 자동으로 hello 프로젝트가 게시 된 tooAzure 있을 때.</span><span class="sxs-lookup"><span data-stu-id="5f502-166">By default, these settings are not migrated automatically when hello project is published tooAzure.</span></span> <span data-ttu-id="5f502-167">사용 하 여 hello `--publish-local-settings` 전환 [게시 하는 경우](#publish) toomake 이러한 설정은 Azure에서 toohello 함수 앱 추가 되어 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-167">Use hello `--publish-local-settings` switch [when you publish](#publish) toomake sure these settings are added toohello function app in Azure.</span></span>

<span data-ttu-id="5f502-168">올바른 저장소 연결 문자열에 대해 설정 된 경우 **AzureWebJobsStorage**, hello 다음과 같은 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-168">When no valid storage connection string is set for **AzureWebJobsStorage**, hello following error message is shown:</span></span>  

><span data-ttu-id="5f502-169">local.settings.json에 AzureWebJobsStorage 값이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="5f502-170">이 값은 HTTP 이외의 모든 트리거에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="5f502-171">'func azure functionary fetch-app-settings <functionAppName>'을 실행하거나 local.settings.json에 연결 문자열을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="5f502-172">앱 설정 구성</span><span class="sxs-lookup"><span data-stu-id="5f502-172">Configure app settings</span></span>

<span data-ttu-id="5f502-173">연결 문자열에 대 한 값 tooset hello 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-173">tooset a value for connection strings, you can do one of hello following:</span></span>
* <span data-ttu-id="5f502-174">연결 문자열 hello 입력 [Azure 저장소 탐색기](http://storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-174">Enter hello connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="5f502-175">Hello 다음 명령 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-175">Use one of hello following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="5f502-176">두 명령 있습니다 toofirst 로그인 tooAzure 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-176">Both commands require you toofirst sign-in tooAzure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="5f502-177">함수 만들기</span><span class="sxs-lookup"><span data-stu-id="5f502-177">Create a function</span></span>

<span data-ttu-id="5f502-178">toocreate 함수 hello 다음 명령을 실행 하는 중:</span><span class="sxs-lookup"><span data-stu-id="5f502-178">toocreate a function, run hello following command:</span></span>

```
func new
``` 
<span data-ttu-id="5f502-179">`func new`hello 다음 선택적 인수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-179">`func new` supports hello following optional arguments:</span></span>

| <span data-ttu-id="5f502-180">인수</span><span class="sxs-lookup"><span data-stu-id="5f502-180">Argument</span></span>     | <span data-ttu-id="5f502-181">설명</span><span class="sxs-lookup"><span data-stu-id="5f502-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="5f502-182">프로그래밍 언어 C#, F #, JavaScript 등 hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="5f502-182">hello template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="5f502-183">hello 템플릿 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-183">hello template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="5f502-184">hello 함수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-184">hello function name.</span></span> |

<span data-ttu-id="5f502-185">예를 들어 toocreate JavaScript HTTP 트리거를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-185">For example, toocreate a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="5f502-186">toocreate 큐 트리거 함수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-186">toocreate a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="5f502-187">로컬로 함수 실행</span><span class="sxs-lookup"><span data-stu-id="5f502-187">Run functions locally</span></span>

<span data-ttu-id="5f502-188">toorun 함수 프로젝트 hello 함수 호스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-188">toorun a Functions project, run hello Functions host.</span></span> <span data-ttu-id="5f502-189">hello 호스트 hello 프로젝트의 모든 함수에 대 한 트리거를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-189">hello host enables triggers for all functions in hello project:</span></span>

```
func host start
```

<span data-ttu-id="5f502-190">`func host start`hello 다음 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-190">`func host start` supports hello following options:</span></span>

| <span data-ttu-id="5f502-191">옵션</span><span class="sxs-lookup"><span data-stu-id="5f502-191">Option</span></span>     | <span data-ttu-id="5f502-192">설명</span><span class="sxs-lookup"><span data-stu-id="5f502-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="5f502-193">hello에 로컬 포트 toolisten 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-193">hello local port toolisten on.</span></span> <span data-ttu-id="5f502-194">기본값: 7071</span><span class="sxs-lookup"><span data-stu-id="5f502-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="5f502-195">hello 옵션은 `VSCode` 및 `VS`합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-195">hello options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="5f502-196">CORS 원본의 공백 없이 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="5f502-197">노드 디버거 toouse hello에 대 한 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-197">hello port for hello node debugger toouse.</span></span> <span data-ttu-id="5f502-198">기본값: launch.json 값 또는 5858</span><span class="sxs-lookup"><span data-stu-id="5f502-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="5f502-199">hello 콘솔 추적 수준 (해제, verbose, 정보, 경고 또는 오류).</span><span class="sxs-lookup"><span data-stu-id="5f502-199">hello console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="5f502-200">기본값: 정보</span><span class="sxs-lookup"><span data-stu-id="5f502-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="5f502-201">시작에 대 한 hello 함수 호스트 t o, 초 단위로 hello 시간이 초과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-201">hello time out for hello Functions host t     o start, in seconds.</span></span> <span data-ttu-id="5f502-202">기본값: 20초</span><span class="sxs-lookup"><span data-stu-id="5f502-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="5f502-203">Toohttps://localhost 바인딩: toohttp://localhost 대신 {port}: {port}.</span><span class="sxs-lookup"><span data-stu-id="5f502-203">Bind toohttps://localhost:{port} rather than toohttp://localhost:{port}.</span></span> <span data-ttu-id="5f502-204">기본적으로 이 옵션은 사용자 컴퓨터에 신뢰할 수 있는 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="5f502-205">Hello 프로세스를 종료 하기 전에 추가 입력에 대 한 일시 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-205">Pause for additional input before exiting hello process.</span></span> <span data-ttu-id="5f502-206">IDE(통합 개발 환경)에서 Azure Functions 핵심 도구를 시작할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="5f502-207">Hello 함수 호스트를 시작할 때 hello HTTP URL 트리거 함수 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-207">When hello Functions host starts, it outputs hello URL of HTTP-triggered functions:</span></span>

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="5f502-208">VS 코드 또는 Visual Studio에서 디버그</span><span class="sxs-lookup"><span data-stu-id="5f502-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="5f502-209">디버거, tooattach 전달 hello `--debug` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-209">tooattach a debugger, pass hello `--debug` argument.</span></span> <span data-ttu-id="5f502-210">toodebug JavaScript 함수의 경우 Visual Studio 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-210">toodebug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="5f502-211">C# 함수의 경우 Visual Studio를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="5f502-212">toodebug C# 함수를 사용 하 여 `--debug vs`합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-212">toodebug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="5f502-213">[Azure Functions Visual Studio 2017 도구](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/)를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="5f502-214">toolaunch hello 호스트 및 JavaScript 디버깅 설정을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-214">toolaunch hello host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="5f502-215">그런 다음 Visual Studio Code에서 hello **디버그** 뷰의 **tooAzure 함수 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-215">Then, in Visual Studio Code, in hello **Debug** view, select **Attach tooAzure Functions**.</span></span> <span data-ttu-id="5f502-216">중단점을 연결하고, 변수를 검사하고, 코드를 단계별로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Visual Studio Code를 사용한 JavaScript 디버깅](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a><span data-ttu-id="5f502-218">전달 테스트 데이터 tooa 함수</span><span class="sxs-lookup"><span data-stu-id="5f502-218">Passing test data tooa function</span></span>

<span data-ttu-id="5f502-219">사용 하 여 직접 함수를 호출 또한 `func run <FunctionName>` hello 함수에 대 한 입력된 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for hello function.</span></span> <span data-ttu-id="5f502-220">이 명령은 비슷한 toorunning hello를 사용 하는 함수는 **테스트** hello Azure 포털에서에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-220">This command is similar toorunning a function using hello **Test** tab in hello Azure portal.</span></span> <span data-ttu-id="5f502-221">이 명령은 hello 전체 함수 호스트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-221">This command launches hello entire Functions host.</span></span>

<span data-ttu-id="5f502-222">`func run`hello 다음 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-222">`func run` supports hello following options:</span></span>

| <span data-ttu-id="5f502-223">옵션</span><span class="sxs-lookup"><span data-stu-id="5f502-223">Option</span></span>     | <span data-ttu-id="5f502-224">설명</span><span class="sxs-lookup"><span data-stu-id="5f502-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="5f502-225">인라인 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="5f502-226">Hello 함수를 실행 하기 전에 디버거 toohello 호스트 프로세스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-226">Attach a debugger toohello host process before running hello function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="5f502-227">Hello 로컬 함수 호스트 될 때까지 초 단위로 시간 toowait 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-227">Time toowait (in seconds) until hello local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="5f502-228">파일 이름 toouse 콘텐츠로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-228">hello file name toouse as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="5f502-229">입력에 대한 메시지를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-229">Does not prompt for input.</span></span> <span data-ttu-id="5f502-230">자동화 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="5f502-231">예를 들어 toocall HTTP 트리거 함수 및 hello 다음 명령을 실행 한 패스 콘텐츠 본문:</span><span class="sxs-lookup"><span data-stu-id="5f502-231">For example, toocall an HTTP-triggered function and pass content body, run hello following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="5f502-232"><a name="publish"></a>TooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="5f502-232"><a name="publish"></a>Publish tooAzure</span></span>

<span data-ttu-id="5f502-233">azure에서 사용 하 여 hello 함수 프로젝트 tooa 함수 앱 toopublish `publish` 명령:</span><span class="sxs-lookup"><span data-stu-id="5f502-233">toopublish a Functions project tooa function app in Azure, use hello `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="5f502-234">Hello 다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-234">You can use hello following options:</span></span>

| <span data-ttu-id="5f502-235">옵션</span><span class="sxs-lookup"><span data-stu-id="5f502-235">Option</span></span>     | <span data-ttu-id="5f502-236">설명</span><span class="sxs-lookup"><span data-stu-id="5f502-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="5f502-237">게시 설정에 local.settings.json tooAzure, toooverwrite hello 설정에 이미 있는 경우 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-237">Publish settings in local.settings.json tooAzure, prompting toooverwrite if hello setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="5f502-238">`-i`와 함께 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-238">Must be used with `-i`.</span></span> <span data-ttu-id="5f502-239">Azure의 AppSettings을 로컬 값으로 덮어씁니다(서로 다른 경우).</span><span class="sxs-lookup"><span data-stu-id="5f502-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="5f502-240">기본값은 프롬프트입니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-240">Default is prompt.</span></span>|

<span data-ttu-id="5f502-241">hello `publish` 명령 hello 함수 프로젝트 디렉터리의 hello 내용을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-241">hello `publish` command uploads hello contents of hello Functions project directory.</span></span> <span data-ttu-id="5f502-242">로컬 파일을 삭제 하면 hello `publish` 명령 삭제 하지는 않습니다 Azure에서.</span><span class="sxs-lookup"><span data-stu-id="5f502-242">If you delete files locally, hello `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="5f502-243">Hello를 사용 하 여 Azure에서 파일을 삭제할 수 있습니다 [Kudu 도구](functions-how-to-use-azure-function-app-settings.md#kudu) hello에 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-243">You can delete files in Azure by using hello [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f502-244">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f502-244">Next steps</span></span>

<span data-ttu-id="5f502-245">Azure Functions 핵심 도구는 [오픈 소스이며 GitHub에서 호스팅](https://github.com/azure/azure-functions-cli)됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="5f502-246">버그 또는 기능 요청 toofile [GitHub 문제를 열고](https://github.com/azure/azure-functions-cli/issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f502-246">toofile a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[Azure 함수 핵심 도구]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure 포털]: https://portal.azure.com 
