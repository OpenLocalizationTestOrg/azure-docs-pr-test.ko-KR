---
title: "SMS, 전자 메일 및 웹후크에 대한 속도 제한 | Microsoft Docs"
description: "작업 그룹에서 가능한 SMS, 전자 메일 또는 웹후크 알림의 수를 Azure에서 제한하는 방법을 알아봅니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: bde645624ab1860d19ba18470f55845855a7d1fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="fe614-103">SMS 메시지, 전자 메일 및 웹후크 게시에 대한 속도 제한</span><span class="sxs-lookup"><span data-stu-id="fe614-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="fe614-104">속도 제한은 특정 전화 번호나 이메일 주소로 너무 많은 알림이 전송될 때 발생하는 알림의 일시 중단입니다.</span><span class="sxs-lookup"><span data-stu-id="fe614-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent to a particular phone number or email address.</span></span> <span data-ttu-id="fe614-105">속도를 제한하면 경고를 관리하고 실행할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe614-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="fe614-106">SMS 및 전자 메일에 대한 규칙은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="fe614-106">The rules for SMS and email are the same.</span></span> <span data-ttu-id="fe614-107">속도 제한 임계값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe614-107">The rate limit threshold is:</span></span>

 - <span data-ttu-id="fe614-108">**SMS**: 1시간에 10개 메시지</span><span class="sxs-lookup"><span data-stu-id="fe614-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="fe614-109">**전자 메일**: 1시간에 100개 메시지</span><span class="sxs-lookup"><span data-stu-id="fe614-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="fe614-110">속도 제한 규칙</span><span class="sxs-lookup"><span data-stu-id="fe614-110">Rate limit rules</span></span>
- <span data-ttu-id="fe614-111">허용된 임계값보다 더 많은 메시지를 수신하는 경우 특정 전화 번호 또는 전자 메일의 속도가 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe614-111">A particular phone number or email is rate limited when it receives more messages than the threshold allows.</span></span>
- <span data-ttu-id="fe614-112">전화 번호 또는 전자 메일은 많은 구독에서 작업 그룹에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe614-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="fe614-113">속도 제한은 모든 구독에 걸쳐 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe614-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="fe614-114">여러 구독에서 메시지가 전송되는 경우에도 임계값에 도달하면 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe614-114">It applies as soon as the threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="fe614-115">전화 번호 또는 전자 메일의 속도가 제한되면 속도 제한을 알리기 위한 추가 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe614-115">When a phone number or email is rate limited, an additional notification is sent to communicate the rate limiting.</span></span> <span data-ttu-id="fe614-116">속도 제한이 만료되면 알림에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe614-116">The notification states when the rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="fe614-117">웹후크의 속도 제한</span><span class="sxs-lookup"><span data-stu-id="fe614-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="fe614-118">현재 웹후크에 대한 속도 제한은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe614-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe614-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe614-119">Next steps</span></span> ##
* <span data-ttu-id="fe614-120">[SMS 경고 동작](monitoring-sms-alert-behavior.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="fe614-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="fe614-121">[활동 로그 경고의 개요](monitoring-overview-alerts.md)를 확인하고 경고를 받는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="fe614-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="fe614-122">[서비스 상태 알림이 게시될 때마다 경고를 구성](monitoring-activity-log-alerts-on-service-notifications.md)하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="fe614-122">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
