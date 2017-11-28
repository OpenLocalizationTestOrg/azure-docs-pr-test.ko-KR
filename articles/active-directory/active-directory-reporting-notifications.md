---
title: "aaaAzure Active Directory Reporting 알림"
description: "어떻게 toouse hello 의심 스러운 로그인에 대 한 Azure Active Directory reporting 알림 기능입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="336a8-103">Azure Active Directory Reporting 알림</span><span class="sxs-lookup"><span data-stu-id="336a8-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="336a8-104">어떤 보고서가 전자 메일 알림을 생성하나요?</span><span class="sxs-lookup"><span data-stu-id="336a8-104">What reports generate email notifications</span></span>
<span data-ttu-id="336a8-105">이때 보고서 트리거 활동에에서 비정상적인 로그인을 hello만 전자 메일 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="336a8-105">At this time, only hello Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="336a8-106">"비정상적인 로그인"이란 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="336a8-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="336a8-107">비정상적인 로그인은 기계 학습 알고리즘을 결합 한 비정상적인 로그인 위치와 장치를 사용 하는 "이동 불가능" 상태의 hello 기준에 의해 식별 된 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="336a8-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on hello basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="336a8-108">이 해커가이 계정을 사용 하 여 toosign 노력해 왔습니다 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="336a8-108">This may indicate that a hacker has been trying toosign in using this account.</span></span>

## <a name="who-receives-hello-email-notifications"></a><span data-ttu-id="336a8-109">Hello 전자 메일 알림을 받는 사람?</span><span class="sxs-lookup"><span data-stu-id="336a8-109">Who receives hello email notifications?</span></span>
<span data-ttu-id="336a8-110">hello 메일이 tooall 전역 관리자에 게는 Active Directory Premium 라이선스가 할당 된 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="336a8-110">hello email is sent tooall global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="336a8-111">제공 된다는 tooensure, 보냅니다 toohello 관리자 대체 전자 메일 주소로 합니다.</span><span class="sxs-lookup"><span data-stu-id="336a8-111">tooensure it is delivered, we send it toohello admins Alternate Email Address as well.</span></span> <span data-ttu-id="336a8-112">관리자가 포함 되어야 aad-alerts-noreply@mail.windowsazure.com 누락 되지 hello 전자 메일 수신 허용 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="336a8-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss hello email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="336a8-113">이러한 전자 메일은 얼마나 자주 전송되나요?</span><span class="sxs-lookup"><span data-stu-id="336a8-113">How often are these emails sent?</span></span>
<span data-ttu-id="336a8-114">지난 30 일 동안 hello에 10 개의 새 비정상적인 로그인 활동 발생 하거나 hello 마지막 전자 메일을 보낸 후 더 작은 경우 hello 메일이 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="336a8-114">hello email is sent if 10 new irregular sign-in activities occur in hello last 30 days, or since hello last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a><span data-ttu-id="336a8-115">Hello 전자 메일에 언급 된 hello 보고서에 액세스 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="336a8-115">How do I access hello report mentioned in hello email?</span></span>
<span data-ttu-id="336a8-116">Hello 링크를 클릭할 때 hello Azure 클래식 포털 내에서 보고서 페이지 리디렉션된 toohello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="336a8-116">When you click on hello link, you will be redirected toohello report page within hello Azure classic portal.</span></span> <span data-ttu-id="336a8-117">순서로 tooaccess hello 보고서 toobe 모두 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="336a8-117">In order tooaccess hello report, you need toobe both:</span></span>

* <span data-ttu-id="336a8-118">Azure 구독의 관리자 또는 공동 관리자</span><span class="sxs-lookup"><span data-stu-id="336a8-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="336a8-119">Hello 디렉터리의 전역 관리자는 Active Directory Premium 라이선스가 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="336a8-119">A global administrator in hello directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="336a8-120">자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="336a8-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="336a8-121">이러한 전자 메일을 끌 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="336a8-121">Can I turn off these emails?</span></span>
<span data-ttu-id="336a8-122">예, 알림 표시 하지 tooturn 관련 hello Azure 클래식 포털 내에서 tooanomalous 로그인을 클릭 **구성**를 선택한 후 **비활성화 된** hello에서 **알림**섹션.</span><span class="sxs-lookup"><span data-stu-id="336a8-122">Yes, tooturn off notifications related tooanomalous sign-ins within hello Azure classic portal, click **Configure**, and then select **Disabled** under hello **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="336a8-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="336a8-123">What's next</span></span>
* <span data-ttu-id="336a8-124">사용 가능한 보안, 감사 및 작업 보고서는</span><span class="sxs-lookup"><span data-stu-id="336a8-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="336a8-125">[Azure AD 보안, 감사 및 작업 보고서](active-directory-view-access-usage-reports.md) 확인</span><span class="sxs-lookup"><span data-stu-id="336a8-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="336a8-126">Azure Active Directory Premium 시작</span><span class="sxs-lookup"><span data-stu-id="336a8-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="336a8-127">회사 브랜딩 tooyour 로그인 및 액세스 패널 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="336a8-127">Add company branding tooyour Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

