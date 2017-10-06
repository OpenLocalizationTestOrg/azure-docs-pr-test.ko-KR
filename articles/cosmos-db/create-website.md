---
title: "-Azure Cosmos DB 템플릿 사용 하 여 웹 응용 프로그램 aaaDeploy | Microsoft Docs"
description: "어떻게 toodeploy Azure Cosmos DB 계정, Azure 앱 서비스 웹 앱 및 샘플 웹 Azure 리소스 관리자 템플릿을 사용 하는 응용 프로그램에 알아봅니다."
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a><span data-ttu-id="ec06e-103">Azure Resource Manager 템플릿을 사용하여 Azure Cosmos DB 및 Azure App Service Web Apps 배포</span><span class="sxs-lookup"><span data-stu-id="ec06e-103">Deploy Azure Cosmos DB and Azure App Service Web Apps using an Azure Resource Manager Template</span></span>
<span data-ttu-id="ec06e-104">이 자습서에서는 Azure 리소스 관리자 템플릿 toodeploy toouse 통합 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) web app 및 샘플 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-104">This tutorial shows you how toouse an Azure Resource Manager template toodeploy and integrate [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app, and a sample web application.</span></span>

<span data-ttu-id="ec06e-105">Azure 리소스 관리자 템플릿을 사용 하 여 Azure 리소스의 hello 배포 및 구성을 쉽게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-105">Using Azure Resource Manager templates, you can easily automate hello deployment and configuration of your Azure resources.</span></span>  <span data-ttu-id="ec06e-106">이 자습서에서는 방법을 toodeploy 웹 응용 프로그램을 자동으로 Azure Cosmos DB 계정 연결 정보를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-106">This tutorial shows how toodeploy a web application and automatically configure Azure Cosmos DB account connection information.</span></span>

<span data-ttu-id="ec06e-107">이 자습서를 완료 하면 다음 질문 수 tooanswer hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-107">After completing this tutorial, you will be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="ec06e-108">Azure 리소스 관리자 템플릿 toodeploy 사용을 Azure Cosmos DB 계정 및 Azure 앱 서비스의 웹 응용 프로그램을 통합할 수 있습니다 어떻게 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ec06e-108">How can I use an Azure Resource Manager template toodeploy and integrate an Azure Cosmos DB account and a web app in Azure App Service?</span></span>
* <span data-ttu-id="ec06e-109">Azure 리소스 관리자 템플릿 toodeploy를 사용 하 여을 Azure Cosmos DB 계정, 앱 서비스 웹 앱의 웹 앱 및 Webdeploy 응용 프로그램을 통합할 수 있습니다 어떻게 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ec06e-109">How can I use an Azure Resource Manager template toodeploy and integrate an Azure Cosmos DB account, a web app in App Service Web Apps, and a Webdeploy application?</span></span>

<a id="Prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="ec06e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ec06e-110">Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="ec06e-111">이 자습서에서는 이전 Azure 리소스 관리자 템플릿을 또는 JSON 사용해 본 경험이 가정 하지, 해야 경우 할 toomodify hello 템플릿이나 배포 옵션을 참조 한 후 이러한 각 영역에 대 한 지식이 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-111">While this tutorial does not assume prior experience with Azure Resource Manager templates or JSON, should you wish toomodify hello referenced templates or deployment options, then knowledge of each of these areas will be required.</span></span>
> 
> 

