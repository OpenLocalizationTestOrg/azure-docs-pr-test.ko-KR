---
title: "Azure Active Directory B2B 공동 작업 초대 전자 메일의 요소 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 초대 전자 메일 템플릿"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 458a2cab13b7e83f120e0926a95d454070181dfb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a><span data-ttu-id="2ab6e-103">B2B 공동 작업 초대 전자 메일의 요소</span><span class="sxs-lookup"><span data-stu-id="2ab6e-103">The elements of the B2B collaboration invitation email</span></span>

<span data-ttu-id="2ab6e-104">초대 전자 메일은 온보드의 파트너를 Azure AD에서 B2B 공동 작업 사용자로 불러오기 위한 중요한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="2ab6e-105">받는 사람의 신뢰를 높이는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-105">You can use them to increase the recipient's trust.</span></span> <span data-ttu-id="2ab6e-106">전자 메일에 적법성과 사회적 증거를 전자 메일에 추가하여 받는 사람이 안심하고 **시작** 단추를 선택하여 초대를 수락할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-106">you can add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span></span> <span data-ttu-id="2ab6e-107">이 신뢰는 공유 마찰을 줄이는 데 핵심적입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-107">This trust is a key means to reduce sharing friction.</span></span> <span data-ttu-id="2ab6e-108">또한 이 템플릿을 통해 전자 메일도 보기 좋게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-108">And you also want to make the email look great!</span></span>

