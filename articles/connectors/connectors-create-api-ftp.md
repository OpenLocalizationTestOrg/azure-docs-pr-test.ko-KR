---
title: "aaaLearn 어떻게 toouse hello 논리 앱에서 FTP 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. TooFTP 서버 toomanage 파일을 연결 합니다. FTP 서버에서 파일 업로드, 업데이트, 가져오기 및 삭제와 같은 다양한 작업을 수행할 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a><span data-ttu-id="e6cbc-105">Hello FTP 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="e6cbc-105">Get started with hello FTP connector</span></span>
<span data-ttu-id="e6cbc-106">커넥터 toomonitor hello FTP 사용 하 여 관리 하 고 FTP 서버에서 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-106">Use hello FTP connector toomonitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="e6cbc-107">toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-107">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="e6cbc-108">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooftp"></a><span data-ttu-id="e6cbc-109">TooFTP 연결</span><span class="sxs-lookup"><span data-stu-id="e6cbc-109">Connect tooFTP</span></span>
<span data-ttu-id="e6cbc-110">Toocreate 먼저 논리 앱에서 모든 서비스에 액세스 하기 전에 *연결* toohello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-110">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="e6cbc-111">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tooftp"></a><span data-ttu-id="e6cbc-112">연결 tooFTP 만들기</span><span class="sxs-lookup"><span data-stu-id="e6cbc-112">Create a connection tooFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="e6cbc-113">FTP 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="e6cbc-113">Use a FTP trigger</span></span>
<span data-ttu-id="e6cbc-114">트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="e6cbc-115">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="e6cbc-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="e6cbc-116">hello FTP 커넥터 hello 인터넷에서에서 액세스할 수 있으며가 FTP 서버 수동 모드 toooperate를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-116">hello FTP connector requires an FTP server that  is accessible from hello Internet and is configured toooperate with PASSIVE mode.</span></span> <span data-ttu-id="e6cbc-117">Hello FTP 커넥터는 또한 **암시적 FTPS (FTP SSL 통해)와 호환 되지 않는**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-117">Also, hello FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="e6cbc-118">hello FTP 커넥터 명시적 FTPS (FTP SSL 통한)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-118">hello FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="e6cbc-119">이 예제에서는 하겠습니다 어떻게 toouse hello **FTP-파일을 추가 하거나 수정 하는 경우** 파일은 추가, 또는 FTP 서버에서 수정 될 때 tooinitiate 논리 앱 워크플로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-119">In this example, I will show you how toouse hello **FTP - When a file is added or modified** trigger tooinitiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="e6cbc-120">엔터프라이즈 예를 들어 고객 으로부터 주문을 나타내는 새 파일에 대 한이 트리거 toomonitor FTP 폴더를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-120">In an enterprise example, you could use this trigger toomonitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="e6cbc-121">사용할 수 있습니다 다음 FTP 커넥터 작업 같은 **파일 콘텐츠를 가져옵니다.** tooget hello 내용의 hello 순서 추가 처리 및 orders 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-121">You could then use an FTP connector action such as **Get file content** tooget hello contents of hello order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="e6cbc-122">입력 *ftp* hello 논리 앱 디자이너에 hello 검색 상자에 다음 hello 선택 **FTP-파일 추가 또는 수정 되 면** 트리거</span><span class="sxs-lookup"><span data-stu-id="e6cbc-122">Enter *ftp* in hello search box on hello logic apps designer then select hello **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="e6cbc-123">![FTP 트리거 이미지 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="e6cbc-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="e6cbc-124">hello **파일 추가 또는 수정할 때** 제어 열립니다</span><span class="sxs-lookup"><span data-stu-id="e6cbc-124">hello **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="e6cbc-125">![FTP 트리거 이미지 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="e6cbc-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="e6cbc-126">선택 hello **...**  hello hello 컨트롤의 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-126">Select hello **...** located on hello right side of hello control.</span></span> <span data-ttu-id="e6cbc-127">Hello 폴더 선택 컨트롤을 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-127">This opens hello folder picker control</span></span>  
   <span data-ttu-id="e6cbc-128">![FTP 트리거 이미지 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="e6cbc-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="e6cbc-129">선택 hello  **>**  (오른쪽 화살표) 새롭거나 수정 된 파일에 대 한 toomonitor 되도록 toofind hello 폴더를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-129">Select hello **>** (right arrow) and browse toofind hello folder that you want toomonitor for new or modified files.</span></span> <span data-ttu-id="e6cbc-130">Hello 폴더를 선택 하 고 hello 폴더는 hello에 표시 된 **폴더** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-130">Select hello folder and notice hello folder is now displayed in hello **Folder** control.</span></span>  
   <span data-ttu-id="e6cbc-131">![FTP 트리거 이미지 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="e6cbc-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="e6cbc-132">이 시점에서 논리 앱 때 시작 될 hello 실행 하는 다른 트리거 및 hello 워크플로에서 작업 파일을 수정 또는 hello 특정 FTP 폴더에 생성 하는 트리거도 구성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-132">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow when a file is either modified or created in hello specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="e6cbc-133">기능 논리 앱 toobe는, 하나 이상의 트리거와 작업을 하나 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-133">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="e6cbc-134">Hello 다음 섹션 tooadd 동작의에서 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-134">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="e6cbc-135">FTP 작업 사용</span><span class="sxs-lookup"><span data-stu-id="e6cbc-135">Use a FTP action</span></span>
<span data-ttu-id="e6cbc-136">동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="e6cbc-137">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="e6cbc-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="e6cbc-138">트리거를 추가 하면 했으므로 이러한 단계 tooadd을 hello 트리거가 여 hello 새롭거나 수정 된 파일의 hello 내용의 받을 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-138">Now that you have added a trigger, follow these steps tooadd an action that will get hello contents of hello new or modified file found by hello trigger.</span></span>    

1. <span data-ttu-id="e6cbc-139">선택 **+ 새 단계** tooadd hello hello 동작 tooget hello hello에 파일의 내용을 hello FTP 서버</span><span class="sxs-lookup"><span data-stu-id="e6cbc-139">Select **+ New step** tooadd hello hello action tooget hello contents of hello file on hello FTP server</span></span>  
2. <span data-ttu-id="e6cbc-140">선택 hello **동작 추가** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-140">Select hello **Add an action** link.</span></span>  
   <span data-ttu-id="e6cbc-141">![FTP 작업 이미지 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="e6cbc-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="e6cbc-142">입력 *FTP* toosearch 모든 작업에 대 한 관련 tooFTP 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-142">Enter *FTP* toosearch for all actions related tooFTP.</span></span>
4. <span data-ttu-id="e6cbc-143">선택 **FTP-파일 내용을 가져오기** hello FTP 폴더에는 새로운 또는 수정 된 파일을 찾으면 동작 tootake hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-143">Select **FTP - Get file content**  as hello action tootake when a new or modified file is found in hello FTP folder.</span></span>      
   <span data-ttu-id="e6cbc-144">![FTP 작업 이미지 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="e6cbc-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="e6cbc-145">hello **파일 콘텐츠를 가져옵니다.** 제어 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-145">hello **Get file content** control opens.</span></span> <span data-ttu-id="e6cbc-146">**참고**: 있습니다 하지 않았으면 지금 이전에 FTP 서버 계정을 하 여 논리 앱 tooaccess tooauthorize 메시지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-146">**Note**: you will be prompted tooauthorize your logic app tooaccess your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="e6cbc-147">![FTP 작업 이미지 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="e6cbc-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="e6cbc-148">선택 hello **파일** 컨트롤 (아래에 있는 공백을 hello **파일***).</span><span class="sxs-lookup"><span data-stu-id="e6cbc-148">Select hello **File** control (hello white space located below **FILE***).</span></span> <span data-ttu-id="e6cbc-149">여기에서 사용할 수 있습니다 hello의 다양 한 속성이 hello FTP 서버에서 발견 된 hello 새롭거나 수정 된 파일에서.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-149">Here, you can use any of hello various properties from hello new or modified file found on hello FTP server.</span></span>  
6. <span data-ttu-id="e6cbc-150">선택 hello **콘텐츠 파일** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-150">Select hello **File content** option.</span></span>  
   <span data-ttu-id="e6cbc-151">![FTP 작업 이미지 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="e6cbc-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="e6cbc-152">해당 hello 나타내는 hello 컨트롤을 업데이트 **FTP-파일 내용을 가져오기** 작업 hello 받아볼 *콘텐츠 파일* hello FTP 서버에 hello 새롭거나 수정 된 파일의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-152">hello control is updated, indicating that hello **FTP - Get file content** action will get hello *file content* of hello new or modified file on hello FTP server.</span></span>      
   <span data-ttu-id="e6cbc-153">![FTP 작업 이미지 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="e6cbc-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="e6cbc-154">작업을 저장 한 다음 파일 toohello FTP 폴더 tootest 워크플로에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-154">Save your work then add a file toohello FTP folder tootest your workflow.</span></span>    

<span data-ttu-id="e6cbc-155">Hello 논리 앱 되었습니다이 시점에 구성 된 트리거 toomonitor로 폴더는 FTP 서버와 시작 hello 워크플로 새 파일 또는 hello FTP 서버에서 수정 된 파일을 찾으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-155">At this point, hello logic app has been configured with a trigger toomonitor a folder on an FTP server and initiate hello workflow when it finds either a new file or a modified file on hello FTP server.</span></span> 

<span data-ttu-id="e6cbc-156">또한 hello 논리 앱 hello 새롭거나 수정 된 파일의 동작 tooget hello 내용으로 구성 되어 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-156">hello logic app also has been configured with an action tooget hello contents of hello new or modified file.</span></span>

<span data-ttu-id="e6cbc-157">이제 hello와 같은 다른 작업을 추가할 수 있습니다 [SQL Server-행 삽입](connectors-create-api-sqlazure.md) hello 새롭거나 수정 된 파일을 SQL 데이터베이스 테이블에 내용의 tooinsert hello 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-157">You can now add another action such as hello [SQL Server - insert row](connectors-create-api-sqlazure.md) action tooinsert hello contents of hello new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="e6cbc-158">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e6cbc-158">Connector-specific details</span></span>

<span data-ttu-id="e6cbc-159">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/ftpconnector/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6cbc-159">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e6cbc-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6cbc-160">Next Steps</span></span>
[<span data-ttu-id="e6cbc-161">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e6cbc-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

