---
title: "aaaCreate 클라우드 앱 및 클라우드 서비스-Azure 논리 앱 간에 첫 번째 워크플로 | Microsoft Docs"
description: "Azure Logic Apps에서 워크플로를 만들고 실행하여 시스템 통합 및 EAI(Enterprise Application Integration) 시나리오에 대한 비즈니스 프로세스 자동화"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "워크플로, 클라우드 앱, 클라우드 서비스, 비즈니스 프로세스, 시스템 통합, Enterprise Application Integration, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="ea618-104">첫 번째 논리 앱 클라우드 앱 및 클라우드 서비스 간에 tooautomate 프로세스 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="ea618-104">Create your first logic app workflow tooautomate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="ea618-105">[Azure Logic Apps](logic-apps-what-are-logic-apps.md)를 사용하여 워크플로를 만들고 실행하는 경우 코드를 작성하지 않고도 비즈니스 프로세스를 쉽고 신속하게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="ea618-106">이 첫 번째 예제에서는 방법을 toocreate RSS를 확인 하는 기본 논리 앱 워크플로 피드 새로운 콘텐츠는 웹 사이트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-106">This first example shows how toocreate a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="ea618-107">Hello 웹 사이트 피드에 새 항목이 표시 되 면 hello 논리 앱 Outlook 또는 Gmail 계정에서 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-107">When new items appear in hello website's feed, hello logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="ea618-108">toocreate 및 실행 논리 앱 이러한 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-108">toocreate and run a logic app, you need these items:</span></span>

