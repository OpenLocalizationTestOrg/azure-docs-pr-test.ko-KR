---
title: "Logic Apps에서 SharePoint Server 커넥터 사용| Microsoft Docs"
description: "Logic Apps에서 SharePoint Server 커넥터 사용 시작"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0f3274816e279a1aa57febaa2f8294914900799a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-connector"></a><span data-ttu-id="4a883-103">SharePoint 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="4a883-103">Get started with the SharePoint connector</span></span>
<span data-ttu-id="4a883-104">SharePoint 커넥터는 SharePoint에서 목록으로 작업하기 위한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-104">The SharePoint Connector provides an way to work with Lists on SharePoint.</span></span>

<span data-ttu-id="4a883-105">논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a883-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sharepoint"></a><span data-ttu-id="4a883-106">SharePoint에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="4a883-106">Create a connection to SharePoint</span></span>
<span data-ttu-id="4a883-107">SharePoint 커넥터를 사용하려면 먼저 **연결** 을 만든 다음 이러한 속성에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-107">To use the SharePoint Connector , you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="4a883-108">속성</span><span class="sxs-lookup"><span data-stu-id="4a883-108">Property</span></span> | <span data-ttu-id="4a883-109">필수</span><span class="sxs-lookup"><span data-stu-id="4a883-109">Required</span></span> | <span data-ttu-id="4a883-110">설명</span><span class="sxs-lookup"><span data-stu-id="4a883-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a883-111">신뢰</span><span class="sxs-lookup"><span data-stu-id="4a883-111">Token</span></span> |<span data-ttu-id="4a883-112">예</span><span class="sxs-lookup"><span data-stu-id="4a883-112">Yes</span></span> |<span data-ttu-id="4a883-113">SharePoint 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="4a883-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="4a883-114">**SharePoint**에 연결하려면 SharePoint에 ID(사용자 이름 및 암호, 스마트 카드 자격 증명 등)를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-114">To connect to **SharePoint**, enter your identity (username and password, smart card credentials, etc.) to SharePoint.</span></span> <span data-ttu-id="4a883-115">인증되면 논리 앱에서 SharePoint 커넥터를 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-115">Once you've been authenticated, you can proceed to use the SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="4a883-116">논리 앱 디자이너에 있는 동안 다음 단계를 따라 SharePoint에 로그인하여 논리 앱에서 사용할 연결 **연결** 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-116">While on the designer of your logic app, follow these steps to sign into SharePoint to create the connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="4a883-117">검색 상자에 SharePoint를 입력하고 이름에 SharePoint가 있는 모든 항목이 반환될 때까지 검색을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-117">Enter SharePoint in the search box and wait for the search to return all entries with SharePoint in the name:</span></span>   
   ![SharePoint 구성][1]  
2. <span data-ttu-id="4a883-119">**SharePoint - 파일을 만들 때** 선택</span><span class="sxs-lookup"><span data-stu-id="4a883-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="4a883-120">**SharePoint에 로그인** 선택</span><span class="sxs-lookup"><span data-stu-id="4a883-120">Select **Sign in to SharePoint**:</span></span>   
   <span data-ttu-id="4a883-121">![SharePoint 구성][2]</span><span class="sxs-lookup"><span data-stu-id="4a883-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="4a883-122">SharePoint 자격 증명을 제공하여 로그인하고 SharePoint에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-122">Provide your SharePoint credentials to sign in to authenticate with SharePoint</span></span>   
   ![SharePoint 구성][3]     
5. <span data-ttu-id="4a883-124">인증이 완료된 후 SharePoint의 **파일을 만들 때** 대화 상자를 구성하여 완료하기 위해 논리 앱으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-124">After the authentication completes you'll be redirected to your logic app to complete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="4a883-125">![SharePoint 구성][4]</span><span class="sxs-lookup"><span data-stu-id="4a883-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="4a883-126">그런 다음 논리 앱을 완료하는 데 필요한 다른 트리거 및 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-126">You can then add other triggers and actions that you need to complete your logic app.</span></span>   
7. <span data-ttu-id="4a883-127">위의 메뉴 모음에서 **저장** 을 선택하여 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-127">Save your work by selecting **Save** on the menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="4a883-128">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="4a883-128">Connector-specific details</span></span>

<span data-ttu-id="4a883-129">[커넥터 세부 정보](/connectors/sharepoint/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-129">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="4a883-130">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="4a883-130">More connectors</span></span>
<span data-ttu-id="4a883-131">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="4a883-131">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
