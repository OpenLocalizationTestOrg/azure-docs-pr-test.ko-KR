---
title: "Visual Studio에서 서버를 사용하지 않는 앱 빌드 | Microsoft Docs"
description: "Visual Studio에서 앱 만들기, 배포 및 관리에 대한 이 가이드를 사용하여 첫 번째 서버를 사용하지 않는 앱을 시작합니다."
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
ms.openlocfilehash: 3672beda8a502e5fe2c8182076a8edef7ee9ebf6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a><span data-ttu-id="71559-103">Logic Apps 및 함수를 사용하여 Visual Studio에서 서버를 사용하지 않는 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="71559-103">Build a serverless app in Visual Studio with Logic Apps and Functions</span></span>

<span data-ttu-id="71559-104">Azure에서 서버를 사용하지 않는 도구 및 기능은 클라우드 응용 프로그램의 신속한 개발 및 배포를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-104">Serverless tools and capabilities in Azure allow for rapid development and deployment of cloud applications.</span></span>  <span data-ttu-id="71559-105">이 문서는 Visual Studio에서 서버를 사용하지 않는 응용 프로그램 작성을 시작하는 방법에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="71559-105">This document focuses on how to get started in Visual Studio building a serverless application.</span></span>  <span data-ttu-id="71559-106">Azure에서 서버를 사용하지 않음 개요는 [이 문서에서 찾을 수 있습니다](logic-apps-serverless-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71559-106">An overview of serverless in Azure [can be found in this article](logic-apps-serverless-overview.md).</span></span>

## <a name="getting-everything-ready"></a><span data-ttu-id="71559-107">모든 항목 준비</span><span class="sxs-lookup"><span data-stu-id="71559-107">Getting everything ready</span></span>

<span data-ttu-id="71559-108">Visual Studio에서 서버를 사용하지 않는 응용 프로그램을 빌드하는 데 필요한 필수 구성 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-108">Here are the prerequisites needed to build a serverless application from Visual Studio:</span></span>

