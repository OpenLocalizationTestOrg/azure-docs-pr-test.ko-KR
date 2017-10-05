---
title: "Azure Logic Apps에 Oracle 데이터베이스 커넥터 추가 | Microsoft Docs"
description: "논리 앱에서 Oracle 데이터베이스 커넥터 사용"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: cc64441617eb5e7d5e70c1cf5c491a672428bc51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-the-oracle-database-connector"></a><span data-ttu-id="f8915-103">Oracle 데이터베이스 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="f8915-103">Get started with the Oracle Database connector</span></span>

<span data-ttu-id="f8915-104">Oracle 데이터베이스 커넥터를 사용하여 기존 데이터베이스의 데이터를 사용하는 조직 워크플로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-104">Using the Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="f8915-105">이 커넥터는 온-프레미스 Oracle 데이터베이스 또는 Oracle 데이터베이스가 설치된 Azure 가상 컴퓨터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-105">This connector can connect to an on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="f8915-106">이 커넥터를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-106">With this connector, you can:</span></span>

* <span data-ttu-id="f8915-107">고객 데이터베이스에 새 고객을 추가하거나 주문 데이터베이스에서 주문을 업데이트하여 워크플로를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-107">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="f8915-108">데이터의 행을 가져오고, 새 행을 삽입하고, 삭제하는 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-108">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="f8915-109">예를 들어 Dynamics CRM Online에서 레코드가 만들어지면(트리거) Oracle 데이터베이스에 행을 삽입합니다(작업).</span><span class="sxs-lookup"><span data-stu-id="f8915-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="f8915-110">이 항목에서는 논리 앱에서 Oracle 데이터베이스 커넥터를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-110">This topic shows you how to use the Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8915-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f8915-111">Prerequisites</span></span>

* <span data-ttu-id="f8915-112">지원되는 Oracle 버전:</span><span class="sxs-lookup"><span data-stu-id="f8915-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="f8915-113">Oracle 9 이상</span><span class="sxs-lookup"><span data-stu-id="f8915-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="f8915-114">Oracle 클라이언트 소프트웨어 8.1.7 이상</span><span class="sxs-lookup"><span data-stu-id="f8915-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="f8915-115">온-프레미스 데이터 게이트웨이 설치</span><span class="sxs-lookup"><span data-stu-id="f8915-115">Install the on-premises data gateway.</span></span> <span data-ttu-id="f8915-116">[논리 앱에서 온-프레미스 데이터에 연결](../logic-apps/logic-apps-gateway-connection.md)에 단계가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-116">[Connect to on-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists the steps.</span></span> <span data-ttu-id="f8915-117">게이트웨이는 온-프레미스 Oracle 데이터베이스 또는 Oracle DB가 설치된 Azure VM에 연결하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-117">The gateway is required to connect to an on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="f8915-118">온-프레미스 데이터 게이트웨이는 브리지 역할로, 온-프레미스 데이터(클라우드의 데이터가 아님)와 논리 앱 간의 보안 데이터 전송을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-118">The on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in the cloud) and your logic apps.</span></span> <span data-ttu-id="f8915-119">여러 서비스 및 데이터 원본에 동일한 게이트웨이를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-119">The same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="f8915-120">따라서 게이트웨이를 한 번만 설치해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-120">So, you may only need to install the gateway once.</span></span>

* <span data-ttu-id="f8915-121">온-프레미스 데이터 게이트웨이를 설치한 컴퓨터에 Oracle 클라이언트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-121">Install the Oracle Client on the machine where you installed the on-premises data gateway.</span></span> <span data-ttu-id="f8915-122">Oracle에서 제공하는 64비트 .NET용 Oracle Data Provider를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-122">Be sure to install the 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="f8915-123">Windows x64용 64비트 ODAC 12c 릴리스 4(12.1.0.2.4)</span><span class="sxs-lookup"><span data-stu-id="f8915-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="f8915-124">Oracle 클라이언트가 설치되지 않으면 연결을 생성하거나 사용할 때 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-124">If the Oracle client is not installed, an error occurs when you try to create or use the connection.</span></span> <span data-ttu-id="f8915-125">이 항목의 일반적인 오류를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8915-125">See the common errors in this topic.</span></span>


