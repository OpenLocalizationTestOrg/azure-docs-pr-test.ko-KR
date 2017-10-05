---
title: "가상 컴퓨터의 변경 사항 모니터링 - Azure Event Grid 및 Logic Apps | Microsoft Docs"
description: "Azure Event Grid와 Logic Apps를 사용하여 VM(가상 컴퓨터)의 구성 변경 사항을 확인합니다."
keywords: "논리 앱, 이벤트 표, 가상 컴퓨터, VM"
services: logic-apps
author: ecfan
manager: anneta
ms.assetid: 
ms.workload: logic-apps
ms.service: logic-apps
ms.topic: article
ms.date: 08/16/2017
ms.author: LADocs; estfan
ms.openlocfilehash: 4d4c16860dbec10162797a13c8f9f57106abd17f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a><span data-ttu-id="44091-104">Azure Event Grid와 Logic Apps를 사용하여 가상 컴퓨터의 변경 사항 모니터링</span><span class="sxs-lookup"><span data-stu-id="44091-104">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>

<span data-ttu-id="44091-105">Azure 리소스 또는 타사 리소스에서 특정 이벤트가 발생하는 경우 자동화된 [논리 앱 워크플로](../logic-apps/logic-apps-what-are-logic-apps.md)를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-105">You can start an automated [logic app workflow](../logic-apps/logic-apps-what-are-logic-apps.md) when specific events happen in Azure resources or third-party resources.</span></span> <span data-ttu-id="44091-106">이러한 리소스는 해당 이벤트를 [Azure Event Grid](../event-grid/overview.md)에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-106">These resources can publish those events to an [Azure event grid](../event-grid/overview.md).</span></span> <span data-ttu-id="44091-107">이에 따라 Event Grid에서는 큐, 웹후크 또는 [이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md)를 끝점으로 가지고 있는 구독자에게 해당 이벤트를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="44091-107">In turn, the event grid pushes those events to subscribers that have queues, webhooks, or [event hubs](../event-hubs/event-hubs-what-is-event-hubs.md) as endpoints.</span></span> <span data-ttu-id="44091-108">구독자로서 논리 앱은 코드를 작성하지 않고 자동화된 워크플로를 실행하여 작업을 수행하기 전에 Event Grid에서 이러한 이벤트를 기다릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-108">As a subscriber, your logic app can wait for those events from the event grid before running automated workflows to perform tasks - without you writing any code.</span></span>

<span data-ttu-id="44091-109">예를 들어 게시자가 Azure Event Grid 서비스를 통해 구독자에게 보낼 수 있는 몇 가지 이벤트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-109">For example, here are some events that publishers can send to subscribers through the Azure Event Grid service:</span></span>

* <span data-ttu-id="44091-110">리소스를 만들고, 읽고, 업데이트하거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-110">Create, read, update, or delete a resource.</span></span> <span data-ttu-id="44091-111">예를 들어 Azure 구독에 요금이 부과되어 청구서에 영향을 줄 수 있는 변경 사항을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-111">For example, you can monitor changes that might incur charges on your Azure subscription and affect your bill.</span></span> 
* <span data-ttu-id="44091-112">Azure 구독에서 사람을 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-112">Add or remove a person from an Azure subscription.</span></span>
* <span data-ttu-id="44091-113">앱에서 특정 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-113">Your app performs a particular action.</span></span>
* <span data-ttu-id="44091-114">새 메시지가 큐에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="44091-114">A new message appears in a queue.</span></span>

<span data-ttu-id="44091-115">이 자습서에서는 가상 컴퓨터의 변경 내용을 모니터링하고 이러한 변경에 대한 전자 메일을 보내는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44091-115">This tutorial creates a logic app that monitors changes to a virtual machine and sends emails about those changes.</span></span> <span data-ttu-id="44091-116">Azure 리소스에 대한 이벤트 구독이 있는 논리 앱을 만드는 경우 이벤트가 Event Grid를 통해 해당 리소스에서 논리 앱으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="44091-116">When you create a logic app with an event subscription for an Azure resource, events flow from that resource through an event grid to the logic app.</span></span> <span data-ttu-id="44091-117">자습서에서는 이 논리 앱을 구축하는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-117">The tutorial walks you through building this logic app:</span></span>