<span data-ttu-id="ec06e-112">이 자습서에서는 hello 지침을 수행 하기 전에 hello 다음 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-112">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="ec06e-113">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="ec06e-113">An Azure subscription.</span></span> <span data-ttu-id="ec06e-114">Azure는 구독 기반 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-114">Azure is a subscription-based platform.</span></span>  <span data-ttu-id="ec06e-115">구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션](https://azure.microsoft.com/pricing/purchase-options/), [구성원 제공 항목](https://azure.microsoft.com/pricing/member-offers/) 또는 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec06e-115">For more information about obtaining a subscription, see [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), [Member Offers](https://azure.microsoft.com/pricing/member-offers/), or [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="ec06e-116"><a id="CreateDB"></a>1 단계: hello 템플릿 파일을 다운로드</span><span class="sxs-lookup"><span data-stu-id="ec06e-116"><a id="CreateDB"></a>Step 1: Download hello template files</span></span>
<span data-ttu-id="ec06e-117">이 자습서에 사용 될 hello 템플릿 파일을 다운로드 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-117">Let's start by downloading hello template files we will use in this tutorial.</span></span>

1. <span data-ttu-id="ec06e-118">Hello 다운로드 [Azure Cosmos DB 계정, 웹 응용 프로그램을 만들고 데모 응용 프로그램 샘플 배포](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) 템플릿 tooa 로컬 폴더 (예: C:\Azure Cosmos DBTemplates).</span><span class="sxs-lookup"><span data-stu-id="ec06e-118">Download hello [Create an Azure Cosmos DB account, Web Apps, and deploy a demo application sample](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) template tooa local folder (e.g. C:\Azure Cosmos DBTemplates).</span></span> <span data-ttu-id="ec06e-119">이 템플릿은 Azure Cosmos DB 계정, App Service 웹앱 및 웹 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-119">This template will deploy an Azure Cosmos DB account, an App Service web app, and a web application.</span></span>  <span data-ttu-id="ec06e-120">Hello 웹 응용 프로그램 tooconnect toohello Azure Cosmos DB 계정을 자동으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-120">It will also automatically configure hello web application tooconnect toohello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="ec06e-121">Hello 다운로드 [Azure Cosmos DB 계정 및 웹 앱 샘플을 만드는](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) 템플릿 tooa 로컬 폴더 (예: C:\Azure Cosmos DBTemplates).</span><span class="sxs-lookup"><span data-stu-id="ec06e-121">Download hello [Create an Azure Cosmos DB account and Web Apps sample](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) template tooa local folder (e.g. C:\Azure Cosmos DBTemplates).</span></span> <span data-ttu-id="ec06e-122">이 템플릿은 Azure Cosmos DB 계정을 앱 서비스 웹 앱을 배포 합니다 및 hello 사이트의 응용 프로그램 설정 tooeasily 표면 Azure Cosmos DB 연결 정보를 수정 합니다 있지만 웹 응용 프로그램에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-122">This template will deploy an Azure Cosmos DB account, an App Service web app, and will modify hello site's application settings tooeasily surface Azure Cosmos DB connection information, but does not include a web application.</span></span>  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a><span data-ttu-id="ec06e-123">2 단계: 배포 hello Azure Cosmos DB 계정으로 앱 서비스 웹 앱과 데모 응용 프로그램 샘플</span><span class="sxs-lookup"><span data-stu-id="ec06e-123">Step 2: Deploy hello Azure Cosmos DB account, App Service web app and demo application sample</span></span>
<span data-ttu-id="ec06e-124">이제 첫 번째 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-124">Now let's deploy our first template.</span></span>

> [!TIP]
> <span data-ttu-id="ec06e-125">hello 템플릿 hello 웹 응용 프로그램 이름 및 Azure Cosmos DB 계정 이름 아래에 입력 되는) 유효 하 고 b) 사용 가능한 유효성이 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-125">hello template does not validate that hello web app name and Azure Cosmos DB account name entered below are a) valid and b) available.</span></span>  <span data-ttu-id="ec06e-126">Hello 가용성 hello의 이름을 확인 하는 것이 좋습니다 toosupply 이전 toosubmitting hello 배포를 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-126">It is highly recommended that you verify hello availability of hello names you plan toosupply prior toosubmitting hello deployment.</span></span>
> 
> 

