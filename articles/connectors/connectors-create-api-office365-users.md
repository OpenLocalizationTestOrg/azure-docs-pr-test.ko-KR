---
title: "논리 앱에 Office 365 사용자 커넥터 추가 | Microsoft Docs"
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
ms.openlocfilehash: 330f733440932a769eb0fe6031cd0d947a820080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-users-connector"></a><span data-ttu-id="27d22-103">Office 365 사용자 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="27d22-103">Get started with the Office 365 Users connector</span></span>
<span data-ttu-id="27d22-104">Office 365 사용자에 연결하여 프로필 가져오기, 사용자 검색 등을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="27d22-104">Connect to Office 365 Users to get profiles, search users, and more.</span></span> <span data-ttu-id="27d22-105">Office 365 사용자를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d22-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="27d22-106">Office 365 사용자에서 가져온 데이터를 기반으로 비즈니스 흐름을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="27d22-106">Build your business flow based on the data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="27d22-107">부하 직원 가져오기, 관리자의 사용자 프로필 가져오기 등의 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27d22-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="27d22-108">이러한 작업을 사용하여 응답을 가져오고 출력을 다른 작업에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="27d22-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="27d22-109">예를 들어 사용자의 부하 직원을 가져온 다음 이 정보를 사용하여 SQL Azure 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="27d22-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="27d22-110">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27d22-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office-365-users"></a><span data-ttu-id="27d22-111">Office 365 사용자에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="27d22-111">Create a connection to Office 365 Users</span></span>
<span data-ttu-id="27d22-112">논리 앱에 이 커넥터를 추가할 때 Office 365 사용자 계정에 로그인하고 논리 앱을 계정에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27d22-112">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="27d22-113">연결을 만든 후 사용자 ID 등의 Office 365 사용자 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27d22-113">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span></span> <span data-ttu-id="27d22-114">이 항목의 **REST API 참조** 에서는 이러한 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="27d22-114">The **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="27d22-115">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="27d22-115">Connector-specific details</span></span>

<span data-ttu-id="27d22-116">[커넥터 세부 정보](/connectors/officeusers/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d22-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="27d22-117">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="27d22-117">More connectors</span></span>
<span data-ttu-id="27d22-118">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="27d22-118">Go back to the [APIs list](apis-list.md).</span></span>