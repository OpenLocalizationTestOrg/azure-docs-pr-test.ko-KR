---
title: "Azure Active Directory B2B 공동 작업 aaaTroubleshooting | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업과 관련된 일반 문제를 해결하는 방법"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="84361-103">Azure Active Directory B2B 공동 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="84361-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="84361-104">Azure AD(Azure Active Directory) B2B 공동 작업과 관련된 일반적인 문제에 대한 몇 가지 해결책은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a><span data-ttu-id="84361-105">외부 사용자를 추가 했으므로 했지만 hello 사용자 선택 또는 전체 주소록 내에서 해당 표시 되지 않으면</span><span class="sxs-lookup"><span data-stu-id="84361-105">I’ve added an external user but do not see them in my Global Address Book or in hello people picker</span></span>

<span data-ttu-id="84361-106">Hello 개체는 외부 사용자에 게 hello 목록의 채워지지 않음의 경우에서 몇 분 tooreplicate를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-106">In cases where external users are not populated in hello list, hello object might take a few minutes tooreplicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="84361-107">B2B 게스트 사용자가 SharePoint Online/OneDrive 사용자 선택에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="84361-108">기존 게스트 사용자 hello SharePoint Online (SPO) 사용자 선택에 대 한 hello 기능 toosearch은 toomatch 레거시 기본적으로 OFF입니다.</span><span class="sxs-lookup"><span data-stu-id="84361-108">hello ability toosearch for existing guest users in hello SharePoint Online (SPO) people picker is OFF by default toomatch legacy behavior.</span></span>

