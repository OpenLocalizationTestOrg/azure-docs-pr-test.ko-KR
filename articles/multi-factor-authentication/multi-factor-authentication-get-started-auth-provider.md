---
title: "Azure Multi-Factor Auth 공급자 시작 | Microsoft Docs"
description: "Azure Multi-Factor Auth 공급자를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: ed14a5a762bab20a1ccde699504dd21f25009b52
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a><span data-ttu-id="76185-103">Azure Multi-Factor Auth 공급자 시작</span><span class="sxs-lookup"><span data-stu-id="76185-103">Getting started with an Azure Multi-Factor Auth Provider</span></span>
<span data-ttu-id="76185-104">두 단계 인증은 기본적으로 Azure Active Directory 및 Office 365 사용자가 있는 전역 관리자를 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76185-104">Two-step verification is available by default for global administrators who have Azure Active Directory, and Office 365 users.</span></span> <span data-ttu-id="76185-105">그러나 [고급 기능](multi-factor-authentication-whats-next.md)을 활용하려는 경우 Azure MFA(Multi-Factor Authentication)의 전체 버전을 구입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-105">However, if you wish to take advantage of [advanced features](multi-factor-authentication-whats-next.md) then you should purchase the full version of Azure Multi-Factor Authentication (MFA).</span></span>

<span data-ttu-id="76185-106">Azure Multi-factor Authentication 공급자는 정식 버전의 Azure MFA에서 제공하는 기능을 활용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="76185-106">An Azure Multi-Factor Auth Provider is used to take advantage of features provided by the full version of Azure MFA.</span></span> <span data-ttu-id="76185-107">**Azure MFA, Azure AD Premium 또는 EMS(Enterprise Mobility + Security)를 통해 라이선스를 갖고 있지 않은** 사용자를 위한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="76185-107">It is for users who **do not have licenses through Azure MFA, Azure AD Premium, or Enterprise Mobility + Security (EMS)**.</span></span>  <span data-ttu-id="76185-108">Azure MFA, Azure AD Premium 및 EMS는 기본적으로 Azure MFA의 전체 버전을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-108">Azure MFA, Azure AD Premium, and EMS include the full version of Azure MFA by default.</span></span> <span data-ttu-id="76185-109">라이선스를 보유한 경우 Multi-Factor Auth 공급자가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76185-109">If you have licenses, then you do not need an Azure Multi-Factor Auth Provider.</span></span>

<span data-ttu-id="76185-110">SDK를 다운로드하려면 Azure Multi-Factor Auth 공급자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-110">An Azure Multi-Factor Auth provider is required to download the SDK.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76185-111">SDK를 다운로드하려면 Azure MFA, AAD Premium 또는 EMS 라이선스가 있더라도 Azure Multi-Factor Auth 공급자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-111">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span>  <span data-ttu-id="76185-112">이를 위해 Azure Multi-Factor Auth 공급자를 만들고 이미 라이선스를 보유한 경우 공급자는 반드시 **활성화된 사용자당** 모델을 사용하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-112">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, be sure to create the Provider with the **Per Enabled User** model.</span></span> <span data-ttu-id="76185-113">그런 다음 Azure MFA, Azure AD Premium 또는 EMS 라이선스를 포함하는 디렉터리에 공급자를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-113">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="76185-114">이 구성을 사용하면 사용자가 소유한 라이선스 수보다는 2단계 인증을 수행하는 고유 사용자가 더 많은 경우에만 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="76185-114">This configuration ensures that you are only billed if you have more unique users performing two-step verification than the number of licenses you own.</span></span>

## <a name="what-is-an-azure-multi-factor-auth-provider"></a><span data-ttu-id="76185-115">Azure Multi-Factor Auth 공급자란?</span><span class="sxs-lookup"><span data-stu-id="76185-115">What is an Azure Multi-Factor Auth Provider?</span></span>

<span data-ttu-id="76185-116">Azure Multi-Factor Authentication에 대한 라이선스가 없는 경우 사용자에 대해 2단계 인증을 요구하는 인증 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76185-116">If you don't have licenses for Azure Multi-Factor Authentication, you can create an auth provider to require two-step verification for your users.</span></span> <span data-ttu-id="76185-117">사용자 지정 앱을 개발 중이고 Azure MFA를 사용하도록 설정하려는 경우 인증 공급자를 만들고 [SDK를 다운로드](multi-factor-authentication-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-117">If you are developing a custom app and want to enable Azure MFA, create an auth provider and [download the SDK](multi-factor-authentication-sdk.md).</span></span>

