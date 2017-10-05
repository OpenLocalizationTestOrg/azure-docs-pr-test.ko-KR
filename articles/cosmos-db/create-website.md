---
title: "템플릿을 사용하여 웹앱 배포 - Azure Cosmos DB | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 Azure Cosmos DB 계정, Azure App Service Web Apps 및 샘플 웹 응용 프로그램을 배포하는 방법을 알아봅니다."
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
ms.openlocfilehash: 633b88761de4d2c99cfd196cfac8e664fc83c546
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a><span data-ttu-id="4cd75-103">Azure Resource Manager 템플릿을 사용하여 Azure Cosmos DB 및 Azure App Service Web Apps 배포</span><span class="sxs-lookup"><span data-stu-id="4cd75-103">Deploy Azure Cosmos DB and Azure App Service Web Apps using an Azure Resource Manager Template</span></span>
<span data-ttu-id="4cd75-104">이 자습서에서는 Azure Resource Manager 템플릿을 사용하여 [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 웹앱 및 샘플 웹 응용 프로그램을 배포 및 통합하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-104">This tutorial shows you how to use an Azure Resource Manager template to deploy and integrate [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app, and a sample web application.</span></span>

<span data-ttu-id="4cd75-105">Azure Resource Manager 템플릿을 사용하여 Azure 리소스의 배포 및 구성을 쉽게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-105">Using Azure Resource Manager templates, you can easily automate the deployment and configuration of your Azure resources.</span></span>  <span data-ttu-id="4cd75-106">이 자습서에서는 웹 응용 프로그램을 배포하고 자동으로 Azure Cosmos DB 계정 연결 정보를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-106">This tutorial shows how to deploy a web application and automatically configure Azure Cosmos DB account connection information.</span></span>

<span data-ttu-id="4cd75-107">이 자습서를 완료하고 나면 다음을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-107">After completing this tutorial, you will be able to answer the following questions:</span></span>  

* <span data-ttu-id="4cd75-108">Azure Resource Manager 템플릿을 사용하여 Azure App Service에서 Azure Cosmos DB 계정 및 웹앱을 배포하고 통합하는 방법</span><span class="sxs-lookup"><span data-stu-id="4cd75-108">How can I use an Azure Resource Manager template to deploy and integrate an Azure Cosmos DB account and a web app in Azure App Service?</span></span>
* <span data-ttu-id="4cd75-109">Azure Resource Manager 템플릿을 사용하여 App Service Web Apps 및 Webdeploy 응용 프로그램에서 Azure Cosmos DB 계정 및 웹앱을 배포 및 통합하는 방법</span><span class="sxs-lookup"><span data-stu-id="4cd75-109">How can I use an Azure Resource Manager template to deploy and integrate an Azure Cosmos DB account, a web app in App Service Web Apps, and a Webdeploy application?</span></span>

<a id="Prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="4cd75-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4cd75-110">Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="4cd75-111">이 자습서에서는 Azure Resource Manager 템플릿 또는 JSON을 이전에 사용해 본 경험이 있다고 가정하지는 않지만, 참조된 템플릿 또는 배포 옵션을 수정하려면 이러한 각 영역에 대한 지식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-111">While this tutorial does not assume prior experience with Azure Resource Manager templates or JSON, should you wish to modify the referenced templates or deployment options, then knowledge of each of these areas will be required.</span></span>
> 
> 

<span data-ttu-id="4cd75-112">이 자습서의 지침을 따르기 전에 다음이 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="4cd75-112">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="4cd75-113">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="4cd75-113">An Azure subscription.</span></span> <span data-ttu-id="4cd75-114">Azure는 구독 기반 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-114">Azure is a subscription-based platform.</span></span>  <span data-ttu-id="4cd75-115">구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션](https://azure.microsoft.com/pricing/purchase-options/), [구성원 제공 항목](https://azure.microsoft.com/pricing/member-offers/) 또는 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4cd75-115">For more information about obtaining a subscription, see [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), [Member Offers](https://azure.microsoft.com/pricing/member-offers/), or [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="4cd75-116"><a id="CreateDB"></a>1단계: 템플릿 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="4cd75-116"><a id="CreateDB"></a>Step 1: Download the template files</span></span>
<span data-ttu-id="4cd75-117">먼저 이 자습서에서 사용할 템플릿 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-117">Let's start by downloading the template files we will use in this tutorial.</span></span>

1. <span data-ttu-id="4cd75-118">[Azure Cosmos DB 계정, Web Apps 만들기 및 데모 응용 프로그램 배포 샘플](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) 템플릿을 로컬 폴더(예: C:\Azure Cosmos DBTemplates)에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-118">Download the [Create an Azure Cosmos DB account, Web Apps, and deploy a demo application sample](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) template to a local folder (e.g. C:\Azure Cosmos DBTemplates).</span></span> <span data-ttu-id="4cd75-119">이 템플릿은 Azure Cosmos DB 계정, App Service 웹앱 및 웹 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-119">This template will deploy an Azure Cosmos DB account, an App Service web app, and a web application.</span></span>  <span data-ttu-id="4cd75-120">또한 Azure Cosmos DB 계정에 연결되도록 웹 응용 프로그램을 자동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-120">It will also automatically configure the web application to connect to the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="4cd75-121">[Azure Cosmos DB 계정 및 Web Apps 만들기 샘플](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) 템플릿을 로컬 폴더(예: C:\Azure Cosmos DBTemplates)에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-121">Download the [Create an Azure Cosmos DB account and Web Apps sample](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) template to a local folder (e.g. C:\Azure Cosmos DBTemplates).</span></span> <span data-ttu-id="4cd75-122">이 템플릿은 Azure Cosmos DB 계정 및 App Service 웹앱을 배포하고 쉽게 Azure Cosmos DB 연결 정보를 노출하도록 사이트의 응용 프로그램 설정을 수정하지만 웹 응용 프로그램을 포함하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-122">This template will deploy an Azure Cosmos DB account, an App Service web app, and will modify the site's application settings to easily surface Azure Cosmos DB connection information, but does not include a web application.</span></span>  

<a id="Build"></a>

## <a name="step-2-deploy-the-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a><span data-ttu-id="4cd75-123">2단계: Azure Cosmos DB 계정, App Service 웹앱 및 데모 응용 프로그램 샘플 배포</span><span class="sxs-lookup"><span data-stu-id="4cd75-123">Step 2: Deploy the Azure Cosmos DB account, App Service web app and demo application sample</span></span>
<span data-ttu-id="4cd75-124">이제 첫 번째 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-124">Now let's deploy our first template.</span></span>

> [!TIP]
> <span data-ttu-id="4cd75-125">템플릿은 아래에 입력된 웹앱 이름과 Azure Cosmos DB 계정 이름이 a) 유효한지, b) 사용 가능한지를 확인하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-125">The template does not validate that the web app name and Azure Cosmos DB account name entered below are a) valid and b) available.</span></span>  <span data-ttu-id="4cd75-126">배포를 제출하기 전에 지정하려는 이름의 가용성을 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-126">It is highly recommended that you verify the availability of the names you plan to supply prior to submitting the deployment.</span></span>
> 
> 

