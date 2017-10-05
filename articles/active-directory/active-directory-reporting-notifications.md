---
title: "Azure Active Directory Reporting 알림"
description: "의심스러운 로그인에 Azure Active Directory Reporting 알림을 사용하는 방법입니다."
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
ms.openlocfilehash: f4632bd2af802b10c8c64972e8c605d7ad7c0eaf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="1e082-103">Azure Active Directory Reporting 알림</span><span class="sxs-lookup"><span data-stu-id="1e082-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="1e082-104">어떤 보고서가 전자 메일 알림을 생성하나요?</span><span class="sxs-lookup"><span data-stu-id="1e082-104">What reports generate email notifications</span></span>
<span data-ttu-id="1e082-105">지금은 비정상적인 로그인 활동 보고서만 메일 알림을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="1e082-105">At this time, only the Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="1e082-106">"비정상적인 로그인"이란 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="1e082-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="1e082-107">비정상적인 로그인은 비정상적인 로그인 위치 및 장치와 결합된 "불가능한 이동" 조건을 기준으로 기계 학습 알고리즘에서 식별된 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="1e082-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="1e082-108">이는 해커가 이 계정을 사용하여 로그인하려고 하고 있음을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e082-108">This may indicate that a hacker has been trying to sign in using this account.</span></span>

## <a name="who-receives-the-email-notifications"></a><span data-ttu-id="1e082-109">누가 전자 메일 알림을 받나요?</span><span class="sxs-lookup"><span data-stu-id="1e082-109">Who receives the email notifications?</span></span>
<span data-ttu-id="1e082-110">Active Directory Premium 라이선스가 할당된 모든 전역 관리자에게 전자 메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e082-110">The email is sent to all global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="1e082-111">성공적인 배달을 위해 관리자 대체 전자 메일 주소로도 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e082-111">To ensure it is delivered, we send it to the admins Alternate Email Address as well.</span></span> <span data-ttu-id="1e082-112">관리자는 전자 메일이 누락되지 않도록 aad-alerts-noreply@mail.windowsazure.com 을 수신 허용 - 보낸 사람 목록에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e082-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss the email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="1e082-113">이러한 전자 메일은 얼마나 자주 전송되나요?</span><span class="sxs-lookup"><span data-stu-id="1e082-113">How often are these emails sent?</span></span>
<span data-ttu-id="1e082-114">지난 30일 또는 마지막 메일이 전송된 이후 중 더 짧은 시간 동안 비정상적인 로그인 활동 10개가 새로 발생한 경우 메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e082-114">The email is sent if 10 new irregular sign-in activities occur in the last 30 days, or since the last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-the-report-mentioned-in-the-email"></a><span data-ttu-id="1e082-115">전자 메일에 언급된 보고서에 액세스하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="1e082-115">How do I access the report mentioned in the email?</span></span>
<span data-ttu-id="1e082-116">링크를 클릭하면 Azure 클래식 포털 내의 보고서 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e082-116">When you click on the link, you will be redirected to the report page within the Azure classic portal.</span></span> <span data-ttu-id="1e082-117">보고서에 액세스하려면 다음 조건을 둘 다 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e082-117">In order to access the report, you need to be both:</span></span>

* <span data-ttu-id="1e082-118">Azure 구독의 관리자 또는 공동 관리자</span><span class="sxs-lookup"><span data-stu-id="1e082-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="1e082-119">디렉터리의 전역 관리자 및 Active Directory Premium 라이선스가 할당됨.</span><span class="sxs-lookup"><span data-stu-id="1e082-119">A global administrator in the directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="1e082-120">자세한 내용은 [Azure Active Directory 버전](active-directory-editions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e082-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="1e082-121">이러한 전자 메일을 끌 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="1e082-121">Can I turn off these emails?</span></span>
<span data-ttu-id="1e082-122">예, Azure 클래식 포털 내에서 비정상적인 로그인과 관련된 알림을 끄려면 **구성**을 클릭한 다음 **알림** 아래에서 **사용 안 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1e082-122">Yes, to turn off notifications related to anomalous sign-ins within the Azure classic portal, click **Configure**, and then select **Disabled** under the **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="1e082-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e082-123">What's next</span></span>
* <span data-ttu-id="1e082-124">사용 가능한 보안, 감사 및 작업 보고서는</span><span class="sxs-lookup"><span data-stu-id="1e082-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="1e082-125">[Azure AD 보안, 감사 및 작업 보고서](active-directory-view-access-usage-reports.md) 확인</span><span class="sxs-lookup"><span data-stu-id="1e082-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="1e082-126">Azure Active Directory Premium 시작</span><span class="sxs-lookup"><span data-stu-id="1e082-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="1e082-127">로그인 및 액세스 패널 페이지에 회사 브랜딩 추가하기</span><span class="sxs-lookup"><span data-stu-id="1e082-127">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

