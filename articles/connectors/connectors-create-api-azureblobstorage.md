---
title: "Logic Apps에 Azure Blob Storage 커넥터 추가 | Microsoft Docs"
description: "시작하여 논리 앱에서 Azure Blob Storage 커넥터 구성"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: bc7908868828bd1628633cf9e57f8c44f8000827
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="945a5-103">논리 앱에서 Azure Blob Storage 커넥터 사용</span><span class="sxs-lookup"><span data-stu-id="945a5-103">Use the Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="945a5-104">Azure Blob Storage 커넥터를 사용하여 논리 앱 내의 저장소 계정에서 blob을 업로드, 업데이트, 가져오기 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-104">Use the Azure Blob storage connector to upload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="945a5-105">Azure Blob 저장소를 사용하여 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="945a5-106">새 프로젝트를 업로드하거나 최근에 업데이트한 파일을 가져와 워크플로를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="945a5-107">파일 메타데이터 가져오기, 파일 삭제, 파일 복사 및 삭제를 위한 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-107">Use actions to get file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="945a5-108">예를 들어 도구가 Azure 웹 사이트에서 업데이트되면(트리거) Blob 저장소에서 파일을 업데이트합니다(작업).</span><span class="sxs-lookup"><span data-stu-id="945a5-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="945a5-109">이 항목에서는 논리 앱에서 Blob 저장소 커넥터를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-109">This topic shows you how to use the blob storage connector in a logic app.</span></span>

<span data-ttu-id="945a5-110">Logic Apps에 대해 자세히 알아보려면 [논리 앱이란 무엇인가요?](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945a5-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="945a5-111">Logic Apps에 대해 자세히 알아보려면 [논리 앱이란 무엇인가요?](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945a5-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-blob-storage"></a><span data-ttu-id="945a5-112">Azure Blob 저장소에 연결</span><span class="sxs-lookup"><span data-stu-id="945a5-112">Connect to Azure blob storage</span></span>
<span data-ttu-id="945a5-113">논리 앱에서 서비스에 액세스하려면 먼저 서비스에 대한 *연결*을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="945a5-114">연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="945a5-115">예를 들어 저장소 계정에 연결하려면 먼저 Blob 저장소 *연결*을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-115">For example, to connect to a storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="945a5-116">연결을 만들려면 연결하려는 서비스에 액세스할 때 일반적으로 사용하는 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-116">To create a connection, enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="945a5-117">따라서 Azure 저장소를 사용하는 경우 저장소 계정에 대한 자격 증명을 입력하여 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-117">So with Azure storage, enter the credentials to your storage account to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="945a5-118">연결 만들기</span><span class="sxs-lookup"><span data-stu-id="945a5-118">Create the connection</span></span>
> [!INCLUDE [Create a connection to Azure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="945a5-119">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="945a5-119">Use a trigger</span></span>
<span data-ttu-id="945a5-120">이 연결에는 트리거가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-120">This connector does not have any triggers.</span></span> <span data-ttu-id="945a5-121">다른 트리거(되풀이 트리거, HTTP 웹후크 트리거, 다른 커넥터와 함께 사용할 수 있는 트리거 포함)를 사용하여 논리 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-121">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="945a5-122">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)에서 예제를 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="945a5-123">작업 사용</span><span class="sxs-lookup"><span data-stu-id="945a5-123">Use an action</span></span>
<span data-ttu-id="945a5-124">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-124">An action is an operation carried out by the workflow defined in a logic app.</span></span>

1. <span data-ttu-id="945a5-125">더하기 기호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-125">Select the plus sign.</span></span> <span data-ttu-id="945a5-126">**작업 추가**, **조건 추가** 또는 **자세히** 옵션 중 하나 등 몇 가지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="945a5-127">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="945a5-128">사용 가능한 모든 작업의 목록을 표시하려면 텍스트 상자에 "blob"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-128">In the text box, type “blob” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="945a5-129">이 예제에서는 **AzureBlob - 경로를 사용하여 파일 메타데이터 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="945a5-130">연결이 이미 있는 경우 **...** (선택기 표시) 단추를 선택하여 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-130">If a connection already exists, then select the **...** (Show Picker) button to select a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="945a5-131">연결 정보를 묻는 메시지가 표시되면 연결을 만들기 위한 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="945a5-132">이 항목의 [연결 만들기](connectors-create-api-azureblobstorage.md#create-the-connection)에서는 이러한 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-132">[Create the connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="945a5-133">이 예제에서는 파일의 메타 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-133">In this example, we get the metadata of a file.</span></span> <span data-ttu-id="945a5-134">메타데이터를 보려면 다른 커넥터를 사용하여 새 파일을 만드는 다른 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-134">To see the metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="945a5-135">예를 들어 메타데이터에 따라 새 "test" 파일을 만드는 OneDrive 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-135">For example, add a OneDrive action that creates a new "test" file based on the metadata.</span></span> 


5. <span data-ttu-id="945a5-136">변경 내용을 **저장**합니다(도구 모음 왼쪽 위 모서리).</span><span class="sxs-lookup"><span data-stu-id="945a5-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="945a5-137">논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="945a5-138">[저장소 탐색기](http://storageexplorer.com/)는 여러 저장소 계정을 관리하는 유용한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-138">[Storage Explorer](http://storageexplorer.com/) is a great tool to  manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="945a5-139">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="945a5-139">Connector-specific details</span></span>

<span data-ttu-id="945a5-140">[커넥터 세부 정보](/connectors/azureblobconnector/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945a5-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="945a5-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="945a5-141">Next steps</span></span>
<span data-ttu-id="945a5-142">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="945a5-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="945a5-143">[API 목록](apis-list.md)에서 Logic Apps의 사용 가능한 다른 커넥터를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="945a5-143">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

