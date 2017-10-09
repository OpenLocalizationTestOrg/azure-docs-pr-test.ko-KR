---
title: "aaaCreate, 빌드 및 Visual Studio-Azure 논리 앱에서에서 논리 앱 배포 | Microsoft Docs"
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
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="ad09c-103">Visual Studio에서 Azure Logic Apps 디자인, 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="ad09c-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="ad09c-104">하지만 hello [Azure 포털](https://portal.azure.com/) toocreate 수 있는 좋은 방법 제공 Azure 논리 앱을 관리 하 고, 설계, 구축 및 논리 앱 배포에 대 한 Visual Studio를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toocreate and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="ad09c-105">Visual Studio hello 논리가 응용 프로그램 디자이너와 같은 풍부한 도구 있습니다 toocreate 논리 앱, 배포 및 자동화 템플릿 구성 하며 tooany 환경을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-105">Visual Studio provides rich tools like hello Logic App Designer for you toocreate logic apps, configure deployment and automation templates, and deploy tooany environment.</span></span> 

<span data-ttu-id="ad09c-106">자세한 내용은 Azure 논리 앱 시작 tooget [어떻게 toocreate hello Azure 포털에서에서 첫 번째 논리 앱](logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-106">tooget started with Azure Logic Apps, learn [how toocreate your first logic app in hello Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="ad09c-107">설치 단계</span><span class="sxs-lookup"><span data-stu-id="ad09c-107">Installation steps</span></span>

<span data-ttu-id="ad09c-108">tooinstall 및 Visual Studio tools for Azure 논리 앱 구성, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-108">tooinstall and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ad09c-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ad09c-109">Prerequisites</span></span>

* <span data-ttu-id="ad09c-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) 또는 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ad09c-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="ad09c-111">[최신 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 이상)</span><span class="sxs-lookup"><span data-stu-id="ad09c-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="ad09c-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad09c-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="ad09c-113">액세스 toohello 웹 hello 포함 된 디자이너를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="ad09c-113">Access toohello web when using hello embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="ad09c-114">Azure Logic Apps용 Visual Studio 도구 설치</span><span class="sxs-lookup"><span data-stu-id="ad09c-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="ad09c-115">Hello 필수 구성 요소를 설치한 후:</span><span class="sxs-lookup"><span data-stu-id="ad09c-115">After you install hello prerequisites:</span></span>

1. <span data-ttu-id="ad09c-116">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-116">Open Visual Studio.</span></span> <span data-ttu-id="ad09c-117">Hello에 **도구** 메뉴 선택 **확장명 및 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-117">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="ad09c-118">Hello 확장 **온라인** 범주 온라인을 검색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-118">Expand hello **Online** category so you can search online.</span></span>
3. <span data-ttu-id="ad09c-119">**Visual Studio용 Azure Logic Apps 도구**를 찾을 때까지 **Logic Apps**을 찾아보거나 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="ad09c-120">toodownload 및 설치 hello 확장 클릭 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-120">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="ad09c-121">설치 후 Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="ad09c-122">다운로드할 수 있습니다 [Visual Studio 2017 용 Azure 논리 앱 도구](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) 및 hello [Visual Studio 2015 용 Azure 논리 앱 도구](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) hello Visual Studio 마켓플레이스에서 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and hello [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from hello Visual Studio Marketplace.</span></span>

<span data-ttu-id="ad09c-123">설치를 완료 한 후 논리 앱 디자이너로 hello Azure 리소스 그룹 프로젝트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-123">After you finish installation, you can use hello Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="ad09c-124">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="ad09c-124">Create your project</span></span>

1. <span data-ttu-id="ad09c-125">Hello에 **파일** 메뉴 너무 이동**새로**를 선택 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-125">On hello **File** menu, go too**New**, and select **Project**.</span></span> <span data-ttu-id="ad09c-126">또는 tooadd 너무 솔루션을 이동 기존 프로그램 프로젝트 tooan**추가**를 선택 하 고 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-126">Or tooadd your project tooan existing solution, go too**Add**, and select **New Project**.</span></span>

    ![파일 메뉴](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="ad09c-128">Hello에 **새 프로젝트** 창 찾기 **클라우드**를 선택 하 고 **Azure 리소스 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-128">In hello **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="ad09c-129">프로젝트 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-129">Name your project, and click **OK**.</span></span>

    ![새 프로젝트 추가](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="ad09c-131">선택 hello **논리 앱** toouse 사용자를 위해 빈 논리 앱 배포 템플릿을 만드는 있는 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-131">Select hello **Logic App** template, which creates a blank logic app deployment template for you toouse.</span></span> <span data-ttu-id="ad09c-132">템플릿을 선택한 후에 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-132">After you select your template, click **OK**.</span></span>

    ![Logic App 템플릿 선택](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="ad09c-134">이제 논리 앱 프로젝트 tooyour 솔루션을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-134">You've now added your logic app project tooyour solution.</span></span> 
    <span data-ttu-id="ad09c-135">배포 파일은 hello 솔루션 탐색기에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-135">In hello Solution Explorer, your deployment file should appear.</span></span>

    ![배포 파일](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="ad09c-137">Logic App Designer에서 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ad09c-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="ad09c-138">논리 앱을 포함 하는 Azure 리소스 그룹 프로젝트를 사용 하는 경우 워크플로 toocreate Visual Studio에서에서 논리 응용 프로그램 디자이너 hello 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-138">When you have an Azure Resource Group project that contains a logic app, you can open hello Logic App Designer in Visual Studio toocreate your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="ad09c-139">hello 디자이너에서 사용 가능한 속성 및 데이터에 대 한 커넥터를 너무 쿼리 하는 인터넷에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-139">hello designer requires an internet connection too query connectors for available properties and data.</span></span> <span data-ttu-id="ad09c-140">예를 들어 hello Dynamics CRM Online 커넥터를 사용 하는 경우 hello 디자이너 CRM 인스턴스 tooshow 사용할 수 있는 사용자 지정 및 기본 속성을 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-140">For example, if you use hello Dynamics CRM Online connector, hello designer queries your CRM instance tooshow available custom and default properties.</span></span>

1. <span data-ttu-id="ad09c-141">`<template>.json` 파일을 마우스 오른쪽 단추로 클릭하고 **Logic App Designer로 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="ad09c-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="ad09c-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="ad09c-143">Azure 구독, 리소스 그룹 및 배포 템플릿의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ad09c-144">논리 앱을 디자인하면 디자인하는 동안 속성을 쿼리하는 API 연결 리소스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="ad09c-145">Visual Studio 디자인 타임 동안 선택한 리소스 그룹 toocreate 해당 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-145">Visual Studio uses your selected resource group toocreate those connections during design time.</span></span> <span data-ttu-id="ad09c-146">tooview 하거나 모든 API 연결 변경, toohello Azure 포털을 이동 하 고 찾아보기 **API 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-146">tooview or change any API Connections, go toohello Azure portal, and browse for **API Connections**.</span></span>

    ![구독 선택기](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="ad09c-148">hello 디자이너 hello 정의 사용 하 여 hello에 `<template>.json` 렌더링에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-148">hello designer uses hello definition in hello `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="ad09c-149">논리 앱을 만들고 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-149">Create and design your logic app.</span></span> <span data-ttu-id="ad09c-150">배포 템플릿에는 변경 내용이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-150">Your deployment template is updated with your changes.</span></span>

    ![Visual Studio의 Logic App Designer](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="ad09c-152">Visual Studio 추가 `Microsoft.Web/connections` 리소스 너무 리소스 파일 모든 연결에 대해 논리 앱 toofunction를 프로비저닝해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-152">Visual Studio adds `Microsoft.Web/connections` resources too your resource file for any connections your logic app needs toofunction.</span></span> <span data-ttu-id="ad09c-153">이러한 연결 속성을 배포할 때 설정 및 배포한 후 관리할 수 **API 연결** hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="ad09c-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in hello Azure portal.</span></span>

### <a name="switch-toojson-code-view"></a><span data-ttu-id="ad09c-154">스위치 tooJSON 코드 보기</span><span class="sxs-lookup"><span data-stu-id="ad09c-154">Switch tooJSON code view</span></span>

<span data-ttu-id="ad09c-155">tooshow hello 선택 hello 논리가 응용 프로그램에 대 한 JSON 표현 **코드 보기** hello hello 디자이너 맨 아래에 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-155">tooshow hello JSON representation for your logic app, select hello **Code View** tab at hello bottom of hello designer.</span></span>

<span data-ttu-id="ad09c-156">tooswitch JSON toohello 전체 리소스를 다시 마우스 오른쪽 단추로 hello `<template>.json` 파일을 찾아 선택 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-156">tooswitch back toohello full resource JSON, right-click hello `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a><span data-ttu-id="ad09c-157">종속 리소스 tooVisual Studio 배포 템플릿에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-157">Add references for dependent resources tooVisual Studio deployment templates</span></span>

<span data-ttu-id="ad09c-158">논리 앱 tooreference 종속 리소스를 원하는 경우 사용할 수 있습니다 [Azure 리소스 관리자 템플릿 함수](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) 논리 앱 배포 템플릿에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-158">When you want your logic app tooreference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="ad09c-159">예를 들어 논리 앱 tooreference 논리 앱 함께 toodeploy 되도록 Azure 기능 또는 통합 계정 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-159">For example, you might want your logic app tooreference an Azure Function or integration account that you want toodeploy alongside your logic app.</span></span> <span data-ttu-id="ad09c-160">배포 템플릿에 hello 논리가 응용 프로그램 디자이너 하므로 toouse 매개 변수가 올바르게 렌더링 하는 방법에 대 한 다음이 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-160">Follow these guidelines about how toouse parameters in your deployment template so that hello Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="ad09c-161">이러한 종류의 트리거 및 작업에서 논리 앱 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="ad09c-162">하위 워크플로</span><span class="sxs-lookup"><span data-stu-id="ad09c-162">Child workflow</span></span>
*   <span data-ttu-id="ad09c-163">함수 앱</span><span class="sxs-lookup"><span data-stu-id="ad09c-163">Function app</span></span>
*   <span data-ttu-id="ad09c-164">APIM 호출</span><span class="sxs-lookup"><span data-stu-id="ad09c-164">APIM call</span></span>
*   <span data-ttu-id="ad09c-165">API 연결 런타임 URL</span><span class="sxs-lookup"><span data-stu-id="ad09c-165">API connection runtime URL</span></span>
*   <span data-ttu-id="ad09c-166">API 연결 경로</span><span class="sxs-lookup"><span data-stu-id="ad09c-166">API connection path</span></span>

<span data-ttu-id="ad09c-167">parameters, variables, resourceId, concat 등과 같은 템플릿 함수를 사용할 수 있습니다. 예를 들어 다음과 같습니다 어떻게 hello Azure 함수 리소스 ID를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace hello Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="ad09c-168">그리고 매개 변수를 사용하는 위치는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-168">And where you would use parameters:</span></span>

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
<span data-ttu-id="ad09c-169">또 다른 예로 서비스 버스 전송 메시지 작업 hello 매개 변수화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-169">As another example you can parameterize hello Service Bus send message operation:</span></span>

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
> <span data-ttu-id="ad09c-170">host.runtimeUrl은 선택 사항이며 있는 경우 템플릿에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="ad09c-171">논리 응용 프로그램 디자이너 toowork hello에 대 한 매개 변수를 사용할 때 제공 해야 기본 값 예:</span><span class="sxs-lookup"><span data-stu-id="ad09c-171">For hello Logic App Designer toowork when you use parameters, you must provide default values, for example:</span></span>
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

### <a name="save-your-logic-app"></a><span data-ttu-id="ad09c-172">논리 앱 저장</span><span class="sxs-lookup"><span data-stu-id="ad09c-172">Save your logic app</span></span>

<span data-ttu-id="ad09c-173">toosave에서 언제 든 지 논리 앱 이동 너무**파일** > **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-173">toosave your logic app at anytime, go too**File** > **Save**.</span></span> <span data-ttu-id="ad09c-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="ad09c-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="ad09c-175">Hello Visual Studio에에서 나타나는 경우 논리 앱에 응용 프로그램을 저장 하면 모든 오류가 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="ad09c-175">If your logic app has any errors when you save your app, they appear in hello Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="ad09c-176">Visual Studio에서 논리 앱 배포</span><span class="sxs-lookup"><span data-stu-id="ad09c-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="ad09c-177">앱을 구성한 후에 몇 단계 만에 Visual Studio에서 직접 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="ad09c-178">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 이동 너무**배포** > **새 배포...**</span><span class="sxs-lookup"><span data-stu-id="ad09c-178">In Solution Explorer, right-click your project, and go too**Deploy** > **New Deployment...**</span></span>

    ![새 배포](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="ad09c-180">메시지가 나타나면 tooyour Azure 구독에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-180">When you're prompted, sign in tooyour Azure subscription.</span></span> 

3. <span data-ttu-id="ad09c-181">이제 저장할 toodeploy 논리 앱 hello 리소스 그룹에 대 한 hello 세부 정보를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-181">Now you must select hello details for hello resource group where you want toodeploy your logic app.</span></span> <span data-ttu-id="ad09c-182">완료되면 **배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ad09c-183">Hello 올바른 템플릿과 hello 리소스 그룹에 대 한 매개 변수 파일을 선택 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-183">Make sure that you select hello correct template and parameters file for hello resource group.</span></span> <span data-ttu-id="ad09c-184">예를 들어 toodeploy tooa 프로덕션 환경 hello 프로덕션 매개 변수 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-184">For example, if you want toodeploy tooa production environment, choose hello production parameters file.</span></span>

    ![Tooresource 그룹 배포](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="ad09c-186">hello에 hello 배포 상태가 표시 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="ad09c-186">hello deployment status appears in hello **Output** window.</span></span> 
    <span data-ttu-id="ad09c-187">Tooselect 해야할 **Azure 프로 비전** hello에 **에서 출력 보기** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-187">You might have tooselect **Azure Provisioning** in hello **Show output from** list.</span></span>

    ![배포 상태 출력](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="ad09c-189">이후 hello, 논리 앱의 소스 제어에서 편집한 Visual Studio toodeploy 새 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-189">In hello future, you can edit your logic app in source control, and use Visual Studio toodeploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="ad09c-190">직접 hello Azure 포털에서에서 hello 정의 변경 하면 다음에 Visual Studio에서 배포할 때 이러한 변경 내용은 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-190">If you change hello definition in hello Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a><span data-ttu-id="ad09c-191">논리 앱 tooan 기존 리소스 그룹 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-191">Add your logic app tooan existing Resource Group project</span></span>

<span data-ttu-id="ad09c-192">기존 리소스 그룹 프로젝트를 사용 하도록 설정한 경우에 hello JSON 개요 창에서 논리 앱 toothat 프로젝트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-192">If you have an existing Resource Group project, you can add your logic app toothat project in hello JSON Outline window.</span></span> <span data-ttu-id="ad09c-193">또한 이전에 만든 hello 응용 프로그램과 함께 다른 논리 앱을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-193">You can also add another logic app alongside hello app you previously created.</span></span>

1. <span data-ttu-id="ad09c-194">열기 hello `<template>.json` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-194">Open hello `<template>.json` file.</span></span>

2. <span data-ttu-id="ad09c-195">JSON 개요 창의 tooopen hello 너무 이동**보기** > **다른 창** > **JSON 개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-195">tooopen hello JSON Outline window, go too**View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="ad09c-196">tooadd 리소스 toohello 템플릿 파일을 클릭 하 여 **리소스 추가** hello hello JSON 개요 창의 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-196">tooadd a resource toohello template file, click **Add Resource** at hello top of hello JSON Outline window.</span></span> <span data-ttu-id="ad09c-197">Hello JSON 개요 창에서 마우스 오른쪽 단추로 클릭 하거나 **리소스**를 선택 하 고 **새 리소스 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-197">Or in hello JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![JSON 개요 창](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="ad09c-199">Hello에 **리소스 추가** 찾기 및 선택 대화 상자, **논리 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-199">In hello **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="ad09c-200">논리 앱의 이름을 지정하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad09c-200">Name your logic app, and choose **Add**.</span></span>

    ![리소스 추가](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="ad09c-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad09c-202">Next Steps</span></span>

* [<span data-ttu-id="ad09c-203">Visual Studio 클라우드 탐색기를 사용하여 Logic Apps 관리</span><span class="sxs-lookup"><span data-stu-id="ad09c-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="ad09c-204">일반적인 예제 및 시나리오 보기</span><span class="sxs-lookup"><span data-stu-id="ad09c-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="ad09c-205">Azure 논리 앱 tooautomate 비즈니스에서 처리 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="ad09c-205">Learn how tooautomate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="ad09c-206">자세한 내용은 방법 toointegrate Azure 논리 앱 시스템</span><span class="sxs-lookup"><span data-stu-id="ad09c-206">Learn how toointegrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
