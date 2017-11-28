---
title: "논리 앱에서 aaaUse hello Office 365 비디오 커넥터 | Microsoft Docs"
description: "Hello Office 365 비디오 커넥터를 사용 하 여 Microsoft Azure 앱 서비스 논리 앱에서 시작"
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
ms.openlocfilehash: 6e0a4b658d166d1cf8096d50f4bf2d502053aa43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office365-video-connector"></a><span data-ttu-id="ef6d1-103">Hello Office365 비디오 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="ef6d1-103">Get started with hello Office365 Video connector</span></span>
<span data-ttu-id="ef6d1-104">TooOffice 365 비디오 tooget 정보 Office 365 비디오에 대 한 연결, 비디오, 등의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-104">Connect tooOffice 365 Video tooget information about an Office 365 video, get a list of videos, and more.</span></span> <span data-ttu-id="ef6d1-105">Office 365 비디오로 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-105">With Office 365 Video, you can:</span></span>

* <span data-ttu-id="ef6d1-106">Office 365 비디오에서 받아야 하는 hello 데이터를 기반으로 비즈니스 흐름을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-106">Build your business flow based on hello data you get from Office 365 Video.</span></span> 
* <span data-ttu-id="ef6d1-107">Hello 비디오 포털 상태를 확인 하는 사용 하 여 작업에는 채널 등 모든 비디오의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-107">Use actions that check hello video portal status, get a list of all video in a channel, and more.</span></span> <span data-ttu-id="ef6d1-108">이러한 작업 응답을 가져오고 다른 작업에 사용할 수 있는 hello 출력을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="ef6d1-109">예를 들어 다음 해당 비디오에 대 한 Office 365 hello 비디오 커넥터 tooget 정보를 사용 하 여 및 Office 365 비디오 hello Bing 검색 커넥터 toosearch 사용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-109">For example, you can use hello Bing Search connector toosearch for Office 365 videos, and then use hello Office 365 video connector tooget information about that video.</span></span> <span data-ttu-id="ef6d1-110">사용자 요구 사항을 충족 하는 hello 비디오 Facebook에이 비디오를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-110">If hello video meets your requirements, you can post this video on Facebook.</span></span> 

<span data-ttu-id="ef6d1-111">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toooffice365-video-connector"></a><span data-ttu-id="ef6d1-112">연결 tooOffice365 비디오 커넥터 만들기</span><span class="sxs-lookup"><span data-stu-id="ef6d1-112">Create a connection tooOffice365 Video connector</span></span>
<span data-ttu-id="ef6d1-113">코드 서명 해야이 커넥터 tooyour 논리 앱을 추가 하면-tooyour Office 365 비디오에서에서 계정 및 tooconnect tooyour 계정 논리 앱을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-113">When you add this connector tooyour logic apps, you must sign-in tooyour Office 365 Video account and allow logic apps tooconnect tooyour account.</span></span>

> [!INCLUDE [Steps toocreate a connection tooOffice 365 Video](../../includes/connectors-create-api-office365video.md)]
> 
> 

<span data-ttu-id="ef6d1-114">Office 365 hello 비디오 속성 hello 테 넌 트 이름 처럼 입력 hello 연결을 만든 후 또는 채널 id입니다.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-114">After you create hello connection, you enter hello Office 365 video properties, like hello tenant name or channel ID.</span></span> 


## <a name="connector-specific-details"></a><span data-ttu-id="ef6d1-115">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="ef6d1-115">Connector-specific details</span></span>

<span data-ttu-id="ef6d1-116">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/office365videoconnector/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-116">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/office365videoconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="ef6d1-117">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="ef6d1-117">More connectors</span></span>
<span data-ttu-id="ef6d1-118">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef6d1-118">Go back toohello [APIs list](apis-list.md).</span></span>
