---
title: "Active Directory Id 보호 알림 aaaAzure | Microsoft Docs"
description: "알림에서 조사 활동을 지원하는 방법에 대해 알아봅니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 클라우드 앱 검색, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약점, 보안 정책"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="9f447-104">Azure Active Directory ID 보호 알림</span><span class="sxs-lookup"><span data-stu-id="9f447-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="9f447-105">Azure AD Id 보호는 두 가지 유형의 자동화 된 알림 사용자 위험 및 위험 이벤트 관리 toohelp 전자 메일로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9f447-105">Azure AD Identity Protection sends two types of automated notification emails toohelp you manage user risk and risk events:</span></span>

* <span data-ttu-id="9f447-106">사용자 손상된 경고 전자 메일</span><span class="sxs-lookup"><span data-stu-id="9f447-106">User compromised alert email</span></span>
* <span data-ttu-id="9f447-107">주간 다이제스트 전자 메일</span><span class="sxs-lookup"><span data-stu-id="9f447-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="9f447-108">사용자 손상된 경고 전자 메일</span><span class="sxs-lookup"><span data-stu-id="9f447-108">User compromised alert email</span></span>
<span data-ttu-id="9f447-109">Azure AD ID 보호가 계정이 손상되었다고 식별하는 경우 사용자 손상된 전자 메일 경고를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9f447-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="9f447-110">hello 전자 메일에 사용자가을 hello Identity Protection 대시보드에서 위험 보고서에 대 한 플래그가 지정 된 링크 toohello를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f447-110">hello email includes a link toohello Users flagged for risk report in hello Identity Protection dashboard.</span></span> <span data-ttu-id="9f447-111">손상된 계정에 대한 알림을 즉시 조사하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9f447-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="9f447-112">주간 다이제스트 전자 메일</span><span class="sxs-lookup"><span data-stu-id="9f447-112">Weekly digest email</span></span>
<span data-ttu-id="9f447-113">주 단위 요약 전자 메일 hello 새 위험 이벤트의 요약을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f447-113">hello weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="9f447-114"> 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9f447-114">It includes:</span></span>

* <span data-ttu-id="9f447-115">위험에 노출된 사용자</span><span class="sxs-lookup"><span data-stu-id="9f447-115">Users at risk</span></span>
* <span data-ttu-id="9f447-116">의심스러운 활동</span><span class="sxs-lookup"><span data-stu-id="9f447-116">Suspicious activities</span></span>
* <span data-ttu-id="9f447-117">감지된 취약점</span><span class="sxs-lookup"><span data-stu-id="9f447-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="9f447-118">링크 toohello Id 보호에서 보고서와 관련 된</span><span class="sxs-lookup"><span data-stu-id="9f447-118">Links toohello related reports in Identity Protection</span></span>

<br><span data-ttu-id="9f447-119">
![업데이트 관리](./media/active-directory-identityprotection-notifications/400.png "업데이트 관리")
</span><span class="sxs-lookup"><span data-stu-id="9f447-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="9f447-120">주 단위 요약 메일 보내기를 끌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f447-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="9f447-121">
![사용자 위험](./media/active-directory-identityprotection-notifications/62.png "사용자 위험")
</span><span class="sxs-lookup"><span data-stu-id="9f447-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="9f447-122">**tooopen hello 관련된 구성 대화 상자**:</span><span class="sxs-lookup"><span data-stu-id="9f447-122">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="9f447-123">Hello에 **Azure AD Identity Protection** 블레이드에서 클릭 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="9f447-123">On hello **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="9f447-124">
   ![사용자 위험 정책](./media/active-directory-identityprotection-notifications/401.png "사용자 위험 정책")
   </span><span class="sxs-lookup"><span data-stu-id="9f447-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="9f447-125">Hello에 **일반** 섹션에서 클릭 **알림**합니다.</span><span class="sxs-lookup"><span data-stu-id="9f447-125">In hello **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="9f447-126">
   ![사용자 위험 정책](./media/active-directory-identityprotection-notifications/405.png "사용자 위험 정책")
   </span><span class="sxs-lookup"><span data-stu-id="9f447-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="9f447-127">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9f447-127">See also</span></span>
* [<span data-ttu-id="9f447-128">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="9f447-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
