---
title: "aaaMonitor 가상 컴퓨터 변경-Azure 이벤트 표 형태 및 논리 앱 | Microsoft Docs"
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
ms.openlocfilehash: f0633e598be6e7880a310e6f8e64f6738cc692b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a><span data-ttu-id="f48b9-104">Azure Event Grid와 Logic Apps를 사용하여 가상 컴퓨터의 변경 사항 모니터링</span><span class="sxs-lookup"><span data-stu-id="f48b9-104">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>

<span data-ttu-id="f48b9-105">Azure 리소스 또는 타사 리소스에서 특정 이벤트가 발생하는 경우 자동화된 [논리 앱 워크플로](../logic-apps/logic-apps-what-are-logic-apps.md)를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-105">You can start an automated [logic app workflow](../logic-apps/logic-apps-what-are-logic-apps.md) when specific events happen in Azure resources or third-party resources.</span></span> <span data-ttu-id="f48b9-106">이러한 리소스는 해당 이벤트 tooan 게시할 수 [Azure 이벤트 표 형태](../event-grid/overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-106">These resources can publish those events tooan [Azure event grid](../event-grid/overview.md).</span></span> <span data-ttu-id="f48b9-107">차례로 hello 이벤트 표 형태 푸시 webhook을 큐에 있는 해당 이벤트 toosubscribers 또는 [이벤트 허브](../event-hubs/event-hubs-what-is-event-hubs.md) 끝점으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-107">In turn, hello event grid pushes those events toosubscribers that have queues, webhooks, or [event hubs](../event-hubs/event-hubs-what-is-event-hubs.md) as endpoints.</span></span> <span data-ttu-id="f48b9-108">구독자 논리 앱 hello 이벤트 표 형태에서 이러한 이벤트에 대 한 모든 코드를 작성 하지 않고 tooperform 작업-자동화 된 워크플로 실행 하기 전에 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-108">As a subscriber, your logic app can wait for those events from hello event grid before running automated workflows tooperform tasks - without you writing any code.</span></span>

<span data-ttu-id="f48b9-109">예를 들어 다음은 게시자 toosubscribers hello 이벤트 표 형태 Azure 서비스를 통해 보낼 수 있음을 일부 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-109">For example, here are some events that publishers can send toosubscribers through hello Azure Event Grid service:</span></span>

* <span data-ttu-id="f48b9-110">리소스를 만들고, 읽고, 업데이트하거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-110">Create, read, update, or delete a resource.</span></span> <span data-ttu-id="f48b9-111">예를 들어 Azure 구독에 요금이 부과되어 청구서에 영향을 줄 수 있는 변경 사항을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-111">For example, you can monitor changes that might incur charges on your Azure subscription and affect your bill.</span></span> 
* <span data-ttu-id="f48b9-112">Azure 구독에서 사람을 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-112">Add or remove a person from an Azure subscription.</span></span>
* <span data-ttu-id="f48b9-113">앱에서 특정 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-113">Your app performs a particular action.</span></span>
* <span data-ttu-id="f48b9-114">새 메시지가 큐에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-114">A new message appears in a queue.</span></span>

<span data-ttu-id="f48b9-115">이 자습서에서는 변경 내용을 tooa 가상 컴퓨터를 모니터링 하 고 이러한 변경에 대 한 전자 메일을 전송 하는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-115">This tutorial creates a logic app that monitors changes tooa virtual machine and sends emails about those changes.</span></span> <span data-ttu-id="f48b9-116">Azure 리소스에 대 한 이벤트 구독 사용 하 여 논리 앱을 만들 때 이벤트를 이벤트 표 형태 toohello 논리가 응용 프로그램을 통해 해당 리소스에서 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-116">When you create a logic app with an event subscription for an Azure resource, events flow from that resource through an event grid toohello logic app.</span></span> <span data-ttu-id="f48b9-117">hello 자습서가 논리 앱을 구축 하는 과정을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-117">hello tutorial walks you through building this logic app:</span></span>

