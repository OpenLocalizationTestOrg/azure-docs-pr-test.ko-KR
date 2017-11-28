---
title: "aaaGet Azure Multi-factor Auth 공급자를 시작 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure 다단계 인증 공급자입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 00ea967a80b43baff38c1de586c54d95c9abac2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a><span data-ttu-id="098a1-103">Azure Multi-Factor Auth 공급자 시작</span><span class="sxs-lookup"><span data-stu-id="098a1-103">Getting started with an Azure Multi-Factor Auth Provider</span></span>
<span data-ttu-id="098a1-104">두 단계 인증은 기본적으로 Azure Active Directory 및 Office 365 사용자가 있는 전역 관리자를 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-104">Two-step verification is available by default for global administrators who have Azure Active Directory, and Office 365 users.</span></span> <span data-ttu-id="098a1-105">그러나 tootake 활용 하려는 경우 [고급 기능](multi-factor-authentication-whats-next.md) hello 정식 버전의 Azure Multi-factor Authentication (MFA)을 구입 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-105">However, if you wish tootake advantage of [advanced features](multi-factor-authentication-whats-next.md) then you should purchase hello full version of Azure Multi-Factor Authentication (MFA).</span></span>

<span data-ttu-id="098a1-106">Azure Multi-factor Auth 공급자가 사용 됩니다 tootake hello Azure MFA의 전체 버전에서 제공 하는 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-106">An Azure Multi-Factor Auth Provider is used tootake advantage of features provided by hello full version of Azure MFA.</span></span> <span data-ttu-id="098a1-107">**Azure MFA, Azure AD Premium 또는 EMS(Enterprise Mobility + Security)를 통해 라이선스를 갖고 있지 않은** 사용자를 위한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-107">It is for users who **do not have licenses through Azure MFA, Azure AD Premium, or Enterprise Mobility + Security (EMS)**.</span></span>  <span data-ttu-id="098a1-108">Azure MFA, Azure AD Premium 및 EMS hello 정식 버전의 Azure MFA 기본적으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-108">Azure MFA, Azure AD Premium, and EMS include hello full version of Azure MFA by default.</span></span> <span data-ttu-id="098a1-109">라이선스를 보유한 경우 Multi-Factor Auth 공급자가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-109">If you have licenses, then you do not need an Azure Multi-Factor Auth Provider.</span></span>

<span data-ttu-id="098a1-110">Azure Multi-factor Auth 공급자는 필요한 toodownload hello SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-110">An Azure Multi-Factor Auth provider is required toodownload hello SDK.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="098a1-111">toodownload SDK hello Azure MFA, AAD Premium 또는 EMS 라이선스를 보유 하는 경우에 Azure Multi-factor Auth 공급자 toocreate 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-111">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span>  <span data-ttu-id="098a1-112">이 목적을 위해 Azure Multi-factor Auth 공급자를 만들고 이미 라이선스가, 수 hello로 있는지 toocreate hello 공급자 **활성화 된 사용자별** 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-112">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, be sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="098a1-113">그런 다음 연결할 hello Azure MFA, Azure AD Premium 또는 EMS 라이선스를 포함 하는 hello 공급자 toohello 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-113">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="098a1-114">이 구성을 통해만 고유 사용자 수가 hello 소유한 라이선스 개수 보다 2 단계 인증을 수행 하는 경우 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-114">This configuration ensures that you are only billed if you have more unique users performing two-step verification than hello number of licenses you own.</span></span>

## <a name="what-is-an-azure-multi-factor-auth-provider"></a><span data-ttu-id="098a1-115">Azure Multi-Factor Auth 공급자란?</span><span class="sxs-lookup"><span data-stu-id="098a1-115">What is an Azure Multi-Factor Auth Provider?</span></span>

<span data-ttu-id="098a1-116">Azure Multi-factor Authentication에 대 한 라이선스 없다면 사용자에 게는 인증 공급자 toorequire 2 단계 인증을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-116">If you don't have licenses for Azure Multi-Factor Authentication, you can create an auth provider toorequire two-step verification for your users.</span></span> <span data-ttu-id="098a1-117">사용자 지정 앱을 개발 하는 Azure MFA tooenable를 원하는 경우 인증 공급자 만들기 및 [hello SDK 다운로드](multi-factor-authentication-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-117">If you are developing a custom app and want tooenable Azure MFA, create an auth provider and [download hello SDK](multi-factor-authentication-sdk.md).</span></span>

