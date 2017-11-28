---
title: "Azure에서 Office 365 구독에 대 한 aaaManage hello 디렉터리 | Microsoft Docs"
description: "Azure Active Directory 및 hello Azure 클래식 포털을 사용 하는 Office 365 구독 디렉터리 관리"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a><span data-ttu-id="43522-103">Hello Azure에서 Office 365 구독의 디렉터리 관리</span><span class="sxs-lookup"><span data-stu-id="43522-103">Manage hello directory for your Office 365 subscription in Azure</span></span>
<span data-ttu-id="43522-104">이 문서에서는 설명 방법을 toomanage hello Azure 클래식 포털을 사용 하 여 Office 365 구독에 대해 생성 된 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="43522-104">This article describes how toomanage a directory that was created for an Office 365 subscription, using hello Azure classic portal.</span></span> <span data-ttu-id="43522-105">Hello 서비스 관리자 또는 공동 관리자는 Azure 구독 toosign toohello Azure 클래식 포털에서에서 중 하나 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-105">You must be either hello Service Administrator or a co-administrator of an Azure subscription toosign in toohello Azure classic portal.</span></span> <span data-ttu-id="43522-106">Azure 구독이 없는 경우 지금 [무료 30일 평가판](https://azure.microsoft.com/trial/get-started-active-directory/) 에 등록하면 이 링크를 사용하여 5분 내에 첫 번째 클라우드 솔루션을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43522-106">If you don’t yet have an Azure subscription, you can sign up for a [free 30-day trial](https://azure.microsoft.com/trial/get-started-active-directory/) today and deploy your first cloud solution in under 5 minutes, using this link.</span></span> <span data-ttu-id="43522-107">있는지 toouse hello 작업이 ळ ा ख tooOffice 365에서는 toosign를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-107">Be sure toouse hello work or school account that you use toosign in tooOffice 365.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43522-108">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="43522-109">Hello Azure 구독을 완료 한 후 toohello Azure 클래식 포털에에서 로그인 하 고 Azure 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43522-109">After you complete hello Azure subscription, you can sign in toohello Azure classic portal and access Azure services.</span></span> <span data-ttu-id="43522-110">Hello Active Directory 확장 클릭 toomanage hello Office 365 사용자를 인증 하는 동일한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="43522-110">Click hello Active Directory extension toomanage hello same directory that authenticates your Office 365 users.</span></span>

<span data-ttu-id="43522-111">Azure 구독이 있으면 이미 hello 프로세스 toomanage 추가 디렉터리는 프로세스도 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-111">If you do already have an Azure subscription, hello process toomanage an additional directory is also straightforward.</span></span> <span data-ttu-id="43522-112">예를 들어 Michael Smith는 Contoso.com에 대한 Office 365 구독을 보유하고 있습니다. 그에게는 본인의 Microsoft 계정인 msmith@hotmail.com을 사용하여 등록한 Azure 구독도 있습니다. 이 경우 두 개의 디렉터리를 관리하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43522-112">For example, Michael Smith might have an Office 365 subscription for Contoso.com. He also has an Azure subscription that he signed up for by using his Microsoft account, msmith@hotmail.com. In this case, he manages two directories.</span></span>

| <span data-ttu-id="43522-113">구독</span><span class="sxs-lookup"><span data-stu-id="43522-113">Subscription</span></span> | <span data-ttu-id="43522-114">Office 365</span><span class="sxs-lookup"><span data-stu-id="43522-114">Office 365</span></span> | <span data-ttu-id="43522-115">Azure</span><span class="sxs-lookup"><span data-stu-id="43522-115">Azure</span></span> |
| --- | --- | --- |
|   <span data-ttu-id="43522-116">표시 이름</span><span class="sxs-lookup"><span data-stu-id="43522-116">Display name</span></span> |<span data-ttu-id="43522-117">Contoso</span><span class="sxs-lookup"><span data-stu-id="43522-117">Contoso</span></span> |<span data-ttu-id="43522-118">기본 Azure AD(Azure Active Directory) 디렉터리</span><span class="sxs-lookup"><span data-stu-id="43522-118">Default Azure Active Directory (Azure AD) directory</span></span> |
|   <span data-ttu-id="43522-119">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="43522-119">Domain name</span></span> |<span data-ttu-id="43522-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="43522-120">contoso.com</span></span> |<span data-ttu-id="43522-121">msmithhotmail.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="43522-121">msmithhotmail.onmicrosoft.com</span></span> |

<span data-ttu-id="43522-122">Multi-factor authentication과 같은 Azure AD 기능을 사용할 수 있도록 tooAzure 자신의 Microsoft 계정을 사용 하 여에 로그인 하는 동안 toomanage hello Contoso 디렉터리의 사용자 id를 hello 하고자 했습니다.</span><span class="sxs-lookup"><span data-stu-id="43522-122">He wants toomanage hello user identities in hello Contoso directory while he is signed in tooAzure using his Microsoft account, so that he can enable Azure AD features such as multifactor authentication.</span></span> <span data-ttu-id="43522-123">다음 다이어그램 hello tooillustrate hello 프로세스를 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43522-123">hello following diagram may help tooillustrate hello process.</span></span>

![두 개의 독립적인 디렉터리 toomanage 다이어그램](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

<span data-ttu-id="43522-125">이 경우 hello 두 디렉터리는 서로 독립적입니다.</span><span class="sxs-lookup"><span data-stu-id="43522-125">In this case, hello two directories are independent of each other.</span></span>

## <a name="toomanage-two-independent-directories"></a><span data-ttu-id="43522-126">두 toomanage 독립 디렉터리</span><span class="sxs-lookup"><span data-stu-id="43522-126">toomanage two independent directories</span></span>
<span data-ttu-id="43522-127">순서로 Michael Smith toomanage에 대 한 디렉터리를 모두로 tooAzure에 로그인 하는 동안 msmith@hotmail.com, 그 hello 다음 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-127">In order for Michael Smith toomanage both directories while he is signed in tooAzure as msmith@hotmail.com, he must complete hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="43522-128">이러한 단계는 사용자가 Microsoft 계정으로 로그인한 경우에만 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43522-128">These steps can be completed only when a user is signed in with a Microsoft account.</span></span> <span data-ttu-id="43522-129">Hello 사용자가 회사 또는 학교 계정으로 로그인 하는 경우 hello 옵션 너무**기존 디렉터리를 사용 하 여** 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="43522-129">If hello user is signed in with a work or school account, hello option too**Use existing directory** isn't available.</span></span> <span data-ttu-id="43522-130">홈 디렉터리 (즉, hello 디렉터리 위치 hello 회사 또는 학교 계정의 저장 하 고 해당 hello 업무 또는 학교 소유)에 의해서만 회사 또는 학교 계정을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43522-130">A work or school account can be authenticated only by its home directory (that is, hello directory where hello work or school account is stored, and that hello business or school owns).</span></span>
>
>

1. <span data-ttu-id="43522-131">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) 으로 msmith@hotmail.com합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-131">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as msmith@hotmail.com.</span></span>
2. <span data-ttu-id="43522-132">**새로 만들기** > **App services** > **Active Directory** > **디렉터리** > **사용자 지정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-132">Click **New** > **App services** > **Active Directory** > **Directory** > **Custom Create**.</span></span>
3. <span data-ttu-id="43522-133">기존 디렉터리 및 선택 hello 사용 하 여 클릭 **지금 로그 아웃 준비 toobe 저는** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-133">Click Use existing directory and select hello **I am ready toobe signed out now** checkbox.</span></span>
4. <span data-ttu-id="43522-134">Contoso.onmicrosoft.com의 전역 관리자로 Azure 클래식 포털을 toohello에 로그인 (예를 들어 msmith@contoso.com).</span><span class="sxs-lookup"><span data-stu-id="43522-134">Sign in toohello Azure classic portal as global admin of Contoso.onmicrosoft.com (for example, msmith@contoso.com).</span></span>
5. <span data-ttu-id="43522-135">너무 대화 상자가 나타나면**Azure와 함께 사용 하 여 hello Contoso 디렉터리?**, 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-135">When prompted too**Use hello Contoso directory with Azure?**, click **Continue**.</span></span>
6. <span data-ttu-id="43522-136">**지금 로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-136">Click **Sign out now**.</span></span>
7. <span data-ttu-id="43522-137">로그인으로 Azure 클래식 포털을 toohello msmith@hotmail.com. hello Contoso 디렉터리와 hello 기본 디렉터리 hello Active Directory 확장에에서 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-137">Sign in toohello Azure classic portal as msmith@hotmail.com. hello Contoso directory and hello Default directory appear in hello Active Directory extension.</span></span>

<span data-ttu-id="43522-138">다음이 단계를 완료 한 후 msmith@hotmail.com hello Contoso 디렉터리의 전역 관리자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43522-138">After completing these steps, msmith@hotmail.com is a global administrator in hello Contoso directory.</span></span>

## <a name="tooadminister-resources-as-hello-global-admin"></a><span data-ttu-id="43522-139">전역 관리자 hello와 tooadminister 리소스</span><span class="sxs-lookup"><span data-stu-id="43522-139">tooadminister resources as hello global admin</span></span>
<span data-ttu-id="43522-140">이제 Jane Doe 필요 웹 사이트를 관리 하며 데이터베이스 리소스와 연결 된 Azure 구독에 대 한 hello 한다고 가정해 보겠습니다 msmith@hotmail.com합니다. 이렇게 하려면 그녀 전에 Michael Smith 필요 toocomplete 이러한 단계를 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-140">Now let’s suppose that Jane Doe needs administer websites and database resources that are associated with hello Azure subscription for msmith@hotmail.com. Before she can do that, Michael Smith needs toocomplete these additional steps:</span></span>

1. <span data-ttu-id="43522-141">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) hello Azure 구독에 대 한 hello 서비스 관리자 계정을 사용 하 여 (이 예제에서는 msmith@hotmail.com).</span><span class="sxs-lookup"><span data-stu-id="43522-141">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) using hello Service Administrator account for hello Azure subscription (in this example, msmith@hotmail.com).</span></span>
2. <span data-ttu-id="43522-142">Hello 구독 toohello Contoso 디렉터리 전송: 클릭 **설정** > **구독** > hello 구독 선택 > **디렉터리 편집** > 선택 **Contoso (Contoso.com)**합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-142">Transfer hello subscription toohello Contoso directory: click **Settings** > **Subscriptions** > select hello subscription > **Edit Directory** > select **Contoso (Contoso.com)**.</span></span> <span data-ttu-id="43522-143">Hello 전송, 회사 또는 학교의 일환으로 hello 구독의 공동 관리자 인 계정은 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43522-143">As part of hello transfer, any work or school accounts that are co-administrators of hello subscription are removed.</span></span>
3. <span data-ttu-id="43522-144">Jane Doe hello 구독의 공동 관리자로 추가: 클릭 **설정** > **관리자** > hello 구독 선택 > **추가** > 형식 **JohnDoe@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="43522-144">Add Jane Doe as co-administrator of hello subscription: click **Settings** > **Administrators** > select hello subscription > **Add** > type **JohnDoe@Contoso.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43522-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43522-145">Next steps</span></span>
<span data-ttu-id="43522-146">구독과 디렉터리 간의 hello 관계에 대 한 자세한 내용은 참조 [구독이 디렉터리와 연결 된 방법을](active-directory-how-subscriptions-associated-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="43522-146">For more information about hello relationship between subscriptions and directories, see [How a subscription is associated with a directory](active-directory-how-subscriptions-associated-directory.md).</span></span>
