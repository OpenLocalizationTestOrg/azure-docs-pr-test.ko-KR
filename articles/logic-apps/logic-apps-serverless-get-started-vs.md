---
title: "Visual Studio에서 서버가 없는 앱 aaaBuild | Microsoft Docs"
description: "첫 번째 서버가 없는 응용 프로그램을 작성, 배포, 및 Visual Studio에서 hello 앱 관리에이 가이드를 시작 하세요."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a><span data-ttu-id="448f6-103">Logic Apps 및 함수를 사용하여 Visual Studio에서 서버를 사용하지 않는 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="448f6-103">Build a serverless app in Visual Studio with Logic Apps and Functions</span></span>

<span data-ttu-id="448f6-104">Azure에서 서버를 사용하지 않는 도구 및 기능은 클라우드 응용 프로그램의 신속한 개발 및 배포를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-104">Serverless tools and capabilities in Azure allow for rapid development and deployment of cloud applications.</span></span>  <span data-ttu-id="448f6-105">이 문서는 방법에 중점을 두고 tooget 서버가 없는 응용 프로그램을 작성 하는 Visual Studio에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-105">This document focuses on how tooget started in Visual Studio building a serverless application.</span></span>  <span data-ttu-id="448f6-106">Azure에서 서버를 사용하지 않음 개요는 [이 문서에서 찾을 수 있습니다](logic-apps-serverless-overview.md).</span><span class="sxs-lookup"><span data-stu-id="448f6-106">An overview of serverless in Azure [can be found in this article](logic-apps-serverless-overview.md).</span></span>

## <a name="getting-everything-ready"></a><span data-ttu-id="448f6-107">모든 항목 준비</span><span class="sxs-lookup"><span data-stu-id="448f6-107">Getting everything ready</span></span>

<span data-ttu-id="448f6-108">Visual Studio에서 서버가 없는 응용 hello 필요한 필수 구성 요소 toobuild 키를 같습니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-108">Here are hello prerequisites needed toobuild a serverless application from Visual Studio:</span></span>

