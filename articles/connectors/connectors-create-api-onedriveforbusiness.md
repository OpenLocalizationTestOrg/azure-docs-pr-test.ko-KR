---
title: "비즈니스용 OneDrive | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. 비즈니스용 OneDrive에 연결하여 파일을 관리합니다. 파일에 대해 업로드, 업데이트, 가져오기 및 삭제와 같은 다양한 작업을 수행할 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cf9484e9-7a20-4de0-93c8-0fa132221f2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 783d6a640d9626508bcabc5f991dc5b6fc22eaf4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-for-business-connector"></a><span data-ttu-id="fe01f-105">비즈니스용 OneDrive 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="fe01f-105">Get started with the OneDrive for Business connector</span></span>
<span data-ttu-id="fe01f-106">비즈니스용 OneDrive에 연결하여 파일을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="fe01f-106">Connect to OneDrive for Business to manage your files.</span></span> <span data-ttu-id="fe01f-107">파일에 대해 업로드, 업데이트, 가져오기 및 삭제와 같은 다양한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe01f-107">You can perform various actions such as upload, update, get, and delete on files.</span></span>

<span data-ttu-id="fe01f-108">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe01f-108">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-onedrive-for-business"></a><span data-ttu-id="fe01f-109">비즈니스용 OneDrive에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="fe01f-109">Create a connection to OneDrive for Business</span></span>
<span data-ttu-id="fe01f-110">비즈니스용 OneDrive로 논리 앱을 만들려면 먼저 **연결**을 만든 후에 다음 속성에 대한 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe01f-110">To create Logic apps with OneDrive for Business, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="fe01f-111">속성</span><span class="sxs-lookup"><span data-stu-id="fe01f-111">Property</span></span> | <span data-ttu-id="fe01f-112">필수</span><span class="sxs-lookup"><span data-stu-id="fe01f-112">Required</span></span> | <span data-ttu-id="fe01f-113">설명</span><span class="sxs-lookup"><span data-stu-id="fe01f-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fe01f-114">신뢰</span><span class="sxs-lookup"><span data-stu-id="fe01f-114">Token</span></span> |<span data-ttu-id="fe01f-115">예</span><span class="sxs-lookup"><span data-stu-id="fe01f-115">Yes</span></span> |<span data-ttu-id="fe01f-116">비즈니스용 OneDrive 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="fe01f-116">Provide OneDrive for Business Credentials</span></span> |

<span data-ttu-id="fe01f-117">연결을 만든 후에 사용하여 작업을 실행하고 이 문서에 설명된 트리거에 대한 수신을 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe01f-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to OneDrive for Business](../../includes/connectors-create-api-onedriveforbusiness.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="fe01f-118">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="fe01f-118">Connector-specific details</span></span>

<span data-ttu-id="fe01f-119">[커넥터 세부 정보](/connectors/onedriveforbusinessconnector/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe01f-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveforbusinessconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="fe01f-120">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="fe01f-120">More connectors</span></span>
<span data-ttu-id="fe01f-121">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="fe01f-121">Go back to the [APIs list](apis-list.md).</span></span>