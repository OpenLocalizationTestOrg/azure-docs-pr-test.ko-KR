---
title: "논리 앱의 SharePoint Server 커넥터 aaaUse hello | Microsoft Docs"
description: "논리 앱에 hello hello SharePoint Server 커넥터를 사용 하 여 시작"
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
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a><span data-ttu-id="18d37-103">Hello SharePoint 커넥터와 함께 시작</span><span class="sxs-lookup"><span data-stu-id="18d37-103">Get started with hello SharePoint connector</span></span>
<span data-ttu-id="18d37-104">SharePoint 커넥터 hello sharepoint 목록 사용 하 여는 방법은 toowork를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18d37-104">hello SharePoint Connector provides an way toowork with Lists on SharePoint.</span></span>

<span data-ttu-id="18d37-105">논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18d37-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toosharepoint"></a><span data-ttu-id="18d37-106">연결 tooSharePoint 만들기</span><span class="sxs-lookup"><span data-stu-id="18d37-106">Create a connection tooSharePoint</span></span>
<span data-ttu-id="18d37-107">toouse hello SharePoint 커넥터를 처음 만들면는 **연결** 다음 이러한 속성에 대 한 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d37-107">toouse hello SharePoint Connector , you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="18d37-108">속성</span><span class="sxs-lookup"><span data-stu-id="18d37-108">Property</span></span> | <span data-ttu-id="18d37-109">필수</span><span class="sxs-lookup"><span data-stu-id="18d37-109">Required</span></span> | <span data-ttu-id="18d37-110">설명</span><span class="sxs-lookup"><span data-stu-id="18d37-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="18d37-111">신뢰</span><span class="sxs-lookup"><span data-stu-id="18d37-111">Token</span></span> |<span data-ttu-id="18d37-112">예</span><span class="sxs-lookup"><span data-stu-id="18d37-112">Yes</span></span> |<span data-ttu-id="18d37-113">SharePoint 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="18d37-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="18d37-114">tooconnect 너무**SharePoint**, identity (사용자 이름 및 암호, 스마트 카드 자격 증명 등) tooSharePoint를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d37-114">tooconnect too**SharePoint**, enter your identity (username and password, smart card credentials, etc.) tooSharePoint.</span></span> <span data-ttu-id="18d37-115">인증 된을 수행한, 논리 앱에서 toouse hello SharePoint 커넥터를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d37-115">Once you've been authenticated, you can proceed toouse hello SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="18d37-116">논리 앱의 hello 디자이너에 있는 동안 이러한 단계 toosign SharePoint toocreate hello 연결에 따라 **연결** 논리 앱에서 사용 하기 위해:</span><span class="sxs-lookup"><span data-stu-id="18d37-116">While on hello designer of your logic app, follow these steps toosign into SharePoint toocreate hello connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="18d37-117">Hello 검색 상자에 SharePoint를 입력 하 고 hello 검색 tooreturn hello 이름에 SharePoint와 함께 모든 항목 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="18d37-117">Enter SharePoint in hello search box and wait for hello search tooreturn all entries with SharePoint in hello name:</span></span>   
   ![SharePoint 구성][1]  
2. <span data-ttu-id="18d37-119">**SharePoint - 파일을 만들 때** 선택</span><span class="sxs-lookup"><span data-stu-id="18d37-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="18d37-120">선택 **tooSharePoint 로그인**:</span><span class="sxs-lookup"><span data-stu-id="18d37-120">Select **Sign in tooSharePoint**:</span></span>   
   <span data-ttu-id="18d37-121">![SharePoint 구성][2]</span><span class="sxs-lookup"><span data-stu-id="18d37-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="18d37-122">와 sharepoint 통합 tooauthenticate의 SharePoint 자격 증명 toosign 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d37-122">Provide your SharePoint credentials toosign in tooauthenticate with SharePoint</span></span>   
   ![SharePoint 구성][3]     
5. <span data-ttu-id="18d37-124">리디렉션된 tooyour 논리 앱 toocomplete 됩니다 hello 인증 완료 된 후 SharePoint를 구성 하 여 해당 **파일을 만들 때** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="18d37-124">After hello authentication completes you'll be redirected tooyour logic app toocomplete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="18d37-125">![SharePoint 구성][4]</span><span class="sxs-lookup"><span data-stu-id="18d37-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="18d37-126">그런 다음 다른 트리거 및 작업 해야 하는 toocomplete 논리 앱을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d37-126">You can then add other triggers and actions that you need toocomplete your logic app.</span></span>   
7. <span data-ttu-id="18d37-127">작업을 선택 하 여 저장 **저장** 위의 hello 메뉴 모음의 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d37-127">Save your work by selecting **Save** on hello menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="18d37-128">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="18d37-128">Connector-specific details</span></span>

<span data-ttu-id="18d37-129">모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/sharepoint/)합니다.</span><span class="sxs-lookup"><span data-stu-id="18d37-129">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="18d37-130">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="18d37-130">More connectors</span></span>
<span data-ttu-id="18d37-131">Toohello 돌아가서 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="18d37-131">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
