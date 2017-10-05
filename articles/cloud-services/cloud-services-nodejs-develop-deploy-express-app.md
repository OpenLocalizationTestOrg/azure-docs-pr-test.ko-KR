---
title: "Express를 사용하여 웹앱 빌드(Node.js) | Microsoft Docs"
description: "클라우드 서비스 자습서를 기반으로 웹앱을 빌드하고 Express 모듈 사용 방법을 보여 주는 자습서입니다."
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
ms.openlocfilehash: 54b715695e24786ec4e8dfcabefc648d76179c8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="0b68f-103">Azure 클라우드 서비스에서 Express를 사용하여 Node.js 웹 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="0b68f-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="0b68f-104">Node.js에는 핵심 런타임에 최소한의 기능이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-104">Node.js includes a minimal set of functionality in the core runtime.</span></span>
<span data-ttu-id="0b68f-105">개발자는 Node.js 응용 프로그램을 개발할 때 추가 기능을 제공하기 위해 종종 타사 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-105">Developers often use 3rd party modules to provide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="0b68f-106">이 자습서에서는 Node.js 웹 응용 프로그램을 만들기 위한 MVC 프레임워크를 제공하는 [Express][Express] 모듈을 사용하여 새 응용 프로그램을 만들어봅니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-106">In this tutorial you will create a new application using the [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="0b68f-107">아래에는 완성된 응용 프로그램의 스크린샷이 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-107">A screenshot of the completed application is below:</span></span>

![Welcome to Express in Azure를 표시하는 웹 브라우저](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="0b68f-109">클라우드 서비스 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="0b68f-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="0b68f-110">다음 단계에 따라 'expressapp'라는 이름의 새 클라우드 서비스 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-110">Perform the following steps to create a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="0b68f-111">**시작 메뉴** 또는 **시작 화면**에서 **Windows PowerShell**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-111">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="0b68f-112">마지막으로, **Windows PowerShell**을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell 아이콘](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="0b68f-114">디렉터리를 **c:\\node** 디렉터리로 변경한 후 다음 명령을 입력하여 **expressapp**라는 이름의 새 솔루션과 **WebRole1**이라는 웹 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-114">Change directories to the **c:\\node** directory and then enter the following commands to create a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="0b68f-115">기본적으로 **Add-AzureNodeWebRole** 은 이전 버전의 Node.js를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="0b68f-116">위의 **Set-AzureServiceProjectRole** 문은 Azure에 Node의 v0.10.21을 사용하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-116">The **Set-AzureServiceProjectRole** statement above instructs Azure to use v0.10.21 of Node.</span></span>  <span data-ttu-id="0b68f-117">매개 변수는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-117">Note the parameters are case-sensitive.</span></span>  <span data-ttu-id="0b68f-118">**WebRole1\package.json**의 **engines** 속성을 확인하여 올바른 버전의 Node.js가 선택되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-118">You can verify the correct version of Node.js has been selected by checking the **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="0b68f-119">Express 설치</span><span class="sxs-lookup"><span data-stu-id="0b68f-119">Install Express</span></span>
1. <span data-ttu-id="0b68f-120">다음 명령을 실행하여 Express 생성기를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-120">Install the Express generator by issuing the following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="0b68f-121">npm 명령의 출력이 아래 결과와 비슷하게 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-121">The output of the npm command should look similar to the result below.</span></span> 
   
    ![express 설치 npm 명령의 출력을 표시하는 Windows PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="0b68f-123">디렉터리를 **WebRole1** 디렉터리로 변경하고 express 명령을 사용하여 새 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-123">Change directories to the **WebRole1** directory and use the express command to generate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="0b68f-124">이전 응용 프로그램을 덮어쓸지 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-124">You will be prompted to overwrite your earlier application.</span></span> <span data-ttu-id="0b68f-125">**y** 또는 **예**를 입력하고 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-125">Enter **y** or **yes** to continue.</span></span> <span data-ttu-id="0b68f-126">Express에서 응용 프로그램 빌드를 위해 app.js 파일과 폴더 구조를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-126">Express will generate the app.js file and a folder structure for building your application.</span></span>
   
    ![express 명령의 출력](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="0b68f-128">package.json 파일에 정의된 추가 종속성을 설치하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-128">To install additional dependencies defined in the package.json file, enter the following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![npm 설치 명령의 출력](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="0b68f-130">다음 명령을 사용하여 **bin/www** 파일을 **server.js**에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-130">Use the following command to copy the **bin/www** file to **server.js**.</span></span> <span data-ttu-id="0b68f-131">이는 클라우드 서비스에서 이 응용 프로그램의 진입점을 찾을 수 있도록 하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-131">This is so the cloud service can find the entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="0b68f-132">이 명령을 완료하면 WebRole1 디렉터리에 **server.js** 파일에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-132">After this command completes, you should have a **server.js** file in the WebRole1 directory.</span></span>
5. <span data-ttu-id="0b68f-133">**server.js** 를 수정하여 다음 줄에서 '.' 문자 중 하나를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-133">Modify the **server.js** to remove one of the '.' characters from the following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="0b68f-134">수정을 완료하면 줄이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-134">After making this modification, the line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="0b68f-135">이 변경 작업은 필요한 앱 파일과 동일한 디렉터리로 파일(이전의 **bin/www**)을 이동했기 때문에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-135">This change is required since we moved the file (formerly **bin/www**,) to the same directory as the app file being required.</span></span> <span data-ttu-id="0b68f-136">이렇게 변경한 후 **server.js** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-136">After making this change, save the **server.js** file.</span></span>
6. <span data-ttu-id="0b68f-137">다음 명령을 사용하여 Azure 에뮬레이터에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-137">Use the following command to run the application in the Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![welcome to express가 들어 있는 웹 페이지](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-the-view"></a><span data-ttu-id="0b68f-139">뷰 수정</span><span class="sxs-lookup"><span data-stu-id="0b68f-139">Modifying the View</span></span>
<span data-ttu-id="0b68f-140">이제 "Welcome to Express in Azure" 메시지를 표시하는 뷰를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-140">Now modify the view to display the message "Welcome to Express in Azure".</span></span>

1. <span data-ttu-id="0b68f-141">다음 명령을 입력하여 index.jade 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-141">Enter the following command to open the index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![index.jade 파일의 내용](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="0b68f-143">Jade는 Express 응용 프로그램에서 사용하는 기본 뷰 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-143">Jade is the default view engine used by Express applications.</span></span> <span data-ttu-id="0b68f-144">Jade 뷰 엔진에 대한 자세한 내용은 [http://jade-lang.com][http://jade-lang.com](영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b68f-144">For more information on the Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="0b68f-145">**in Azure**를 추가하여 텍스트의 마지막 줄을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-145">Modify the last line of text by appending **in Azure**.</span></span>
   
   ![index.jade 파일, 마지막 줄: p Welcome to \#{title} in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="0b68f-147">파일을 저장하고 메모장을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-147">Save the file and exit Notepad.</span></span>
4. <span data-ttu-id="0b68f-148">브라우저를 새로 고치면 변경 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-148">Refresh your browser and you will see your changes.</span></span>
   
   ![브라우저 창, Welcome to Express in Azure가 들어 있는 페이지](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="0b68f-150">응용 프로그램을 테스트한 후 **Stop-AzureEmulator** cmdlet을 사용하여 에뮬레이터를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-150">After testing the application, use the **Stop-AzureEmulator** cmdlet to stop the emulator.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="0b68f-151">Azure에 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="0b68f-151">Publishing the Application to Azure</span></span>
<span data-ttu-id="0b68f-152">Azure PowerShell 창에서 **Publish-AzureServiceProject** cmdlet을 사용하여 응용 프로그램을 클라우드 서비스에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-152">In the Azure PowerShell window, use the **Publish-AzureServiceProject** cmdlet to deploy the application to a cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="0b68f-153">배포 작업을 완료하면 브라우저가 열리고 웹 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b68f-153">Once the deployment operation completes, your browser will open and display the web page.</span></span>

![Express 페이지를 표시하는 웹 브라우저입니다.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="0b68f-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b68f-156">Next steps</span></span>
<span data-ttu-id="0b68f-157">자세한 내용은 [Node.js 개발자 센터](/develop/nodejs/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b68f-157">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


