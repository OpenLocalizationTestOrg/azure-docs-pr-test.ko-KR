---
title: "Node.js 시작 가이드 | Microsoft 문서"
description: "간단한 Node.js 웹 응용 프로그램을 만들고 Azure 클라우드 서비스에 배포하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 980643f35c78bbae7b1b12336331ca15ad4fb89b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="build-and-deploy-a-nodejs-application-to-an-azure-cloud-service"></a><span data-ttu-id="33df3-103">Azure 클라우드 서비스에서 Node.js 응용 프로그램 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="33df3-103">Build and deploy a Node.js application to an Azure Cloud Service</span></span>

<span data-ttu-id="33df3-104">이 자습서에서는 Azure 클라우드 서비스에서 실행되는 간단한 Node.js 응용 프로그램을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-104">This tutorial shows how to create a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="33df3-105">클라우드 서비스는 Azure에서 확장 가능한 클라우드 응용 프로그램의 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-105">Cloud Services are the building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="33df3-106">이 클라우드 서비스는 응용 프로그램의 프런트 엔드 및 백 엔드 구성 요소의 구분과 독립적인 관리 및 확장을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-106">They allow the separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="33df3-107">클라우드 서비스는 각 역할을 안정적으로 호스팅할 수 있는 강력한 전용 가상 컴퓨터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="33df3-108">클라우드 서비스에 대한 자세한 내용 및 Azure 웹 사이트와 가상 컴퓨터와의 비교에 대한 자세한 내용은 [Azure 웹 사이트, 클라우드 서비스 및 가상 컴퓨터 비교]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33df3-108">For more information on Cloud Services, and how they compare to Azure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="33df3-109">간단한 웹 사이트를 빌드하려는 경우</span><span class="sxs-lookup"><span data-stu-id="33df3-109">Looking to build a simple website?</span></span> <span data-ttu-id="33df3-110">시나리오에 간단한 웹 사이트 프런트 엔드만 포함된 경우 [간단한 웹앱 사용]을 고려해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="33df3-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="33df3-111">그러면 웹앱이 커지고 요구 사항이 변경될 때 클라우드 서비스로 쉽게 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-111">You can easily upgrade to a Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="33df3-112">이 자습서를 수행하여 웹 역할 내에서 호스트되는 간단한 웹 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="33df3-113">계산 에뮬레이터를 사용하여 로컬에서 응용 프로그램을 테스트한 다음 PowerShell 명령줄 도구를 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-113">You will use the compute emulator to test your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="33df3-114">응용 프로그램은 간단한 "hello world" 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-114">The application is a simple "hello world" application:</span></span>