<span data-ttu-id="098a1-118">두 가지 유형의 인증 공급자 있으며 Azure 구독 요금이 부과 됩니다 어떻게 주위 hello 차이.</span><span class="sxs-lookup"><span data-stu-id="098a1-118">There are two types of auth providers, and hello distinction is around how your Azure subscription is charged.</span></span> <span data-ttu-id="098a1-119">hello 인증 단위 옵션 hello 한 달에 테 넌 트에 대해 수행 하는 인증 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-119">hello per-authentication option calculates hello number of authentications performed against your tenant in a month.</span></span> <span data-ttu-id="098a1-120">이 옵션은 사용자 지정 응용 프로그램에 대해 MFA를 요구하는 경우처럼 가끔씩만 인증하는 여러 사용자가 있는 경우 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-120">This option is best if you have a number of users authenticating only occasionally, like if you require MFA for a custom application.</span></span> <span data-ttu-id="098a1-121">hello 사용자별 옵션 한 달에 2 단계 인증을 수행 하는 테 넌 트에 대 한 개인 hello 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-121">hello per-user option calculates hello number of individuals in your tenant who perform two-step verification in a month.</span></span> <span data-ttu-id="098a1-122">일부 사용자 라이선스를 갖고 있는 하지만 프로그램 라이선스 한도 넘어 tooextend MFA toomore 사용자가 할 경우이 옵션이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-122">This option is best if you have some users with licenses but need tooextend MFA toomore users beyond your licensing limits.</span></span>

## <a name="create-a-multi-factor-auth-provider"></a><span data-ttu-id="098a1-123">Multi-Factor Auth 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="098a1-123">Create a Multi-Factor Auth Provider</span></span>
<span data-ttu-id="098a1-124">다음 단계는 Azure Multi-factor Auth 공급자 toocreate hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-124">Use hello following steps toocreate an Azure Multi-Factor Auth Provider.</span></span> <span data-ttu-id="098a1-125">Azure Multi-factor Auth 공급자 hello Azure 클래식 포털에에서만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-125">Azure Multi-Factor Auth Providers can only be created in hello Azure classic portal.</span></span> <span data-ttu-id="098a1-126">Azure AD 테 넌 트 인지 toomake 확인 toohello Azure 클래식 포털에에서 로그인 할 수 없습니다, [Azure 구독과 연결 된](../active-directory/active-directory-how-subscriptions-associated-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-126">If you can't sign in toohello Azure classic portal, check toomake sure that your Azure AD tenant is [associated with an Azure subscription](../active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span> 

1. <span data-ttu-id="098a1-127">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com) 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-127">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="098a1-128">Hello 왼쪽에서 선택 **Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-128">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="098a1-129">Hello 위쪽에, hello Active Directory 페이지에서 선택 **Multi-factor Authentication 공급자**합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-129">On hello Active Directory page, at hello top, select **Multi-Factor Authentication Providers**.</span></span>
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. <span data-ttu-id="098a1-131">Hello 맨 아래에 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-131">At hello bottom, click **New**.</span></span>
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. <span data-ttu-id="098a1-133">App Services 아래에서 **Multi-Factor Auth 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-133">Under App Services, select **Multi-Factor Auth Provider**</span></span>
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. <span data-ttu-id="098a1-135">**빠른 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-135">Select **Quick Create**.</span></span>
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. <span data-ttu-id="098a1-137">Hello 다음 필드를 입력 하 고 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-137">Fill in hello following fields and select **Create**.</span></span>
   1. <span data-ttu-id="098a1-138">**이름** – hello hello Multi-factor Auth 공급자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-138">**Name** – hello name of hello Multi-Factor Auth Provider.</span></span>
   2. <span data-ttu-id="098a1-139">**사용 모델** – 두 가지 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-139">**Usage Model** – Choose one of two options:</span></span>
      * <span data-ttu-id="098a1-140">인증당 - 인증 단위로 요금이 청구되는 구매 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-140">Per Authentication – purchasing model that charges per authentication.</span></span> <span data-ttu-id="098a1-141">일반적으로 소비자 지향 응용 프로그램에서 Azure Multi-Factor Authentication을 사용하는 시나리오에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-141">Typically used for scenarios that use Azure Multi-Factor Authentication in a consumer-facing application.</span></span>
      * <span data-ttu-id="098a1-142">활성화된 사용자별 – 활성화된 사용자 단위로 요금이 청구되는 구매 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-142">Per Enabled User – purchasing model that charges per enabled user.</span></span> <span data-ttu-id="098a1-143">Office 365와 같은 액세스 tooapplications 직원에 대 한 일반적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-143">Typically used for employee access tooapplications such as Office 365.</span></span> <span data-ttu-id="098a1-144">이미 Azure MFA에 대한 사용이 허가된 사용자가 있는 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-144">Choose this option if you have some users that are already licensed for Azure MFA.</span></span>
   3. <span data-ttu-id="098a1-145">**디렉터리** – hello Azure Active Directory에 Multi-factor Authentication 공급자가 연결 된 해당 hello 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-145">**Directory** – hello Azure Active Directory tenant that hello Multi-Factor Authentication Provider is associated with.</span></span> <span data-ttu-id="098a1-146">Hello 다음에 유의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-146">Be aware of hello following:</span></span>
      * <span data-ttu-id="098a1-147">Azure AD 디렉터리 toocreate Multi-factor Auth 공급자를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-147">You do not need an Azure AD directory toocreate a Multi-Factor Auth Provider.</span></span> <span data-ttu-id="098a1-148">이 상자 toodownload hello Azure Multi-factor Authentication 서버 또는 SDK만 계획이 있는 경우 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-148">Leave this box blank if you are only planning toodownload hello Azure Multi-Factor Authentication Server or SDK.</span></span>
      * <span data-ttu-id="098a1-149">hello Multi-factor Auth 공급자는 Azure AD 디렉터리 tootake 활용 고급 기능 hello와 연결 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-149">hello Multi-Factor Auth Provider must be associated with an Azure AD directory tootake advantage of hello advanced features.</span></span>
      * <span data-ttu-id="098a1-150">한 Multi-Factor Auth 공급자를 한 Azure AD 디렉터리에만 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-150">Only one Multi-Factor Auth Provider can be associated with any one Azure AD directory.</span></span>  
      ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. <span data-ttu-id="098a1-152">클릭 하면 만들기, Multi-factor Authentication 공급자가 생성 하는 hello 및 수 없다는 메시지가 표시 됩니다: **다단계 인증 공급자를 만들었습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-152">Once you click create, hello Multi-Factor Authentication Provider is created and you should see a message stating: **Successfully created Multi-Factor Authentication Provider**.</span></span> <span data-ttu-id="098a1-153">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-153">Click **Ok**.</span></span>  
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a><span data-ttu-id="098a1-155">Multi-Factor Auth 공급자 관리</span><span class="sxs-lookup"><span data-stu-id="098a1-155">Manage your Multi-Factor Auth Provider</span></span>

