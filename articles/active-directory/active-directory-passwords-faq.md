---
title: 'FAQ: Azure AD SSPR | Microsoft Docs'
description: "Azure AD 셀프 서비스 암호 재설정에 대해 자주 묻는 질문과 대답"
services: active-directory
keywords: "Active Directory 암호 관리, 암호 관리, Azure AD 셀프 서비스 암호 재설정"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b3fab99ff9fab5bc67fa70113dc5b06fac775b09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="77667-104">암호 관리 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="77667-104">Password management frequently asked questions</span></span>

<span data-ttu-id="77667-105">다음은 암호 재설정과 관련된 모든 항목에 대한 몇 가지 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="77667-105">The following are some frequently asked questions for all things related to password reset.</span></span>

<span data-ttu-id="77667-106">여기에서 답변되지 않은 Azure AD 및 셀프 서비스 암호 재설정에 대한 일반적인 질문이 있는 경우 커뮤니티 지원에 [Azure AD 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD)을 지원하도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask the community for assistance on the [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="77667-107">커뮤니티 구성원에는 엔지니어, 제품 관리자, MVP 및 동료 IT 전문가가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-107">Members of the community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="77667-108">이 FAQ는 다음 섹션으로 구분하여 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-108">This FAQ is split into the following sections:</span></span>

* [<span data-ttu-id="77667-109">**암호 재설정 등록에 대한 질문**</span><span class="sxs-lookup"><span data-stu-id="77667-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="77667-110">**암호 재설정에 대한 질문**</span><span class="sxs-lookup"><span data-stu-id="77667-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="77667-111">**암호 변경에 대한 질문**</span><span class="sxs-lookup"><span data-stu-id="77667-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="77667-112">**암호 관리 보고서에 대한 질문**</span><span class="sxs-lookup"><span data-stu-id="77667-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="77667-113">**비밀번호 쓰기 저장에 대한 질문**</span><span class="sxs-lookup"><span data-stu-id="77667-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="77667-114">암호 재설정 등록</span><span class="sxs-lookup"><span data-stu-id="77667-114">Password reset registration</span></span>
* <span data-ttu-id="77667-115">**Q: 내 사용자가 자신의 암호 재설정 데이터를 등록할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="77667-116">**A:** 예, 암호 재설정이 사용되고 라이선스가 부여된 경우 http://aka.ms/ssprsetup의 암호 재설정 등록 포털로 이동하여 인증 정보를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go to the Password Reset Registration portal at http://aka.ms/ssprsetup to register their authentication information.</span></span> <span data-ttu-id="77667-117">사용자는 http://myapps.microsoft.com의 액세스 패널로 이동하고, 프로필 탭을 클릭하고 암호 재설정 등록 옵션을 클릭하여 등록할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-117">Users can also register by going to the access panel at http://myapps.microsoft.com, clicking the profile tab, and clicking the Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="77667-118">**Q: 내 사용자 대신 암호 재설정 데이터를 정의할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="77667-119">**A:** 예, Azure AD Connect, PowerShell, [Azure Portal](https://portal.azure.com) 또는 Office 관리자 포털을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, the [Azure portal](https://portal.azure.com), or the Office Admin portal.</span></span> <span data-ttu-id="77667-120">자세한 내용은 [Azure AD 셀프 서비스 암호 재설정에서 사용하는 데이터](active-directory-passwords-data.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77667-120">For more information, see the article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="77667-121">**Q: 온-프레미스에서 보안 질문에 대한 데이터를 동기화 할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="77667-122">**A:** 현재 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="77667-123">**Q: 내 사용자가 다른 사용자가 이 데이터를 볼 수 없는 방식으로 데이터를 등록할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="77667-124">**A:** 예, 사용자가 암호 재설정 등록 포털을 사용하여 데이터를 등록한 경우 전역 관리자 사용자에게만 표시되는 개인 인증 필드로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-124">**A:** Yes, when users register data using the Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and the user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="77667-125">**Azure 관리자 계정**이 해당 인증 전화 번호를 등록하는 경우 휴대폰 필드로 채워지고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into the mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="77667-126">**Q: 내 사용자를 등록해야 암호 재설정을 사용할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-126">**Q:  Do my users have to be registered before they can use password reset?**</span></span>

  > <span data-ttu-id="77667-127">**A:** 아니요, 충분한 인증 정보를 정의한 경우 사용자를 등록하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-127">**A:** No, if you define enough authentication information on their behalf, users do not have to register.</span></span> <span data-ttu-id="77667-128">디렉터리의 적절한 필드에 데이터의 형식이 저장되어 있다면 암호 재설정이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-128">Password reset works as long as you have properly formatted data stored in the appropriate fields in the directory.</span></span>
  >
  >
* <span data-ttu-id="77667-129">**Q: 내 사용자 대신 인증 전화, 인증 전자 메일 인증 또는 대체 인증 전화 필드를 동기화하거나 설정할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-129">**Q:  Can I synchronize or set the Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="77667-130">**A:** 현재 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="77667-131">**Q: 등록 포털이 사용자에게 표시하는 옵션을 어떻게 확인합니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-131">**Q:  How does the registration portal know which options to show my users?**</span></span>

  > <span data-ttu-id="77667-132">**A:** 암호 재설정 등록 포털은 사용자에게 사용하도록 설정된 옵션만을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-132">**A:** The password reset registration portal only shows the options that you have enabled for your users.</span></span> <span data-ttu-id="77667-133">사용자 디렉터리에 있는 [구성] 탭의 [사용자 암호 재설정 정책] 섹션에서 이러한 옵션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-133">These options are found under the User Password Reset Policy section of your directory’s Configure tab.</span></span> <span data-ttu-id="77667-134">예를 들어, 보안 질문을 할 수 없는 경우, 사용자는 해당 옵션에 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-134">For example, this means that if you do not enable security questions, then users are not able to register for that option.</span></span>
  >
  >
* <span data-ttu-id="77667-135">**Q: 사용자가 등록된 것으로 간주되는 경우는 언제입니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-135">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="77667-136">**A:** 사용자가 적어도 [Azure Portal](https://portal.azure.com)에서 설정한 **재설정에 필요한 메서드의 수**를 등록한 경우 SSPR에 등록된 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-136">**A:** A user is considered registered for SSPR when they have registered at least the **Number of methods required to reset** that you have set in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="77667-137">암호 재설정</span><span class="sxs-lookup"><span data-stu-id="77667-137">Password reset</span></span>
* <span data-ttu-id="77667-138">**Q: 암호 재설정에서 전자 메일, SMS 또는 전화 통화를 받으려면 얼마나 오래 대기해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-138">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="77667-139">**A:** 전자 메일, SMS 메시지 및 전화 통화는 1초 미만이며, 일반적인 경우 5-20초 대기해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-139">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with the normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="77667-140">이 시간 내에 알림을 수신하지 않은 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-140">If you do not receive the notification in this time frame:</span></span>
        > * <span data-ttu-id="77667-141">정크 메일 폴더를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-141">Check your junk folder.</span></span>
        > * <span data-ttu-id="77667-142">연락 중인 전자 메일의 수가 예상대로인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-142">Check the number or email being contacted is the one you expect.</span></span>
        > * <span data-ttu-id="77667-143">디렉터리의 인증 데이터 형식이 정확한지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-143">Check the authentication data in the directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="77667-144">예: "+1 4255551234" 또는 "user@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="77667-144">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="77667-145">**Q: 암호 재설정에서 지원되는 언어는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-145">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="77667-146">**A:** 암호 재설정 UI, SMS 메시지 및 음성 통화는 Office 365에서 지원되는 동일한 언어로 지역화됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-146">**A:** The password reset UI, SMS messages, and voice calls are localized in the same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="77667-147">**Q: 내 디렉터리의 구성 탭에서 조직 브랜드를 설정하는 경우 암호 재설정의 어느 부분에서 브랜드를 설정합니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-147">**Q:  What parts of the password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="77667-148">**A:** 암호 재설정 포털은 조직 로고를 표시하며 사용자 지정 전자 메일 또는 URL을 가리키는 관리자에게 문의 링크를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-148">**A:** The password reset portal shows your organizational logo and allows you to configure the Contact your administrator link to point to a custom email or URL.</span></span> <span data-ttu-id="77667-149">암호 재설정에서 보낸 전자 메일에는 조직의 로고, 색, 전자 메일 본문의 이름 및 이름으로 사용자 지정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-149">Any email that gets sent by password reset includes your organization’s logo, colors, name in the body of the email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="77667-150">**Q: 암호 재설정으로 이동할 수 있는 위치에 대해 사용자에게 어떻게 교육할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-150">**Q:  How can I educate my users about where to go to reset their passwords?**</span></span>

  > <span data-ttu-id="77667-151">**A:** 사용자를 https://passwordreset.microsoftonline.com에 직접 보내거나, 모든 회사 또는 학교 ID 로그인 화면에서 찾은 **계정 링크에 액세스할 수 없음**을 클릭하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-151">**A:** You can send your users to https://passwordreset.microsoftonline.com directly, or you can instruct them to click the **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="77667-152">또한 사용자에게 쉽게 액세스할 수 있는 곳에 이러한 링크를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-152">You can also publish these links in a place easily accessible to your users.</span></span>
  >
  >
* <span data-ttu-id="77667-153">**Q: 모바일 장치에서 이 페이지를 사용할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-153">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="77667-154">**A:** 예, 이 페이지는 모바일 장치에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-154">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="77667-155">**Q: 사용자가 암호를 재설정할 때 로컬 활성 디렉터리 계정 잠금해제를 지원합니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-155">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="77667-156">**A:** 예, 사용자가 자신의 암호를 재설정하고 Azure AD Connect를 사용하여 비밀번호 쓰기 저장을 배포한 경우 암호를 재설정할 때 해당 사용자의 계정은 자동으로 잠금이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-156">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="77667-157">**Q: 암호 재설정을 내 사용자의 데스크톱 로그인 환경으로 직접 통합하려면 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-157">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="77667-158">**A:** 사용자가 Azure AD Premium 고객인 경우, 추가 비용 없이 Microsoft Identity Manager를 설치하고 온-프레미스 암호 재설정 솔루션을 배포하여 이 요구 사항을 충족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-158">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution to meet this requirement.</span></span>
  >
  >
* <span data-ttu-id="77667-159">**Q: 서로 다른 로캘로 다른 보안 질문을 설정할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-159">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="77667-160">**A:** 현재 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-160">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="77667-161">**Q: 보안 질문 인증 옵션으로 얼마나 많은 질문을 구성할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-161">**Q:  How many questions can we configure for the Security Questions authentication option?**</span></span>

  > <span data-ttu-id="77667-162">**A:**[Azure Portal](https://portal.azure.com)에서 최대 20개의 사용자 지정 보안 질문을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-162">**A:** You can configure up to 20 custom security questions in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="77667-163">**Q: 질문의 길이는 어떻게 설정할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-163">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="77667-164">**A:** 보안 질문은 3자에서 200자 사이일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-164">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="77667-165">**Q: 보안 질문에 대한 답변의 길이는 어떻게 설정할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-165">**Q:  How long may answers to security questions be?**</span></span>

  > <span data-ttu-id="77667-166">**A:** 답변은 3자에서 40자 사이일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-166">**A:** Answers may be 3 to 40 characters long.</span></span>
  >
  >
* <span data-ttu-id="77667-167">**Q: 보안 질문에 대해 중복 답변은 거부됩니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-167">**Q:  Are duplicate answers to security questions rejected?**</span></span>

  > <span data-ttu-id="77667-168">**A:** 예, 보안 질문에 대한 중복 답변은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-168">**A:** Yes, we reject duplicate answers to security questions.</span></span>
  >
  >
* <span data-ttu-id="77667-169">**Q: 사용자는 동일한 보안 질문을 두 번 이상 등록할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="77667-169">**Q:  May a user register the same security question more than once?**</span></span>

  > <span data-ttu-id="77667-170">**A:** 아니요, 사용자가 특정 질문을 등록하면 해당 질문을 두 번 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-170">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="77667-171">**Q:는 등록을 위한 보안 질문의 최소 제한을 설정할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-171">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="77667-172">**A:** 예, 등록에 대해 하나의 제한, 재설정에 대해 또 하나의 제한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-172">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="77667-173">3-5개의 보안 질문을 등록해야 하며 3-5개 질문은 재설정을 위해 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-173">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="77667-174">**Q: 사용자가 재설정에 필요한 질문의 최대 개수 보다 많은 질문을 등록한 경우, 재설정 중 보안 질문은 어떻게 선택됩니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-174">**Q:  If a user has registered more than the maximum number of questions required to reset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="77667-175">**A:** N개의 보안 질문이 사용자가 등록한 전체 질문 개수에서 임의로 선택되며, 여기서 N은 **재설정에 필요한 질문 개수**입니다.</span><span class="sxs-lookup"><span data-stu-id="77667-175">**A:** N security questions are selected at random out of the total number of questions a user has registered for, where N is the **Number of questions required to reset**.</span></span> <span data-ttu-id="77667-176">예를 들어, 사용자가 5개의 보안 질문을 등록했지만 3개만 재설정에 필요한 경우, 5개 중 3개가 임의로 선택되며 재설정 시 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-176">For example, if a user has 5 security questions registered, but only 3 are required to reset, 3 of the 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="77667-177">사용자가 질문에 대답을 잘못하면, 선택 프로세스가 다시 시작되어 계속되는 질문을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-177">If the user gets the answers to the questions wrong, the selection process reoccurs to prevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="77667-178">**Q: 사용자가 짧은 기간 내에 여러 번 암호 재설정을 시도하지 못합니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-178">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="77667-179">**A:** 예, 암호 재설정을 잘못 사용하지 않도록 기본 제공되는 몇 가지 보안 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-179">**A:** Yes, there are security features built into password reset to protect from misuse.</span></span> <span data-ttu-id="77667-180">사용자가 24시간 동안 잠그기 전에 한 시간 내에 5번만 암호 재설정을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-180">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="77667-181">사용자가 24시간 동안 잠그기 전에 한 시간 내에 5번만 전화 번호의 유효성 검사를 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-181">Users may only try to validate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="77667-182">사용자가 24시간 동안 잠그기 전에 한 시간 내에 5번만 단일 인증 방법을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-182">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="77667-183">**Q: 얼마 동안 전자 메일 및 SMS 일회용 암호가 유효합니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-183">**Q:  For how long are the email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="77667-184">**A:** 암호 재설정을 위한 세션 수명은 105분입니다.</span><span class="sxs-lookup"><span data-stu-id="77667-184">**A:** The session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="77667-185">사용자에게는 암호 재설정 작업 시작부터 해당 암호를 재설정하는 데 105분이 주어집니다.</span><span class="sxs-lookup"><span data-stu-id="77667-185">From the beginning of the password reset operation, the user has 105 minutes to reset their password.</span></span> <span data-ttu-id="77667-186">이 기간이 만료된 후 전자 메일 및 SMS 일회용 암호는 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-186">The email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="77667-187">암호 변경</span><span class="sxs-lookup"><span data-stu-id="77667-187">Password change</span></span>
* <span data-ttu-id="77667-188">**Q: 내 사용자는 어디서 자신의 암호를 변경해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-188">**Q:  Where should my users go to change their passwords?**</span></span>

  > <span data-ttu-id="77667-189">**A:** 사용자는 자신의 [Office 365](https://portal.office.com) 또는 [액세스 패널](https://myapps.microsoft.com) 환경의 오른쪽 위 모서리와 같이 프로필 사진이나 아이콘이 표시된 곳이면 어디서나 자신의 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-189">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in the upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="77667-190">사용자는 [액세스 패널 프로필 페이지](https://account.activedirectory.windowsazure.com/r#/profile)에서 자신의 암호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-190">Users may change their passwords from the [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="77667-191">또한 암호가 만료된 경우 사용자는 Azure AD 로그인 화면에서 자신의 암호를 변경하도록 자동으로 요청받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-191">Users may also be asked to change their passwords automatically at the Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="77667-192">마지막으로 자신의 암호를 변경하려는 경우 사용자는 [Azure AD 암호 변경 포털](https://account.activedirectory.windowsazure.com/ChangePassword.aspx)로 직접 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-192">Finally, users may navigate to the [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish to change their passwords.</span></span>
  >
  >
* <span data-ttu-id="77667-193">**Q: 온-프레미스 암호가 만료되는 경우 Office 포털에서 내 사용자에게 알릴 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-193">**Q:  Can my users be notified in the Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="77667-194">**A:** [ADFS로 암호 정책 클레임 보내기](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396)에 나와 있는 지침에 따라 ADFS를 사용하는 경우 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-194">**A:** This is possible today if you are using ADFS by following the instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="77667-195">암호 해시 동기화를 사용하는 경우에는 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-195">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="77667-196">이는 온-프레미스의 암호 정책을 동기화하지 않기 때문이며, 이에 따라 만료 알림을 클라우드 환경에 게시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-196">This is because we do not sync password policies from on-premises, so it is not possible for us to post expiry notifications to cloud experiences.</span></span> <span data-ttu-id="77667-197">두 경우 모두 [PowerShell을 사용하여 암호가 만료될 사용자에게 알림](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx)(영문)을 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-197">In either case, it is also possible to [notify users whose passwords are about to expire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="77667-198">암호 관리 보고서</span><span class="sxs-lookup"><span data-stu-id="77667-198">Password management reports</span></span>
* <span data-ttu-id="77667-199">**Q: 데이터가 암호 관리 보고서를 표시하는 데 시간이 얼마나 소요됩니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-199">**Q:  How long does it take for data to show up on the password management reports?**</span></span>

  > <span data-ttu-id="77667-200">**A:** 데이터는 5~10분 내에 암호 관리 보고서를 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-200">**A:** Data should appear on the password management reports within 5-10 minutes.</span></span> <span data-ttu-id="77667-201">최대 한 시간이 소요되는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-201">It some instances it may take up to an hour to appear.</span></span>
  >
  >
* <span data-ttu-id="77667-202">**Q: 어떻게 암호 관리 보고서를 필터링할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-202">**Q:  How can I filter the password management reports?**</span></span>

  > <span data-ttu-id="77667-203">**A:** 보고서 위쪽의 열 레이블 맨 오른쪽에 있는 작은 돋보기를 클릭하여 암호 관리 보고서를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-203">**A:** You can filter the password management reports by clicking the small magnifying glass to the extreme right of the column labels, near the top of the report.</span></span> <span data-ttu-id="77667-204">다양한 필터링을 원하는 경우, 보고서를 excel로 다운로드하고 피벗 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-204">If you want to do richer filtering, you can download the report to excel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="77667-205">**Q: 암호 관리 보고서에 저장되는 최대 이벤트 수는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-205">**Q: What is the maximum number of events are stored in the password management reports?**</span></span>

  > <span data-ttu-id="77667-206">**A:** 최대 75,000개의 암호 다시 설정 또는 암호 다시 설정 등록 이벤트가 암호 관리 보고서에 저장되며, 최대 30 일 동안 백업됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-206">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back up to 30 days.</span></span>  <span data-ttu-id="77667-207">이 번호를 확장하여 더 많은 이벤트를 포함하도록 노력하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-207">We are working to expand this number to include more events.</span></span>
  >
  >
* <span data-ttu-id="77667-208">**Q: 암호 관리 보고서는 어디까지 표시할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-208">**Q:  How far back do the password management reports go?**</span></span>

  > <span data-ttu-id="77667-209">**A:** 암호 관리 보고서는 지난 30일 내에 발생한 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-209">**A:** The password management reports show operations occurring within the last 30 days.</span></span> <span data-ttu-id="77667-210">지금까지는, 이 데이터를 보관해야 하는 경우 보고서를 주기적으로 다운로드하여 별도 위치에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-210">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="77667-211">**Q: 암호 관리 보고서에 최대 몇 행을 표시할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-211">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span></span>

  > <span data-ttu-id="77667-212">**A:** 예, UI에 표시되거나 다운로드되는지 여부에 관계 없이 최대 75,000개 행이 암호 관리 보고서에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-212">**A:** Yes, a maximum of 75,000 rows may appear on either of the password management reports, whether they are being shown in the UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="77667-213">**Q: 암호 재설정 또는 등록 보고 데이터에 액세스하는 API가 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-213">**Q:  Is there an API to access the password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="77667-214">**A:** 예, 데이터 스트림을 보고하는 암호 재설정에 액세스하는 방법에 대해 알아보려면 다음 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77667-214">**A:** Yes, see the following documentation to learn how you can access the password reset reporting data stream.</span></span>  <span data-ttu-id="77667-215">[이벤트를 프로그래밍 방식으로 보고하는 암호 재설정에 액세스하는 방법을 알아봅니다](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="77667-215">[Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="77667-216">비밀번호 쓰기 저장</span><span class="sxs-lookup"><span data-stu-id="77667-216">Password writeback</span></span>
* <span data-ttu-id="77667-217">**Q: 비밀번호 쓰기 저장은 배후에서 어떻게 작동합니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-217">**Q:  How does password writeback work behind the scenes?**</span></span>

  > <span data-ttu-id="77667-218">**A:** 비밀번호 쓰기 저장을 사용하는 경우 및 시스템을 통해 온-프레미스 환경으로 다시 데이터가 흐르는 경우에 발생하는 일에 대한 설명은 [비밀번호 쓰기 저장 작동 원리](active-directory-passwords-writeback.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77667-218">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through the system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="77667-219">**Q: 얼마 동안 비밀번호 쓰기 저장이 작동합니까?  암호 해시 동기화와 같이 동기화 지연이 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-219">**Q:  How long does password writeback take to work?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="77667-220">**A:** 비밀번호 쓰기 저장은 인스턴트입니다.</span><span class="sxs-lookup"><span data-stu-id="77667-220">**A:** Password writeback is instant.</span></span> <span data-ttu-id="77667-221">암호 해시 동기화와는 근본적으로 다르게 작동하는 동기 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="77667-221">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="77667-222">비밀번호 쓰기 저장을 사용하면 변경 작업 또는 해당 암호 재설정의 성공 여부에 대한 실시간 피드백을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77667-222">Password writeback allows users to get real-time feedback about the success of their password reset or change operation.</span></span> <span data-ttu-id="77667-223">성공적인 쓰기 저장에 대한 평균 시간은 500밀리초 미만입니다.</span><span class="sxs-lookup"><span data-stu-id="77667-223">The average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="77667-224">**Q: 온-프레미스 계정을 사용하지 않으면 클라우드 계정/액세스에 어떤 영향을 주나요?**</span><span class="sxs-lookup"><span data-stu-id="77667-224">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="77667-225">**A:** 온-프레미스 ID를 사용하지 않는 경우 AAD Connect를 통해 다음 동기화 간격(기본적으로 30분) 시 클라우드 ID/액세스도 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="77667-225">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at the next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="77667-226">**Q: 온-프레미스 계정이 온-프레미스 Active Directory 암호 정책에 의해 제한되는 경우 암호를 변경할 때 SSPR은 이 정책을 준수하나요?**</span><span class="sxs-lookup"><span data-stu-id="77667-226">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change the password?**</span></span>

  > <span data-ttu-id="77667-227">**A:** 예, SSPR은 일반적인 AD 도메인 암호 정책을 비롯한 온-프레미스 AD 암호 정책뿐만 아니라 지정된 사용자를 대상으로 서분화되어 있는 정의된 암호 정책에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="77667-227">**A:** Yes, SSPR relies on and abides by the on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted to a given user.</span></span>
  >
  >
* <span data-ttu-id="77667-228">**Q: 비밀번호 쓰기 저장에 대해 어떤 유형의 계정이 작동합니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-228">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="77667-229">**A:** 페더레이션 및 암호 해시 동기화된 사용자에 대한 비밀번호 쓰기 저장이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-229">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="77667-230">**Q: 비밀번호 쓰기 저장을 내 도메인 암호 정책에 적용합니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-230">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="77667-231">**A:** 예, 비밀번호 쓰기 저장을 암호 사용 기간, 기록, 복잡성, 필터 및 로컬 도메인의 암호에 대해 시행할 다른 제한 사항에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-231">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="77667-232">**Q: 비밀번호 쓰기 저장은 안전합니까?  해킹을 당하지 않는다고 어떻게 확신할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="77667-232">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="77667-233">**A:** 예, 비밀번호 쓰기 저장은 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-233">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="77667-234">비밀번호 쓰기 저장 서비스에서 구현된 4개의 보안 계층 구현에 대한 자세한 내용은 비밀번호 쓰기 저장 작동 원리에서 [비밀번호 쓰기 저장 보안 모델](active-directory-passwords-writeback.md#password-writeback-security-model) 섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-234">To read more about the four layers of security implemented by the password writeback service, check out the [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="77667-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77667-235">Next steps</span></span>

<span data-ttu-id="77667-236">다음 링크는 Azure AD를 사용한 암호 재설정에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="77667-236">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="77667-237">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="77667-237">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="77667-238">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="77667-238">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="77667-239">[**데이터**](active-directory-passwords-data.md) - 암호 관리에 필요한 데이터 및 사용 방식을 이해</span><span class="sxs-lookup"><span data-stu-id="77667-239">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="77667-240">[**롤아웃**](active-directory-passwords-best-practices.md) - 여기서 제공하는 지침을 사용하여 배포 계획을 세우고 사용자에게 SSPR 배포</span><span class="sxs-lookup"><span data-stu-id="77667-240">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="77667-241">[**사용자 지정**](active-directory-passwords-customize.md) - 회사 SSPR 경험의 모양과 느낌을 사용자 지정.</span><span class="sxs-lookup"><span data-stu-id="77667-241">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="77667-242">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="77667-242">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="77667-243">[**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정</span><span class="sxs-lookup"><span data-stu-id="77667-243">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="77667-244">[**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리</span><span class="sxs-lookup"><span data-stu-id="77667-244">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="77667-245">[**기술 심층 분석**](active-directory-passwords-how-it-works.md) - 작동 방식을 이해하기 위해 심층 분석</span><span class="sxs-lookup"><span data-stu-id="77667-245">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="77667-246">[**문제 해결**](active-directory-passwords-troubleshoot.md) - SSPR의 일반적인 문제 해결 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="77667-246">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
