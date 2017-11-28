---
title: "Azure Logic Apps에서 온-프레미스 파일 시스템에 연결 | Microsoft Docs"
description: "온-프레미스 데이터 게이트웨이 및 파일 시스템 커넥터를 통해 논리 앱 워크플로에서 온-프레미스 파일 시스템에 연결"
keywords: "파일 시스템"
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: f33e7c58103c57e17e4e273caba1ab9b83f0cd2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-file-systems-from-logic-apps-with-the-file-system-connector"></a><span data-ttu-id="d2ff7-104">파일 시스템 커넥터를 사용하여 Logic Apps에서 온-프레미스 파일 시스템에 연결</span><span class="sxs-lookup"><span data-stu-id="d2ff7-104">Connect to on-premises file systems from logic apps with the File System connector</span></span>

<span data-ttu-id="d2ff7-105">하이브리드 클라우드 연결은 Logic Apps의 핵심이므로, 온-프레미스 리소스에서 데이터를 관리하고 안전하게 액세스하기 위해 Logic Apps에서는 온-프레미스 데이터 게이트웨이를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-105">Hybrid cloud connectivity is central to logic apps, so to manage data and securely access on-premises resources, your logic apps can use the on-premises data gateway.</span></span> <span data-ttu-id="d2ff7-106">이 문서에서는 기본적인 시나리오 “Dropbox에 업로드된 파일을 파일 공유에 복사한 다음 전자 메일 전송”를 사용하여 온-프레미스 파일 시스템에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-106">In this article, we show how to connect to an on-premises file system with a basic scenario: copy a file that's uploaded to Dropbox to a file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2ff7-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d2ff7-107">Prerequisites</span></span>

