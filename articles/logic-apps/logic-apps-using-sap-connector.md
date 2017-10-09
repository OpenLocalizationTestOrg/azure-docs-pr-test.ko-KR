---
title: "aaaConnect tooan 온-프레미스 SAP 시스템에 Azure 논리 앱 | Microsoft Docs"
description: "Hello 온-프레미스 데이터 게이트웨이 통해 논리 앱 워크플로에서 tooan 온-프레미스 SAP 시스템에 연결"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a><span data-ttu-id="7c33e-103">Hello SAP connector 사용 하 여 논리 앱에서 tooan 온-프레미스 SAP 시스템에 연결</span><span class="sxs-lookup"><span data-stu-id="7c33e-103">Connect tooan on-premises SAP system from logic apps with hello SAP connector</span></span> 

<span data-ttu-id="7c33e-104">hello 온-프레미스 데이터 게이트웨이 toomanage 데이터 있으며는 온-프레미스 리소스에 안전 하 게 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-104">hello on-premises data gateway enables you toomanage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="7c33e-105">이 항목에서는 논리 앱 tooan 온-프레미스 SAP 시스템을 연결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-105">This topic shows how you can connect logic apps tooan on-premises SAP system.</span></span> <span data-ttu-id="7c33e-106">이 예제에서는 논리 앱 HTTP를 통한 IDOC를 요청 하 고 hello 응답을 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-106">In this example, your logic app requests an IDOC over HTTP and sends hello response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="7c33e-107">현재 제한 사항:</span><span class="sxs-lookup"><span data-stu-id="7c33e-107">Current limitations:</span></span> 
> - <span data-ttu-id="7c33e-108">Hello 응답에 필요한 모든 단계 hello 내에 완료 하지 않는 경우 논리 앱 시간 초과 [요청 시간 제한](./logic-apps-limits-and-config.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-108">Your logic app times out if all steps required for hello response don't finish within hello [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="7c33e-109">이 시나리오에서는 요청이 차단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="7c33e-110">hello 파일 선택기는 hello 사용 가능한 모든 필드를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-110">hello file picker does not display all hello available fields.</span></span> <span data-ttu-id="7c33e-111">이 시나리오에서는 경로를 수동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c33e-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7c33e-112">Prerequisites</span></span>

- <span data-ttu-id="7c33e-113">설치 하 고 최신 hello 구성 [온-프레미스 데이터 게이트웨이](https://www.microsoft.com/download/details.aspx?id=53127) 1.15.6150.1 버전 이상.</span><span class="sxs-lookup"><span data-stu-id="7c33e-113">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="7c33e-114">[어떻게 tooconnect toohello 온-프레미스 데이터 게이트웨이 논리 앱에서](http://aka.ms/logicapps-gateway) 목록 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-114">[How tooconnect toohello on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="7c33e-115">hello 게이트웨이 계속 하려면 먼저 온-프레미스 컴퓨터에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-115">hello gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="7c33e-116">다운로드 및 설치 hello 최신 SAP 클라이언트 라이브러리에 hello hello 데이터 게이트웨이 설치한 컴퓨터 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-116">Download and install hello latest SAP client library on hello same machine where you installed hello data gateway.</span></span> <span data-ttu-id="7c33e-117">Hello SAP 버전을 다음 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-117">Use any of hello following SAP versions:</span></span> 
    - <span data-ttu-id="7c33e-118">SAP Server</span><span class="sxs-lookup"><span data-stu-id="7c33e-118">SAP Server</span></span>
        - <span data-ttu-id="7c33e-119">SAP 서버는 지원 hello.NET 커넥터 (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="7c33e-119">Any SAP Server that support hello .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="7c33e-120">SAP Client</span><span class="sxs-lookup"><span data-stu-id="7c33e-120">SAP Client</span></span>
        - <span data-ttu-id="7c33e-121">SAP .NET Connector(NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="7c33e-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a><span data-ttu-id="7c33e-122">트리거 및 tooyour SAP 시스템 연결에 대 한 작업 추가</span><span class="sxs-lookup"><span data-stu-id="7c33e-122">Add triggers and actions for connecting tooyour SAP system</span></span>

<span data-ttu-id="7c33e-123">hello SAP connector에 동작을 있지만 트리거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-123">hello SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="7c33e-124">따라서는 toouse 다른 트리거 hello 워크플로의 hello 시작 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-124">So, we have toouse another trigger at hello start of hello workflow.</span></span> 

1. <span data-ttu-id="7c33e-125">Hello 요청/응답 트리거를 추가 하 고 다음 선택 **새 단계**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-125">Add hello Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="7c33e-126">선택 **동작 추가**, 다음을 입력 하 여 hello SAP 커넥터를 선택 하 고 `SAP` hello 검색 필드에:</span><span class="sxs-lookup"><span data-stu-id="7c33e-126">Select **Add an action**, and then select hello SAP connector by typing `SAP` in hello search field:</span></span>    

     ![SAP 응용 프로그램 서버 또는 SAP 메시지 서버 선택](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="7c33e-128">SAP 설치 프로그램에 따라 [**SAP 응용 프로그램 서버**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) 또는 [**SAP 메시지 서버**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="7c33e-129">기존 연결 되지 않은 경우 하나 toocreate 메시지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-129">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="7c33e-130">선택 **온-프레미스 데이터 게이트웨이 통해 연결**, SAP 시스템에 대 한 hello 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-130">Select **Connect via on-premises data gateway**, and enter hello details for your SAP system:</span></span>   

       ![연결 문자열 tooSAP 추가](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="7c33e-132">아래 **게이트웨이**, 기존 게이트웨이 또는 tooinstall 새 게이트웨이 선택, 선택 **게이트웨이 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-132">Under **Gateway**, select an existing gateway, or tooinstall a new gateway, select **Install Gateway**.</span></span>

        ![새 게이트웨이 설치](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="7c33e-134">Hello에 대 한 세부 정보를 모두 입력 한 후 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-134">After you enter all hello details, select **Create**.</span></span> 
   <span data-ttu-id="7c33e-135">논리 앱 구성 및 hello 연결이 제대로 작동 하는지 확인 하는 hello 연결을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-135">Logic Apps configures and tests hello connection, making sure that hello connection works properly.</span></span>

4. <span data-ttu-id="7c33e-136">SAP 연결의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="7c33e-137">hello 다른 SAP 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-137">hello different SAP options are now available.</span></span> <span data-ttu-id="7c33e-138">toofind IDOC 범주를 hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-138">toofind your IDOC category, select from hello list.</span></span> <span data-ttu-id="7c33e-139">Hello 경로 및 hello에 대 한 선택 hello HTTP 응답에 수동으로 입력 하거나 **본문** 필드:</span><span class="sxs-lookup"><span data-stu-id="7c33e-139">Or manually type in hello path, and select hello HTTP response in hello **body** field:</span></span>

     ![SAP 작업](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="7c33e-141">Hello 동작을 만들기 위한 추가 **HTTP 응답**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-141">Add hello action for creating an **HTTP Response**.</span></span> <span data-ttu-id="7c33e-142">hello 응답 메시지의 hello SAP 출력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-142">hello response message should be from hello SAP output.</span></span>

7. <span data-ttu-id="7c33e-143">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-143">Save your logic app.</span></span> <span data-ttu-id="7c33e-144">IDOC hello HTTP 트리거 URL 통해 전송 하 여 테스트 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7c33e-144">Test it by sending an IDOC through hello HTTP trigger URL.</span></span> <span data-ttu-id="7c33e-145">IDOC 보내집니다 hello, 후 hello 논리 앱에서 hello 응답을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-145">After hello IDOC is sent, wait for hello response from hello logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="7c33e-146">방법에 대해 너무 확인[논리 앱 모니터링](../logic-apps/logic-apps-monitor-your-logic-apps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-146">Check out how too[monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="7c33e-147">Hello SAP connector는 tooyour 논리 앱을 추가 하는 다른 기능과 탐색을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-147">Now that hello SAP connector is added tooyour logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="7c33e-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="7c33e-148">BAPI</span></span>
- <span data-ttu-id="7c33e-149">RFC</span><span class="sxs-lookup"><span data-stu-id="7c33e-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="7c33e-150">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="7c33e-150">Get help</span></span>

<span data-ttu-id="7c33e-151">tooask 질문 질문에 답변 하 고 다른 Azure 논리 앱을 수행 하는 사용자가 방문 hello 자세한 [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-151">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="7c33e-152">Azure 논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [Azure 논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-152">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c33e-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c33e-153">Next steps</span></span>

- <span data-ttu-id="7c33e-154">자세한 내용은 방법 toovalidate, 변환 및 다른 BizTalk와 비슷한 함수 hello에서 [엔터프라이즈 통합 팩](../logic-apps/logic-apps-enterprise-integration-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c33e-154">Learn how toovalidate, transform, and other BizTalk-like functions in hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="7c33e-155">[Tooon 온-프레미스 데이터 연결](../logic-apps/logic-apps-gateway-connection.md) 논리 앱에서</span><span class="sxs-lookup"><span data-stu-id="7c33e-155">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