![개요 - Event Grid와 논리 앱으로 가상 컴퓨터 모니터링](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

<span data-ttu-id="f48b9-119">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-119">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f48b9-120">Event Grid를 통해 이벤트를 모니터링하는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-120">Create a logic app that monitors events from an event grid.</span></span>
> * <span data-ttu-id="f48b9-121">특별히 가상 컴퓨터 변경 내용을 확인하는 조건을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-121">Add a condition that specifically checks for virtual machine changes.</span></span>
> * <span data-ttu-id="f48b9-122">가상 컴퓨터가 변경될 때 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-122">Send email when your virtual machine changes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f48b9-123">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f48b9-123">Prerequisites</span></span>

* <span data-ttu-id="f48b9-124">알림 전송을 위한 [Azure Logic Apps에서 지원하는 전자 메일 공급자](../connectors/apis-list.md)(예: Office 365 Outlook, Outlook.com 또는 Gmail)의 전자 메일 계정.</span><span class="sxs-lookup"><span data-stu-id="f48b9-124">An email account from [any email provider supported by Azure Logic Apps](../connectors/apis-list.md), such as Office 365 Outlook, Outlook.com, or Gmail, for sending notifications.</span></span> <span data-ttu-id="f48b9-125">이 자습서에서는 Office 365 Outlook을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-125">This tutorial uses Office 365 Outlook.</span></span>

* <span data-ttu-id="f48b9-126">[가상 컴퓨터](https://azure.microsoft.com/services/virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="f48b9-126">A [virtual machine](https://azure.microsoft.com/services/virtual-machines).</span></span> <span data-ttu-id="f48b9-127">가상 컴퓨터가 아직 없는 경우 [VM 만들기 자습서](https://docs.microsoft.com/azure/virtual-machines/)를 통해 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-127">If you haven't already done so, create a virtual machine through a [Create a VM tutorial](https://docs.microsoft.com/azure/virtual-machines/).</span></span> <span data-ttu-id="f48b9-128">toomake hello 가상 컴퓨터 이벤트를 게시 하면 [다른 무엇 toodo 필요 하지 않은](../event-grid/overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-128">toomake hello virtual machine publish events, you [don't need toodo anything else](../event-grid/overview.md).</span></span>

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a><span data-ttu-id="f48b9-129">Event Grid에서 이벤트를 모니터링하는 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-129">Create a logic app that monitors events from an event grid</span></span>

<span data-ttu-id="f48b9-130">첫째, 논리 앱 만들고 hello 리소스 그룹에서 가상 컴퓨터에 대 한 모니터링 하는 이벤트 표 트리거를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-130">First, create a logic app and add an Event grid trigger that monitors hello resource group for your virtual machine.</span></span> 

1. <span data-ttu-id="f48b9-131">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-131">Sign in toohello [Azure portal](https://portal.azure.com).</span></span> 

2. <span data-ttu-id="f48b9-132">Hello 왼쪽된 위 모서리의 hello 주 Azure 메뉴에서 선택 **새로** > **엔터프라이즈 통합** > **논리 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-132">From hello upper left corner of hello main Azure menu, choose **New** > **Enterprise Integration** > **Logic App**.</span></span>

   ![논리 앱 만들기](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. <span data-ttu-id="f48b9-134">다음 표에 hello에 지정 된 hello 설정을 사용 하 여 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-134">Create your logic app with hello settings specified in hello following table:</span></span>

   ![논리 앱 세부 정보 제공](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | <span data-ttu-id="f48b9-136">설정</span><span class="sxs-lookup"><span data-stu-id="f48b9-136">Setting</span></span> | <span data-ttu-id="f48b9-137">제안 값</span><span class="sxs-lookup"><span data-stu-id="f48b9-137">Suggested value</span></span> | <span data-ttu-id="f48b9-138">설명</span><span class="sxs-lookup"><span data-stu-id="f48b9-138">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="f48b9-139">**Name**</span><span class="sxs-lookup"><span data-stu-id="f48b9-139">**Name**</span></span> | <span data-ttu-id="f48b9-140">*{your-logic-app-name}*</span><span class="sxs-lookup"><span data-stu-id="f48b9-140">*{your-logic-app-name}*</span></span> | <span data-ttu-id="f48b9-141">고유한 논리 앱 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-141">Provide a unique logic app name.</span></span> | 
   | <span data-ttu-id="f48b9-142">**구독**</span><span class="sxs-lookup"><span data-stu-id="f48b9-142">**Subscription**</span></span> | <span data-ttu-id="f48b9-143">*{your-Azure-subscription}*</span><span class="sxs-lookup"><span data-stu-id="f48b9-143">*{your-Azure-subscription}*</span></span> | <span data-ttu-id="f48b9-144">선택 hello이 자습서의 모든 서비스에 대해 동일한 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="f48b9-144">Select hello same Azure subscription for all services in this tutorial.</span></span> | 
   | <span data-ttu-id="f48b9-145">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="f48b9-145">**Resource group**</span></span> | <span data-ttu-id="f48b9-146">*{your-Azure-resource-group}*</span><span class="sxs-lookup"><span data-stu-id="f48b9-146">*{your-Azure-resource-group}*</span></span> | <span data-ttu-id="f48b9-147">선택이이 자습서의 모든 서비스에 대해 같은 Azure 리소스 그룹을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-147">Select hello same Azure resource group for all services in this tutorial.</span></span> | 
   | <span data-ttu-id="f48b9-148">**위치**:</span><span class="sxs-lookup"><span data-stu-id="f48b9-148">**Location**</span></span> | <span data-ttu-id="f48b9-149">*{your-Azure-region}*</span><span class="sxs-lookup"><span data-stu-id="f48b9-149">*{your-Azure-region}*</span></span> | <span data-ttu-id="f48b9-150">선택이이 자습서의 모든 서비스에 대해 동일한 지역을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-150">Select hello same region for all services in this tutorial.</span></span> | 
   | | | 

4. <span data-ttu-id="f48b9-151">준비 되 면 선택 **Pin toodashboard**, 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-151">When you're ready, select **Pin toodashboard**, and choose **Create**.</span></span>

   <span data-ttu-id="f48b9-152">이제 논리 앱에 대한 Azure 리소스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-152">You've now created an Azure resource for your logic app.</span></span> 
   <span data-ttu-id="f48b9-153">Azure 논리 앱을 배포 후 hello 논리 앱 디자이너를 보면 일반적인 패턴에 대 한 템플릿을 더 빠르게 시작할 수 있도록 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-153">After Azure deploys your logic app, hello Logic Apps Designer shows you templates for common patterns so you can get started faster.</span></span>

   > [!NOTE] 
   > <span data-ttu-id="f48b9-154">선택 하는 경우 **Pin toodashboard**, 논리 앱 논리 앱 디자이너에서 자동으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-154">When you select **Pin toodashboard**, your logic app automatically opens in Logic Apps Designer.</span></span> <span data-ttu-id="f48b9-155">그렇지 않으면 논리 앱을 수동으로 찾아 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-155">Otherwise, you can manually find and open your logic app.</span></span>

5. <span data-ttu-id="f48b9-156">이제 논리 앱 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-156">Now choose a logic app template.</span></span> <span data-ttu-id="f48b9-157">**템플릿** 아래에서 **비어 있는 논리 앱**을 선택하면 논리 앱을 처음부터 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-157">Under **Templates**, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

   ![논리 앱 템플릿 선택](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   <span data-ttu-id="f48b9-159">이제 표시 hello 논리 앱 디자이너 [ *커넥터* ](../connectors/apis-list.md) 및 [ *트리거* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) 논리 앱과도 동작 toostart를 사용할 수 있는 트리거 tooperform 작업 후 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-159">hello Logic Apps Designer now shows you [*connectors*](../connectors/apis-list.md) and [*triggers*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) that you can use toostart your logic app, and also actions that you can add after a trigger tooperform tasks.</span></span> <span data-ttu-id="f48b9-160">트리거는 논리 앱 인스턴스를 만들고 논리 앱 워크플로를 시작하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-160">A trigger is an event that creates a logic app instance and starts your logic app workflow.</span></span> 
   <span data-ttu-id="f48b9-161">논리 앱 hello 첫 번째 항목으로 트리거를 프로비저닝해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-161">Your logic app needs a trigger as hello first item.</span></span>

6. <span data-ttu-id="f48b9-162">Hello 검색 상자에 필터로 "이벤트 표 형태"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-162">In hello search box, enter "event grid" as your filter.</span></span> <span data-ttu-id="f48b9-163">**Azure Event Grid - On a resource event**(Azure Event Grid - 리소스 이벤트 시) 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-163">Select this trigger: **Azure Event Grid - On a resource event**</span></span>

   !["Azure Event Grid - On a resource event"(Azure Event Grid - 리소스 이벤트 시) 트리거 선택](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. <span data-ttu-id="f48b9-165">메시지가 표시 되 면 Azure 자격 증명으로 tooAzure 이벤트 표 형태에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-165">When prompted, sign in tooAzure Event Grid with your Azure credentials.</span></span>

   ![Azure 자격 증명으로 로그인](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > <span data-ttu-id="f48b9-167">하는 경우 로그인 개인 Microsoft 계정으로 같은 @outlook.com 또는 @hotmail.com, hello 이벤트 표 형태 트리거가 제대로 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-167">If you're signed in with a personal Microsoft account, such as @outlook.com or @hotmail.com, hello Event Grid trigger might not appear correctly.</span></span> <span data-ttu-id="f48b9-168">이 문제를 해결 선택 [서비스 사용자와 연결](/azure-resource-manager/resource-group-create-service-principal-portal.md), hello 예를 들어 Azure 구독과 연결 된 Azure Active Directory의 멤버인 인증 또는 *사용자 이름* @emailoutlook.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f48b9-168">As a workaround, choose [Connect with Service Principal](/azure-resource-manager/resource-group-create-service-principal-portal.md), or authenticate as a member of hello Azure Active Directory that's associated with your Azure subscription, for example, *user-name*@emailoutlook.onmicrosoft.com.</span></span>

8. <span data-ttu-id="f48b9-169">이제 논리 앱 toopublisher 이벤트를 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-169">Now subscribe your logic app toopublisher events.</span></span> <span data-ttu-id="f48b9-170">다음 표에 hello에 지정 된 대로 이벤트 구독에 대 한 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-170">Provide hello details for your event subscription as specified in hello following table:</span></span>

   ![이벤트 구독에 대한 세부 정보 제공](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | <span data-ttu-id="f48b9-172">설정</span><span class="sxs-lookup"><span data-stu-id="f48b9-172">Setting</span></span> | <span data-ttu-id="f48b9-173">제안 값</span><span class="sxs-lookup"><span data-stu-id="f48b9-173">Suggested value</span></span> | <span data-ttu-id="f48b9-174">설명</span><span class="sxs-lookup"><span data-stu-id="f48b9-174">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="f48b9-175">**구독**</span><span class="sxs-lookup"><span data-stu-id="f48b9-175">**Subscription**</span></span> | <span data-ttu-id="f48b9-176">*{virtual-machine-Azure-subscription}*</span><span class="sxs-lookup"><span data-stu-id="f48b9-176">*{virtual-machine-Azure-subscription}*</span></span> | <span data-ttu-id="f48b9-177">Hello 이벤트 게시자의 Azure 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-177">Select hello event publisher's Azure subscription.</span></span> <span data-ttu-id="f48b9-178">이 자습서에 대 한 hello 가상 컴퓨터에 대 한 Azure 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-178">For this tutorial, select hello Azure subscription for your virtual machine.</span></span> | 
   | <span data-ttu-id="f48b9-179">**리소스 종류**</span><span class="sxs-lookup"><span data-stu-id="f48b9-179">**Resource Type**</span></span> | <span data-ttu-id="f48b9-180">Microsoft.Resources.resourceGroups</span><span class="sxs-lookup"><span data-stu-id="f48b9-180">Microsoft.Resources.resourceGroups</span></span> | <span data-ttu-id="f48b9-181">Hello 이벤트 게시자의 리소스 종류를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-181">Select hello event publisher's resource type.</span></span> <span data-ttu-id="f48b9-182">이 자습서에 대 한 선택 논리 앱 리소스 그룹에만 모니터링 하도록 지정 된 값을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-182">For this tutorial, select hello specified value so your logic app monitors only resource groups.</span></span> | 
   | <span data-ttu-id="f48b9-183">**리소스 이름**</span><span class="sxs-lookup"><span data-stu-id="f48b9-183">**Resource Name**</span></span> | <span data-ttu-id="f48b9-184">*{virtual-machine-resource-group-name}*</span><span class="sxs-lookup"><span data-stu-id="f48b9-184">*{virtual-machine-resource-group-name}*</span></span> | <span data-ttu-id="f48b9-185">Hello 게시자의 리소스 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-185">Select hello publisher's resource name.</span></span> <span data-ttu-id="f48b9-186">이 자습서에 대 한 가상 컴퓨터에 대 한 hello 리소스 그룹의 hello 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-186">For this tutorial, select hello name of hello resource group for your virtual machine.</span></span> | 
   | <span data-ttu-id="f48b9-187">옵션 설정의 경우 **고급 옵션 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-187">For optional settings, choose **Show advanced options**.</span></span> | <span data-ttu-id="f48b9-188">*{see descriptions}*</span><span class="sxs-lookup"><span data-stu-id="f48b9-188">*{see descriptions}*</span></span> | <span data-ttu-id="f48b9-189">* **접두사 필터**: 이 자습서에서는 이 설정을 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-189">* **Prefix Filter**: For this tutorial, leave this setting empty.</span></span> <span data-ttu-id="f48b9-190">hello 기본 동작은 모든 값 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-190">hello default behavior matches all values.</span></span> <span data-ttu-id="f48b9-191">그러나 접두사 문자열(예: 특정 리소스에 대한 경로 및 매개 변수)을 필터로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-191">However, you can specify a prefix string as a filter, for example, a path and a parameter for a specific resource.</span></span> <p><span data-ttu-id="f48b9-192">* **접미사 필터**: 이 자습서에서는 이 설정을 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-192">* **Suffix Filter**: For this tutorial, leave this setting empty.</span></span> <span data-ttu-id="f48b9-193">hello 기본 동작은 모든 값 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-193">hello default behavior matches all values.</span></span> <span data-ttu-id="f48b9-194">그러나 특정 파일 형식만 원하는 경우 접미사 문자열(예: 파일 이름 확장명)을 필터로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-194">However, you can specify a suffix string as a filter, for example, a file name extension, when you want only specific file types.</span></span><p><span data-ttu-id="f48b9-195">* **구독 이름**: 이벤트 구독에 대한 고유한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-195">* **Subscription Name**: Provide a unique name for your event subscription.</span></span> |
   | | | 

   <span data-ttu-id="f48b9-196">완료되면 Event Grid 트리거가 다음 예와 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-196">When you're done, your event grid trigger might look like this example:</span></span>
   
   ![Event Grid 트리거 세부 정보의 예](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. <span data-ttu-id="f48b9-198">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-198">Save your logic app.</span></span> <span data-ttu-id="f48b9-199">Hello 디자이너 도구 모음에서 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-199">On hello designer toolbar, choose **Save**.</span></span> <span data-ttu-id="f48b9-200">toocollapse / 숨기기 논리 앱에서 동작의 세부 hello 액션의 제목 표시줄을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-200">toocollapse and hide an action's details in your logic app, choose hello action's title bar.</span></span>

   ![논리 앱 저장](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   <span data-ttu-id="f48b9-202">논리 앱 이벤트 표 트리거를 저장 하면 Azure 논리 앱 tooyour 선택한 리소스에 대 한 이벤트 구독을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-202">When you save your logic app with an event grid trigger, Azure automatically creates an event subscription for your logic app tooyour selected resource.</span></span> <span data-ttu-id="f48b9-203">따라서 hello 리소스 이벤트 toohello 이벤트 표 형태를 게시 하면 해당 이벤트 표 형태 hello 이벤트 tooyour 논리 앱을 자동으로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-203">So when hello resource publishes an event toohello event grid, that event grid automatically pushes hello event tooyour logic app.</span></span> <span data-ttu-id="f48b9-204">이 이벤트 트리거 논리 앱 다음 만들고 단계에서 정의 하는 hello 워크플로 인스턴스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-204">This event triggers your logic app, then creates and runs an instance of hello workflow that you define in these next steps.</span></span>

<span data-ttu-id="f48b9-205">논리 앱 현재 라이브 및 tooevents hello 이벤트 표 형태에서 수신 대기 있지만 toohello 워크플로 작업을 추가할 때까지 아무런 동작이 수행 되지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-205">Your logic app is now live and listens tooevents from hello event grid, but doesn't do anything until you add actions toohello workflow.</span></span> 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a><span data-ttu-id="f48b9-206">가상 컴퓨터의 변경 사항을 확인하는 조건 추가</span><span class="sxs-lookup"><span data-stu-id="f48b9-206">Add a condition that checks for virtual machine changes</span></span>

<span data-ttu-id="f48b9-207">toorun 논리 앱 워크플로 특정 이벤트가 발생 하는 경우에 가상 컴퓨터에 대 한 "쓰기" 작업을 확인 하는 조건을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-207">toorun your logic app workflow only when a specific event happens, add a condition that checks for virtual machine "write" operations.</span></span> <span data-ttu-id="f48b9-208">이 조건이 true 일 때 논리 앱 업데이트 hello 가상 컴퓨터에 대 한 세부 정보는 전자 메일로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-208">When this condition is true, your logic app sends you email with details about hello updated virtual machine.</span></span>

1. <span data-ttu-id="f48b9-209">논리가 응용 프로그램 디자이너에서 hello 이벤트 표 트리거 선택 **새 단계** > **조건 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-209">In Logic App Designer, under hello event grid trigger, choose **New step** > **Add a condition**.</span></span>

   ![조건 tooyour 논리 앱 추가](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   <span data-ttu-id="f48b9-211">hello 논리가 응용 프로그램 디자이너 hello 조건이 true 또는 false 인지를 기반으로 하는 작업 경로 toofollow를 포함 하는 빈 조건 tooyour 워크플로에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-211">hello Logic App Designer adds an empty condition tooyour workflow, including action paths toofollow based whether hello condition is true or false.</span></span>

   ![빈 조건](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. <span data-ttu-id="f48b9-213">Hello에 **조건** 상자 **고급 모드에서 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-213">In hello **Condition** box, choose **Edit in advanced mode**.</span></span>
<span data-ttu-id="f48b9-214">다음 식을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-214">Enter this expression:</span></span>

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   <span data-ttu-id="f48b9-215">이제 조건은 다음 예와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-215">Your condition now looks like this example:</span></span>

   ![빈 조건](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   <span data-ttu-id="f48b9-217">이 식은 hello 이벤트 확인 `body` 에 대 한는 `data` 여기서 hello 개체 `operationName` 속성은 hello `Microsoft.Compute/virtualMachines/write` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-217">This expression checks hello event `body` for a `data` object where hello `operationName` property is hello `Microsoft.Compute/virtualMachines/write` operation.</span></span> 
   <span data-ttu-id="f48b9-218">[Event Grid 이벤트 스키마](../event-grid/event-schema.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f48b9-218">Learn more about [Event Grid event schema](../event-grid/event-schema.md).</span></span>

3. <span data-ttu-id="f48b9-219">tooprovide hello 조건에 대 한 설명을 선택 hello **줄임표** (**...** ) hello 조건 셰이프를 단추 한 다음 선택 **이름 바꾸기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-219">tooprovide a description for hello condition, choose hello **ellipses** (**...**) button on hello condition shape, then choose **Rename**.</span></span>

   > [!NOTE] 
   > <span data-ttu-id="f48b9-220">hello이 자습서의 뒷부분에 나오는 예제 제공 hello 논리 앱 워크플로의 단계에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-220">hello later examples in this tutorial also provide descriptions for steps in hello logic app workflow.</span></span>

4. <span data-ttu-id="f48b9-221">이제 선택할 **기본 모드에서 편집** hello 식 표시 된 것 처럼 자동으로 해결 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-221">Now choose **Edit in basic mode** so that hello expression automatically resolves as shown:</span></span>

   ![논리 앱 조건](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. <span data-ttu-id="f48b9-223">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-223">Save your logic app.</span></span>

## <a name="send-email-when-your-virtual-machine-changes"></a><span data-ttu-id="f48b9-224">가상 컴퓨터가 변경될 때 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="f48b9-224">Send email when your virtual machine changes</span></span>

<span data-ttu-id="f48b9-225">이제 추가 [ *동작* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) hello를 지정 된 조건이 true 인 경우 전자 메일을 받을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-225">Now add an [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) so that you get an email when hello specified condition is true.</span></span>

1. <span data-ttu-id="f48b9-226">Hello 조건에 **True** 상자 **동작 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-226">In hello condition's **If true** box, choose **Add an action**.</span></span>

   ![조건이 true인 경우의 작업 추가](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. <span data-ttu-id="f48b9-228">Hello 검색 상자에 "email" 필터로 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-228">In hello search box, enter "email" as your filter.</span></span> <span data-ttu-id="f48b9-229">전자 메일 공급자에 따라를 찾기 되어 hello 일치 하는 커넥터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-229">Based on your email provider, find and select hello matching connector.</span></span> <span data-ttu-id="f48b9-230">커넥터에 대 한 hello "전자 메일 보내기" 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-230">Then select hello "send email" action for your connector.</span></span> <span data-ttu-id="f48b9-231">예:</span><span class="sxs-lookup"><span data-stu-id="f48b9-231">For example:</span></span> 

   * <span data-ttu-id="f48b9-232">Azure에 대 한 작업 또는 학교 계정이 선택 hello Office 365 Outlook 커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-232">For an Azure work or school account, select hello Office 365 Outlook connector.</span></span> 
   * <span data-ttu-id="f48b9-233">개인 Microsoft 계정에 대 한 hello Outlook.com 커넥터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-233">For personal Microsoft accounts, select hello Outlook.com connector.</span></span> 
   * <span data-ttu-id="f48b9-234">Gmail 계정에 대 한 hello Gmail 커넥터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-234">For Gmail accounts, select hello Gmail connector.</span></span> 

   <span data-ttu-id="f48b9-235">Hello Office 365 Outlook 커넥터와 함께 toocontinue를 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-235">We're going toocontinue with hello Office 365 Outlook connector.</span></span> 
   <span data-ttu-id="f48b9-236">다른 공급자를 사용 하는 경우 단계 상태를 유지 하는 hello hello 동일 하지만 UI 다르게 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-236">If you use a different provider, hello steps remain hello same, but your UI might appear different.</span></span> 

   !["전자 메일 보내기" 작업 선택](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. <span data-ttu-id="f48b9-238">전자 메일 공급자에 대 한 연결이 없는 경우 인증에 대 한 묻는 tooyour 전자 메일 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-238">If you don't already have a connection for your email provider, sign in tooyour email account when you're asked for authentication.</span></span>

4. <span data-ttu-id="f48b9-239">다음 표에 hello에 지정 된 대로 hello 전자 메일에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-239">Provide details for hello email as specified in hello following table:</span></span>

   ![빈 전자 메일 작업](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > <span data-ttu-id="f48b9-241">워크플로에서 사용할 수 있는 필드에서 tooselect 클릭 편집 상자에 있으므로 해당 hello **동적 콘텐츠** 열리고 나열 하거나 선택 **동적 콘텐츠를 추가할**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-241">tooselect from fields available in your workflow, click in an edit box so that hello **Dynamic content** list opens, or choose **Add dynamic content**.</span></span> <span data-ttu-id="f48b9-242">더 많은 필드에 대 한 선택 **더 보려면** hello 목록에서 각 섹션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-242">For more fields, choose **See more** for each section in hello list.</span></span> <span data-ttu-id="f48b9-243">tooclose hello **동적 콘텐츠** 목록에서 선택 **동적 콘텐츠를 추가할**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-243">tooclose hello **Dynamic content** list, choose **Add dynamic content**.</span></span>

   | <span data-ttu-id="f48b9-244">설정</span><span class="sxs-lookup"><span data-stu-id="f48b9-244">Setting</span></span> | <span data-ttu-id="f48b9-245">제안 값</span><span class="sxs-lookup"><span data-stu-id="f48b9-245">Suggested value</span></span> | <span data-ttu-id="f48b9-246">설명</span><span class="sxs-lookup"><span data-stu-id="f48b9-246">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="f48b9-247">**To**</span><span class="sxs-lookup"><span data-stu-id="f48b9-247">**To**</span></span> | <span data-ttu-id="f48b9-248">*{recipient-email-address}*</span><span class="sxs-lookup"><span data-stu-id="f48b9-248">*{recipient-email-address}*</span></span> |<span data-ttu-id="f48b9-249">Hello 받는 사람의 전자 메일 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-249">Enter hello recipient's email address.</span></span> <span data-ttu-id="f48b9-250">자신의 이메일 주소를 사용하여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-250">For testing purposes, you can use your own email address.</span></span> | 
   | <span data-ttu-id="f48b9-251">**제목**</span><span class="sxs-lookup"><span data-stu-id="f48b9-251">**Subject**</span></span> | <span data-ttu-id="f48b9-252">업데이트된 리소스: **제목**</span><span class="sxs-lookup"><span data-stu-id="f48b9-252">Resource updated: **Subject**</span></span>| <span data-ttu-id="f48b9-253">Hello 메일 제목에 대 한 hello 콘텐츠를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-253">Enter hello content for hello email's subject.</span></span> <span data-ttu-id="f48b9-254">이 자습서에 대 한 입력 텍스트 및 선택 hello 이벤트 hello 제안 **주체** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-254">For this tutorial, enter hello suggested text and select hello event's **Subject** field.</span></span> <span data-ttu-id="f48b9-255">여기에서 메일 제목에는 업데이트 하는 hello 리소스 (가상 컴퓨터)에 대 한 hello 이름이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-255">Here, your email subject includes hello name for hello updated resource (virtual machine).</span></span> | 
   | <span data-ttu-id="f48b9-256">**본문**</span><span class="sxs-lookup"><span data-stu-id="f48b9-256">**Body**</span></span> | <span data-ttu-id="f48b9-257">리소스 그룹: **토픽**</span><span class="sxs-lookup"><span data-stu-id="f48b9-257">Resource group: **Topic**</span></span> <p><span data-ttu-id="f48b9-258">이벤트 유형: **이벤트 유형**</span><span class="sxs-lookup"><span data-stu-id="f48b9-258">Event type: **Event Type**</span></span><p><span data-ttu-id="f48b9-259">이벤트 ID: **ID**</span><span class="sxs-lookup"><span data-stu-id="f48b9-259">Event ID: **ID**</span></span><p><span data-ttu-id="f48b9-260">시간: **이벤트 시간**</span><span class="sxs-lookup"><span data-stu-id="f48b9-260">Time: **Event Time**</span></span> | <span data-ttu-id="f48b9-261">Hello 메일의 본문에 대 한 hello 콘텐츠를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-261">Enter hello content for hello email's body.</span></span> <span data-ttu-id="f48b9-262">이 자습서에 대 한 입력 텍스트 및 선택 hello 이벤트 hello 제안 **항목**, **이벤트 유형을**, **ID**, 및 **이벤트 시간** 필드 있도록 사용자의 전자 메일 hello 리소스 그룹 이름, 이벤트 유형, 이벤트 타임 스탬프 및 hello 업데이트에 대 한 이벤트 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-262">For this tutorial, enter hello suggested text and select hello event's **Topic**, **Event Type**, **ID**, and **Event Time** fields so that your email includes hello resource group name, event type, event timestamp, and event ID for hello update.</span></span> <p><span data-ttu-id="f48b9-263">콘텐츠를에서 빈 줄 tooadd Shift + Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-263">tooadd blank lines in your content, press Shift + Enter.</span></span> | 
   | | | 

   > [!NOTE] 
   > <span data-ttu-id="f48b9-264">배열을 나타내는 필드 선택 hello 디자이너가 자동으로 추가 **각** hello 배열 참조 하는 hello 동작 주위 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-264">If you select a field that represents an array, hello designer automatically adds a **For each** loop around hello action that references hello array.</span></span> <span data-ttu-id="f48b9-265">그렇게 하면 논리 앱에서 각 배열 항목에 대한 해당 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-265">That way, your logic app performs that action on each array item.</span></span>

   <span data-ttu-id="f48b9-266">이제 전자 메일 작업이 다음 예와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-266">Now, your email action might look like this example:</span></span>

   ![전자 메일에서 출력 tooinclude를 선택 합니다.](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   <span data-ttu-id="f48b9-268">완료된 논리 앱이 다음 예와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-268">And your finished logic app might look like this example:</span></span>

   ![완료된 논리 앱](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. <span data-ttu-id="f48b9-270">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-270">Save your logic app.</span></span> <span data-ttu-id="f48b9-271">toocollapse / 숨기기 논리 앱에서 각 작업의 세부 hello 액션의 제목 표시줄을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-271">toocollapse and hide each action's details in your logic app, choose hello action's title bar.</span></span>

   ![논리 앱 저장](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   <span data-ttu-id="f48b9-273">논리 앱 현재 라이브가 있지만 작업을 수행 하기 전에 변경 내용 tooyour 가상 컴퓨터에 대 한 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-273">Your logic app is now live, but waits for changes tooyour virtual machine before doing anything.</span></span> 
   <span data-ttu-id="f48b9-274">tootest 논리 앱 toohello 다음 섹션은 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-274">tootest your logic app now, continue toohello next section.</span></span>

## <a name="test-your-logic-app-workflow"></a><span data-ttu-id="f48b9-275">논리 앱 워크플로 테스트</span><span class="sxs-lookup"><span data-stu-id="f48b9-275">Test your logic app workflow</span></span>

1. <span data-ttu-id="f48b9-276">논리 앱 hello 하다는 toocheck 지정 된 이벤트, 가상 컴퓨터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-276">toocheck that your logic app is getting hello specified events, update your virtual machine.</span></span> 

   <span data-ttu-id="f48b9-277">예를 들어 hello Azure 포털에서에서 가상 컴퓨터를 조정할 수 있습니다 또는 [Azure PowerShell을 사용한 VM의 크기를 조정](../virtual-machines/windows/resize-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-277">For example, you can resize your virtual machine in hello Azure portal or [resize your VM with Azure PowerShell](../virtual-machines/windows/resize-vm.md).</span></span> 

   <span data-ttu-id="f48b9-278">몇 분 후에 전자 메일을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-278">After a few moments, you should get an email.</span></span> <span data-ttu-id="f48b9-279">예:</span><span class="sxs-lookup"><span data-stu-id="f48b9-279">For example:</span></span>

   ![가상 컴퓨터 업데이트에 대한 전자 메일](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. <span data-ttu-id="f48b9-281">tooreview hello를 실행 하 고 논리 앱 메뉴에서 논리 앱에 대 한 트리거 기록을 선택 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-281">tooreview hello runs and trigger history for your logic app, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="f48b9-282">실행에 대 한 자세한 내용은 tooview 실행에 대 한 hello 행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-282">tooview more details about a run, choose hello row for that run.</span></span>

   ![논리 앱 실행 기록](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. <span data-ttu-id="f48b9-284">tooview hello 입 / 출력 각 단계에 대 한 tooreview hello 단계를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-284">tooview hello inputs and outputs for each step, expand hello step that you want tooreview.</span></span> <span data-ttu-id="f48b9-285">이 정보는 논리 앱의 문제를 진단하고 디버깅하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-285">This information can help you diagnose and debug problems in your logic app.</span></span>
 
   ![논리 앱 실행 기록 세부 정보](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

<span data-ttu-id="f48b9-287">축하합니다! Event Grid를 통해 리소스 이벤트를 모니터링하고 이러한 이벤트가 발생하면 전자 메일을 보내는 논리 앱을 만들고 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-287">Congratulations, you've created and run a logic app that monitors resource events through an event grid and emails you when those events happen.</span></span> <span data-ttu-id="f48b9-288">또한 프로세스를 자동화하고 시스템과 클라우드 서비스를 통합하는 워크플로를 쉽게 만들 수 있는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-288">You also learned how easily you can create workflows that automate processes and integrate systems and cloud services.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="f48b9-289">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="f48b9-289">Clean up resources</span></span>

<span data-ttu-id="f48b9-290">이 자습서에서는 리소스를 사용하고 Azure 구독에 요금을 부과하는 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-290">This tutorial uses resources and performs actions that incur charges on your Azure subscription.</span></span> <span data-ttu-id="f48b9-291">따라서 hello 자습서 및 테스트을 마친 경우 사용 하지 않도록 설정 하거나 tooincur 요금 않도록 하려는 모든 리소스를 삭제 하면 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-291">So when you're done with hello tutorial and testing, make sure that you disable or delete any resources where you don't want tooincur charges.</span></span>

<span data-ttu-id="f48b9-292">논리 앱을 실행 하 고 hello 앱을 삭제 하지 않고 전자 메일을 보내기에서 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-292">You can stop your logic app from running and sending email without deleting hello app.</span></span> <span data-ttu-id="f48b9-293">논리 앱 메뉴에서 **개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-293">On your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="f48b9-294">Hello 도구 모음에서 선택 **사용 하지 않도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-294">On hello toolbar, choose **Disable**.</span></span>

![논리 앱 사용 해제](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a><span data-ttu-id="f48b9-296">FAQ</span><span class="sxs-lookup"><span data-stu-id="f48b9-296">FAQ</span></span>

<span data-ttu-id="f48b9-297">**Q**: Event Grid 및 논리 앱으로 수행할 수 있는 다른 가상 컴퓨터 모니터링 작업은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="f48b9-297">**Q**: What other virtual machine monitoring tasks can I perform with event grids and logic apps?</span></span> </br><span data-ttu-id="f48b9-298">
**A**: 다음과 같이 다른 구성 변경 내용을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-298">
**A**: You can monitor other configuration changes, for example:</span></span>

* <span data-ttu-id="f48b9-299">가상 컴퓨터에서 RBAC(역할 기반 액세스 제어) 권한을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-299">A virtual machine gets role-based access control (RBAC) rights.</span></span>
* <span data-ttu-id="f48b9-300">변경 내용이 tooa NSG 네트워크 보안 그룹 () (NIC) 네트워크 인터페이스에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-300">Changes are made tooa network security group (NSG) on a network interface (NIC).</span></span>
* <span data-ttu-id="f48b9-301">가상 컴퓨터용 디스크가 추가되거나 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f48b9-301">Disks for a virtual machine are added or removed.</span></span>
* <span data-ttu-id="f48b9-302">공용 IP 주소를 가상 컴퓨터 NIC. tooa 할당</span><span class="sxs-lookup"><span data-stu-id="f48b9-302">A public IP address is assigned tooa virtual machine NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f48b9-303">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f48b9-303">Next steps</span></span>

* [<span data-ttu-id="f48b9-304">Event Grid 개요</span><span class="sxs-lookup"><span data-stu-id="f48b9-304">Event Grid Overview</span></span>](../event-grid/overview.md)
* [<span data-ttu-id="f48b9-305">Event Grid 개념</span><span class="sxs-lookup"><span data-stu-id="f48b9-305">Event Grid Concepts</span></span>](../event-grid/concepts.md)
* [<span data-ttu-id="f48b9-306">빠른 시작: Event Grid로 사용자 지정 이벤트 만들기 및 라우팅</span><span class="sxs-lookup"><span data-stu-id="f48b9-306">Quickstart: Create and route custom events with Event Grid</span></span>](../event-grid/custom-event-quickstart.md)
* [<span data-ttu-id="f48b9-307">Event Grid 이벤트 스키마</span><span class="sxs-lookup"><span data-stu-id="f48b9-307">Event Grid event schema</span></span>](../event-grid/event-schema.md)
* [<span data-ttu-id="f48b9-308">Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f48b9-308">Azure Logic Apps</span></span>](../logic-apps/logic-apps-what-are-logic-apps.md)
* [<span data-ttu-id="f48b9-309">미리 정의된 템플릿을 사용하여 논리 앱 워크플로 만들기</span><span class="sxs-lookup"><span data-stu-id="f48b9-309">Create logic app workflows with predefined templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)