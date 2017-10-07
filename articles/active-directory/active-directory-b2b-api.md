---
title: "aaaAzure Active Directory B2B 공동 작업 API 및 사용자 지정 | Microsoft Docs"
description: "Azure Active Directory B2B 공동 작업 비즈니스 파트너 tooselectively 액세스 회사 응용 프로그램을 사용 하 여 회사 간 관계 지원"
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
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="ca66b-103">Azure Active Directory B2B 공동 작업 API 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="ca66b-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="ca66b-104">많은 고객 조직에 가장 적합 하는 방식으로 toocustomize hello 초대 프로세스 않겠다고 알려 주십시오 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-104">We've had many customers tell us that they want toocustomize hello invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="ca66b-105">API를 사용하면 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-105">With our API, you can do just that.</span></span> [<span data-ttu-id="ca66b-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="ca66b-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a><span data-ttu-id="ca66b-107">Hello 초대 API의 기능</span><span class="sxs-lookup"><span data-stu-id="ca66b-107">Capabilities of hello invitation API</span></span>
<span data-ttu-id="ca66b-108">hello API hello 다음 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-108">hello API offers hello following capabilities:</span></span>

1. <span data-ttu-id="ca66b-109">*어떤* 전자 메일 주소가 있는 내부 사용자도 초대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="ca66b-110">사용자 지정 위치 사용자 tooland 자신의 초대를 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-110">Customize where you want your users tooland after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="ca66b-111">Us를 통해 toosend hello 표준 초대 메일 선택</span><span class="sxs-lookup"><span data-stu-id="ca66b-111">Choose toosend hello standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="ca66b-112">사용자 지정할 수 있는 메시지 toohello 받는 사람으로</span><span class="sxs-lookup"><span data-stu-id="ca66b-112">with a message toohello recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="ca66b-113">Toocc 선택: tookeep hello에 원하는 사람 사용자 초대이 공동 작업자에 대 한 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-113">And choose toocc: people you want tookeep in hello loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="ca66b-114">또는 Azure AD 통해 하지 toosend 알림을 선택 하 여 초대 및 온 보 딩 워크플로 작업을 완벽 하 게 갖추고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-114">Or completely customize your invitation and onboarding workflow by choosing not toosend notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="ca66b-115">이 경우 얻게 다시 상환 URL hello 전자 메일 템플릿을, 인스턴트 메시지 또는 선택한 다른 배포 방법을에 포함할 수 있는 API에서.</span><span class="sxs-lookup"><span data-stu-id="ca66b-115">In this case, you get back a redemption URL from hello API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="ca66b-116">마지막으로, 관리자 인 경우 멤버로 tooinvite hello 사용자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-116">Finally, if you are an admin, you can choose tooinvite hello user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="ca66b-117">인증 모델</span><span class="sxs-lookup"><span data-stu-id="ca66b-117">Authorization model</span></span>
<span data-ttu-id="ca66b-118">hello API hello 권한 부여 모드를 다음에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-118">hello API can be run in hello following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="ca66b-119">앱 + 사용자 모드</span><span class="sxs-lookup"><span data-stu-id="ca66b-119">App + User mode</span></span>
<span data-ttu-id="ca66b-120">이 모드에서는 API hello 요구를 사용 중인 누구 든 지 toohave hello 권한을 toobe B2B 초대를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-120">In this mode, whoever is using hello API needs toohave hello permissions toobe create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="ca66b-121">앱 전용 모드</span><span class="sxs-lookup"><span data-stu-id="ca66b-121">App only mode</span></span>
<span data-ttu-id="ca66b-122">앱만 컨텍스트에서 hello 앱 초대 toosucceed hello에 대 한 hello User.ReadWrite.All 또는 Directory.ReadWrite.All 범위를 프로비저닝해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-122">In app only context, hello app needs hello User.ReadWrite.All or Directory.ReadWrite.All scopes for hello invitation toosucceed.</span></span>

<span data-ttu-id="ca66b-123">자세한 내용은 https://graph.microsoft.io/docs/authorization/permission_scopes를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca66b-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="ca66b-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca66b-124">PowerShell</span></span>
<span data-ttu-id="ca66b-125">것은 이제 가능한 toouse PowerShell tooadd 및 초대 외부 사용자에 게 tooan 조직 쉽게입니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-125">It is now possible toouse PowerShell tooadd and invite external users tooan organization easily.</span></span> <span data-ttu-id="ca66b-126">Hello cmdlet을 사용 하 여 초대를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-126">Create an invitation using hello cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="ca66b-127">Hello 다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca66b-127">You can use hello following options:</span></span>

* <span data-ttu-id="ca66b-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="ca66b-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="ca66b-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="ca66b-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="ca66b-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="ca66b-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="ca66b-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="ca66b-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="ca66b-132">Hello 초대 API 참조에도 확인할 수 있습니다 [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="ca66b-132">You can also check out hello invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca66b-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ca66b-133">Next steps</span></span>

<span data-ttu-id="ca66b-134">Azure AD B2B 공동 작업에 대한 다른 문서 찾아보기:</span><span class="sxs-lookup"><span data-stu-id="ca66b-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="ca66b-135">Azure AD B2B 공동 작업이란?</span><span class="sxs-lookup"><span data-stu-id="ca66b-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="ca66b-136">Azure Active Directory 관리자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="ca66b-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="ca66b-137">정보 근로자가 B2B 공동 작업 사용자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="ca66b-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="ca66b-138">hello B2B 공동 작업 초대 메일의 hello 요소</span><span class="sxs-lookup"><span data-stu-id="ca66b-138">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="ca66b-139">B2B 공동 작업 초대 상환</span><span class="sxs-lookup"><span data-stu-id="ca66b-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="ca66b-140">Azure AD B2B 공동 작업 라이선스</span><span class="sxs-lookup"><span data-stu-id="ca66b-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="ca66b-141">Azure Active Directory B2B 공동 작업 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ca66b-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="ca66b-142">Azure Active Directory B2B 공동 작업 자주 묻는 질문(FAQ)</span><span class="sxs-lookup"><span data-stu-id="ca66b-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="ca66b-143">B2B 공동 작업 사용자에 대한 다단계 인증</span><span class="sxs-lookup"><span data-stu-id="ca66b-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="ca66b-144">초대 없이 B2B 공동 작업 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="ca66b-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="ca66b-145">Azure Active Directory의 응용 프로그램 관리를 위한 문서 인덱스</span><span class="sxs-lookup"><span data-stu-id="ca66b-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
