---
title: "Azure Logic Apps의 MailChimp 커넥터 | Microsoft Docs"
description: "Azure 앱 서비스로 논리 앱을 만듭니다. MailChimp는 비즈니스에서 마케팅 전자 메일, 자동화된 메시지 및 대상 캠페인 전송을 비롯한 전자 메일 마케팅 작업을 관리하고 자동화할 수 있는 SaaS 서비스입니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 36559de2-94f0-4355-b492-2926dfc56486
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 46de91881f84183d0359755f49a115e712a7033b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-mailchimp-connector"></a><span data-ttu-id="36863-104">MailChimp 커넥터 시작</span><span class="sxs-lookup"><span data-stu-id="36863-104">Get started with the MailChimp connector</span></span>
<span data-ttu-id="36863-105">MailChimp는 비즈니스에서 마케팅 전자 메일, 자동화된 메시지 및 대상 캠페인 전송을 비롯한 전자 메일 마케팅 작업을 관리하고 자동화할 수 있는 SaaS 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="36863-105">MailChimp is a SaaS service that allows businesses to manage and automate email marketing activities, including sending marketing emails, automated messages and targeted campaigns.</span></span>

<span data-ttu-id="36863-106">이제 논리 앱을 만들어 시작할 수 있습니다. [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36863-106">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-mailchimp"></a><span data-ttu-id="36863-107">MailChimp에 대한 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="36863-107">Create a connection to MailChimp</span></span>
<span data-ttu-id="36863-108">MailChimp로 논리 앱을 만들려면 먼저 **연결**을 만든 후에 다음 속성에 대한 세부 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36863-108">To create Logic apps with MailChimp, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="36863-109">속성</span><span class="sxs-lookup"><span data-stu-id="36863-109">Property</span></span> | <span data-ttu-id="36863-110">필수</span><span class="sxs-lookup"><span data-stu-id="36863-110">Required</span></span> | <span data-ttu-id="36863-111">설명</span><span class="sxs-lookup"><span data-stu-id="36863-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36863-112">신뢰</span><span class="sxs-lookup"><span data-stu-id="36863-112">Token</span></span> |<span data-ttu-id="36863-113">예</span><span class="sxs-lookup"><span data-stu-id="36863-113">Yes</span></span> |<span data-ttu-id="36863-114">MailChimp 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="36863-114">Provide MailChimp Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to MailChimp](../../includes/connectors-create-api-mailchimp.md)]
> 


## <a name="connector-specific-details"></a><span data-ttu-id="36863-115">커넥터 관련 세부 정보</span><span class="sxs-lookup"><span data-stu-id="36863-115">Connector-specific details</span></span>

<span data-ttu-id="36863-116">[커넥터 세부 정보](/connectors/mailchimp/)에서 swagger에 정의된 모든 트리거 및 작업과 제한 사항도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36863-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/mailchimp/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="36863-117">추가 커넥터</span><span class="sxs-lookup"><span data-stu-id="36863-117">More connectors</span></span>
<span data-ttu-id="36863-118">[API 목록](apis-list.md)으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="36863-118">Go back to the [APIs list](apis-list.md).</span></span>