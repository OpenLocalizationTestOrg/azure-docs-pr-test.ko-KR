---
title: "aaaNode.js 시작 가이드 | Microsoft Docs"
description: "Toocreate 간단한 Node.js 웹 응용 프로그램 및 tooan Azure 클라우드 서비스 배포 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a><span data-ttu-id="ed41a-103">빌드 및 배포는 Node.js 응용 프로그램 tooan Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="ed41a-103">Build and deploy a Node.js application tooan Azure Cloud Service</span></span>

<span data-ttu-id="ed41a-104">이 자습서에서는 어떻게 toocreate 간단한 Node.js 응용 프로그램에서 Azure 클라우드 서비스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-104">This tutorial shows how toocreate a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="ed41a-105">클라우드 서비스는 Azure에서 확장 가능한 클라우드 응용 프로그램의 hello 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-105">Cloud Services are hello building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="ed41a-106">Hello 분리 하 고 독립적인 관리 및 응용 프로그램의 프런트 엔드 및 백 엔드 구성 요소 확장을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-106">They allow hello separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="ed41a-107">클라우드 서비스는 각 역할을 안정적으로 호스팅할 수 있는 강력한 전용 가상 컴퓨터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="ed41a-108">클라우드 서비스와 어떻게 다른 지 tooAzure 웹 사이트 및 가상 컴퓨터에 대 한 자세한 내용은 참조 하십시오. [Azure 웹 사이트, 클라우드 서비스 및 가상 컴퓨터 비교]합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-108">For more information on Cloud Services, and how they compare tooAzure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="ed41a-109">Toobuild 간단한 웹 사이트를 찾고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ed41a-109">Looking toobuild a simple website?</span></span> <span data-ttu-id="ed41a-110">시나리오에 간단한 웹 사이트 프런트 엔드만 포함된 경우 [간단한 웹앱 사용]을 고려해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="ed41a-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="ed41a-111">웹 응용 프로그램 증가 및 요구 사항 변경 tooa 클라우드 서비스를 쉽게 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-111">You can easily upgrade tooa Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="ed41a-112">이 자습서를 수행하여 웹 역할 내에서 호스트되는 간단한 웹 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="ed41a-113">사용 하는 hello 계산 에뮬레이터 tootest 응용 프로그램을 로컬로 합니다 PowerShell 명령줄 도구를 사용 하 여 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-113">You will use hello compute emulator tootest your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="ed41a-114">hello 응용 프로그램은 간단한 "hello world" 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="ed41a-114">hello application is a simple "hello world" application:</span></span>

