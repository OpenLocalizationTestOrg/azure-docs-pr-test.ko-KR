---
title: "Azure Logic Apps의 ProjectOnline 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. Project Online은 PPM(프로젝트 포트폴리오 관리) 및 Microsoft의 일상 업무를 위한 유연한 온라인 솔루션입니다. 조직에서는 Office 365를 통해 지원되는 Project Online을 통해 강력한 프로젝트 관리 기능을 신속하게 시작하여 어디서든지 모든 장치의 프로젝트와 프로젝트 포트폴리오 투자를 계획하고 우선 순위를 정하며 관리할 수 있습니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 40ce621e-4925-4653-93bb-71ab9abcbdf1
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b075e2eb36f54afb7544e0aeb698701cd224ff93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-projectonline-connector"></a><span data-ttu-id="4f112-105">ProjectOnline 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="4f112-105">Get started with the ProjectOnline connector</span></span>
<span data-ttu-id="4f112-106">Project Online은 PPM(프로젝트 포트폴리오 관리) 및 Microsoft의 일상 업무를 위한 유연한 온라인 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="4f112-106">Project Online is a flexible online solution for project portfolio management (PPM) and everyday work from Microsoft.</span></span> <span data-ttu-id="4f112-107">조직에서는 Office 365를 통해 지원되는 Project Online을 통해 강력한 프로젝트 관리 기능을 신속하게 시작하여 어디서든지 모든 장치의 프로젝트와 프로젝트 포트폴리오 투자를 계획하고 우선 순위를 정하며 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f112-107">Delivered through Office 365, Project Online enables organizations to get started quickly with powerful project management capabilities to plan, prioritize, and manage projects and project portfolio investments—from almost anywhere on almost any device.</span></span>

<span data-ttu-id="4f112-108">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f112-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-projectonline"></a><span data-ttu-id="4f112-109">ProjectOnline에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="4f112-109">Create a connection to ProjectOnline</span></span>
<span data-ttu-id="4f112-110">ProjectOnline으로 논리 앱을 만들려면 먼저 **연결**을 만든 후에 다음 속성에 대한 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f112-110">To create Logic apps with ProjectOnline, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="4f112-111">속성</span><span class="sxs-lookup"><span data-stu-id="4f112-111">Property</span></span> | <span data-ttu-id="4f112-112">필수</span><span class="sxs-lookup"><span data-stu-id="4f112-112">Required</span></span> | <span data-ttu-id="4f112-113">설명</span><span class="sxs-lookup"><span data-stu-id="4f112-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f112-114">신뢰</span><span class="sxs-lookup"><span data-stu-id="4f112-114">Token</span></span> |<span data-ttu-id="4f112-115">예</span><span class="sxs-lookup"><span data-stu-id="4f112-115">Yes</span></span> |<span data-ttu-id="4f112-116">ProjectOnline 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="4f112-116">Provide ProjectOnline Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to ProjectOnline](../../includes/connectors-create-api-projectonline.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="4f112-117">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="4f112-117">Connector-specific details</span></span>

<span data-ttu-id="4f112-118">[커넥터 세부 정보](/connectors/projectonline/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f112-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/projectonline/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="4f112-119">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="4f112-119">More connectors</span></span>
<span data-ttu-id="4f112-120">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="4f112-120">Go back to the [APIs list](apis-list.md).</span></span>