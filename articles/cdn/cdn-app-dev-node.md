---
title: "Node.js 용 aaaGet hello Azure CDN SDK 시작 | Microsoft Docs"
description: "자세한 내용은 방법 toowrite Node.js 응용 프로그램 toomanage Azure CDN 합니다."
services: cdn
documentationcenter: nodejs
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c4bb6a61-de3d-4f0c-9dca-202554c43dfa
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c805e5fb8e0b471e8b248cb2f4b29efd6c85940
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="7ceb4-103">Azure CDN 개발 시작</span><span class="sxs-lookup"><span data-stu-id="7ceb4-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ceb4-104">Node.JS</span><span class="sxs-lookup"><span data-stu-id="7ceb4-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="7ceb4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="7ceb4-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="7ceb4-106">Hello를 사용할 수 있습니다 [Node.js 용 Azure CDN SDK](https://www.npmjs.com/package/azure-arm-cdn) tooautomate CDN 프로필 및 끝점의 생성 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-106">You can use hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="7ceb4-107">이 자습서는 몇몇 hello 사용할 수 있는 작업을 보여 주는 간단한 Node.js 콘솔 응용 프로그램의 hello 만들기를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-107">This tutorial walks through hello creation of a simple Node.js console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="7ceb4-108">이 자습서는 만들어지지 toodescribe hello Azure CDN SDK의 모든 측면 Node.js 용 자세히 설명에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="7ceb4-109">toocomplete 이미 있어야이 자습서에서는 [Node.js](http://www.nodejs.org) **4.x.x** 또는 이상이 설치 및 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-109">toocomplete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="7ceb4-110">Toocreate Node.js 응용 프로그램을 원하는 텍스트 편집기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-110">You can use any text editor you want toocreate your Node.js application.</span></span>  <span data-ttu-id="7ceb4-111">toowrite 사용이 자습서에서는 [Visual Studio Code](https://code.visualstudio.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-111">toowrite this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="7ceb4-112">hello [이 자습서에서 완성 된 프로젝트](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) MSDN에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-112">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="7ceb4-113">프로젝트 만들기 및 NPM 종속성 추가</span><span class="sxs-lookup"><span data-stu-id="7ceb4-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="7ceb4-114">우리의 CDN 프로필에 대 한 리소스 그룹을 만들고이 Azure AD 응용 프로그램 사용 권한 toomanage CDN 프로필 및 해당 그룹 내에서 끝점을 지정 했 म, 했으므로 응용 프로그램을 만들기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="7ceb4-115">폴더 toostore 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-115">Create a folder toostore your application.</span></span>  <span data-ttu-id="7ceb4-116">현재 경로에 hello Node.js 도구와 함께 콘솔에서 현재 위치 toothis 새 폴더를 설정 하 고 실행 하 여 프로젝트를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-116">From a console with hello Node.js tools in your current path, set your current location toothis new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="7ceb4-117">그러면 됩니다는 일련의 질문 tooinitialize 프로젝트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-117">You will then be presented a series of questions tooinitialize your project.</span></span>  <span data-ttu-id="7ceb4-118">**진입점**의 경우 이 자습서에서는 *app.js*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="7ceb4-119">다음 예제는 hello 내 다른 선택 항목을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-119">You can see my other choices in hello following example.</span></span>

