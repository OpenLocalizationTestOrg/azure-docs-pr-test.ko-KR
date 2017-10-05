---
title: "논리 앱에 Azure SQL 데이터베이스 커넥터 추가 | Microsoft Docs"
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
ms.openlocfilehash: a3d5cb909dbfcb00f3fbfa0165bb6cd58eb18688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-sql-database-connector"></a><span data-ttu-id="ac2bc-103">Azure SQL 데이터베이스 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="ac2bc-103">Get started with the Azure SQL Database connector</span></span>
<span data-ttu-id="ac2bc-104">Azure SQL 데이터베이스 커넥터를 사용하여 테이블의 데이터를 관리하는 조직의 워크플로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-104">Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="ac2bc-105">SQL 데이터베이스를 사용하여 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-105">With SQL Database, you:</span></span>

* <span data-ttu-id="ac2bc-106">고객 데이터베이스에 새 고객을 추가하거나 주문 데이터베이스에서 주문을 업데이트하여 워크플로를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-106">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="ac2bc-107">데이터의 행을 가져오고, 새 행을 삽입하고, 삭제하는 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-107">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="ac2bc-108">예를 들어 Dynamics CRM Online에서 레코드가 만들어지면(트리거) Azure SQL Database에 행을 삽입합니다(작업).</span><span class="sxs-lookup"><span data-stu-id="ac2bc-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="ac2bc-109">이 항목에서는 논리 앱에서 SQL Database 커넥터를 사용하는 방법을 보여 주고, 트리거 및 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-109">This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.</span></span>

<span data-ttu-id="ac2bc-110">Logic Apps에 대해 자세히 알아보려면 [논리 앱이란 무엇인가요?](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-sql-database"></a><span data-ttu-id="ac2bc-111">Azure SQL 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="ac2bc-111">Connect to Azure SQL Database</span></span>
<span data-ttu-id="ac2bc-112">논리 앱에서 서비스에 액세스하려면 먼저 서비스에 대한 *연결*을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-112">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="ac2bc-113">연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="ac2bc-114">예를 들어 SQL Database에 연결하려면 먼저 SQL Database *연결*을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-114">For example, to connect to SQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="ac2bc-115">연결을 만들려면 연결하려는 서비스에 액세스할 때 일반적으로 사용하는 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-115">To create a connection, you enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="ac2bc-116">따라서 SQL 데이터베이스에서 SQL 데이터베이스 자격 증명을 입력하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-116">So, in SQL Database, enter your SQL Database credentials to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="ac2bc-117">연결 만들기</span><span class="sxs-lookup"><span data-stu-id="ac2bc-117">Create the connection</span></span>
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="ac2bc-118">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="ac2bc-118">Use a trigger</span></span>
<span data-ttu-id="ac2bc-119">이 연결에는 트리거가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-119">This connector does not have any triggers.</span></span> <span data-ttu-id="ac2bc-120">다른 트리거(되풀이 트리거, HTTP 웹후크 트리거, 다른 커넥터와 함께 사용할 수 있는 트리거 포함)를 사용하여 논리 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-120">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="ac2bc-121">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)에서 예제를 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="ac2bc-122">작업 사용</span><span class="sxs-lookup"><span data-stu-id="ac2bc-122">Use an action</span></span>
<span data-ttu-id="ac2bc-123">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-123">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="ac2bc-124">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="ac2bc-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="ac2bc-125">더하기 기호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-125">Select the plus sign.</span></span> <span data-ttu-id="ac2bc-126">**작업 추가**, **조건 추가** 또는 **자세히** 옵션 중 하나 등 몇 가지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="ac2bc-127">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="ac2bc-128">텍스트 상자에 "sql"을 입력하여 사용 가능한 모든 작업의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-128">In the text box, type “sql” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="ac2bc-129">이 예제에서는 **SQL Server - 행 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="ac2bc-130">연결이 이미 있는 경우 드롭다운 목록에서 **테이블 이름**을 선택하고 반환할 **행 ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-130">If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="ac2bc-131">연결 정보를 묻는 메시지가 표시되면 연결을 만들기 위한 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="ac2bc-132">이 항목의 [연결 만들기](connectors-create-api-sqlazure.md#create-the-connection)에서는 이러한 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-132">[Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ac2bc-133">이 예제에서는 테이블의 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="ac2bc-134">이 행의 데이터를 보려면 테이블의 필드를 사용하여 파일을 만드는 다른 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-134">To see the data in this row, add another action that creates a file using the fields from the table.</span></span> <span data-ttu-id="ac2bc-135">예를 들어 FirstName 및 LastName 필드를 사용하여 클라우드 저장소 계정에 새 파일을 만드는 OneDrive 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-135">For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="ac2bc-136">변경 내용을 **저장**합니다(도구 모음 왼쪽 위 모서리).</span><span class="sxs-lookup"><span data-stu-id="ac2bc-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="ac2bc-137">논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="ac2bc-138">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="ac2bc-138">Connector-specific details</span></span>

<span data-ttu-id="ac2bc-139">[커넥터 세부 정보](/connectors/sql/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-139">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ac2bc-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac2bc-140">Next steps</span></span>
<span data-ttu-id="ac2bc-141">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="ac2bc-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="ac2bc-142">[API 목록](apis-list.md)에서 Logic Apps의 사용 가능한 다른 커넥터를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ac2bc-142">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

