---
title: "Azure 논리 앱에서 aaaAdd hello Oracle 데이터베이스 커넥터 | Microsoft Docs"
description: "Hello Oracle 데이터베이스 커넥터를 사용 하 여 논리 앱"
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
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a><span data-ttu-id="5109e-103">Hello Oracle 데이터베이스 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="5109e-103">Get started with hello Oracle Database connector</span></span>

<span data-ttu-id="5109e-104">기존 데이터베이스의 데이터를 사용 하는 조직 구성 워크플로 만들 hello Oracle 데이터베이스 커넥터를 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-104">Using hello Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="5109e-105">이 커넥터는 온-프레미스 Oracle 데이터베이스 또는 Oracle 데이터베이스와 Azure 가상 컴퓨터에 설치 된 tooan을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-105">This connector can connect tooan on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="5109e-106">이 커넥터를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-106">With this connector, you can:</span></span>

* <span data-ttu-id="5109e-107">새 고객 tooa 고객 데이터베이스를 추가 하거나 orders 데이터베이스에 순서를 업데이트 하 여 워크플로 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-107">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="5109e-108">동작 tooget 데이터 행을 사용 하 고, 새 행을 삽입 하 고 및 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-108">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="5109e-109">예를 들어 Dynamics CRM Online에서 레코드가 만들어지면(트리거) Oracle 데이터베이스에 행을 삽입합니다(작업).</span><span class="sxs-lookup"><span data-stu-id="5109e-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="5109e-110">이 항목에서는 toouse 논리 앱에서 Oracle 데이터베이스 커넥터 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-110">This topic shows you how toouse hello Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5109e-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="5109e-111">Prerequisites</span></span>

* <span data-ttu-id="5109e-112">지원되는 Oracle 버전:</span><span class="sxs-lookup"><span data-stu-id="5109e-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="5109e-113">Oracle 9 이상</span><span class="sxs-lookup"><span data-stu-id="5109e-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="5109e-114">Oracle 클라이언트 소프트웨어 8.1.7 이상</span><span class="sxs-lookup"><span data-stu-id="5109e-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="5109e-115">Hello 온-프레미스 데이터 게이트웨이 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-115">Install hello on-premises data gateway.</span></span> <span data-ttu-id="5109e-116">[논리 앱에서 tooon 온-프레미스 데이터 연결](../logic-apps/logic-apps-gateway-connection.md) 목록 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-116">[Connect tooon-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists hello steps.</span></span> <span data-ttu-id="5109e-117">hello 게이트웨이 온-프레미스 Oracle 데이터베이스 또는 Oracle DB 설치는 Azure VM에 필요한 tooconnect tooan입니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-117">hello gateway is required tooconnect tooan on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="5109e-118">hello 온-프레미스 데이터 게이트웨이 브리지 역할을 하 고 온-프레미스 데이터 (클라우드 hello에에서 없는 데이터) 및 논리 앱 간에 안전한 데이터 전송을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-118">hello on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in hello cloud) and your logic apps.</span></span> <span data-ttu-id="5109e-119">hello 여러 서비스와 여러 데이터 원본이 동일한 게이트웨이에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-119">hello same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="5109e-120">따라서만 해야 tooinstall hello 게이트웨이 한 번만 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-120">So, you may only need tooinstall hello gateway once.</span></span>

* <span data-ttu-id="5109e-121">Oracle 클라이언트 hello hello 온-프레미스 데이터 게이트웨이 설치한 hello 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-121">Install hello Oracle Client on hello machine where you installed hello on-premises data gateway.</span></span> <span data-ttu-id="5109e-122">Tooinstall는 64 비트 Oracle Data Provider for Oracle에서.NET hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-122">Be sure tooinstall hello 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="5109e-123">Windows x64용 64비트 ODAC 12c 릴리스 4(12.1.0.2.4)</span><span class="sxs-lookup"><span data-stu-id="5109e-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="5109e-124">Hello Oracle 클라이언트가 설치 되지 않은 경우 toocreate 시도 하거나 hello 연결을 사용할 때 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-124">If hello Oracle client is not installed, an error occurs when you try toocreate or use hello connection.</span></span> <span data-ttu-id="5109e-125">이 항목의 일반적인 오류 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5109e-125">See hello common errors in this topic.</span></span>