<span data-ttu-id="84361-109">'ShowPeoplePickerSuggestionsForGuestUsers' hello 테 넌 트 및 사이트 모음에서 수준으로 설정 하는 hello를 사용 하 여이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-109">You can enable this feature by using hello setting 'ShowPeoplePickerSuggestionsForGuestUsers' at hello tenant and site collection level.</span></span> <span data-ttu-id="84361-110">Hello 기능을 통해 멤버는 hello 집합 SPOTenant 및 집합 SPOSite cmdlet을 사용 하 여 설정할 수 있습니다 toosearch hello 디렉터리의 모든 기존 게스트 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="84361-110">You can set hello feature using hello Set-SPOTenant and Set-SPOSite cmdlets, which allow members toosearch all existing guest users in hello directory.</span></span> <span data-ttu-id="84361-111">Hello 테 넌 트 범위에 대 한 변경 내용을 이미 프로 비전 된 SPO 사이트 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-111">Changes in hello tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="84361-112">디렉터리에 대한 초대가 사용하도록 설정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="84361-113">Tooinvite 사용자 사용 권한 않았는지, 표시 되 면 사용자 계정이 사용자 설정에서 외부 사용자가 권한 있는 tooinvite 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="84361-113">If you are notified that you do not have permissions tooinvite users, verify that your user account is authorized tooinvite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="84361-114">이러한 설정을 수정 하거나 할당 된 hello 게스트 초대자 역할 tooa 사용자 최근에, 될 15 ~ 60 분 정도 지연 hello 변경 내용을 적용 하려면.</span><span class="sxs-lookup"><span data-stu-id="84361-114">If you have recently modified these settings or assigned hello Guest Inviter role tooa user, there might be a 15-60 minute delay before hello changes take effect.</span></span>

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="84361-115">있습니까 초대 hello 사용자 상환 하는 동안 오류가 발생 하는</span><span class="sxs-lookup"><span data-stu-id="84361-115">hello user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="84361-116">일반적인 오류는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="84361-117">초대 대상자의 관리자가 테넌트에 EmailVerified 사용자를 만들지 못하도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="84361-118">때 사용자가 해당 조직에 Azure Active Directory를 사용 하는 있지만 특정 사용자의 계정이 있는 hello 초대 존재 하지 않는 (예를 들어 hello 사용자가 없습니다 Azure AD contoso.com에서).</span><span class="sxs-lookup"><span data-stu-id="84361-118">When inviting users whose organization is using Azure Active Directory, but where hello specific user’s account does not exist (for example, hello user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="84361-119">contoso.com의 관리자에 게 사용자가 만들어지지 않도록 방지 하는 위치에는 정책이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-119">hello administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="84361-120">외부 사용자가 있는 경우 hello 사용자 자신의 관리자 toodetermine와 대조해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84361-120">hello user must check with their admin toodetermine if external users are allowed.</span></span> <span data-ttu-id="84361-121">hello 외부 사용자의 관리자 해야 tooallow가 도메인에서 사용자 전자 메일 확인 (이 [문서](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) 전자 메일 확인 사용자가에).</span><span class="sxs-lookup"><span data-stu-id="84361-121">hello external user’s admin may need tooallow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="84361-122">외부 사용자가 이미 페더레이션된 도메인에 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="84361-123">페더레이션 인증을 사용 하는 Azure Active Directory에 hello 사용자가 아직 없는 경우 hello 사용자를 초대할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-123">If you are using federation authentication and hello user does not already exist in Azure Active Directory, hello user cannot be invited.</span></span>

<span data-ttu-id="84361-124">이 문제를 hello tooresolve 외부 사용자의 관리자 계정 tooAzure hello 사용자의 Active Directory를 동기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84361-124">tooresolve this issue, hello external user’s admin must synchronize hello user’s account tooAzure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="84361-125">일반적으로 잘못된 문자인 ‘\#’은 Azure AD와 어떻게 동기화됩니까?</span><span class="sxs-lookup"><span data-stu-id="84361-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="84361-126">"\#" Azure AD B2B 공동 작업 또는 외부 사용자에 대 한 Upn에 예약된 된 문자 이므로 hello 초대 계정 user@contoso.com user_contoso.com# 되EXT@fabrikam.onmicrosoft.com합니다. 따라서 \# 에서 온-프레미스에서 오는 Upn에에서 사용할 수 없습니다 toosign toohello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="84361-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because hello invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com. Therefore, \# in UPNs coming from on-premises aren't allowed toosign in toohello Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a><span data-ttu-id="84361-127">그룹 동기화 tooa 외부 사용자가 추가 될 때 오류가 나타남</span><span class="sxs-lookup"><span data-stu-id="84361-127">I receive an error when adding external users tooa synchronized group</span></span>

<span data-ttu-id="84361-128">"보안" 그룹 및 하지 않은 toogroups 온-프레미스 마스터 또는 너무만 "할당" 외부 사용자가 추가할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="84361-128">External users can be added only too“assigned” or “Security” groups and not toogroups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a><span data-ttu-id="84361-129">외부 사용자 전자 메일 tooredeem 받지</span><span class="sxs-lookup"><span data-stu-id="84361-129">My external user did not receive an email tooredeem</span></span>

<span data-ttu-id="84361-130">hello 초대 대 ISP을 확인 해야 또는 주소 다음 hello 스팸 필터 tooensure ï ´ ù.Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="84361-130">hello invitee should check with their ISP or spam filter tooensure that hello following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="84361-131">Hello 사용자 지정 메시지를 가져오지 않습니다 초대 메시지와 함께 포함 된 시간에 보 니 소개</span><span class="sxs-lookup"><span data-stu-id="84361-131">I notice that hello custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="84361-132">개인 정보 보호와 toocomply, hello 전자 메일 초대에 Api 사용자 지정 메시지 포함 하지 않는 경우:</span><span class="sxs-lookup"><span data-stu-id="84361-132">toocomply with privacy laws, our APIs do not include custom messages in hello email invitation when:</span></span>

- <span data-ttu-id="84361-133">hello 초대자 테 넌 트를 초대 hello에 전자 메일 주소 없습니다</span><span class="sxs-lookup"><span data-stu-id="84361-133">hello inviter doesn’t have an email address in hello inviting tenant</span></span>
- <span data-ttu-id="84361-134">앱 서비스 보안 주체는 hello 초대를 보낼 때</span><span class="sxs-lookup"><span data-stu-id="84361-134">When an appservice principal sends hello invitation</span></span>

<span data-ttu-id="84361-135">이 시나리오에 중요 한 tooyou 이면 우리의 API 초대 메일을 표시 하지 않을 수 있으며 원하는 hello 전자 메일 메커니즘을 통해 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84361-135">If this scenario is important tooyou, you can suppress our API invitation email, and send it through hello email mechanism of your choice.</span></span> <span data-ttu-id="84361-136">또한 개인 정보 보호법 이런 방식이으로 보내는 모든 전자 메일을 준수 하는지 조직의 변호사 toomake를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="84361-136">Consult your organization’s legal counsel toomake sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84361-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="84361-137">Next steps</span></span>

<span data-ttu-id="84361-138">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="84361-138">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="84361-139">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="84361-139">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="84361-140">Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="84361-140">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="84361-141">정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="84361-141">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="84361-142">hello B2B 공동 작업 초대 메일의 hello 요소</span><span class="sxs-lookup"><span data-stu-id="84361-142">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="84361-143">B2B 공동 작업 초대 상환</span><span class="sxs-lookup"><span data-stu-id="84361-143">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="84361-144">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="84361-144">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="84361-145">Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)</span><span class="sxs-lookup"><span data-stu-id="84361-145">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="84361-146">Azure Active Directory B2B 공동 작업 API 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="84361-146">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="84361-147">B2B 공동 작업 사용자에 대한 다단계 인증</span><span class="sxs-lookup"><span data-stu-id="84361-147">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="84361-148">초대 없이 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="84361-148">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="84361-149">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="84361-149">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
