---
title: "aaaWeb 앱 빠른 (Node.js) | Microsoft Docs"
description: "자습서 hello 클라우드 서비스 자습서를 바탕으로 하며 toouse Express 모듈 hello 하는 방법을 보여 줍니다.입니다."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="77094-103">Azure 클라우드 서비스에서 Express를 사용하여 Node.js 웹 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="77094-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="77094-104">Node.js는 hello 핵심 런타임을에 최소한의 기능 모음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-104">Node.js includes a minimal set of functionality in hello core runtime.</span></span>
<span data-ttu-id="77094-105">Node.js 응용 프로그램을 개발할 때 개발자는 종종 3rd 파티 모듈 tooprovide 추가 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-105">Developers often use 3rd party modules tooprovide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="77094-106">이 자습서에서는 hello를 사용 하 여 새 응용 프로그램을 만듭니다 [Express] [ Express] Node.js 웹 응용 프로그램을 만들기 위한는 MVC 프레임 워크를 제공 하는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="77094-106">In this tutorial you will create a new application using hello [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="77094-107">완료 하는 hello 응용 프로그램의 스크린샷을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="77094-107">A screenshot of hello completed application is below:</span></span>

![Azure에서 시작 tooExpress를 표시 하는 웹 브라우저](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="77094-109">클라우드 서비스 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="77094-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="77094-110">Hello 다음이 수행 단계 toocreate 새 클라우드 서비스 프로젝트 라는 'expressapp':</span><span class="sxs-lookup"><span data-stu-id="77094-110">Perform hello following steps toocreate a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="77094-111">Hello에서 **시작 메뉴** 또는 **시작 화면**, 검색할 **Windows PowerShell**합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-111">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="77094-112">마지막으로, **Windows PowerShell**을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell 아이콘](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="77094-114">디렉터리 toohello 변경 **c:\\노드** 디렉터리 hello 명령을 toocreate 이라는 새 솔루션을 다음에 enter **expressapp** 이라는 웹 역할 및 **WebRole1** :</span><span class="sxs-lookup"><span data-stu-id="77094-114">Change directories toohello **c:\\node** directory and then enter hello following commands toocreate a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="77094-115">기본적으로 **Add-AzureNodeWebRole** 은 이전 버전의 Node.js를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="77094-116">hello **집합 AzureServiceProjectRole** 위의 문은 노드의 Azure toouse v0.10.21 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-116">hello **Set-AzureServiceProjectRole** statement above instructs Azure toouse v0.10.21 of Node.</span></span>  <span data-ttu-id="77094-117">참고 hello 매개 변수는 대/소문자 구분.</span><span class="sxs-lookup"><span data-stu-id="77094-117">Note hello parameters are case-sensitive.</span></span>  <span data-ttu-id="77094-118">Hello를 확인 하 여 hello 올바른 버전의 Node.js가 선택한 확인할 수 있습니다 **엔진** 속성 **WebRole1\package.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-118">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="77094-119">Express 설치</span><span class="sxs-lookup"><span data-stu-id="77094-119">Install Express</span></span>
1. <span data-ttu-id="77094-120">Hello 다음 명령을 실행 하 여 hello Express 생성기를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-120">Install hello Express generator by issuing hello following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="77094-121">hello npm 명령의 hello 출력 아래 비슷한 toohello 결과 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-121">hello output of hello npm command should look similar toohello result below.</span></span> 
   
    ![Windows PowerShell의 hello npm 표시 hello 출력 명령 express를 설치 합니다.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="77094-123">디렉터리 toohello 변경 **WebRole1** 디렉터리 및 사용 하 여 빠른 명령 toogenerate 새 응용 프로그램을 hello:</span><span class="sxs-lookup"><span data-stu-id="77094-123">Change directories toohello **WebRole1** directory and use hello express command toogenerate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="77094-124">하면 이전 응용 프로그램 증명된 toooverwrite 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77094-124">You will be prompted toooverwrite your earlier application.</span></span> <span data-ttu-id="77094-125">입력 **y** 또는 **예** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-125">Enter **y** or **yes** toocontinue.</span></span> <span data-ttu-id="77094-126">Express는 hello app.js 파일 및 응용 프로그램을 구축 하기 위한 폴더 구조를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-126">Express will generate hello app.js file and a folder structure for building your application.</span></span>
   
    ![hello express 명령의 hello 출력](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="77094-128">tooinstall 추가 종속성 hello package.json 파일에 정의 된 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-128">tooinstall additional dependencies defined in hello package.json file, enter hello following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![hello 출력의 hello npm 설치 명령](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="77094-130">사용 하 여 hello 다음 명령은 toocopy hello **bin/w w w** 파일 너무**server.js**합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-130">Use hello following command toocopy hello **bin/www** file too**server.js**.</span></span> <span data-ttu-id="77094-131">이 hello 클라우드 서비스는이 응용 프로그램에 대 한 hello 진입점을 찾을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-131">This is so hello cloud service can find hello entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="77094-132">이 명령이 완료 된 후 해야는 **server.js** hello WebRole1 디렉터리의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="77094-132">After this command completes, you should have a **server.js** file in hello WebRole1 directory.</span></span>
5. <span data-ttu-id="77094-133">Hello 수정 **server.js** hello 중 tooremove '.' hello 다음 줄의에서 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="77094-133">Modify hello **server.js** tooremove one of hello '.' characters from hello following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="77094-134">이 수정 후 hello 줄 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77094-134">After making this modification, hello line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="77094-135">이 변경은 hello 파일 이동 후에 필요 (이전의 **bin/w w w**,) toohello 필수 hello 응용 프로그램 파일과 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="77094-135">This change is required since we moved hello file (formerly **bin/www**,) toohello same directory as hello app file being required.</span></span> <span data-ttu-id="77094-136">이 변경 후 hello 저장 **server.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="77094-136">After making this change, save hello **server.js** file.</span></span>
6. <span data-ttu-id="77094-137">사용 하 여 hello 다음 명령 hello Azure 에뮬레이터에서에서 toorun hello 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77094-137">Use hello following command toorun hello application in hello Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![시작 tooexpress를 포함 하는 웹 페이지입니다.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a><span data-ttu-id="77094-139">Hello 보기 수정</span><span class="sxs-lookup"><span data-stu-id="77094-139">Modifying hello View</span></span>
<span data-ttu-id="77094-140">이제 hello toodisplay hello 메시지 보기 "Azure에서 시작 tooExpress"를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-140">Now modify hello view toodisplay hello message "Welcome tooExpress in Azure".</span></span>

1. <span data-ttu-id="77094-141">다음 명령은 tooopen hello index.jade 파일 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-141">Enter hello following command tooopen hello index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![hello index.jade 파일의 hello 내용입니다.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="77094-143">Jade는 Express 응용 프로그램에서 사용 하는 hello 기본 뷰 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="77094-143">Jade is hello default view engine used by Express applications.</span></span> <span data-ttu-id="77094-144">Hello Jade 뷰 엔진에 대 한 자세한 내용은 참조 하십시오. [http://jade-lang.com][http://jade-lang.com]합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-144">For more information on hello Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="77094-145">Hello 텍스트의 마지막 줄을 추가 하 여 수정 **Azure에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-145">Modify hello last line of text by appending **in Azure**.</span></span>
   
   ![hello index.jade 파일 hello 마지막 줄 읽어: p 너무 시작\#Azure에서 {제목}](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="77094-147">Hello 파일을 저장 하 고 메모장을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-147">Save hello file and exit Notepad.</span></span>
4. <span data-ttu-id="77094-148">브라우저를 새로 고치면 변경 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77094-148">Refresh your browser and you will see your changes.</span></span>
   
   ![브라우저 창을 hello 페이지에 Azure에서 시작 tooExpress](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="77094-150">Hello 응용 프로그램을 테스트 후 hello를 사용 하 여 **중지 AzureEmulator** cmdlet toostop hello 에뮬레이터입니다.</span><span class="sxs-lookup"><span data-stu-id="77094-150">After testing hello application, use hello **Stop-AzureEmulator** cmdlet toostop hello emulator.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="77094-151">게시 hello 응용 프로그램 tooAzure</span><span class="sxs-lookup"><span data-stu-id="77094-151">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="77094-152">Hello Azure PowerShell 창에서 hello를 사용 하 여 **게시 AzureServiceProject** cmdlet toodeploy hello 응용 프로그램 tooa 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="77094-152">In hello Azure PowerShell window, use hello **Publish-AzureServiceProject** cmdlet toodeploy hello application tooa cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="77094-153">Hello 배포 작업이 완료 되 면 브라우저가 열리고 hello 웹 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-153">Once hello deployment operation completes, your browser will open and display hello web page.</span></span>

![웹 브라우저 hello Express 페이지를 표시 합니다.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="77094-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77094-156">Next steps</span></span>
<span data-ttu-id="77094-157">자세한 내용은 참조 hello [Node.js 개발자 센터](/develop/nodejs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="77094-157">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


