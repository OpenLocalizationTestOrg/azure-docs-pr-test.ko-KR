---
title: "aaaAdd hello Azure blob 저장소에서 논리 앱 커넥터 | Microsoft Docs"
description: "시작 하 고 논리 앱의 hello Azure blob 저장소 커넥터를 구성 합니다."
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
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="2cc1d-103">논리 앱에서 hello Azure blob 저장소 커넥터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-103">Use hello Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="2cc1d-104">메뉴 및 도구 모음을 사용 하 여 hello Azure Blob 저장소 커넥터 tooupload 업데이트 get, 논리 앱 내에서 모든 저장소 계정의 blob을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-104">Use hello Azure Blob storage connector tooupload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="2cc1d-105">Azure Blob 저장소를 사용하여 다음과 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="2cc1d-106">새 프로젝트를 업로드하거나 최근에 업데이트한 파일을 가져와 워크플로를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="2cc1d-107">동작 tooget 파일 메타 데이터를 사용 하 여, 파일, 파일 복사 및 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-107">Use actions tooget file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="2cc1d-108">예를 들어 도구가 Azure 웹 사이트에서 업데이트되면(트리거) Blob 저장소에서 파일을 업데이트합니다(작업).</span><span class="sxs-lookup"><span data-stu-id="2cc1d-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="2cc1d-109">이 항목 toouse hello 논리 앱의 저장소 커넥터 blob 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-109">This topic shows you how toouse hello blob storage connector in a logic app.</span></span>

<span data-ttu-id="2cc1d-110">논리 앱에 대해 자세히 toolearn 참조 [논리 앱 이란](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="2cc1d-111">논리 앱에 대해 자세히 toolearn 참조 [논리 앱 이란](../logic-apps/logic-apps-what-are-logic-apps.md) 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-blob-storage"></a><span data-ttu-id="2cc1d-112">TooAzure blob 저장소에 연결</span><span class="sxs-lookup"><span data-stu-id="2cc1d-112">Connect tooAzure blob storage</span></span>
<span data-ttu-id="2cc1d-113">논리 앱에서 모든 서비스에 액세스 하기 전에 먼저 만들어야는 *연결* toohello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="2cc1d-114">연결은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="2cc1d-115">예를 들어 tooconnect tooa 저장소 계정을 처음 만들 blob 저장소 *연결*합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-115">For example, tooconnect tooa storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="2cc1d-116">toocreate 연결을 tooaccess hello 서비스에 연결 하는 일반적으로 사용 하는 hello 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="2cc1d-117">따라서 Azure 저장소와 hello tooyour 저장소 계정 toocreate hello 연결 시 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-117">So with Azure storage, enter hello credentials tooyour storage account toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="2cc1d-118">Hello 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="2cc1d-118">Create hello connection</span></span>
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="2cc1d-119">트리거 사용</span><span class="sxs-lookup"><span data-stu-id="2cc1d-119">Use a trigger</span></span>
<span data-ttu-id="2cc1d-120">이 연결에는 트리거가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-120">This connector does not have any triggers.</span></span> <span data-ttu-id="2cc1d-121">다른 트리거 toostart hello 논리 앱과 되풀이 트리거, HTTP Webhook 트리거는 트리거를 사용 하 여 다른 커넥터를 사용할 수 있는 등을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-121">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="2cc1d-122">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)에서 예제를 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="2cc1d-123">작업 사용</span><span class="sxs-lookup"><span data-stu-id="2cc1d-123">Use an action</span></span>
<span data-ttu-id="2cc1d-124">동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span>

1. <span data-ttu-id="2cc1d-125">Hello 더하기 기호를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-125">Select hello plus sign.</span></span> <span data-ttu-id="2cc1d-126">여러 선택 항목을 참조 하십시오: **동작 추가**, **조건을 추가**, hello 중 하나 또는 **자세한** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="2cc1d-127">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="2cc1d-128">Hello 텍스트 상자에 "blob" tooget hello 사용 가능한 모든 작업 목록을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-128">In hello text box, type “blob” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="2cc1d-129">이 예제에서는 **AzureBlob - 경로를 사용하여 파일 메타데이터 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="2cc1d-130">연결이 이미 존재 하는 경우 다음 hello 선택 **...** (선택 표시) 단추 tooselect 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-130">If a connection already exists, then select hello **...** (Show Picker) button tooselect a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="2cc1d-131">Hello 연결 정보에 대 한 메시지가 표시 되 면 hello, toocreate hello 연결 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="2cc1d-132">[Hello 연결을 만들](connectors-create-api-azureblobstorage.md#create-the-connection) 이 항목에서 이러한 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-132">[Create hello connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2cc1d-133">이 예제에서는 hello 메타 데이터를 파일의 구했습니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-133">In this example, we get hello metadata of a file.</span></span> <span data-ttu-id="2cc1d-134">toosee hello 메타 데이터, 다른 커넥터를 사용 하 여 새 파일을 만드는 다른 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-134">toosee hello metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="2cc1d-135">예를 들어 hello 메타 데이터에 따라 새로운 "test" 파일을 만드는 OneDrive 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-135">For example, add a OneDrive action that creates a new "test" file based on hello metadata.</span></span> 


5. <span data-ttu-id="2cc1d-136">**저장** 변경 내용을 (hello 도구 모음의 왼쪽된 상단 모서리).</span><span class="sxs-lookup"><span data-stu-id="2cc1d-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="2cc1d-137">논리 앱이 저장되며 이 논리 앱이 사용 상태로 자동 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="2cc1d-138">[저장소 탐색기](http://storageexplorer.com/) 좋은 도구에는 너무 여러 저장소 계정을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-138">[Storage Explorer](http://storageexplorer.com/) is a great tool too manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="2cc1d-139">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2cc1d-139">Connector-specific details</span></span>

<span data-ttu-id="2cc1d-140">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/azureblobconnector/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2cc1d-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2cc1d-141">Next steps</span></span>
<span data-ttu-id="2cc1d-142">[논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="2cc1d-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="2cc1d-143">탐색에서 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2cc1d-143">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

