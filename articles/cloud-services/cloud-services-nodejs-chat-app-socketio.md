---
title: "Socket.io를 사용 하 여 aaaNode.js 응용 | Microsoft Docs"
description: "Azure에서 node.js 응용 프로그램에서 toouse socket.io 호스팅 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="c985e-103">Azure 클라우드 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="c985e-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="c985e-104">Socket.IO는 node.js 서버와 클라이언트 간에 실시간 커뮤니케이션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="c985e-105">이 자습서는 Azure에서 채팅 응용 프로그램을 기반으로 하는 socket.IO 호스팅에 대해 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="c985e-106">Socket.IO에 대한 자세한 내용은 <http://socket.io/>(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c985e-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="c985e-107">완료 하는 hello 응용 프로그램의 스크린샷을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-107">A screenshot of hello completed application is below:</span></span>

![Azure에서 호스팅된 hello 서비스를 표시 하는 브라우저 창][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="c985e-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c985e-109">Prerequisites</span></span>
<span data-ttu-id="c985e-110">제품에 따라 해당 hello를 확인 하 고 버전은이 문서에 설치 된 toosuccessfully 완료 hello 예제:</span><span class="sxs-lookup"><span data-stu-id="c985e-110">Ensure that hello following products and versions are installed toosuccessfully complete hello example in this article:</span></span>

* <span data-ttu-id="c985e-111">[Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="c985e-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="c985e-112">[Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="c985e-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="c985e-113">[Python 버전 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="c985e-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="c985e-114">클라우드 서비스 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c985e-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="c985e-115">hello 다음 단계 hello 클라우드 서비스 프로젝트를 만들 hello Socket.IO 응용 프로그램을 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-115">hello following steps create hello cloud service project that will host hello Socket.IO application.</span></span>

1. <span data-ttu-id="c985e-116">Hello에서 **시작 메뉴** 또는 **시작 화면**, 검색할 **Windows PowerShell**합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-116">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="c985e-117">마지막으로, **Windows PowerShell**을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell 아이콘][powershell-menu]
2. <span data-ttu-id="c985e-119">**c:\\node**라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="c985e-120">디렉터리 toohello 변경 **c:\\노드** 디렉터리</span><span class="sxs-lookup"><span data-stu-id="c985e-120">Change directories toohello **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="c985e-121">Hello 명령을 toocreate 이라는 새 솔루션을 다음 입력 **chatapp** 라는 작업자 역할이 **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="c985e-121">Enter hello following commands toocreate a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="c985e-122">Hello 응답을 따라 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-122">You will see hello following response:</span></span>
   
    ![hello 새 azureservice 및 추가 azurenodeworkerrolecmdlets hello 출력](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a><span data-ttu-id="c985e-124">Hello 채팅 예제를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-124">Download hello Chat Example</span></span>
<span data-ttu-id="c985e-125">이 프로젝트에 대 한 hello 채팅 예제 hello에서 사용 합니다 [Socket.IO GitHub 리포지토리]합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-125">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="c985e-126">다음 단계 toodownload hello 예제 hello를 수행 하 고 앞에서 만든 toohello 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-126">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="c985e-127">Hello를 사용 하 여 hello 저장소의 로컬 복사본을 만들 **복제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-127">Create a local copy of hello repository by using hello **Clone** button.</span></span> <span data-ttu-id="c985e-128">Hello를 사용할 수 있습니다 **ZIP** 단추 toodownload hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="c985e-128">You may also use hello **ZIP** button toodownload hello project.</span></span>
   
   ![브라우저 창을 강조 표시 하는 hello ZIP 다운로드 아이콘으로 https://github.com/LearnBoost/socket.io/tree/master/examples/chat, 보기][chat-example-view]
2. <span data-ttu-id="c985e-130">Hello에 도착할 때까지 hello 로컬 저장소의 hello 디렉터리 구조를 탐색 **예제\\채팅** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-130">Navigate hello directory structure of hello local repository until you arrive at hello **examples\\chat** directory.</span></span> <span data-ttu-id="c985e-131">이 디렉터리 toothe의 hello 내용을 복사 **c:\\노드\\chatapp\\WorkerRole1** 앞에서 만든 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-131">Copy hello contents of this directory toothe **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![탐색기의 hello 예제 hello 내용 표시\\hello 보관 파일에서 추출 채팅 디렉터리][chat-contents]
   
   <span data-ttu-id="c985e-133">hello 강조 표시 된에 또한 위의 스크린 샷에서 hello 항목이 hello에서 복사 하는 hello 파일 **예제\\채팅** 디렉터리</span><span class="sxs-lookup"><span data-stu-id="c985e-133">hello highlighted items in hello screenshot above are hello files copied from hello **examples\\chat** directory</span></span>
3. <span data-ttu-id="c985e-134">Hello에 **c:\\노드\\chatapp\\WorkerRole1** 디렉터리, delete hello **server.js** 파일을 선택한 다음 이름을 hello **app.js**파일 너무**server.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-134">In hello **C:\\node\\chatapp\\WorkerRole1** directory, delete hello **server.js** file, and then rename hello **app.js** file too**server.js**.</span></span> <span data-ttu-id="c985e-135">이렇게 하면 제거 hello 기본 **server.js** hello에서 이전에 만든 파일 **추가 AzureNodeWorkerRole** cmdlet을 사용 하 여 hello 응용 프로그램에서 파일을 대체 hello 채팅 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-135">This removes hello default **server.js** file created previously by hello **Add-AzureNodeWorkerRole** cmdlet and replaces it with hello application file from hello chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="c985e-136">Server.js 수정 및 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="c985e-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="c985e-137">Hello Azure 에뮬레이터에서에서 테스트 hello 응용 프로그램, 하기 전에 항상 약간의 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-137">Before testing hello application in hello Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="c985e-138">다음 단계 toothe server.js 파일 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-138">Perform hello following steps toothe server.js file:</span></span>

1. <span data-ttu-id="c985e-139">열기 hello **server.js** Visual Studio 또는 임의의 텍스트 편집기에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-139">Open hello **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="c985e-140">Hello **모듈 종속성** hello server.js 맨 앞에 섹션 및 포함 하는 hello 줄 변경 **sio require('.. = //.. lib//socket.io')** 너무**sio require('socket.io') =** 아래와 같이:</span><span class="sxs-lookup"><span data-stu-id="c985e-140">Find hello **Module dependencies** section at hello beginning of server.js and change hello line containing **sio = require('..//..//lib//socket.io')** too**sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="c985e-141">hello 올바른 포트에서 수신 대기 tooensure hello 응용 프로그램 server.js 메모장 이나 선호 하는 편집기에서 열고 대체 하 여 다음 줄을 변경 **3000** 와 **process.env.port** 표시 된 것 처럼 아래:</span><span class="sxs-lookup"><span data-stu-id="c985e-141">tooensure hello application listens on hello correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="c985e-142">너무 hello 변경 내용을 저장 한 후**server.js**단계를 수행 하는 hello를 사용 하 여 필요한 모듈을 설치 하 고 다음 Azure 에뮬레이터에서 hello 응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-142">After saving hello changes too**server.js**, use hello following steps to install required modules, and then test hello application in the Azure emulator:</span></span>

1. <span data-ttu-id="c985e-143">사용 하 여 **Azure PowerShell**, 디렉터리 toohello 변경 **c:\\노드\\chatapp\\WorkerRole1** 명령 tooinstall hello 다음 디렉터리 및 사용 하 여 hello 이 응용 프로그램에 필요한 모듈:</span><span class="sxs-lookup"><span data-stu-id="c985e-143">Using **Azure PowerShell**, change directories toohello **C:\\node\\chatapp\\WorkerRole1** directory and use hello following command tooinstall hello modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="c985e-144">그러면 hello package.json 파일에 나열 된 hello 모듈 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-144">This will install hello modules listed in hello package.json file.</span></span> <span data-ttu-id="c985e-145">Hello 명령이 완료 된 후 비슷한 toothe 다음 출력이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-145">After hello command completes, you should see output similar toothe following:</span></span>
   
   ![hello 출력의 hello npm 설치 명령][The-output-of-the-npm-install-command]
2. <span data-ttu-id="c985e-147">이 예에서는 원래 hello Socket.IO GitHub 리포지토리의 일부 였 고 hello Socket.IO 라이브러리 상대 경로에서 직접 참조를에서는 hello 다음 명령을 실행 하 여 설치 해야 하므로 Socket.IO hello package.json 파일에서 참조 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-147">Since this example was originally a part of hello Socket.IO GitHub repository, and directly referenced hello Socket.IO library by relative path, Socket.IO was not referenced in hello package.json file, so we must install it by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="c985e-148">테스트 및 배포</span><span class="sxs-lookup"><span data-stu-id="c985e-148">Test and Deploy</span></span>
1. <span data-ttu-id="c985e-149">Hello 다음 명령을 실행 하 여 hello 에뮬레이터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-149">Launch hello emulator by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="c985e-150">에뮬레이터 시작 문제가 발생하는 경우(예: Start-AzureEmulator: 예기치 않은 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="c985e-151">세부 정보: 발생 했습니다. 예기치 않은 오류 hello 통신 개체 System.ServiceModel.Channels.ServiceChannel 사용할 수 없습니다 통신을 위해 hello Faulted 상태 이기 때문에.</span><span class="sxs-lookup"><span data-stu-id="c985e-151">Details: Encountered an unexpected error hello communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in hello Faulted state.</span></span>
   
      <span data-ttu-id="c985e-152">AzureAuthoringTools v 2.7.1 및 AzureComputeEmulator v 2.7을 다시 설치하세요. 버전이 일치하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c985e-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="c985e-153">브라우저를 열고 너무 이동**http://127.0.0.1**합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-153">Open a browser and navigate too**http://127.0.0.1**.</span></span>
3. <span data-ttu-id="c985e-154">Hello 브라우저 창이 열리면 별명을 입력 한 다음 enter 키를 눌러 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-154">When hello browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="c985e-155">이렇게 하면 toopost 메시지 특정 애칭으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-155">This will allow you toopost messages as a specific nickname.</span></span> <span data-ttu-id="c985e-156">tootest 다중 사용자 기능을 동일한 URL을 사용 하 여 다른 브라우저 창을 열고 다른 애칭을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-156">tootest multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![User1 및 User2의 채팅 메시지를 표시하는 두 브라우저 창](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="c985e-158">Hello 응용 프로그램을 테스트 한 후 다음 명령을 실행 하 여 hello 에뮬레이터를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-158">After testing hello application, stop hello emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="c985e-159">toodeploy hello 응용 프로그램 tooAzure를 사용 하 여는 **게시 AzureServiceProject** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c985e-159">toodeploy hello application tooAzure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="c985e-160">예:</span><span class="sxs-lookup"><span data-stu-id="c985e-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="c985e-161">있는지 toouse 고유 이름 수, 그렇지 않으면 hello 게시 프로세스에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-161">Be sure toouse a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="c985e-162">Hello 배포 완료 되 면 hello 브라우저 열리고 toohello 배포 된 서비스를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-162">After hello deployment has completed, hello browser will open and navigate toohello deployed service.</span></span>
   > 
   > <span data-ttu-id="c985e-163">구독 이름을 가져올 hello에 없으면 해당 hello 제공 알리는 오류가 표시 되 면 게시 프로필, 다운로드 하 고 tooAzure를 배포 하기 전에 구독을 위한 hello 게시 프로필을 가져올 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-163">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="c985e-164">Hello 참조 **hello 응용 프로그램 tooAzure 배포** 섹션 [빌드하고 Node.js 응용 프로그램 tooan Azure 클라우드 서비스 배포](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="c985e-164">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Azure에서 호스팅된 hello 서비스를 표시 하는 브라우저 창][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="c985e-166">구독 이름을 가져올 hello에 없으면 해당 hello 제공 알리는 오류가 표시 되 면 게시 프로필, 다운로드 하 고 tooAzure를 배포 하기 전에 구독을 위한 hello 게시 프로필을 가져올 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-166">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="c985e-167">Hello 참조 **hello 응용 프로그램 tooAzure 배포** 섹션 [빌드하고 Node.js 응용 프로그램 tooan Azure 클라우드 서비스 배포](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="c985e-167">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="c985e-168">현재 응용 프로그램이 Azure에서 실행되고 있으며 Socket.IO를 사용하여 다른 클라이언트 간에 채팅 메시지를 릴레이할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="c985e-169">간단한 설명을 위해이 샘플은 사용자가 연결 된 toohello 사이의 제한 toochatting 동일한 인스턴스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-169">For simplicity, this sample is limited toochatting between users connected toohello same instance.</span></span> <span data-ttu-id="c985e-170">즉, 두 작업자 역할 인스턴스를 hello 클라우드 서비스를 만드는 경우 사용자는 에서만 수 있다는 toochat 사람과 연결 toohello 동일한 작업자 역할 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="c985e-170">This means that if hello cloud service creates two worker role instances, users will only be able toochat with others connected toohello same worker role instance.</span></span> <span data-ttu-id="c985e-171">여러 역할 인스턴스와 tooscale hello 응용 프로그램 toowork, 인스턴스 간에 기술 서비스 버스 tooshare hello Socket.IO 저장소 상태와 같은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-171">tooscale hello application toowork with multiple role instances, you could use a technology like Service Bus tooshare hello Socket.IO store state across instances.</span></span> <span data-ttu-id="c985e-172">예제를 보려면 hello에서 hello 서비스 버스 큐 및 항목 사용 예제를 참조 [Azure SDK for Node.js GitHub 리포지토리](https://github.com/WindowsAzure/azure-sdk-for-node)합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-172">For examples, see hello Service Bus Queues and Topics usage samples in hello [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c985e-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c985e-173">Next steps</span></span>
<span data-ttu-id="c985e-174">이 자습서 toocreate 기본 채팅 응용 프로그램 호스팅 방법 Azure 클라우드 서비스에 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-174">In this tutorial you learned how toocreate a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="c985e-175">toolearn toohost는 Azure 웹 사이트에서이 응용 프로그램 확인 하려면 어떻게 해야 [Azure 웹 사이트에서 사용 하는 Node.js 채팅 응용 Socket.IO 빌드][chatwebsite]합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-175">toolearn how toohost this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="c985e-176">자세한 내용은 참고 항목 hello [Node.js 개발자 센터](/develop/nodejs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c985e-176">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Socket.IO GitHub 리포지토리]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