1. <span data-ttu-id="4cd75-127">[Azure 포털](https://portal.azure.com)에 로그인하고 새로 만들기를 클릭하고 "템플릿 배포"를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-127">Login to the [Azure Portal](https://portal.azure.com), click New and search for "Template deployment".</span></span>
    <span data-ttu-id="4cd75-128">![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment1.png)</span><span class="sxs-lookup"><span data-stu-id="4cd75-128">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment1.png)</span></span>
2. <span data-ttu-id="4cd75-129">템플릿 배포 항목을 선택하고 **만들기** ![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment2.png)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-129">Select the Template deployment item and click **Create** ![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment2.png)</span></span>
3. <span data-ttu-id="4cd75-130">**템플릿 편집**을 클릭하고 DocDBWebsiteTodo.json 템플릿 파일의 내용을 붙여 넣고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-130">Click **Edit template**, paste the contents of the DocDBWebsiteTodo.json template file, and click **Save**.</span></span>
   <span data-ttu-id="4cd75-131">![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment3.png)</span><span class="sxs-lookup"><span data-stu-id="4cd75-131">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment3.png)</span></span>
4. <span data-ttu-id="4cd75-132">**매개 변수 편집**을 클릭하고 각 필수 매개 변수 값을 제공하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-132">Click **Edit parameters**, provide values for each of the mandatory parameters, and click **OK**.</span></span>  <span data-ttu-id="4cd75-133">매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-133">The parameters are as follows:</span></span>
   
   1. <span data-ttu-id="4cd75-134">SITENAME: 앱 서비스 웹앱 이름을 지정하고 웹앱에 액세스하는 데 사용할 URL을 만드는 데 사용됩니다(예: "mydemodocdbwebsite"를 지정할 경우 웹앱에 액세스하는 데 사용되는 URL은 mydemodocdbwebsite.azurewebsites.net이 됨).</span><span class="sxs-lookup"><span data-stu-id="4cd75-134">SITENAME: Specifies the App Service web app name and is used to construct the URL that you will use to access the web app (e.g. if you specify "mydemodocdbwebapp", then the URL by which you will access the web app will be mydemodocdbwebapp.azurewebsites.net).</span></span>
   2. <span data-ttu-id="4cd75-135">HOSTINGPLANNAME: 만들려는 앱 서비스 호스팅 계획의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-135">HOSTINGPLANNAME: Specifies the name of App Service hosting plan to create.</span></span>
   3. <span data-ttu-id="4cd75-136">LOCATION: Azure Cosmos DB 및 웹앱 리소스를 만들 Azure 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-136">LOCATION: Specifies the Azure location in which to create the Azure Cosmos DB and web app resources.</span></span>
   4. <span data-ttu-id="4cd75-137">DATABASEACCOUNTNAME: 만들 Azure Cosmos DB 계정의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-137">DATABASEACCOUNTNAME: Specifies the name of the Azure Cosmos DB account to create.</span></span>   
      
      ![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment4.png)
