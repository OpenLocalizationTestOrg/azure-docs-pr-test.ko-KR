---
title: "논리 앱에 SFTP 커넥터 사용 방법 알아보기 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. SFTP API에 연결하여 파일을 보내고 받습니다. 파일 만들기, 업데이트, 가져오기 또는 삭제와 같은 다양한 작업을 수행할 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 31253d8daee1581167a96a20ba8ad529a04b3e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sftp-connector"></a><span data-ttu-id="2e08c-105">SFTP 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="2e08c-105">Get started with the SFTP connector</span></span>
<span data-ttu-id="2e08c-106">SFTP 커넥터를 사용하여 SFTP 계정에 액세스하여 파일을 보내고 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-106">Use the SFTP connector to access an SFTP account to send and receive files.</span></span> <span data-ttu-id="2e08c-107">파일 만들기, 업데이트, 가져오기 또는 삭제와 같은 다양한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="2e08c-108">[커넥터](apis-list.md)를 사용하려면 먼저 논리 앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="2e08c-109">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sftp"></a><span data-ttu-id="2e08c-110">SFTP에 연결</span><span class="sxs-lookup"><span data-stu-id="2e08c-110">Connect to SFTP</span></span>
<span data-ttu-id="2e08c-111">논리 앱에서 서비스에 액세스하려면 먼저 서비스에 대한 *연결*을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="2e08c-112">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sftp"></a><span data-ttu-id="2e08c-113">SFTP에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="2e08c-113">Create a connection to SFTP</span></span>
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="2e08c-114">SFTP 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="2e08c-114">Use an SFTP trigger</span></span>
<span data-ttu-id="2e08c-115">트리거는 논리 앱에 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="2e08c-116">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="2e08c-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="2e08c-117">이 예제에서는 파일이 SFTP 서버에 추가되거나 수정될 때 **SFTP - 파일을 추가하거나 수정할 때** 트리거를 사용하여 논리 앱 워크플로를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-117">In this example, the **SFTP - When a file is added or modified** trigger is used to initiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="2e08c-118">새 파일 또는 수정된 파일의 콘텐츠를 확인하는 조건을 추가하고 해당 콘텐츠를 사용하기 전에 추출해야 하는 것으로 나타나는 경우 파일을 추출하도록 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-118">You also add a condition that checks the contents of the new or modified file, and makes a decision to extract the file if its contents indicate that it should be extracted before using the contents.</span></span> <span data-ttu-id="2e08c-119">마지막으로, 파일의 콘텐츠를 추출하고 추출한 콘텐츠를 SFTP 서버의 폴더에 배치하는 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-119">Finally, add an action to extract the contents of a file, and place the extracted contents in a folder on the SFTP server.</span></span> 

<span data-ttu-id="2e08c-120">엔터프라이즈 예제에서는 이 트리거를 사용하여 고객의 주문을 나타내는 새 파일에 대한 SFTP 폴더를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-120">In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="2e08c-121">그런 다음 **파일 콘텐츠 가져오기**와 같은 SFTP 커넥터 작업을 사용하여 추가 처리할 주문 및 주문 데이터베이스에 있는 저장소의 콘텐츠를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-121">You could then use an SFTP connector action, such as **Get file content**, to get the contents of the order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="2e08c-122">조건 추가</span><span class="sxs-lookup"><span data-stu-id="2e08c-122">Add a condition</span></span>
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="2e08c-123">SFTP 작업 사용</span><span class="sxs-lookup"><span data-stu-id="2e08c-123">Use an SFTP action</span></span>
<span data-ttu-id="2e08c-124">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-124">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="2e08c-125">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="2e08c-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="2e08c-126">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2e08c-126">Connector-specific details</span></span>

<span data-ttu-id="2e08c-127">[커넥터 세부 정보](/connectors/sftpconnector/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-127">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="2e08c-128">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="2e08c-128">More connectors</span></span>
<span data-ttu-id="2e08c-129">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="2e08c-129">Go back to the [APIs list](apis-list.md).</span></span>