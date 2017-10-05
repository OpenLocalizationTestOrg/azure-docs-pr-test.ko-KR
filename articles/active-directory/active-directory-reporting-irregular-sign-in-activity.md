---
title: "비정상적인 로그인 작업"
description: "보고서에는 기계 학습 알고리즘에 의해 비정상으로 확인된 로그인이 포함됩니다."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: a5a270a9-a0eb-4a99-b04c-ccde3829ffe4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 565321b6f3ad5988f383a701cb9d8bd5c9937795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="irregular-sign-in-activity"></a><span data-ttu-id="b8777-103">비정상적인 로그인 작업</span><span class="sxs-lookup"><span data-stu-id="b8777-103">Irregular sign-in activity</span></span>
<span data-ttu-id="b8777-104">비정상적인 로그인은 비정상적인 로그인 위치 및 장치와 결합된 "불가능한 이동" 조건을 기준으로 기계 학습 알고리즘에서 식별된 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="b8777-104">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign in location and device.</span></span> <span data-ttu-id="b8777-105">이는 해커가 이 계정을 사용하여 성공적으로 로그인했음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8777-105">This may indicate that a hacker has successfully signed in using this account.</span></span>
<span data-ttu-id="b8777-106">30일 이하의 범위 내에서 비정상적인 로그인 이벤트가 10개 이상 발생할 경우 전역 관리자에게 메일 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8777-106">We will send an email notification to the global admins if we encounter 10 or more anomalous sign-in events within a span of 30 days or less.</span></span> <span data-ttu-id="b8777-107">수신 허용 - 보낸 사람 목록에 aad-alerts-noreply@mail.windowsazure.com 이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8777-107">Please be sure to include aad-alerts-noreply@mail.windowsazure.com in your safe senders list.</span></span>