![NPM init 출력](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="7ceb4-121">프로젝트는 *packages.json* 파일을 사용하여 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="7ceb4-122">프로젝트 진행 NPM 패키지에 포함 된 일부 Azure 라이브러리 toouse를 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-122">Our project is going toouse some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="7ceb4-123">Hello (ms rest azure) Node.js 용 Azure 클라이언트 런타임 및 hello (azure arm cd) Node.js 용 Azure CDN 클라이언트 라이브러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-123">We'll use hello Azure Client Runtime for Node.js (ms-rest-azure) and hello Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="7ceb4-124">종속성으로 해당 toohello 프로젝트를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-124">Let's add those toohello project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="7ceb4-125">패키지 작업을 마쳤으면 hello 후 설치를 hello *package.json* 파일은 유사한 toothis 예 (버전 번호가 달라질 수 있습니다) 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-125">After hello packages are done installing, hello *package.json* file should look similar toothis example (version numbers may differ):</span></span>

``` json
{
  "name": "cdn_node",
  "version": "1.0.0",
  "description": "Azure CDN Node.js tutorial project",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Cam Soper",
  "license": "MIT",
  "dependencies": {
    "azure-arm-cdn": "^0.2.1",
    "ms-rest-azure": "^1.14.4"
  }
}
```

<span data-ttu-id="7ceb4-126">마지막으로, 텍스트 편집기를 사용 하 여 빈 텍스트 파일을 만들고 저장으로 우리의 프로젝트 폴더의 hello 루트에서 *app.js*합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-126">Finally, using your text editor, create a blank text file and save it in hello root of our project folder as *app.js*.</span></span>  <span data-ttu-id="7ceb4-127">이제 준비 toobegin 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-127">We're now ready toobegin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="7ceb4-128">requires, 상수, 인증 및 구조</span><span class="sxs-lookup"><span data-stu-id="7ceb4-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="7ceb4-129">와 *app.js* 편집기에서 열고, hello 작성이 프로그램의 기본 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-129">With *app.js* open in our editor, let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="7ceb4-130">Hello 다음과 같이 hello 위쪽 우리의 NPM 패키지에 대 한 "필요" hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-130">Add hello "requires" for our NPM packages at hello top with hello following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="7ceb4-131">이 메서드는 사용 하 여 일부 상수 toodefine 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-131">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="7ceb4-132">Hello 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-132">Add hello following.</span></span>  <span data-ttu-id="7ceb4-133">수 있는지 tooreplace hello를 포함 하 여 hello 자리 표시자  **&lt;꺾쇠 괄호&gt;**, 필요에 따라 고유한 값으로.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-133">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
    ``` javascript
    //Tenant app constants
    const clientId = "<YOUR CLIENT ID>";
    const clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    const tenantId = "<YOUR TENANT ID>";
   
    //Application constants
    const subscriptionId = "<YOUR SUBSCRIPTION ID>";
    const resourceGroupName = "CdnConsoleTutorial";
    const resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. <span data-ttu-id="7ceb4-134">다음으로 hello CDN 관리 클라이언트를 인스턴스화하고 알아보고이 자격 증명 지정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-134">Next, we'll instantiate hello CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="7ceb4-135">개별 사용자 인증을 사용한다면 다음 두 줄은 약간 다르게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7ceb4-136">서비스 사용자 대신 toohave 개별 사용자 인증을 선택 하는 경우에이 코드 예제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-136">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="7ceb4-137">신중 하 게 tooguard 개별 사용자 자격 증명 되며 비밀로 유지 하세요.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-137">Be careful tooguard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="7ceb4-138">있는지 tooreplace hello 항목 이어야  **&lt;꺾쇠 괄호&gt;**  hello로 정보를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-138">Be sure tooreplace hello items in **&lt;angle brackets&gt;** with hello correct information.</span></span>  <span data-ttu-id="7ceb4-139">에 대 한 `<redirect URI>`, hello 리디렉션 hello 응용 프로그램을 Azure AD에 등록할 때 입력 한 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-139">For `<redirect URI>`, use hello redirect URI you entered when you registered hello application in Azure AD.</span></span>
4. <span data-ttu-id="7ceb4-140">Node.js 콘솔 응용 프로그램 일부 명령줄 매개 변수가 tootake 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-140">Our Node.js console application is going tootake some command-line parameters.</span></span>  <span data-ttu-id="7ceb4-141">적어도 하나의 매개 변수가 전달되었는지 유효성을 검사해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-141">Let's validate that at least one parameter was passed.</span></span>
   
   ```javascript
   //Collect command-line parameters
   var parms = process.argv.slice(2);
   
   //Do we have parameters?
   if(parms == null || parms.length == 0)
   {
       console.log("Not enough parameters!");
       console.log("Valid commands are list, delete, create, and purge.");
       process.exit(1);
   }
   ```
5. <span data-ttu-id="7ceb4-142">전달 된 매개 변수에 대해 tooother 기능 여기서 분기에서는 프로그램의 주요 부분 toohello를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-142">That brings us toohello main part of our program, where we branch off tooother functions based on what parameters were passed.</span></span>
   
    ```javascript
    switch(parms[0].toLowerCase())
    {
        case "list":
            cdnList();
            break;
   
        case "create":
            cdnCreate();
            break;
   
        case "delete":
            cdnDelete();
            break;
   
        case "purge":
            cdnPurge();
            break;
   
        default:
            console.log("Valid commands are list, delete, create, and purge.");
            process.exit(1);
    }
    ```
6. <span data-ttu-id="7ceb4-143">이 프로그램의 여러 위치에서 toomake hello 오른쪽 매개 변수 개수에 전달 하 고 올바른 표시 되지 않는 경우 일부 도움말을 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-143">At several places in our program, we'll need toomake sure hello right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="7ceb4-144">만들어 보겠습니다 함수 toodo입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-144">Let's create functions toodo that.</span></span>
   
   ```javascript
   function requireParms(parmCount) {
       if(parms.length < parmCount) {
           usageHelp(parms[0].toLowerCase());
           process.exit(1);
       }
   }
   
   function usageHelp(cmd) {
       console.log("Usage for " + cmd + ":");
       switch(cmd)
       {
           case "list":
               console.log("list profiles");
               console.log("list endpoints <profile name>");
               break;
   
           case "create":
               console.log("create profile <profile name>");
               console.log("create endpoint <profile name> <endpoint name> <origin hostname>");
               break;
   
           case "delete":
               console.log("delete profile <profile name>");
               console.log("delete endpoint <profile name> <endpoint name>");
               break;
   
           case "purge":
               console.log("purge <profile name> <endpoint name> <path>");
               break;
   
           default:
               console.log("Invalid command.");
       }
   }
   ```
7. <span data-ttu-id="7ceb4-145">마지막으로, 하므로, 메서드 toocall 작업이 완료 되 면 다시 hello CDN 관리 클라이언트에 사용할 예정 hello 함수는 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-145">Finally, hello functions we'll be using on hello CDN management client are asynchronous, so they need a method toocall back when they're done.</span></span>  <span data-ttu-id="7ceb4-146">Hello 출력 hello CDN 관리 클라이언트 (있는 경우)을에서 표시 하 고 hello 프로그램을 정상적으로 종료할 수 있는 파일을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-146">Let's make one that can display hello output from hello CDN management client (if any) and exit hello program gracefully.</span></span>
   
    ```javascript
    function callback(err, result, request, response) {
        if (err) {
            console.log(err);
            process.exit(1);
        } else {
            console.log((result == null) ? "Done!" : result);
            process.exit(0);
        }
    }
    ```

<span data-ttu-id="7ceb4-147">를 hello이 프로그램의 기본 구조를 작성 했으므로에서는 매개 변수에 따라 호출 된 hello 함수 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-147">Now that hello basic structure of our program is written, we should create hello functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="7ceb4-148">CDN 프로필 및 끝점 목록화하기</span><span class="sxs-lookup"><span data-stu-id="7ceb4-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="7ceb4-149">기존 프로필 및 끝점 우리의 코드 toolist부터 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-149">Let's start with code toolist our existing profiles and endpoints.</span></span>  <span data-ttu-id="7ceb4-150">코드 주석 각 매개 변수 방향은 알 수 있도록 예상 hello 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-150">My code comments provide hello expected syntax so we know where each parameter goes.</span></span>

```javascript
// list profiles
// list endpoints <profile name>
function cdnList(){
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profiles":
            console.log("Listing profiles...");
            cdnClient.profiles.listByResourceGroup(resourceGroupName, callback);
            break;

        case "endpoints":
            requireParms(3);
            console.log("Listing endpoints...");
            cdnClient.endpoints.listByProfile(parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="7ceb4-151">CDN 프로필 및 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="7ceb4-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="7ceb4-152">다음으로 hello 함수 toocreate 프로필 및 끝점 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-152">Next, we'll write hello functions toocreate profiles and endpoints.</span></span>

```javascript
function cdnCreate() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profile":
            cdnCreateProfile();
            break;

        case "endpoint":
            cdnCreateEndpoint();
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}

// create profile <profile name>
function cdnCreateProfile() {
    requireParms(3);
    console.log("Creating profile...");
    var standardCreateParameters = {
        location: resourceLocation,
        sku: {
            name: 'Standard_Verizon'
        }
    };

    cdnClient.profiles.create(parms[2], standardCreateParameters, resourceGroupName, callback);
}

// create endpoint <profile name> <endpoint name> <origin hostname>        
function cdnCreateEndpoint() {
    requireParms(5);
    console.log("Creating endpoint...");
    var endpointProperties = {
        location: resourceLocation,
        origins: [{
            name: parms[4],
            hostName: parms[4]
        }]
    };

    cdnClient.endpoints.create(parms[3], endpointProperties, parms[2], resourceGroupName, callback);
}
```

## <a name="purge-an-endpoint"></a><span data-ttu-id="7ceb4-153">끝점 삭제</span><span class="sxs-lookup"><span data-stu-id="7ceb4-153">Purge an endpoint</span></span>
<span data-ttu-id="7ceb4-154">Hello 끝점이 만들어졌으며 라고 가정할 경우 일반적인 작업 tooperform 프로그램에서 원하는 수 있는지는 제거 우리의 끝점의 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-154">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="7ceb4-155">CDN 프로필 및 끝점 삭제</span><span class="sxs-lookup"><span data-stu-id="7ceb4-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="7ceb4-156">hello 마지막 함수를 포함할 예정 끝점 및 프로필을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-156">hello last function we will include deletes endpoints and profiles.</span></span>

```javascript
function cdnDelete() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        // delete profile <profile name>
        case "profile":
            requireParms(3);
            console.log("Deleting profile...");
            cdnClient.profiles.deleteIfExists(parms[2], resourceGroupName, callback);
            break;

        // delete endpoint <profile name> <endpoint name>
        case "endpoint":
            requireParms(4);
            console.log("Deleting endpoint...");
            cdnClient.endpoints.deleteIfExists(parms[3], parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="running-hello-program"></a><span data-ttu-id="7ceb4-157">Hello 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7ceb4-157">Running hello program</span></span>
<span data-ttu-id="7ceb4-158">이제 당사의 즐겨 찾는 디버거를 사용 하 여이 Node.js 프로그램 실행 또는 hello 콘솔.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-158">We can now execute our Node.js program using our favorite debugger or at hello console.</span></span>

> [!TIP]
> <span data-ttu-id="7ceb4-159">Visual Studio Code 디버거를 사용 중인 tooset 사용자 환경 toopass hello 명령줄 매개 변수에서를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-159">If you're using Visual Studio Code as your debugger, you'll need tooset up your environment toopass in hello command-line parameters.</span></span>  <span data-ttu-id="7ceb4-160">Visual Studio 코드 작업을 위해 hello **lanuch.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-160">Visual Studio Code does this in hello **lanuch.json** file.</span></span>  <span data-ttu-id="7ceb4-161">명명 된 속성을 찾습니다 **args** 비슷한 toothis 나타나도록 매개 변수를 문자열 값의 배열을 추가 하 고: `"args": ["list", "profiles"]`합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar toothis:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="7ceb4-162">프로필을 나열하여 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-162">Let's start by listing our profiles.</span></span>

![프로필 나열](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="7ceb4-164">다시 빈 배열로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-164">We got back an empty array.</span></span>  <span data-ttu-id="7ceb4-165">리소스 그룹에 프로필이 없기 때문에 정상입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="7ceb4-166">이제 프로필을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-166">Let's create a profile now.</span></span>

![프로필 만들기](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="7ceb4-168">이제 끝점을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-168">Now, let's add an endpoint.</span></span>

![끝점 만들기](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="7ceb4-170">마지막으로 프로필을 삭제하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-170">Finally, let's delete our profile.</span></span>

![프로필 삭제](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="7ceb4-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ceb4-172">Next Steps</span></span>
<span data-ttu-id="7ceb4-173">이 연습에서 완료 하는 hello 프로젝트 toosee [hello 샘플 다운로드](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-173">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="7ceb4-174">hello 보기 hello Node.js 용 Azure CDN SDK에 대 한 toosee hello 참조 [참조](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-174">toosee hello reference for hello Azure CDN SDK for Node.js, view hello [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="7ceb4-175">Node.js, 보기 hello에 대 한 hello Azure SDK에 대 한 toofind 추가 설명서 [참조 전체](http://azure.github.io/azure-sdk-for-node/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-175">toofind additional documentation on hello Azure SDK for Node.js, view hello [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="7ceb4-176">[PowerShell](cdn-manage-powershell.md)을 사용하여 CDN 리소스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceb4-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

