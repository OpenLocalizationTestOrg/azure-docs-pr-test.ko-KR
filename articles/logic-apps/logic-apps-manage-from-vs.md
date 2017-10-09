---
title: "Visual Studio-Azure 논리 앱에서에서 aaaManage 논리 앱 | Microsoft Docs"
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
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="f4f16-103">Visual Studio 클라우드 탐색기를 사용하여 Logic Apps 관리</span><span class="sxs-lookup"><span data-stu-id="f4f16-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="f4f16-104">하지만 hello [Azure 포털](https://portal.azure.com/) toodesign 수 있는 좋은 방법 제공 Azure 논리 앱을 관리 하 고, 논리 앱을 포함 하 여 Azure 자산을 관리 하기 위한 Visual Studio 클라우드 탐색기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toodesign and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="f4f16-105">Visual Studio 클라우드 탐색기를 사용하면 게시된 논리 앱을 찾아보기, 관리, 편집 및 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="f4f16-106">관리 작업에는 실행 기록의 보기, 활성화 및 비활성화가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="f4f16-107">먼저 이러한 Azure Logic Apps용 Visual Studio Tools를 설치하고 구성해야 Visual Studio에서 논리 앱에 액세스하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f4f16-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f4f16-108">Prerequisites</span></span>

* [<span data-ttu-id="f4f16-109">Visual Studio 2015 또는 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f4f16-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="f4f16-110">[최신 Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 이상)</span><span class="sxs-lookup"><span data-stu-id="f4f16-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="f4f16-111">Visual Studio 클라우드 탐색기</span><span class="sxs-lookup"><span data-stu-id="f4f16-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="f4f16-112">액세스 toohello 웹 hello 포함 된 디자이너를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f4f16-112">Access toohello web when using hello embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="f4f16-113">Logic Apps용 Visual Studio 도구 설치</span><span class="sxs-lookup"><span data-stu-id="f4f16-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="f4f16-114">Hello 필수 구성 요소를 설치한 후 다운로드 하 고 Visual Studio 용 hello Azure 논리 앱 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-114">After you install hello prerequisites, download and install hello Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="f4f16-115">Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-115">Open Visual Studio.</span></span> <span data-ttu-id="f4f16-116">Hello에 **도구** 메뉴 선택 **확장명 및 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-116">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="f4f16-117">Hello 확장 **온라인** 범주 온라인 hello Visual Studio 갤러리에서에서 검색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-117">Expand hello **Online** category so you can search online in hello Visual Studio Gallery.</span></span>
3. <span data-ttu-id="f4f16-118">**Visual Studio용 Azure Logic Apps 도구**를 찾을 때까지 **Logic Apps**을 찾아보거나 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="f4f16-119">toodownload 및 설치 hello 확장 클릭 **다운로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-119">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="f4f16-120">설치 후 Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="f4f16-121">toodownload hello Azure 논리 앱 Tools for Visual Studio를 이동한 다음 toohello [Visual Studio 마켓플레이스](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-121">toodownload hello Azure Logic Apps Tools for Visual Studio directly, go toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="f4f16-122">클라우드 탐색기에서 논리 앱 찾아보기</span><span class="sxs-lookup"><span data-stu-id="f4f16-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="f4f16-123">hello에 클라우드 탐색기 tooopen **보기** 메뉴 선택 **클라우드 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-123">tooopen Cloud Explorer, on hello **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="f4f16-124">리소스 그룹 또는 리소스 유형별로 논리 앱을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="f4f16-125">Azure 구독을 선택, hello 확장을 리소스 유형에 따라 이동 하는 경우 **논리 앱** 섹션을 논리 앱을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-125">If you browse by resource type, select your Azure subscription, expand hello **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="f4f16-126">리소스 그룹으로 이동 하는 경우 논리 앱 없는 hello 리소스 그룹을 확장 하 고 논리 앱을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-126">If you browse by resource group, expand hello resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="f4f16-127">tooview 명령을 논리 앱에 대 한 논리 앱을 마우스 오른쪽 단추로 클릭 하거나 클라우드 탐색기 hello 맨 아래에 선택 hello에서 **동작** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="f4f16-127">tooview commands for your logic app, either right-click your logic app, or at hello bottom of Cloud Explorer, choose from hello **Actions** menu.</span></span>

    ![논리 앱 찾아보기](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="f4f16-129">Logic Apps 디자이너로 논리 앱 편집</span><span class="sxs-lookup"><span data-stu-id="f4f16-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="f4f16-130">클라우드 탐색기에서 hello에 현재 배포 된 논리 앱을 열 수 있습니다 hello Azure 포털에서에서 사용 하는 동일한 디자이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-130">From Cloud Explorer, you can open a currently deployed logic app in hello same designer that you use in hello Azure portal.</span></span> 

* <span data-ttu-id="f4f16-131">tooedit 클라우드 탐색기에서 논리 앱, 논리 앱을 마우스 오른쪽 단추로 클릭 하 고 선택 **논리가 응용 프로그램 편집기 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-131">tooedit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="f4f16-132">toopublish 업데이트 toohello 클라우드 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-132">toopublish your updates toohello cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="f4f16-133">새 실행 toostart 선택 **트리거 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-133">toostart a new run, choose **Run Trigger**.</span></span>

![논리 앱 디자이너](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="f4f16-135">Hello 디자이너에서 수도 있습니다 **다운로드** 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="f4f16-135">From hello designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="f4f16-136">이 작업은 자동으로 hello 논리 앱 정의 매개 변수화 하 고 Azure 리소스 관리자 배포 템플릿으로 hello 정의 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-136">This action automatically parameterizes hello logic app definition, and saves hello definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="f4f16-137">이 배포 템플릿 tooyour Azure 리소스 그룹 프로젝트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-137">You can add this deployment template tooyour Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="f4f16-138">논리 앱 실행 기록 찾아보기</span><span class="sxs-lookup"><span data-stu-id="f4f16-138">Browse your logic app run history</span></span>

<span data-ttu-id="f4f16-139">실행 논리 앱에 대 한 기록이 tooview hello 논리 앱을 마우스 오른쪽 단추로 클릭 하 고 선택 **열기 실행 기록이**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-139">tooview hello run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="f4f16-140">tooreorder hello 속성 선택 하 여 표시 된 hello 열 머리글 중 하나에 실행된 기록을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-140">tooreorder your run history based on any of hello properties shown, select hello column header.</span></span>

![실행 기록](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="f4f16-142">hello 실행 hello 입 / 출력에서 각 단계를 포함 하 여 결과 검토할 수 있도록 실행 인스턴스에 대 한 기록이 tooshow hello는 인스턴스를 실행 하는 hello 중 하나를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4f16-142">tooshow hello run history for an instance so you can review hello run results, including hello inputs and outputs from each step, double-click one of hello run instances.</span></span>

![단계에서 기록 결과, 입력 및 출력 실행](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="f4f16-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4f16-144">Next steps</span></span>

* [<span data-ttu-id="f4f16-145">첫 번째 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f4f16-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="f4f16-146">Visual Studio에서 Logic Apps 디자인, 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="f4f16-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="f4f16-147">일반적인 예제 및 시나리오 보기</span><span class="sxs-lookup"><span data-stu-id="f4f16-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="f4f16-148">동영상: Azure Logic Apps를 사용하여 비즈니스 프로세스 자동화</span><span class="sxs-lookup"><span data-stu-id="f4f16-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="f4f16-149">동영상: Azure Logic Apps와 시스템 통합</span><span class="sxs-lookup"><span data-stu-id="f4f16-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