<span data-ttu-id="76185-118">두 가지 유형의 인증 공급자가 있으며 Azure 구독이 청구되는 방식에 따라 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-118">There are two types of auth providers, and the distinction is around how your Azure subscription is charged.</span></span> <span data-ttu-id="76185-119">인증 단위 옵션은 한 달에 테넌트에 대해 수행한 인증 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-119">The per-authentication option calculates the number of authentications performed against your tenant in a month.</span></span> <span data-ttu-id="76185-120">이 옵션은 사용자 지정 응용 프로그램에 대해 MFA를 요구하는 경우처럼 가끔씩만 인증하는 여러 사용자가 있는 경우 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-120">This option is best if you have a number of users authenticating only occasionally, like if you require MFA for a custom application.</span></span> <span data-ttu-id="76185-121">사용자당 옵션은 테넌트에서 한 달 동안 2단계 인증을 수행하는 개인 수를 계산한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76185-121">The per-user option calculates the number of individuals in your tenant who perform two-step verification in a month.</span></span> <span data-ttu-id="76185-122">이 옵션은 라이선스를 갖고 있지만 라이선스 한도를 초과하여 더 많은 사용자까지 MFA를 확장해야 하는 사용자가 있는 경우 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-122">This option is best if you have some users with licenses but need to extend MFA to more users beyond your licensing limits.</span></span>

## <a name="create-a-multi-factor-auth-provider"></a><span data-ttu-id="76185-123">Multi-Factor Auth 공급자 만들기</span><span class="sxs-lookup"><span data-stu-id="76185-123">Create a Multi-Factor Auth Provider</span></span>
<span data-ttu-id="76185-124">다음 단계를 따라 Azure Multi-Factor Auth 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76185-124">Use the following steps to create an Azure Multi-Factor Auth Provider.</span></span> <span data-ttu-id="76185-125">Azure Multi-Factor Auth 공급자는 Azure 클래식 포털에서만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76185-125">Azure Multi-Factor Auth Providers can only be created in the Azure classic portal.</span></span> <span data-ttu-id="76185-126">Azure 클래식 포털에 로그인할 수 없는 경우 Azure AD 테넌트가 [Azure 구독과 연결](../active-directory/active-directory-how-subscriptions-associated-directory.md)되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-126">If you can't sign in to the Azure classic portal, check to make sure that your Azure AD tenant is [associated with an Azure subscription](../active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span> 

