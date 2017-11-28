---
title: "논리 앱에서 aaaAdd hello Office 365 사용자 커넥터 | Microsoft Docs"
description: "REST API 매개 변수를 사용하는 Office 365 사용자 커넥터 개요"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 2fae1c80d195a368b5f6c1ad650905a0d6e94c83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-users-connector"></a><span data-ttu-id="11fef-103">Hello Office 365 사용자 커넥터와 함께 시작.</span><span class="sxs-lookup"><span data-stu-id="11fef-103">Get started with hello Office 365 Users connector</span></span>
<span data-ttu-id="11fef-104">TooOffice 365 사용자 tooget 프로필, 검색 사용자 등을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="11fef-104">Connect tooOffice 365 Users tooget profiles, search users, and more.</span></span> <span data-ttu-id="11fef-105">Office 365 사용자를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11fef-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="11fef-106">Office 365 사용자에서 받아야 하는 hello 데이터를 기반으로 비즈니스 흐름을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="11fef-106">Build your business flow based on hello data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="11fef-107">부하 직원 가져오기, 관리자의 사용자 프로필 가져오기 등의 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="11fef-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="11fef-108">이러한 작업 응답을 가져오고 다른 작업에 사용할 수 있는 hello 출력을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="11fef-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="11fef-109">예를 들어 사용자의 부하 직원을 가져온 다음 이 정보를 사용하여 SQL Azure 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="11fef-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="11fef-110">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11fef-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toooffice-365-users"></a><span data-ttu-id="11fef-111">연결 tooOffice 365 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11fef-111">Create a connection tooOffice 365 Users</span></span>
<span data-ttu-id="11fef-112">이 커넥터 tooyour 논리 앱을 추가 하면 해야 로그인 할 tooyour Office 365 사용자 계정 및 tooconnect tooyour 계정 논리 앱을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11fef-112">When you add this connector tooyour logic apps, you must sign-in tooyour Office 365 Users account and allow logic apps tooconnect tooyour account.</span></span>

> [!INCLUDE [Steps toocreate a connection tooOffice 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="11fef-113">Hello Office 365 사용자 속성, 사용자 id입니다. hello와 같은 입력 hello 연결을 만든 후</span><span class="sxs-lookup"><span data-stu-id="11fef-113">After you create hello connection, you enter hello Office 365 Users properties, like hello user ID.</span></span> <span data-ttu-id="11fef-114">hello **REST API 참조** 이 항목에서 이러한 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="11fef-114">hello **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="11fef-115">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="11fef-115">Connector-specific details</span></span>

<span data-ttu-id="11fef-116">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/officeusers/)합니다.</span><span class="sxs-lookup"><span data-stu-id="11fef-116">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="11fef-117">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="11fef-117">More connectors</span></span>
<span data-ttu-id="11fef-118">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="11fef-118">Go back toohello [APIs list](apis-list.md).</span></span>