* <span data-ttu-id="448f6-109">[Visual Studio 2017](https://www.visualstudio.com/vs/) 또는 Visual Studio 2015 - Community, Professional 또는 Enterprise</span><span class="sxs-lookup"><span data-stu-id="448f6-109">[Visual Studio 2017](https://www.visualstudio.com/vs/) or Visual Studio 2015 - Community, Professional, or Enterprise</span></span>
* [<span data-ttu-id="448f6-110">Visual Studio용 Logic Apps 도구</span><span class="sxs-lookup"><span data-stu-id="448f6-110">Logic Apps Tools for Visual Studio</span></span>](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* <span data-ttu-id="448f6-111">[최신 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 이상)</span><span class="sxs-lookup"><span data-stu-id="448f6-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="448f6-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="448f6-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="448f6-113">[Azure 함수 핵심 도구](https://www.npmjs.com/package/azure-functions-core-tools) toodebug 로컬로 함수</span><span class="sxs-lookup"><span data-stu-id="448f6-113">[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools) toodebug Functions locally</span></span>
* <span data-ttu-id="448f6-114">Hello를 사용 하는 경우 액세스 toohello 웹 포함 논리 응용 프로그램 디자이너</span><span class="sxs-lookup"><span data-stu-id="448f6-114">Access toohello web when using hello embedded Logic App designer</span></span>

## <a name="getting-started-with-a-deployment-template"></a><span data-ttu-id="448f6-115">배포 템플릿 시작</span><span class="sxs-lookup"><span data-stu-id="448f6-115">Getting started with a deployment template</span></span>

<span data-ttu-id="448f6-116">Azure의 리소스 관리는 리소스 그룹 내에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-116">Managing resources in Azure are done within a resource group.</span></span>  <span data-ttu-id="448f6-117">리소스 그룹은 리소스의 논리적 그룹화입니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-117">A resource group is a logical grouping of resources.</span></span>  <span data-ttu-id="448f6-118">리소스 그룹은 리소스의 컬렉션의 배포 및 관리를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-118">Resource groups allow deployment and management of a collection of resources.</span></span>  <span data-ttu-id="448f6-119">Azure에서 서버를 사용하지 않는 응용 프로그램의 경우 리소스 그룹에는 Azure Logic Apps 및 Azure Functions 모두가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-119">For a Serverless application in Azure, our resource group contains both Azure Logic Apps, and Azure Functions.</span></span>  <span data-ttu-id="448f6-120">Visual Studio 내에서 리소스 그룹 프로젝트 hello를 사용 하 여 수 toodevelop 하는, 관리 및 단일 자산으로 hello 전체 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-120">By using hello Resource Group project within Visual Studio, we are able toodevelop, manage, and deploy hello entire application as a single asset.</span></span>

### <a name="create-a-resource-group-project-in-visual-studio"></a><span data-ttu-id="448f6-121">Visual Studio에서 리소스 그룹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="448f6-121">Create a Resource Group project in Visual Studio</span></span>

1. <span data-ttu-id="448f6-122">Visual Studio에서 tooadd 클릭는 **새 프로젝트**</span><span class="sxs-lookup"><span data-stu-id="448f6-122">In Visual Studio, click tooadd a **New Project**</span></span>
1. <span data-ttu-id="448f6-123">Hello에 **클라우드** 범주를 선택 toocreate Azure **리소스 그룹** 프로젝트</span><span class="sxs-lookup"><span data-stu-id="448f6-123">In hello **Cloud** category, select toocreate an Azure **Resource Group** project</span></span>  
 * <span data-ttu-id="448f6-124">Hello 범주 또는 나열 된 프로젝트 표시 되지 않으면 되어 있는지 확인 hello Azure SDK for Visual Studio 설치</span><span class="sxs-lookup"><span data-stu-id="448f6-124">If you do not see hello category or project listed, be sure you have hello Azure SDK installed for Visual Studio</span></span>
1. <span data-ttu-id="448f6-125">이름 및 위치를 hello 프로젝트를 지정 하 고 선택 **확인** toocreate Visual Studio 템플릿을 tooselect 라는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-125">Give hello project a name and location, and select **Ok** toocreate Visual Studio prompts tooselect a template.</span></span>  <span data-ttu-id="448f6-126">공백, 논리 앱 시작 또는 다른 리소스에서 toostart를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-126">You could select toostart from Blank, start with a Logic App or other resource.</span></span>  <span data-ttu-id="448f6-127">그러나이 경우 사용 서버가 없는 앱 시작 우리는 Azure 빠른 시작 템플릿 tooget 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-127">However, in this case we use an Azure Quickstart Template tooget us started with a serverless app.</span></span>
1. <span data-ttu-id="448f6-128">tooshow 템플릿을 선택 **Azure 빠른 시작** ![Azure 빠른 시작을 선택 하면 템플릿][1]</span><span class="sxs-lookup"><span data-stu-id="448f6-128">Select tooshow templates from **Azure Quickstart** ![Selecting Azure Quickstart templates][1]</span></span>
1. <span data-ttu-id="448f6-129">서버 빠른 시작 템플릿 선택 hello: **101-logic-app-and-function-app** 클릭 **확인**</span><span class="sxs-lookup"><span data-stu-id="448f6-129">Select hello serverless quickstart template: **101-logic-app-and-function-app** and click **Ok**</span></span>

<span data-ttu-id="448f6-130">hello 퀵 스타트 템플릿은 리소스 그룹 프로젝트의 배포 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-130">hello quickstart template creates a deployment template in your resource group project.</span></span>  <span data-ttu-id="448f6-131">hello 템플릿은 Azure 함수를 호출 하 고 hello 결과 반환 하는 간단한 논리 앱을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-131">hello template contains a simple Logic App that calls an Azure Functions, and returns hello result.</span></span>  <span data-ttu-id="448f6-132">Hello를 열면 `azuredeploy.json` 파일에 hello 솔루션 탐색기, hello 서버가 없는 응용 프로그램에 대 한 hello 리소스를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-132">If you open hello `azuredeploy.json` file in hello Solution Explorer, you can see hello resources for hello serverless app.</span></span>

## <a name="deploying-hello-serverless-application"></a><span data-ttu-id="448f6-133">Hello 서버가 없는 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="448f6-133">Deploying hello serverless application</span></span>

<span data-ttu-id="448f6-134">Visual Studio에서 hello 논리 앱에 대 한 비주얼 디자이너를 열 수 있습니다, 전에 미리 배포할된 Azure 리소스 그룹 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-134">Before you can open hello Logic App visual designer in Visual Studio, there needs toobe a pre-deployed Azure Resource Group.</span></span>  <span data-ttu-id="448f6-135">그러면 디자이너 toocreate hello 및 사용 하 여 연결 tooresources 및 서비스를 hello 논리 앱 있습니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-135">This allows hello designer toocreate and use connections tooresources and services in hello logic app.</span></span>  <span data-ttu-id="448f6-136">시작 tooget, 단순히 필요 toodeploy hello 솔루션을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-136">tooget started, we simply need toodeploy hello solution created.</span></span>

1. <span data-ttu-id="448f6-137">Visual studio에서는 선택 hello 프로젝트를 마우스 오른쪽 단추로 클릭 **배포**, 만들고는 **새로** 배포 ![새 리소스 배포를 선택 하면][2]</span><span class="sxs-lookup"><span data-stu-id="448f6-137">Right-click hello project in Visual Studio, select **Deploy**, and create a **New** deployment  ![Selecting new resource deployment][2]</span></span>
1. <span data-ttu-id="448f6-138">유효한 Azure 구독 및 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-138">Select a valid Azure subscription and Resource group</span></span>
1. <span data-ttu-id="448f6-139">너무 선택**배포** hello 솔루션</span><span class="sxs-lookup"><span data-stu-id="448f6-139">Select too**Deploy** hello solution</span></span>
1. <span data-ttu-id="448f6-140">논리 앱 hello에 대 한 hello 이름과 hello Azure 함수 앱에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-140">Enter in hello name for hello Logic App and hello Azure Function App.</span></span>  <span data-ttu-id="448f6-141">hello Azure 함수 이름은 필요 toobe 전역적으로 고유</span><span class="sxs-lookup"><span data-stu-id="448f6-141">hello Azure Function name does need toobe globally unique</span></span>

<span data-ttu-id="448f6-142">hello 서버가 없는 솔루션 hello 지정 된 리소스 그룹으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-142">hello serverless solution deploys into hello specified resource group.</span></span>  <span data-ttu-id="448f6-143">Hello 보면 **출력** Visual Studio에서 hello 배포의 hello 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-143">If you look at hello **Output** in Visual Studio you can see hello status of hello deployment.</span></span>

## <a name="editing-hello-logic-app-in-visual-studio"></a><span data-ttu-id="448f6-144">Visual Studio에서 편집 hello 논리 앱</span><span class="sxs-lookup"><span data-stu-id="448f6-144">Editing hello logic app in Visual Studio</span></span>

<span data-ttu-id="448f6-145">모든 리소스 그룹에 배포 된 hello 솔루션, hello 비주얼 디자이너 사용된 tooedit 수 있으며 변경 내용을 toohello 논리 앱 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-145">Once hello solution has been deployed into any resource group, hello visual designer can be used tooedit and make changes toohello logic app.</span></span>

1. <span data-ttu-id="448f6-146">마우스 오른쪽 단추로 클릭 hello `azuredeploy.json` hello 솔루션 탐색기에서에서 파일을 선택 **와 논리 앱 디자이너 열기**</span><span class="sxs-lookup"><span data-stu-id="448f6-146">Right-click hello `azuredeploy.json` file in hello Solution Explorer and select **Open With Logic Apps Designer**</span></span>
1. <span data-ttu-id="448f6-147">선택 hello **리소스 그룹** 및 **위치** hello 솔루션 되었습니다 tooand 선택 배포 **확인**</span><span class="sxs-lookup"><span data-stu-id="448f6-147">Select hello **Resource Group** and **Location** hello solution has been deployed tooand select **OK**</span></span>

<span data-ttu-id="448f6-148">hello 논리 앱에 대 한 비주얼 디자이너 이제 Visual Studio와 함께 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-148">hello Logic App visual designer should now be visible with Visual Studio.</span></span>  <span data-ttu-id="448f6-149">Tooadd 단계를 계속 지정, hello 워크플로 수정 및 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-149">You can continue tooadd steps, modify hello workflow, and save changes.</span></span>  <span data-ttu-id="448f6-150">또한 Visual Studio에서 논리 앱을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-150">You can also create logic apps from Visual Studio.</span></span>  <span data-ttu-id="448f6-151">Hello를 마우스 오른쪽 단추로 클릭 하는 경우 **리소스** tooadd hello 템플릿 탐색기에서 선택할 수 있습니다는 **논리 앱** toohello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="448f6-151">If you right-click hello **Resources** in hello template navigator, you can choose tooadd a **Logic App** toohello project.</span></span>  <span data-ttu-id="448f6-152">빈 논리 앱을 로드 하지 않고 hello 비주얼 디자이너는 미리 리소스 그룹으로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-152">Empty logic apps load in hello visual designer without a pre-deploy into a resource group.</span></span>

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a><span data-ttu-id="448f6-153">배포된 논리 앱에 대한 실행 기록 관리 및 보기</span><span class="sxs-lookup"><span data-stu-id="448f6-153">Managing and viewing run history for a deployed logic app</span></span>

<span data-ttu-id="448f6-154">또한 관리 하 고 Azure에 배포 된 논리 앱에 대 한 hello 실행 기록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-154">You can also manage and view hello run history for logic apps deployed in Azure.</span></span>  <span data-ttu-id="448f6-155">Hello를 열면 **클라우드 탐색기** 도구 실행 기록 보기 또는 Visual Studio, 모든 논리 앱을 마우스 오른쪽 단추로 클릭 하 고 수 tooedit, 사용 안 함, 속성 보기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-155">If you open hello **Cloud Explorer** tool in Visual Studio, you can right-click any Logic App and choose tooedit, disable, view properties, or view run history.</span></span>  <span data-ttu-id="448f6-156">편집을 클릭 하면 수도 있습니다를 Visual Studio 리소스 그룹 프로젝트에 게시 된 논리 앱 toodownload를.</span><span class="sxs-lookup"><span data-stu-id="448f6-156">Clicking edit also allows you toodownload a published logic app into a Visual Studio Resource Group project.</span></span>  <span data-ttu-id="448f6-157">즉, Azure 포털 hello 사용 하 여 논리 앱 빌드를 시작 하는 경우에 수 여전히 가져와야 하는 Visual Studio에서 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-157">This means that even if you started building your logic app in hello Azure portal, you can still import it and manage it from Visual Studio.</span></span>

## <a name="developing-an-azure-function-in-visual-studio"></a><span data-ttu-id="448f6-158">Visual Studio에서 Azure 함수 개발</span><span class="sxs-lookup"><span data-stu-id="448f6-158">Developing an Azure Function in Visual Studio</span></span>

<span data-ttu-id="448f6-159">hello 배포 템플릿 배포 hello에 지정 된 hello git 리포지토리에 대 한 hello 솔루션에 포함 된 모든 Azure 함수 `azuredeploy.json` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-159">hello deployment template deploys any Azure Functions that are contained in hello solution for hello git repository specified in hello `azuredeploy.json` variables.</span></span>  <span data-ttu-id="448f6-160">Hello 솔루션 내에 함수 개체를 작성 하는 경우 소스 제어 (GitHub, Visual Studio Team Services 등)로 확인 하 고 hello 업데이트 `repo` 변수인 hello 템플릿 배포 hello Azure 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-160">If you author a function project within hello solution, check it into source control (GitHub, Visual Studio Team Services, etc.), and update hello `repo` variable, hello template will deploy hello Azure Function.</span></span>

### <a name="creating-an-azure-function-project"></a><span data-ttu-id="448f6-161">Azure 함수 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="448f6-161">Creating an Azure Function project</span></span>

<span data-ttu-id="448f6-162">JavaScript, Python, F #, Bash, 일괄 처리 또는 PowerShell을 사용 하 여 hello 수행 [hello 함수 CLI의에서 단계를](../azure-functions/functions-run-local.md) toocreate 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-162">If using JavaScript, Python, F#, Bash, Batch, or PowerShell, follow hello [steps in hello Functions CLI](../azure-functions/functions-run-local.md) toocreate a project.</span></span>  <span data-ttu-id="448f6-163">C#의 기능을 개발 하는 경우 사용할 수 있습니다는 [C# 클래스 라이브러리](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) hello Azure 함수 hello에 대 한 현재 솔루션의 합니다.</span><span class="sxs-lookup"><span data-stu-id="448f6-163">If developing a function in C#, you can use a [C# class library](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) in hello current solution for hello Azure Function.</span></span>

## <a name="next-steps"></a><span data-ttu-id="448f6-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="448f6-164">Next steps</span></span>

* [<span data-ttu-id="448f6-165">자세한 내용은 방법 toobuild 서버가 없는 소셜 대시보드</span><span class="sxs-lookup"><span data-stu-id="448f6-165">Learn how toobuild a serverless social dashboard</span></span>](logic-apps-scenario-social-serverless.md)
* [<span data-ttu-id="448f6-166">Visual Studio 클라우드 탐색기에서 논리 앱 관리</span><span class="sxs-lookup"><span data-stu-id="448f6-166">Manage a logic app from Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="448f6-167">논리 앱 워크플로 정의 언어</span><span class="sxs-lookup"><span data-stu-id="448f6-167">Logic App workflow definition language</span></span>](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
