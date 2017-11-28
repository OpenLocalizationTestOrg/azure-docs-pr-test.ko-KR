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
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="e7954-104">암호 관리 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="e7954-104">Password management frequently asked questions</span></span>

<span data-ttu-id="e7954-105">모든 것 관련 toopassword 다시 설정에 대 한 hello 다음은 몇 가지 질문과 대답된 질문 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-105">hello following are some frequently asked questions for all things related toopassword reset.</span></span>

<span data-ttu-id="e7954-106">Azure AD에 대 한 일반적인 질문이 있는 경우 및 셀프 서비스 암호 재설정 응답이 여기는 hello 커뮤니티 지원에 요청 hello [Azure Ad 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask hello community for assistance on hello [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="e7954-107">Hello 커뮤니티 구성원 엔지니어, 제품 관리자, Mvp 및 친구 IT 전문가 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-107">Members of hello community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="e7954-108">이 FAQ는 hello 다음 섹션으로 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-108">This FAQ is split into hello following sections:</span></span>

* [<span data-ttu-id="e7954-109">**암호 재설정 등록에 대한 질문**</span><span class="sxs-lookup"><span data-stu-id="e7954-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="e7954-110">**암호 재설정에 대한 질문**</span><span class="sxs-lookup"><span data-stu-id="e7954-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="e7954-111">**암호 변경에 대한 질문**</span><span class="sxs-lookup"><span data-stu-id="e7954-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="e7954-112">**암호 관리 보고서에 대한 질문**</span><span class="sxs-lookup"><span data-stu-id="e7954-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="e7954-113">**비밀번호 쓰기 저장에 대한 질문**</span><span class="sxs-lookup"><span data-stu-id="e7954-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="e7954-114">암호 재설정 등록</span><span class="sxs-lookup"><span data-stu-id="e7954-114">Password reset registration</span></span>
* <span data-ttu-id="e7954-115">**Q: 내 사용자가 자신의 암호 재설정 데이터를 등록할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="e7954-116">**A:** 예, 암호 재설정이 활성화 되 고 사용이 허가 됩니다, 것 toohello 암호 재설정 등록 포털 http://aka.ms/ssprsetup tooregister에 해당 인증 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go toohello Password Reset Registration portal at http://aka.ms/ssprsetup tooregister their authentication information.</span></span> <span data-ttu-id="e7954-117">Hello 프로필 탭을 클릭 하 고 암호 재설정 옵션에 대 한 hello 레지스터를 클릭 하면 사용자가 http://myapps.microsoft.com, toohello 액세스 패널로 이동 하 여 등록할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-117">Users can also register by going toohello access panel at http://myapps.microsoft.com, clicking hello profile tab, and clicking hello Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="e7954-118">**Q: 내 사용자 대신 암호 재설정 데이터를 정의할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="e7954-119">**A:** 예, 이렇게 하려면 Azure AD Connect PowerShell hello로 [Azure 포털](https://portal.azure.com), 또는 hello Office 관리 포털.</span><span class="sxs-lookup"><span data-stu-id="e7954-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, hello [Azure portal](https://portal.azure.com), or hello Office Admin portal.</span></span> <span data-ttu-id="e7954-120">자세한 내용은 hello 문서 참조 [Azure AD 셀프 서비스 암호 재설정 사용 되는 데이터](active-directory-passwords-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-120">For more information, see hello article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="e7954-121">**Q: 온-프레미스에서 보안 질문에 대한 데이터를 동기화 할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="e7954-122">**A:** 현재 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="e7954-123">**Q: 내 사용자가 다른 사용자가 이 데이터를 볼 수 없는 방식으로 데이터를 등록할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="e7954-124">**A:** 예, 사용자 에게만 전역 관리자 및 hello 사용자가 표시 되는 개인 인증 필드에 암호 재설정 등록 포털로 저장 된 hello를 사용 하 여 데이터를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-124">**A:** Yes, when users register data using hello Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and hello user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="e7954-125">경우는 **Azure 관리자 계정** hello 휴대폰 필드에 채워집니다도 표시 되 고 인증 전화 번호를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into hello mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="e7954-126">**Q: 내 사용자가 암호 재설정을 사용 하기 전에 등록 toobe를 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-126">**Q:  Do my users have toobe registered before they can use password reset?**</span></span>

  > <span data-ttu-id="e7954-127">**A:** 아니요, 대신에 충분 한 인증 정보를 정의 하면 사용자가 없는 tooregister 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-127">**A:** No, if you define enough authentication information on their behalf, users do not have tooregister.</span></span> <span data-ttu-id="e7954-128">암호 재설정이 작동 하는 상태로 제대로 hello hello 디렉터리에 적절 한 필드에 저장 된 데이터의 서식을 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-128">Password reset works as long as you have properly formatted data stored in hello appropriate fields in hello directory.</span></span>
  >
  >
* <span data-ttu-id="e7954-129">**Q: 동기화 하거나 내 사용자를 대신 하 여 hello 인증 전화, 인증 전자 메일 또는 대체 인증 전화 필드를 설정 합니다. 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-129">**Q:  Can I synchronize or set hello Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="e7954-130">**A:** 현재 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="e7954-131">**Q: 어떻게는 hello 등록 포털 알 수 있는 옵션 tooshow 내 사용자가?**</span><span class="sxs-lookup"><span data-stu-id="e7954-131">**Q:  How does hello registration portal know which options tooshow my users?**</span></span>

  > <span data-ttu-id="e7954-132">**A:** hello 암호 재설정 등록 포털에서는 사용자에 대해 설정한 옵션 hello만 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-132">**A:** hello password reset registration portal only shows hello options that you have enabled for your users.</span></span> <span data-ttu-id="e7954-133">이러한 옵션은 디렉터리의 구성 탭의 사용자 암호 재설정 정책 섹션 hello 있습니다. 예를 들어,이 보안 질문을 사용 하지 않도록 하는 경우 다음 사용자가 없으면 수 tooregister 해당 옵션에 대 한 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-133">These options are found under hello User Password Reset Policy section of your directory’s Configure tab. For example, this means that if you do not enable security questions, then users are not able tooregister for that option.</span></span>
  >
  >
* <span data-ttu-id="e7954-134">**Q: 사용자가 등록된 것으로 간주되는 경우는 언제입니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-134">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="e7954-135">**A:** 등록 한 경우 SSPR에 등록 된 것으로 간주 이상 hello **메서드 필요한 tooreset 수가** hello에 설정 된 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-135">**A:** A user is considered registered for SSPR when they have registered at least hello **Number of methods required tooreset** that you have set in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="e7954-136">암호 재설정</span><span class="sxs-lookup"><span data-stu-id="e7954-136">Password reset</span></span>
* <span data-ttu-id="e7954-137">**Q:는 전자 메일, SMS 또는 전화 통화 암호 재설정에서 tooreceive를 대기 해야는 시간**</span><span class="sxs-lookup"><span data-stu-id="e7954-137">**Q:  How long should I wait tooreceive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="e7954-138">**A:** 전자 메일, SMS 메시지가 고 전화 통화 5-20 초 동안 hello 일반적인 경우와 1 분 미만에 도착 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-138">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with hello normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="e7954-139">이 시간 내에 hello 알림을 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-139">If you do not receive hello notification in this time frame:</span></span>
        > * <span data-ttu-id="e7954-140">정크 메일 폴더를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-140">Check your junk folder.</span></span>
        > * <span data-ttu-id="e7954-141">Hello 수 확인 또는 연결할 수 없거나 전자 메일은 hello 예상 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-141">Check hello number or email being contacted is hello one you expect.</span></span>
        > * <span data-ttu-id="e7954-142">Hello 디렉터리의 hello 인증 데이터 형식이 올바로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-142">Check hello authentication data in hello directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="e7954-143">예: "+1 4255551234" 또는 "user@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="e7954-143">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="e7954-144">**Q: 암호 재설정에서 지원되는 언어는 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-144">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="e7954-145">**A:** 암호 재설정 UI, SMS 메시지 및 음성 hello 호출 hello로 지역화 된 Office 365에서 지원 되는 동일한 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-145">**A:** hello password reset UI, SMS messages, and voice calls are localized in hello same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="e7954-146">**Q: 조직 내 디렉터리에 대 한 브랜딩 설정 하는 경우 hello 암호 재설정 환경의 어떤 부분 브랜드 가져오기의 구성 탭?**</span><span class="sxs-lookup"><span data-stu-id="e7954-146">**Q:  What parts of hello password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="e7954-147">**A:** hello 암호 재설정 포털에서 조직 로고를 보여주며 tooconfigure hello 연락처 관리자 링크 toopoint tooa 사용자 지정 메일 또는 URL 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-147">**A:** hello password reset portal shows your organizational logo and allows you tooconfigure hello Contact your administrator link toopoint tooa custom email or URL.</span></span> <span data-ttu-id="e7954-148">암호 재설정에서 보내는 전자 메일 hello 전자 메일의 hello 본문에 조직 로고, 색상, 이름이 포함 및 이름에서 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-148">Any email that gets sent by password reset includes your organization’s logo, colors, name in hello body of hello email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="e7954-149">**Q: 어떻게 수 합니까 내 사용자에 게 교육 where toogo tooreset 암호?**</span><span class="sxs-lookup"><span data-stu-id="e7954-149">**Q:  How can I educate my users about where toogo tooreset their passwords?**</span></span>

  > <span data-ttu-id="e7954-150">**A:** 사용자 toohttps://passwordreset.microsoftonline.com를 직접 보내거나 tooclick hello 지시할 수 **계정 링크에 액세스할 수 없습니다** 페이지에 있는 모든 회사 또는 학교에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-150">**A:** You can send your users toohttps://passwordreset.microsoftonline.com directly, or you can instruct them tooclick hello **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="e7954-151">전체 tooyour 쉽게 액세스할 수 있는 사용자가 이러한 링크를 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-151">You can also publish these links in a place easily accessible tooyour users.</span></span>
  >
  >
* <span data-ttu-id="e7954-152">**Q: 모바일 장치에서 이 페이지를 사용할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-152">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="e7954-153">**A:** 예, 이 페이지는 모바일 장치에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-153">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="e7954-154">**Q: 사용자가 암호를 재설정할 때 로컬 활성 디렉터리 계정 잠금해제를 지원합니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-154">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="e7954-155">**A:** 예, 사용자가 자신의 암호를 재설정하고 Azure AD Connect를 사용하여 비밀번호 쓰기 저장을 배포한 경우 암호를 재설정할 때 해당 사용자의 계정은 자동으로 잠금이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-155">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="e7954-156">**Q: 암호 재설정을 내 사용자의 데스크톱 로그인 환경으로 직접 통합하려면 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-156">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="e7954-157">**A:** Azure AD Premium 고객 인 경우 추가 비용 없이 Microsoft Identity Manager를 설치 하 고 hello 온-프레미스 암호 다시 설정 솔루션 toomeet이 요구이 사항을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-157">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy hello on-premises password reset solution toomeet this requirement.</span></span>
  >
  >
* <span data-ttu-id="e7954-158">**Q: 서로 다른 로캘로 다른 보안 질문을 설정할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-158">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="e7954-159">**A:** 현재 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-159">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="e7954-160">**Q: 몇 개의 질문 hello 보안 질문 인증 옵션에 대해 구성할 수 있습니다?**</span><span class="sxs-lookup"><span data-stu-id="e7954-160">**Q:  How many questions can we configure for hello Security Questions authentication option?**</span></span>

  > <span data-ttu-id="e7954-161">**A:** hello에 too20 사용자 지정 보안 질문을 구성할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-161">**A:** You can configure up too20 custom security questions in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="e7954-162">**Q: 질문의 길이는 어떻게 설정할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-162">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="e7954-163">**A:** 보안 질문은 3자에서 200자 사이일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-163">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="e7954-164">**Q: 얼마나 답변 toosecurity 질문 수? 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="e7954-164">**Q:  How long may answers toosecurity questions be?**</span></span>

  > <span data-ttu-id="e7954-165">**A:** 대답이 3 too40 자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-165">**A:** Answers may be 3 too40 characters long.</span></span>
  >
  >
* <span data-ttu-id="e7954-166">**Q: 중복 된 답변 toosecurity 질문 거부?**</span><span class="sxs-lookup"><span data-stu-id="e7954-166">**Q:  Are duplicate answers toosecurity questions rejected?**</span></span>

  > <span data-ttu-id="e7954-167">**A:** 예, 중복 된 답변 toosecurity 질문 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-167">**A:** Yes, we reject duplicate answers toosecurity questions.</span></span>
  >
  >
* <span data-ttu-id="e7954-168">**Q: 월 사용자 레지스터 hello 동일한 보안 질문에 두 번 이상?**</span><span class="sxs-lookup"><span data-stu-id="e7954-168">**Q:  May a user register hello same security question more than once?**</span></span>

  > <span data-ttu-id="e7954-169">**A:** 아니요, 사용자가 특정 질문을 등록하면 해당 질문을 두 번 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-169">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="e7954-170">**Q: 가능한 tooset 등록 및 재설정에 대 한 보안 질문의 최소 제한을 입니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-170">**Q:  Is it possible tooset a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="e7954-171">**A:** 예, 등록에 대해 하나의 제한, 재설정에 대해 또 하나의 제한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-171">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="e7954-172">3-5개의 보안 질문을 등록해야 하며 3-5개 질문은 재설정을 위해 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-172">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="e7954-173">**Q: 사용자가 질문 필요한 tooreset hello 최대 개수 보다 많은 등록 경우 보안 질문 선택 방법을 재설정 하는 동안?**</span><span class="sxs-lookup"><span data-stu-id="e7954-173">**Q:  If a user has registered more than hello maximum number of questions required tooreset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="e7954-174">**A:** N 보안 질문은 hello 총 사용자 질문 수 중 임의로 선택 하기 위해 등록, 여기서 N은 hello **질문 필요한 tooreset 수가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-174">**A:** N security questions are selected at random out of hello total number of questions a user has registered for, where N is hello **Number of questions required tooreset**.</span></span> <span data-ttu-id="e7954-175">예를 들어 사용자에 게 5 개의 보안 질문을 등록 하는 경우 3 개만 필요 tooreset는 hello 5의 3 임의로 선택 되어 표시 됩니다 다시 설정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-175">For example, if a user has 5 security questions registered, but only 3 are required tooreset, 3 of hello 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="e7954-176">Hello 사용자 가져오는 hello 답변 toohello 질문 잘못 된 경우 hello 선택 프로세스 tooprevent 질문 공세 다시 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-176">If hello user gets hello answers toohello questions wrong, hello selection process reoccurs tooprevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="e7954-177">**Q: 사용자가 짧은 기간 내에 여러 번 암호 재설정을 시도하지 못합니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-177">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="e7954-178">**A:** 예, 잘못 사용 되지 않도록에서 암호 재설정 tooprotect에 기본 제공 보안 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-178">**A:** Yes, there are security features built into password reset tooprotect from misuse.</span></span> <span data-ttu-id="e7954-179">사용자가 24시간 동안 잠그기 전에 한 시간 내에 5번만 암호 재설정을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-179">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="e7954-180">사용자가 toovalidate 전화 번호를 24 시간 동안 계정이 잠깁니다 하기 전에 1 시간 내에 5 번 시도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-180">Users may only try toovalidate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="e7954-181">사용자가 24시간 동안 잠그기 전에 한 시간 내에 5번만 단일 인증 방법을 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-181">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="e7954-182">**Q:는 얼마나 hello 전자 메일 및 SMS 일회용 암호가 유효?**</span><span class="sxs-lookup"><span data-stu-id="e7954-182">**Q:  For how long are hello email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="e7954-183">**A:** hello 되 암호 재설정을 위해 세션 수명은 105 분입니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-183">**A:** hello session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="e7954-184">암호 재설정 작업 hello hello부터에서, hello 사용자에 게 자신의 암호 105 분 tooreset 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-184">From hello beginning of hello password reset operation, hello user has 105 minutes tooreset their password.</span></span> <span data-ttu-id="e7954-185">hello 전자 메일 및 SMS 일회용 암호가 유효 하지 않습니다이 기간이 만료 된 후.</span><span class="sxs-lookup"><span data-stu-id="e7954-185">hello email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="e7954-186">암호 변경</span><span class="sxs-lookup"><span data-stu-id="e7954-186">Password change</span></span>
* <span data-ttu-id="e7954-187">**Q: 해야 사용자가 어디에 toochange 암호 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-187">**Q:  Where should my users go toochange their passwords?**</span></span>

  > <span data-ttu-id="e7954-188">**A:** 사용자가 자신의 암호를 변경할 수 자신의 프로필 사진 또는 아이콘 참조 위치 (hello의 오른쪽 상단 모서리에서와 같이 해당 [Office 365](https://portal.office.com) 또는 [액세스 패널](https://myapps.microsoft.com) 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-188">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in hello upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="e7954-189">Hello에서 사용자가 자신의 암호를 변경할 수 [액세스 패널 프로필 페이지](https://account.activedirectory.windowsazure.com/r#/profile)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-189">Users may change their passwords from hello [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="e7954-190">사용자가 수도 있습니다의 암호가 만료 되었다고 경우 toochange hello Azure AD 로그인 화면에 자동으로 해당 암호를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-190">Users may also be asked toochange their passwords automatically at hello Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="e7954-191">마지막으로, 사용자가 toohello를 탐색할 수 있습니다 [Azure AD 암호 변경 포털](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) 직접 암호 toochange 만들려는 경우.</span><span class="sxs-lookup"><span data-stu-id="e7954-191">Finally, users may navigate toohello [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish toochange their passwords.</span></span>
  >
  >
* <span data-ttu-id="e7954-192">**Q: 내 사용자가 알림을 받을 수 hello Office 포털에서에서 자신의 온-프레미스 암호 만료 되 면?**</span><span class="sxs-lookup"><span data-stu-id="e7954-192">**Q:  Can my users be notified in hello Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="e7954-193">**A:** 이것이 가능 오늘 여기 hello 지침에 따라 ad FS를 사용 하는 경우: [adfs 암호 정책 클레임 보내기](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-193">**A:** This is possible today if you are using ADFS by following hello instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="e7954-194">암호 해시 동기화를 사용하는 경우에는 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-194">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="e7954-195">에서는 동기화 온-프레미스에서 암호 정책 때문에 이것이, toopost 만료 알림 toocloud 환경을 불가능 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-195">This is because we do not sync password policies from on-premises, so it is not possible for us toopost expiry notifications toocloud experiences.</span></span> <span data-ttu-id="e7954-196">두 경우 모두 것도 가능 너무[암호를 가진 tooexpire에 대 한 PowerShell을 사용 하 여 사용자에 게 알림](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-196">In either case, it is also possible too[notify users whose passwords are about tooexpire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="e7954-197">암호 관리 보고서</span><span class="sxs-lookup"><span data-stu-id="e7954-197">Password management reports</span></span>
* <span data-ttu-id="e7954-198">**Q: 어떻게 것 시간이를 hello 암호 관리 보고서에 데이터 tooshow?**</span><span class="sxs-lookup"><span data-stu-id="e7954-198">**Q:  How long does it take for data tooshow up on hello password management reports?**</span></span>

  > <span data-ttu-id="e7954-199">**A:** 데이터 5-10 분 내 hello 암호 관리 보고서에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-199">**A:** Data should appear on hello password management reports within 5-10 minutes.</span></span> <span data-ttu-id="e7954-200">이 경우에 따라 tooan 시간 tooappear를 차지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-200">It some instances it may take up tooan hour tooappear.</span></span>
  >
  >
* <span data-ttu-id="e7954-201">**Q: hello 암호 관리 보고서는 어떻게 필터링 할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-201">**Q:  How can I filter hello password management reports?**</span></span>

  > <span data-ttu-id="e7954-202">**A:** hello 작은 돋보기 toohello (오른쪽) hello 열 레이블이 hello 보고서의 hello 위쪽을 클릭 하 여 hello 암호 관리 보고서를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-202">**A:** You can filter hello password management reports by clicking hello small magnifying glass toohello extreme right of hello column labels, near hello top of hello report.</span></span> <span data-ttu-id="e7954-203">Toodo 다양 한 필터링을 원하는 경우 hello 보고서 tooexcel 다운로드 하 고 피벗 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-203">If you want toodo richer filtering, you can download hello report tooexcel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="e7954-204">**Q: 이란 hello 최대 이벤트 수 hello 암호 관리 보고서에 저장 되는 방법**</span><span class="sxs-lookup"><span data-stu-id="e7954-204">**Q: What is hello maximum number of events are stored in hello password management reports?**</span></span>

  > <span data-ttu-id="e7954-205">**A:** too75, 위로 000 암호 재설정 또는 암호 재설정 등록 이벤트 too30 일 백업 스패닝 hello 암호 관리 보고서에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-205">**A:** Up too75,000 password reset or password reset registration events are stored in hello password management reports, spanning back up too30 days.</span></span>  <span data-ttu-id="e7954-206">Tooexpand이 작업 하는 더 많은 이벤트 tooinclude 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-206">We are working tooexpand this number tooinclude more events.</span></span>
  >
  >
* <span data-ttu-id="e7954-207">**Q: 얼마나 다시 어떤 hello 암호 관리 보고서도?**</span><span class="sxs-lookup"><span data-stu-id="e7954-207">**Q:  How far back do hello password management reports go?**</span></span>

  > <span data-ttu-id="e7954-208">**A:** hello 암호 관리 보고서 표시 작업 hello 내 지난 30 일 이내에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-208">**A:** hello password management reports show operations occurring within hello last 30 days.</span></span> <span data-ttu-id="e7954-209">지금은 tooarchive이이 데이터를 유지 해야 하는 경우 hello 보고서를 주기적으로 다운로드할 수 있고 별도 위치에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-209">For now, if you need tooarchive this data, you can download hello reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="e7954-210">**Q: hello 암호 관리 보고서에 표시할 수 있는 행의 최대 수는 없는 입니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-210">**Q:  Is there a maximum number of rows that can appear on hello password management reports?**</span></span>

  > <span data-ttu-id="e7954-211">**A:** 예, 최대 사람들이 75000 행 hello 암호 관리 보고서 중 하나에 나타날 수 있습니다에 표시 되 고 여부 hello UI 또는 다운로드 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-211">**A:** Yes, a maximum of 75,000 rows may appear on either of hello password management reports, whether they are being shown in hello UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="e7954-212">**Q:는 API tooaccess hello 암호 재설정 또는 등록 보고 데이터 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-212">**Q:  Is there an API tooaccess hello password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="e7954-213">**A:** 예, hello 참조 설명서 toolearn 다음 보고 데이터 스트림을 재설정 어떻게 hello 암호에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-213">**A:** Yes, see hello following documentation toolearn how you can access hello password reset reporting data stream.</span></span>  <span data-ttu-id="e7954-214">[Tooaccess 암호 다시 설정 방법 보고 이벤트 프로그래밍 방식으로 알아봅니다](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent)합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-214">[Learn how tooaccess password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="e7954-215">비밀번호 쓰기 저장</span><span class="sxs-lookup"><span data-stu-id="e7954-215">Password writeback</span></span>
* <span data-ttu-id="e7954-216">**Q: 암호 쓰기 저장 hello 백그라운드 어떻게 작동 합니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-216">**Q:  How does password writeback work behind hello scenes?**</span></span>

  > <span data-ttu-id="e7954-217">**A:** 참조 [암호 쓰기 저장의 작동 원리](active-directory-passwords-writeback.md) 에 암호 쓰기 저장 및 데이터 흐름 hello 시스템을 통해 온-프레미스 환경으로 다시 사용 하도록 설정 하면 발생 하는 기능에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-217">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through hello system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="e7954-218">**Q: 암호 쓰기 저장 toowork를 수행 하는 시간  암호 해시 동기화와 같이 동기화 지연이 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-218">**Q:  How long does password writeback take toowork?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="e7954-219">**A:** 비밀번호 쓰기 저장은 인스턴트입니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-219">**A:** Password writeback is instant.</span></span> <span data-ttu-id="e7954-220">암호 해시 동기화와는 근본적으로 다르게 작동하는 동기 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-220">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="e7954-221">암호 쓰기 저장에는 사용자를 암호의 hello 성공에 대 한 실시간 피드백 tooget 다시 설정 또는 변경 작업 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-221">Password writeback allows users tooget real-time feedback about hello success of their password reset or change operation.</span></span> <span data-ttu-id="e7954-222">성공적인 암호 쓰기 저장에 대 한 평균 시간 hello 0.5 초 미만입니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-222">hello average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="e7954-223">**Q: 온-프레미스 계정을 사용하지 않으면 클라우드 계정/액세스에 어떤 영향을 주나요?**</span><span class="sxs-lookup"><span data-stu-id="e7954-223">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="e7954-224">**A:** 온-프레미스 ID를 사용 하지 않도록 설정 하는 경우 클라우드 byt 기본 AAD Connect를 통해 다음 동기화 간격 hello에 i D/액세스도 비활성화 됩니다이 30 분 마다.</span><span class="sxs-lookup"><span data-stu-id="e7954-224">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at hello next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="e7954-225">**Q: 경우 온-프레미스 Active Directory 암호 정책에 따라 내 온-프레미스 계정 메모리가 제한지 않습니다 SSPR 준수이 정책을 hello 암호를 변경 합니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-225">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change hello password?**</span></span>

  > <span data-ttu-id="e7954-226">**A:** 예, SSPR에 의존 하 고 관련 하 여 hello 온-프레미스도 일반적인 AD 도메인 암호 정책을 비롯 한 AD 암호 정책에 정의 된 모든 세분화 된 암호 정책을 대상 tooa 사용자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-226">**A:** Yes, SSPR relies on and abides by hello on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted tooa given user.</span></span>
  >
  >
* <span data-ttu-id="e7954-227">**Q: 비밀번호 쓰기 저장에 대해 어떤 유형의 계정이 작동합니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-227">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="e7954-228">**A:** 페더레이션 및 암호 해시 동기화된 사용자에 대한 비밀번호 쓰기 저장이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-228">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="e7954-229">**Q: 비밀번호 쓰기 저장을 내 도메인 암호 정책에 적용합니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-229">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="e7954-230">**A:** 예, 비밀번호 쓰기 저장을 암호 사용 기간, 기록, 복잡성, 필터 및 로컬 도메인의 암호에 대해 시행할 다른 제한 사항에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-230">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="e7954-231">**Q: 비밀번호 쓰기 저장은 안전합니까?  해킹을 당하지 않는다고 어떻게 확신할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="e7954-231">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="e7954-232">**A:** 예, 비밀번호 쓰기 저장은 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-232">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="e7954-233">hello 4 단계 보안 계층이 대해 자세히 tooread hello 암호 쓰기 저장 서비스에 의해 구현, 체크 아웃 hello [암호 쓰기 저장 보안 모델](active-directory-passwords-writeback.md#password-writeback-security-model) 암호 쓰기 저장의 작동 방식에 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-233">tooread more about hello four layers of security implemented by hello password writeback service, check out hello [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="e7954-234">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e7954-234">Next steps</span></span>

<span data-ttu-id="e7954-235">링크를 따라 hello Azure AD를 사용 하 여 다시 설정 하는 암호에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-235">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="e7954-236">[**빠른 시작**](active-directory-passwords-getting-started.md) - Azure AD 셀프 서비스 암호 관리를 사용하여 운영 시작</span><span class="sxs-lookup"><span data-stu-id="e7954-236">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="e7954-237">[**라이선스**](active-directory-passwords-licensing.md) - Azure AD 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="e7954-237">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="e7954-238">[**데이터** ](active-directory-passwords-data.md) -hello 필요한 데이터를 이해 하 고 암호 관리에 대 한 사용 방법</span><span class="sxs-lookup"><span data-stu-id="e7954-238">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="e7954-239">[**롤아웃** ](active-directory-passwords-best-practices.md) -계획 및 배포 ´ ֿ ´ hello 지침을 사용 하 여 SSPR tooyour 사용자</span><span class="sxs-lookup"><span data-stu-id="e7954-239">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="e7954-240">[**사용자 지정** ](active-directory-passwords-customize.md) -hello SSPR 귀사에 대 한 경험의 hello 모양과 느낌을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7954-240">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="e7954-241">[**보고**](active-directory-passwords-reporting.md) - 사용자가 SSPR 기능에 액세스하는 조건, 시간 및 위치 탐색</span><span class="sxs-lookup"><span data-stu-id="e7954-241">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="e7954-242">[**정책**](active-directory-passwords-policy.md) - Azure AD 암호 정책을 이해하고 설정</span><span class="sxs-lookup"><span data-stu-id="e7954-242">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="e7954-243">[**비밀번호 쓰기 저장**](active-directory-passwords-writeback.md) - 비밀번호 쓰기 저장이 온-프레미스 디렉터리와 함께 작동 하는 원리</span><span class="sxs-lookup"><span data-stu-id="e7954-243">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="e7954-244">[**기술 심층 분석** ](active-directory-passwords-how-it-works.md) -이동 hello 커튼 toounderstand 뒤 작동 방법</span><span class="sxs-lookup"><span data-stu-id="e7954-244">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="e7954-245">[**문제를 해결** ](active-directory-passwords-troubleshoot.md) -SSPR으로 보면 tooresolve 공통을 발급 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="e7954-245">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
