---
title: "Azure Active Directory B2B 공동 작업 API 및 사용자 지정 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업은 비즈니스 파트너가 선택적으로 회사 응용 프로그램에 액세스할 수 있게 함으로써 회사 간 관계를 지원합니다."
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: c85e05b38b4a9525e13ec510a17b7ef4841198d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="f4ffd-103">Azure Active Directory B2B 공동 작업 API 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="f4ffd-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="f4ffd-104">조직에 가장 잘 작동하는 방식으로 초대 프로세스를 사용자 지정하기 원하는 많은 고객이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="f4ffd-105">API를 사용하면 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-105">With our API, you can do just that.</span></span> [<span data-ttu-id="f4ffd-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="f4ffd-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a><span data-ttu-id="f4ffd-107">초대 API의 기능</span><span class="sxs-lookup"><span data-stu-id="f4ffd-107">Capabilities of the invitation API</span></span>
<span data-ttu-id="f4ffd-108">이 API는 다음과 같은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-108">The API offers the following capabilities:</span></span>

1. <span data-ttu-id="f4ffd-109">*어떤* 전자 메일 주소가 있는 내부 사용자도 초대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="f4ffd-110">초대를 수락한 후에 사용자가 리디렉션되려는 위치를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-110">Customize where you want your users to land after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="f4ffd-111">다음과 같이 Microsoft를 통해 표준 초대 메일을 보내려면 선택하고</span><span class="sxs-lookup"><span data-stu-id="f4ffd-111">Choose to send the standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="f4ffd-112">사용자 지정할 수 있는 받는 사람에게 보내려는 메시지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-112">with a message to the recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="f4ffd-113">또한 이 공동 작업자 초대에 대한 정보를 계속 알리려는 사람을 참조:에 추가하도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-113">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="f4ffd-114">또는 Azure AD 통해 알림을 보내지 않도록 선택하여 초대 및 온보딩 워크플로를 완전히 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-114">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="f4ffd-115">이 경우 전자 메일 템플릿, IM 또는 선택한 기타 배포 방법에 포함할 수 있는 API에서 상환 URL을 다시 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-115">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="f4ffd-116">마지막으로 관리자는 사용자를 구성원으로 초대하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-116">Finally, if you are an admin, you can choose to invite the user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="f4ffd-117">인증 모델</span><span class="sxs-lookup"><span data-stu-id="f4ffd-117">Authorization model</span></span>
<span data-ttu-id="f4ffd-118">API는 다음과 같은 인증 모드에서 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-118">The API can be run in the following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="f4ffd-119">앱 + 사용자 모드</span><span class="sxs-lookup"><span data-stu-id="f4ffd-119">App + User mode</span></span>
<span data-ttu-id="f4ffd-120">이 모드에서 API를 사용하는 모든 사용자에게 B2B 초대를 만들기 위한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-120">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="f4ffd-121">앱 전용 모드</span><span class="sxs-lookup"><span data-stu-id="f4ffd-121">App only mode</span></span>
<span data-ttu-id="f4ffd-122">앱 전용 컨텍스트에서 앱은 성공적인 초대를 위해 User.ReadWrite.All 또는 Directory.ReadWrite.All 범위를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-122">In app only context, the app needs the User.ReadWrite.All or Directory.ReadWrite.All scopes for the invitation to succeed.</span></span>

<span data-ttu-id="f4ffd-123">자세한 내용은 https://graph.microsoft.io/docs/authorization/permission_scopes를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="f4ffd-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4ffd-124">PowerShell</span></span>
<span data-ttu-id="f4ffd-125">이제 PowerShell을 사용하여 외부 사용자를 조직에 쉽게 추가하고 초대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-125">It is now possible to use PowerShell to add and invite external users to an organization easily.</span></span> <span data-ttu-id="f4ffd-126">cmdlet을 사용하여 초대 만들기</span><span class="sxs-lookup"><span data-stu-id="f4ffd-126">Create an invitation using the cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="f4ffd-127">다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-127">You can use the following options:</span></span>

* <span data-ttu-id="f4ffd-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="f4ffd-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="f4ffd-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="f4ffd-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="f4ffd-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="f4ffd-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="f4ffd-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="f4ffd-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="f4ffd-132">[https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)에서 초대 API 참조를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ffd-132">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4ffd-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4ffd-133">Next steps</span></span>

<span data-ttu-id="f4ffd-134">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="f4ffd-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="f4ffd-135">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="f4ffd-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="f4ffd-136">Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="f4ffd-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="f4ffd-137">정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="f4ffd-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="f4ffd-138">B2B 공동 작업 초대 전자 메일의 요소</span><span class="sxs-lookup"><span data-stu-id="f4ffd-138">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="f4ffd-139">B2B 공동 작업 초대 상환</span><span class="sxs-lookup"><span data-stu-id="f4ffd-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="f4ffd-140">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="f4ffd-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="f4ffd-141">Azure Active Directory B2B 공동 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f4ffd-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="f4ffd-142">Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)</span><span class="sxs-lookup"><span data-stu-id="f4ffd-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="f4ffd-143">B2B 공동 작업 사용자에 대한 다단계 인증</span><span class="sxs-lookup"><span data-stu-id="f4ffd-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="f4ffd-144">초대 없이 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="f4ffd-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="f4ffd-145">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="f4ffd-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
