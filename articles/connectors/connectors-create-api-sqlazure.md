---
title: "논리 앱에서 aaaAdd hello Azure SQL 데이터베이스 커넥터 | Microsoft Docs"
description: "REST API 매개 변수를 사용하는 Azure SQL 데이터베이스 커넥터 개요"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a><span data-ttu-id="b9b5f-103">Hello Azure SQL 데이터베이스 커넥터와 함께 시작.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-103">Get started with hello Azure SQL Database connector</span></span>
<span data-ttu-id="b9b5f-104">Hello Azure SQL 데이터베이스 커넥터를 사용 하 여 조직에 대 한 테이블의 데이터를 관리 하는 워크플로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-104">Using hello Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="b9b5f-105">SQL 데이터베이스를 사용하여 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-105">With SQL Database, you:</span></span>

* <span data-ttu-id="b9b5f-106">새 고객 tooa 고객 데이터베이스를 추가 하거나 orders 데이터베이스에 순서를 업데이트 하 여 워크플로 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-106">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="b9b5f-107">동작 tooget 데이터 행을 사용 하 고, 새 행을 삽입 하 고 및 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-107">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="b9b5f-108">예를 들어 Dynamics CRM Online에서 레코드가 만들어지면(트리거) Azure SQL Database에 행을 삽입합니다(작업).</span><span class="sxs-lookup"><span data-stu-id="b9b5f-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="b9b5f-109">이 항목에서는 방법을 toouse hello 논리 앱에서 SQL 데이터베이스 커넥터와도 목록 hello 동작.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-109">This topic shows you how toouse hello SQL Database connector in a logic app, and also lists hello actions.</span></span>

<span data-ttu-id="b9b5f-110">논리 앱에 대해 자세히 toolearn 참조 [논리 앱 이란](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-sql-database"></a><span data-ttu-id="b9b5f-111">TooAzure SQL 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="b9b5f-111">Connect tooAzure SQL Database</span></span>
<span data-ttu-id="b9b5f-112">논리 앱에서 모든 서비스에 액세스 하기 전에 먼저 만들어야는 *연결* toohello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-112">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="b9b5f-113">연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="b9b5f-114">예를 들어 tooconnect tooSQL 데이터베이스를 먼저 만들어야 SQL 데이터베이스 *연결*합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-114">For example, tooconnect tooSQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="b9b5f-115">tooaccess hello 서비스에 연결 하는 일반적으로 사용 하는 hello 자격 증명을 입력 한 toocreate 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-115">toocreate a connection, you enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="b9b5f-116">따라서 SQL 데이터베이스의 SQL 데이터베이스 자격 증명 toocreate hello 연결을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-116">So, in SQL Database, enter your SQL Database credentials toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="b9b5f-117">Hello 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="b9b5f-117">Create hello connection</span></span>
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="b9b5f-118">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="b9b5f-118">Use a trigger</span></span>
<span data-ttu-id="b9b5f-119">이 연결에는 트리거가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-119">This connector does not have any triggers.</span></span> <span data-ttu-id="b9b5f-120">다른 트리거 toostart hello 논리 앱과 되풀이 트리거, HTTP Webhook 트리거는 트리거를 사용 하 여 다른 커넥터를 사용할 수 있는 등을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-120">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="b9b5f-121">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)에서 예제를 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="b9b5f-122">작업 사용</span><span class="sxs-lookup"><span data-stu-id="b9b5f-122">Use an action</span></span>
<span data-ttu-id="b9b5f-123">동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-123">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="b9b5f-124">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="b9b5f-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="b9b5f-125">Hello 더하기 기호를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-125">Select hello plus sign.</span></span> <span data-ttu-id="b9b5f-126">여러 선택 항목을 참조 하십시오: **동작 추가**, **조건을 추가**, hello 중 하나 또는 **자세한** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="b9b5f-127">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="b9b5f-128">Hello 텍스트 상자에 "sql" tooget hello 사용 가능한 모든 작업 목록을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-128">In hello text box, type “sql” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="b9b5f-129">이 예제에서는 **SQL Server - 행 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="b9b5f-130">연결이 이미 존재 하는 경우 다음 hello 선택 **테이블 이름** hello 드롭다운 목록에서 목록을 연 hello 입력 **행 ID** tooreturn 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-130">If a connection already exists, then select hello **Table name** from hello drop-down list, and enter hello **Row ID** you want tooreturn.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="b9b5f-131">Hello 연결 정보에 대 한 메시지가 표시 되 면 hello, toocreate hello 연결 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="b9b5f-132">[Hello 연결을 만들](connectors-create-api-sqlazure.md#create-the-connection) 이 항목에서 이러한 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-132">[Create hello connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b9b5f-133">이 예제에서는 테이블의 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="b9b5f-134">이 행에 toosee hello 데이터가 hello 테이블의 필드를 hello를 사용 하 여 파일을 만드는 다른 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-134">toosee hello data in this row, add another action that creates a file using hello fields from hello table.</span></span> <span data-ttu-id="b9b5f-135">예를 들어 hello FirstName 및 LastName 필드 toocreate hello 클라우드 저장소 계정에 새 파일을 사용 하는 OneDrive 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-135">For example, add a OneDrive action that uses hello FirstName and LastName fields toocreate a new file in hello cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="b9b5f-136">**저장** 변경 내용을 (hello 도구 모음의 왼쪽된 상단 모서리).</span><span class="sxs-lookup"><span data-stu-id="b9b5f-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="b9b5f-137">논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="b9b5f-138">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="b9b5f-138">Connector-specific details</span></span>

<span data-ttu-id="b9b5f-139">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/sql/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-139">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b9b5f-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9b5f-140">Next steps</span></span>
<span data-ttu-id="b9b5f-141">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="b9b5f-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="b9b5f-142">탐색에서 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9b5f-142">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