![Azure AD B2b 초대 전자 메일](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a><span data-ttu-id="2ab6e-110">전자 메일 설명</span><span class="sxs-lookup"><span data-stu-id="2ab6e-110">Explaining the email</span></span>
<span data-ttu-id="2ab6e-111">전자 메일의 몇 가지 요소를 확인하여 이러한 기능을 최대한 활용하는 방법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-111">Let's look at a few elements of the email so you know how best to use their capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="2ab6e-112">제목</span><span class="sxs-lookup"><span data-stu-id="2ab6e-112">Subject</span></span>
<span data-ttu-id="2ab6e-113">전자 메일의 제목은 다음 패턴을 따릅니다. &lt;tenantname&gt; 조직에 초대되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-113">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="2ab6e-114">보낸 사람 주소</span><span class="sxs-lookup"><span data-stu-id="2ab6e-114">From address</span></span>
<span data-ttu-id="2ab6e-115">보낸 사람 주소에 대해서는 LinkedIn 유사 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-115">We use a LinkedIn-like pattern for the From address.</span></span>  <span data-ttu-id="2ab6e-116">초대자가 누구인지와 어떤 회사에 소속되어 있는지를 명확히 하고 전자 메일이 Microsoft 전자 메일 주소에서 전송된 것인지를 명확히 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-116">You should be clear who the inviter is and from which company, and also clarify that the email is coming from a Microsoft email address.</span></span> <span data-ttu-id="2ab6e-117">형식: &lt;tenantname&gt;(Microsoft를 통해) <invites@microsoft.com&gt;의 &lt;초대자 표시 이름&gt;</span><span class="sxs-lookup"><span data-stu-id="2ab6e-117">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="2ab6e-118">회신</span><span class="sxs-lookup"><span data-stu-id="2ab6e-118">Reply To</span></span>
<span data-ttu-id="2ab6e-119">회신 전자 메일은 사용 가능할 때 초대자의 전자 메일로 설정되므로 전자 메일에 회신하면 초대자에게 전자 메일이 다시 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-119">The reply-to email is set to the inviter's email when available, so that replying to the email sends an email back to the inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="2ab6e-120">브랜딩</span><span class="sxs-lookup"><span data-stu-id="2ab6e-120">Branding</span></span>
<span data-ttu-id="2ab6e-121">테넌트에서 보낸 초대 전자 메일은 테넌트에 대해 설정했을 수 있는 회사 브랜딩을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-121">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="2ab6e-122">이 기능을 활용하려는 경우 자세한 구성 방법은 [다음](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-122">If you want to take advantage of this capability, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span></span> <span data-ttu-id="2ab6e-123">전자 메일에 배너 로고가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-123">The banner logo appears in the email.</span></span> <span data-ttu-id="2ab6e-124">최상의 결과를 얻으려면 [여기](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal)에 제공되는 이미지 크기 및 품질 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-124">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="2ab6e-125">또한 회사 이름이 활용 방안에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-125">In addition, the company name also shows up in the call to action.</span></span>

### <a name="call-to-action"></a><span data-ttu-id="2ab6e-126">활용 방안</span><span class="sxs-lookup"><span data-stu-id="2ab6e-126">Call to action</span></span>
<span data-ttu-id="2ab6e-127">활용 방안은 받는 사람이 메일을 받은 이유에 대한 설명과 받는 사람이 요청 받은 작업의 두 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-127">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span></span>
- <span data-ttu-id="2ab6e-128">"이유" 섹션은 다음 패턴을 사용하여 처리될 수 있습니다. &lt;tenantname&gt; 조직에서 응용 프로그램에 액세스하도록 초대되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-128">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="2ab6e-129">또한 "요청되는 작업" 섹션은 **시작** 단추의 존재 여부에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-129">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span></span> <span data-ttu-id="2ab6e-130">초대 받을 필요가 없는 받는 사람이 추가되면 이 단추가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-130">When the recipient has been added without the need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="2ab6e-131">초대자에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="2ab6e-131">Inviter's information</span></span>
<span data-ttu-id="2ab6e-132">초대자의 표시 이름이 전자 메일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-132">The inviter's display name is included in the email.</span></span> <span data-ttu-id="2ab6e-133">또한 Azure AD 계정에 대해 프로필 사진을 설정한 경우 초대 전자 메일에 해당 사진도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-133">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span></span> <span data-ttu-id="2ab6e-134">두 가지 항목 모두 전자 메일에 대한 받는 사람의 신뢰도를 높이기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-134">Both are intended to increase your recipient's confidence in the email.</span></span>

<span data-ttu-id="2ab6e-135">자신의 프로필 사진을 아직 설정하지 않은 경우 다음과 같이 사진 대신 초대자의 이니셜이 있는 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-135">If you haven't yet set up your profile picture, an icon with the inviter's initials in place of the picture is shown:</span></span>

  ![초대자의 이니셜 표시](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="2ab6e-137">body</span><span class="sxs-lookup"><span data-stu-id="2ab6e-137">Body</span></span>
<span data-ttu-id="2ab6e-138">본문에는 초대자가 작성했거나 초대 API를 통해 전달된 메시지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-138">The body contains the message that the inviter composes or is passed through the invitation API.</span></span> <span data-ttu-id="2ab6e-139">이것은 텍스트 영역에 불과하며, 보안상의 이유로 HTML 태그를 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-139">It is a text area, so it does not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="2ab6e-140">바닥글 섹션</span><span class="sxs-lookup"><span data-stu-id="2ab6e-140">Footer section</span></span>
<span data-ttu-id="2ab6e-141">바닥글에는 Microsoft 회사 브랜드가 포함되며, 받는 사람은 이를 통해 전자 메일이 모니터링되지 않은 별칭에서 전송되었는지 여부를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-141">The footer contains the Microsoft company brand and lets the recipient know if the email was sent from an unmonitored alias.</span></span> <span data-ttu-id="2ab6e-142">특수 사례:</span><span class="sxs-lookup"><span data-stu-id="2ab6e-142">Special cases:</span></span>

- <span data-ttu-id="2ab6e-143">초대자에게 초대 테넌시의 전자 메일 주소가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-143">The inviter doesn't have an email address in the inviting tenancy</span></span>

  ![초대자 사진에 초대 테넌시의 전자 메일 주소가 없습니다.](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="2ab6e-145">받는 사람이 초대를 충전할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab6e-145">The recipient doesn't need to redeem the invitation</span></span>

  ![받는 사람이 초대를 충전할 필요가 없는 경우](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="2ab6e-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ab6e-147">Next steps</span></span>

<span data-ttu-id="2ab6e-148">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="2ab6e-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="2ab6e-149">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="2ab6e-149">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="2ab6e-150">Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2ab6e-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="2ab6e-151">정보 작업자가 B2B 공동 작업 사용자를 추가하는 방법은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="2ab6e-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="2ab6e-152">B2B 공동 작업 초대 상환</span><span class="sxs-lookup"><span data-stu-id="2ab6e-152">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="2ab6e-153">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="2ab6e-153">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="2ab6e-154">Azure Active Directory B2B 공동 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2ab6e-154">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="2ab6e-155">Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)</span><span class="sxs-lookup"><span data-stu-id="2ab6e-155">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="2ab6e-156">Azure Active Directory B2B 공동 작업 API 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2ab6e-156">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="2ab6e-157">B2B 공동 작업 사용자에 대한 다단계 인증</span><span class="sxs-lookup"><span data-stu-id="2ab6e-157">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="2ab6e-158">초대 없이 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="2ab6e-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="2ab6e-159">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="2ab6e-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
