---
title: Active Directory Identity Protection FAQ aaaAzure | Microsoft Docs
description: "Azure AD ID 보호에 대한 질문과 대답입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6a053ce02bf7a248a284f482f20f96a312f1c204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="e347f-103">Azure Active Directory ID 보호 FAQ</span><span class="sxs-lookup"><span data-stu-id="e347f-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="e347f-104">일부 위험 이벤트에 "닫힘(시스템)" 상태가 있는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="e347f-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="e347f-105">**A:** 찾아서 hello 이벤트가 더 이상 위험한 것으로 간주 된 닫혀 나중에 Azure Active Directory Id 보호 하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="e347f-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because hello events were no longer considered risky.</span></span> <span data-ttu-id="e347f-106">이러한 이벤트는 hello 사용자의 위험 수준으로 계산 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e347f-106">These events do not count towards hello user’s risk level.</span></span> 

---

## <a name="do-i-need-toobe-a-global-admin-toouse-identity-protection-in-hello-azure-portal"></a><span data-ttu-id="e347f-107">Toobe hello Azure 포털의에서 전역 관리자 toouse Id 보호 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="e347f-107">Do I need toobe a global admin toouse Identity Protection in hello Azure portal?</span></span>
<span data-ttu-id="e347f-108">**A:** **아니요**.</span><span class="sxs-lookup"><span data-stu-id="e347f-108">**A:** **No**.</span></span> <span data-ttu-id="e347f-109">보안 판독기, 보안 관리자 또는 전역 관리자 toouse Id 보호 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e347f-109">You can either be a Security Reader, a Security Admin or a Global Admin toouse Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="e347f-110">ID 보호를 얻으려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="e347f-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="e347f-111">**A:** 참조 [Azure Active Directory Premium 시작](active-directory-get-started-premium.md) 응답 toothis 질문에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e347f-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="e347f-112">Azure Active Directory Premium 2 평가판이 만료되면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="e347f-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="e347f-113">**A:** Azure Active Directory Free, Basic 또는 Premium 1 버전에서는 Azure Active Directory 프리미엄 2 평가판이 만료 되었습니다 경우 Id 보호를 사용 하도록 설정 되어 있으면 있습니다 있습니다 액세스 tooit compliance 사용 하지 않은 라이선스.</span><span class="sxs-lookup"><span data-stu-id="e347f-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access tooit even though you are not in compliance with licensing.</span></span>

---
