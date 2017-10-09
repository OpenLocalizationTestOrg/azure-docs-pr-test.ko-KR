---
title: "aaaCreate Socket.IO Azure 앱 서비스에서 사용 하는 Node.js 채팅 응용 프로그램"
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
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="f9d95-103">Azure 앱 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f9d95-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="f9d95-104">Socket.IO는 WebSocket을 사용하여 node.js 서버와 클라이언트 간의 실시간 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="f9d95-105">또한 이전 버전의 브라우저를 사용 하는 대체 (fallback) tooother 전송 (예: 긴 폴링)을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-105">It also supports fallback tooother transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="f9d95-106">이 자습서는 Azure 웹 앱으로 기반 Socket.IO 채팅 응용 프로그램 호스팅 하지 안내 하 고 tooscale hello 응용 프로그램을 사용 하는 방법을 보여 [Azure Redis Cache]합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how tooscale hello application using [Azure Redis Cache].</span></span> <span data-ttu-id="f9d95-107">Socket.IO에 대한 자세한 내용은 <http://socket.io/>(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9d95-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="f9d95-108">이 작업의 절차에서는 hello 너무 적용[앱 서비스 웹 앱]; 클라우드 서비스에 대 한 참조 [Azure 클라우드 서비스에 사용 하는 Node.js 채팅 응용 Socket.IO 빌드]합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-108">hello procedures in this task apply too[App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-hello-chat-example"></a><span data-ttu-id="f9d95-109">Hello 채팅 예제를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-109">Download hello chat example</span></span>
<span data-ttu-id="f9d95-110">이 프로젝트에 대 한 hello 채팅 예제 hello에서 사용 합니다 [Socket.IO GitHub 리포지토리]합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-110">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="f9d95-111">다음 단계 toodownload hello 예제 hello를 수행 하 고 앞에서 만든 toohello 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-111">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="f9d95-112">다운로드 한 [ZIP 또는 GZ 보관 릴리스] hello Socket.IO 프로젝트의 (버전 1.3.5이이 문서에 사용 된)</span><span class="sxs-lookup"><span data-stu-id="f9d95-112">Download a [ZIP or GZ archived release] of hello Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="f9d95-113">Hello 보관 및 복사 hello 추출 **예제\\채팅** 디렉터리 tooa 새 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-113">Extract hello archive and copy hello **examples\\chat** directory tooa new location.</span></span> <span data-ttu-id="f9d95-114">예를 들어 **\\node\\chat**입니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="f9d95-115">app.js 수정 및 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="f9d95-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="f9d95-116">Hello 이름 바꾸기 **index.js** 파일 너무**app.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-116">Rename hello **index.js** file too**app.js**.</span></span> <span data-ttu-id="f9d95-117">이렇게 하면 Azure toodetect이는 Node.js 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="f9d95-117">This allows Azure toodetect that this is a Node.js application.</span></span>
2. <span data-ttu-id="f9d95-118">열기 hello **app.js** 파일 텍스트 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="f9d95-118">Open hello **app.js** file in a text editor.</span></span> <span data-ttu-id="f9d95-119">변경 hello 줄 포함 된 `var io = require('../..')(server);` 아래와 같이:</span><span class="sxs-lookup"><span data-stu-id="f9d95-119">Change hello line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="f9d95-120">열기 hello **package.json** 파일에서 참조 toosocket.io 더하고 `dependencies`다음과 같이:</span><span class="sxs-lookup"><span data-stu-id="f9d95-120">Open hello **package.json** file and add a reference toosocket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="f9d95-121">Hello 명령줄에서 toohello 변경  **\\노드\\채팅** 디렉터리 및 사용 하 여 npm tooinstall hello 모듈이 응용이 프로그램에 필요한:</span><span class="sxs-lookup"><span data-stu-id="f9d95-121">From hello command-line, change toohello **\\node\\chat** directory and use npm tooinstall hello modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="f9d95-122">라는 하위 폴더에 hello 모듈을 설치 됩니다.이 **node_modules**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-122">This will install hello modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="f9d95-123">Azure 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f9d95-123">Create an Azure Web App</span></span>
<span data-ttu-id="f9d95-124">이러한 단계 toocreate Azure 웹 앱, Git 게시를 활성화 하 고 hello 웹 앱에 대 한 WebSocket 지원을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-124">Follow these steps toocreate an Azure web app, enable Git publishing, and then enable WebSocket support for hello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="f9d95-125">toocomplete이이 자습서에서는 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-125">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="f9d95-126">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f9d95-127">자세한 내용은 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure 무료 체험</a>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9d95-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="f9d95-128">Hello Azure 명령줄 인터페이스 (Azure CLI)를 설치 하 고 tooyour Azure 구독을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-128">Install hello Azure Command-Line Interface (Azure CLI) and connect tooyour Azure subscription.</span></span> <span data-ttu-id="f9d95-129">참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-129">See [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="f9d95-130">Azure에서 리포지토리를 첫 번째 시간 설정에 이면 toocreate 로그인 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-130">If this is your first time setting up a repository in Azure, you need toocreate login credentials.</span></span> <span data-ttu-id="f9d95-131">Hello Azure CLI에서 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-131">From hello Azure CLI, enter hello following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="f9d95-132">Toohello 변경  **\\node\chat** 디렉터리 및 사용 하 여 hello 다음 toocreate 새 Azure 웹 앱 및 로컬 Git 리포지토리에서 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-132">Change toohello **\\node\chat** directory and use hello following command toocreate a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="f9d95-133">이 명령은 'azure'라는 Git 원격도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="f9d95-134">'mysitename'을 웹 앱의 고유한 이름으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="f9d95-135">다음 명령을 hello를 사용 하 여 hello 기존 파일 toohello 로컬 리포지토리를 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="f9d95-135">Commit hello existing files toohello local repository by using hello following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="f9d95-136">다음 명령을 hello로 hello 파일 toohello Azure 웹 앱 리포지토리 푸시:</span><span class="sxs-lookup"><span data-stu-id="f9d95-136">Push hello files toohello Azure Web Apps repository with hello following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="f9d95-137">메시지가 표시되면 2단계에서 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="f9d95-138">Hello 서버에서 가져오지 않는 모듈 상태 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-138">You will receive status messages as modules are imported on hello server.</span></span> <span data-ttu-id="f9d95-139">이 프로세스가 완료 되 면 hello 응용 프로그램을 Azure 웹 앱에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-139">Once this process has completed, hello application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f9d95-140">모듈 설치 하는 동안 오류가 나타날 수 있습니다 하는 ' hello 가져온된 프로젝트... 찾을 수 없습니다 '.</span><span class="sxs-lookup"><span data-stu-id="f9d95-140">During module installation, you may notice errors that 'hello imported project ... was not found'.</span></span> <span data-ttu-id="f9d95-141">이 오류는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="f9d95-142">Socket.IO는 Azure에서 기본적으로 사용되지 않는 WebSocket을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="f9d95-143">다음 명령을 사용 하 여 hello tooenable 웹 소켓:</span><span class="sxs-lookup"><span data-stu-id="f9d95-143">tooenable web sockets, use hello following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="f9d95-144">메시지가 표시 되 면 hello 웹 앱의 hello 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-144">If prompted, enter hello name of hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f9d95-145">안녕 버전 0.7.4 에서만 작동 이상 hello Azure 명령줄 인터페이스의 azure 사이트 설정-w 명령 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-145">hello 'azure site set -w' command will work only with version 0.7.4 or higher of hello Azure Command-Line Interface.</span></span> <span data-ttu-id="f9d95-146">WebSocket 지원 hello를 사용 하 여 설정할 수도 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-146">You can also enable WebSocket support using hello [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="f9d95-147">tooenable WebSockets를 사용 하 여 Azure 포털 hello hello 웹 응용 프로그램에서 웹 앱 블레이드 hello 클릭 하 고 **모든 설정을** > **응용 프로그램 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-147">tooenable WebSockets using hello Azure Portal, click hello web app from hello Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="f9d95-148">**웹 소켓**에서 **켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="f9d95-149">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="f9d95-150">tooview hello 웹 응용 프로그램에 액세스, 사용 하 여 hello 다음 명령 toolaunch 웹 브라우저를 toohello 호스팅된 웹 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-150">tooview hello web app on Azure, use hello following command toolaunch your web browser and navigate toohello hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="f9d95-151">현재 앱이 Azure에서 실행되고 있으며 Socket.IO를 사용하여 다른 클라이언트 간에 채팅 메시지를 릴레이할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="f9d95-152">확장</span><span class="sxs-lookup"><span data-stu-id="f9d95-152">Scale out</span></span>
<span data-ttu-id="f9d95-153">사용 하 여 Socket.IO 응용 프로그램을 확장할 수 있습니다는 **어댑터** toodistribute 메시지 및 이벤트 여러 응용 프로그램 인스턴스가 사이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-153">Socket.IO applications can be scaled out by using an **adapter** toodistribute messages and events between multiple application instances.</span></span> <span data-ttu-id="f9d95-154">사용 가능한 어댑터가 여러 개 있을 때는 hello [socket.io redis] hello Azure Redis 캐시 기능을 통해 어댑터를 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-154">While there are several adapters available, hello [socket.io-redis] adapter can be easily used with hello Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="f9d95-155">Socket.IO 솔루션 확장에 대한 추가 요구 사항은 고정 세션의 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="f9d95-156">고정 세션은 Azure 요청 라우팅을 통해 Azure 웹 앱에서 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="f9d95-157">자세한 내용은 [Azure 웹 사이트의 인스턴스 선호도]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9d95-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="f9d95-158">Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="f9d95-158">Create a Redis cache</span></span>
<span data-ttu-id="f9d95-159">Hello 단계를 수행 [Azure Redis Cache에서 캐시 만들기] toocreate 새 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-159">Perform hello steps in [Create a cache in Azure Redis Cache] toocreate a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="f9d95-160">Hello 저장 **호스트 이름** 및 **기본 키** 캐시에 필요 이러한 대로 hello 다음 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-160">Save hello **Host name** and **Primary key** for your cache, as these will be needed in hello next steps.</span></span>
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a><span data-ttu-id="f9d95-161">Hello redis 및 socket.io redis 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="f9d95-161">Add hello redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="f9d95-162">명령줄에서 변경 toohello  **\\노드\\채팅** 다음 명령을 디렉터리 및 사용 하 여 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-162">From a command-line, change toohello **\\node\\chat** directory and use hello following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="f9d95-163">이 명령에 지정 된 hello 버전은이 문서를 테스트할 때 사용 하는 hello 버전.</span><span class="sxs-lookup"><span data-stu-id="f9d95-163">hello versions specified in this command are hello versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="f9d95-164">Hello 수정 **app.js** 직후 파일 tooadd hello 다음 줄`var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="f9d95-164">Modify hello **app.js** file tooadd hello following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="f9d95-165">대체 **redishostname** 및 **rediskey** hello 호스트 이름과 Redis 캐시에 대 한 키 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-165">Replace **redishostname** and **rediskey** with hello host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="f9d95-166">게시를 만들고 클라이언트 toohello 이전에 만든 Redis cache를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-166">This will create a publish and subscribe client toohello Redis cache created previously.</span></span> <span data-ttu-id="f9d95-167">hello 클라이언트는 다음 hello 어댑터 tooconfigure Socket.IO toouse hello Redis 캐시에 대 사용 응용 프로그램의 인스턴스 간에 메시지 및 이벤트를 전달</span><span class="sxs-lookup"><span data-stu-id="f9d95-167">hello clients are then used with hello adapter tooconfigure Socket.IO toouse hello Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f9d95-168">Hello 동안 **socket.io redis** 어댑터 직접 tooRedis 통신할 수, 현재 버전 hello Azure Redis 캐시에 필요한 hello 인증을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-168">While hello **socket.io-redis** adapter can communicate directly tooRedis, hello current version does not support hello authentication required by Azure Redis cache.</span></span> <span data-ttu-id="f9d95-169">Hello를 사용 하 여 hello 초기 연결 되어 만들어 **redis** 모듈에서는 다음 hello 클라이언트 전달 toohello **socket.io redis** 어댑터.</span><span class="sxs-lookup"><span data-stu-id="f9d95-169">So hello initial connection is created using hello **redis** module, then hello client is passed toohello **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="f9d95-170">Azure Redis Cache를 6380 포트를 사용 하 여 보안 연결을 지원 하지만이 예에서 사용 된 hello 모듈 2014 년 7 월 14를 기준으로 하는 보안 연결을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-170">While Azure Redis Cache supports secure connections using port 6380, hello modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="f9d95-171">코드 위의 hello hello 기본적으로 6379의 보안 되지 않은 포트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-171">hello above code uses hello default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="f9d95-172">수정 저장 hello **app.js**</span><span class="sxs-lookup"><span data-stu-id="f9d95-172">Save hello modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="f9d95-173">변경 내용 커밋 및 다시 배포</span><span class="sxs-lookup"><span data-stu-id="f9d95-173">Commit changes and redeploy</span></span>
<span data-ttu-id="f9d95-174">Hello hello에 명령줄에서  **\\노드\\채팅** 디렉터리 명령을 toocommit 변경 내용을 따라 hello를 사용 하 여 및 hello 응용 프로그램을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-174">From hello command-line in hello **\\node\\chat** directory, use hello following commands toocommit changes and redeploy hello application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="f9d95-175">Hello 변경 내용이 toohello 서버 푸시 되었습니다 면 hello 다음 명령을 사용 하 여 여러 인스턴스에 걸쳐 사이트를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-175">Once hello changes have been pushed toohello server, you can scale your site across multiple instances by using hello following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="f9d95-176">여기서  **#**  인스턴스 toocreate hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-176">Where **#** is hello number of instances toocreate.</span></span>

<span data-ttu-id="f9d95-177">여러 브라우저 또는 컴퓨터 tooverify 배달 되는 메시지 올바르게 tooall 클라이언트에서에서 tooyour 웹 응용 프로그램을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-177">You can connect tooyour web app from multiple browsers or computers tooverify that messages are correctly sent tooall clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f9d95-178">문제 해결</span><span class="sxs-lookup"><span data-stu-id="f9d95-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="f9d95-179">연결 제한</span><span class="sxs-lookup"><span data-stu-id="f9d95-179">Connection limits</span></span>
<span data-ttu-id="f9d95-180">Azure 웹 앱 hello 리소스 사용 가능한 tooyour 사이트를 결정 하는 여러 Sku에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-180">Azure Web Apps is available in multiple SKUs, which determine hello resources available tooyour site.</span></span> <span data-ttu-id="f9d95-181">여기에 hello 허용 된 WebSocket 연결 수가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-181">This includes hello number of allowed WebSocket connections.</span></span> <span data-ttu-id="f9d95-182">자세한 내용은 참조 hello [웹 앱 가격 페이지]합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-182">For more information, see hello [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="f9d95-183">메시지가 WebSocket을 사용하여 전송되지 않음</span><span class="sxs-lookup"><span data-stu-id="f9d95-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="f9d95-184">클라이언트 브라우저 Websocket을 사용 하는 대신 폴링 toolong 다시 떨어지고 유지 hello 다음 중 하나로 인해 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-184">If client browsers keep falling back toolong polling instead of using WebSockets, it may be because of one of hello following.</span></span>

* <span data-ttu-id="f9d95-185">**Hello 전송 toojust Websocket 제한**</span><span class="sxs-lookup"><span data-stu-id="f9d95-185">**Try limiting hello transport toojust WebSockets**</span></span>
  
    <span data-ttu-id="f9d95-186">Socket.IO toouse 전송 메시징 hello로 Websocket에서에서 hello 서버와 클라이언트 Websocket을 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-186">In order for Socket.IO toouse WebSockets as hello messaging transport, both hello server and client must support WebSockets.</span></span> <span data-ttu-id="f9d95-187">하나 또는 다른 hello를 가리키지 않으면 Socket.IO 긴 폴링 같은 다른 전송에서 협상 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-187">If one or hello other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="f9d95-188">hello 기본 Socket.IO에서 사용 되는 전송 목록은 ` websocket, htmlfile, xhr-polling, jsonp-polling`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-188">hello default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="f9d95-189">다음 코드 toohello hello를 추가 하 여 tooonly 사용 하 여 Websocket 강제로 수 있습니다 **app.js** 파일을 포함 하는 hello 줄 후 `, nicknames = {};`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-189">You can force it tooonly use WebSockets by adding hello following code toohello **app.js** file, after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="f9d95-190">참고 Websocket을 지원 하지 않는 이전 버전의 브라우저 수 없음을 수 tooconnect toohello 사이트 통신 tooWebSockets만을 제한 하는 대로 코드 위의 hello를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-190">Note that older browsers that do not support WebSockets will not be able tooconnect toohello site while hello above code is active, as it restricts communication tooWebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="f9d95-191">**SSL 사용**</span><span class="sxs-lookup"><span data-stu-id="f9d95-191">**Use SSL**</span></span>
  
    <span data-ttu-id="f9d95-192">Websocket hello와 같은 사용 되는 일부 미만 HTTP 헤더, 의존 **업그레이드** 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-192">WebSockets relies on some lesser used HTTP headers, such as hello **Upgrade** header.</span></span> <span data-ttu-id="f9d95-193">웹 프록시와 같은 일부 중간 네트워크 장치는 이러한 헤더를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="f9d95-194">tooavoid이이 문제를 SSL을 통한 hello WebSocket 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-194">tooavoid this problem, you can establish hello WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="f9d95-195">쉽게 tooaccomplish tooconfigure Socket.IO를 너무 이것이`match origin protocol`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-195">An easy way tooaccomplish this is tooconfigure Socket.IO too`match origin protocol`.</span></span> <span data-ttu-id="f9d95-196">이렇게 하면 Socket.IO toosecure Websocket 통신 hello hello 웹 페이지에 대 한 요청 HTTP/HTTPS를 시작 하는 hello와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-196">This instructs Socket.IO toosecure WebSockets communication hello same as hello originating HTTP/HTTPS request for hello web page.</span></span> <span data-ttu-id="f9d95-197">브라우저는 HTTPS URL toovisit 웹 사이트를 사용 하면 후속 WebSocket 통신 Socket.IO 통해 SSL을 통해 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-197">If a browser uses an HTTPS URL toovisit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="f9d95-198">toomodify이 예제에서는 tooenable이이 구성에서는 다음 코드 toohello hello 추가 **app.js** 포함 하는 hello 줄 후 파일 `, nicknames = {};`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-198">toomodify this example tooenable this configuration, add hello following code toohello **app.js** file after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="f9d95-199">**web.config 설정 확인**</span><span class="sxs-lookup"><span data-stu-id="f9d95-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="f9d95-200">Node.js 응용 프로그램을 호스트 하는 azure 웹 앱 hello를 사용 하 여 **web.config** 파일 tooroute 들어오는 toohello Node.js 응용 프로그램을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-200">Azure web apps that host Node.js applications use hello **web.config** file tooroute incoming requests toohello Node.js application.</span></span> <span data-ttu-id="f9d95-201">Node.js 응용 프로그램에서 올바로 Websocket toofunction, hello **web.config** hello 다음 항목을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-201">For WebSockets toofunction correctly with Node.js applications, hello **web.config** must contain hello following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="f9d95-202">그러면 Websocket 및 Socket.IO 등의 특정 WebSocket 모듈 Node.js와 충돌의 자체 구현을 포함 하는 hello IIS WebSockets 모듈을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-202">This disables hello IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="f9d95-203">이 줄이 없으면 또는 너무 설정 된 경우`true`, hello 이유 hello WebSocket 전송 응용 프로그램에 대해 작동 하지 않는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-203">If this line is not present, or is set too`true`, this may be hello reason that hello WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="f9d95-204">일반적으로 Node.js 응용 프로그램에는 **web.config** 파일이 포함되어 있지 않으므로 Azure 웹 사이트를 배포할 때 해당 웹 사이트에서 Node.js 응용 프로그램에 대해 이 파일을 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="f9d95-205">Hello 서버에서이 파일은 자동으로 생성 하므로이 파일을 사용 해야 hello FTP 또는 FTPS URL에 대 한 웹 사이트 tooview이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-205">Since this file is automatically generated on hello server, you must use hello FTP or FTPS URL for your website tooview this file.</span></span> <span data-ttu-id="f9d95-206">Hello FTP 및 FTPS Url이 사이트에 대 한 hello 클래식 포털에서 웹 앱을 선택 하 여 찾아 수 다음 hello **대시보드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-206">You can find hello FTP and FTPS URLs for your site in hello classic portal by selecting your web app, and then hello **Dashboard** link.</span></span> <span data-ttu-id="f9d95-207">hello Url에에서 표시 되는 hello **눈에 보는** 섹션.</span><span class="sxs-lookup"><span data-stu-id="f9d95-207">hello URLs are displayed in hello **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="f9d95-208">hello **web.config** 파일이 응용 프로그램 하나를 제공 하지 않는 경우에 Azure 웹 사이트에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-208">hello **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="f9d95-209">제공 하는 경우는 **web.config** 파일 hello 응용 프로그램 프로젝트의 루트에 있는 것에서 사용할 Azure 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-209">If you provide a **web.config** file in hello root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="f9d95-210">Hello 항목이 없으면, 또는의 tooa 값으로 설정 되어 있으면 `true`를 만들어야 합니다는 **web.config** 에서 Node.js 응용 프로그램의 루트 hello 하 고 값을 지정 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-210">If hello entry is not present, or is set tooa value of `true`, then you should create a **web.config** in hello root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="f9d95-211">참조의 경우, 아래 hello은 기본 **web.config** 사용 하는 응용 프로그램에 대 한 **app.js** hello 진입점으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-211">For reference, hello below is a default **web.config** for an application that uses **app.js** as hello entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="f9d95-212">응용 프로그램 진입점이 아닌 다른 사용 **app.js**의 항목을 모두 바꾸어야 **app.js** hello로 진입점을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with hello correct entry point.</span></span> <span data-ttu-id="f9d95-213">예를 들어 **app.js**를 **server.js**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="f9d95-214">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도]앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-214">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f9d95-215">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f9d95-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f9d95-216">Next steps</span></span>
<span data-ttu-id="f9d95-217">이 자습서에서는 어떻게 toocreate 채팅 응용 프로그램에서에서 호스트 되는 Azure 웹 앱 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-217">In this tutorial you learned how toocreate a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="f9d95-218">이 응용 프로그램은 Azure 클라우드 서비스로 호스트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="f9d95-219">방법에 대 한 단계 tooaccomplish이,이 참조 [Azure 클라우드 서비스에 사용 하는 Node.js 채팅 응용 Socket.IO 빌드]합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-219">For steps on how tooaccomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="f9d95-220">자세한 내용은 참고 항목 hello [Node.js 개발자 센터]합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-220">For more information, see also hello [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f9d95-221">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="f9d95-221">What's changed</span></span>
* <span data-ttu-id="f9d95-222">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [Azure 앱 서비스 및 기존 Azure 서비스에 대 한 해당 영향]합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d95-222">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

[Azure Redis Cache]: /documentation/services/redis-cache/
[앱 서비스 웹 앱]: http://go.microsoft.com/fwlink/?LinkId=529714
[웹 앱 가격 페이지]: http://go.microsoft.com/fwlink/?LinkId=511643
[Azure 클라우드 서비스에 사용 하는 Node.js 채팅 응용 Socket.IO 빌드]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[Azure 앱 서비스 및 기존 Azure 서비스에 대 한 해당 영향]: http://go.microsoft.com/fwlink/?LinkId=529714
[Node.js 개발자 센터]: /develop/nodejs/
[앱 서비스 시도]: https://azure.microsoft.com/try/app-service/
[Azure 웹 사이트의 인스턴스 선호도]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[Azure Redis Cache에서 캐시 만들기]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[Socket.IO GitHub 리포지토리]: https://github.com/socketio/socket.io
[ZIP 또는 GZ 보관 릴리스]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
