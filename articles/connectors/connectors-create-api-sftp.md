---
title: "aaaLearn 어떻게 toouse hello 논리 앱에서 SFTP 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. API tooSFTP toosend를 연결 하 고 파일을 받습니다. 파일 만들기, 업데이트, 가져오기 또는 삭제와 같은 다양한 작업을 수행할 수 있습니다."
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
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a><span data-ttu-id="552d4-105">Hello SFTP 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="552d4-105">Get started with hello SFTP connector</span></span>
<span data-ttu-id="552d4-106">사용 하 여 hello SFTP 커넥터 tooaccess SFTP toosend 계정 및 파일을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-106">Use hello SFTP connector tooaccess an SFTP account toosend and receive files.</span></span> <span data-ttu-id="552d4-107">파일 만들기, 업데이트, 가져오기 또는 삭제와 같은 다양한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="552d4-108">toouse [커넥터](apis-list.md), toocreate 논리 앱을 먼저 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="552d4-109">[지금 논리 앱을 만들어](../logic-apps/logic-apps-create-a-logic-app.md) 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosftp"></a><span data-ttu-id="552d4-110">TooSFTP 연결</span><span class="sxs-lookup"><span data-stu-id="552d4-110">Connect tooSFTP</span></span>
<span data-ttu-id="552d4-111">Toocreate 먼저 논리 앱에서 모든 서비스에 액세스 하기 전에 *연결* toohello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="552d4-112">[연결](connectors-overview.md)은 논리 앱과 다른 서비스 간의 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosftp"></a><span data-ttu-id="552d4-113">연결 tooSFTP 만들기</span><span class="sxs-lookup"><span data-stu-id="552d4-113">Create a connection tooSFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="552d4-114">SFTP 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="552d4-114">Use an SFTP trigger</span></span>
<span data-ttu-id="552d4-115">트리거는 이벤트를 사용 하는 toostart hello 워크플로 논리 앱에 정의 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="552d4-116">[트리거에 대해 자세히 알아보세요.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="552d4-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="552d4-117">이 예제에서는 hello **SFTP-파일 추가 또는 수정 되 면** 파일은 추가, 또는 SFTP 서버에서 수정 될 때 트리거를 사용 하는 tooinitiate 논리 앱 워크플로 합니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-117">In this example, hello **SFTP - When a file is added or modified** trigger is used tooinitiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="552d4-118">또한 hello 새롭거나 수정 된 파일의 hello 내용을 확인 하 고 내용이 hello 내용을 사용 하기 전에 추출할 수를 나타내는 경우 의사 결정 tooextract hello 파일 하 게 하는 조건을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-118">You also add a condition that checks hello contents of hello new or modified file, and makes a decision tooextract hello file if its contents indicate that it should be extracted before using hello contents.</span></span> <span data-ttu-id="552d4-119">마지막으로 파일의 동작 tooextract hello 내용을 추가 하 고 hello SFTP 서버의 폴더에 추출 하는 hello 내용을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-119">Finally, add an action tooextract hello contents of a file, and place hello extracted contents in a folder on hello SFTP server.</span></span> 

<span data-ttu-id="552d4-120">엔터프라이즈 예를 들어 고객 주문을 나타내는 새 파일에 대 한이 트리거 toomonitor SFTP 폴더를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-120">In an enterprise example, you could use this trigger toomonitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="552d4-121">사용할 수 있습니다 다음 SFTP 커넥터 동작의 경우와 같은 **파일 콘텐츠를 가져옵니다.**, 추가 처리 및 orders 데이터베이스의 저장소에 대 한 hello 주문의 tooget hello 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-121">You could then use an SFTP connector action, such as **Get file content**, tooget hello contents of hello order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="552d4-122">조건 추가</span><span class="sxs-lookup"><span data-stu-id="552d4-122">Add a condition</span></span>
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="552d4-123">SFTP 작업 사용</span><span class="sxs-lookup"><span data-stu-id="552d4-123">Use an SFTP action</span></span>
<span data-ttu-id="552d4-124">동작은 논리 앱에 정의 된 hello 워크플로에 의해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="552d4-125">[작업에 대해 자세히 알아봅니다.](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)</span><span class="sxs-lookup"><span data-stu-id="552d4-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="552d4-126">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="552d4-126">Connector-specific details</span></span>

<span data-ttu-id="552d4-127">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/sftpconnector/)합니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-127">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="552d4-128">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="552d4-128">More connectors</span></span>
<span data-ttu-id="552d4-129">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="552d4-129">Go back toohello [APIs list](apis-list.md).</span></span>
