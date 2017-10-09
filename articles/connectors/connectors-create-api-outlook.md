---
title: "Azure 논리 앱에서 aaaOutlook.com 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. Outlook.com 커넥터 toomanage을 사용 하면 메일, 일정 및 연락처입니다. 메일 보내기, 모임 예약, 연락처 추가 등 다양한 작업을 수행할 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 87113c85-d158-4dd5-9ed5-5748130003d6
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1df299b7a01390ebc6931707f3788c10fcacfae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-outlookcom-connector"></a><span data-ttu-id="83f60-105">Hello Outlook.com 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="83f60-105">Get started with hello Outlook.com connector</span></span>
<span data-ttu-id="83f60-106">Outlook.com 커넥터 toomanage을 사용 하면 메일, 일정 및 연락처입니다.</span><span class="sxs-lookup"><span data-stu-id="83f60-106">Outlook.com connector allows you toomanage your mail, calendars, and contacts.</span></span> <span data-ttu-id="83f60-107">메일 보내기, 모임 예약, 연락처 추가 등 다양한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f60-107">You can perform various actions such as send mail, schedule meetings, add contacts, etc.</span></span>

<span data-ttu-id="83f60-108">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83f60-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toooutlookcom"></a><span data-ttu-id="83f60-109">연결 tooOutlook.com 만들기</span><span class="sxs-lookup"><span data-stu-id="83f60-109">Create a connection tooOutlook.com</span></span>
<span data-ttu-id="83f60-110">Outlook.com 사용 하 여 toocreate 논리 앱을 먼저 만들어야 합니다는 **연결** hello 다음과 같은 속성에 대 한 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="83f60-110">toocreate Logic apps with Outlook.com, you must first create a **connection** then provide hello details for hello following properties:</span></span>

| <span data-ttu-id="83f60-111">속성</span><span class="sxs-lookup"><span data-stu-id="83f60-111">Property</span></span> | <span data-ttu-id="83f60-112">필수</span><span class="sxs-lookup"><span data-stu-id="83f60-112">Required</span></span> | <span data-ttu-id="83f60-113">설명</span><span class="sxs-lookup"><span data-stu-id="83f60-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83f60-114">신뢰</span><span class="sxs-lookup"><span data-stu-id="83f60-114">Token</span></span> |<span data-ttu-id="83f60-115">예</span><span class="sxs-lookup"><span data-stu-id="83f60-115">Yes</span></span> |<span data-ttu-id="83f60-116">Outlook.com 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="83f60-116">Provide Outlook.com Credentials</span></span> |

<span data-ttu-id="83f60-117">Hello 연결을 만든 후 tooexecute hello 동작을 사용 하 고이 문서에서 설명 하는 hello 트리거 수신 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83f60-117">After you create hello connection, you can use it tooexecute hello actions and listen for hello triggers described in this article.</span></span>

> [!INCLUDE [Steps toocreate a connection tooOutlook.com](../../includes/connectors-create-api-outlook.md)]
>

## <a name="connector-specific-details"></a><span data-ttu-id="83f60-118">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="83f60-118">Connector-specific details</span></span>

<span data-ttu-id="83f60-119">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/outlook/)합니다.</span><span class="sxs-lookup"><span data-stu-id="83f60-119">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/outlook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="83f60-120">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="83f60-120">More connectors</span></span>
<span data-ttu-id="83f60-121">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="83f60-121">Go back toohello [APIs list](apis-list.md).</span></span>