![Hello World 웹 페이지를 표시하는 웹 브라우저][A web browser displaying the Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="33df3-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="33df3-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="33df3-117">이 자습서는 Azure PowerShell을 사용하며,</span><span class="sxs-lookup"><span data-stu-id="33df3-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="33df3-118">[Azure PowerShell]을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="33df3-119">[Azure SDK for .NET 2.7]을 다운로드 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-119">Download and install the [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="33df3-120">설치 설정에서 다음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-120">In the install setup, select:</span></span>
  * <span data-ttu-id="33df3-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="33df3-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="33df3-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="33df3-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="33df3-123">Azure 클라우드 서비스 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="33df3-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="33df3-124">기본 Node.js 스캐폴딩과 함께 새 Azure 클라우드 서비스 프로젝트를 만들려면 다음 작업을 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="33df3-124">Perform the following tasks to create a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="33df3-125">**시작 메뉴** 또는 **시작 화면**에서 관리자 권한으로 **Windows PowerShell**을 실행하고 **Windows PowerShell**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-125">Run **Windows PowerShell** as Administrator; from the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="33df3-126">[PowerShell을 연결] 합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-126">[Connect PowerShell] to your subscription.</span></span>
3. <span data-ttu-id="33df3-127">프로젝트를 만들려면 다음 PowerShell cmdlet을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-127">Enter the following PowerShell cmdlet to create to create the project:</span></span>

        New-AzureServiceProject helloworld

    ![New-AzureService helloworld 명령의 결과][The result of the New-AzureService helloworld command]

    <span data-ttu-id="33df3-129">**New-AzureServiceProject** cmdlet은 클라우드 서비스에 Node.js 응용 프로그램을 게시하기 위한 기본 구조를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-129">The **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application to a Cloud Service.</span></span> <span data-ttu-id="33df3-130">여기에는 Azure에 게시하는 데 필요한 구성 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-130">It contains configuration files necessary for publishing to Azure.</span></span> <span data-ttu-id="33df3-131">또한 이 cmdlet은 작업 디렉터리를 서비스에 대한 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-131">The cmdlet also changes your working directory to the directory for the service.</span></span>

    <span data-ttu-id="33df3-132">Cmdlet은 다음 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-132">The cmdlet creates the following files:</span></span>

   * <span data-ttu-id="33df3-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** 및 **ServiceDefinition.csdef**는 응용 프로그램을 게시하는 데 필요한 Azure 관련 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="33df3-134">자세한 내용은 [Azure에 대한 호스티드 서비스 만들기 개요](영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33df3-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="33df3-135">**deploymentSettings.json**: Azure PowerShell 배포 cmdlet에 사용되는 로컬 설정이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-135">**deploymentSettings.json**: Stores local settings that are used by the Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="33df3-136">다음 명령을 사용하여 새 웹 역할을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="33df3-136">Enter the following command to add a new web role:</span></span>

       Add-AzureNodeWebRole

   ![Add-AzureNodeWebRole 명령의 출력][The output of the Add-AzureNodeWebRole command]

   <span data-ttu-id="33df3-138">**Add-AzureNodeWebRole** cmdlet는 기본 Node.js 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-138">The **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="33df3-139">또한 **.csfg** 및 **.csdef** 파일을 수정하여 새 역할에 대한 구성 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-139">It also modifies the **.csfg** and **.csdef** files to add configuration entries for the new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="33df3-140">역할 이름을 지정하지 않으면 기본 이름이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="33df3-141">첫번째 cmdlet 매개변수로 이름을 제공할 수 있습니다. `Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="33df3-141">You can provide a name as the first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="33df3-142">Node.js 앱은 웹 역할에 대한 디렉터리에 있는 **server.js** 파일에 정의됩니다(기본값은 **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="33df3-142">The Node.js app is defined in the file **server.js**, located in the directory for the web role (**WebRole1** by default).</span></span> <span data-ttu-id="33df3-143">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-143">Here is the code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="33df3-144">이 코드는 클라우드 환경에서 지정된 포트 번호를 사용한다는 점을 제외하고 기본적으로 [nodejs.org] 웹사이트의 "Hello World" 예제와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-144">This code is essentially the same as the "Hello World" sample on the [nodejs.org] website, except it uses the port number assigned by the cloud environment.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="33df3-145">Azure에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="33df3-145">Deploy the application to Azure</span></span>

> [!NOTE]
> <span data-ttu-id="33df3-146">이 자습서를 완료하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-146">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="33df3-147">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF)하거나 [무료 계정을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-the-azure-publishing-settings"></a><span data-ttu-id="33df3-148">Azure 게시 설정 다운로드</span><span class="sxs-lookup"><span data-stu-id="33df3-148">Download the Azure publishing settings</span></span>
<span data-ttu-id="33df3-149">응용 프로그램을 Azure에 배포하려면 먼저 Azure 구독에 대한 게시 설정을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-149">To deploy your application to Azure, you must first download the publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="33df3-150">다음 Azure PowerShell cmdlet를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-150">Run the following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="33df3-151">그러면 브라우저를 사용하여 게시 설정 다운로드 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-151">This will use your browser to navigate to the publish settings download page.</span></span> <span data-ttu-id="33df3-152">Microsoft 계정으로 로그인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-152">You may be prompted to log in with a Microsoft Account.</span></span> <span data-ttu-id="33df3-153">그럴 경우 Azure 구독과 연결된 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-153">If so, use the account associated with your Azure subscription.</span></span>

   <span data-ttu-id="33df3-154">다운로드한 프로필을 쉽게 액세스할 수 있는 파일 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-154">Save the downloaded profile to a file location you can easily access.</span></span>
2. <span data-ttu-id="33df3-155">다음 Cmdlet를 실행하여 다운로드한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-155">Run following cmdlet to import the publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path to file]

    > [!NOTE]
    > <span data-ttu-id="33df3-156">게시 설정을 가져온 후, 다른 사용자가 계정에 액세스할 수 있는 정보가 포함되어 있으므로 다운로드한 .publishSettings 파일 삭제를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-156">After importing the publish settings, consider deleting the downloaded .publishSettings file, because it contains information that could allow someone to access your account.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="33df3-157">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="33df3-157">Publish the application</span></span>
<span data-ttu-id="33df3-158">게시하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-158">To publish, run the following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="33df3-159">**-ServiceName**은 배포에 대한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-159">**-ServiceName** specifies the name for the deployment.</span></span> <span data-ttu-id="33df3-160">이 이름은 고유해야 합니다. 그렇지 않으면 게시 프로세스가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-160">This must be a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="33df3-161">**Get-Date** 명령은 이름을 고유하게 만들어야 하는 날짜/시간 문자열을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-161">The **Get-Date** command tacks on a date/time string that should make the name unique.</span></span>
* <span data-ttu-id="33df3-162">**-위치** 응용 프로그램이 호스팅될 데이터센터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-162">**-Location** specifies the datacenter that the application will be hosted in.</span></span> <span data-ttu-id="33df3-163">사용 가능한 데이터센터 목록을 보려면 **Get-AzureLocation** cmdlet을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="33df3-163">To see a list of available datacenters, use the **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="33df3-164">**-Launch** 는 브라우저 창을 열고 배포가 완료 된 후 호스티ㅡㄷ 서비스를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-164">**-Launch** opens a browser window and navigates to the hosted service after deployment has completed.</span></span>

<span data-ttu-id="33df3-165">게시가 성공하면 다음과 같은 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-165">After publishing succeeds, you will see a response similar to the following:</span></span>

![The output of the Publish-AzureService command][The output of the Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="33df3-167">응용 프로그램이 처음 게시된 후 몇 분 지나야 배포되어 사용이 가능할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-167">It can take several minutes for the application to deploy and become available when first published.</span></span>

<span data-ttu-id="33df3-168">배포가 완료되면 브라우저 창이 열리고 클라우드 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-168">Once the deployment has completed, a browser window will open and navigate to the cloud service.</span></span>

![hello world 페이지가 표시된 브라우저 창. URL은 Azure에 호스팅된 페이지임을 나타냅니다.][A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]

<span data-ttu-id="33df3-170">이제 응용 프로그램이 Azure에서 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="33df3-171">**Publish-AzureServiceProject** cmdlet은 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-171">The **Publish-AzureServiceProject** cmdlet performs the following steps:</span></span>

1. <span data-ttu-id="33df3-172">배포할 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-172">Creates a package to deploy.</span></span> <span data-ttu-id="33df3-173">이 패키지에는 응용 프로그램 폴더의 모든 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-173">The package contains all the files in your application folder.</span></span>
2. <span data-ttu-id="33df3-174">**저장소 계정** 이 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="33df3-175">Azure 저장소 계정은 배포 중 응용 프로그램 패키지를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-175">The Azure storage account is used to store the application package during deployment.</span></span> <span data-ttu-id="33df3-176">배포가 완료된 후에는 저장소 계정을 삭제해도 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-176">You can safely delete the storage account after deployment is done.</span></span>
3. <span data-ttu-id="33df3-177">**클라우드 서비스** 가 아직 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="33df3-178">**클라우드 서비스** 는 응용 프로그램이 Azure에 배포될 때 호스트되는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-178">A **cloud service** is the container in which your application is hosted when it is deployed to Azure.</span></span> <span data-ttu-id="33df3-179">자세한 내용은 [Azure에 대한 호스티드 서비스 만들기 개요](영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33df3-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="33df3-180">배포 패키지를 Azure에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-180">Publishes the deployment package to Azure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="33df3-181">응용 프로그램 중지 및 삭제</span><span class="sxs-lookup"><span data-stu-id="33df3-181">Stopping and deleting your application</span></span>
<span data-ttu-id="33df3-182">응용 프로그램을 배포한 후 사용하지 않도록 설정하여 추가 비용을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-182">After deploying your application, you may want to disable it so you can avoid extra costs.</span></span> <span data-ttu-id="33df3-183">Azure는 사용된 서버 시간의 시간당 웹 역할 인스턴스 요금을 청구합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="33df3-184">서버 시간은 응용 프로그램이 배포된 다음에 사용되며 인스턴스가 실행되지 않고 중지된 상태인 경우에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-184">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

1. <span data-ttu-id="33df3-185">Windows PowerShell 창에서, 이전 섹션에서 만든 서비스 배포를 다음 cmdlet을 사용하여 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-185">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="33df3-186">서비스를 중지하려면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-186">Stopping the service may take several minutes.</span></span> <span data-ttu-id="33df3-187">서비스가 중지되면 서비스가 중지되었다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-187">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![Stop-AzureService 명령의 상태][The status of the Stop-AzureService command]
2. <span data-ttu-id="33df3-189">서비스를 삭제하려면 다음 cmdlet을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-189">To delete the service, call the following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="33df3-190">메시지가 표시되면 **Y** 를 입력하여 서비스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-190">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="33df3-191">서비스를 삭제하려면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-191">Deleting the service may take several minutes.</span></span> <span data-ttu-id="33df3-192">서비스가 삭제되면 서비스가 삭제되었다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-192">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

   ![Remove-AzureService 명령의 상태][The status of the Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="33df3-194">서비스를 삭제해도 서비스가 처음 게시될 때 만들어진 저장소 계정은 삭제되지 않으므로 사용된 저장소에 대해 계속 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-194">Deleting the service does not delete the storage account that was created when the service was initially published, and you will continue to be billed for storage used.</span></span> <span data-ttu-id="33df3-195">저장소를 전혀 사용하지 않으면 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="33df3-195">If nothing else is using the storage, you may want to delete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33df3-196">다음 단계</span><span class="sxs-lookup"><span data-stu-id="33df3-196">Next steps</span></span>
<span data-ttu-id="33df3-197">자세한 내용은 [Node.js 개발자 센터]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="33df3-197">For more information, see the [Node.js Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="33df3-198">[Azure 웹 사이트, 클라우드 서비스 및 가상 컴퓨터 비교]: ../app-service-web/choose-web-site-cloud-service-vm.md</span><span class="sxs-lookup"><span data-stu-id="33df3-198">[Azure Websites, Cloud Services and Virtual Machines comparison]: ../app-service-web/choose-web-site-cloud-service-vm.md</span></span>
<span data-ttu-id="33df3-199">[간단한 웹앱 사용]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="33df3-199">[using a lightweight web app]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="33df3-200">[Azure PowerShell]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="33df3-200">[Azure Powershell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="33df3-201">[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span><span class="sxs-lookup"><span data-stu-id="33df3-201">[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span></span>
<span data-ttu-id="33df3-202">[PowerShell을 연결]: /powershell/azureps-cmdlets-docs#step-3-connect</span><span class="sxs-lookup"><span data-stu-id="33df3-202">[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span></span>
<span data-ttu-id="33df3-203">[nodejs.org]: http://nodejs.org/</span><span class="sxs-lookup"><span data-stu-id="33df3-203">[nodejs.org]: http://nodejs.org/</span></span>
<span data-ttu-id="33df3-204">[Azure에 대한 호스티드 서비스 만들기 개요]: https://azure.microsoft.com/documentation/services/cloud-services/</span><span class="sxs-lookup"><span data-stu-id="33df3-204">[Overview of Creating a Hosted Service for Azure]: https://azure.microsoft.com/documentation/services/cloud-services/</span></span>
<span data-ttu-id="33df3-205">[Node.js 개발자 센터]: https://azure.microsoft.com/develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="33df3-205">[Node.js Developer Center]: https://azure.microsoft.com/develop/nodejs/</span></span>

<!-- IMG List -->

[The result of the New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[The output of the Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying the Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[The status of the Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[The status of the Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
