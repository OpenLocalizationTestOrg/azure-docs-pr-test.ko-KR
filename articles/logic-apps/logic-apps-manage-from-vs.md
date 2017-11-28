---
title: "Visual Studio에서 Logic Apps 관리 - Azure Logic Apps | Microsoft Docs"
description: "Visual Studio 클라우드 탐색기를 사용하여 Logic Apps 및 기타 Azure 자산 관리"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: a5bf24de1a7a2b6d4c1ae6416c95d83ef7506da3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="4365c-103">Visual Studio 클라우드 탐색기를 사용하여 Logic Apps 관리</span><span class="sxs-lookup"><span data-stu-id="4365c-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="4365c-104">[Azure Portal](https://portal.azure.com/)에서는 Azure Logic Apps를 디자인하고 관리하는 유용한 방법을 제공하지만 Visual Studio 클라우드 탐색기를 사용하면 논리 앱을 포함한 여러 Azure 자산을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to design and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="4365c-105">Visual Studio 클라우드 탐색기를 사용하면 게시된 논리 앱을 찾아보기, 관리, 편집 및 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="4365c-106">관리 작업에는 실행 기록의 보기, 활성화 및 비활성화가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="4365c-107">먼저 이러한 Azure Logic Apps용 Visual Studio Tools를 설치하고 구성해야 Visual Studio에서 논리 앱에 액세스하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4365c-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4365c-108">Prerequisites</span></span>

* [<span data-ttu-id="4365c-109">Visual Studio 2015 또는 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4365c-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="4365c-110">[최신 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 이상)</span><span class="sxs-lookup"><span data-stu-id="4365c-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="4365c-111">Visual Studio 클라우드 탐색기</span><span class="sxs-lookup"><span data-stu-id="4365c-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="4365c-112">포함된 디자이너를 사용하는 경우 웹에 대한 액세스</span><span class="sxs-lookup"><span data-stu-id="4365c-112">Access to the web when using the embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="4365c-113">Logic Apps용 Visual Studio 도구 설치</span><span class="sxs-lookup"><span data-stu-id="4365c-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="4365c-114">필수 구성 요소를 설치한 후 Visual Studio용 Azure Logic Apps 도구를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-114">After you install the prerequisites, download and install the Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="4365c-115">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-115">Open Visual Studio.</span></span> <span data-ttu-id="4365c-116">**도구** 메뉴에서 **확장 및 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-116">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="4365c-117">Visual Studio 갤러리에서 온라인을 검색할 수 있도록 **온라인** 범주를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-117">Expand the **Online** category so you can search online in the Visual Studio Gallery.</span></span>
3. <span data-ttu-id="4365c-118">**Visual Studio용 Azure Logic Apps 도구**를 찾을 때까지 **Logic Apps**을 찾아보거나 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="4365c-119">확장을 다운로드하고 설치하려면 **다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-119">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="4365c-120">설치 후 Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="4365c-121">직접 Visual Studio용 Azure Logic Apps 도구를 다운로드하려면 [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-121">To download the Azure Logic Apps Tools for Visual Studio directly, go to the [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="4365c-122">클라우드 탐색기에서 논리 앱 찾아보기</span><span class="sxs-lookup"><span data-stu-id="4365c-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="4365c-123">클라우드 탐색기를 열려면 **보기** 메뉴에서 **클라우드 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-123">To open Cloud Explorer, on the **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="4365c-124">리소스 그룹 또는 리소스 유형별로 논리 앱을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="4365c-125">리소스 종류별로 찾아보는 경우 Azure 구독을 선택하고 **Logic Apps** 섹션을 확장한 다음 논리 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-125">If you browse by resource type, select your Azure subscription, expand the **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="4365c-126">리소스 그룹별로 찾아보는 경우 논리 앱을 갖는 리소스 그룹을 확장하고 논리 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-126">If you browse by resource group, expand the resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="4365c-127">논리 앱에 대한 명령을 보려면 논리 앱을 마우스 오른쪽 단추로 클릭하거나 클라우드 탐색기 아래쪽의 **작업** 메뉴에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-127">To view commands for your logic app, either right-click your logic app, or at the bottom of Cloud Explorer, choose from the **Actions** menu.</span></span>

    ![논리 앱 찾아보기](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="4365c-129">Logic Apps 디자이너로 논리 앱 편집</span><span class="sxs-lookup"><span data-stu-id="4365c-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="4365c-130">클라우드 탐색기에서는 Azure Portal에서 사용하는 동일한 디자이너에서 현재 배포된 논리 앱을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-130">From Cloud Explorer, you can open a currently deployed logic app in the same designer that you use in the Azure portal.</span></span> 

* <span data-ttu-id="4365c-131">클라우드 탐색기에서 논리 앱을 편집하려면 논리 앱을 마우스 오른쪽 단추로 클릭하고 **논리 앱 편집기로 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-131">To edit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="4365c-132">업데이트를 클라우드에 게시하려면 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-132">To publish your updates to the cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="4365c-133">새 실행을 시작하려면 **트리거 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-133">To start a new run, choose **Run Trigger**.</span></span>

![논리 앱 디자이너](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="4365c-135">디자이너에서 논리 앱을 **다운로드**할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-135">From the designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="4365c-136">이 작업은 자동으로 논리 앱 정의를 매개 변수화하고 Azure Resource Manager 배포 템플릿으로 정의를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-136">This action automatically parameterizes the logic app definition, and saves the definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="4365c-137">Azure 리소스 그룹 프로젝트에 이 배포 템플릿을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-137">You can add this deployment template to your Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="4365c-138">논리 앱 실행 기록 찾아보기</span><span class="sxs-lookup"><span data-stu-id="4365c-138">Browse your logic app run history</span></span>

<span data-ttu-id="4365c-139">논리 앱의 실행 기록을 보려면 논리 앱을 마우스 오른쪽 단추로 클릭하고 **실행 기록 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-139">To view the run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="4365c-140">표시된 속성 중 하나에 따라 실행 기록의 순서를 변경하려면 열 머리글을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-140">To reorder your run history based on any of the properties shown, select the column header.</span></span>

![실행 기록](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="4365c-142">각 단계의 입력 및 출력을 비롯하여 실행 결과를 검토할 수 있도록 인스턴스에 대한 실행 기록을 표시하려면 실행 인스턴스 중 하나를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4365c-142">To show the run history for an instance so you can review the run results, including the inputs and outputs from each step, double-click one of the run instances.</span></span>

![단계에서 기록 결과, 입력 및 출력 실행](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="4365c-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4365c-144">Next steps</span></span>

* [<span data-ttu-id="4365c-145">첫 번째 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="4365c-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="4365c-146">Visual Studio에서 Logic Apps 디자인, 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="4365c-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="4365c-147">일반적인 예제 및 시나리오 보기</span><span class="sxs-lookup"><span data-stu-id="4365c-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="4365c-148">동영상: Azure Logic Apps를 사용하여 비즈니스 프로세스 자동화</span><span class="sxs-lookup"><span data-stu-id="4365c-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="4365c-149">동영상: Azure Logic Apps와 시스템 통합</span><span class="sxs-lookup"><span data-stu-id="4365c-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
