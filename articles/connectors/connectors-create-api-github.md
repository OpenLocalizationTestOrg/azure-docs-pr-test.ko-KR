---
title: "Azure Logic Apps의 GitHub 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. GitHub은 서비스를 호스팅하는 웹 기반 Git 리포지토리입니다. 고유한 기능을 추가할 뿐 아니라 Git의 분산된 수정 버전 제어 및 SCM(소스 코드 관리) 기능을 모두 제공합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: d4614b0ceff0ec0d36dbb1a136551f985f2fc1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-github-connector"></a><span data-ttu-id="6c616-105">GitHub 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="6c616-105">Get started with the GitHub connector</span></span>
<span data-ttu-id="6c616-106">GitHub은 서비스를 호스팅하는 웹 기반 Git 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="6c616-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="6c616-107">고유한 기능을 추가할 뿐 아니라 Git의 분산된 수정 버전 제어 및 SCM(소스 코드 관리) 기능을 모두 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c616-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

<span data-ttu-id="6c616-108">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c616-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-github"></a><span data-ttu-id="6c616-109">GitHub에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="6c616-109">Create a connection to GitHub</span></span>
<span data-ttu-id="6c616-110">GitHub로 논리 앱을 만들려면 먼저 **연결**을 만든 후에 다음 속성에 대한 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c616-110">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="6c616-111">속성</span><span class="sxs-lookup"><span data-stu-id="6c616-111">Property</span></span> | <span data-ttu-id="6c616-112">필수</span><span class="sxs-lookup"><span data-stu-id="6c616-112">Required</span></span> | <span data-ttu-id="6c616-113">설명</span><span class="sxs-lookup"><span data-stu-id="6c616-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c616-114">신뢰</span><span class="sxs-lookup"><span data-stu-id="6c616-114">Token</span></span> |<span data-ttu-id="6c616-115">예</span><span class="sxs-lookup"><span data-stu-id="6c616-115">Yes</span></span> |<span data-ttu-id="6c616-116">GitHub 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="6c616-116">Provide GitHub Credentials</span></span> |

<span data-ttu-id="6c616-117">연결을 만든 후에 사용하여 작업을 실행하고 이 문서에 설명된 트리거에 대한 수신을 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c616-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span> 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="6c616-118">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="6c616-118">Connector-specific details</span></span>

<span data-ttu-id="6c616-119">[커넥터 세부 정보](/connectors/github/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c616-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/github/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="6c616-120">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="6c616-120">More connectors</span></span>
<span data-ttu-id="6c616-121">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="6c616-121">Go back to the [APIs list](apis-list.md).</span></span>