1. <span data-ttu-id="76185-127">관리자 권한으로 [Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-127">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="76185-128">왼쪽 창에서 **Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-128">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="76185-129">Active Directory 페이지 위쪽에서 **Multi-Factor Authentication 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-129">On the Active Directory page, at the top, select **Multi-Factor Authentication Providers**.</span></span>
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. <span data-ttu-id="76185-131">아래쪽에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-131">At the bottom, click **New**.</span></span>
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. <span data-ttu-id="76185-133">App Services 아래에서 **Multi-Factor Auth 공급자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-133">Under App Services, select **Multi-Factor Auth Provider**</span></span>
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. <span data-ttu-id="76185-135">**빠른 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-135">Select **Quick Create**.</span></span>
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. <span data-ttu-id="76185-137">다음 필드를 입력하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-137">Fill in the following fields and select **Create**.</span></span>
   1. <span data-ttu-id="76185-138">**이름** – Multi-Factor Auth 공급자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76185-138">**Name** – The name of the Multi-Factor Auth Provider.</span></span>
   2. <span data-ttu-id="76185-139">**사용 모델** – 두 가지 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-139">**Usage Model** – Choose one of two options:</span></span>
      * <span data-ttu-id="76185-140">인증당 - 인증 단위로 요금이 청구되는 구매 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="76185-140">Per Authentication – purchasing model that charges per authentication.</span></span> <span data-ttu-id="76185-141">일반적으로 소비자 지향 응용 프로그램에서 Azure Multi-Factor Authentication을 사용하는 시나리오에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="76185-141">Typically used for scenarios that use Azure Multi-Factor Authentication in a consumer-facing application.</span></span>
      * <span data-ttu-id="76185-142">활성화된 사용자별 – 활성화된 사용자 단위로 요금이 청구되는 구매 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="76185-142">Per Enabled User – purchasing model that charges per enabled user.</span></span> <span data-ttu-id="76185-143">일반적으로 Office 365와 같은 응용 프로그램에 대한 직원 액세스에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-143">Typically used for employee access to applications such as Office 365.</span></span> <span data-ttu-id="76185-144">이미 Azure MFA에 대한 사용이 허가된 사용자가 있는 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-144">Choose this option if you have some users that are already licensed for Azure MFA.</span></span>
   3. <span data-ttu-id="76185-145">**디렉터리** – Multi-Factor Authentication 공급자와 연결된 Azure Active Directory 테넌트입니다.</span><span class="sxs-lookup"><span data-stu-id="76185-145">**Directory** – The Azure Active Directory tenant that the Multi-Factor Authentication Provider is associated with.</span></span> <span data-ttu-id="76185-146">다음에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="76185-146">Be aware of the following:</span></span>
      * <span data-ttu-id="76185-147">Multi-Factor Auth 공급자를 만드는 데 Azure AD 디렉터리가 필요하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76185-147">You do not need an Azure AD directory to create a Multi-Factor Auth Provider.</span></span> <span data-ttu-id="76185-148">Azure Multi-Factor Authentication 서버 또는 SDK를 다운로드만 하려는 경우 이 상자를 비워둡니다.</span><span class="sxs-lookup"><span data-stu-id="76185-148">Leave this box blank if you are only planning to download the Azure Multi-Factor Authentication Server or SDK.</span></span>
      * <span data-ttu-id="76185-149">Multi-Factor Authentication 공급자를 Azure AD 디렉터리와 연결하여 고급 기능을 활용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-149">The Multi-Factor Auth Provider must be associated with an Azure AD directory to take advantage of the advanced features.</span></span>
      * <span data-ttu-id="76185-150">한 Multi-Factor Auth 공급자를 한 Azure AD 디렉터리에만 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76185-150">Only one Multi-Factor Auth Provider can be associated with any one Azure AD directory.</span></span>  
      ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. <span data-ttu-id="76185-152">만들기를 클릭하면 Multi-Factor Authentication 공급자가 생성되고 **Multi-Factor Authentication 공급자를 성공적으로 만들었습니다**라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="76185-152">Once you click create, the Multi-Factor Authentication Provider is created and you should see a message stating: **Successfully created Multi-Factor Authentication Provider**.</span></span> <span data-ttu-id="76185-153">**Ok**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-153">Click **Ok**.</span></span>  
   
   ![MFA 공급자 만들기](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a><span data-ttu-id="76185-155">Multi-Factor Auth 공급자 관리</span><span class="sxs-lookup"><span data-stu-id="76185-155">Manage your Multi-Factor Auth Provider</span></span>

<span data-ttu-id="76185-156">MFA 공급자를 만든 후에는 사용 모델(활성화된 사용자별 또는 인증별)을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76185-156">You cannot change the usage model (per enabled user or per authentication) after an MFA provider is created.</span></span> <span data-ttu-id="76185-157">하지만 MFA 공급자를 삭제하고 다른 사용 모델로 새 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76185-157">However, you can delete the MFA provider and then create one with a different usage model.</span></span>

<span data-ttu-id="76185-158">현재 Multi-Factor Auth 공급자가 Azure AD 디렉터리(Azure AD 테넌트라고도 함)에 연결된 경우 MFA 공급자를 안전하게 삭제하고 동일한 Azure AD 테넌트에 연결된 새 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76185-158">If the current Multi-Factor Auth Provider is associated with an Azure AD directory (also known as an Azure AD tenant), you can safely delete the MFA provider and create one that is linked to the same Azure AD tenant.</span></span> <span data-ttu-id="76185-159">또는 MFA로 설정된 모든 사용자를 처리할 만큼 충분한 MFA, Azure AD Premium 또는 Enterprise Mobility + Security(EMS) 라이선스를 구입한 경우 MFA 공급자를 모두 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76185-159">Alternatively, if you purchased enough MFA, Azure AD Premium, or Enterprise Mobility + Security (EMS) licenses to cover all users that are enabled for MFA, you can delete the MFA provider altogether.</span></span>

<span data-ttu-id="76185-160">하지만 MFA 공급자가 Azure AD 테넌트에 연결되어 있지 않거나 새 MFA 공급자를 다른 Azure AD 테넌트에 연결한 경우 사용자 설정 및 구성 옵션이 전송되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76185-160">If your MFA provider is not linked to an Azure AD tenant, or you link the new MFA provider to a different Azure AD tenant, user settings and configuration options are not transferred.</span></span> <span data-ttu-id="76185-161">또한 새 MFA 공급자를 통해 생성된 활성화 자격 증명을 사용하여 기존 Azure MFA 서버를 다시 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76185-161">Also, existing Azure MFA Servers need to be reactivated using activation credentials generated through the new MFA Provider.</span></span> <span data-ttu-id="76185-162">MFA 서버를 새 MFA 공급자에 연결하기 위해 다시 활성화해도 전화 및 문자 메시지 인증에는 영향을 미치지 않지만 모바일 앱을 다시 활성화할 때까지 모바일 앱 알림이 모든 사용자에 대해 작동 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="76185-162">Reactivating the MFA Servers to link them to the new MFA Provider doesn't impact phone call and text message authentication, but mobile app notifications will stop working for all users until they reactivate the mobile app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76185-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="76185-163">Next steps</span></span>

[<span data-ttu-id="76185-164">Multi-Factor Authentication SDK 다운로드</span><span class="sxs-lookup"><span data-stu-id="76185-164">Download the Multi-Factor Authentication SDK</span></span>](multi-factor-authentication-sdk.md)

[<span data-ttu-id="76185-165">Multi-Factor Authentication 설정 구성</span><span class="sxs-lookup"><span data-stu-id="76185-165">Configure Multi-Factor Authentication settings</span></span>](multi-factor-authentication-whats-next.md)
