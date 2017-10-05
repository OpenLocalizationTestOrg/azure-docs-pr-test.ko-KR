---
title: "논리 앱에서 Office 365 비디오 커넥터 사용 | Microsoft Docs"
description: "Microsoft Azure 앱 서비스 논리 앱에서 Office 365 비디오 커넥터 사용을 시작"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 738e5aa7-2523-4116-8b65-211b9063852d
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: f0e3613d4a3fd5478787c0365eb7a0bcde886c81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office365-video-connector"></a><span data-ttu-id="009e0-103">Office 365 비디오 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="009e0-103">Get started with the Office365 Video connector</span></span>
<span data-ttu-id="009e0-104">Office 365 비디오에 연결하여 Office 365 비디오에 대한 정보 가져오기, 비디오 목록 가져오기 등을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="009e0-104">Connect to Office 365 Video to get information about an Office 365 video, get a list of videos, and more.</span></span> <span data-ttu-id="009e0-105">Office 365 비디오로 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="009e0-105">With Office 365 Video, you can:</span></span>

* <span data-ttu-id="009e0-106">Office 365 비디오에서 가져온 데이터를 기반으로 비즈니스 흐름을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="009e0-106">Build your business flow based on the data you get from Office 365 Video.</span></span> 
* <span data-ttu-id="009e0-107">비디오 포털 상태 확인, 채널의 모든 비디오 목록 가져오기 등의 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="009e0-107">Use actions that check the video portal status, get a list of all video in a channel, and more.</span></span> <span data-ttu-id="009e0-108">이러한 작업을 사용하여 응답을 가져오고 출력을 다른 작업에 사용할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="009e0-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="009e0-109">예를 들어 Bing 검색 커넥터를 사용하여 Office 365 비디오를 검색한 다음, Office 365 비디오 커넥터를 사용하여 해당 비디오에 대한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="009e0-109">For example, you can use the Bing Search connector to search for Office 365 videos, and then use the Office 365 video connector to get information about that video.</span></span> <span data-ttu-id="009e0-110">비디오가 요구 사항을 충족하면 Facebook에 이 비디오를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="009e0-110">If the video meets your requirements, you can post this video on Facebook.</span></span> 

<span data-ttu-id="009e0-111">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="009e0-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office365-video-connector"></a><span data-ttu-id="009e0-112">Office 365 비디오 커넥터에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="009e0-112">Create a connection to Office365 Video connector</span></span>
<span data-ttu-id="009e0-113">논리 앱에 이 커넥터를 추가할 때 Office 365 비디오 계정에 로그인하고 논리 앱을 계정에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="009e0-113">When you add this connector to your logic apps, you must sign-in to your Office 365 Video account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Video](../../includes/connectors-create-api-office365video.md)]
> 
> 

<span data-ttu-id="009e0-114">연결을 만든 후 테넌트 이름 또는 채널 ID 등의 Office 365 비디오 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="009e0-114">After you create the connection, you enter the Office 365 video properties, like the tenant name or channel ID.</span></span> 


## <a name="connector-specific-details"></a><span data-ttu-id="009e0-115">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="009e0-115">Connector-specific details</span></span>

<span data-ttu-id="009e0-116">[커넥터 세부 정보](/connectors/office365videoconnector/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="009e0-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365videoconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="009e0-117">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="009e0-117">More connectors</span></span>
<span data-ttu-id="009e0-118">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="009e0-118">Go back to the [APIs list](apis-list.md).</span></span>