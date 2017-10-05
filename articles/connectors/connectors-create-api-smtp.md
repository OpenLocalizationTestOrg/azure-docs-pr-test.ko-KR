---
title: "Azure Logic Apps의 SMTP 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. SMTP에 연결하여 전자 메일을 보냅니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1cf96bbf8bd215d7ddb3c99860a5cb4e668be3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-smtp-connector"></a><span data-ttu-id="550bf-104">SMTP 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="550bf-104">Get started with the SMTP connector</span></span>
<span data-ttu-id="550bf-105">SMTP에 연결하여 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-105">Connect to SMTP to send email.</span></span>

<span data-ttu-id="550bf-106">[커넥터](apis-list.md)를 사용하려면 먼저 논리 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="550bf-107">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-smtp"></a><span data-ttu-id="550bf-108">SMTP에 연결</span><span class="sxs-lookup"><span data-stu-id="550bf-108">Connect to SMTP</span></span>
<span data-ttu-id="550bf-109">논리 앱에서 서비스에 액세스하려면 먼저 서비스에 대한 *연결*을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="550bf-110">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="550bf-111">예를 들어 SMTP에 연결하려면 먼저 SMTP *연결*이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-111">For example, to connect to SMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="550bf-112">연결을 만들려면 연결하려는 서비스에 액세스할 때 일반적으로 사용하는 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-112">To create a connection, enter the credentials you normally use to access the service you connect to.</span></span> <span data-ttu-id="550bf-113">따라서 SMTP 예제에서는 SMTP에 대한 연결을 만들기 위해 연결 이름, SMTP 서버 주소 및 사용자 로그인 정보에 대한 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-113">So, in the SMTP example, enter the credentials to your connection name, SMTP server address, and user login information to create the connection to SMTP.</span></span>  

### <a name="create-a-connection-to-smtp"></a><span data-ttu-id="550bf-114">SMTP에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="550bf-114">Create a connection to SMTP</span></span>
> [!INCLUDE [Steps to create a connection to SMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="550bf-115">SMTP 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="550bf-115">Use an SMTP trigger</span></span>
<span data-ttu-id="550bf-116">트리거는 논리 앱에 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-116">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="550bf-117">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="550bf-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="550bf-118">이 예제에서는 SMTP가 자체 트리거를 포함하지 않으므로 **Salesforce - 개체를 만들 때** 트리거를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-118">In this example, because SMTP does not have a trigger of its own, we'll use the **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="550bf-119">이 트리거는 Salesforce에서 새 개체를 만들 때 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="550bf-120">예제에서는 Salesforce에서 새 잠재 고객이 생성될 때마다 새 잠재 고객이 생성되었다는 알림과 함께 SMTP 커넥터를 통해 *메일 보내기* 작업이 발생하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via the SMTP connector with a notification of the new lead being created.</span></span>

1. <span data-ttu-id="550bf-121">논리 앱 디자이너에서 검색 상자에 *salesforce* 를 입력한 후 **Salesforce - 개체를 만들 때** 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-121">Enter *salesforce* in the search box on the logic apps designer then select the **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="550bf-122">**개체를 만들 때** 컨트롤이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-122">The **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="550bf-123">**개체 형식** 을 선택하고 개체 목록에서 *Lead* 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-123">Select the **Object Type** then select *Lead* from the list of objects.</span></span> <span data-ttu-id="550bf-124">이 단계에서는 Salesforce에서 새 잠재 고객을 만들 때마다 논리 앱에 알리는 트리거를 만들고 있음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="550bf-125">트리거를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-125">The trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="550bf-126">SMTP 작업 사용</span><span class="sxs-lookup"><span data-stu-id="550bf-126">Use an SMTP action</span></span>
<span data-ttu-id="550bf-127">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="550bf-128">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="550bf-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="550bf-129">이제 트리거가 추가되었고 다음 단계에 따라 Salesforce에 새 잠재 고객이 생성될 대 발생할 SMTP 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-129">Now that the trigger has been added, follow these steps to add an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="550bf-130">**+ 새 단계**를 선택하여 새 잠재 고객이 생성될 때 수행할 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-130">Select **+ New Step** to add the action you would like to take when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="550bf-131">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-131">Select **Add an action**.</span></span> <span data-ttu-id="550bf-132">수행할 동작을 검색할 수 있는 검색 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="550bf-133">*smtp*를 입력하여 SMTP와 관련된 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-133">Enter *smtp* to search for actions related to SMTP.</span></span>  
4. <span data-ttu-id="550bf-134">새 잠재 고객이 생성될 때 수행할 작업으로 **SMTP - 전자 메일 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-134">Select **SMTP - Send Email** as the action to take when the new lead is created.</span></span> <span data-ttu-id="550bf-135">작업 제어 블록이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-135">The action control block opens.</span></span> <span data-ttu-id="550bf-136">아직 수행하지 않은 경우 디자이너 블록에서 smtp 연결을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-136">You will have to establish your smtp connection in the designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="550bf-137">**SMTP - 전자 메일 보내기** 블록에 원하는 전자 메일 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-137">Input your desired email information in the **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="550bf-138">워크플로를 활성화하려면 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-138">Save your work in order to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="550bf-139">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="550bf-139">Connector-specific details</span></span>

<span data-ttu-id="550bf-140">[커넥터 세부 정보](/connectors/smtpconnector/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="550bf-141">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="550bf-141">More connectors</span></span>
<span data-ttu-id="550bf-142">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="550bf-142">Go back to the [APIs list](apis-list.md).</span></span>