## <a name="add-the-connector"></a><span data-ttu-id="f8915-126">커넥터 추가</span><span class="sxs-lookup"><span data-stu-id="f8915-126">Add the connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8915-127">이 연결에는 트리거가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-127">This connector does not have any triggers.</span></span> <span data-ttu-id="f8915-128">작업만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-128">It has only actions.</span></span> <span data-ttu-id="f8915-129">따라서 논리 앱을 만들 때 **일정 - 되풀이** 또는 **요청/응답 - 응답**처럼 논리 앱을 시작하는 다른 트리거를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-129">So when you create your logic app, add another trigger to start your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="f8915-130">[Azure Portal](https://portal.azure.com)에서 빈 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-130">In the [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="f8915-131">논리 앱 시작 시 **요청/응답 - 요청** 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-131">At the start of your logic app, select the **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="f8915-132">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-132">Select **Save**.</span></span> <span data-ttu-id="f8915-133">저장하면 요청 URL이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="f8915-134">**새 단계**를 선택한 다음 **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="f8915-135">사용 가능한 작업을 보려면 `oracle`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-135">Type in `oracle` to see the available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="f8915-136">이 방법은 커넥터에 대해 사용 가능한 트리거 및 작업을 확인하는 가장 빠른 방법이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-136">This is also the quickest way to see the triggers and actions available for any connector.</span></span> <span data-ttu-id="f8915-137">커넥터 이름의 일부를 입력합니다(예: `oracle`).</span><span class="sxs-lookup"><span data-stu-id="f8915-137">Type in part of the connector name, such as `oracle`.</span></span> <span data-ttu-id="f8915-138">디자이너에 모든 트리거 및 작업이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-138">The designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="f8915-139">작업 중 하나를 선택합니다(예: **Oracle 데이터베이스 - 행 가져오기**).</span><span class="sxs-lookup"><span data-stu-id="f8915-139">Select one of the actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="f8915-140">**온-프레미스 데이터 게이트웨이를 통해 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="f8915-141">Oracle 서버 이름, 인증 방법, 사용자 이름, 암호를 입력하고 게이트웨이를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-141">Enter the Oracle server name, authentication method, username, password, and select the gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="f8915-142">연결되었으면 목록에서 테이블을 선택하고 테이블에 행 ID를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-142">Once connected, select a table from the list, and enter the row ID to your table.</span></span> <span data-ttu-id="f8915-143">테이블에 대한 식별자를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-143">You need to know the identifier to the table.</span></span> <span data-ttu-id="f8915-144">모르는 경우 Oracle DB 관리자에게 연락하고 `select * from yourTableName`에서 출력을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-144">If you don't know, contact your Oracle DB administrator, and get the output from `select * from yourTableName`.</span></span> <span data-ttu-id="f8915-145">그러면 진행하는 데 필요한 식별 가능한 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-145">This gives you the identifiable information you need to proceed.</span></span>

    <span data-ttu-id="f8915-146">다음 예제에서는 인사 관리 데이터베이스에서 작업 데이터가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-146">In the following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="f8915-147">다음 단계에서는 다른 커넥터를 사용하여 워크플로를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-147">In this next step, you can use any of the other connectors to build your workflow.</span></span> <span data-ttu-id="f8915-148">Oracle에서 데이터 가져오기를 테스트하려면 전자 메일 보내기 커넥터(예: Office 365 또는 Gmail) 중 하나를 사용하여 Oracle 데이터가 포함된 전자 메일을 직접 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-148">If you want to test getting data from Oracle, then send yourself an email with the Oracle data using one of the send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="f8915-149">Oracle 테이블의 동적 토큰을 사용하여 전자 메일의 `Subject` 및 `Body`을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-149">Use the dynamic tokens from the Oracle table to build the `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="f8915-150">논리 앱을 **저장**한 후 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="f8915-151">디자이너를 선택하고 실행 기록에서 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-151">Close the designer, and look at the runs history for the status.</span></span> <span data-ttu-id="f8915-152">실패하면 실패한 메시지 행을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-152">If it fails, select the failed message row.</span></span> <span data-ttu-id="f8915-153">디자이너가 열리고 어떤 단계에서 실패했는지와 오류 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-153">The designer opens, and shows you which step failed, and also shows the error information.</span></span> <span data-ttu-id="f8915-154">성공하면 추가된 정보와 함께 전자 메일을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-154">If it succeeds, then you should receive an email with the information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="f8915-155">워크플로 아이디어</span><span class="sxs-lookup"><span data-stu-id="f8915-155">Workflow ideas</span></span>

* <span data-ttu-id="f8915-156">\#oracle 해시 태그를 모니터하고 데이터베이스에 트윗을 배치하여 다른 응용 프로그램 내에서 사용하고 쿼리할 수 있도록 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-156">You want to monitor the #oracle hashtag, and put the tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="f8915-157">논리 앱에서 `Twitter - When a new tweet is posted` 트리거를 추가하고 **#oracle** 해시 태그를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-157">In a logic app, add the `Twitter - When a new tweet is posted` trigger, and enter the **#oracle** hashtag.</span></span> <span data-ttu-id="f8915-158">그런 다음 `Oracle Database - Insert row` 작업을 추가하고 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-158">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="f8915-159">메시지가 Service Bus 큐에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-159">Messages are sent to a Service Bus queue.</span></span> <span data-ttu-id="f8915-160">이러한 메시지를 가져와 데이터베이스에 넣으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-160">You want to get these messages, and put them in a database.</span></span> <span data-ttu-id="f8915-161">논리 앱에서 `Service Bus - when a message is received in a queue` 트리거를 추가하고 큐를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-161">In a logic app, add the `Service Bus - when a message is received in a queue` trigger, and select the queue.</span></span> <span data-ttu-id="f8915-162">그런 다음 `Oracle Database - Insert row` 작업을 추가하고 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-162">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="f8915-163">일반 오류</span><span class="sxs-lookup"><span data-stu-id="f8915-163">Common errors</span></span>

#### <a name="error-cannot-reach-the-gateway"></a><span data-ttu-id="f8915-164">**오류**: 게이트웨이에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-164">**Error**: Cannot reach the Gateway</span></span>

<span data-ttu-id="f8915-165">**원인**: 온-프레미스 데이터 게이트웨이가 클라우드에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-165">**Cause**: The on-premises data gateway is not able to connect to the cloud.</span></span> 

<span data-ttu-id="f8915-166">**완화**: 게이트웨이가 설치되어 있는 온-프레미스 컴퓨터에서 실행 중이며 인터넷에 연결할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-166">**Mitigation**: Make sure your gateway is running on the on-premises machine where you installed it, and that it can connect to the internet.</span></span>  <span data-ttu-id="f8915-167">꺼져 있거나 절전 모드 상태일 수 있는 컴퓨터에는 게이트웨이를 설치하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-167">We recommend not installing the gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="f8915-168">온-프레미스 데이터 게이트웨이 서비스(PBIEgwService)를 다시 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-168">You can also restart the on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-the-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-to-install-the-official-provider"></a><span data-ttu-id="f8915-169">**오류**: 사용 중인 공급자가 사용 중단됨: 'System.Data.OracleClient에 Oracle 클라이언트 소프트웨어 버전 8.1.7 이상이 필요합니다.'</span><span class="sxs-lookup"><span data-stu-id="f8915-169">**Error**: The provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="f8915-170">공식 공급자를 설치하려면 [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="f8915-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) to install the official provider.</span></span>

<span data-ttu-id="f8915-171">**원인**: 온-프레미스 데이터 게이트웨이가 실행 중인 컴퓨터에 Oracle 클라이언트 SDK가 설치되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-171">**Cause**: The Oracle client SDK is not installed on the machine where the on-premises data gateway is running.</span></span>  

<span data-ttu-id="f8915-172">**해결 방법**: 온-프레미스 데이터 게이트웨이와 동일한 컴퓨터에 Oracle 클라이언트 SDK를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-172">**Resolution**: Download and install the Oracle client SDK on the same computer as the on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="f8915-173">**오류**: 테이블 '[Tablename]'에 키 열이 정의되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="f8915-174">**원인**: 테이블에 기본 키가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-174">**Cause**: The table does not have any primary key.</span></span>  

<span data-ttu-id="f8915-175">**해결 방법**: Oracle 데이터베이스 커넥터에는 기본 키 열이 있는 테이블을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-175">**Resolution**: The Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="f8915-176">현재 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="f8915-176">Currently not supported</span></span>

* <span data-ttu-id="f8915-177">뷰 및 저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="f8915-177">Views and stored procedures</span></span> 
* <span data-ttu-id="f8915-178">복합 키가 있는 모든 테이블</span><span class="sxs-lookup"><span data-stu-id="f8915-178">Any table with composite keys</span></span>
* <span data-ttu-id="f8915-179">테이블의 중첩된 개체 유형</span><span class="sxs-lookup"><span data-stu-id="f8915-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="f8915-180">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="f8915-180">Connector-specific details</span></span>

<span data-ttu-id="f8915-181">[커넥터 세부 정보](/connectors/oracle/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-181">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="f8915-182">도움 받기</span><span class="sxs-lookup"><span data-stu-id="f8915-182">Get some help</span></span>

<span data-ttu-id="f8915-183">[Azure Logic Apps 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)에서는 질문하고, 질문에 답변하고, 다른 Logic Apps 사용자가 어떤 일을 하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-183">The [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place to ask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="f8915-184">[http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish)에서 투표하고 아이디어를 제출해 주시면 Logic Apps 및 커넥터를 개선하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8915-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="f8915-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8915-185">Next steps</span></span>
<span data-ttu-id="f8915-186">[논리 앱을 만들고](../logic-apps/logic-apps-create-a-logic-app.md) [API 목록](apis-list.md)에서 Logic Apps의 사용 가능한 커넥터를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f8915-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore the available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