* <span data-ttu-id="ea618-109">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="ea618-109">An Azure subscription.</span></span> <span data-ttu-id="ea618-110">구독이 없는 경우 [Azure 계정을 사용하여 시작](https://azure.microsoft.com/free/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="ea618-111">그렇지 않으면 [종량제 구독에 등록](https://azure.microsoft.com/pricing/purchase-options/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="ea618-112">Azure 구독은 논리 앱 사용 요금을 청구하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="ea618-113">Azure Logic Apps에서 [사용 계량](../logic-apps/logic-apps-pricing.md) 및 [가격 책정](https://azure.microsoft.com/pricing/details/logic-apps)의 작동 방식에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="ea618-114">또한 이 예제에는 다음과 같은 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="ea618-115">Outlook.com, Office 365 Outlook 또는 Gmail 계정</span><span class="sxs-lookup"><span data-stu-id="ea618-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="ea618-116">개인 [Microsoft 계정](https://account.microsoft.com/account)이 있는 경우 Outlook.com 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="ea618-117">그렇지 않은 경우 Azure 직장 또는 학교 계정이 있으면 **Office 365 Outlook** 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="ea618-118">웹 사이트의 RSS 피드 링크 tooa입니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-118">A link tooa website's RSS feed.</span></span> <span data-ttu-id="ea618-119">이 예에서는 hello [RSS hello CNN.com 웹 사이트에서 상위 스토리에 대 한 피드](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="ea618-119">This example uses hello [RSS feed for top stories from hello CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="ea618-120">워크플로를 시작하는 트리거 추가</span><span class="sxs-lookup"><span data-stu-id="ea618-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="ea618-121">A [ *트리거* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) 논리 앱 워크플로 시작 하는 이벤트 이며 논리 앱 필요한 hello 첫 번째 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is hello first item that your logic app needs.</span></span>

1. <span data-ttu-id="ea618-122">Toohello 로그인 [Azure 포털](https://portal.azure.com "Azure 포털")합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-122">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="ea618-123">Hello 왼쪽된 메뉴에서 선택 **새로** > **엔터프라이즈 통합** > **논리 앱** 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-123">From hello left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Azure Portal, New, 엔터프라이즈 통합, Logic App](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="ea618-125">선택할 수도 있습니다 **새로**, hello 검색 상자에 입력 한 다음 `logic app`, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-125">You can also choose **New**, then in hello search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="ea618-126">그런 다음 **Logic App** > **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="ea618-127">논리 앱의 이름을 지정하고 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="ea618-128">이제 Azure 리소스 그룹을 만들거나 선택합니다. 이를 통해 관련 Azure 리소스를 구성하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="ea618-129">마지막으로, 논리 앱을 호스트에 대 한 hello 데이터 센터 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-129">Finally, select hello datacenter location for hosting your logic app.</span></span> <span data-ttu-id="ea618-130">준비 되 면 선택 **Pin toodashboard** 차례로 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-130">When you're ready, choose **Pin toodashboard** and then **Create**.</span></span>

     ![논리 앱 세부 정보](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="ea618-132">선택 하는 경우 **Pin toodashboard**, 논리 앱 배포 후 Azure 대시보드 hello에 표시 되 고 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-132">When you select **Pin toodashboard**, your logic app appears on hello Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="ea618-133">논리 앱 hello에 hello 대시보드에 표시 되지 않습니다 **모든 리소스** 타일에서 선택 **참조 더**, 논리 앱을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-133">If your logic app doesn't appear on hello dashboard, on hello **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="ea618-134">Hello 왼쪽된 메뉴에서 선택 하거나 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-134">Or on hello left menu, choose **More services**.</span></span> <span data-ttu-id="ea618-135">**엔터프라이즈 통합** 아래에서 **Logic Apps**을 선택하고 논리 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="ea618-136">Hello에 대 한 논리 앱을 처음 열 때 hello 논리가 응용 프로그램 디자이너 템플릿을 보여줍니다 tooget 시작을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-136">When you open your logic app for hello first time, hello Logic App Designer shows templates that you can use tooget started.</span></span> <span data-ttu-id="ea618-137">이제 **빈 Logic App**을 선택하여 처음부터 논리 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="ea618-138">hello 논리 앱 디자이너가 열리고 사용 가능한 서비스를 표시 하 고 *트리거* 논리 앱에서 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-138">hello Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="ea618-139">Hello 검색 상자에 입력 `RSS`,이 트리거를 선택 하 고: **-RSS 피드 항목은 게시 된 경우**</span><span class="sxs-lookup"><span data-stu-id="ea618-139">In hello search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![RSS 트리거](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="ea618-141">Hello 링크 tootrack 원하는 hello 웹 사이트의 RSS 피드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-141">Enter hello link for hello website's RSS feed that you want tootrack.</span></span> 

     <span data-ttu-id="ea618-142">**주파수** 및 **간격**을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="ea618-143">이러한 설정은 논리 앱이 새 항목을 확인하는 빈도를 결정하고 시간 범위 동안 찾은 모든 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="ea618-144">이 예에서는 상위 스토리에 대 한 매일 toohello 만우절 웹 사이트 게시 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-144">For this example, let's check every day for   top stories posted toohello CNN website.</span></span>

     ![RSS 피드, 빈도 및 간격을 사용하여 트리거 설정](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="ea618-146">이제 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-146">Save your work for now.</span></span> <span data-ttu-id="ea618-147">(Hello 디자이너 명령 모음에서 **저장**.)</span><span class="sxs-lookup"><span data-stu-id="ea618-147">(On hello designer command bar, choose **Save**.)</span></span>

   ![논리 앱 저장](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="ea618-149">저장 하면 논리 앱 문제, 하지만 새 항목에 대 한 논리 앱만 확인 현재 hello RSS 피드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in hello specified RSS feed.</span></span> 
   <span data-ttu-id="ea618-150">toomake 보다 유용한 추가 논리가 응용 프로그램의 사용자의 트리거 후 실행 하는 작업이 예제를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-150">toomake this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-tooyour-trigger"></a><span data-ttu-id="ea618-151">Tooyour 트리거가 응답 하는 작업 추가</span><span class="sxs-lookup"><span data-stu-id="ea618-151">Add an action that responds tooyour trigger</span></span>

<span data-ttu-id="ea618-152">[*작업*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)은 논리 앱 워크플로에서 수행하는 태스크입니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="ea618-153">트리거 tooyour 논리 앱을 추가 하면 해당 트리거에 의해 생성 된 데이터와 작업 tooperform 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-153">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="ea618-154">이 예에서는 이제 hello 웹 사이트의 RSS 피드에 새 항목이 표시 되 면 전자 메일을 보내는 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-154">For our example, we now add an action that sends email when new items appear in hello website's RSS feed.</span></span>

1. <span data-ttu-id="ea618-155">트리거를 아래 hello 디자이너에서 선택 **새 단계** > **동작 추가** 다음과 같이:</span><span class="sxs-lookup"><span data-stu-id="ea618-155">In hello designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![작업 추가](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="ea618-157">디자이너에서는 hello [사용할 커넥터](../connectors/apis-list.md) 트리거가 발생할 때 작업 tooperform를 선택할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-157">hello designer shows [available connectors](../connectors/apis-list.md) so that you can select an action tooperform when your trigger fires.</span></span>

2. <span data-ttu-id="ea618-158">에 따라 전자 메일 계정을 수행 hello 단계 Outlook 또는 Gmail에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-158">Based on your email account, follow hello steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="ea618-159">hello 검색 상자에, Outlook 계정에서 전자 메일 toosend 입력 `outlook`합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-159">toosend email from your Outlook account, in hello search box, enter `outlook`.</span></span> <span data-ttu-id="ea618-160">**서비스** 아래에서 개인 Microsoft 계정에 **Outlook.com**을 선택하거나 Azure 회사 또는 학교 계정에 **Office 365 Outlook**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="ea618-161">**작업** 아래에서 **전자 메일 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-161">Under **Actions**, select **Send an email**.</span></span>

       ![Outlook "전자 메일 보내기" 작업 선택](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="ea618-163">hello 검색 상자에, Gmail 계정에서 전자 메일 toosend 입력 `gmail`합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-163">toosend email from your Gmail account, in hello search box, enter `gmail`.</span></span> 
   <span data-ttu-id="ea618-164">**작업** 아래에서 **전자 메일 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-164">Under **Actions**, select **Send email**.</span></span>

       !["Gmail - 전자 메일 보내기" 선택](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="ea618-166">전자 메일 계정에 대 한 자격 증명에 대 한 메시지가 면 hello 사용자 이름 및 암호를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-166">When you're prompted for credentials, sign in with hello username and password for your email account.</span></span> 

4. <span data-ttu-id="ea618-167">Hello 대상 전자 메일 주소 처럼이 작업에 대 한 hello 세부 정보를 제공 하 고 예를 들어 hello 전자 메일로 데이터 tooinclude hello에 대 한 hello 매개 변수를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-167">Provide hello details for this action, like hello destination email address, and choose hello parameters for hello data tooinclude in hello email, for example:</span></span>

   ![전자 메일로 데이터 tooinclude 선택](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="ea618-169">따라서 Outlook을 선택한 경우 논리 앱은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![완료된 논리 앱](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="ea618-171">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-171">Save your changes.</span></span> <span data-ttu-id="ea618-172">(Hello 디자이너 명령 모음에서 **저장**.)</span><span class="sxs-lookup"><span data-stu-id="ea618-172">(On hello designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="ea618-173">이제 테스트하기 위해 논리 앱을 수동으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="ea618-174">Hello 디자이너 명령 모음에서 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-174">On hello designer command bar, choose **Run**.</span></span> <span data-ttu-id="ea618-175">그렇지 않으면 논리 앱을 설정 하는 hello 일정에 따라 RSS 피드를 지정 하는 hello 확인 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-175">Otherwise, you can let your logic app check hello specified RSS feed based on hello schedule that you set up.</span></span>

   <span data-ttu-id="ea618-176">논리 앱은 새 항목을 찾는 경우 hello 논리 앱 선택한 데이터를 포함 된 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-176">If your logic app finds new items, hello logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="ea618-177">새 항목을 찾지 논리 앱 전자 메일을 보내는 hello 동작을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-177">If no new items are found, your logic app skips hello action that sends email.</span></span>

7. <span data-ttu-id="ea618-178">논리 앱의 실행 하 고 트리거 논리 앱 메뉴에서 기록을 확인 하 고 toomonitor 선택 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-178">toomonitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![논리 앱 실행 및 트리거 기록 모니터링 및 보기](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="ea618-180">Hello 명령 모음에서 예상 하는 hello 데이터를 찾을 수 없는 경우을 선택 해 보십시오 **새로 고침**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-180">If you don't find hello data that you expect, on hello command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="ea618-181">논리 앱의 상태에 대 한 자세한 toolearn 또는 실행 하 고 기록 또는 toodiagnose 논리 앱 트리거, 참조 [논리 앱의 문제를 해결](logic-apps-diagnosing-failures.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-181">toolearn more about your logic app's status or run and trigger history, or toodiagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="ea618-182">논리 앱은 앱을 해제할 때까지 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="ea618-183">지금은 논리 앱 메뉴에서 응용 프로그램 해제 tooturn 선택 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-183">tooturn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="ea618-184">Hello 명령 모음에서 **사용 하지 않도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-184">On hello command bar, choose **Disable**.</span></span>

<span data-ttu-id="ea618-185">축하드립니다. 첫 번째 기본 논리 앱을 설정하고 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="ea618-186">또한 코드 없이 프로세스를 자동화하는 워크플로를 쉽게 만들고 클라우드 앱 및 클라우드 서비스를 통합하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="ea618-187">논리 앱 관리</span><span class="sxs-lookup"><span data-stu-id="ea618-187">Manage your logic app</span></span>

<span data-ttu-id="ea618-188">toomanage 응용 프로그램을 hello 상태를 확인, 편집, 기록 보기, 해제 또는 논리 앱을 삭제 하는 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-188">toomanage your app, you can perform tasks like check hello status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="ea618-189">Toohello 로그인 [Azure 포털](https://portal.azure.com "Azure 포털")합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-189">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="ea618-190">Hello 왼쪽된 메뉴에서 선택 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-190">On hello left menu, choose **More services**.</span></span> <span data-ttu-id="ea618-191">**엔터프라이즈 통합** 아래에서 **논리 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="ea618-192">논리 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-192">Select your logic app.</span></span> 

   <span data-ttu-id="ea618-193">Hello 논리 앱 메뉴에서 이러한 논리 앱 관리 작업을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-193">In hello logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="ea618-194">작업</span><span class="sxs-lookup"><span data-stu-id="ea618-194">Task</span></span>|<span data-ttu-id="ea618-195">단계</span><span class="sxs-lookup"><span data-stu-id="ea618-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="ea618-196">앱의 상태, 실행 기록 및 일반 정보 보기</span><span class="sxs-lookup"><span data-stu-id="ea618-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="ea618-197">**개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="ea618-198">앱 편집</span><span class="sxs-lookup"><span data-stu-id="ea618-198">Edit your app</span></span> | <span data-ttu-id="ea618-199">**Logic App Designer**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="ea618-200">앱의 워크플로 JSON 정의 보기</span><span class="sxs-lookup"><span data-stu-id="ea618-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="ea618-201">**Logic App 코드 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="ea618-202">논리 앱에 수행된 작업 보기</span><span class="sxs-lookup"><span data-stu-id="ea618-202">View operations performed on your logic app</span></span> | <span data-ttu-id="ea618-203">**활동 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="ea618-204">논리 앱의 이전 버전 보기</span><span class="sxs-lookup"><span data-stu-id="ea618-204">View past versions for your logic app</span></span> | <span data-ttu-id="ea618-205">**버전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="ea618-206">일시적으로 앱 해제</span><span class="sxs-lookup"><span data-stu-id="ea618-206">Turn off your app temporarily</span></span> | <span data-ttu-id="ea618-207">선택 **개요**, hello 명령 모음에서 선택 합니다 **사용 하지 않도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-207">Choose **Overview**, then on hello command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="ea618-208">앱 삭제</span><span class="sxs-lookup"><span data-stu-id="ea618-208">Delete your app</span></span> | <span data-ttu-id="ea618-209">선택 **개요**, hello 명령 모음에서 선택 합니다 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-209">Choose **Overview**, then on hello command bar, choose **Delete**.</span></span> <span data-ttu-id="ea618-210">논리 앱의 이름을 입력하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="ea618-211">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="ea618-211">Get help</span></span>

<span data-ttu-id="ea618-212">tooask 질문 질문에 답변 하 고 다른 Azure 논리 앱을 수행 하는 사용자가 방문 hello 자세한 [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-212">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="ea618-213">Azure 논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [Azure 논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea618-213">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea618-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea618-214">Next steps</span></span>

*  [<span data-ttu-id="ea618-215">조건 추가 및 워크플로 실행</span><span class="sxs-lookup"><span data-stu-id="ea618-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="ea618-216">논리 앱 템플릿</span><span class="sxs-lookup"><span data-stu-id="ea618-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="ea618-217">Azure Resource Manager 템플릿에서 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ea618-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
