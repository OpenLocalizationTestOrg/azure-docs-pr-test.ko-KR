---
title: "논리 앱에서 FTP 커넥터를 사용하는 방법 알아보기 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. FTP 서버에 연결하여 파일을 관리합니다. FTP 서버에서 파일 업로드, 업데이트, 가져오기 및 삭제와 같은 다양한 작업을 수행할 수 있습니다."
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
ms.openlocfilehash: 61bfbedfd4f1e84b6976099323a32f3a720634c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="67267-105">FTP 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="67267-105">Get started with the FTP connector</span></span>
<span data-ttu-id="67267-106">FTP 커넥터를 사용하여 FTP 서버에서 파일을 모니터링 및 관리하고 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67267-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="67267-107">[커넥터](apis-list.md)를 사용하려면 먼저 논리 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-107">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="67267-108">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67267-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="67267-109">FTP에 연결</span><span class="sxs-lookup"><span data-stu-id="67267-109">Connect to FTP</span></span>
<span data-ttu-id="67267-110">논리 앱에서 서비스에 액세스하려면 먼저 서비스에 대한 *연결*을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="67267-111">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="67267-112">FTP에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="67267-112">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="67267-113">FTP 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="67267-113">Use a FTP trigger</span></span>
<span data-ttu-id="67267-114">트리거는 논리 앱에 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="67267-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="67267-115">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="67267-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="67267-116">FTP 커넥터를 사용하려면 인터넷에서 액세스할 수 있고 PASSIVE 모드로 작동하도록 구성된 FTP 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="67267-117">또한 FTP 커넥터는 **암시적 FTPS(FTP over SSL)와 호환되지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="67267-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="67267-118">FTP 커넥터는 명시적 FTPS(FTP over SSL)만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="67267-119">이 예제에서는 파일이 FTP 서버에 추가되거나 수정될 때 **FTP - 파일을 추가하거나 수정할 때** 트리거를 사용하여 논리 앱 워크플로를 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="67267-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="67267-120">엔터프라이즈 예에서는 이 트리거를 사용하여 고객의 주문을 나타내는 새 파일에 대한 FTP 폴더를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67267-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="67267-121">그런 다음 **파일 콘텐츠 가져오기**와 같은 FTP 커넥터 작업을 사용하여 추가 처리할 주문 및 주문 데이터베이스에 있는 저장소의 콘텐츠를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67267-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="67267-122">Logic Apps 디자이너의 검색 상자에 *ftp*를 입력한 후 **FTP - 파일을 추가하거나 수정할 때** 트리거를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="67267-123">![FTP 트리거 이미지 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="67267-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="67267-124">**파일을 추가하거나 수정할 때** 컨트롤이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="67267-124">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="67267-125">![FTP 트리거 이미지 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="67267-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="67267-126">컨트롤의 오른쪽에 있는 **...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-126">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="67267-127">이렇게 하면 폴더 선택 컨트롤이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="67267-127">This opens the folder picker control</span></span>  
   <span data-ttu-id="67267-128">![FTP 트리거 이미지 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="67267-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="67267-129">**>**(오른쪽 화살표)를 선택하고 새 파일 또는 수정된 파일을 모니터링할 폴더를 탐색하여 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="67267-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="67267-130">해당 폴더를 선택하면 이제 폴더가 **폴더** 컨트롤에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67267-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="67267-131">![FTP 트리거 이미지 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="67267-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="67267-132">이제, 논리 앱은 파일이 특정 FTP 폴더에서 수정되거나 만들어질 때 워크플로의 다른 트리거 및 작업의 실행을 시작하는 트리거로 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="67267-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="67267-133">논리 앱이 작동하려면 하나 이상의 트리거와 동작이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-133">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="67267-134">다음 섹션의 단계에 따라 동작을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-134">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="67267-135">FTP 작업 사용</span><span class="sxs-lookup"><span data-stu-id="67267-135">Use a FTP action</span></span>
<span data-ttu-id="67267-136">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="67267-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="67267-137">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="67267-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="67267-138">이제 트리거를 추가했으므로 다음 단계에 따라 트리거가 찾은 새 파일 또는 수정된 파일의 콘텐츠를 가져올 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="67267-139">**+ 새 단계**를 선택하여 FTP 서버에서 파일의 콘텐츠를 가져올 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="67267-140">**동작 추가** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-140">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="67267-141">![FTP 작업 이미지 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="67267-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="67267-142">*FTP*를 입력하여 FTP와 관련된 모든 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-142">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="67267-143">FTP 폴더에서 새 파일 또는 수정된 파일을 찾을 때 수행할 작업으로 **FTP - 파일 콘텐츠 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="67267-144">![FTP 작업 이미지 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="67267-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="67267-145">**파일 콘텐츠 가져오기** 컨트롤이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="67267-145">The **Get file content** control opens.</span></span> <span data-ttu-id="67267-146">**참고**: 논리 앱에 FTP 서버 계정에 액세스하기 위한 권한을 아직 부여하지 않았으면 이러한 권한을 부여하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67267-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="67267-147">![FTP 작업 이미지 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="67267-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="67267-148">**파일** 컨트롤(**FILE*** 아래에 흰색 영역)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-148">Select the **File** control (the white space located below **FILE***).</span></span> <span data-ttu-id="67267-149">여기에서 FTP 서버에서 찾은 새 파일 또는 수정된 파일의 다양한 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67267-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="67267-150">**파일 콘텐츠** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-150">Select the **File content** option.</span></span>  
   <span data-ttu-id="67267-151">![FTP 작업 이미지 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="67267-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="67267-152">컨트롤이 업데이트되고 **FTP - 파일 콘텐츠 가져오기** 작업에서 FTP 서버에 있는 새 파일 또는 수정된 파일의 *파일 콘텐츠*를 가져오는 것이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="67267-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="67267-153">![FTP 작업 이미지 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="67267-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="67267-154">작업을 저장한 후 파일을 FTP 폴더에 추가하여 워크플로를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="67267-154">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="67267-155">이제 FTP 서버에서 폴더를 모니터링하고 FTP 서버에서 새 파일 또는 수정된 파일을 찾으면 워크플로를 시작하는 트리거로 논리 앱이 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="67267-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="67267-156">또한 새 파일 또는 수정된 파일의 콘텐츠를 가져오는 작업으로도 논리 앱이 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="67267-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="67267-157">이제 새 파일 또는 수정된 파일의 콘텐츠를 SQL 데이터베이스 테이블에 삽입하는 [SQL Server - 행 삽입](connectors-create-api-sqlazure.md) 작업과 같은 다른 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67267-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="67267-158">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="67267-158">Connector-specific details</span></span>

<span data-ttu-id="67267-159">[커넥터 세부 정보](/connectors/ftpconnector/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67267-159">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="67267-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67267-160">Next Steps</span></span>
[<span data-ttu-id="67267-161">논리 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="67267-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

