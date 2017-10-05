---
title: "Socket.io를 사용하는 Node.js 응용 프로그램 | Microsoft Docs"
description: "Azure에 호스트된 node.js 응용 프로그램에서 socket.io를 사용하는 방법을 알아봅니다."
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
ms.openlocfilehash: a85d4348a13b79b5b7542362de9956aa3398375a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="5810d-103">Azure 클라우드 서비스에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="5810d-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="5810d-104">Socket.IO는 node.js 서버와 클라이언트 간에 실시간 커뮤니케이션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="5810d-105">이 자습서는 Azure에서 채팅 응용 프로그램을 기반으로 하는 socket.IO 호스팅에 대해 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="5810d-106">Socket.IO에 대한 자세한 내용은 <http://socket.io/>(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5810d-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="5810d-107">아래에는 완성된 응용 프로그램의 스크린샷이 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-107">A screenshot of the completed application is below:</span></span>

![Azure에 호스트된 서비스를 표시하는 브라우저 창][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="5810d-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5810d-109">Prerequisites</span></span>
<span data-ttu-id="5810d-110">이 문서의 예제를 완료하려면 다음 제품 및 버전이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-110">Ensure that the following products and versions are installed to successfully complete the example in this article:</span></span>

* <span data-ttu-id="5810d-111">[Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="5810d-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="5810d-112">[Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="5810d-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="5810d-113">[Python 버전 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="5810d-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="5810d-114">클라우드 서비스 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="5810d-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="5810d-115">다음은 Socket.IO 응용 프로그램을 호스트하는 클라우드 서비스 프로젝트를 만드는 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-115">The following steps create the cloud service project that will host the Socket.IO application.</span></span>

1. <span data-ttu-id="5810d-116">**시작 메뉴** 또는 **시작 화면**에서 **Windows PowerShell**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-116">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="5810d-117">마지막으로, **Windows PowerShell**을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell 아이콘][powershell-menu]
2. <span data-ttu-id="5810d-119">**c:\\node**라는 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="5810d-120">디렉터리를 **c:\\node** 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-120">Change directories to the **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="5810d-121">다음 명령을 입력하여 **chatapp**라는 이름의 새 솔루션과 **WorkerRole1**이라는 작업자 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-121">Enter the following commands to create a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="5810d-122">You will see the following response:</span><span class="sxs-lookup"><span data-stu-id="5810d-122">You will see the following response:</span></span>
   
    ![new-azureservice 및 add-azurenodeworkerrolecmdlets의 출력](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-the-chat-example"></a><span data-ttu-id="5810d-124">채팅 예제 다운로드</span><span class="sxs-lookup"><span data-stu-id="5810d-124">Download the Chat Example</span></span>
<span data-ttu-id="5810d-125">이 프로젝트에서는 [Socket.IO GitHub 리포지토리](영문)의 채팅 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-125">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="5810d-126">다음 단계에 따라 예제를 다운로드하여 이전에 만든 프로젝트에 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="5810d-126">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="5810d-127">**복제** 단추를 눌러 리포지토리의 로컬 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-127">Create a local copy of the repository by using the **Clone** button.</span></span> <span data-ttu-id="5810d-128">**ZIP** 단추를 눌러 프로젝트를 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-128">You may also use the **ZIP** button to download the project.</span></span>
   
   ![ZIP 다운로드 아이콘이 강조 표시된 https://github.com/LearnBoost/socket.io/tree/master/examples/chat을 표시하는 브라우저 창][chat-example-view]
2. <span data-ttu-id="5810d-130">**examples\\chat** 디렉터리를 찾을 때까지 로컬 리포지토리의 디렉터리 구조를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-130">Navigate the directory structure of the local repository until you arrive at the **examples\\chat** directory.</span></span> <span data-ttu-id="5810d-131">이 디렉터리의 내용을 이전에 만든 **C:\\node\\chatapp\\WorkerRole1** 디렉터리로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-131">Copy the contents of this directory to the **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![보관 파일에서 압축을 푼 examples\\chat 디렉터리의 내용을 표시하는 탐색기][chat-contents]
   
   <span data-ttu-id="5810d-133">위 스크린샷에서 강조 표시된 항목은 **examples\\chat** 디렉터리에서 복사한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-133">The highlighted items in the screenshot above are the files copied from the **examples\\chat** directory</span></span>
3. <span data-ttu-id="5810d-134">**C:\\node\\chatapp\\WorkerRole1** 디렉터리에서 **server.js** 파일을 삭제한 다음 **app.js** 파일의 이름을 **server.js**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-134">In the **C:\\node\\chatapp\\WorkerRole1** directory, delete the **server.js** file, and then rename the **app.js** file to **server.js**.</span></span> <span data-ttu-id="5810d-135">그러면 이전에 **Add-AzureNodeWorkerRole** cmdlet로 만든 기본 **server.js** 파일이 제거되고 채팅 예제의 응용 프로그램 파일로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-135">This removes the default **server.js** file created previously by the **Add-AzureNodeWorkerRole** cmdlet and replaces it with the application file from the chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="5810d-136">Server.js 수정 및 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="5810d-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="5810d-137">Azure 에뮬레이터에서 응용 프로그램을 테스트하기 전에 몇 가지 항목을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-137">Before testing the application in the Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="5810d-138">server.js 파일에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-138">Perform the following steps to the server.js file:</span></span>

1. <span data-ttu-id="5810d-139">Visual Studio 또는 임의의 텍스트 편집기에서 **server.js** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-139">Open the **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="5810d-140">server.js의 시작 부분에서 **모듈 종속성** 섹션을 찾아 아래와 같이 **sio = require('..//..//lib//socket.io')**가 포함된 줄을 **sio = require('socket.io')**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-140">Find the **Module dependencies** section at the beginning of server.js and change the line containing **sio = require('..//..//lib//socket.io')** to **sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="5810d-141">응용 프로그램이 올바른 포트에서 수신하도록 메모장 또는 좋아하는 편집기에서 server.js를 연 후 아래와 같이 다음 줄에서 **3000**을 **process.env.port**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-141">To ensure the application listens on the correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="5810d-142">**server.js**에 변경 내용을 저장한 후 다음 단계에 따라 필요한 모듈을 설치하고 Azure 에뮬레이터에서 응용 프로그램을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-142">After saving the changes to **server.js**, use the following steps to install required modules, and then test the application in the Azure emulator:</span></span>

1. <span data-ttu-id="5810d-143">**Azure PowerShell**을 사용하여 디렉터리를 **C:\\node\\chatapp\\WorkerRole1** 디렉터리를 변경하고 다음 명령을 사용하여 이 응용 프로그램에서 필요한 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-143">Using **Azure PowerShell**, change directories to the **C:\\node\\chatapp\\WorkerRole1** directory and use the following command to install the modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="5810d-144">그러면 package.json 파일에 나열된 모듈이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-144">This will install the modules listed in the package.json file.</span></span> <span data-ttu-id="5810d-145">명령을 완료한 후 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-145">After the command completes, you should see output similar to the following:</span></span>
   
   ![npm 설치 명령의 출력][The-output-of-the-npm-install-command]
2. <span data-ttu-id="5810d-147">이 예제는 원래 Socket.IO GitHub 리포지토리의 일부이고, 상대 경로에서 Socket.IO 라이브러리를 직접 참조하며 package.json 파일에서 Socket.IO가 참조되지 않기 때문에 다음 명령을 실행하여 모듈을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-147">Since this example was originally a part of the Socket.IO GitHub repository, and directly referenced the Socket.IO library by relative path, Socket.IO was not referenced in the package.json file, so we must install it by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="5810d-148">테스트 및 배포</span><span class="sxs-lookup"><span data-stu-id="5810d-148">Test and Deploy</span></span>
1. <span data-ttu-id="5810d-149">다음 명령을 실행하여 에뮬레이터를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-149">Launch the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="5810d-150">에뮬레이터 시작 문제가 발생하는 경우(예: Start-AzureEmulator: 예기치 않은 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="5810d-151">세부 정보: 예기치 않은 오류가 발생했습니다. 통신 개체 System.ServiceModel.Channels.ServiceChannel은(는) Faulted 상태이기 때문에 통신에 사용할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="5810d-151">Details: Encountered an unexpected error The communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in the Faulted state.</span></span>
   
      <span data-ttu-id="5810d-152">AzureAuthoringTools v 2.7.1 및 AzureComputeEmulator v 2.7을 다시 설치하세요. 버전이 일치하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5810d-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="5810d-153">브라우저를 열고 **http://127.0.0.1**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-153">Open a browser and navigate to **http://127.0.0.1**.</span></span>
3. <span data-ttu-id="5810d-154">브라우저 창이 열리면 애칭을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-154">When the browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="5810d-155">이렇게 하면 특정 애칭으로 메시지를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-155">This will allow you to post messages as a specific nickname.</span></span> <span data-ttu-id="5810d-156">다중 사용자 기능을 테스트하려면 같은 URL을 사용하여 브라우저 창을 추가로 열고 다른 애칭을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-156">To test multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![User1 및 User2의 채팅 메시지를 표시하는 두 브라우저 창](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="5810d-158">응용 프로그램을 테스트한 후 다음 명령을 실행하여 에뮬레이터를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-158">After testing the application, stop the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="5810d-159">Azure에 응용 프로그램을 배포하려면 **Publish-AzureServiceProject** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-159">To deploy the application to Azure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="5810d-160">예:</span><span class="sxs-lookup"><span data-stu-id="5810d-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="5810d-161">고유한 이름을 사용해야 합니다. 그렇지 않으면 게시 프로세스가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-161">Be sure to use a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="5810d-162">배포가 완료되면 브라우저가 열리고 배포된 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-162">After the deployment has completed, the browser will open and navigate to the deployed service.</span></span>
   > 
   > <span data-ttu-id="5810d-163">제공한 구독 이름이 가져온 게시 프로필에 존재하지 않는다는 내용의 오류를 받게 되는 경우, Azure를 배포하기 전에 구독에 대한 게시 프로필을 다운로드하고 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-163">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="5810d-164">**Azure 클라우드 서비스에 Node.js 응용 프로그램 빌드 및 배포** (영문)에서 [Azure에 응용 프로그램 배포](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="5810d-164">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Azure에 호스트된 서비스를 표시하는 브라우저 창][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="5810d-166">제공한 구독 이름이 가져온 게시 프로필에 존재하지 않는다는 내용의 오류를 받게 되는 경우, Azure를 배포하기 전에 구독에 대한 게시 프로필을 다운로드하고 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-166">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="5810d-167">**Azure 클라우드 서비스에 Node.js 응용 프로그램 빌드 및 배포** (영문)에서 [Azure에 응용 프로그램 배포](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="5810d-167">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="5810d-168">현재 응용 프로그램이 Azure에서 실행되고 있으며 Socket.IO를 사용하여 다른 클라이언트 간에 채팅 메시지를 릴레이할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="5810d-169">간단히 하기 위해 샘플은 같은 인스턴스에 연결된 사용자 간 채팅으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-169">For simplicity, this sample is limited to chatting between users connected to the same instance.</span></span> <span data-ttu-id="5810d-170">즉 클라우드 서비스에서 작업자 역할 인스턴스를 두 개 만드는 경우 사용자는 같은 작업자 역할 인스턴스에 연결된 사람들과만 채팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-170">This means that if the cloud service creates two worker role instances, users will only be able to chat with others connected to the same worker role instance.</span></span> <span data-ttu-id="5810d-171">응용 프로그램을 여러 역할 인스턴스와 작업하도록 조정하려면 서비스 버스 같은 기술을 사용하여 인스턴스 간에 Socket.IO 저장소 상태를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-171">To scale the application to work with multiple role instances, you could use a technology like Service Bus to share the Socket.IO store state across instances.</span></span> <span data-ttu-id="5810d-172">예를 들어, [Node.js에 대한 Azure SDK GitHub 리포지토리](https://github.com/WindowsAzure/azure-sdk-for-node)(영문)의 서비스 버스 큐 및 토픽 사용 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5810d-172">For examples, see the Service Bus Queues and Topics usage samples in the [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5810d-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5810d-173">Next steps</span></span>
<span data-ttu-id="5810d-174">이 자습서에서는 Azure 클라우드 서비스에 호스팅된 기본 채팅 응용 프로그램을 만드는 방법을 학습했습니다.</span><span class="sxs-lookup"><span data-stu-id="5810d-174">In this tutorial you learned how to create a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="5810d-175">이 응용 프로그램을 Azure 웹 사이트에 호스트하는 방법을 학습하려면 [Azure 웹 사이트에서 Socket.IO를 사용하여 Node.js 채팅 응용 프로그램 빌드][chatwebsite]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5810d-175">To learn how to host this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="5810d-176">자세한 내용은 [Node.js 개발자 센터](/develop/nodejs/)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5810d-176">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
<span data-ttu-id="5810d-177">[Socket.IO GitHub 리포지토리]: https://github.com/LearnBoost/socket.io/tree/0.9.14</span><span class="sxs-lookup"><span data-stu-id="5810d-177">[Socket.IO GitHub repository]: https://github.com/LearnBoost/socket.io/tree/0.9.14</span></span>
[Azure Considerations]: #windowsazureconsiderations
[Hosting the Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


