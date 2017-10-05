---
title: "Azure Active Directory ID 보호 FAQ | Microsoft Docs"
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
ms.openlocfilehash: 781f868c87cea3cd790d89c61e26eecf352babea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="3ab98-103">Azure Active Directory ID 보호 FAQ</span><span class="sxs-lookup"><span data-stu-id="3ab98-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="3ab98-104">일부 위험 이벤트에 "닫힘(시스템)" 상태가 있는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="3ab98-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="3ab98-105">**A:** 이러한 이벤트는 Azure Active Directory ID 보호에서 검색했지만 나중에 해당 이벤트가 더 이상 위험하다고 간주되지 않아 닫힌 이벤트이며,</span><span class="sxs-lookup"><span data-stu-id="3ab98-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because the events were no longer considered risky.</span></span> <span data-ttu-id="3ab98-106">사용자의 위험 수준으로 계산되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab98-106">These events do not count towards the user’s risk level.</span></span> 

---

## <a name="do-i-need-to-be-a-global-admin-to-use-identity-protection-in-the-azure-portal"></a><span data-ttu-id="3ab98-107">Azure Portal에서 ID 보호를 사용하려면 전역 관리자여야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3ab98-107">Do I need to be a global admin to use Identity Protection in the Azure portal?</span></span>
<span data-ttu-id="3ab98-108">**A:** **아니요**.</span><span class="sxs-lookup"><span data-stu-id="3ab98-108">**A:** **No**.</span></span> <span data-ttu-id="3ab98-109">보안 읽기 권한자, 보안 관리자 또는 전역 관리자는 ID 보호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab98-109">You can either be a Security Reader, a Security Admin or a Global Admin to use Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="3ab98-110">ID 보호를 얻으려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3ab98-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="3ab98-111">**A:** 이 질문에 대한 답변은 [Azure Active Directory Premium 시작하기](active-directory-get-started-premium.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ab98-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="3ab98-112">Azure Active Directory Premium 2 평가판이 만료되면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="3ab98-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="3ab98-113">**A:** Azure Active Directory Premium 2 평가 버전이 Azure Active Directory Free, Basic 또는 Premium 1 버전에서 만료되고 ID 보호 기능을 사용하도록 설정한 경우에는 라이선스를 준수하지 않아도 여전히 해당 버전에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab98-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access to it even though you are not in compliance with licensing.</span></span>

---