5. <span data-ttu-id="4cd75-139">기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만들도록 이름을 제공하며 리소스 그룹에 대한 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-139">Choose an existing Resource group or provide a name to make a new resource group, and choose a location for the resource group.</span></span>

    ![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment5.png)
6. <span data-ttu-id="4cd75-141">**약관 검토**, **구매**를 클릭한 다음 **만들기**를 클릭하여 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-141">Click **Review legal terms**, **Purchase**, and then click **Create** to begin the deployment.</span></span>  <span data-ttu-id="4cd75-142">**대시보드에 고정** 을 선택하여 결과 배포를 Azure 포털 홈 페이지에서 쉽게 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-142">Select **Pin to dashboard** so the resulting deployment is easily visible on your Azure portal home page.</span></span>
   <span data-ttu-id="4cd75-143">![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment6.png)</span><span class="sxs-lookup"><span data-stu-id="4cd75-143">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment6.png)</span></span>
7. <span data-ttu-id="4cd75-144">배포가 완료되면 리소스 그룹 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-144">When the deployment finishes, the Resource group blade will open.</span></span>
   <span data-ttu-id="4cd75-145">![리소스 그룹 블레이드의 스크린샷](./media/create-website/TemplateDeployment7.png)</span><span class="sxs-lookup"><span data-stu-id="4cd75-145">![Screenshot of the resource group blade](./media/create-website/TemplateDeployment7.png)</span></span>  
