---
title: "Azure 앱 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 만들기"
description: "Azure에서 호스트되는 node.js 웹 앱에서 socket.io를 사용하는 방법을 보여 주는 자습서입니다."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: e1aa539e1134884261ea7464bfda6d14815618d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="6c6c7-103">Azure 앱 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6c6c7-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="6c6c7-104">Socket.IO는 WebSocket을 사용하여 node.js 서버와 클라이언트 간의 실시간 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="6c6c7-105">또한 이전 브라우저에서 작동하는 다른 전송(예: 긴 폴링)으로의 대체를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-105">It also supports fallback to other transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="6c6c7-106">이 자습서는 Azure 웹앱으로 Socket.IO를 기반으로 하는 호스팅을 안내하고 [Azure Redis Cache]를 사용하여 응용 프로그램의 크기를 조정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how to scale the application using [Azure Redis Cache].</span></span> <span data-ttu-id="6c6c7-107">Socket.IO에 대한 자세한 내용은 <http://socket.io/>(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="6c6c7-108">이 작업의 절차는 [App Service Web Apps]에 적용됩니다. 클라우드 서비스에 대해서는 [Azure 클라우드 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-108">The procedures in this task apply to [App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-the-chat-example"></a><span data-ttu-id="6c6c7-109">채팅 예제 다운로드</span><span class="sxs-lookup"><span data-stu-id="6c6c7-109">Download the chat example</span></span>
<span data-ttu-id="6c6c7-110">이 프로젝트에서는 [Socket.IO GitHub 리포지토리](영문)의 채팅 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-110">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="6c6c7-111">다음 단계에 따라 예제를 다운로드하여 이전에 만든 프로젝트에 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-111">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="6c6c7-112">Socket.IO 프로젝트의 [ZIP 또는 GZ 보관 릴리스] 를 다운로드합니다(이 문서에서는 버전 1.3.5 사용).</span><span class="sxs-lookup"><span data-stu-id="6c6c7-112">Download a [ZIP or GZ archived release] of the Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="6c6c7-113">보관 파일을 추출하고 **examples\\chat** 디렉터리를 새 위치에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-113">Extract the archive and copy the **examples\\chat** directory to a new location.</span></span> <span data-ttu-id="6c6c7-114">예를 들어 **\\node\\chat**입니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="6c6c7-115">app.js 수정 및 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="6c6c7-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="6c6c7-116">**index.js** 파일의 이름을 **app.js**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-116">Rename the **index.js** file to **app.js**.</span></span> <span data-ttu-id="6c6c7-117">그러면 Azure에서 이 파일을 Node.js 응용 프로그램으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-117">This allows Azure to detect that this is a Node.js application.</span></span>
2. <span data-ttu-id="6c6c7-118">텍스트 편집기에서 **app.js** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-118">Open the **app.js** file in a text editor.</span></span> <span data-ttu-id="6c6c7-119">아래와 같이 `var io = require('../..')(server);` 을 포함한 줄을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-119">Change the line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="6c6c7-120">아래와 같이 **package.json** 파일을 열고 `dependencies` 아래의 socket.io에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-120">Open the **package.json** file and add a reference to socket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="6c6c7-121">명령줄에서 **\\node\\chat** 디렉터리로 변경하고 npm을 사용하여 이 응용 프로그램에 필요한 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-121">From the command-line, change to the **\\node\\chat** directory and use npm to install the modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="6c6c7-122">이는 모듈을 **node_modules**라는 하위 폴더에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-122">This will install the modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="6c6c7-123">Azure 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6c6c7-123">Create an Azure Web App</span></span>
<span data-ttu-id="6c6c7-124">다음 단계에 따라 Azure 웹 앱을 만들고, Git 게시를 사용하도록 설정한 다음, 웹 앱에 대한 WebSocket 지원을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-124">Follow these steps to create an Azure web app, enable Git publishing, and then enable WebSocket support for the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="6c6c7-125">이 자습서를 완료하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-125">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="6c6c7-126">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6c6c7-127">자세한 내용은 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure 무료 평가판</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="6c6c7-128">Azure CLI(Azure 명령줄 인터페이스)를 설치하고 Azure 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-128">Install the Azure Command-Line Interface (Azure CLI) and connect to your Azure subscription.</span></span> <span data-ttu-id="6c6c7-129">[Azure CLI 설치 및 구성](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-129">See [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="6c6c7-130">Azure에서 리포지토리를 처음 설정하는 경우 로그인 자격 증명을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-130">If this is your first time setting up a repository in Azure, you need to create login credentials.</span></span> <span data-ttu-id="6c6c7-131">Azure CLI에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-131">From the Azure CLI, enter the following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="6c6c7-132">**\\node\chat** 디렉터리로 변경하고 다음 명령을 사용하여 새 Azure 웹앱 및 로컬 Git 리포지토리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-132">Change to the **\\node\chat** directory and use the following command to create a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="6c6c7-133">이 명령은 'azure'라는 Git 원격도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="6c6c7-134">'mysitename'을 웹 앱의 고유한 이름으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="6c6c7-135">다음 명령을 사용하여 기존 파일을 로컬 리포지토리로 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-135">Commit the existing files to the local repository by using the following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="6c6c7-136">다음 명령으로 파일을 Azure 웹 앱 리포지토리로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-136">Push the files to the Azure Web Apps repository with the following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="6c6c7-137">메시지가 표시되면 2단계에서 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="6c6c7-138">서버에서 모듈을 가져올 때 상태 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-138">You will receive status messages as modules are imported on the server.</span></span> <span data-ttu-id="6c6c7-139">이 프로세스가 완료되면 응용 프로그램이 Azure 웹 앱에 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-139">Once this process has completed, the application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6c6c7-140">모듈이 설치되는 동안 'The imported project ... was not found' 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-140">During module installation, you may notice errors that 'The imported project ... was not found'.</span></span> <span data-ttu-id="6c6c7-141">이 오류는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="6c6c7-142">Socket.IO는 Azure에서 기본적으로 사용되지 않는 WebSocket을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="6c6c7-143">WebSocket을 사용하도록 설정하려면 다음 명령을 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-143">To enable web sockets, use the following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="6c6c7-144">메시지가 표시되면 웹 앱 이름을 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-144">If prompted, enter the name of the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6c6c7-145">'azure site set -w' 명령은 버전 0.7.4 이상의 Azure 명령줄 인터페이스에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-145">The 'azure site set -w' command will work only with version 0.7.4 or higher of the Azure Command-Line Interface.</span></span> <span data-ttu-id="6c6c7-146">또한 [Azure 포털](https://portal.azure.com)에서 WebSocket 지원을 사용하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-146">You can also enable WebSocket support using the [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="6c6c7-147">Azure Portal에서 WebSocket을 사용하도록 설정하려면 Web Apps 블레이드에서 해당 웹앱을 클릭하고 **모든 설정** > **응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-147">To enable WebSockets using the Azure Portal, click the web app from the Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="6c6c7-148">**웹 소켓**에서 **켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="6c6c7-149">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="6c6c7-150">Azure에서 웹 앱을 보려면 다음 명령을 사용하여 웹 브라우저를 시작하고 호스트되는 웹 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-150">To view the web app on Azure, use the following command to launch your web browser and navigate to the hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="6c6c7-151">현재 앱이 Azure에서 실행되고 있으며 Socket.IO를 사용하여 다른 클라이언트 간에 채팅 메시지를 릴레이할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="6c6c7-152">확장</span><span class="sxs-lookup"><span data-stu-id="6c6c7-152">Scale out</span></span>
<span data-ttu-id="6c6c7-153">**어댑터**를 사용하여 여러 응용 프로그램 인스턴스 간에 메시지 및 이벤트를 배포하는 방식으로 Socket.IO 응용 프로그램을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-153">Socket.IO applications can be scaled out by using an **adapter** to distribute messages and events between multiple application instances.</span></span> <span data-ttu-id="6c6c7-154">사용 가능한 여러 어댑터가 있지만 Azure Redis 캐시 기능에 사용하기 편리한 어댑터는 [socket.io-redis] 어댑터입니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-154">While there are several adapters available, the [socket.io-redis] adapter can be easily used with the Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="6c6c7-155">Socket.IO 솔루션 확장에 대한 추가 요구 사항은 고정 세션의 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="6c6c7-156">고정 세션은 Azure 요청 라우팅을 통해 Azure 웹 앱에서 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="6c6c7-157">자세한 내용은 [Azure 웹 사이트의 인스턴스 선호도]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="6c6c7-158">Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="6c6c7-158">Create a Redis cache</span></span>
<span data-ttu-id="6c6c7-159">[Azure Redis 캐시에서 캐시 만들기] 의 단계를 수행하여 새 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-159">Perform the steps in [Create a cache in Azure Redis Cache] to create a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="6c6c7-160">캐시의 **호스트 이름** 및 **기본 키**를 저장합니다. 이러한 정보는 다음 단계에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-160">Save the **Host name** and **Primary key** for your cache, as these will be needed in the next steps.</span></span>
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a><span data-ttu-id="6c6c7-161">Redis 및 socket.io-redis 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="6c6c7-161">Add the redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="6c6c7-162">명령줄에서 **\\node\\chat** 디렉터리로 변경하여 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-162">From a command-line, change to the **\\node\\chat** directory and use the following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="6c6c7-163">이 명령에 지정된 버전은 이 문서를 테스트할 때 사용된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-163">The versions specified in this command are the versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="6c6c7-164">**app.js** 파일을 수정하여 다음 줄을 `var io = require('socket.io')(server);` 바로 뒤에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-164">Modify the **app.js** file to add the following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="6c6c7-165">**redishostname** 및 **rediskey**를 Redis 캐시의 호스트 이름 및 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-165">Replace **redishostname** and **rediskey** with the host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="6c6c7-166">그러면 이전에 만든 Redis 캐시에 대한 게시 및 구독 클라이언트가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-166">This will create a publish and subscribe client to the Redis cache created previously.</span></span> <span data-ttu-id="6c6c7-167">이 클라이언트는 어댑터에서 응용 프로그램의 인스턴스 간에 메시지 및 이벤트를 전달하는 데 Redis 캐시를 사용하도록 Socket.IO를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-167">The clients are then used with the adapter to configure Socket.IO to use the Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6c6c7-168">**socket.io-redis** 어댑터는 Redis와 직접 통신할 수 있지만 현재 버전에서는 Azure Redis 캐시에 필요한 인증을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-168">While the **socket.io-redis** adapter can communicate directly to Redis, the current version does not support the authentication required by Azure Redis cache.</span></span> <span data-ttu-id="6c6c7-169">따라서 **redis** 모듈을 통해 초기 연결이 만들어진 다음 **socket.io-redis** 어댑터로 클라이언트가 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-169">So the initial connection is created using the **redis** module, then the client is passed to the **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="6c6c7-170">Azure Redis 캐시는 포트 6380을 사용한 보안 연결을 지원하지만 이 예제에 사용된 모듈에서는 2014년 7월 14일 현재 보안 연결을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-170">While Azure Redis Cache supports secure connections using port 6380, the modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="6c6c7-171">위의 코드에서는 기본적으로 비보안 포트 6379를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-171">The above code uses the default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="6c6c7-172">수정한 **app.js** 저장</span><span class="sxs-lookup"><span data-stu-id="6c6c7-172">Save the modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="6c6c7-173">변경 내용 커밋 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="6c6c7-173">Commit changes and redeploy</span></span>
<span data-ttu-id="6c6c7-174">**\\node\\chat** 디렉터리의 명령줄에서 다음 명령을 사용하여 변경 내용을 커밋하고 응용 프로그램을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-174">From the command-line in the **\\node\\chat** directory, use the following commands to commit changes and redeploy the application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="6c6c7-175">변경 내용이 서버에 푸시되고 나면 다음 명령을 사용하여 여러 인스턴스 간에 사이트를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-175">Once the changes have been pushed to the server, you can scale your site across multiple instances by using the following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="6c6c7-176">여기서 **#**은 만들 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-176">Where **#** is the number of instances to create.</span></span>

<span data-ttu-id="6c6c7-177">여러 브라우저 또는 컴퓨터에서 웹 앱에 연결하여 메시지가 모든 클라이언트에 올바르게 전송되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-177">You can connect to your web app from multiple browsers or computers to verify that messages are correctly sent to all clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6c6c7-178">문제 해결</span><span class="sxs-lookup"><span data-stu-id="6c6c7-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="6c6c7-179">연결 제한</span><span class="sxs-lookup"><span data-stu-id="6c6c7-179">Connection limits</span></span>
<span data-ttu-id="6c6c7-180">Azure 웹 앱은 여러 SKU에서 사용할 수 있으며, 이러한 SKU에 따라 사이트에 사용 가능한 리소스가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-180">Azure Web Apps is available in multiple SKUs, which determine the resources available to your site.</span></span> <span data-ttu-id="6c6c7-181">여기에는 허용되는 WebSocket 연결 수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-181">This includes the number of allowed WebSocket connections.</span></span> <span data-ttu-id="6c6c7-182">자세한 내용은 [웹 앱 가격 책정 페이지]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-182">For more information, see the [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="6c6c7-183">메시지가 WebSocket을 사용하여 전송되지 않음</span><span class="sxs-lookup"><span data-stu-id="6c6c7-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="6c6c7-184">클라이언트 브라우저에서 WebSocket을 사용하는 대신 긴 폴링으로의 대체를 유지하는 경우 다음 중 하나가 원인일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-184">If client browsers keep falling back to long polling instead of using WebSockets, it may be because of one of the following.</span></span>

* <span data-ttu-id="6c6c7-185">**전송을 WebSocket으로만 제한**</span><span class="sxs-lookup"><span data-stu-id="6c6c7-185">**Try limiting the transport to just WebSockets**</span></span>
  
    <span data-ttu-id="6c6c7-186">Socket.IO에서 WebSocket을 메시징 전송으로 사용하려면 서버와 클라이언트가 모두 WebSocket을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-186">In order for Socket.IO to use WebSockets as the messaging transport, both the server and client must support WebSockets.</span></span> <span data-ttu-id="6c6c7-187">둘 중 하나가 지원하지 않으면 Socket.IO에서 긴 폴링과 같은 다른 전송을 협상합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-187">If one or the other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="6c6c7-188">Socket.IO에서 사용하는 기본 전송 목록은 ` websocket, htmlfile, xhr-polling, jsonp-polling`입니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-188">The default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="6c6c7-189">**app.js** 파일에서 `, nicknames = {};`가 포함된 줄 뒤에 다음 코드를 추가하여 Socket.IO에서 WebSocket만 사용하도록 강제로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-189">You can force it to only use WebSockets by adding the following code to the **app.js** file, after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="6c6c7-190">위 코드가 활성화되어 있는 동안에는 통신이 WebSocket으로만 제한되므로 WebSocket을 지원하지 않는 이전 브라우저에서 사이트에 연결할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-190">Note that older browsers that do not support WebSockets will not be able to connect to the site while the above code is active, as it restricts communication to WebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="6c6c7-191">**SSL 사용**</span><span class="sxs-lookup"><span data-stu-id="6c6c7-191">**Use SSL**</span></span>
  
    <span data-ttu-id="6c6c7-192">WebSocket은 **Upgrade** 헤더와 같은 보다 적은 수의 사용된 HTTP 헤더를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-192">WebSockets relies on some lesser used HTTP headers, such as the **Upgrade** header.</span></span> <span data-ttu-id="6c6c7-193">웹 프록시와 같은 일부 중간 네트워크 장치는 이러한 헤더를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="6c6c7-194">이 문제를 방지하기 위해 SSL을 통해 WebSocket 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-194">To avoid this problem, you can establish the WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="6c6c7-195">이 작업을 수행하는 간단한 방법은 `match origin protocol`로 Socket.IO를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-195">An easy way to accomplish this is to configure Socket.IO to `match origin protocol`.</span></span> <span data-ttu-id="6c6c7-196">이 명령은 Socket.IO에 웹 페이지에 대한 시작 HTTP/HTTPS 요청과 동일하게 WebSockets 통신의 보안을 유지하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-196">This instructs Socket.IO to secure WebSockets communication the same as the originating HTTP/HTTPS request for the web page.</span></span> <span data-ttu-id="6c6c7-197">브라우저에서 HTTPS URL을 사용하여 웹 사이트를 방문한 경우 Socket.IO를 통한 이후의 WebSocket 통신은 SSL을 통해 보안이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-197">If a browser uses an HTTPS URL to visit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="6c6c7-198">이 구성을 사용하도록 이 예제를 수정하려면 **app.js** 파일에서 `, nicknames = {};`가 포함된 줄 뒤에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-198">To modify this example to enable this configuration, add the following code to the **app.js** file after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="6c6c7-199">**web.config 설정 확인**</span><span class="sxs-lookup"><span data-stu-id="6c6c7-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="6c6c7-200">Node.js 응용 프로그램을 호스트하는 Azure 웹 앱에서는 **web.config** 파일을 사용하여 들어오는 요청을 Node.js 응용 프로그램으로 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-200">Azure web apps that host Node.js applications use the **web.config** file to route incoming requests to the Node.js application.</span></span> <span data-ttu-id="6c6c7-201">Node.js 응용 프로그램에서 WebSocket이 올바르게 작동하려면 **web.config** 에 다음 항목이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-201">For WebSockets to function correctly with Node.js applications, the **web.config** must contain the following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="6c6c7-202">그러면 WebSocket의 자체 구현을 포함하고 Socket.IO와 같은 Node.js 관련 WebSocket 모듈과 충돌하는 IIS WebSocket 모듈이 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-202">This disables the IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="6c6c7-203">이 줄이 없거나 `true`로 설정되면 WebSocket 전송이 사용자 응용 프로그램에 작동하지 않기 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-203">If this line is not present, or is set to `true`, this may be the reason that the WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="6c6c7-204">일반적으로 Node.js 응용 프로그램에는 **web.config** 파일이 포함되어 있지 않으므로 Azure 웹 사이트를 배포할 때 해당 웹 사이트에서 Node.js 응용 프로그램에 대해 이 파일을 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="6c6c7-205">이 파일은 서버에서 자동으로 생성되기 때문에 이 파일을 보려면 웹 사이트에 FTP 또는 FTPS URL을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-205">Since this file is automatically generated on the server, you must use the FTP or FTPS URL for your website to view this file.</span></span> <span data-ttu-id="6c6c7-206">사이트의 FTP 및 FTPS URL은 클래식 포털에서 웹앱을 선택한 후 **대시보드** 링크를 선택하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-206">You can find the FTP and FTPS URLs for your site in the classic portal by selecting your web app, and then the **Dashboard** link.</span></span> <span data-ttu-id="6c6c7-207">이러한 URL은 **간략 상태** 섹션에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-207">The URLs are displayed in the **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="6c6c7-208">**web.config** 파일은 응용 프로그램에서 제공하지 않는 경우에만 Azure 웹 사이트에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-208">The **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="6c6c7-209">응용 프로그램 프로젝트의 루트에 **web.config** 파일을 제공한 경우에는 Azure 웹 앱에서 이 파일이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-209">If you provide a **web.config** file in the root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="6c6c7-210">이 항목이 없거나 `true` 값으로 설정된 경우 Node.js 응용 프로그램의 루트에 **web.config**를 만들고 `false` 값을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-210">If the entry is not present, or is set to a value of `true`, then you should create a **web.config** in the root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="6c6c7-211">참고로 다음은 **app.js**를 진입점으로 사용하는 응용 프로그램의 기본 **web.config**입니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-211">For reference, the below is a default **web.config** for an application that uses **app.js** as the entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used to run node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that the server.js file is a node.js web app to be handled by the iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped to the node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using the following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
                * node_env: will be propagated to node as NODE_ENV environment variable
                * debuggingEnabled - controls whether the built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="6c6c7-212">사용자 응용 프로그램에서 **app.js**가 아닌 다른 진입점을 사용하는 경우, 표시되는 **app.js**를 모두 올바른 진입점으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with the correct entry point.</span></span> <span data-ttu-id="6c6c7-213">예를 들어 **app.js**를 **server.js**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="6c6c7-214">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험]으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-214">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6c6c7-215">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6c6c7-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c6c7-216">Next steps</span></span>
<span data-ttu-id="6c6c7-217">이 자습서에서는 Azure 웹 앱에 호스트되는 기본 채팅 응용 프로그램을 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-217">In this tutorial you learned how to create a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="6c6c7-218">이 응용 프로그램은 Azure 클라우드 서비스로 호스트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="6c6c7-219">이를 수행하는 방법에 대한 단계는 [Azure 클라우드 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드]를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-219">For steps on how to accomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="6c6c7-220">자세한 내용은 [Node.js 개발자 센터]도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-220">For more information, see also the [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="6c6c7-221">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="6c6c7-221">What's changed</span></span>
* <span data-ttu-id="6c6c7-222">웹 사이트에서 앱 서비스로 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c6c7-222">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

<span data-ttu-id="6c6c7-223">[Azure Redis Cache]: /documentation/services/redis-cache/</span><span class="sxs-lookup"><span data-stu-id="6c6c7-223">[Azure Redis Cache]: /documentation/services/redis-cache/</span></span>
<span data-ttu-id="6c6c7-224">[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="6c6c7-224">[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="6c6c7-225">[웹 앱 가격 책정 페이지]: http://go.microsoft.com/fwlink/?LinkId=511643</span><span class="sxs-lookup"><span data-stu-id="6c6c7-225">[Web Apps Pricing page]: http://go.microsoft.com/fwlink/?LinkId=511643</span></span>
<span data-ttu-id="6c6c7-226">[Azure 클라우드 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="6c6c7-226">[Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span></span>
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
<span data-ttu-id="6c6c7-227">[Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="6c6c7-227">[Azure App Service and Its Impact on Existing Azure Services]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="6c6c7-228">[Node.js 개발자 센터]: /develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="6c6c7-228">[Node.js Developer Center]: /develop/nodejs/</span></span>
<span data-ttu-id="6c6c7-229">[App Service 체험]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="6c6c7-229">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>
<span data-ttu-id="6c6c7-230">[Azure 웹 사이트의 인스턴스 선호도]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span><span class="sxs-lookup"><span data-stu-id="6c6c7-230">[Instance Affinity in Azure Web Sites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span></span>
<span data-ttu-id="6c6c7-231">[Azure Redis 캐시에서 캐시 만들기]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span><span class="sxs-lookup"><span data-stu-id="6c6c7-231">[Create a cache in Azure Redis Cache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span></span>

<span data-ttu-id="6c6c7-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="6c6c7-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span></span>
<span data-ttu-id="6c6c7-233">[Socket.IO GitHub 리포지토리]: https://github.com/socketio/socket.io</span><span class="sxs-lookup"><span data-stu-id="6c6c7-233">[Socket.IO GitHub repository]: https://github.com/socketio/socket.io</span></span>
<span data-ttu-id="6c6c7-234">[ZIP 또는 GZ 보관 릴리스]: https://github.com/socketio/socket.io/releases</span><span class="sxs-lookup"><span data-stu-id="6c6c7-234">[ZIP or GZ archived release]: https://github.com/socketio/socket.io/releases</span></span>

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
