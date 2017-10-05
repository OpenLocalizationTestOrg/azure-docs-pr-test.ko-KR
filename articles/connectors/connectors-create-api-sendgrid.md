---
title: SendGrid | Microsoft Docs
description: "Azure 앱 서비스로 논리 앱을 만듭니다. SendGrid 연결 공급자를 통해 전자 메일을 보내고 받는 사람 목록을 관리할 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: bc4f1fc2-824c-4ed7-8de8-e82baff3b746
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 9ff0591741899d65b8274fb14ab3f3c8db9abe36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sendgrid-connector"></a><span data-ttu-id="84702-104">SendGrid 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="84702-104">Get started with the SendGrid connector</span></span>
<span data-ttu-id="84702-105">SendGrid 연결 공급자를 통해 전자 메일을 보내고 받는 사람 목록을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84702-105">SendGrid Connection Provider lets you send email and manage recipient lists.</span></span>

<span data-ttu-id="84702-106">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84702-106">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sendgrid"></a><span data-ttu-id="84702-107">SendGrid에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="84702-107">Create a connection to SendGrid</span></span>
<span data-ttu-id="84702-108">SendGrid로 논리 앱을 만들려면 먼저 **연결**을 만든 후에 다음 속성에 대한 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84702-108">To create Logic apps with SendGrid, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="84702-109">속성</span><span class="sxs-lookup"><span data-stu-id="84702-109">Property</span></span> | <span data-ttu-id="84702-110">필수</span><span class="sxs-lookup"><span data-stu-id="84702-110">Required</span></span> | <span data-ttu-id="84702-111">설명</span><span class="sxs-lookup"><span data-stu-id="84702-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84702-112">ApiKey</span><span class="sxs-lookup"><span data-stu-id="84702-112">ApiKey</span></span> |<span data-ttu-id="84702-113">예</span><span class="sxs-lookup"><span data-stu-id="84702-113">Yes</span></span> |<span data-ttu-id="84702-114">SendGrid API 키 제공</span><span class="sxs-lookup"><span data-stu-id="84702-114">Provide Your SendGrid Api Key</span></span> |

> [!INCLUDE [Steps to create a connection to SendGrid](../../includes/connectors-create-api-sendgrid.md)]
> 


<span data-ttu-id="84702-115">연결을 만든 후에 사용하여 작업을 실행하고 트리거에 대한 수신을 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84702-115">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="84702-116">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="84702-116">Connector-specific details</span></span>

<span data-ttu-id="84702-117">[커넥터 세부 정보](/connectors/sendgrid/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84702-117">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sendgrid/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="84702-118">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="84702-118">More connectors</span></span>
<span data-ttu-id="84702-119">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="84702-119">Go back to the [APIs list](apis-list.md).</span></span>