![개요 - Event Grid와 논리 앱으로 가상 컴퓨터 모니터링](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

<span data-ttu-id="44091-119">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="44091-119">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44091-120">Event Grid를 통해 이벤트를 모니터링하는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44091-120">Create a logic app that monitors events from an event grid.</span></span>
> * <span data-ttu-id="44091-121">특별히 가상 컴퓨터 변경 내용을 확인하는 조건을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-121">Add a condition that specifically checks for virtual machine changes.</span></span>
> * <span data-ttu-id="44091-122">가상 컴퓨터가 변경될 때 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="44091-122">Send email when your virtual machine changes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44091-123">필수 조건</span><span class="sxs-lookup"><span data-stu-id="44091-123">Prerequisites</span></span>

* <span data-ttu-id="44091-124">알림 전송을 위한 [Azure Logic Apps에서 지원하는 전자 메일 공급자](../connectors/apis-list.md)(예: Office 365 Outlook, Outlook.com 또는 Gmail)의 전자 메일 계정.</span><span class="sxs-lookup"><span data-stu-id="44091-124">An email account from [any email provider supported by Azure Logic Apps](../connectors/apis-list.md), such as Office 365 Outlook, Outlook.com, or Gmail, for sending notifications.</span></span> <span data-ttu-id="44091-125">이 자습서에서는 Office 365 Outlook을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-125">This tutorial uses Office 365 Outlook.</span></span>

* <span data-ttu-id="44091-126">[가상 컴퓨터](https://azure.microsoft.com/services/virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="44091-126">A [virtual machine](https://azure.microsoft.com/services/virtual-machines).</span></span> <span data-ttu-id="44091-127">가상 컴퓨터가 아직 없는 경우 [VM 만들기 자습서](https://docs.microsoft.com/azure/virtual-machines/)를 통해 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44091-127">If you haven't already done so, create a virtual machine through a [Create a VM tutorial](https://docs.microsoft.com/azure/virtual-machines/).</span></span> <span data-ttu-id="44091-128">가상 컴퓨터에서 이벤트를 게시하기 위해 [필요한 별도의 작업은 없습니다](../event-grid/overview.md).</span><span class="sxs-lookup"><span data-stu-id="44091-128">To make the virtual machine publish events, you [don't need to do anything else](../event-grid/overview.md).</span></span>

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a><span data-ttu-id="44091-129">Event Grid에서 이벤트를 모니터링하는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44091-129">Create a logic app that monitors events from an event grid</span></span>

<span data-ttu-id="44091-130">먼저 논리 앱을 만들고 가상 컴퓨터에 대한 리소스 그룹을 모니터링하는 Event Grid 트리거를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-130">First, create a logic app and add an Event grid trigger that monitors the resource group for your virtual machine.</span></span> 

1. <span data-ttu-id="44091-131">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-131">Sign in to the [Azure portal](https://portal.azure.com).</span></span> 

2. <span data-ttu-id="44091-132">Azure 주 메뉴의 왼쪽 위 모서리에서 **새로 만들기** > **엔터프라이즈 통합** > **논리 앱**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-132">From the upper left corner of the main Azure menu, choose **New** > **Enterprise Integration** > **Logic App**.</span></span>

   ![논리 앱 만들기](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. <span data-ttu-id="44091-134">다음 테이블에 지정된 설정을 사용하여 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44091-134">Create your logic app with the settings specified in the following table:</span></span>

   ![논리 앱 세부 정보 제공](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | <span data-ttu-id="44091-136">설정</span><span class="sxs-lookup"><span data-stu-id="44091-136">Setting</span></span> | <span data-ttu-id="44091-137">제안 값</span><span class="sxs-lookup"><span data-stu-id="44091-137">Suggested value</span></span> | <span data-ttu-id="44091-138">설명</span><span class="sxs-lookup"><span data-stu-id="44091-138">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="44091-139">**Name**</span><span class="sxs-lookup"><span data-stu-id="44091-139">**Name**</span></span> | <span data-ttu-id="44091-140">*{your-logic-app-name}*</span><span class="sxs-lookup"><span data-stu-id="44091-140">*{your-logic-app-name}*</span></span> | <span data-ttu-id="44091-141">고유한 논리 앱 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-141">Provide a unique logic app name.</span></span> | 
   | <span data-ttu-id="44091-142">**구독**</span><span class="sxs-lookup"><span data-stu-id="44091-142">**Subscription**</span></span> | <span data-ttu-id="44091-143">*{your-Azure-subscription}*</span><span class="sxs-lookup"><span data-stu-id="44091-143">*{your-Azure-subscription}*</span></span> | <span data-ttu-id="44091-144">이 자습서의 모든 서비스에 대해 동일한 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-144">Select the same Azure subscription for all services in this tutorial.</span></span> | 
   | <span data-ttu-id="44091-145">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="44091-145">**Resource group**</span></span> | <span data-ttu-id="44091-146">*{your-Azure-resource-group}*</span><span class="sxs-lookup"><span data-stu-id="44091-146">*{your-Azure-resource-group}*</span></span> | <span data-ttu-id="44091-147">이 자습서의 모든 서비스에 대해 동일한 Azure 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-147">Select the same Azure resource group for all services in this tutorial.</span></span> | 
   | <span data-ttu-id="44091-148">**위치**:</span><span class="sxs-lookup"><span data-stu-id="44091-148">**Location**</span></span> | <span data-ttu-id="44091-149">*{your-Azure-region}*</span><span class="sxs-lookup"><span data-stu-id="44091-149">*{your-Azure-region}*</span></span> | <span data-ttu-id="44091-150">이 자습서의 모든 서비스에 대해 동일한 하위 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-150">Select the same region for all services in this tutorial.</span></span> | 
   | | | 

4. <span data-ttu-id="44091-151">준비가 되면 **대시보드에 고정**을 선택하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-151">When you're ready, select **Pin to dashboard**, and choose **Create**.</span></span>

   <span data-ttu-id="44091-152">이제 논리 앱에 대한 Azure 리소스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-152">You've now created an Azure resource for your logic app.</span></span> 
   <span data-ttu-id="44091-153">Azure에서 논리 앱을 배포하면 Logic Apps 디자이너에서 일반적인 패턴에 대한 템플릿을 표시하므로 더 빨리 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-153">After Azure deploys your logic app, the Logic Apps Designer shows you templates for common patterns so you can get started faster.</span></span>

   > [!NOTE] 
   > <span data-ttu-id="44091-154">**대시보드에 고정**을 선택하면 Logic Apps 디자이너에서 해당 논리 앱이 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="44091-154">When you select **Pin to dashboard**, your logic app automatically opens in Logic Apps Designer.</span></span> <span data-ttu-id="44091-155">그렇지 않으면 논리 앱을 수동으로 찾아 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-155">Otherwise, you can manually find and open your logic app.</span></span>

5. <span data-ttu-id="44091-156">이제 논리 앱 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-156">Now choose a logic app template.</span></span> <span data-ttu-id="44091-157">**템플릿** 아래에서 **비어 있는 논리 앱**을 선택하면 논리 앱을 처음부터 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-157">Under **Templates**, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

   ![논리 앱 템플릿 선택](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   <span data-ttu-id="44091-159">이제 Logic Apps 디자이너에 논리 앱을 시작하는 데 사용할 수 있는 [*커넥터*](../connectors/apis-list.md) 및 [*트리거*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)와 함께 작업을 수행하기 위해 트리거 후에 추가할 수 있는 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="44091-159">The Logic Apps Designer now shows you [*connectors*](../connectors/apis-list.md) and [*triggers*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) that you can use to start your logic app, and also actions that you can add after a trigger to perform tasks.</span></span> <span data-ttu-id="44091-160">트리거는 논리 앱 인스턴스를 만들고 논리 앱 워크플로를 시작하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="44091-160">A trigger is an event that creates a logic app instance and starts your logic app workflow.</span></span> 
   <span data-ttu-id="44091-161">논리 앱에는 첫 번째 항목으로 트리거가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-161">Your logic app needs a trigger as the first item.</span></span>

6. <span data-ttu-id="44091-162">검색 상자에 필터로 "event grid"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-162">In the search box, enter "event grid" as your filter.</span></span> <span data-ttu-id="44091-163">**Azure Event Grid - On a resource event**(Azure Event Grid - 리소스 이벤트 시) 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-163">Select this trigger: **Azure Event Grid - On a resource event**</span></span>

   !["Azure Event Grid - On a resource event"(Azure Event Grid - 리소스 이벤트 시) 트리거 선택](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. <span data-ttu-id="44091-165">메시지가 표시되면 Azure 자격 증명을 사용하여 Azure Event Grid에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-165">When prompted, sign in to Azure Event Grid with your Azure credentials.</span></span>

   ![Azure 자격 증명으로 로그인](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > <span data-ttu-id="44091-167">@outlook.com 또는 @hotmail.com과 같은 개인 Microsoft 계정으로 로그인하는 경우 Event Grid 트리거가 제대로 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-167">If you're signed in with a personal Microsoft account, such as @outlook.com or @hotmail.com, the Event Grid trigger might not appear correctly.</span></span> <span data-ttu-id="44091-168">이 문제를 해결하기 위해 [서비스 주체와 연결](/azure-resource-manager/resource-group-create-service-principal-portal.md)을 선택하거나 Azure 구독과 연결된 Azure Active Directory의 구성원(예: *user-name*@emailoutlook.onmicrosoft.com)으로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-168">As a workaround, choose [Connect with Service Principal](/azure-resource-manager/resource-group-create-service-principal-portal.md), or authenticate as a member of the Azure Active Directory that's associated with your Azure subscription, for example, *user-name*@emailoutlook.onmicrosoft.com.</span></span>

8. <span data-ttu-id="44091-169">이제 논리 앱을 게시자 이벤트에 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-169">Now subscribe your logic app to publisher events.</span></span> <span data-ttu-id="44091-170">다음 테이블에 지정된 이벤트 구독에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-170">Provide the details for your event subscription as specified in the following table:</span></span>

   ![이벤트 구독에 대한 세부 정보 제공](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | <span data-ttu-id="44091-172">설정</span><span class="sxs-lookup"><span data-stu-id="44091-172">Setting</span></span> | <span data-ttu-id="44091-173">제안 값</span><span class="sxs-lookup"><span data-stu-id="44091-173">Suggested value</span></span> | <span data-ttu-id="44091-174">설명</span><span class="sxs-lookup"><span data-stu-id="44091-174">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="44091-175">**구독**</span><span class="sxs-lookup"><span data-stu-id="44091-175">**Subscription**</span></span> | <span data-ttu-id="44091-176">*{virtual-machine-Azure-subscription}*</span><span class="sxs-lookup"><span data-stu-id="44091-176">*{virtual-machine-Azure-subscription}*</span></span> | <span data-ttu-id="44091-177">이벤트 게시자의 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-177">Select the event publisher's Azure subscription.</span></span> <span data-ttu-id="44091-178">이 자습서에서는 가상 컴퓨터에 대한 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-178">For this tutorial, select the Azure subscription for your virtual machine.</span></span> | 
   | <span data-ttu-id="44091-179">**리소스 종류**</span><span class="sxs-lookup"><span data-stu-id="44091-179">**Resource Type**</span></span> | <span data-ttu-id="44091-180">Microsoft.Resources.resourceGroups</span><span class="sxs-lookup"><span data-stu-id="44091-180">Microsoft.Resources.resourceGroups</span></span> | <span data-ttu-id="44091-181">이벤트 게시자의 리소스 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-181">Select the event publisher's resource type.</span></span> <span data-ttu-id="44091-182">이 자습서의 경우 논리 앱이 리소스 그룹만 모니터링하도록 지정된 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-182">For this tutorial, select the specified value so your logic app monitors only resource groups.</span></span> | 
   | <span data-ttu-id="44091-183">**리소스 이름**</span><span class="sxs-lookup"><span data-stu-id="44091-183">**Resource Name**</span></span> | <span data-ttu-id="44091-184">*{virtual-machine-resource-group-name}*</span><span class="sxs-lookup"><span data-stu-id="44091-184">*{virtual-machine-resource-group-name}*</span></span> | <span data-ttu-id="44091-185">게시자의 리소스 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-185">Select the publisher's resource name.</span></span> <span data-ttu-id="44091-186">이 자습서에서는 가상 컴퓨터에 대한 리소스 그룹의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-186">For this tutorial, select the name of the resource group for your virtual machine.</span></span> | 
   | <span data-ttu-id="44091-187">옵션 설정의 경우 **고급 옵션 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-187">For optional settings, choose **Show advanced options**.</span></span> | <span data-ttu-id="44091-188">*{see descriptions}*</span><span class="sxs-lookup"><span data-stu-id="44091-188">*{see descriptions}*</span></span> | <span data-ttu-id="44091-189">* **접두사 필터**: 이 자습서에서는 이 설정을 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="44091-189">* **Prefix Filter**: For this tutorial, leave this setting empty.</span></span> <span data-ttu-id="44091-190">기본 동작은 모든 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-190">The default behavior matches all values.</span></span> <span data-ttu-id="44091-191">그러나 접두사 문자열(예: 특정 리소스에 대한 경로 및 매개 변수)을 필터로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-191">However, you can specify a prefix string as a filter, for example, a path and a parameter for a specific resource.</span></span> <p><span data-ttu-id="44091-192">* **접미사 필터**: 이 자습서에서는 이 설정을 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="44091-192">* **Suffix Filter**: For this tutorial, leave this setting empty.</span></span> <span data-ttu-id="44091-193">기본 동작은 모든 값과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-193">The default behavior matches all values.</span></span> <span data-ttu-id="44091-194">그러나 특정 파일 형식만 원하는 경우 접미사 문자열(예: 파일 이름 확장명)을 필터로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-194">However, you can specify a suffix string as a filter, for example, a file name extension, when you want only specific file types.</span></span><p><span data-ttu-id="44091-195">* **구독 이름**: 이벤트 구독에 대한 고유한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-195">* **Subscription Name**: Provide a unique name for your event subscription.</span></span> |
   | | | 

   <span data-ttu-id="44091-196">완료되면 Event Grid 트리거가 다음 예와 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="44091-196">When you're done, your event grid trigger might look like this example:</span></span>
   
   ![Event Grid 트리거 세부 정보의 예](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. <span data-ttu-id="44091-198">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-198">Save your logic app.</span></span> <span data-ttu-id="44091-199">디자이너 도구 모음에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-199">On the designer toolbar, choose **Save**.</span></span> <span data-ttu-id="44091-200">논리 앱에서 작업의 세부 정보를 접고 숨기려면 작업의 제목 표시줄을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-200">To collapse and hide an action's details in your logic app, choose the action's title bar.</span></span>

   ![논리 앱 저장](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   <span data-ttu-id="44091-202">Event Grid 트리거가 있는 논리 앱을 저장하면 Azure에서 사용자가 선택한 리소스에 대한 논리 앱의 이벤트 구독을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44091-202">When you save your logic app with an event grid trigger, Azure automatically creates an event subscription for your logic app to your selected resource.</span></span> <span data-ttu-id="44091-203">따라서 리소스가 이벤트를 Event Grid에 게시하면 이 Event Grid는 해당 이벤트를 논리 앱에 자동으로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-203">So when the resource publishes an event to the event grid, that event grid automatically pushes the event to your logic app.</span></span> <span data-ttu-id="44091-204">이 이벤트는 다음 단계에서 정의하는 워크플로의 인스턴스를 만들고 실행하는 논리 앱을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-204">This event triggers your logic app, then creates and runs an instance of the workflow that you define in these next steps.</span></span>

<span data-ttu-id="44091-205">논리 앱이 현재 라이브 상태이며 Event Grid의 이벤트를 수신 대기하지만, 워크플로에 작업을 추가하기 전까지는 아무 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-205">Your logic app is now live and listens to events from the event grid, but doesn't do anything until you add actions to the workflow.</span></span> 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a><span data-ttu-id="44091-206">가상 컴퓨터의 변경 사항을 확인하는 조건 추가</span><span class="sxs-lookup"><span data-stu-id="44091-206">Add a condition that checks for virtual machine changes</span></span>

<span data-ttu-id="44091-207">특정 이벤트가 발생할 때만 논리 앱 워크플로를 실행하려면 가상 컴퓨터 “쓰기” 작업을 확인하는 조건을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-207">To run your logic app workflow only when a specific event happens, add a condition that checks for virtual machine "write" operations.</span></span> <span data-ttu-id="44091-208">이 조건이 true인 경우 논리 앱에서 업데이트된 가상 컴퓨터에 대한 세부 정보가 포함된 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="44091-208">When this condition is true, your logic app sends you email with details about the updated virtual machine.</span></span>

1. <span data-ttu-id="44091-209">논리 앱 디자이너의 Event Grid 트리거 아래에서 **새 단계** > **조건 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-209">In Logic App Designer, under the event grid trigger, choose **New step** > **Add a condition**.</span></span>

   ![논리 앱에 조건 추가](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   <span data-ttu-id="44091-211">Logic Apps 디자이너에서는 조건이 참인지 거짓인지를 기준으로 따라야 할 작업 경로를 포함하여 워크플로에 조건을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-211">The Logic App Designer adds an empty condition to your workflow, including action paths to follow based whether the condition is true or false.</span></span>

   ![빈 조건](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. <span data-ttu-id="44091-213">**조건** 상자에서 **고급 모드에서 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-213">In the **Condition** box, choose **Edit in advanced mode**.</span></span>
<span data-ttu-id="44091-214">다음 식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-214">Enter this expression:</span></span>

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   <span data-ttu-id="44091-215">이제 조건은 다음 예와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-215">Your condition now looks like this example:</span></span>

   ![빈 조건](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   <span data-ttu-id="44091-217">이 식은 `operationName` 속성이 `Microsoft.Compute/virtualMachines/write` 작업인 `data` 개체에 대해 `body` 이벤트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-217">This expression checks the event `body` for a `data` object where the `operationName` property is the `Microsoft.Compute/virtualMachines/write` operation.</span></span> 
   <span data-ttu-id="44091-218">[Event Grid 이벤트 스키마](../event-grid/event-schema.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="44091-218">Learn more about [Event Grid event schema](../event-grid/event-schema.md).</span></span>

3. <span data-ttu-id="44091-219">조건에 대한 설명을 제공하려면 조건 셰이프에서 **줄임표**(**...**) 단추를 선택한 다음 **이름 바꾸기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-219">To provide a description for the condition, choose the **ellipses** (**...**) button on the condition shape, then choose **Rename**.</span></span>

   > [!NOTE] 
   > <span data-ttu-id="44091-220">또한 이 자습서의 뒷부분에 나오는 예제에는 논리 앱 워크플로의 단계에 대한 설명이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-220">The later examples in this tutorial also provide descriptions for steps in the logic app workflow.</span></span>

4. <span data-ttu-id="44091-221">이제 **기본 모드에서 편집**을 선택하여 다음과 같이 식이 자동으로 해결되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-221">Now choose **Edit in basic mode** so that the expression automatically resolves as shown:</span></span>

   ![논리 앱 조건](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. <span data-ttu-id="44091-223">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-223">Save your logic app.</span></span>

## <a name="send-email-when-your-virtual-machine-changes"></a><span data-ttu-id="44091-224">가상 컴퓨터가 변경될 때 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="44091-224">Send email when your virtual machine changes</span></span>

<span data-ttu-id="44091-225">이제 지정한 조건이 true일 때 전자 메일을 받을 수 있도록 [*작업*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-225">Now add an [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) so that you get an email when the specified condition is true.</span></span>

1. <span data-ttu-id="44091-226">조건의 **참인 경우** 상자에서 **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-226">In the condition's **If true** box, choose **Add an action**.</span></span>

   ![조건이 true인 경우의 작업 추가](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. <span data-ttu-id="44091-228">검색 상자에서 필터로 “전자 메일”을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-228">In the search box, enter "email" as your filter.</span></span> <span data-ttu-id="44091-229">전자 메일 공급자에 따라 일치하는 커넥터를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-229">Based on your email provider, find and select the matching connector.</span></span> <span data-ttu-id="44091-230">그런 다음 커넥터에 대한 "전자 메일 보내기" 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-230">Then select the "send email" action for your connector.</span></span> <span data-ttu-id="44091-231">예:</span><span class="sxs-lookup"><span data-stu-id="44091-231">For example:</span></span> 

   * <span data-ttu-id="44091-232">예를 들어 Azure 회사 또는 학교 계정의 경우 Office 365 Outlook 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-232">For an Azure work or school account, select the Office 365 Outlook connector.</span></span> 
   * <span data-ttu-id="44091-233">Microsoft 개인 계정의 경우 Outlook.com 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-233">For personal Microsoft accounts, select the Outlook.com connector.</span></span> 
   * <span data-ttu-id="44091-234">Gmail 계정의 경우 Gmail 커넥터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-234">For Gmail accounts, select the Gmail connector.</span></span> 

   <span data-ttu-id="44091-235">Office 365 Outlook 커넥터를 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-235">We're going to continue with the Office 365 Outlook connector.</span></span> 
   <span data-ttu-id="44091-236">다른 공급자를 사용하는 경우 단계는 동일하지만 UI의 표시가 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-236">If you use a different provider, the steps remain the same, but your UI might appear different.</span></span> 

   !["전자 메일 보내기" 작업 선택](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. <span data-ttu-id="44091-238">전자 메일 공급자에 대한 연결이 아직 없는 경우 인증을 요청받을 때 전자 메일 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-238">If you don't already have a connection for your email provider, sign in to your email account when you're asked for authentication.</span></span>

4. <span data-ttu-id="44091-239">다음 테이블에 지정된 대로 전자 메일에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-239">Provide details for the email as specified in the following table:</span></span>

   ![빈 전자 메일 작업](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > <span data-ttu-id="44091-241">워크플로에 사용할 수 있는 필드를 선택하려면 **동적 콘텐츠** 목록이 열리는 편집 상자를 클릭하거나 **동적 콘텐츠 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-241">To select from fields available in your workflow, click in an edit box so that the **Dynamic content** list opens, or choose **Add dynamic content**.</span></span> <span data-ttu-id="44091-242">더 많은 필드는 목록에서 각 섹션에 대한 **자세히 보기**를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="44091-242">For more fields, choose **See more** for each section in the list.</span></span> <span data-ttu-id="44091-243">**동적 콘텐츠** 목록을 닫으려면 **동적 콘텐츠 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-243">To close the **Dynamic content** list, choose **Add dynamic content**.</span></span>

   | <span data-ttu-id="44091-244">설정</span><span class="sxs-lookup"><span data-stu-id="44091-244">Setting</span></span> | <span data-ttu-id="44091-245">제안 값</span><span class="sxs-lookup"><span data-stu-id="44091-245">Suggested value</span></span> | <span data-ttu-id="44091-246">설명</span><span class="sxs-lookup"><span data-stu-id="44091-246">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="44091-247">**To**</span><span class="sxs-lookup"><span data-stu-id="44091-247">**To**</span></span> | <span data-ttu-id="44091-248">*{recipient-email-address}*</span><span class="sxs-lookup"><span data-stu-id="44091-248">*{recipient-email-address}*</span></span> |<span data-ttu-id="44091-249">수신자의 이메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-249">Enter the recipient's email address.</span></span> <span data-ttu-id="44091-250">자신의 이메일 주소를 사용하여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-250">For testing purposes, you can use your own email address.</span></span> | 
   | <span data-ttu-id="44091-251">**제목**</span><span class="sxs-lookup"><span data-stu-id="44091-251">**Subject**</span></span> | <span data-ttu-id="44091-252">업데이트된 리소스: **제목**</span><span class="sxs-lookup"><span data-stu-id="44091-252">Resource updated: **Subject**</span></span>| <span data-ttu-id="44091-253">전자 메일의 제목에 콘텐츠를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-253">Enter the content for the email's subject.</span></span> <span data-ttu-id="44091-254">이 자습서의 경우 제안된 텍스트를 입력하고 이벤트의 **제목** 필드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-254">For this tutorial, enter the suggested text and select the event's **Subject** field.</span></span> <span data-ttu-id="44091-255">여기에서 전자 메일 제목에는 업데이트된 리소스(가상 컴퓨터)에 대한 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="44091-255">Here, your email subject includes the name for the updated resource (virtual machine).</span></span> | 
   | <span data-ttu-id="44091-256">**본문**</span><span class="sxs-lookup"><span data-stu-id="44091-256">**Body**</span></span> | <span data-ttu-id="44091-257">리소스 그룹: **토픽**</span><span class="sxs-lookup"><span data-stu-id="44091-257">Resource group: **Topic**</span></span> <p><span data-ttu-id="44091-258">이벤트 유형: **이벤트 유형**</span><span class="sxs-lookup"><span data-stu-id="44091-258">Event type: **Event Type**</span></span><p><span data-ttu-id="44091-259">이벤트 ID: **ID**</span><span class="sxs-lookup"><span data-stu-id="44091-259">Event ID: **ID**</span></span><p><span data-ttu-id="44091-260">시간: **이벤트 시간**</span><span class="sxs-lookup"><span data-stu-id="44091-260">Time: **Event Time**</span></span> | <span data-ttu-id="44091-261">전자 메일의 본문에 콘텐츠를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-261">Enter the content for the email's body.</span></span> <span data-ttu-id="44091-262">이 자습서의 경우 제안된 텍스트를 입력하고 이벤트의 **토픽**, **이벤트 유형**, **ID** 및 **이벤트 시간** 필드를 선택하여 업데이트에 대한 리소스 그룹 이름, 이벤트 유형, 이벤트 타임스탬프 및 이벤트 ID가 전자 메일에 포함되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-262">For this tutorial, enter the suggested text and select the event's **Topic**, **Event Type**, **ID**, and **Event Time** fields so that your email includes the resource group name, event type, event timestamp, and event ID for the update.</span></span> <p><span data-ttu-id="44091-263">콘텐츠에 빈 줄을 추가하려면 Shift + Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="44091-263">To add blank lines in your content, press Shift + Enter.</span></span> | 
   | | | 

   > [!NOTE] 
   > <span data-ttu-id="44091-264">배열을 나타내는 필드를 선택하면 디자이너에서 배열을 참조하는 작업 주위에 **For each** 루프를 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-264">If you select a field that represents an array, the designer automatically adds a **For each** loop around the action that references the array.</span></span> <span data-ttu-id="44091-265">그렇게 하면 논리 앱에서 각 배열 항목에 대한 해당 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-265">That way, your logic app performs that action on each array item.</span></span>

   <span data-ttu-id="44091-266">이제 전자 메일 작업이 다음 예와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="44091-266">Now, your email action might look like this example:</span></span>

   ![전자 메일에 포함될 출력 선택](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   <span data-ttu-id="44091-268">완료된 논리 앱이 다음 예와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="44091-268">And your finished logic app might look like this example:</span></span>

   ![완료된 논리 앱](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. <span data-ttu-id="44091-270">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-270">Save your logic app.</span></span> <span data-ttu-id="44091-271">논리 앱에서 각 작업의 세부 정보를 접고 숨기려면 작업의 제목 표시줄을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-271">To collapse and hide each action's details in your logic app, choose the action's title bar.</span></span>

   ![논리 앱 저장](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   <span data-ttu-id="44091-273">논리 앱은 현재 라이브 상태이지만 가상 컴퓨터에 변경 사항이 있을 때까지 아무 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-273">Your logic app is now live, but waits for changes to your virtual machine before doing anything.</span></span> 
   <span data-ttu-id="44091-274">이제 논리 앱을 테스트하려면 다음 섹션으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="44091-274">To test your logic app now, continue to the next section.</span></span>

## <a name="test-your-logic-app-workflow"></a><span data-ttu-id="44091-275">논리 앱 워크플로 테스트</span><span class="sxs-lookup"><span data-stu-id="44091-275">Test your logic app workflow</span></span>

1. <span data-ttu-id="44091-276">지정한 이벤트를 논리 앱에서 받고 있는지 확인하려면 가상 컴퓨터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-276">To check that your logic app is getting the specified events, update your virtual machine.</span></span> 

   <span data-ttu-id="44091-277">예를 들어 Azure Portal에서 가상 컴퓨터의 크기를 조정하거나 [Azure PowerShell로 VM 크기를 조정](../virtual-machines/windows/resize-vm.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-277">For example, you can resize your virtual machine in the Azure portal or [resize your VM with Azure PowerShell](../virtual-machines/windows/resize-vm.md).</span></span> 

   <span data-ttu-id="44091-278">몇 분 후에 전자 메일을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-278">After a few moments, you should get an email.</span></span> <span data-ttu-id="44091-279">예:</span><span class="sxs-lookup"><span data-stu-id="44091-279">For example:</span></span>

   ![가상 컴퓨터 업데이트에 대한 전자 메일](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. <span data-ttu-id="44091-281">논리 앱에 대한 실행 및 트리거 기록을 검토하려면 논리 앱 메뉴에서 **개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-281">To review the runs and trigger history for your logic app, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="44091-282">실행에 대한 자세한 세부 정보를 보려면 해당 실행에 대한 행을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-282">To view more details about a run, choose the row for that run.</span></span>

   ![논리 앱 실행 기록](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. <span data-ttu-id="44091-284">각 단계에 대한 입력 및 출력을 보려면 검토하려는 단계를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-284">To view the inputs and outputs for each step, expand the step that you want to review.</span></span> <span data-ttu-id="44091-285">이 정보는 논리 앱의 문제를 진단하고 디버깅하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-285">This information can help you diagnose and debug problems in your logic app.</span></span>
 
   ![논리 앱 실행 기록 세부 정보](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

<span data-ttu-id="44091-287">축하합니다! Event Grid를 통해 리소스 이벤트를 모니터링하고 이러한 이벤트가 발생하면 전자 메일을 보내는 논리 앱을 만들고 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-287">Congratulations, you've created and run a logic app that monitors resource events through an event grid and emails you when those events happen.</span></span> <span data-ttu-id="44091-288">또한 프로세스를 자동화하고 시스템과 클라우드 서비스를 통합하는 워크플로를 쉽게 만들 수 있는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-288">You also learned how easily you can create workflows that automate processes and integrate systems and cloud services.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="44091-289">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="44091-289">Clean up resources</span></span>

<span data-ttu-id="44091-290">이 자습서에서는 리소스를 사용하고 Azure 구독에 요금을 부과하는 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-290">This tutorial uses resources and performs actions that incur charges on your Azure subscription.</span></span> <span data-ttu-id="44091-291">따라서 이 자습서를 완료하고 테스트할 때 요금이 부과되지 않도록 리소스를 사용하지 않도록 설정하거나 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-291">So when you're done with the tutorial and testing, make sure that you disable or delete any resources where you don't want to incur charges.</span></span>

<span data-ttu-id="44091-292">앱을 삭제하지 않고도 논리 앱을 중지하여 실행되거나 전자 메일을 보내지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-292">You can stop your logic app from running and sending email without deleting the app.</span></span> <span data-ttu-id="44091-293">논리 앱 메뉴에서 **개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-293">On your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="44091-294">도구 모음에서 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="44091-294">On the toolbar, choose **Disable**.</span></span>

![논리 앱 사용 해제](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a><span data-ttu-id="44091-296">FAQ</span><span class="sxs-lookup"><span data-stu-id="44091-296">FAQ</span></span>

<span data-ttu-id="44091-297">**Q**: Event Grid 및 논리 앱으로 수행할 수 있는 다른 가상 컴퓨터 모니터링 작업은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="44091-297">**Q**: What other virtual machine monitoring tasks can I perform with event grids and logic apps?</span></span> </br><span data-ttu-id="44091-298">
**A**: 다음과 같이 다른 구성 변경 내용을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-298">
**A**: You can monitor other configuration changes, for example:</span></span>

* <span data-ttu-id="44091-299">가상 컴퓨터에서 RBAC(역할 기반 액세스 제어) 권한을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="44091-299">A virtual machine gets role-based access control (RBAC) rights.</span></span>
* <span data-ttu-id="44091-300">NIC(네트워크 인터페이스)의 NSG(네트워크 보안 그룹)가 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-300">Changes are made to a network security group (NSG) on a network interface (NIC).</span></span>
* <span data-ttu-id="44091-301">가상 컴퓨터용 디스크가 추가되거나 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-301">Disks for a virtual machine are added or removed.</span></span>
* <span data-ttu-id="44091-302">공용 IP 주소가 가상 컴퓨터 NIC에 할당되었습니다.</span><span class="sxs-lookup"><span data-stu-id="44091-302">A public IP address is assigned to a virtual machine NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44091-303">다음 단계</span><span class="sxs-lookup"><span data-stu-id="44091-303">Next steps</span></span>

* [<span data-ttu-id="44091-304">Event Grid 개요</span><span class="sxs-lookup"><span data-stu-id="44091-304">Event Grid Overview</span></span>](../event-grid/overview.md)
* [<span data-ttu-id="44091-305">Event Grid 개념</span><span class="sxs-lookup"><span data-stu-id="44091-305">Event Grid Concepts</span></span>](../event-grid/concepts.md)
* [<span data-ttu-id="44091-306">빠른 시작: Event Grid로 사용자 지정 이벤트 만들기 및 라우팅</span><span class="sxs-lookup"><span data-stu-id="44091-306">Quickstart: Create and route custom events with Event Grid</span></span>](../event-grid/custom-event-quickstart.md)
* [<span data-ttu-id="44091-307">Event Grid 이벤트 스키마</span><span class="sxs-lookup"><span data-stu-id="44091-307">Event Grid event schema</span></span>](../event-grid/event-schema.md)
* [<span data-ttu-id="44091-308">Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="44091-308">Azure Logic Apps</span></span>](../logic-apps/logic-apps-what-are-logic-apps.md)
* [<span data-ttu-id="44091-309">미리 정의된 템플릿을 사용하여 논리 앱 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="44091-309">Create logic app workflows with predefined templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)