8. <span data-ttu-id="4cd75-146">응용 프로그램을 사용하려면 웹앱 URL로 이동하기만 하면 됩니다(위의 예제에서 URL은 http://mydemodocdbwebapp.azurewebsites.net이 됨).</span><span class="sxs-lookup"><span data-stu-id="4cd75-146">To use the application, simply navigate to the web app URL (in the example above, the URL would be http://mydemodocdbwebapp.azurewebsites.net).</span></span>  <span data-ttu-id="4cd75-147">다음과 같은 웹 응용 프로그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-147">You'll see the following web application:</span></span>
   
   ![샘플 Todo 응용 프로그램](./media/create-website/image2.png)
9. <span data-ttu-id="4cd75-149">계속해서 웹앱에서 몇 가지 작업을 만든 다음 Azure 포털의 리소스 그룹 블레이드로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-149">Go ahead and create a couple of tasks in the web app and then return to the Resource group blade in the Azure portal.</span></span> <span data-ttu-id="4cd75-150">리소스 목록에서 Azure Cosmos DB 계정 리소스를 클릭한 다음 **쿼리 탐색기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-150">Click the Azure Cosmos DB account resource in the Resources list and then click **Query Explorer**.</span></span>
    <span data-ttu-id="4cd75-151">![웹앱이 강조 표시된 요약 렌즈의 스크린샷](./media/create-website/TemplateDeployment8.png)</span><span class="sxs-lookup"><span data-stu-id="4cd75-151">![Screenshot of the Summary lens with the web app highlighted](./media/create-website/TemplateDeployment8.png)</span></span>  
10. <span data-ttu-id="4cd75-152">기본 쿼리 "SELECT * FROM c"를 실행하고 결과를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-152">Run the default query, "SELECT * FROM c" and inspect the results.</span></span>  <span data-ttu-id="4cd75-153">쿼리가 위의 7단계에서 만든 todo 항목의 JSON 표현을 검색했음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-153">Notice that the query has retrieved the JSON representation of the todo items you created in step 7 above.</span></span>  <span data-ttu-id="4cd75-154">자유롭게 쿼리를 실험합니다. 예를 들어 SELECT * FROM c WHERE c.isComplete = true를 실행하면 완료로 표시된 모든 todo 항목이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-154">Feel free to experiment with queries; for example, try running SELECT * FROM c WHERE c.isComplete = true to return all todo items which have been marked as complete.</span></span>
    
    ![쿼리 결과를 보여주는 쿼리 탐색기 및 결과 블레이드의 스크린샷](./media/create-website/image5.png)
11. <span data-ttu-id="4cd75-156">자유롭게 Azure Cosmos DB 포털 환경을 탐색하거나 샘플 Todo 응용 프로그램을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-156">Feel free to explore the Azure Cosmos DB portal experience or modify the sample Todo application.</span></span>  <span data-ttu-id="4cd75-157">준비가 되면 다른 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-157">When you're ready, let's deploy another template.</span></span>

<a id="Build"></a> 

## <a name="step-3-deploy-the-document-account-and-web-app-sample"></a><span data-ttu-id="4cd75-158">3단계: 문서 계정 및 웹앱 샘플 배포</span><span class="sxs-lookup"><span data-stu-id="4cd75-158">Step 3: Deploy the Document account and web app sample</span></span>
<span data-ttu-id="4cd75-159">이제 두 번째 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-159">Now let's deploy our second template.</span></span>  <span data-ttu-id="4cd75-160">이 템플릿은 계정 끝점 및 마스터 키와 같은 Azure Cosmos DB 연결 정보를 응용 프로그램 설정 또는 사용자 지정 연결 문자열로 웹앱에 주입하는 방법을 보여 주는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-160">This template is useful to show how you can inject Azure Cosmos DB connection information such as account endpoint and master key into a web app as application settings or as a custom connection string.</span></span> <span data-ttu-id="4cd75-161">예를 들어 Azure Cosmos DB 계정을 사용하여 배포하는 웹 응용 프로그램이 있어서 배포하는 동안 연결 정보가 자동으로 채워졌을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-161">For example, perhaps you have your own web application that you would like to deploy with an Azure Cosmos DB account and have the connection information automatically populated during deployment.</span></span>

> [!TIP]
> <span data-ttu-id="4cd75-162">템플릿은 아래에 입력된 웹앱 이름과 Azure Cosmos DB 계정 이름이 a) 유효한지, b) 사용 가능한지를 확인하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-162">The template does not validate that the web app name and Azure Cosmos DB account name entered below are a) valid and b) available.</span></span>  <span data-ttu-id="4cd75-163">배포를 제출하기 전에 지정하려는 이름의 가용성을 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-163">It is highly recommended that you verify the availability of the names you plan to supply prior to submitting the deployment.</span></span>
> 
> 

