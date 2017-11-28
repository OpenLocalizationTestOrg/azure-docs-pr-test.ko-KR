---
title: "Azure 논리 앱에 aaaUse hello Slack 커넥터 | Microsoft Docs"
description: "TooSlack 논리 앱에 연결"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a><span data-ttu-id="32998-103">Hello Slack 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="32998-103">Get started with hello Slack connector</span></span>
<span data-ttu-id="32998-104">Slack은 팀의 모든 통신을 한데 모아, 어디서나 즉시 검색 및 사용할 수 있는 팀 통신 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="32998-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="32998-105">논리 앱을 만들어 시작합니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32998-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooslack"></a><span data-ttu-id="32998-106">연결 tooSlack 만들기</span><span class="sxs-lookup"><span data-stu-id="32998-106">Create a connection tooSlack</span></span>
<span data-ttu-id="32998-107">toouse hello Slack 커넥터를 처음 만들면는 **연결** 다음 이러한 속성에 대 한 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="32998-107">toouse hello Slack connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="32998-108">속성</span><span class="sxs-lookup"><span data-stu-id="32998-108">Property</span></span> | <span data-ttu-id="32998-109">필수</span><span class="sxs-lookup"><span data-stu-id="32998-109">Required</span></span> | <span data-ttu-id="32998-110">설명</span><span class="sxs-lookup"><span data-stu-id="32998-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="32998-111">신뢰</span><span class="sxs-lookup"><span data-stu-id="32998-111">Token</span></span> |<span data-ttu-id="32998-112">예</span><span class="sxs-lookup"><span data-stu-id="32998-112">Yes</span></span> |<span data-ttu-id="32998-113">Slack 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="32998-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="32998-114">이러한 단계 toosign 여유 시간 및 완료 hello 구성의 hello 여유 시간에 따라 **연결** 논리 앱에서:</span><span class="sxs-lookup"><span data-stu-id="32998-114">Follow these steps toosign into Slack, and complete hello configuration of hello Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="32998-115">**되풀이**</span><span class="sxs-lookup"><span data-stu-id="32998-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="32998-116">**빈도**를 선택하고 **간격**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="32998-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="32998-117">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32998-117">Select **Add an action**</span></span>  
   <span data-ttu-id="32998-118">![Slack 구성][1]</span><span class="sxs-lookup"><span data-stu-id="32998-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="32998-119">Hello 검색 상자에 Slack을 입력 하 고 기다리는 hello 검색 tooreturn hello 이름에 Slack 가진 모든 항목</span><span class="sxs-lookup"><span data-stu-id="32998-119">Enter Slack in hello search box and wait for hello search tooreturn all entries with Slack in hello name</span></span>
5. <span data-ttu-id="32998-120">**Slack-메시지 게시**</span><span class="sxs-lookup"><span data-stu-id="32998-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="32998-121">선택 **tooSlack 로그인**:</span><span class="sxs-lookup"><span data-stu-id="32998-121">Select **Sign in tooSlack**:</span></span>  
   <span data-ttu-id="32998-122">![Slack 구성][2]</span><span class="sxs-lookup"><span data-stu-id="32998-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="32998-123">사용자 자격 증명 Slack toosign tooauthorize hello 응용 프로그램에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="32998-123">Provide your Slack credentials toosign in tooauthorize hello  application</span></span>    
   ![Slack 구성][3]  
8. <span data-ttu-id="32998-125">리디렉션된 tooyour 조직의 로그인 페이지 수. 있습니다</span><span class="sxs-lookup"><span data-stu-id="32998-125">You'll be redirected tooyour organization's Log in page.</span></span> <span data-ttu-id="32998-126">**권한 부여** 논리 앱과 함께 Slack toointeract:</span><span class="sxs-lookup"><span data-stu-id="32998-126">**Authorize** Slack toointeract with your logic app:</span></span>      
   <span data-ttu-id="32998-127">![Slack 구성][5]</span><span class="sxs-lookup"><span data-stu-id="32998-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="32998-128">Hello 권한 부여가 완료 된 후 수 리디렉션된 tooyour 논리 앱 toocomplete hello를 구성 하 여 해당 **여유-모든 메시지를 가져오기** 섹션.</span><span class="sxs-lookup"><span data-stu-id="32998-128">After hello authorization completes you'll be redirected tooyour logic app toocomplete it by configuring hello **Slack - Get all messages** section.</span></span> <span data-ttu-id="32998-129">필요한 다른 트리거 및 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32998-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="32998-130">![Slack 구성][6]</span><span class="sxs-lookup"><span data-stu-id="32998-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="32998-131">작업을 선택 하 여 저장 **저장** 위의 hello 메뉴 모음의 합니다.</span><span class="sxs-lookup"><span data-stu-id="32998-131">Save your work by selecting **Save** on hello menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="32998-132">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="32998-132">Connector-specific details</span></span>

<span data-ttu-id="32998-133">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/slack/)합니다.</span><span class="sxs-lookup"><span data-stu-id="32998-133">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="32998-134">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="32998-134">More connectors</span></span>
<span data-ttu-id="32998-135">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="32998-135">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