![Hello World Hello 웹 페이지를 표시 하는 웹 브라우저][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="ed41a-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ed41a-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="ed41a-117">이 자습서는 Azure PowerShell을 사용하며,</span><span class="sxs-lookup"><span data-stu-id="ed41a-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="ed41a-118">[Azure PowerShell]을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="ed41a-119">다운로드 및 설치 hello [Azure SDK for.NET 2.7]합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-119">Download and install hello [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="ed41a-120">Hello에서 설치 프로그램을 설치, 선택:</span><span class="sxs-lookup"><span data-stu-id="ed41a-120">In hello install setup, select:</span></span>
  * <span data-ttu-id="ed41a-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="ed41a-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="ed41a-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="ed41a-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="ed41a-123">Azure 클라우드 서비스 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="ed41a-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="ed41a-124">Hello 작업 toocreate 기본 Node.js 스 캐 폴딩 함께 새 Azure 클라우드 서비스 프로젝트를 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-124">Perform hello following tasks toocreate a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="ed41a-125">실행 **Windows PowerShell** 관리자 권한으로; hello **시작 메뉴** 또는 **시작 화면**, 검색할 **Windows PowerShell**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-125">Run **Windows PowerShell** as Administrator; from hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="ed41a-126">[PowerShell 연결] tooyour 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-126">[Connect PowerShell] tooyour subscription.</span></span>
3. <span data-ttu-id="ed41a-127">다음 PowerShell cmdlet toocreate toocreate hello 프로젝트 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-127">Enter hello following PowerShell cmdlet toocreate toocreate hello project:</span></span>

        New-AzureServiceProject helloworld

    ![hello New-azureservice helloworld 명령의 hello 결과][hello result of hello New-AzureService helloworld command]

    <span data-ttu-id="ed41a-129">hello **새로 AzureServiceProject** cmdlet은 Node.js 응용 프로그램 tooa 클라우드 서비스를 게시 하기 위한 기본 구조를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-129">hello **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application tooa Cloud Service.</span></span> <span data-ttu-id="ed41a-130">여기에 게시 tooAzure에 필요한 구성 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-130">It contains configuration files necessary for publishing tooAzure.</span></span> <span data-ttu-id="ed41a-131">hello cmdlet도 hello 서비스에 대 한 작업 디렉터리 toohello 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-131">hello cmdlet also changes your working directory toohello directory for hello service.</span></span>

    <span data-ttu-id="ed41a-132">hello cmdlet에는 다음 파일이 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-132">hello cmdlet creates hello following files:</span></span>

   * <span data-ttu-id="ed41a-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** 및 **ServiceDefinition.csdef**는 응용 프로그램을 게시하는 데 필요한 Azure 관련 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="ed41a-134">자세한 내용은 [Azure에 대한 호스티드 서비스 만들기 개요](영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed41a-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="ed41a-135">**deploymentSettings.json**: hello Azure PowerShell 배포 cmdlet에서 사용 되는 로컬 설정을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-135">**deploymentSettings.json**: Stores local settings that are used by hello Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="ed41a-136">Hello 명령 tooadd 새 웹 역할 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-136">Enter hello following command tooadd a new web role:</span></span>

       Add-AzureNodeWebRole

   ![hello 추가 AzureNodeWebRole 명령의 hello 출력][hello output of hello Add-AzureNodeWebRole command]

   <span data-ttu-id="ed41a-138">hello **추가 AzureNodeWebRole** cmdlet은 기본 Node.js 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-138">hello **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="ed41a-139">또한 hello 수정 **.csfg** 및 **.csdef** hello 새 역할에 대 한 구성 항목 tooadd 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-139">It also modifies hello **.csfg** and **.csdef** files tooadd configuration entries for hello new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ed41a-140">역할 이름을 지정하지 않으면 기본 이름이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="ed41a-141">Hello 첫 번째 cmdlet 매개 변수로 이름을 제공할 수 있습니다.`Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="ed41a-141">You can provide a name as hello first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="ed41a-142">hello 파일에 정의 된 hello Node.js 앱 **server.js**hello 웹 역할에 대 한 hello 디렉터리에 있는 (**WebRole1** 기본적으로).</span><span class="sxs-lookup"><span data-stu-id="ed41a-142">hello Node.js app is defined in hello file **server.js**, located in hello directory for hello web role (**WebRole1** by default).</span></span> <span data-ttu-id="ed41a-143">Hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-143">Here is hello code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="ed41a-144">이 코드는 "Hello World" hello와 동일 hello에 예제 hello 기본적으로 [nodejs.org] hello 클라우드 환경에 의해 할당 된 hello 포트 번호를 사용 하 여 제외 하 고 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-144">This code is essentially hello same as hello "Hello World" sample on hello [nodejs.org] website, except it uses hello port number assigned by hello cloud environment.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="ed41a-145">Hello 응용 프로그램 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="ed41a-145">Deploy hello application tooAzure</span></span>

> [!NOTE]
> <span data-ttu-id="ed41a-146">toocomplete이이 자습서에서는 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-146">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="ed41a-147">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF)하거나 [무료 계정을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-hello-azure-publishing-settings"></a><span data-ttu-id="ed41a-148">Hello Azure 다운로드 게시 설정</span><span class="sxs-lookup"><span data-stu-id="ed41a-148">Download hello Azure publishing settings</span></span>
<span data-ttu-id="ed41a-149">toodeploy 프로그램 응용 프로그램 tooAzure 하면 Azure 구독에 대 한 설정을 게시 하는 hello 먼저 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-149">toodeploy your application tooAzure, you must first download hello publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="ed41a-150">Hello 다음 Azure PowerShell cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-150">Run hello following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="ed41a-151">브라우저를 사용 하는이 toonavigate toohello 설정 다운로드 페이지를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-151">This will use your browser toonavigate toohello publish settings download page.</span></span> <span data-ttu-id="ed41a-152">Microsoft 계정으로 증명된 toolog 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-152">You may be prompted toolog in with a Microsoft Account.</span></span> <span data-ttu-id="ed41a-153">이 경우에 Azure 구독에 연결 된 hello 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-153">If so, use hello account associated with your Azure subscription.</span></span>

   <span data-ttu-id="ed41a-154">다운로드 한 hello 프로필 tooa 파일 위치에 쉽게 액세스할 수를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-154">Save hello downloaded profile tooa file location you can easily access.</span></span>
2. <span data-ttu-id="ed41a-155">Cmdlet tooimport hello 게시 프로필 다운로드 한 다음 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-155">Run following cmdlet tooimport hello publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > <span data-ttu-id="ed41a-156">Hello를 가져온 다음 게시 설정, 누군가가 문제가 발생할 수 있는 정보가 포함 되어 있어.publishSettings 파일을 다운로드 한 hello 삭제를 고려해 tooaccess 계정.</span><span class="sxs-lookup"><span data-stu-id="ed41a-156">After importing hello publish settings, consider deleting hello downloaded .publishSettings file, because it contains information that could allow someone tooaccess your account.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="ed41a-157">Hello 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="ed41a-157">Publish hello application</span></span>
<span data-ttu-id="ed41a-158">toopublish hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-158">toopublish, run hello following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="ed41a-159">**-ServiceName** hello 배포에 대 한 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-159">**-ServiceName** specifies hello name for hello deployment.</span></span> <span data-ttu-id="ed41a-160">고유 이름 이어야 합니다, 그렇지 않으면 hello 게시 프로세스가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-160">This must be a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="ed41a-161">hello **Get-date** hello 이름이 고유 해야 하는 날짜/시간 문자열에 tacks 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-161">hello **Get-Date** command tacks on a date/time string that should make hello name unique.</span></span>
* <span data-ttu-id="ed41a-162">**-위치** hello 응용 프로그램에서 호스팅하는 hello 데이터 센터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-162">**-Location** specifies hello datacenter that hello application will be hosted in.</span></span> <span data-ttu-id="ed41a-163">사용 가능한 데이터 센터를 사용 하 여 hello 목록이 toosee **Get AzureLocation** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ed41a-163">toosee a list of available datacenters, use hello **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="ed41a-164">**-시작** 배포 완료 된 후 toohello 호스팅된 서비스를 이동 하는 브라우저 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-164">**-Launch** opens a browser window and navigates toohello hosted service after deployment has completed.</span></span>

<span data-ttu-id="ed41a-165">게시에 성공 하면 응답 비슷한 toohello 다음을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-165">After publishing succeeds, you will see a response similar toohello following:</span></span>

![hello Publish-azureservice 명령의 hello 출력][hello output of hello Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="ed41a-167">응용 프로그램 toodeploy hello에 대 일 분 정도 걸릴 하 고 처음 게시할 때 사용할 수 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-167">It can take several minutes for hello application toodeploy and become available when first published.</span></span>

<span data-ttu-id="ed41a-168">Hello 배포 완료 되 면 브라우저 창을 열고 toohello 클라우드 서비스를 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-168">Once hello deployment has completed, a browser window will open and navigate toohello cloud service.</span></span>

![Hello hello world 페이지를 표시 하는 브라우저 창 hello URL hello 페이지는 Azure에서 호스트 되는 것을 나타냅니다.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

<span data-ttu-id="ed41a-170">이제 응용 프로그램이 Azure에서 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="ed41a-171">hello **게시 AzureServiceProject** cmdlet hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-171">hello **Publish-AzureServiceProject** cmdlet performs hello following steps:</span></span>

1. <span data-ttu-id="ed41a-172">패키지 toodeploy를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-172">Creates a package toodeploy.</span></span> <span data-ttu-id="ed41a-173">hello 패키지 응용 프로그램 폴더에 모든 hello 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-173">hello package contains all hello files in your application folder.</span></span>
2. <span data-ttu-id="ed41a-174">**저장소 계정** 이 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="ed41a-175">hello Azure 저장소 계정에는 배포 하는 동안 사용 되는 toostore hello 응용 프로그램 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-175">hello Azure storage account is used toostore hello application package during deployment.</span></span> <span data-ttu-id="ed41a-176">배포를 완료 한 후에 안전 하 게 hello 저장소 계정을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-176">You can safely delete hello storage account after deployment is done.</span></span>
3. <span data-ttu-id="ed41a-177">**클라우드 서비스** 가 아직 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="ed41a-178">A **클라우드 서비스** 는 배포 된 tooAzure 되었을 때 응용 프로그램 호스팅 hello 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-178">A **cloud service** is hello container in which your application is hosted when it is deployed tooAzure.</span></span> <span data-ttu-id="ed41a-179">자세한 내용은 [Azure에 대한 호스티드 서비스 만들기 개요](영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed41a-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="ed41a-180">배포 패키지 tooAzure hello를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-180">Publishes hello deployment package tooAzure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="ed41a-181">응용 프로그램 중지 및 삭제</span><span class="sxs-lookup"><span data-stu-id="ed41a-181">Stopping and deleting your application</span></span>
<span data-ttu-id="ed41a-182">응용 프로그램을 배포한 후 toodisable 경우가 되므로 추가 비용을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-182">After deploying your application, you may want toodisable it so you can avoid extra costs.</span></span> <span data-ttu-id="ed41a-183">Azure는 사용된 서버 시간의 시간당 웹 역할 인스턴스 요금을 청구합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="ed41a-184">서버 시간 hello 인스턴스를 실행 하지 않는 및 hello 중지 상태인 경우에 응용 프로그램을 배포한 후에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-184">Server time is consumed once your application is deployed, even if hello instances are not running and are in hello stopped state.</span></span>

1. <span data-ttu-id="ed41a-185">Hello Windows PowerShell 창에서 cmdlet 뒤 hello를 사용 하 여 hello 이전 섹션에서 만든 hello 서비스 배포를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-185">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="ed41a-186">Hello 서비스를 중지 하면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-186">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="ed41a-187">Hello 서비스가 중지 되 면이 중지 되었음을 나타내는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-187">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![hello 중지 AzureService 명령 hello 상태][hello status of hello Stop-AzureService command]
2. <span data-ttu-id="ed41a-189">cmdlet을 다음 호출 hello toodelete hello 서비스:</span><span class="sxs-lookup"><span data-stu-id="ed41a-189">toodelete hello service, call hello following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="ed41a-190">메시지가 표시 되 면 입력 **Y** toodelete hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-190">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="ed41a-191">Hello 서비스를 삭제 하면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-191">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="ed41a-192">Hello 서비스를 삭제 한 후에 hello 서비스가 삭제 되었거나를 나타내는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-192">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

   ![hello 제거 AzureService 명령 hello 상태][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="ed41a-194">Hello 서비스를 삭제 hello 서비스, 초기에 게시 하는 경우 만든 hello 저장소 계정을 삭제 되지 않으며 사용 되는 저장소에 대 한 청구 toobe 계속 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-194">Deleting hello service does not delete hello storage account that was created when hello service was initially published, and you will continue toobe billed for storage used.</span></span> <span data-ttu-id="ed41a-195">Toodelete hello 저장소를 사용 하는 다른 경우 않을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-195">If nothing else is using hello storage, you may want toodelete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed41a-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed41a-196">Next steps</span></span>
<span data-ttu-id="ed41a-197">자세한 내용은 참조 hello [Node.js 개발자 센터]합니다.</span><span class="sxs-lookup"><span data-stu-id="ed41a-197">For more information, see hello [Node.js Developer Center].</span></span>

<!-- URL List -->

[Azure 웹 사이트, 클라우드 서비스 및 가상 컴퓨터 비교]: ../app-service-web/choose-web-site-cloud-service-vm.md
[간단한 웹앱 사용]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK for.NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[PowerShell 연결]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Azure에 대한 호스티드 서비스 만들기 개요]: https://azure.microsoft.com/documentation/services/cloud-services/
[Node.js 개발자 센터]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