1. <span data-ttu-id="4cd75-164">[Azure 포털](https://portal.azure.com)에서 새로 만들기를 클릭하고 "템플릿 배포"를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-164">In the [Azure Portal](https://portal.azure.com), click New and search for "Template deployment".</span></span>
    <span data-ttu-id="4cd75-165">![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment1.png)</span><span class="sxs-lookup"><span data-stu-id="4cd75-165">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment1.png)</span></span>
2. <span data-ttu-id="4cd75-166">템플릿 배포 항목을 선택하고 **만들기** ![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment2.png)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-166">Select the Template deployment item and click **Create** ![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment2.png)</span></span>
3. <span data-ttu-id="4cd75-167">**템플릿 편집**을 클릭하고 DocDBWebSite.json 템플릿 파일의 내용을 붙여 넣고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-167">Click **Edit template**, paste the contents of the DocDBWebSite.json template file, and click **Save**.</span></span>
   <span data-ttu-id="4cd75-168">![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment3.png)</span><span class="sxs-lookup"><span data-stu-id="4cd75-168">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment3.png)</span></span>
4. <span data-ttu-id="4cd75-169">**매개 변수 편집**을 클릭하고 각 필수 매개 변수 값을 제공하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-169">Click **Edit parameters**, provide values for each of the mandatory parameters, and click **OK**.</span></span>  <span data-ttu-id="4cd75-170">매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-170">The parameters are as follows:</span></span>
   
   1. <span data-ttu-id="4cd75-171">SITENAME: 앱 서비스 웹앱 이름을 지정하고 웹앱에 액세스하는 데 사용할 URL을 만드는 데 사용됩니다(예: "mydemodocdbwebsite"를 지정할 경우 웹앱에 액세스하는 데 사용되는 URL은 mydemodocdbwebsite.azurewebsites.net이 됨).</span><span class="sxs-lookup"><span data-stu-id="4cd75-171">SITENAME: Specifies the App Service web app name and is used to construct the URL that you will use to access the web app (e.g. if you specify "mydemodocdbwebapp", then the URL by which you will access the web app will be mydemodocdbwebapp.azurewebsites.net).</span></span>
   2. <span data-ttu-id="4cd75-172">HOSTINGPLANNAME: 만들려는 앱 서비스 호스팅 계획의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-172">HOSTINGPLANNAME: Specifies the name of App Service hosting plan to create.</span></span>
   3. <span data-ttu-id="4cd75-173">LOCATION: Azure Cosmos DB 및 웹앱 리소스를 만들 Azure 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-173">LOCATION: Specifies the Azure location in which to create the Azure Cosmos DB and web app resources.</span></span>
   4. <span data-ttu-id="4cd75-174">DATABASEACCOUNTNAME: 만들 Azure Cosmos DB 계정의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-174">DATABASEACCOUNTNAME: Specifies the name of the Azure Cosmos DB account to create.</span></span>   
      
      ![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment4.png)
5. <span data-ttu-id="4cd75-176">기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만들도록 이름을 제공하며 리소스 그룹에 대한 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-176">Choose an existing Resource group or provide a name to make a new resource group, and choose a location for the resource group.</span></span>

    ![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment5.png)
6. <span data-ttu-id="4cd75-178">**약관 검토**, **구매**를 클릭한 다음 **만들기**를 클릭하여 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-178">Click **Review legal terms**, **Purchase**, and then click **Create** to begin the deployment.</span></span>  <span data-ttu-id="4cd75-179">**대시보드에 고정** 을 선택하여 결과 배포를 Azure 포털 홈 페이지에서 쉽게 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-179">Select **Pin to dashboard** so the resulting deployment is easily visible on your Azure portal home page.</span></span>
   <span data-ttu-id="4cd75-180">![템플릿 배포 UI의 스크린샷](./media/create-website/TemplateDeployment6.png)</span><span class="sxs-lookup"><span data-stu-id="4cd75-180">![Screenshot of the template deployment UI](./media/create-website/TemplateDeployment6.png)</span></span>
