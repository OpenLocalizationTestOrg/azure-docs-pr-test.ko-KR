---
title: "클라우드 앱과 클라우드 서비스 간에 첫 번째 워크플로 만들기 - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 204bf123509729b60b55c306050cef54aa7fecc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-logic-app-workflow-to-automate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="f81d1-104">클라우드 앱과 클라우드 서비스 간에 프로세스를 자동화하는 첫 번째 논리 앱 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="f81d1-104">Create your first logic app workflow to automate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="f81d1-105">[Azure Logic Apps](logic-apps-what-are-logic-apps.md)를 사용하여 워크플로를 만들고 실행하는 경우 코드를 작성하지 않고도 비즈니스 프로세스를 쉽고 신속하게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="f81d1-106">이 첫 번째 예제에서는 웹 사이트에서 새 콘텐츠에 대한 RSS 피드를 확인하는 기본 논리 앱 워크플로를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-106">This first example shows how to create a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="f81d1-107">웹 사이트의 피드에서 새 항목이 표시되면 논리 앱은 Outlook 또는 Gmail 계정에서 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-107">When new items appear in the website's feed, the logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="f81d1-108">논리 앱을 만들고 실행하려면 다음이 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-108">To create and run a logic app, you need these items:</span></span>

* <span data-ttu-id="f81d1-109">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="f81d1-109">An Azure subscription.</span></span> <span data-ttu-id="f81d1-110">구독이 없는 경우 [Azure 계정을 사용하여 시작](https://azure.microsoft.com/free/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="f81d1-111">그렇지 않으면 [종량제 구독에 등록](https://azure.microsoft.com/pricing/purchase-options/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="f81d1-112">Azure 구독은 논리 앱 사용 요금을 청구하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="f81d1-113">Azure Logic Apps에서 [사용 계량](../logic-apps/logic-apps-pricing.md) 및 [가격 책정](https://azure.microsoft.com/pricing/details/logic-apps)의 작동 방식에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="f81d1-114">또한 이 예제에는 다음과 같은 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="f81d1-115">Outlook.com, Office 365 Outlook 또는 Gmail 계정</span><span class="sxs-lookup"><span data-stu-id="f81d1-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="f81d1-116">개인 [Microsoft 계정](https://account.microsoft.com/account)이 있는 경우 Outlook.com 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="f81d1-117">그렇지 않은 경우 Azure 직장 또는 학교 계정이 있으면 **Office 365 Outlook** 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="f81d1-118">웹 사이트의 RSS 피드에 대한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-118">A link to a website's RSS feed.</span></span> <span data-ttu-id="f81d1-119">이 예제에서는 [CNN.com 웹 사이트의 주요 기사에 대한 RSS 피드](http://rss.cnn.com/rss/cnn_topstories.rss)(`http://rss.cnn.com/rss/cnn_topstories.rss`)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-119">This example uses the [RSS feed for top stories from the CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="f81d1-120">워크플로를 시작하는 트리거 추가</span><span class="sxs-lookup"><span data-stu-id="f81d1-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="f81d1-121">[*트리거*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)는 논리 앱 워크플로를 시작하는 이벤트이며 논리 앱에 필요한 첫 번째 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is the first item that your logic app needs.</span></span>

1. <span data-ttu-id="f81d1-122">[Azure Portal](https://portal.azure.com "Azure Portal")에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-122">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="f81d1-123">다음과 같이 왼쪽 메뉴에서 **새로 만들기** > **엔터프라이즈 통합** > **Logic App**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-123">From the left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Azure Portal, New, 엔터프라이즈 통합, Logic App](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="f81d1-125">또한 **새로 만들기**를 선택하고 검색 상자에서 `logic app`을 입력한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-125">You can also choose **New**, then in the search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="f81d1-126">그런 다음 **Logic App** > **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="f81d1-127">논리 앱의 이름을 지정하고 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="f81d1-128">이제 Azure 리소스 그룹을 만들거나 선택합니다. 이를 통해 관련 Azure 리소스를 구성하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="f81d1-129">마지막으로 논리 앱을 호스팅할 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-129">Finally, select the datacenter location for hosting your logic app.</span></span> <span data-ttu-id="f81d1-130">준비되면 **대시보드에 고정** 및 **만들기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-130">When you're ready, choose **Pin to dashboard** and then **Create**.</span></span>

     ![논리 앱 세부 정보](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="f81d1-132">**대시보드에 고정**을 선택하면 논리 앱이 배포 후에 Azure 대시보드에 표시되고 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-132">When you select **Pin to dashboard**, your logic app appears on the Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="f81d1-133">논리 앱이 대시보드에 표시되지 않으면 **모든 리소스** 타일에서 **추가 보기**를 선택하고 논리 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-133">If your logic app doesn't appear on the dashboard, on the **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="f81d1-134">또는 왼쪽 메뉴에서 **추가 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-134">Or on the left menu, choose **More services**.</span></span> <span data-ttu-id="f81d1-135">**엔터프라이즈 통합** 아래에서 **Logic Apps**을 선택하고 논리 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="f81d1-136">논리 앱을 처음으로 열면 Logic App Designer에서는 시작하는 데 사용할 수 있는 템플릿을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-136">When you open your logic app for the first time, the Logic App Designer shows templates that you can use to get started.</span></span> <span data-ttu-id="f81d1-137">이제 **빈 Logic App**을 선택하여 처음부터 논리 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="f81d1-138">논리 앱 디자이너가 열리고 사용 가능한 서비스를 표시 하 고 *트리거* 논리 앱에서 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-138">The Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="f81d1-139">검색 상자에 `RSS`를 입력하고 다음 트리거를 선택합니다. **RSS - 피드 항목이 게시되는 경우**</span><span class="sxs-lookup"><span data-stu-id="f81d1-139">In the search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![RSS 트리거](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="f81d1-141">추적하려는 웹 사이트의 RSS 피드에 대한 링크를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-141">Enter the link for the website's RSS feed that you want to track.</span></span> 

     <span data-ttu-id="f81d1-142">**주파수** 및 **간격**을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="f81d1-143">이러한 설정은 논리 앱이 새 항목을 확인하는 빈도를 결정하고 시간 범위 동안 찾은 모든 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="f81d1-144">이 예제에서는 CNN 웹 사이트에 게시된 주요 기사를 매일 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-144">For this example, let's check every day for   top stories posted to the CNN website.</span></span>

     ![RSS 피드, 빈도 및 간격을 사용하여 트리거 설정](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="f81d1-146">이제 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-146">Save your work for now.</span></span> <span data-ttu-id="f81d1-147">(디자이너 명령 모음에서 **저장**을 선택합니다.)</span><span class="sxs-lookup"><span data-stu-id="f81d1-147">(On the designer command bar, choose **Save**.)</span></span>

   ![논리 앱 저장](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="f81d1-149">논리 앱을 저장하면 실시간으로 전송되지만 현재 논리 앱은 지정된 RSS 피드에서 새 항목을 확인하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in the specified RSS feed.</span></span> 
   <span data-ttu-id="f81d1-150">이 예제를 더 유용하게 사용하기 위해 트리거가 발생한 후에 논리 앱이 수행하는 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-150">To make this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-to-your-trigger"></a><span data-ttu-id="f81d1-151">트리거에 응답하는 작업 추가</span><span class="sxs-lookup"><span data-stu-id="f81d1-151">Add an action that responds to your trigger</span></span>

<span data-ttu-id="f81d1-152">[*작업*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)은 논리 앱 워크플로에서 수행하는 태스크입니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="f81d1-153">논리 앱에 트리거를 추가한 후에 해당 트리거에 의해 생성된 데이터를 사용하여 작업을 수행하는 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-153">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="f81d1-154">예를 들어 이제 웹 사이트의 RSS 피드에 새 항목이 표시되면 전자 메일을 보내는 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-154">For our example, we now add an action that sends email when new items appear in the website's RSS feed.</span></span>

1. <span data-ttu-id="f81d1-155">디자이너의 트리거 아래에서 **새 단계** > **작업 추가**를 다음과 같이 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-155">In the designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![작업 추가](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="f81d1-157">디자이너에서는 [사용 가능한 커넥터](../connectors/apis-list.md)를 표시하여 트리거가 발생할 때 수행할 작업을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-157">The designer shows [available connectors](../connectors/apis-list.md) so that you can select an action to perform when your trigger fires.</span></span>

2. <span data-ttu-id="f81d1-158">전자 메일 계정에 따라 Outlook 또는 Gmail에 대한 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-158">Based on your email account, follow the steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="f81d1-159">Outlook 계정에서 전자 메일을 보내려면 검색 상자에서 `outlook`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-159">To send email from your Outlook account, in the search box, enter `outlook`.</span></span> <span data-ttu-id="f81d1-160">**서비스** 아래에서 개인 Microsoft 계정에 **Outlook.com**을 선택하거나 Azure 회사 또는 학교 계정에 **Office 365 Outlook**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="f81d1-161">**작업** 아래에서 **전자 메일 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-161">Under **Actions**, select **Send an email**.</span></span>

       ![Outlook "전자 메일 보내기" 작업 선택](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="f81d1-163">Gmail 계정에서 전자 메일을 보내려면 검색 상자에서 `gmail`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-163">To send email from your Gmail account, in the search box, enter `gmail`.</span></span> 
   <span data-ttu-id="f81d1-164">**작업** 아래에서 **전자 메일 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-164">Under **Actions**, select **Send email**.</span></span>

       !["Gmail - 전자 메일 보내기" 선택](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="f81d1-166">자격 증명을 묻는 메시지가 표시되는 경우 전자 메일 계정의 사용자 이름 및 암호를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-166">When you're prompted for credentials, sign in with the username and password for your email account.</span></span> 

4. <span data-ttu-id="f81d1-167">예를 들어 대상 전자 메일 주소와 간이 이 작업에 대한 세부 정보를 제공하고 전자 메일에 포함할 데이터의 매개 변수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-167">Provide the details for this action, like the destination email address, and choose the parameters for the data to include in the email, for example:</span></span>

   ![전자 메일에 포함할 데이터 선택](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="f81d1-169">따라서 Outlook을 선택한 경우 논리 앱은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![완료된 논리 앱](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="f81d1-171">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-171">Save your changes.</span></span> <span data-ttu-id="f81d1-172">(디자이너 명령 모음에서 **저장**을 선택합니다.)</span><span class="sxs-lookup"><span data-stu-id="f81d1-172">(On the designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="f81d1-173">이제 테스트하기 위해 논리 앱을 수동으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="f81d1-174">디자이너 명령 모음에서 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-174">On the designer command bar, choose **Run**.</span></span> <span data-ttu-id="f81d1-175">그렇지 않은 경우 논리 앱에서 설정한 일정에 따라 지정된 RSS 피드를 확인하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-175">Otherwise, you can let your logic app check the specified RSS feed based on the schedule that you set up.</span></span>

   <span data-ttu-id="f81d1-176">논리 앱이 새 항목을 찾으면 선택한 데이터를 포함하는 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-176">If your logic app finds new items, the logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="f81d1-177">새 항목이 발견되면 논리 앱이 전자 메일을 보내는 작업을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-177">If no new items are found, your logic app skips the action that sends email.</span></span>

7. <span data-ttu-id="f81d1-178">논리 앱의 실행 및 트리거 기록을 모니터링하고 확인하려면 **개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-178">To monitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![논리 앱 실행 및 트리거 기록 모니터링 및 보기](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="f81d1-180">예상하는 데이터를 찾을 수 없는 경우 명령 모음에서 **새로 고침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-180">If you don't find the data that you expect, on the command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="f81d1-181">논리 앱의 상태 또는 실행 및 트리거 기록에 대한 자세한 내용을 알아보거나 논리 앱을 진단하려면 [논리 앱 문제 해결](logic-apps-diagnosing-failures.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f81d1-181">To learn more about your logic app's status or run and trigger history, or to diagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="f81d1-182">논리 앱은 앱을 해제할 때까지 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="f81d1-183">지금 앱을 해제하려면 논리 앱 메뉴에서 **개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-183">To turn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="f81d1-184">명령 모음에서 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-184">On the command bar, choose **Disable**.</span></span>

<span data-ttu-id="f81d1-185">축하드립니다. 첫 번째 기본 논리 앱을 설정하고 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="f81d1-186">또한 코드 없이 프로세스를 자동화하는 워크플로를 쉽게 만들고 클라우드 앱 및 클라우드 서비스를 통합하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="f81d1-187">논리 앱 관리</span><span class="sxs-lookup"><span data-stu-id="f81d1-187">Manage your logic app</span></span>

<span data-ttu-id="f81d1-188">앱을 관리하기 위해 상태 검사, 편집, 기록 보기, 해제 또는 논리 앱 삭제와 같은 태스크를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-188">To manage your app, you can perform tasks like check the status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="f81d1-189">[Azure Portal](https://portal.azure.com "Azure Portal")에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-189">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="f81d1-190">왼쪽 메뉴에서 **추가 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-190">On the left menu, choose **More services**.</span></span> <span data-ttu-id="f81d1-191">**엔터프라이즈 통합** 아래에서 **논리 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="f81d1-192">논리 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-192">Select your logic app.</span></span> 

   <span data-ttu-id="f81d1-193">논리 앱 메뉴에서 다음과 같은 논리 앱 관리 태스크를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-193">In the logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="f81d1-194">작업</span><span class="sxs-lookup"><span data-stu-id="f81d1-194">Task</span></span>|<span data-ttu-id="f81d1-195">단계</span><span class="sxs-lookup"><span data-stu-id="f81d1-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="f81d1-196">앱의 상태, 실행 기록 및 일반 정보 보기</span><span class="sxs-lookup"><span data-stu-id="f81d1-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="f81d1-197">**개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="f81d1-198">앱 편집</span><span class="sxs-lookup"><span data-stu-id="f81d1-198">Edit your app</span></span> | <span data-ttu-id="f81d1-199">**Logic App Designer**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="f81d1-200">앱의 워크플로 JSON 정의 보기</span><span class="sxs-lookup"><span data-stu-id="f81d1-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="f81d1-201">**Logic App 코드 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="f81d1-202">논리 앱에 수행된 작업 보기</span><span class="sxs-lookup"><span data-stu-id="f81d1-202">View operations performed on your logic app</span></span> | <span data-ttu-id="f81d1-203">**활동 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="f81d1-204">논리 앱의 이전 버전 보기</span><span class="sxs-lookup"><span data-stu-id="f81d1-204">View past versions for your logic app</span></span> | <span data-ttu-id="f81d1-205">**버전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="f81d1-206">일시적으로 앱 해제</span><span class="sxs-lookup"><span data-stu-id="f81d1-206">Turn off your app temporarily</span></span> | <span data-ttu-id="f81d1-207">**개요**를 선택한 다음 명령 모음에서 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-207">Choose **Overview**, then on the command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="f81d1-208">앱 삭제</span><span class="sxs-lookup"><span data-stu-id="f81d1-208">Delete your app</span></span> | <span data-ttu-id="f81d1-209">**개요**를 선택한 다음 명령 모음에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-209">Choose **Overview**, then on the command bar, choose **Delete**.</span></span> <span data-ttu-id="f81d1-210">논리 앱의 이름을 입력하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f81d1-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="f81d1-211">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="f81d1-211">Get help</span></span>

<span data-ttu-id="f81d1-212">질문하고, 질문에 답변하고, 다른 Azure Logic Apps 사용자가 어떤 일을 하는지 알아보려면 [Azure Logic Apps 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="f81d1-212">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="f81d1-213">Azure Logic Apps 및 커넥터 개선에 도움을 주려면 [Azure Logic Apps 사용자 의견 사이트](http://aka.ms/logicapps-wish)에서 투표하고 아이디어를 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="f81d1-213">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f81d1-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f81d1-214">Next steps</span></span>

*  [<span data-ttu-id="f81d1-215">조건 추가 및 워크플로 실행</span><span class="sxs-lookup"><span data-stu-id="f81d1-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="f81d1-216">논리 앱 템플릿</span><span class="sxs-lookup"><span data-stu-id="f81d1-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="f81d1-217">Azure Resource Manager 템플릿에서 논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f81d1-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
