---
title: "Logic Apps에서 Slack 커넥터 사용 | Microsoft Docs"
description: "Logic Apps에서 Slack에 연결"
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
ms.openlocfilehash: fc5fc128efe01bd0727e3ff30d8938918e89ac3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-slack-connector"></a><span data-ttu-id="ef707-103">Slack 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="ef707-103">Get started with the Slack connector</span></span>
<span data-ttu-id="ef707-104">Slack은 팀의 모든 통신을 한데 모아, 어디서나 즉시 검색 및 사용할 수 있는 팀 통신 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="ef707-105">논리 앱을 만들어 시작합니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef707-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-slack"></a><span data-ttu-id="ef707-106">Slack에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="ef707-106">Create a connection to Slack</span></span>
<span data-ttu-id="ef707-107">Slack 커넥터를 사용하려면 먼저 **연결** 을 만든 다음 이러한 속성에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-107">To use the Slack connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="ef707-108">속성</span><span class="sxs-lookup"><span data-stu-id="ef707-108">Property</span></span> | <span data-ttu-id="ef707-109">필수</span><span class="sxs-lookup"><span data-stu-id="ef707-109">Required</span></span> | <span data-ttu-id="ef707-110">설명</span><span class="sxs-lookup"><span data-stu-id="ef707-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ef707-111">신뢰</span><span class="sxs-lookup"><span data-stu-id="ef707-111">Token</span></span> |<span data-ttu-id="ef707-112">예</span><span class="sxs-lookup"><span data-stu-id="ef707-112">Yes</span></span> |<span data-ttu-id="ef707-113">Slack 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="ef707-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="ef707-114">다음 단계를 따라 Slack에 로그인하고 논리 앱의 Slack **연결** 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-114">Follow these steps to sign into Slack, and complete the configuration of the Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="ef707-115">**되풀이**</span><span class="sxs-lookup"><span data-stu-id="ef707-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="ef707-116">**빈도**를 선택하고 **간격**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="ef707-117">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-117">Select **Add an action**</span></span>  
   <span data-ttu-id="ef707-118">![Slack 구성][1]</span><span class="sxs-lookup"><span data-stu-id="ef707-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="ef707-119">검색 상자에 Slack을 입력하고 이름에 Slack이 있는 모든 항목이 반환될 때까지 검색을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-119">Enter Slack in the search box and wait for the search to return all entries with Slack in the name</span></span>
5. <span data-ttu-id="ef707-120">**Slack-메시지 게시**</span><span class="sxs-lookup"><span data-stu-id="ef707-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="ef707-121">**Slack에 로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-121">Select **Sign in to Slack**:</span></span>  
   <span data-ttu-id="ef707-122">![Slack 구성][2]</span><span class="sxs-lookup"><span data-stu-id="ef707-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="ef707-123">Slack 자격 증명을 제공하여 로그인하고 응용 프로그램에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-123">Provide your Slack credentials to sign in to authorize the  application</span></span>    
   ![Slack 구성][3]  
8. <span data-ttu-id="ef707-125">조직의 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-125">You'll be redirected to your organization's Log in page.</span></span> <span data-ttu-id="ef707-126">논리 앱과 상호 작용하도록 Slack에 **권한을 부여**합니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-126">**Authorize** Slack to interact with your logic app:</span></span>      
   <span data-ttu-id="ef707-127">![Slack 구성][5]</span><span class="sxs-lookup"><span data-stu-id="ef707-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="ef707-128">권한 부여가 완료된 후 **Slack - 모든 메시지 가져오기** 섹션을 구성하여 완료하기 위해 논리 앱으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-128">After the authorization completes you'll be redirected to your logic app to complete it by configuring the **Slack - Get all messages** section.</span></span> <span data-ttu-id="ef707-129">필요한 다른 트리거 및 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="ef707-130">![Slack 구성][6]</span><span class="sxs-lookup"><span data-stu-id="ef707-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="ef707-131">위의 메뉴 모음에서 **저장** 을 선택하여 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-131">Save your work by selecting **Save** on the menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="ef707-132">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="ef707-132">Connector-specific details</span></span>

<span data-ttu-id="ef707-133">[커넥터 세부 정보](/connectors/slack/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-133">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="ef707-134">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="ef707-134">More connectors</span></span>
<span data-ttu-id="ef707-135">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="ef707-135">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