## <a name="add-hello-connector"></a><span data-ttu-id="5109e-126">Hello 커넥터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-126">Add hello connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5109e-127">이 연결에는 트리거가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-127">This connector does not have any triggers.</span></span> <span data-ttu-id="5109e-128">작업만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-128">It has only actions.</span></span> <span data-ttu-id="5109e-129">따라서 논리 앱을 만들 때 다른 트리거 toostart 논리 앱와 같은 추가 **되풀이 일정을 예약**, 또는 **요청 / 응답-응답**합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-129">So when you create your logic app, add another trigger toostart your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="5109e-130">Hello에 [Azure 포털](https://portal.azure.com), 빈 논리 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-130">In hello [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="5109e-131">논리 앱을 hello 시작 시 hello 선택 **요청 / 응답-요청** 트리거:</span><span class="sxs-lookup"><span data-stu-id="5109e-131">At hello start of your logic app, select hello **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="5109e-132">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-132">Select **Save**.</span></span> <span data-ttu-id="5109e-133">저장하면 요청 URL이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="5109e-134">**새 단계**를 선택한 다음 **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="5109e-135">에 입력 `oracle` toosee hello 사용 가능한 작업:</span><span class="sxs-lookup"><span data-stu-id="5109e-135">Type in `oracle` toosee hello available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="5109e-136">이 가장 빠른 방법은 toosee hello도 hello 트리거 및 모든 커넥터에 대해 사용할 수 있는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-136">This is also hello quickest way toosee hello triggers and actions available for any connector.</span></span> <span data-ttu-id="5109e-137">와 같은 일부 hello 커넥터 이름에서에서 입력 `oracle`합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-137">Type in part of hello connector name, such as `oracle`.</span></span> <span data-ttu-id="5109e-138">hello 디자이너는 트리거 및 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-138">hello designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="5109e-139">과 같은 hello 작업 중 하나를 선택 **Oracle 데이터베이스-Get 행**합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-139">Select one of hello actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="5109e-140">**온-프레미스 데이터 게이트웨이를 통해 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="5109e-141">Hello Oracle 서버 이름, 인증 방법, 사용자 이름, 암호 및 선택 hello 게이트웨이 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-141">Enter hello Oracle server name, authentication method, username, password, and select hello gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="5109e-142">연결 되 면 hello 목록에서 테이블을 선택 하 고 hello 행 ID tooyour 테이블을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-142">Once connected, select a table from hello list, and enter hello row ID tooyour table.</span></span> <span data-ttu-id="5109e-143">Tooknow hello 식별자 toohello 테이블이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-143">You need tooknow hello identifier toohello table.</span></span> <span data-ttu-id="5109e-144">Oracle DB 관리자에 게 문의 하 고에서 hello 출력을 가져올 알지 못하는 경우 `select * from yourTableName`합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-144">If you don't know, contact your Oracle DB administrator, and get hello output from `select * from yourTableName`.</span></span> <span data-ttu-id="5109e-145">이렇게 하면 tooproceed 필요한 식별이 가능한 정보 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-145">This gives you hello identifiable information you need tooproceed.</span></span>

    <span data-ttu-id="5109e-146">다음 예제는 hello, 인사 관리 데이터베이스에서 작업 데이터를 반환 되 고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-146">In hello following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="5109e-147">다음이 단계에서 사용할 수 있습니다 hello의 다른 커넥터가 toobuild 워크플로에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-147">In this next step, you can use any of hello other connectors toobuild your workflow.</span></span> <span data-ttu-id="5109e-148">Oracle에서 데이터를 가져오지 tootest 원하는 다음 사용자가 직접 hello 중 하나를 사용 하 여 hello Oracle 데이터와 전자 메일 보내기에 해당 하는 Office 365 또는 Gmail 메일 커넥터 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-148">If you want tootest getting data from Oracle, then send yourself an email with hello Oracle data using one of hello send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="5109e-149">Hello Oracle 테이블 toobuild hello의 hello 동적 토큰을 사용 하 여 `Subject` 및 `Body` 전자 메일:</span><span class="sxs-lookup"><span data-stu-id="5109e-149">Use hello dynamic tokens from hello Oracle table toobuild hello `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="5109e-150">논리 앱을 **저장**한 후 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="5109e-151">Hello 디자이너를 닫고 hello 상태에 대 한 실행 기록을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-151">Close hello designer, and look at hello runs history for hello status.</span></span> <span data-ttu-id="5109e-152">실패 한 경우 hello 메시지 실패 한 행을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-152">If it fails, select hello failed message row.</span></span> <span data-ttu-id="5109e-153">hello 디자이너가 열리고 오류 정보를 hello 및 실패 단계 된 방법을 보여 줍니다.도 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-153">hello designer opens, and shows you which step failed, and also shows hello error information.</span></span> <span data-ttu-id="5109e-154">성공 하면 추가한 hello 정보로 메일을 받을 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-154">If it succeeds, then you should receive an email with hello information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="5109e-155">워크플로 아이디어</span><span class="sxs-lookup"><span data-stu-id="5109e-155">Workflow ideas</span></span>

