---
title: "Azure 논리 앱에서 aaaSMTP 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. TooSMTP toosend 전자 메일을 연결 합니다."
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
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a><span data-ttu-id="22c29-104">Hello SMTP 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="22c29-104">Get started with hello SMTP connector</span></span>
<span data-ttu-id="22c29-105">TooSMTP toosend 전자 메일을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-105">Connect tooSMTP toosend email.</span></span>

<span data-ttu-id="22c29-106">toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="22c29-107">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosmtp"></a><span data-ttu-id="22c29-108">TooSMTP 연결</span><span class="sxs-lookup"><span data-stu-id="22c29-108">Connect tooSMTP</span></span>
<span data-ttu-id="22c29-109">Toocreate 먼저 논리 앱에서 모든 서비스에 액세스 하기 전에 *연결* toohello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="22c29-110">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="22c29-111">예를 들어, tooconnect tooSMTP 먼저 SMTP *연결*합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-111">For example, tooconnect tooSMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="22c29-112">toocreate 연결을 일반적으로 tooaccess hello 서비스에 연결을 사용 하는 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-112">toocreate a connection, enter hello credentials you normally use tooaccess hello service you connect to.</span></span> <span data-ttu-id="22c29-113">따라서 hello SMTP 예에서 hello 자격 증명 tooyour 연결 이름, SMTP 서버 주소 및 사용자 로그인 정보 toocreate hello 연결 tooSMTP를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-113">So, in hello SMTP example, enter hello credentials tooyour connection name, SMTP server address, and user login information toocreate hello connection tooSMTP.</span></span>  

### <a name="create-a-connection-toosmtp"></a><span data-ttu-id="22c29-114">연결 tooSMTP 만들기</span><span class="sxs-lookup"><span data-stu-id="22c29-114">Create a connection tooSMTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="22c29-115">SMTP 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="22c29-115">Use an SMTP trigger</span></span>
<span data-ttu-id="22c29-116">트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-116">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="22c29-117">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="22c29-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="22c29-118">이 예제에서는 SMTP 자체의 트리거 없기 때문에에서는 hello **Salesforce-개체가 만들어질 때** 트리거.</span><span class="sxs-lookup"><span data-stu-id="22c29-118">In this example, because SMTP does not have a trigger of its own, we'll use hello **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="22c29-119">이 트리거는 Salesforce에서 새 개체를 만들 때 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="22c29-120">이 예에서는에서는 설정 하면 해당 새 잠재 고객, Salesforce에 만들어진 될 때마다 되도록 한 *전자 메일을 보낼* 동작은 만들려는 hello 새 잠재 고객의 알림 사용 하 여 hello SMTP 커넥터를 통해 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via hello SMTP connector with a notification of hello new lead being created.</span></span>

1. <span data-ttu-id="22c29-121">입력 *salesforce* hello 논리 앱 디자이너에 hello 검색 상자에 다음 hello 선택 **Salesforce-개체가 만들어질 때** 트리거.</span><span class="sxs-lookup"><span data-stu-id="22c29-121">Enter *salesforce* in hello search box on hello logic apps designer then select hello **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="22c29-122">hello **개체를 만들 때** 컨트롤이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-122">hello **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="22c29-123">선택 hello **개체 유형** 다음 선택 *발생할* 개체의 hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-123">Select hello **Object Type** then select *Lead* from hello list of objects.</span></span> <span data-ttu-id="22c29-124">이 단계에서는 Salesforce에서 새 잠재 고객을 만들 때마다 논리 앱에 알리는 트리거를 만들고 있음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="22c29-125">hello 트리거 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-125">hello trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="22c29-126">SMTP 작업 사용</span><span class="sxs-lookup"><span data-stu-id="22c29-126">Use an SMTP action</span></span>
<span data-ttu-id="22c29-127">동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="22c29-128">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="22c29-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="22c29-129">Hello 트리거 추가 했으므로 Salesforce에서 새 잠재 고객을 만들 때 발생 하는 이러한 단계에서는 SMTP tooadd 동작을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-129">Now that hello trigger has been added, follow these steps tooadd an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="22c29-130">선택 **+ 새 단계** tooadd hello 작업 원하는 tootake 새 잠재 고객을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="22c29-130">Select **+ New Step** tooadd hello action you would like tootake when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="22c29-131">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-131">Select **Add an action**.</span></span> <span data-ttu-id="22c29-132">검색할 수 있는 모든 작업에 대 한 있습니다이 열립니다 hello 검색 상자 tootake를 것인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="22c29-133">입력 *smtp* toosearch 관련된 tooSMTP 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-133">Enter *smtp* toosearch for actions related tooSMTP.</span></span>  
4. <span data-ttu-id="22c29-134">선택 **SMTP-전자 메일 보내기** hello 새 잠재 고객 만들어질 때 작업 tootake hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-134">Select **SMTP - Send Email** as hello action tootake when hello new lead is created.</span></span> <span data-ttu-id="22c29-135">hello 동작 제어 블록을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-135">hello action control block opens.</span></span> <span data-ttu-id="22c29-136">Tooestablish smtp 연결에에서 있을 hello 디자이너 블록 하지 않았으면 지금 이전 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="22c29-136">You will have tooestablish your smtp connection in hello designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="22c29-137">Hello에 원하는 전자 메일 정보를 입력 **SMTP-전자 메일 보내기** 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-137">Input your desired email information in hello **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="22c29-138">순서 tooactivate 워크플로 작업을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-138">Save your work in order tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="22c29-139">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="22c29-139">Connector-specific details</span></span>

<span data-ttu-id="22c29-140">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/smtpconnector/)합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="22c29-141">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="22c29-141">More connectors</span></span>
<span data-ttu-id="22c29-142">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="22c29-142">Go back toohello [APIs list](apis-list.md).</span></span>