<span data-ttu-id="098a1-156">Hello 사용법을 변경할 수 없습니다 (활성화 된 사용자별 또는 인증 단위)는 MFA 공급자를 만든 후 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-156">You cannot change hello usage model (per enabled user or per authentication) after an MFA provider is created.</span></span> <span data-ttu-id="098a1-157">그러나 hello MFA 공급자를 삭제 하 고에 다른 사용 모델 하나를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-157">However, you can delete hello MFA provider and then create one with a different usage model.</span></span>

<span data-ttu-id="098a1-158">Hello 현재 Multi-factor Auth 공급자와 연결 된 경우 Azure AD 디렉터리 (Azure AD 테 넌 라고도 함)와 안전 하 게 hello MFA 공급자를 삭제 고 만들 수 있습니다 연결된 toohello 동일한 Azure AD 테 넌 트 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-158">If hello current Multi-Factor Auth Provider is associated with an Azure AD directory (also known as an Azure AD tenant), you can safely delete hello MFA provider and create one that is linked toohello same Azure AD tenant.</span></span> <span data-ttu-id="098a1-159">또는 모든 사용자가 MFA에 대해 사용할 수 있는 충분 한 MFA, Azure AD Premium 또는 Enterprise Mobility + 보안 (EMS) 라이선스 toocover를 구입, hello MFA 공급자를 완전히 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-159">Alternatively, if you purchased enough MFA, Azure AD Premium, or Enterprise Mobility + Security (EMS) licenses toocover all users that are enabled for MFA, you can delete hello MFA provider altogether.</span></span>

<span data-ttu-id="098a1-160">MFA 공급자, 연결 된 tooan Azure AD 테 넌 트 아니거나 hello 새 MFA 공급자 tooa 다른 Azure AD 테 넌 트를 연결 하면 사용자 설정 및 구성 옵션 전송 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-160">If your MFA provider is not linked tooan Azure AD tenant, or you link hello new MFA provider tooa different Azure AD tenant, user settings and configuration options are not transferred.</span></span> <span data-ttu-id="098a1-161">또한 Azure MFA 서버를 기존 필요를 통해 생성 되는 정품 인증 자격 증명을 사용 하 여 다시 활성화 toobe hello 새 MFA 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-161">Also, existing Azure MFA Servers need toobe reactivated using activation credentials generated through hello new MFA Provider.</span></span> <span data-ttu-id="098a1-162">MFA 서버 toolink hello를 다시 활성화 하 toohello 새 MFA 공급자에 영향을 주지 전화 통화 및 문자 메시지 인증 하지만 모바일 앱 알림을 hello 모바일 앱을 다시 활성화 될 때까지 모든 사용자에 대해 작동이 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="098a1-162">Reactivating hello MFA Servers toolink them toohello new MFA Provider doesn't impact phone call and text message authentication, but mobile app notifications will stop working for all users until they reactivate hello mobile app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="098a1-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="098a1-163">Next steps</span></span>

[<span data-ttu-id="098a1-164">Hello Multi-factor Authentication SDK 다운로드</span><span class="sxs-lookup"><span data-stu-id="098a1-164">Download hello Multi-Factor Authentication SDK</span></span>](multi-factor-authentication-sdk.md)

[<span data-ttu-id="098a1-165">Multi-Factor Authentication 설정 구성</span><span class="sxs-lookup"><span data-stu-id="098a1-165">Configure Multi-Factor Authentication settings</span></span>](multi-factor-authentication-whats-next.md)