7. <span data-ttu-id="4cd75-181">배포가 완료되면 리소스 그룹 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-181">When the deployment finishes, the Resource group blade will open.</span></span>
   <span data-ttu-id="4cd75-182">![리소스 그룹 블레이드의 스크린샷](./media/create-website/TemplateDeployment7.png)</span><span class="sxs-lookup"><span data-stu-id="4cd75-182">![Screenshot of the resource group blade](./media/create-website/TemplateDeployment7.png)</span></span>  
8. <span data-ttu-id="4cd75-183">리소스 목록에서 웹앱 리소스를 클릭한 다음 **응용 프로그램 설정** ![리소스 그룹의 스크린샷](./media/create-website/TemplateDeployment9.png)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-183">Click the Web App resource in the Resources list and then click **Application settings** ![Screenshot of the resource group](./media/create-website/TemplateDeployment9.png)</span></span>  
9. <span data-ttu-id="4cd75-184">응용 프로그램 설정이 Azure Cosmos DB 끝점 및 각 Azure Cosmos DB 마스터 키에 대해 어떻게 제시되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-184">Note how there are application settings present for the Azure Cosmos DB endpoint and each of the Azure Cosmos DB master keys.</span></span>

    ![응용 프로그램 설정의 스크린샷](./media/create-website/TemplateDeployment10.png)  
10. <span data-ttu-id="4cd75-186">자유롭게 Azure Portal을 계속 탐색하거나 Azure Cosmos DB [샘플](http://go.microsoft.com/fwlink/?LinkID=402386) 중 하나에 따라 고유한 Azure Cosmos DB 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-186">Feel free to continue exploring the Azure Portal, or follow one of our Azure Cosmos DB [samples](http://go.microsoft.com/fwlink/?LinkID=402386) to create your own Azure Cosmos DB application.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="4cd75-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4cd75-187">Next steps</span></span>
<span data-ttu-id="4cd75-188">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-188">Congratulations!</span></span> <span data-ttu-id="4cd75-189">Azure Resource Manager 템플릿을 사용하여 Azure Cosmos DB, App Service 웹앱 및 샘플 웹 응용 프로그램을 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-189">You've deployed Azure Cosmos DB, App Service web app and a sample web application using Azure Resource Manager templates.</span></span>

* <span data-ttu-id="4cd75-190">Azure Cosmos DB에 대해 자세히 알아보려면 [여기](http://azure.com/docdb)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="4cd75-190">To learn more about Azure Cosmos DB, click [here](http://azure.com/docdb).</span></span>
* <span data-ttu-id="4cd75-191">Azure 앱 서비스 웹앱에 대해 자세히 알아보려면 [여기](http://go.microsoft.com/fwlink/?LinkId=325362)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="4cd75-191">To learn more about Azure App Service Web apps, click [here](http://go.microsoft.com/fwlink/?LinkId=325362).</span></span>
* <span data-ttu-id="4cd75-192">Azure 리소스 관리자 템플릿에 대해 자세히 알아보려면 [여기](https://msdn.microsoft.com/library/azure/dn790549.aspx)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="4cd75-192">To learn more about Azure Resource Manager templates, click [here](https://msdn.microsoft.com/library/azure/dn790549.aspx).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="4cd75-193">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="4cd75-193">What's changed</span></span>
* <span data-ttu-id="4cd75-194">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="4cd75-194">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
* <span data-ttu-id="4cd75-195">이전 포털에서 새 포털로의 변경에 대한 지침은 [Azure 클래식 포털 탐색에 대한 참조](http://go.microsoft.com/fwlink/?LinkId=529715)</span><span class="sxs-lookup"><span data-stu-id="4cd75-195">For a guide to the change of the old portal to the new portal see: [Reference for navigating the Azure Classic Portal](http://go.microsoft.com/fwlink/?LinkId=529715)</span></span>

> [!NOTE]
> <span data-ttu-id="4cd75-196">Azure 계정을 등록하기 전에 Azure 앱 서비스를 시작하려면 [App Service 체험](http://go.microsoft.com/fwlink/?LinkId=523751)으로 이동합니다. 앱 서비스에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-196">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](http://go.microsoft.com/fwlink/?LinkId=523751), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4cd75-197">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4cd75-197">No credit cards required; no commitments.</span></span>
> 
> 