1. <span data-ttu-id="ec06e-127">로그인 toohello [Azure 포털](https://portal.azure.com)"템플릿 배포"에 대 한 검색을 새로 만들기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-127">Login toohello [Azure Portal](https://portal.azure.com), click New and search for "Template deployment".</span></span>
    <span data-ttu-id="ec06e-128">![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment1.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-128">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment1.png)</span></span>
2. <span data-ttu-id="ec06e-129">Hello 템플릿 배포 항목을 선택 하 고 클릭 **만들기** ![hello 템플릿 배포 UI의 스크린 샷](./media/create-website/TemplateDeployment2.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-129">Select hello Template deployment item and click **Create** ![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment2.png)</span></span>
3. <span data-ttu-id="ec06e-130">클릭 **템플릿 편집**hello DocDBWebsiteTodo.json 템플릿 파일의 hello 내용을 붙여넣고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-130">Click **Edit template**, paste hello contents of hello DocDBWebsiteTodo.json template file, and click **Save**.</span></span>
   <span data-ttu-id="ec06e-131">![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment3.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-131">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment3.png)</span></span>
4. <span data-ttu-id="ec06e-132">클릭 **매개 변수 편집**각 매개 변수에 필수 hello에 대 한 값을 제공 하 고 클릭, **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-132">Click **Edit parameters**, provide values for each of hello mandatory parameters, and click **OK**.</span></span>  <span data-ttu-id="ec06e-133">hello 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-133">hello parameters are as follows:</span></span>
   
   1. <span data-ttu-id="ec06e-134">SITENAME: hello 앱 서비스 웹 앱 이름 지정 및 tooaccess hello 웹 응용 프로그램 사용 하 여 사용 되는 tooconstruct hello URL입니다 (예: 경우 "mydemodocdbwebapp"를 지정 하 고 hello URL hello 웹 응용 프로그램을 액세스 합니다 기준이 됩니다. mydemodocdbwebapp.azurewebsites.net)입니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-134">SITENAME: Specifies hello App Service web app name and is used tooconstruct hello URL that you will use tooaccess hello web app (e.g. if you specify "mydemodocdbwebapp", then hello URL by which you will access hello web app will be mydemodocdbwebapp.azurewebsites.net).</span></span>
   2. <span data-ttu-id="ec06e-135">HOSTINGPLANNAME: 앱 서비스 계획 toocreate 호스팅의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-135">HOSTINGPLANNAME: Specifies hello name of App Service hosting plan toocreate.</span></span>
   3. <span data-ttu-id="ec06e-136">위치: 지정 hello toocreate hello Azure Cosmos DB 및 웹 응용 프로그램 리소스에는 Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-136">LOCATION: Specifies hello Azure location in which toocreate hello Azure Cosmos DB and web app resources.</span></span>
   4. <span data-ttu-id="ec06e-137">DATABASEACCOUNTNAME: hello Azure Cosmos DB 계정 toocreate의 hello 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-137">DATABASEACCOUNTNAME: Specifies hello name of hello Azure Cosmos DB account toocreate.</span></span>   
      
      ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment4.png)
5. <span data-ttu-id="ec06e-139">기존 리소스 그룹을 선택 또는 새 리소스 그룹 이름을 toomake를 제공 하 고 hello 리소스 그룹에 대 한 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-139">Choose an existing Resource group or provide a name toomake a new resource group, and choose a location for hello resource group.</span></span>

    ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment5.png)
6. <span data-ttu-id="ec06e-141">클릭 **약관을 검토**, **구매**, 클릭 하 고 **만들기** toobegin hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-141">Click **Review legal terms**, **Purchase**, and then click **Create** toobegin hello deployment.</span></span>  <span data-ttu-id="ec06e-142">선택 **Pin toodashboard** hello 결과 배포는 Azure 포털 홈 페이지에 쉽게 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-142">Select **Pin toodashboard** so hello resulting deployment is easily visible on your Azure portal home page.</span></span>
   <span data-ttu-id="ec06e-143">![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment6.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-143">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment6.png)</span></span>
7. <span data-ttu-id="ec06e-144">Hello 배포 완료 되 면 hello 리소스 그룹 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-144">When hello deployment finishes, hello Resource group blade will open.</span></span>
   <span data-ttu-id="ec06e-145">![Hello 리소스 그룹 블레이드의 스크린샷](./media/create-website/TemplateDeployment7.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-145">![Screenshot of hello resource group blade](./media/create-website/TemplateDeployment7.png)</span></span>  
8. <span data-ttu-id="ec06e-146">toouse 단순히 toohello 웹 앱 URL을 이동 하 여 응용 프로그램 hello (hello 위의 예에서 hello URL 일 http://mydemodocdbwebapp.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="ec06e-146">toouse hello application, simply navigate toohello web app URL (in hello example above, hello URL would be http://mydemodocdbwebapp.azurewebsites.net).</span></span>  <span data-ttu-id="ec06e-147">웹 응용 프로그램을 다음 hello에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-147">You'll see hello following web application:</span></span>
   
   ![샘플 Todo 응용 프로그램](./media/create-website/image2.png)
9. <span data-ttu-id="ec06e-149">계속 하 고 hello 웹 앱에서 몇 가지 작업을 만드는 hello Azure 포털에서에서 toohello 리소스 그룹 블레이드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-149">Go ahead and create a couple of tasks in hello web app and then return toohello Resource group blade in hello Azure portal.</span></span> <span data-ttu-id="ec06e-150">Hello 리소스 목록에 hello Azure Cosmos DB 계정 리소스를 클릭 한 다음 클릭 **쿼리 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-150">Click hello Azure Cosmos DB account resource in hello Resources list and then click **Query Explorer**.</span></span>
    <span data-ttu-id="ec06e-151">![강조 표시 하는 hello 웹 앱과 요약 렌즈를 hello의 스크린샷](./media/create-website/TemplateDeployment8.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-151">![Screenshot of hello Summary lens with hello web app highlighted](./media/create-website/TemplateDeployment8.png)</span></span>  
10. <span data-ttu-id="ec06e-152">Hello 기본 쿼리를 실행 "선택 * c에서" hello 결과 검사 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-152">Run hello default query, "SELECT * FROM c" and inspect hello results.</span></span>  <span data-ttu-id="ec06e-153">Hello 쿼리 7 위의 단계에서 만든 hello 할 일 항목의 JSON 표현을 hello를 읽어들일 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-153">Notice that hello query has retrieved hello JSON representation of hello todo items you created in step 7 above.</span></span>  <span data-ttu-id="ec06e-154">쿼리로; 무료 tooexperiment을 생각 합니다. 예를 들어 SELECT를 실행 해 보십시오 * FROM c WHERE c.isComplete = true tooreturn 완료 상태로 표시 된 모든 할 일 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-154">Feel free tooexperiment with queries; for example, try running SELECT * FROM c WHERE c.isComplete = true tooreturn all todo items which have been marked as complete.</span></span>
    
    ![Hello 쿼리 탐색기 및 결과 블레이드 hello 쿼리 결과 보여 주는 스크린샷](./media/create-website/image5.png)
11. <span data-ttu-id="ec06e-156">무료 tooexplore hello Azure Cosmos DB 포털 환경 느껴집니다 또는 hello 샘플 Todo 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-156">Feel free tooexplore hello Azure Cosmos DB portal experience or modify hello sample Todo application.</span></span>  <span data-ttu-id="ec06e-157">준비가 되면 다른 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-157">When you're ready, let's deploy another template.</span></span>

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a><span data-ttu-id="ec06e-158">3 단계: 배포 hello 문서 계정 및 웹 앱 샘플</span><span class="sxs-lookup"><span data-stu-id="ec06e-158">Step 3: Deploy hello Document account and web app sample</span></span>
<span data-ttu-id="ec06e-159">이제 두 번째 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-159">Now let's deploy our second template.</span></span>  <span data-ttu-id="ec06e-160">이 서식 파일은 유용 tooshow 어떻게 주입할 수 계정 끝점 및 마스터 키와 같은 Azure Cosmos DB 연결 정보는 웹 앱에 응용 프로그램 설정 또는 사용자 지정 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-160">This template is useful tooshow how you can inject Azure Cosmos DB connection information such as account endpoint and master key into a web app as application settings or as a custom connection string.</span></span> <span data-ttu-id="ec06e-161">예를 들어 경우가 있습니다 직접 웹 응용 프로그램을 Azure Cosmos DB 계정과 toodeploy 선택한 hello 연결 정보를 배포 하는 동안 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-161">For example, perhaps you have your own web application that you would like toodeploy with an Azure Cosmos DB account and have hello connection information automatically populated during deployment.</span></span>

> [!TIP]
> <span data-ttu-id="ec06e-162">hello 템플릿 hello 웹 응용 프로그램 이름 및 Azure Cosmos DB 계정 이름 아래에 입력 되는) 유효 하 고 b) 사용 가능한 유효성이 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-162">hello template does not validate that hello web app name and Azure Cosmos DB account name entered below are a) valid and b) available.</span></span>  <span data-ttu-id="ec06e-163">Hello 가용성 hello의 이름을 확인 하는 것이 좋습니다 toosupply 이전 toosubmitting hello 배포를 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-163">It is highly recommended that you verify hello availability of hello names you plan toosupply prior toosubmitting hello deployment.</span></span>
> 
> 

1. <span data-ttu-id="ec06e-164">Hello에 [Azure 포털](https://portal.azure.com)"템플릿 배포"에 대 한 검색을 새로 만들기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-164">In hello [Azure Portal](https://portal.azure.com), click New and search for "Template deployment".</span></span>
    <span data-ttu-id="ec06e-165">![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment1.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-165">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment1.png)</span></span>
2. <span data-ttu-id="ec06e-166">Hello 템플릿 배포 항목을 선택 하 고 클릭 **만들기** ![hello 템플릿 배포 UI의 스크린 샷](./media/create-website/TemplateDeployment2.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-166">Select hello Template deployment item and click **Create** ![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment2.png)</span></span>
3. <span data-ttu-id="ec06e-167">클릭 **템플릿 편집**hello DocDBWebSite.json 템플릿 파일의 hello 내용을 붙여넣고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-167">Click **Edit template**, paste hello contents of hello DocDBWebSite.json template file, and click **Save**.</span></span>
   <span data-ttu-id="ec06e-168">![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment3.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-168">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment3.png)</span></span>
4. <span data-ttu-id="ec06e-169">클릭 **매개 변수 편집**각 매개 변수에 필수 hello에 대 한 값을 제공 하 고 클릭, **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-169">Click **Edit parameters**, provide values for each of hello mandatory parameters, and click **OK**.</span></span>  <span data-ttu-id="ec06e-170">hello 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-170">hello parameters are as follows:</span></span>
   
   1. <span data-ttu-id="ec06e-171">SITENAME: hello 앱 서비스 웹 앱 이름 지정 및 tooaccess hello 웹 응용 프로그램 사용 하 여 사용 되는 tooconstruct hello URL입니다 (예: 경우 "mydemodocdbwebapp"를 지정 하 고 hello URL hello 웹 응용 프로그램을 액세스 합니다 기준이 됩니다. mydemodocdbwebapp.azurewebsites.net)입니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-171">SITENAME: Specifies hello App Service web app name and is used tooconstruct hello URL that you will use tooaccess hello web app (e.g. if you specify "mydemodocdbwebapp", then hello URL by which you will access hello web app will be mydemodocdbwebapp.azurewebsites.net).</span></span>
   2. <span data-ttu-id="ec06e-172">HOSTINGPLANNAME: 앱 서비스 계획 toocreate 호스팅의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-172">HOSTINGPLANNAME: Specifies hello name of App Service hosting plan toocreate.</span></span>
   3. <span data-ttu-id="ec06e-173">위치: 지정 hello toocreate hello Azure Cosmos DB 및 웹 응용 프로그램 리소스에는 Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-173">LOCATION: Specifies hello Azure location in which toocreate hello Azure Cosmos DB and web app resources.</span></span>
   4. <span data-ttu-id="ec06e-174">DATABASEACCOUNTNAME: hello Azure Cosmos DB 계정 toocreate의 hello 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-174">DATABASEACCOUNTNAME: Specifies hello name of hello Azure Cosmos DB account toocreate.</span></span>   
      
      ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment4.png)
5. <span data-ttu-id="ec06e-176">기존 리소스 그룹을 선택 또는 새 리소스 그룹 이름을 toomake를 제공 하 고 hello 리소스 그룹에 대 한 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-176">Choose an existing Resource group or provide a name toomake a new resource group, and choose a location for hello resource group.</span></span>

    ![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment5.png)
6. <span data-ttu-id="ec06e-178">클릭 **약관을 검토**, **구매**, 클릭 하 고 **만들기** toobegin hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-178">Click **Review legal terms**, **Purchase**, and then click **Create** toobegin hello deployment.</span></span>  <span data-ttu-id="ec06e-179">선택 **Pin toodashboard** hello 결과 배포는 Azure 포털 홈 페이지에 쉽게 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-179">Select **Pin toodashboard** so hello resulting deployment is easily visible on your Azure portal home page.</span></span>
   <span data-ttu-id="ec06e-180">![Hello 템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment6.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-180">![Screenshot of hello template deployment UI](./media/create-website/TemplateDeployment6.png)</span></span>
7. <span data-ttu-id="ec06e-181">Hello 배포 완료 되 면 hello 리소스 그룹 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-181">When hello deployment finishes, hello Resource group blade will open.</span></span>
   <span data-ttu-id="ec06e-182">![Hello 리소스 그룹 블레이드의 스크린샷](./media/create-website/TemplateDeployment7.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-182">![Screenshot of hello resource group blade](./media/create-website/TemplateDeployment7.png)</span></span>  
8. <span data-ttu-id="ec06e-183">Hello 리소스 목록에 hello 웹 응용 프로그램 리소스를 클릭 한 다음 클릭 **응용 프로그램 설정** ![hello 리소스 그룹의 스크린 샷](./media/create-website/TemplateDeployment9.png)</span><span class="sxs-lookup"><span data-stu-id="ec06e-183">Click hello Web App resource in hello Resources list and then click **Application settings** ![Screenshot of hello resource group](./media/create-website/TemplateDeployment9.png)</span></span>  
9. <span data-ttu-id="ec06e-184">Note 있다는 hello Azure Cosmos DB 끝점 및 각 hello Azure Cosmos DB 마스터 키에 있는 응용 프로그램 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-184">Note how there are application settings present for hello Azure Cosmos DB endpoint and each of hello Azure Cosmos DB master keys.</span></span>

    ![응용 프로그램 설정의 스크린샷](./media/create-website/TemplateDeployment10.png)  
10. <span data-ttu-id="ec06e-186">Hello Azure 포털을 탐색 하는 무료 toocontinue 느껴집니다 또는 우리의 Azure Cosmos DB 중 하나를 수행 [샘플](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate Azure Cosmos DB 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-186">Feel free toocontinue exploring hello Azure Portal, or follow one of our Azure Cosmos DB [samples](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate your own Azure Cosmos DB application.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="ec06e-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec06e-187">Next steps</span></span>
<span data-ttu-id="ec06e-188">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-188">Congratulations!</span></span> <span data-ttu-id="ec06e-189">Azure Resource Manager 템플릿을 사용하여 Azure Cosmos DB, App Service 웹앱 및 샘플 웹 응용 프로그램을 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-189">You've deployed Azure Cosmos DB, App Service web app and a sample web application using Azure Resource Manager templates.</span></span>

* <span data-ttu-id="ec06e-190">Azure Cosmos DB에 대해 자세히 toolearn 클릭 [여기](http://azure.com/docdb)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-190">toolearn more about Azure Cosmos DB, click [here](http://azure.com/docdb).</span></span>
* <span data-ttu-id="ec06e-191">Azure 앱 서비스 웹 앱에 대해 자세히 toolearn 클릭 [여기](http://go.microsoft.com/fwlink/?LinkId=325362)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-191">toolearn more about Azure App Service Web apps, click [here](http://go.microsoft.com/fwlink/?LinkId=325362).</span></span>
* <span data-ttu-id="ec06e-192">Azure 리소스 관리자 템플릿에 대해 자세히 toolearn 클릭 [여기](https://msdn.microsoft.com/library/azure/dn790549.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-192">toolearn more about Azure Resource Manager templates, click [here](https://msdn.microsoft.com/library/azure/dn790549.aspx).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="ec06e-193">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="ec06e-193">What's changed</span></span>
* <span data-ttu-id="ec06e-194">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ec06e-194">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
* <span data-ttu-id="ec06e-195">가이드 toohello hello 이전 포털 toohello 새 포털의 변경 참조: [탐색에 대 한 참조 hello Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkId=529715)</span><span class="sxs-lookup"><span data-stu-id="ec06e-195">For a guide toohello change of hello old portal toohello new portal see: [Reference for navigating hello Azure Classic Portal](http://go.microsoft.com/fwlink/?LinkId=529715)</span></span>

> [!NOTE]
> <span data-ttu-id="ec06e-196">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](http://go.microsoft.com/fwlink/?LinkId=523751)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-196">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](http://go.microsoft.com/fwlink/?LinkId=523751), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ec06e-197">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec06e-197">No credit cards required; no commitments.</span></span>
> 
> 