* <span data-ttu-id="71559-109">[Visual Studio 2017](https://www.visualstudio.com/vs/) 또는 Visual Studio 2015 - Community, Professional 또는 Enterprise</span><span class="sxs-lookup"><span data-stu-id="71559-109">[Visual Studio 2017](https://www.visualstudio.com/vs/) or Visual Studio 2015 - Community, Professional, or Enterprise</span></span>
* [<span data-ttu-id="71559-110">Visual Studio용 Logic Apps 도구</span><span class="sxs-lookup"><span data-stu-id="71559-110">Logic Apps Tools for Visual Studio</span></span>](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* <span data-ttu-id="71559-111">[최신 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 이상)</span><span class="sxs-lookup"><span data-stu-id="71559-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="71559-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="71559-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="71559-113">Functions를 로컬로 디버그할 [Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)</span><span class="sxs-lookup"><span data-stu-id="71559-113">[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools) to debug Functions locally</span></span>
* <span data-ttu-id="71559-114">포함된 논리 앱 디자이너를 사용하는 경우 웹에 대한 액세스</span><span class="sxs-lookup"><span data-stu-id="71559-114">Access to the web when using the embedded Logic App designer</span></span>

## <a name="getting-started-with-a-deployment-template"></a><span data-ttu-id="71559-115">배포 템플릿 시작</span><span class="sxs-lookup"><span data-stu-id="71559-115">Getting started with a deployment template</span></span>

<span data-ttu-id="71559-116">Azure의 리소스 관리는 리소스 그룹 내에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="71559-116">Managing resources in Azure are done within a resource group.</span></span>  <span data-ttu-id="71559-117">리소스 그룹은 리소스의 논리적 그룹화입니다.</span><span class="sxs-lookup"><span data-stu-id="71559-117">A resource group is a logical grouping of resources.</span></span>  <span data-ttu-id="71559-118">리소스 그룹은 리소스의 컬렉션의 배포 및 관리를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-118">Resource groups allow deployment and management of a collection of resources.</span></span>  <span data-ttu-id="71559-119">Azure에서 서버를 사용하지 않는 응용 프로그램의 경우 리소스 그룹에는 Azure Logic Apps 및 Azure Functions 모두가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-119">For a Serverless application in Azure, our resource group contains both Azure Logic Apps, and Azure Functions.</span></span>  <span data-ttu-id="71559-120">Visual Studio 내에서 리소스 그룹 프로젝트를 사용하여 단일 자산으로 전체 응용 프로그램을 개발, 관리 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-120">By using the Resource Group project within Visual Studio, we are able to develop, manage, and deploy the entire application as a single asset.</span></span>

### <a name="create-a-resource-group-project-in-visual-studio"></a><span data-ttu-id="71559-121">Visual Studio에서 리소스 그룹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="71559-121">Create a Resource Group project in Visual Studio</span></span>

1. <span data-ttu-id="71559-122">Visual Studio에서 클릭하여 **새 프로젝트**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-122">In Visual Studio, click to add a **New Project**</span></span>
1. <span data-ttu-id="71559-123">**클라우드** 범주에서 Azure **리소스 그룹** 프로젝트를 만들도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-123">In the **Cloud** category, select to create an Azure **Resource Group** project</span></span>  
 * <span data-ttu-id="71559-124">나열된 범주 또는 프로젝트가 표시되지 않는 경우 Visual Studio용 Azure SDK가 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-124">If you do not see the category or project listed, be sure you have the Azure SDK installed for Visual Studio</span></span>
1. <span data-ttu-id="71559-125">프로젝트에 이름 및 위치를 지정하고 **확인**을 선택하여 템플릿을 선택하라는 메시지를 표시하는 Visual Studio를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71559-125">Give the project a name and location, and select **Ok** to create Visual Studio prompts to select a template.</span></span>  <span data-ttu-id="71559-126">빈 값, 논리 앱 또는 다른 리소스로 시작하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-126">You could select to start from Blank, start with a Logic App or other resource.</span></span>  <span data-ttu-id="71559-127">그러나 이 경우 Azure 빠른 시작 템플릿을 사용하여 서버를 사용하지 않는 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-127">However, in this case we use an Azure Quickstart Template to get us started with a serverless app.</span></span>
1. <span data-ttu-id="71559-128">서식 파일을 표시 하려면 선택 **Azure 빠른 시작** ![Azure 빠른 시작을 선택 하면 템플릿][1]</span><span class="sxs-lookup"><span data-stu-id="71559-128">Select to show templates from **Azure Quickstart** ![Selecting Azure Quickstart templates][1]</span></span>
1. <span data-ttu-id="71559-129">서버를 사용하지 않는 빠른 시작 템플릿(**101-logic-app-and-function-app**)을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-129">Select the serverless quickstart template: **101-logic-app-and-function-app** and click **Ok**</span></span>

<span data-ttu-id="71559-130">빠른 시작 템플릿은 리소스 그룹 프로젝트에서 배포 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71559-130">The quickstart template creates a deployment template in your resource group project.</span></span>  <span data-ttu-id="71559-131">템플릿은 Azure Functions를 호출하는 간단한 논리 앱을 포함하고 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-131">The template contains a simple Logic App that calls an Azure Functions, and returns the result.</span></span>  <span data-ttu-id="71559-132">솔루션 탐색기에서 `azuredeploy.json` 파일을 여는 경우 서버를 사용하지 않는 앱에 대한 리소스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-132">If you open the `azuredeploy.json` file in the Solution Explorer, you can see the resources for the serverless app.</span></span>

## <a name="deploying-the-serverless-application"></a><span data-ttu-id="71559-133">서버를 사용하지 않는 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="71559-133">Deploying the serverless application</span></span>

<span data-ttu-id="71559-134">Visual Studio에서 논리 앱 비주얼 디자이너를 열려면 미리 배포된 Azure 리소스 그룹이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-134">Before you can open the Logic App visual designer in Visual Studio, there needs to be a pre-deployed Azure Resource Group.</span></span>  <span data-ttu-id="71559-135">이렇게 하면 디자이너는 논리 앱에 리소스에 대한 연결 및 서비스를 만들고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-135">This allows the designer to create and use connections to resources and services in the logic app.</span></span>  <span data-ttu-id="71559-136">시작하려면 단순히 만든 솔루션을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-136">To get started, we simply need to deploy the solution created.</span></span>

1. <span data-ttu-id="71559-137">선택, Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭 **배포**, 만들고는 **새로 만들기** 배포 ![새 리소스 배포를 선택 합니다.][2]</span><span class="sxs-lookup"><span data-stu-id="71559-137">Right-click the project in Visual Studio, select **Deploy**, and create a **New** deployment  ![Selecting new resource deployment][2]</span></span>
1. <span data-ttu-id="71559-138">유효한 Azure 구독 및 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-138">Select a valid Azure subscription and Resource group</span></span>
1. <span data-ttu-id="71559-139">솔루션을 **배포**하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-139">Select to **Deploy** the solution</span></span>
1. <span data-ttu-id="71559-140">논리 앱과 Azure 함수 앱의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-140">Enter in the name for the Logic App and the Azure Function App.</span></span>  <span data-ttu-id="71559-141">Azure 함수 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-141">The Azure Function name does need to be globally unique</span></span>

<span data-ttu-id="71559-142">서버를 사용하지 않는 솔루션이 지정된 리소스 그룹으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="71559-142">The serverless solution deploys into the specified resource group.</span></span>  <span data-ttu-id="71559-143">Visual Studio에서 **출력**을 보면 배포의 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-143">If you look at the **Output** in Visual Studio you can see the status of the deployment.</span></span>

## <a name="editing-the-logic-app-in-visual-studio"></a><span data-ttu-id="71559-144">Visual Studio에서 논리 앱 편집</span><span class="sxs-lookup"><span data-stu-id="71559-144">Editing the logic app in Visual Studio</span></span>

<span data-ttu-id="71559-145">솔루션을 모든 리소스 그룹에 배포한 후 비주얼 디자이너를 사용하여 논리 앱을 편집하고 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-145">Once the solution has been deployed into any resource group, the visual designer can be used to edit and make changes to the logic app.</span></span>

1. <span data-ttu-id="71559-146">솔루션 탐색기에서 `azuredeploy.json` 파일을 마우스 오른쪽 단추로 클릭하고 **논리 앱 디자이너로 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-146">Right-click the `azuredeploy.json` file in the Solution Explorer and select **Open With Logic Apps Designer**</span></span>
1. <span data-ttu-id="71559-147">솔루션이 배포된 **리소스 그룹** 및 **위치**를 선택하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-147">Select the **Resource Group** and **Location** the solution has been deployed to and select **OK**</span></span>

<span data-ttu-id="71559-148">이제 논리 앱 비주얼 디자이너가 Visual Studio와 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="71559-148">The Logic App visual designer should now be visible with Visual Studio.</span></span>  <span data-ttu-id="71559-149">단계 추가, 워크플로 수정 및 변경 내용 저장을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-149">You can continue to add steps, modify the workflow, and save changes.</span></span>  <span data-ttu-id="71559-150">또한 Visual Studio에서 논리 앱을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-150">You can also create logic apps from Visual Studio.</span></span>  <span data-ttu-id="71559-151">템플릿 탐색기에서 **리소스**를 마우스 오른쪽 단추로 클릭하면 **논리 앱**을 프로젝트에 추가하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-151">If you right-click the **Resources** in the template navigator, you can choose to add a **Logic App** to the project.</span></span>  <span data-ttu-id="71559-152">빈 논리 앱이 리소스 그룹으로 미리 배포 없이 비주얼 디자이너에 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="71559-152">Empty logic apps load in the visual designer without a pre-deploy into a resource group.</span></span>

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a><span data-ttu-id="71559-153">배포된 논리 앱에 대한 실행 기록 관리 및 보기</span><span class="sxs-lookup"><span data-stu-id="71559-153">Managing and viewing run history for a deployed logic app</span></span>

<span data-ttu-id="71559-154">Azure에 배포된 논리 앱에 대한 실행 기록을 관리하고 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-154">You can also manage and view the run history for logic apps deployed in Azure.</span></span>  <span data-ttu-id="71559-155">Visual Studio에서 **클라우드 탐색기** 도구를 여는 경우 논리 앱을 마우스 오른쪽 단추로 클릭하고 속성 편집, 비활성화, 보기 또는 실행 기록 보기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-155">If you open the **Cloud Explorer** tool in Visual Studio, you can right-click any Logic App and choose to edit, disable, view properties, or view run history.</span></span>  <span data-ttu-id="71559-156">또한 편집을 클릭하면 Visual Studio 리소스 그룹 프로젝트에 게시된 논리 앱을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-156">Clicking edit also allows you to download a published logic app into a Visual Studio Resource Group project.</span></span>  <span data-ttu-id="71559-157">즉, Azure Portal에서 논리 앱 빌드를 시작한 경우에도 여전히 가져와서 Visual Studio에서 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-157">This means that even if you started building your logic app in the Azure portal, you can still import it and manage it from Visual Studio.</span></span>

## <a name="developing-an-azure-function-in-visual-studio"></a><span data-ttu-id="71559-158">Visual Studio에서 Azure 함수 개발</span><span class="sxs-lookup"><span data-stu-id="71559-158">Developing an Azure Function in Visual Studio</span></span>

<span data-ttu-id="71559-159">배포 템플릿은 `azuredeploy.json` 변수 배포에 지정된 git 리포지토리에 대한 솔루션에 포함된 모든 Azure Functions를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-159">The deployment template deploys any Azure Functions that are contained in the solution for the git repository specified in the `azuredeploy.json` variables.</span></span>  <span data-ttu-id="71559-160">솔루션 내에서 함수 프로젝트를 작성하고 원본 제어(GitHub, Visual Studio Team Services 등)로 확인하고 `repo` 변수를 업데이트하는 경우 템플릿은 Azure 함수를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="71559-160">If you author a function project within the solution, check it into source control (GitHub, Visual Studio Team Services, etc.), and update the `repo` variable, the template will deploy the Azure Function.</span></span>

### <a name="creating-an-azure-function-project"></a><span data-ttu-id="71559-161">Azure 함수 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="71559-161">Creating an Azure Function project</span></span>

<span data-ttu-id="71559-162">JavaScript, Python, F #, Bash, Batch 또는 PowerShell을 사용하는 경우 [함수 CLI의 단계](../azure-functions/functions-run-local.md)를 따라 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71559-162">If using JavaScript, Python, F#, Bash, Batch, or PowerShell, follow the [steps in the Functions CLI](../azure-functions/functions-run-local.md) to create a project.</span></span>  <span data-ttu-id="71559-163">C#에서 함수를 개발하는 경우 Azure 함수에 대한 현재 솔루션에서 [C# 클래스 라이브러리](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71559-163">If developing a function in C#, you can use a [C# class library](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) in the current solution for the Azure Function.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71559-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71559-164">Next steps</span></span>

* [<span data-ttu-id="71559-165">서버를 사용하지 않는 소셜 대시보드를 빌드하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="71559-165">Learn how to build a serverless social dashboard</span></span>](logic-apps-scenario-social-serverless.md)
* [<span data-ttu-id="71559-166">Visual Studio 클라우드 탐색기에서 논리 앱 관리</span><span class="sxs-lookup"><span data-stu-id="71559-166">Manage a logic app from Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="71559-167">논리 앱 워크플로 정의 언어</span><span class="sxs-lookup"><span data-stu-id="71559-167">Logic App workflow definition language</span></span>](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
