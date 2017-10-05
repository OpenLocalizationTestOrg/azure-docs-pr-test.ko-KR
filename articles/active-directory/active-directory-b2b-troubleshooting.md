---
title: "Azure Active Directory B2B 공동 작업 문제 해결 | Microsoft Docs"
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
ms.openlocfilehash: 2009cfc956a2703e268c9364996aa2d0fbd8f279
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="e1f19-103">Azure Active Directory B2B 공동 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e1f19-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="e1f19-104">Azure AD(Azure Active Directory) B2B 공동 작업과 관련된 일반적인 문제에 대한 몇 가지 해결책은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a><span data-ttu-id="e1f19-105">외부 사용자를 추가했지만 [전체 주소 목록]이나 사용자 선택에서 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span></span>

<span data-ttu-id="e1f19-106">외부 사용자가 목록에 채워지지 않은 경우 개체를 복제하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="e1f19-107">B2B 게스트 사용자가 SharePoint Online/OneDrive 사용자 선택에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="e1f19-108">SPO(SharePoint Online) 사용자 선택에서 기존 게스트 사용자를 검색하는 기능은 기존 동작과의 일치를 위해 기본적으로 꺼져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-108">The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.</span></span>

<span data-ttu-id="e1f19-109">이 기능은 테넌트 및 사이트 모음 수준에서 설정 'ShowPeoplePickerSuggestionsForGuestUsers'를 통해 이 기능을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-109">You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span></span> <span data-ttu-id="e1f19-110">또한 멤버가 디렉터리에서 모든 기존 게스트 사용자를 검색할 수 있도록 허용하는 Set-SPOTenant 및 Set-SPOSite cmdlet을 사용하여 이 기능을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-110">You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span></span> <span data-ttu-id="e1f19-111">테넌트 범위에 대한 변경 내용은 이미 프로비전된 SPO 사이트에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="e1f19-112">디렉터리에 대한 초대가 사용하도록 설정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="e1f19-113">사용자를 초대할 수 있는 권한이 없다는 알림이 표시되면 사용자 설정에서 사용자 계정이 외부 사용자를 초대할 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-113">If you are notified that you do not have permissions to invite users, verify that your user account is authorized to invite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="e1f19-114">최근에 이러한 설정을 수정했거나 사용자에게 [게스트 초대자] 역할을 할당한 경우 변경 내용이 적용되는 데 15-60분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-114">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span></span>

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="e1f19-115">상환 중에 내가 초대한 사용자에게 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-115">The user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="e1f19-116">일반적인 오류는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="e1f19-117">초대 대상자의 관리자가 테넌트에 EmailVerified 사용자를 만들지 못하도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="e1f19-118">Azure Active Directory를 사용하는 조직의 사용자를 초대하였으나 특정 사용자의 계정이 없는(예: Azure AD contoso.com에 존재하지 않는 사용자) 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-118">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="e1f19-119">contoso.com의 관리자가 정책을 사용하여 사용자를 만들지 못하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-119">The administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="e1f19-120">사용자는 외부 사용자가 허용된 경우인지 해당 관리자에게 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-120">The user must check with their admin to determine if external users are allowed.</span></span> <span data-ttu-id="e1f19-121">외부 사용자의 관리자가 자체 도메인의 전자 메일 확인 사용자를 허용해야 할 수도 있습니다(전자 메일 확인 사용자 허용은 이 [문서](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)를 확인).</span><span class="sxs-lookup"><span data-stu-id="e1f19-121">The external user’s admin may need to allow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="e1f19-122">외부 사용자가 이미 페더레이션된 도메인에 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="e1f19-123">페더레이션 인증을 사용하려고 하며 사용자가 Azure Active Directory에 아직 없는 경우에는 사용자를 초대할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-123">If you are using federation authentication and the user does not already exist in Azure Active Directory, the user cannot be invited.</span></span>

<span data-ttu-id="e1f19-124">이 문제를 해결하려면 외부 사용자의 관리자가 사용자 계정을 Azure Active Directory와 동기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-124">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="e1f19-125">일반적으로 잘못된 문자인 ‘\#’은 Azure AD와 어떻게 동기화됩니까?</span><span class="sxs-lookup"><span data-stu-id="e1f19-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="e1f19-126">초대된 계정 user@contoso.com은 user_contoso.com#EXT@fabrikam.onmicrosoft.com이므로 "\#"은 Azure AD B2B 공동 작업 또는 외부 사용자에 대해 예약된 UPN 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because the invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span></span> <span data-ttu-id="e1f19-127">따라서 온-프레미스에서 가져온 UPN의 \#은 Azure Portal에 로그인할 때 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-127">Therefore, \# in UPNs coming from on-premises aren't allowed to sign in to the Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a><span data-ttu-id="e1f19-128">동기화된 그룹에 외부 사용자를 추가할 때 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-128">I receive an error when adding external users to a synchronized group</span></span>

<span data-ttu-id="e1f19-129">외부 사용자는 "할당된" 그룹 또는 "보안" 그룹에만 추가할 수 있으며 온-프레미스에 마스터된 그룹에는 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a><span data-ttu-id="e1f19-130">외부 사용자가 상환할 전자 메일을 받지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-130">My external user did not receive an email to redeem</span></span>

<span data-ttu-id="e1f19-131">초대 대상자는 ISP 또는 스팸 필터를 확인하여 Invites@microsoft.com 주소가 허용되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="e1f19-132">사용자 지정 메시지가 초대 메시지에 포함되지 않는다는 것을 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-132">I notice that the custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="e1f19-133">개인 정보 보호 법률을 준수하기 위해 다음 경우에 API에는 전자 메일 초대의 사용자 지정 메시지가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when:</span></span>

- <span data-ttu-id="e1f19-134">초대자에게 초대하는 테넌트의 전자 메일 주소가 없는 경우</span><span class="sxs-lookup"><span data-stu-id="e1f19-134">The inviter doesn’t have an email address in the inviting tenant</span></span>
- <span data-ttu-id="e1f19-135">AppService 보안 주체가 초대를 보내는 경우</span><span class="sxs-lookup"><span data-stu-id="e1f19-135">When an appservice principal sends the invitation</span></span>

<span data-ttu-id="e1f19-136">이 시나리오가 중요한 경우 API 초대 전자 메일을 표시하지 않으면서 선택한 전자 메일 메커니즘을 통해 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f19-136">If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice.</span></span> <span data-ttu-id="e1f19-137">조직의 법률 자문에게 문의하여 이러한 방식으로 전송하는 전자 메일이 개인 정보 보호 법률을 준수하는지도 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="e1f19-137">Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1f19-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e1f19-138">Next steps</span></span>

<span data-ttu-id="e1f19-139">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="e1f19-139">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="e1f19-140">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="e1f19-140">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="e1f19-141">Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="e1f19-141">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="e1f19-142">정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="e1f19-142">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="e1f19-143">B2B 공동 작업 초대 전자 메일의 요소</span><span class="sxs-lookup"><span data-stu-id="e1f19-143">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="e1f19-144">B2B 공동 작업 초대 상환</span><span class="sxs-lookup"><span data-stu-id="e1f19-144">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="e1f19-145">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="e1f19-145">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="e1f19-146">Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)</span><span class="sxs-lookup"><span data-stu-id="e1f19-146">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="e1f19-147">Azure Active Directory B2B 공동 작업 API 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="e1f19-147">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="e1f19-148">B2B 공동 작업 사용자에 대한 다단계 인증</span><span class="sxs-lookup"><span data-stu-id="e1f19-148">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="e1f19-149">초대 없이 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="e1f19-149">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="e1f19-150">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="e1f19-150">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
