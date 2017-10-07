---
title: "Azure 논리 앱에서 aaaGitHub 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. GitHub은 서비스를 호스팅하는 웹 기반 Git 리포지토리입니다. 모든 distributed hello 수정 버전 제어와 소스 코드 관리 (SCM) 기능 고유 기능을 추가할 뿐 아니라 Git을 제공 합니다."
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
ms.openlocfilehash: a75070e6371be625e5cf24a8dc0200844b7a6891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-github-connector"></a><span data-ttu-id="308b6-105">Hello GitHub 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="308b6-105">Get started with hello GitHub connector</span></span>
<span data-ttu-id="308b6-106">GitHub은 서비스를 호스팅하는 웹 기반 Git 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="308b6-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="308b6-107">모든 distributed hello 수정 버전 제어와 소스 코드 관리 (SCM) 기능 고유 기능을 추가할 뿐 아니라 Git을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="308b6-107">It offers all of hello distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

<span data-ttu-id="308b6-108">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="308b6-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toogithub"></a><span data-ttu-id="308b6-109">연결 tooGitHub 만들기</span><span class="sxs-lookup"><span data-stu-id="308b6-109">Create a connection tooGitHub</span></span>
<span data-ttu-id="308b6-110">GitHub 사용 하 여 toocreate 논리 앱을 먼저 만들어야 합니다는 **연결** hello 다음과 같은 속성에 대 한 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="308b6-110">toocreate Logic apps with GitHub, you must first create a **connection** then provide hello details for hello following properties:</span></span> 

| <span data-ttu-id="308b6-111">속성</span><span class="sxs-lookup"><span data-stu-id="308b6-111">Property</span></span> | <span data-ttu-id="308b6-112">필수</span><span class="sxs-lookup"><span data-stu-id="308b6-112">Required</span></span> | <span data-ttu-id="308b6-113">설명</span><span class="sxs-lookup"><span data-stu-id="308b6-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="308b6-114">신뢰</span><span class="sxs-lookup"><span data-stu-id="308b6-114">Token</span></span> |<span data-ttu-id="308b6-115">예</span><span class="sxs-lookup"><span data-stu-id="308b6-115">Yes</span></span> |<span data-ttu-id="308b6-116">GitHub 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="308b6-116">Provide GitHub Credentials</span></span> |

<span data-ttu-id="308b6-117">Hello 연결을 만든 후 tooexecute hello 동작을 사용 하 고이 문서에서 설명 하는 hello 트리거 수신 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="308b6-117">After you create hello connection, you can use it tooexecute hello actions and listen for hello triggers described in this article.</span></span> 

> [!INCLUDE [Steps toocreate a connection tooGitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="308b6-118">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="308b6-118">Connector-specific details</span></span>

<span data-ttu-id="308b6-119">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/github/)합니다.</span><span class="sxs-lookup"><span data-stu-id="308b6-119">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/github/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="308b6-120">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="308b6-120">More connectors</span></span>
<span data-ttu-id="308b6-121">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="308b6-121">Go back toohello [APIs list](apis-list.md).</span></span>