* <span data-ttu-id="5109e-156">Toomonitor hello #oracle hashtag 원하는 쿼리 및 다른 응용 프로그램 내에서 사용할 수 있도록 데이터베이스의 hello 트 윗을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-156">You want toomonitor hello #oracle hashtag, and put hello tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="5109e-157">논리 앱에서 추가 hello `Twitter - When a new tweet is posted` 트리거되며 hello 입력 **#oracle** hashtag 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-157">In a logic app, add hello `Twitter - When a new tweet is posted` trigger, and enter hello **#oracle** hashtag.</span></span> <span data-ttu-id="5109e-158">Hello을 추가 합니다 `Oracle Database - Insert row` 동작을 사용자 테이블을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-158">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="5109e-159">Tooa 서비스 버스 큐를 다시 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-159">Messages are sent tooa Service Bus queue.</span></span> <span data-ttu-id="5109e-160">Tooget 이러한 메시지를 한 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-160">You want tooget these messages, and put them in a database.</span></span> <span data-ttu-id="5109e-161">논리 앱에서 추가 hello `Service Bus - when a message is received in a queue` 트리거와 선택 hello 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-161">In a logic app, add hello `Service Bus - when a message is received in a queue` trigger, and select hello queue.</span></span> <span data-ttu-id="5109e-162">Hello을 추가 합니다 `Oracle Database - Insert row` 동작을 사용자 테이블을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-162">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="5109e-163">일반 오류</span><span class="sxs-lookup"><span data-stu-id="5109e-163">Common errors</span></span>

#### <a name="error-cannot-reach-hello-gateway"></a><span data-ttu-id="5109e-164">**오류**: hello 게이트웨이 연결할 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="5109e-164">**Error**: Cannot reach hello Gateway</span></span>

<span data-ttu-id="5109e-165">**원인**: hello 온-프레미스 데이터 게이트웨이 수 tooconnect toohello 클라우드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-165">**Cause**: hello on-premises data gateway is not able tooconnect toohello cloud.</span></span> 

<span data-ttu-id="5109e-166">**완화**: 게이트웨이 설치 하 고 한다는 toohello 연결할 수 있는 hello 온-프레미스 컴퓨터에서 실행 되 고 있는지 확인 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-166">**Mitigation**: Make sure your gateway is running on hello on-premises machine where you installed it, and that it can connect toohello internet.</span></span>  <span data-ttu-id="5109e-167">해제 되어 있는 컴퓨터 또는 절전 모드를 hello 게이트웨이 설치 하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-167">We recommend not installing hello gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="5109e-168">Hello 온-프레미스 데이터 게이트웨이 서비스 (PBIEgwService)를 다시 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-168">You can also restart hello on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a><span data-ttu-id="5109e-169">**오류**: 사용 중인 hello 공급자는 사용 되지 않습니다: ' System.Data.OracleClient 필요 Oracle 클라이언트 소프트웨어 버전 8.1.7 이상입니다.'.</span><span class="sxs-lookup"><span data-stu-id="5109e-169">**Error**: hello provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="5109e-170">방문 하세요 [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello 공식 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello official provider.</span></span>

<span data-ttu-id="5109e-171">**원인**: hello Oracle 클라이언트 SDK에 설치 되어 있지 hello 컴퓨터 위치 hello 온-프레미스 데이터 게이트웨이가 실행 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-171">**Cause**: hello Oracle client SDK is not installed on hello machine where hello on-premises data gateway is running.</span></span>  

<span data-ttu-id="5109e-172">**해결 방법**:에 다운로드 및 설치 hello Oracle 클라이언트 SDK hello hello 온-프레미스 데이터 게이트웨이와 동일한 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="5109e-172">**Resolution**: Download and install hello Oracle client SDK on hello same computer as hello on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="5109e-173">**오류**: 테이블 '[Tablename]'에 키 열이 정의되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="5109e-174">**원인**: hello 테이블의 모든 기본 키가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-174">**Cause**: hello table does not have any primary key.</span></span>  

<span data-ttu-id="5109e-175">**해결 방법**: hello Oracle 데이터베이스 커넥터는 기본 키 열에 있는 테이블을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-175">**Resolution**: hello Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="5109e-176">현재 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="5109e-176">Currently not supported</span></span>

* <span data-ttu-id="5109e-177">뷰 및 저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="5109e-177">Views and stored procedures</span></span> 
* <span data-ttu-id="5109e-178">복합 키가 있는 모든 테이블</span><span class="sxs-lookup"><span data-stu-id="5109e-178">Any table with composite keys</span></span>
* <span data-ttu-id="5109e-179">테이블의 중첩된 개체 유형</span><span class="sxs-lookup"><span data-stu-id="5109e-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="5109e-180">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="5109e-180">Connector-specific details</span></span>

<span data-ttu-id="5109e-181">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/oracle/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-181">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="5109e-182">도움 받기</span><span class="sxs-lookup"><span data-stu-id="5109e-182">Get some help</span></span>

<span data-ttu-id="5109e-183">hello [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) 는 좋은 tooask 질문 배치 질문에 답변 하 고 다른 논리 앱 사용자가 수행 하는 작업을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-183">hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place tooask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="5109e-184">[http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish)에서 투표하고 아이디어를 제출해 주시면 Logic Apps 및 커넥터를 개선하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="5109e-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5109e-185">Next steps</span></span>
<span data-ttu-id="5109e-186">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md), hello에서 논리 앱에서 사용할 수 있는 커넥터를 탐색 하 고 우리의 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5109e-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore hello available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
