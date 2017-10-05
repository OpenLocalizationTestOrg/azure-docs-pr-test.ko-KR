---
title: "Visual Studio에서 Logic Apps 만들기, 빌드 및 배포 - Azure Logic Apps | Microsoft Docs"
description: "Azure Logic Apps를 디자인, 빌드 및 배포할 수 있도록 Visual Studio 프로젝트를 만듭니다."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: e7f5cf483d22e4c60dedbe5176ceb0bc8b2b6e66
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="034c8-103">Visual Studio에서 Azure Logic Apps 디자인, 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="034c8-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="034c8-104">[Azure Portal](https://portal.azure.com/)에서 Azure Logic Apps를 만들고 관리할 수 있는 좋은 방법을 제공하지만 Logic Apps를 디자인, 빌드 및 배포하기 위해 Visual Studio를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to create and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="034c8-105">Visual Studio는 Logic Apps Designer와 같이 논리 앱을 빌드하는 풍부한 도구를 제공하고, 배포 및 자동화 템플릿을 구성하고, 모든 환경에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-105">Visual Studio provides rich tools like the Logic App Designer for you to create logic apps, configure deployment and automation templates, and deploy to any environment.</span></span> 

<span data-ttu-id="034c8-106">Azure Logic Apps을 시작하려면 [Azure Portal에서 첫 번째 논리 앱을 만드는 방법](logic-apps-create-a-logic-app.md)을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="034c8-106">To get started with Azure Logic Apps, learn [how to create your first logic app in the Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="034c8-107">설치 단계</span><span class="sxs-lookup"><span data-stu-id="034c8-107">Installation steps</span></span>

<span data-ttu-id="034c8-108">Azure Logic Apps용 Visual Studio 도구를 설치하고 구성하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="034c8-108">To install and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="034c8-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="034c8-109">Prerequisites</span></span>

* <span data-ttu-id="034c8-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) 또는 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="034c8-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="034c8-111">[최신 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 이상)</span><span class="sxs-lookup"><span data-stu-id="034c8-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="034c8-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="034c8-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="034c8-113">포함된 디자이너를 사용하는 경우 웹에 대한 액세스</span><span class="sxs-lookup"><span data-stu-id="034c8-113">Access to the web when using the embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="034c8-114">Azure Logic Apps용 Visual Studio 도구 설치</span><span class="sxs-lookup"><span data-stu-id="034c8-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="034c8-115">필수 구성 요소를 설치한 후에:</span><span class="sxs-lookup"><span data-stu-id="034c8-115">After you install the prerequisites:</span></span>

1. <span data-ttu-id="034c8-116">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-116">Open Visual Studio.</span></span> <span data-ttu-id="034c8-117">**도구** 메뉴에서 **확장 및 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-117">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="034c8-118">온라인을 검색할 수 있도록 **온라인** 범주를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-118">Expand the **Online** category so you can search online.</span></span>
3. <span data-ttu-id="034c8-119">**Visual Studio용 Azure Logic Apps 도구**를 찾을 때까지 **Logic Apps**을 찾아보거나 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="034c8-120">확장을 다운로드하고 설치하려면 **다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-120">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="034c8-121">설치 후 Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="034c8-122">Visual Studio Marketplace에서 직접 [Visual Studio 2017용 Azure Logic Apps 도구](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) 및 [Visual Studio 2015용 Azure Logic Apps 도구](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio)를 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and the [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from the Visual Studio Marketplace.</span></span>

<span data-ttu-id="034c8-123">설치를 완료한 후에 Logic App Designer에서 Azure 리소스 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-123">After you finish installation, you can use the Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="034c8-124">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="034c8-124">Create your project</span></span>

1. <span data-ttu-id="034c8-125">**파일** 메뉴에서 **새로 만들기**로 이동하고 **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-125">On the **File** menu, go to **New**, and select **Project**.</span></span> <span data-ttu-id="034c8-126">또는 기존 솔루션에 프로젝트를 추가하려면 **추가**로 이동하고 **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-126">Or to add your project to an existing solution, go to **Add**, and select **New Project**.</span></span>

    ![파일 메뉴](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="034c8-128">**새 프로젝트** 창에서 **클라우드**를 찾고 **Azure 리소스 그룹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-128">In the **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="034c8-129">프로젝트 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-129">Name your project, and click **OK**.</span></span>

    ![새 프로젝트 추가](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="034c8-131">**Logic App** 템플릿을 선택하면 사용자가 사용할 빈 논리 앱 배포 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-131">Select the **Logic App** template, which creates a blank logic app deployment template for you to use.</span></span> <span data-ttu-id="034c8-132">템플릿을 선택한 후에 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-132">After you select your template, click **OK**.</span></span>

    ![Logic App 템플릿 선택](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="034c8-134">이제 논리 앱 프로젝트가 솔루션에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-134">You've now added your logic app project to your solution.</span></span> 
    <span data-ttu-id="034c8-135">솔루션 탐색기에서 배포 파일이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-135">In the Solution Explorer, your deployment file should appear.</span></span>

    ![배포 파일](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="034c8-137">Logic App Designer에서 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="034c8-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="034c8-138">Logic App이 포함된 Azure 리소스 그룹 프로젝트가 있는 경우 Visual Studio에서 Logic App Designer를 열어 워크플로를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-138">When you have an Azure Resource Group project that contains a logic app, you can open the Logic App Designer in Visual Studio to create your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="034c8-139">사용 가능한 속성 및 데이터에 대한 커넥터를 쿼리하기 위해 디자이너가 인터넷에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-139">The designer requires an internet connection to query connectors for available properties and data.</span></span> <span data-ttu-id="034c8-140">예를 들어, Dynamics CRM Online 커넥터를 사용하는 경우 디자이너는 사용 가능한 사용자 지정 및 기본 속성을 표시하기 위해 CRM 인스턴스를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-140">For example, if you use the Dynamics CRM Online connector, the designer queries your CRM instance to show available custom and default properties.</span></span>

1. <span data-ttu-id="034c8-141">`<template>.json` 파일을 마우스 오른쪽 단추로 클릭하고 **Logic App Designer로 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="034c8-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="034c8-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="034c8-143">Azure 구독, 리소스 그룹 및 배포 템플릿의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="034c8-144">논리 앱을 디자인하면 디자인하는 동안 속성을 쿼리하는 API 연결 리소스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="034c8-145">Visual Studio에서는 디자인하는 동안 선택한 리소스 그룹을 사용하여 해당 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-145">Visual Studio uses your selected resource group to create those connections during design time.</span></span> <span data-ttu-id="034c8-146">API 연결을 보거나 변경하려면 Azure Portal로 이동하고 **API 연결**을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-146">To view or change any API Connections, go to the Azure portal, and browse for **API Connections**.</span></span>

    ![구독 선택기](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="034c8-148">디자이너는 렌더링할 `<template>.json` 파일에서 정의를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-148">The designer uses the definition in the `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="034c8-149">논리 앱을 만들고 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-149">Create and design your logic app.</span></span> <span data-ttu-id="034c8-150">배포 템플릿에는 변경 내용이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-150">Your deployment template is updated with your changes.</span></span>

    ![Visual Studio의 Logic App Designer](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="034c8-152">Visual Studio는 논리 앱이 작동하는 데 필요한 연결을 설정하기 위해 리소스 파일에 `Microsoft.Web/connections` 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-152">Visual Studio adds `Microsoft.Web/connections` resources to your resource file for any connections your logic app needs to function.</span></span> <span data-ttu-id="034c8-153">이러한 연결 속성은 배포할 때 설정할 수 있으며 배포한 후 Azure Portal의 **API 연결** 에서 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in the Azure portal.</span></span>

### <a name="switch-to-json-code-view"></a><span data-ttu-id="034c8-154">JSON 코드 보기로 전환</span><span class="sxs-lookup"><span data-stu-id="034c8-154">Switch to JSON code view</span></span>

<span data-ttu-id="034c8-155">논리 앱의 JSON 표현으로 표시하려면 디자이너 아래에 있는 **코드 보기** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-155">To show the JSON representation for your logic app, select the **Code View** tab at the bottom of the designer.</span></span>

<span data-ttu-id="034c8-156">전체 리소스 JSON으로 다시 전환하려면 `<template>.json` 파일을 마우스 오른쪽 단추로 클릭하고 **열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-156">To switch back to the full resource JSON, right-click the `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-to-visual-studio-deployment-templates"></a><span data-ttu-id="034c8-157">Visual Studio 배포 템플릿에 종속 리소스에 대한 참조 추가</span><span class="sxs-lookup"><span data-stu-id="034c8-157">Add references for dependent resources to Visual Studio deployment templates</span></span>

<span data-ttu-id="034c8-158">논리 앱에서 종속 리소스를 참조하려는 경우 논리 앱 배포 템플릿에서 [Azure Resource Manager 템플릿 함수](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-158">When you want your logic app to reference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="034c8-159">예를 들어, 논리 앱에서 논리 앱과 함께 배포하려는 Azure Function 또는 통합 계정을 참조하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-159">For example, you might want your logic app to reference an Azure Function or integration account that you want to deploy alongside your logic app.</span></span> <span data-ttu-id="034c8-160">Logic App Designer가 올바르게 렌더링하도록 배포 템플릿에서 매개 변수를 사용하는 방법에 대한 다음 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="034c8-160">Follow these guidelines about how to use parameters in your deployment template so that the Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="034c8-161">이러한 종류의 트리거 및 작업에서 논리 앱 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="034c8-162">하위 워크플로</span><span class="sxs-lookup"><span data-stu-id="034c8-162">Child workflow</span></span>
*   <span data-ttu-id="034c8-163">함수 앱</span><span class="sxs-lookup"><span data-stu-id="034c8-163">Function app</span></span>
*   <span data-ttu-id="034c8-164">APIM 호출</span><span class="sxs-lookup"><span data-stu-id="034c8-164">APIM call</span></span>
*   <span data-ttu-id="034c8-165">API 연결 런타임 URL</span><span class="sxs-lookup"><span data-stu-id="034c8-165">API connection runtime URL</span></span>
*   <span data-ttu-id="034c8-166">API 연결 경로</span><span class="sxs-lookup"><span data-stu-id="034c8-166">API connection path</span></span>

<span data-ttu-id="034c8-167">parameters, variables, resourceId, concat 등과 같은 템플릿 함수를 사용할 수 있습니다. 예를 들어, Azure Function 리소스 ID를 대체하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace the Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="034c8-168">그리고 매개 변수를 사용하는 위치는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-168">And where you would use parameters:</span></span>

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
<span data-ttu-id="034c8-169">또 다른 예로, Service Bus 메시지 전송 작업을 매개 변수화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-169">As another example you can parameterize the Service Bus send message operation:</span></span>

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> <span data-ttu-id="034c8-170">host.runtimeUrl은 선택 사항이며 있는 경우 템플릿에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="034c8-171">매개 변수를 사용할 때 Logic App Designer를 작동시키려면 다음과 같은 기본값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-171">For the Logic App Designer to work when you use parameters, you must provide default values, for example:</span></span>
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a><span data-ttu-id="034c8-172">논리 앱 저장</span><span class="sxs-lookup"><span data-stu-id="034c8-172">Save your logic app</span></span>

<span data-ttu-id="034c8-173">언제든지 논리 앱을 저장하려면 **파일** > **저장**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-173">To save your logic app at anytime, go to **File** > **Save**.</span></span> <span data-ttu-id="034c8-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="034c8-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="034c8-175">앱을 저장할 때 논리 앱에 오류가 발생하면 Visual Studio **출력** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-175">If your logic app has any errors when you save your app, they appear in the Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="034c8-176">Visual Studio에서 논리 앱 배포</span><span class="sxs-lookup"><span data-stu-id="034c8-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="034c8-177">앱을 구성한 후에 몇 단계 만에 Visual Studio에서 직접 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="034c8-178">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **배포** > **새로운 배포...**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-178">In Solution Explorer, right-click your project, and go to **Deploy** > **New Deployment...**</span></span>

    ![새 배포](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="034c8-180">메시지가 표시되면 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-180">When you're prompted, sign in to your Azure subscription.</span></span> 

3. <span data-ttu-id="034c8-181">이제 논리 앱을 배포하려는 리소스 그룹에 대한 세부 정보를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-181">Now you must select the details for the resource group where you want to deploy your logic app.</span></span> <span data-ttu-id="034c8-182">완료되면 **배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="034c8-183">리소스 그룹에 대한 올바른 템플릿 및 매개 변수 파일을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-183">Make sure that you select the correct template and parameters file for the resource group.</span></span> <span data-ttu-id="034c8-184">예를 들어, 프로덕션 환경에 배포하려는 경우 프로덕션 매개 변수 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-184">For example, if you want to deploy to a production environment, choose the production parameters file.</span></span>

    ![리소스 그룹 배포](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="034c8-186">배포 상태는 **출력** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-186">The deployment status appears in the **Output** window.</span></span> 
    <span data-ttu-id="034c8-187">**출력 보기 선택** 목록에서 **Azure 프로비전**을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-187">You might have to select **Azure Provisioning** in the **Show output from** list.</span></span>

    ![배포 상태 출력](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="034c8-189">나중에 원본 제어에서 논리 앱을 편집하고 Visual Studio를 사용하여 새 버전을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-189">In the future, you can edit your logic app in source control, and use Visual Studio to deploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="034c8-190">Azure Portal에서 정의를 직접 변경하게 되면 해당 변경 내용은 다음에 Visual Studio에서 배포할 경우 덮어쓰여집니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-190">If you change the definition in the Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-to-an-existing-resource-group-project"></a><span data-ttu-id="034c8-191">논리 앱을 기존 리소스 그룹 프로젝트에 추가</span><span class="sxs-lookup"><span data-stu-id="034c8-191">Add your logic app to an existing Resource Group project</span></span>

<span data-ttu-id="034c8-192">기존 리소스 그룹 프로젝트가 있는 경우 JSON 개요 창에서 해당 프로젝트에 논리 앱을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-192">If you have an existing Resource Group project, you can add your logic app to that project in the JSON Outline window.</span></span> <span data-ttu-id="034c8-193">이전에 만든 앱과 함께 다른 논리 앱을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-193">You can also add another logic app alongside the app you previously created.</span></span>

1. <span data-ttu-id="034c8-194">`<template>.json` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-194">Open the `<template>.json` file.</span></span>

2. <span data-ttu-id="034c8-195">JSON 개요 창을 열려면 **보기** > **다른 창** > **JSON 개요**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-195">To open the JSON Outline window, go to **View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="034c8-196">템플릿 파일에 리소스를 추가하려면 JSON 개요 창의 위쪽에서 **리소스 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-196">To add a resource to the template file, click **Add Resource** at the top of the JSON Outline window.</span></span> <span data-ttu-id="034c8-197">또는 JSON 개요 창에서 **리소스**를 마우스 오른쪽 단추로 클릭하고 **새 리소스 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-197">Or in the JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![JSON 개요 창](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="034c8-199">**리소스 추가** 대화 상자에서 **Logic App**을 찾고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-199">In the **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="034c8-200">논리 앱의 이름을 지정하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="034c8-200">Name your logic app, and choose **Add**.</span></span>

    ![리소스 추가](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="034c8-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="034c8-202">Next Steps</span></span>

* [<span data-ttu-id="034c8-203">Visual Studio 클라우드 탐색기를 사용하여 Logic Apps 관리</span><span class="sxs-lookup"><span data-stu-id="034c8-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="034c8-204">일반적인 예제 및 시나리오 보기</span><span class="sxs-lookup"><span data-stu-id="034c8-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="034c8-205">Azure Logic Apps을 사용하여 비즈니스 프로세스를 자동화하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="034c8-205">Learn how to automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="034c8-206">Azure Logic Apps과 시스템을 통합하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="034c8-206">Learn how to integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