- <span data-ttu-id="d2ff7-108">최신 [온-프레미스 데이터 게이트웨이](https://www.microsoft.com/download/details.aspx?id=53127)를 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-108">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="d2ff7-109">최신 온-프레미스 데이터 게이트웨이 버전 1.15.6150.1 이상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-109">Install the latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="d2ff7-110">[온-프레미스 데이터 게이트웨이에 연결](http://aka.ms/logicapps-gateway)에서 단계를 나열하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-110">[Connect to the on-premises data gateway](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="d2ff7-111">나머지 단계를 계속하기 전에 게이트웨이를 온-프레미스 컴퓨터에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-111">The gateway must be installed on an on-premises machine before you can continue with the rest of the steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-to-your-file-system"></a><span data-ttu-id="d2ff7-112">파일 시스템에 연결하기 위한 트리거 및 작업 추가</span><span class="sxs-lookup"><span data-stu-id="d2ff7-112">Add trigger and actions for connecting to your file system</span></span>

1. <span data-ttu-id="d2ff7-113">논리 앱을 만들고 Dropbox 트리거: **파일이 만들어진 경우**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="d2ff7-114">트리거에서 **다음 단계** > **작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-114">Under the trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="d2ff7-115">파일 시스템 커넥터에 대해 지원되는 모든 작업을 볼 수 있도록 검색 상자에서 `file system`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-115">In the search box, enter `file system` so you can view all supported actions for the File System connector.</span></span>

   ![파일 커넥터 검색](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="d2ff7-117">**파일 만들기** 작업을 선택하고 파일 시스템에 대한 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-117">Choose the **Create file** action, and create a connection to your file system.</span></span>

   <span data-ttu-id="d2ff7-118">기존 연결이 없으면 새로 만들라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-118">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="d2ff7-119">**온-프레미스 데이터 게이트웨이를 통해 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="d2ff7-120">더 많은 속성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-120">More properties appear.</span></span>
   2. <span data-ttu-id="d2ff7-121">파일 시스템에 대한 루트 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="d2ff7-122">루트 폴더는 모든 파일 관련 작업의 상대 경로에 사용되는 기본 상위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-122">The root folder is the main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="d2ff7-123">온-프레미스 데이터 게이트웨이가 설치된 컴퓨터의 로컬 폴더 또는 컴퓨터에서 액세스할 수 있는 네트워크 공유 폴더를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-123">You can specify a local folder on the machine where the on-premises data gateway is installed, or the folder can be a network share that the machine can access.</span></span>

   3. <span data-ttu-id="d2ff7-124">게이트웨이에 대한 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-124">Enter the username and password for the gateway.</span></span>
   4. <span data-ttu-id="d2ff7-125">이전에 설치한 게이트웨이를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-125">Select the gateway that you previously installed.</span></span>

       ![연결 구성](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="d2ff7-127">모든 세부 정보를 제공한 후 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-127">After you provide all the details, choose **Create**.</span></span> 

   <span data-ttu-id="d2ff7-128">Logic Apps는 연결을 구성하고 테스트하여 제대로 작동되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-128">Logic Apps configures and tests your connection, making sure that the connection works properly.</span></span> 
   <span data-ttu-id="d2ff7-129">연결이 제대로 설치되면 이전에 선택한 작업에 대한 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-129">If the connection is set up correctly, you see options for the action that you previously selected.</span></span> 
   <span data-ttu-id="d2ff7-130">이제 파일 시스템 커넥터를 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-130">The file system connector is now ready for use.</span></span>

4. <span data-ttu-id="d2ff7-131">온-프레미스 파일 공유를 위해 Dropbox의 파일을 루트 폴더로 복사할 것임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-131">Specify that you want to copy files from Dropbox to the root folder for your on-premises file share.</span></span>

   ![파일 작업 만들기](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="d2ff7-133">논리 앱에서 파일을 복사한 후에는 관련 사용자만 새 파일에 대해 알 수 있도록 전자 메일을 보내는 Outlook 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-133">After your logic app copies the file, add an Outlook action that sends an email so relevant users know about the new file.</span></span> <span data-ttu-id="d2ff7-134">전자 메일의 받는 사람, 제목 및 본문을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-134">Enter the recipients, title, and body of the email.</span></span> 

   <span data-ttu-id="d2ff7-135">동적 콘텐츠 선택기에는 전자 메일에 더 많은 세부 정보를 추가할 수 있도록 파일 커넥터의 데이터 출력을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-135">In the dynamic content selector, you can choose data outputs from the file connector so you can add more details to the email.</span></span>

   ![전자 메일 보내기 작업](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="d2ff7-137">논리 앱을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-137">Save your logic app.</span></span> <span data-ttu-id="d2ff7-138">Dropbox에 파일을 업로드하여 앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-138">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="d2ff7-139">파일은 온-프레미스 파일 공유로 복사되며 해당 작업에 대한 전자 메일 알림이 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-139">The file should get copied to the on-premises file share, and you should receive an email about the operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="d2ff7-140">[Logic Apps 모니터링](../logic-apps/logic-apps-monitor-your-logic-apps.md) 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-140">Learn how to [monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="d2ff7-141">축하합니다. 이제 온-프레미스 파일 시스템에 연결할 수 있는 작업 논리 앱이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-141">Congratulations, you now have a working logic app that can connect to your on-premises file system.</span></span> <span data-ttu-id="d2ff7-142">다음과 같이 커넥터가 제공하는 다른 기능도 함께 탐색해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-142">Try exploring other functionalities that the connector offers, for example:</span></span>

- <span data-ttu-id="d2ff7-143">파일 만들기</span><span class="sxs-lookup"><span data-stu-id="d2ff7-143">Create file</span></span>
- <span data-ttu-id="d2ff7-144">폴더의 파일 나열</span><span class="sxs-lookup"><span data-stu-id="d2ff7-144">List files in folder</span></span>
- <span data-ttu-id="d2ff7-145">파일 첨부</span><span class="sxs-lookup"><span data-stu-id="d2ff7-145">Append file</span></span>
- <span data-ttu-id="d2ff7-146">파일 삭제</span><span class="sxs-lookup"><span data-stu-id="d2ff7-146">Delete file</span></span>
- <span data-ttu-id="d2ff7-147">파일 콘텐츠 가져오기</span><span class="sxs-lookup"><span data-stu-id="d2ff7-147">Get file content</span></span>
- <span data-ttu-id="d2ff7-148">경로를 사용하여 파일 콘텐츠 가져오기</span><span class="sxs-lookup"><span data-stu-id="d2ff7-148">Get file content using path</span></span>
- <span data-ttu-id="d2ff7-149">파일 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="d2ff7-149">Get file metadata</span></span>
- <span data-ttu-id="d2ff7-150">경로를 사용하여 파일 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="d2ff7-150">Get file metadata using path</span></span>
- <span data-ttu-id="d2ff7-151">루트 폴더의 파일 나열</span><span class="sxs-lookup"><span data-stu-id="d2ff7-151">List files in root folder</span></span>
- <span data-ttu-id="d2ff7-152">파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="d2ff7-152">Update file</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="d2ff7-153">swagger 보기</span><span class="sxs-lookup"><span data-stu-id="d2ff7-153">View the swagger</span></span>
<span data-ttu-id="d2ff7-154">[swagger 정보](/connectors/fileconnector/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-154">See the [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="d2ff7-155">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="d2ff7-155">Get help</span></span>

<span data-ttu-id="d2ff7-156">질문하고, 질문에 답변하고, 다른 Azure Logic Apps 사용자가 어떤 일을 하는지 알아보려면 [Azure Logic Apps 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-156">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="d2ff7-157">Azure Logic Apps 및 커넥터 개선에 도움을 주려면 [Azure Logic Apps 사용자 의견 사이트](http://aka.ms/logicapps-wish)에서 투표하고 아이디어를 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-157">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2ff7-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2ff7-158">Next steps</span></span>

- <span data-ttu-id="d2ff7-159">Logic Apps에서 [온-프레미스 데이터에 연결](../logic-apps/logic-apps-gateway-connection.md)</span><span class="sxs-lookup"><span data-stu-id="d2ff7-159">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="d2ff7-160">[엔터프라이즈 통합](../logic-apps/logic-apps-enterprise-integration-overview.md)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d2ff7-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
